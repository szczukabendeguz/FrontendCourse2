# Angular Komponens Kommunikáció Jegyzetek

## Előző Óra Összefoglalás: Input/Output Kommunikáció

Az **Input/Output (I/O) módszer** a leggyakoribb és ajánlott komponens kommunikációs forma Angularban. Az A komponens inputot ad a B komponensnek, de nem tudja, hogy azzal mi történik - ez biztosítja a komponensek függetlenségét és újrafelhasználhatóságát.

```typescript
// Szülő → Gyerek kommunikáció
@Input() data: string;
// Gyerek → Szülő kommunikáció  
@Output() notify = new EventEmitter<string>();
```


## ViewChild Decorator

### Mikor használjuk a ViewChild-ot?

A **@ViewChild** decorator lehetővé teszi, hogy a szülő komponens teljes hozzáférést szerezzen egy gyerek komponenshez. Ellentétben az I/O módszerrel, itt a szülő komponens közvetlenül birtokolja és irányítja a gyerek komponenst.

### Implementáció lépései:

1. **Komponens generálás:**
```bash
ng generate component card --skip-tests
```

2. **App komponens template:**
```html
<h1>App komponens</h1>
<button (click)="update()">Update</button>
<app-card #card></app-card>
```

3. **App komponens TypeScript:**
```typescript
@ViewChild('card') card!: CardComponent;

update(): void {
  this.card.changeMessage();
}
```

4. **Card komponens:**
```typescript
export class CardComponent {
  message = 'Eredeti üzenet';
  
  changeMessage(): void {
    this.message = 'New content';
  }
}
```

```html
<p>{{message}}</p>
```


### Mikor érdemes használni?

- **Elsődleges választás:** I/O módszer (SOLID elvekkel összhangban)
- **ViewChild használata:** Csak akkor, ha muszáj, mivel kissé szembe megy a SOLID elvekkel
- A ViewChild teljes elérést biztosít a gyerek komponens minden tulajdonságához és metódusához


## Content Projection (ng-content)

### Alapfogalom

A **Content Projection** vagy **Transclusion** lehetővé teszi, hogy tartalmat adjunk át egy szülő komponensből egy gyerek komponensbe. Ez különösen hasznos sablonfelépítéseknél és újrafelhasználható komponenseknél.

### Gyakorlati példa implementáció:

1. **Movie osztály létrehozása:**
```bash
ng generate class movie
```

```typescript
export class Movie {
  constructor(
    public title: string,
    public year: number,
    public intro: string
  ) {}
}
```

2. **App komponens beállítása:**
```typescript
export class AppComponent {
  movies: Movie[] = [];
  
  constructor() {
    this.movies.push(
      new Movie('Matrix', 1999, 'Jó kis film'),
      new Movie('Inception', 2010, 'Ez is jó kis film'),
      new Movie('Interstellar', 2014, 'Ez is jó kis film')
    );
  }
}
```

3. **App komponens template (Content Projection):**
```html
<div *ngFor="let item of movies">
  <app-card>
    <div title>{{item.title}}</div>
    <div year>{{item.year}}</div>
    <div intro>{{item.intro}}</div>
  </app-card>
</div>
```

4. **Card komponens template:**
```html
<div>
  <h1><ng-content select="[title]"></ng-content></h1>
  <p><ng-content select="[year]"></ng-content></p>
  <p><ng-content select="[intro]"></ng-content></p>
</div>
```


### Content Projection típusai

- **Single-slot:** Egyszerű `<ng-content></ng-content>`
- **Multi-slot:** Named projection `select` attribútummal

```html
<!-- Multi-slot példa -->
<ng-content select="[header]"></ng-content>
<ng-content select="[content]"></ng-content>
<ng-content select="[footer]"></ng-content>
```


## Kommunikációs Módszerek Összehasonlítása

| Módszer | Előnyök | Hátrányok | Mikor használjuk |
| :-- | :-- | :-- | :-- |
| **Input/Output** | SOLID elvekkel összhangban, lazán csatolt komponensek  | Korlátozott hozzáférés | Elsődleges választás |
| **ViewChild** | Teljes hozzáférés a gyerek komponenshez  | Szorosan csatolt komponensek | Csak szükség esetén |
| **Content Projection** | Rugalmas sablonfelépítés, újrafelhasználhatóság  | Komplexebb logika | Dinamikus tartalom átadásához |

Az Angular komponens kommunikáció során az **Input/Output módszer** használata javasolt elsődlegesen, míg a **ViewChild** és **Content Projection** specifikus esetekben nyújt előnyöket.

