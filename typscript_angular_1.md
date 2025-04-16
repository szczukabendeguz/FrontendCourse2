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



