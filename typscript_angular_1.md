## Angular, TypeScript, Frameworkök és Könyvtárak

### TypeScript (TS)

- **Mi az a TypeScript?**
    - A TypeScript a JavaScript „supersetje”, vagyis a JavaScript kibővítése.
    - Minden, ami JavaScript, az TypeScript-ben is érvényes – de a TypeScript ad hozzá típusosságot, OOP-tulajdonságokat (osztályok, interfészek), fejlettebb szerkesztés támogatást.
    - Kód:

```ts
let age: number = 22;
```


### Angular – Miért keretrendszer?

- **Angular** egy fejlett keretrendszer (framework), amit a Google fejleszt.
- A keretrendszerek (pl. Angular, React, Vue) a frontenden egységes szerkezetet, best practice-ket adnak, támogatnak routingot, állapotkezelést, űrlapkezelést, stb.
- _Előny:_ Komplett megoldásokat kínálnak a fejlesztés szinte minden részére, emiatt támogatják a projekt struktúrálását, a moduláris kódbázist és az újrafelhasználhatóságot.


### Könyvtárak (Libraries) és különbségük a keretrendszerekkel szemben

- **Könyvtár (lib, library):** Előre megírt, újrahasznosítható kódrészletek, függvények vagy modulok gyűjteménye.
    - Példa: Egy képfeldolgozó vagy grafikai library, amit egyszerűen behívhatsz a projektedbe.
    - Ezek nem adnak meg projekt struktúrát és fejlesztési mintákat – csak bizonyos feladatok megoldásához nyújtanak funkciókat.
    - Példakód:

```js
// Pl. Lodash egy gyakori JS könyvtár
import _ from 'lodash';
const arr = [1, 2, 3, 4];
const first = _.first(arr);
```

- **Keretrendszer (framework):**
    - Egy komplett, összefüggő megoldásrendszer, sok előre gyártott eszközzel: routing, state management, komponensstruktúra, stb.
    - Tipikus „best practice” megoldásokat használ, nem kell mindent nulláról írni.
    - Példa:
        - Routing: Angularban, React Routerben, Vue Routerben mind adott.
        - Auth/login: Keretrendszerekben legtöbbször van előre kidolgozott megoldás vagy integráció.
- **Fő különbség**:
    - Könyvtárat (lib) te használsz, azt hívod meg ott, ahol akarod.
    - Keretrendszer (framework) diktálja, hogyan épül fel az alkalmazás – a te kódod „illeszkedik” bele a framework által definiált struktúrába.


### A helyes tanulási sorrend

- Először tanuld meg nulláról, hogyan lehet felépíteni egy megoldást (például SPA-t), aztán térj át a keretrendszerekre és használd a best practice-ket.


### Népszerű név szerint:

- **React**: Facebook fejleszti.
- **Angular**: Google fejleszti.
- **Vue**: Közösségi fejlesztés, célja a React és Angular előnyeinek ötvözése.
- (Továbbiak: Svelte, Ember.js, stb.)


### Framework Hell

- Folyamatosan újabb keretrendszerek jelennek meg, ráadásul egyes keretrendszerekre is készülnek új „framework-ök” (pl. Vue → Nuxt.js).
- Egyet megtanulva azonban könnyen tudsz boldogulni a többivel is, mert a szemléletük, architektúrájuk hasonló.


### Kell-e keretrendszer?

- **Nem mindig szükséges!**
    - Kis, egyszerűbb projekthez, gyors prototípushoz elég egy-egy library vagy magad által írt JS.
    - Nagy, összetett, bővíthető és karbantartható alkalmazásokhoz (pl. vállalati rendszerek) viszont megéri keretrendszert használni.


### SPA – Single Page Application

- Ezeket gyakran modern keretrendszerekkel készítik.
- **SPA**: Az egész alkalmazás egyetlen oldalon fut (tipikusan index.html), és az adatokat AJAX/Fetch/HTTP-kérésekkel dinamikusan tölti be, oldalfrissítés nélkül.


### AJAX – Az SPA-k őse

- **AJAX** = Asynchronous JavaScript And XML
- Lehetővé tette, hogy a weboldal frissítése nélkül dinamikus adatokat kérjünk le a szervertől (például JSON formátumban) és mutassunk meg a felhasználónak.
- Nincs teljes oldalfrissítés, csak az adatok frissülnek.

  ## Angular alapok és AJAX/XHR

### AJAX és XHR részletek

- **AJAX** nem önálló technológia, hanem **meglévő eszközök kombinációja**:
    - `XMLHttpRequest` (XHR) objektum a kérések kezelésére.
    - Adatformátumok (XML/JSON).
    - Aszinkron JavaScript logika.
- **XHR kérések** ma is használatosak (rövidítés: **XHR**).
A böngésző fejlesztői eszközein (DevTools) a **Network** fülön a **Fetch/XHR** szekcióban láthatók ezek a kérések.
_Interjú tipp:_ Sok helyen kérdeznek XHR-ről, ne feledd, hogy ez a klasszikus AJAX megvalósítás módja!


### jQuery és szerepe

- **jQuery** egy JavaScript könyvtár, ami régebben nagy népszerűségnek örvendett.
    - _Előnyei_ anno:
        - Egységesítette a böngészők közötti különbségeket (pl. event kezelés).
        - Egyszerű DOM manipuláció (pl. `$('#elem').slideToggle()`).
        - Szintaxis rövidség (pl. `$('.class')` helyett `document.querySelectorAll`).
    - _Hanyatlás oka_: A modern JavaScript (ES6+) és CSS3 megoldások kivetkőztették a szükségességét.
    - _Fejlesztő_: John Resig (korábbi Microsoft mérnök).

---

## Angular konkrétumok

![angular](https://github.com/user-attachments/assets/7b8da3a6-1730-41f4-ba05-c8d0fa7d5fb6)

### Projekt létrehozás és CLI

- **Angular CLI** telepítése:

```bash
npm install -g @angular/cli
```

- **Új projekt** indítása:

```bash
ng new demo-app --standalone=false
```

    - **Kérdések a generálásnál**:
        - _CSS preprocesszor_: Válaszd az `SCSS`-t (pl. indentation-based stílus).
        - _SSR (Server-Side Rendering)_: Ha nem kell, válaszolj „No”.


### Mappaszerkezet táblázatban

| Mappa/fájl | Leírás |
| :-- | :-- |
| `src/` | Forráskódok fő mappája. |
| `src/app/` | Az alkalmazás fő modulja és komponensei. |
| `src/app/app.component.ts` | Alapértelmezett komponens TypeScript fájlja. |
| `src/app/app.component.html` | A komponens HTML sablonja. |
| `src/app/app.component.scss` | A komponens stíluslapja (SCSS). |
| `src/assets/` | Statikus fájlok (pl. képek, betűtípusok). |
| `src/environments/` | Környezeti változók (pl. dev/prod API URL-ek). |
| `angular.json` | Projektkonfiguráció (build, serve, teszt beállítások). |

### Komponens szerkezet

Minden komponens 3 fájlból áll:

1. **HTML** - Sablon (pl. `app.component.html`).
2. **TypeScript** - Logika (pl. `app.component.ts`).
3. **SCSS** - Stílusok (pl. `app.component.scss`).

### Futtatás és szerver

- **Szerver indítása**:

```bash
ng serve
```

    - A parancs buildeli az alkalmazást és elindít egy lokális szervert (általában `http://localhost:4200`).


### Adatkötés és eseménykezelés

- **Interpoláció**: TS változók megjelenítése HTML-ben:

```html
<h1>{{ cim }}</h1>
```

A `cim` változó értéke dinamikusan frissül a komponensben.
- **Eseménykötés**:

```html
&lt;button (click)="valamiFuggveny()"&gt;Kattints!&lt;/button&gt;
```

A `(click)` esemény hozzárendelődik a TS fájlban lévő `valamiFuggveny` függvényhez.
- **Two-way data binding**:
Kétirányú adatkötéshez (pl. űrlapmezőknél) használd az `[(ngModel)]` direktívát:

```html
&lt;input [(ngModel)]="felhasznaloNeve"&gt;
```

A `felhasznaloNeve` változó szinkronban marad az input mezővel.

![image](https://github.com/user-attachments/assets/7497915b-4e56-47c3-a375-fcc10f6c6a6b)

## `ngModel` és FormsModule használata Angularban

### Kétirányú adatkötés input mezőnél – `ngModel`

- Az **`ngModel`** direktíva segítségével kétirányú (two-way) adatkapcsolatot létesíthetsz egy input mező és a komponensben (TS fájlban) lévő változó között.
- Például:

```html
&lt;input type="number" [(ngModel)]="myNumber"&gt;
```

Itt a `myNumber` változó értéke mindig tükrözi az input mező aktuális értékét és fordítva.


### FormsModule importálása

- Ahhoz, hogy az **`ngModel`** használható legyen, az adott Angular modulban (pl. `AppModule`) **be kell importálni a `FormsModule`-t**!
- Amikor a projekt `standalone: false` módban lett létrehozva (klasszikus modul-rendszer), az import így néz ki:

1. Nyisd meg a `src/app/app.module.ts` fájlt.
2. Egészítsd ki az importokat:

```typescript
import { FormsModule } from '@angular/forms';
```

3. Tedd be a `imports` tömbbe:

```typescript
@NgModule({
  declarations: [
    AppComponent,
    // egyéb komponensek
  ],
  imports: [
    BrowserModule,
    FormsModule,        // &lt;&lt;-- itt!
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

- Ezután már működni fog az `ngModel` a template-ben bármilyen input elemen.


### Standalone komponensek esetén

- Ha standalone Angular komponenseket használnál (**standalone: true** esetén), akkor nem a modulba, hanem közvetlenül a komponenshez kellene importálni a `FormsModule`-t vagy az adott form vezérlőt.
- Most viszont a klasszikus modul struktúra szerint dolgozol, ezért a fenti lépéseket kövesd!

---
## For ciklus HTML-ben – *ngFor használata Angularban

Az Angular **strukturális direktívákat** kínál a sablonban (HTML-ben) történő ciklikus megjelenítéshez. A leggyakoribb példa a **`*ngFor`**:

### Példa használat:

```html
<p>{{ item }}</p>
```

- **Mit jelent ez?**
    - Az `increments` egy tömb a komponens TypeScript fájljában.
    - A sor minden egyes eleméhez (item) létrejön egy `<p>`, amelyben a sablonban az adott elem értéke jelenik meg.


### Részletesebb példa:

#### TypeScript fájl (app.component.ts):

```typescript
export class AppComponent {
  increments = [1, 2, 3, 4, 5];
}
```


#### HTML (app.component.html):

```html
</p><p>{{ item }}</p>
```


#### Eredmény:

```
1
2
3
4
5
```


### Fontosabb tudnivalók az *ngFor-ról

- Mindig **`*ngFor`** (csillaggal), mert strukturális direktíva!
- A sablonban az **`let item of lista`** szintaxist használjuk, ahol `item` az aktuális elem, `lista` pedig a bejárni kívánt tömb.
- További index kezelésére is van lehetőség:

```html
<li>
  #{{ i }}: {{ elem }}
</li>
```


---

## Konstruktor szerepe komponensben

- Az Angular komponens TypeScript osztályának **konstruktorában** (constructor) inicializálhatod az adatokat, például alapértékeket adhatsz egy tömbhöz:

```typescript
export class AppComponent {
  increments: number[] = [];

  constructor() {
    this.increments.push(1, 2, 3, 4, 5);
  }
}
```

- A konstruktor **fő szerepe**: a komponens létrejöttekor (példányosításakor) egyszer fut le, így alkalmas kezdőértékek beállítására, szolgáltatások (service-ek) injektálására stb.

---

## `*ngIf` – Feltételes megjelenítés Angularban

- Az **`*ngIf`** strukturális direktíva feltételhez köti egy HTML elem megjelenítését.


### Alapszintaxisa:

```html
<p>Ez akkor látszik, ha a 'visible' igaz!</p>
```

- Csak akkor jelenik meg a `<p>`, ha a komponensben a **`visible`** változó értéke true.


### Példa logika a komponensben:

```typescript
export class AppComponent {
  visible = true;
}
```


### Ágak kezelése (`else`):

- *ngIf-else* eset:

```html
</p><div>
  Hiba történt!
</div>
&lt;ng-template #mindenOk&gt;
  Minden rendben.
&lt;/ng-template&gt;
```

- Az `&lt;ng-template&gt;` blokk az else ág.

---

## `ngClass` – Dinamikus osztály (class) kezelés Angularban

Az **`[ngClass]`** direktíva lehetővé teszi, hogy egy elemhez dinamikusan adj többféle CSS osztályt (class-t) Angularban, feltételek alapján.

### Alapszintaxisa:

```html
<div>
  Dinamikus class-váltás példa
</div>
```

- **`bigger`** osztály akkor lesz ráadva, ha az `isBig` változó true.
- **`smaller`** osztály akkor, ha az `isBig` false.


### Példakód teljesen:

#### app.component.ts

```typescript
export class AppComponent {
  isBig = true;
}
```


#### app.component.html

```html
<div>
  Ez a szöveg vagy nagyobb, vagy kisebb stílust kap!
</div>
&lt;button (click)="isBig = !isBig"&gt;Vált&lt;/button&gt;
```


#### app.component.scss

```scss
.bigger {
  font-size: 2rem;
  color: green;
}
.smaller {
  font-size: 1rem;
  color: red;
}
```


### További lehetőségek

- Több osztály adásához is használhatsz tömböt:

```html
<div></div>
```

- Egyedi logika alapján object vagy függvény is visszaadhatja az osztályokat.

---

### Röviden:

- **[ngClass]** – Egy elem CSS osztályainak dinamikus, feltételes beállítása Angular komponens változói/logikája alapján.

---
## Angular Service-ek

### Mi az a service Angularban?

Az Angularban a **service** (szolgáltatás) egy újrafelhasználható TypeScript osztály, amely logikát, adatokat vagy funkcionalitást (pl. API-hívásokat, állapotkezelést) biztosít több komponens számára. A service-ek célja, hogy a közös logikát ne komponensekben, hanem különálló, könnyen tesztelhető és karbantartható egységekben tartsuk.

### Dependency Injection (DI) Angularban

Az Angular egyik alapelve a **dependency injection** (függőséginjektálás): a komponensek vagy más service-ek nem maguk hozzák létre a szükséges objektumokat, hanem az Angular injector rendszere „injektálja” (adja oda) nekik azokat. Ez lehetővé teszi a laza csatolást, könnyebb tesztelhetőséget és újrafelhasználhatóságot.

### Singleton service – Mit jelent ez?

Alapértelmezés szerint az Angular service-ek **singleton** módon működnek: az alkalmazás életciklusa alatt csak egy példány jön létre belőlük, és ezt az egy példányt kapja meg minden komponens vagy más service, amelyik igényli. Ez azt jelenti, hogy a service által tárolt állapot vagy logika mindenhol ugyanaz marad – például egy bejelentkezett felhasználó adatai, cache-elt API válaszok, stb..

#### Singleton service előnyei:

- **Állapot megosztás**: Minden komponens ugyanazt az adatot látja.
- **Memóriahatékonyság**: Nem jön létre feleslegesen több példány.
- **Központi logika**: Pl. autentikáció, naplózás, API-hívások, stb.


### Hogyan hozol létre service-t Angularban?

A legegyszerűbb módja a service generálásának az Angular CLI használata:

```bash
ng g service szolgaltatas-neve
```

Ez létrehoz egy új service-t a `src/app` mappában, pl. `szolgaltatas-neve.service.ts` néven.

#### Példa generált service-re:

```typescript
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root' // így lesz singleton az egész alkalmazásban!
})
export class SzolgaltatasNeveService {
  constructor() { }
}
```

A `providedIn: 'root'` beállítás azt mondja az Angularnak, hogy a service singletonként, az egész alkalmazás szintjén legyen elérhető.

### Hogyan működik a dependency injection?

- Ha egy komponens vagy más service konstruktorában megadod a service típusát, az Angular automatikusan beadja a példányt:

```typescript
constructor(private szolgaltatas: SzolgaltatasNeveService) { }
```

- Bármelyik komponensben, ahol így hivatkozol rá, ugyanazt a példányt kapod vissza.


### Összefoglalva

- Az Angular service-ek alapból singletonok, ha a `providedIn: 'root'`-tal hozod létre őket.
- A dependency injection automatikusan beadja a szükséges service példányt a komponensbe vagy más service-be.
- Service-ekkel közös logikát, állapotot, adatokat tudsz megosztani az alkalmazásod különböző részei között.

---
## Angular CLI – Projekt és komponensek létrehozása

Az **Angular CLI** (Command Line Interface) egy parancssoros eszköz, amellyel gyorsan, egységes szerkezetben hozhatsz létre új Angular projekteket és komponenseket.

### Új projekt indítása

```bash
ng new devcrud --standalone=false --skip-tests --style=sass --ssr=false
```

- Ez létrehoz egy új projektet `devcrud` néven, klasszikus modulrendszerrel, tesztek nélkül, Sass stílusokkal.


### Komponensek és osztály generálása

```bash
cd devcrud
ng g class developer --skip-tests
ng g c create --skip-tests
ng g c list --skip-tests
ng g c edit --skip-tests
```

- Ezek a parancsok létrehozzák a `developer` osztályt, valamint a `create`, `list`, `edit` komponenseket a `src/app/` mappában.
- Minden komponenshez három fő fájl jön létre: `.ts` (logika), `.html` (sablon), `.scss` (stílus).
- A CLI automatikusan hozzáadja a komponenst az `app.module.ts`-hez.


### Fejlesztői szerver indítása

```bash
ng serve
```

- Ezzel buildeli a projektet és elindítja a helyi szervert, általában a `http://localhost:4200` címen.

---

## Angular Router – Útvonalak és navigáció

Az **Angular Router** lehetővé teszi, hogy különböző komponensekhez különböző URL-eket rendelj.

### Útvonalak beállítása

Az útvonalakat az `src/app/app-routing.module.ts` fájlban kell konfigurálni:

```typescript
// src/app/app-routing.module.ts
const routes: Routes = [
  { path: '', redirectTo: 'list', pathMatch: 'full' },
  { path: 'list', component: ListComponent },
  { path: 'create', component: CreateComponent },
  { path: 'edit/:id', component: EditComponent },
  { path: 'delete', component: DeleteComponent },
  { path: '**', redirectTo: 'list', pathMatch: 'full' }
];
```

- Minden útvonalhoz hozzárendeled a megfelelő komponenst.
- A `router-outlet` direktíva helyén jelenik meg az aktuális oldal tartalma.


### Egyszerű navigáció a sablonban

A navigációs sávhoz (pl. `src/app/nav/nav.component.html`):

```html
<a routerLink="/list">Listázás</a>
<a routerLink="/create">Létrehozás</a>
<a routerLink="/delete">Törlés</a>
```


### Fő sablon szerkezet

A főoldal sablonjában (`src/app/app.component.html`):

```html
<app-nav></app-nav>
<router-outlet></router-outlet>
<app-footer></app-footer>
```

- A `<router-outlet>` helyén jelenik meg mindig az aktuális route-hoz tartozó komponens.

---

## Az Angular **change detection** rendszere és **életciklus hook**-jai

Az Angular **change detection** rendszere és **életciklus hook**-jai közvetlenül kapcsolódnak a kétirányú adatkötés működéséhez. A különbség az `alma()` metódus és a `get alma()` getter között pedig kritikus a változások észlelésében:

### 1. **Change Detection \& Életciklus**

- A **ngOnChanges** hook csak akkor aktiválódik, ha egy `@Input()` property változik (primitív típusoknál értékváltozás, objektumoknál referencia változás)[^2][^8].
- A **ngDoCheck** hook minden változásdetekciós ciklusban lefut, és itt lehet egyéni változásvizsgálatot implementálni (pl. objektumok mélyebb vizsgálata)[^2].


### 2. **Metódus (`alma()`) vs. Getter (`get alma()`)**

| Szempont | `alma()` metódus | `get alma()` getter |
| :-- | :-- | :-- |
| **Hívási gyakoriság** | Minden változásdetekciós ciklusban lefut | Csak akkor, ha a getter függőségei változnak |
| **Teljesítmény** | Potenciálisan lassabb (felesleges hívások) | Hatékonyabb, ha függőségek változnak ritkán |
| **Változásészlelés** | Angular nem követi a metódus függőségeit | Angular automatikusan kezeli a getter függőségeit |
| **Példa** | `{{ alma() }}` | `{{ alma }}` |

### 3. Kétirányú adatkötés kapcsolat

- A **[(ngModel)]** kétirányú kötés mögött `@Input()` és `@Output()` dekorátorok vannak, amelyek a change detection rendszert aktiválják.
- Ha getter/setter-t használsz `@Input()` property-ként, a **ngOnChanges** nem fog jelezni változást, hacsak explicit nem frissíted a referenciát.


### 4. Ajánlott gyakorlat

- **Getterek** használata előnyösebb, ha a számítás költséges, vagy ha a template-ben gyakran hivatkoznak rá.
- **Metódusok** kerülendők template kifejezésekben, kivéve, ha tudod, hogy ritkán változnak a függőségeik.

**Példa problémára:** Ha egy metódus minden ciklusban új objektumot ad vissza, `ExpressionChangedAfterItHasBeenCheckedError` hibát okozhat[^4]. Getter esetén ez csak akkor fordul elő, ha a belső állapot nem megfelelően kezelt.

---
