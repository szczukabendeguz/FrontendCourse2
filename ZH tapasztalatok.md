
## Frontend gyakorlati és elméleti zh eredményértékelés

### Témakörök:

- **JavaScript (JS)**: Az egyik legfontosabb, dinamikus weboldalak készítésére alkalmas nyelv. Gyakorlati alkalmazásai közé tartozik például az űrlapellenőrzés, interaktív elemek létrehozása, aszinkron adatkérés (AJAX) stb.
- **CSS (Cascading Style Sheets)**: A weboldalak megjelenésének (dizájn, színek, elrendezés, animációk) kialakítására szolgál. A gyakorlatban kiemelt szerepet kap a reszponzív dizájn (különböző eszközökhöz való igazodás) készítésében.
- **Bootstrap**: Egy népszerű, nyílt forráskódú CSS-keretrendszer, amely előre elkészített komponenseket (gombok, űrlapok, rácsrendszer stb.) és reszponzív elrendezést biztosít a gyorsabb fejlesztéshez.
- **HTML (HyperText Markup Language)**: A weboldalak szerkezetének leírására szolgáló jelölőnyelv. Minden weboldal alapja, struktúrát ad a tartalomnak (pl. címsorok, bekezdések, listák, táblázatok).


### Ezek működésének gyakorlati alkalmazása:

- A frontend fejlesztés során a HTML-lel létrehozzuk a weboldal vázát.
- A CSS-sel formázzuk, stílusossá tesszük az elemeket.
- A Bootstrap segítségével gyorsan és könnyedén készítünk modern, mobilbarát felületeket sablonok vagy komponensek használatával.
- A JavaScript működést, interaktivitást és dinamikus tartalomkezelést ad az oldalaknak.


### Az óra témája:

A mai órán az elkészült dolgozatok értékelését végeztük el. Megbeszéltük a tipikus hibákat, sikeres megoldásokat, illetve áttekintettük a legfontosabb tanulságokat. Az értékelés során külön kitértünk a technológiák helyes alkalmazására, a kódban előforduló hibákra és a kreatív megoldásokra is.

## Gyakorlati hibák és tippek

- **Saját CSS használata**:
Ha a feladat külön kéri, mindig hozz létre saját CSS fájlt, és ne csak a Bootstrap alapértelmezett stílusaira hagyatkozz!
- **Helyes elérési út megadása**:
Ha a forrásfájl egy mappában található, a relatív elérési utat pontosan add meg:
`href="./bootstrap.css"`
Ne csak `href="bootstrap.css"` legyen, mert bár ez működik Live Server-rel, a deploy (élesítés) során könnyen eltörhetnek a hivatkozások. A forrásfájlok elérési útjának követése és helyes megadása nagyon fontos!
- **Formázási problémák javítása**:
Ha elcsúszik a formázás vagy rendezetlen a kód, VS Code-ban az **Alt + Shift + F** billentyűparancsot használd a gyors formázáshoz.
- **Bootstrap táblázat (table) használata**:
    - Ismerd a Bootstrap `table` működését (osztályok, például `table`, `table-striped` stb.).
    - Tudnod kell, hogyan lehet JavaScript-ből hivatkozni a táblázat egyes elemeire.
    - A táblázat szerkezete:
        - `&lt;thead&gt;`: Fejléc, ide kerülnek a címkék
        - `&lt;tbody&gt;`: Ide generál a JavaScript dinamikusan sorokat (pl. adat beolvasás után)
    - Példa: A `&lt;tbody&gt;`-ba alapból nem írunk semmit, oda a JS tölti be az adatokat.
- **JSON beolvasása és megjelenítése JS-sel táblázatban**:
    - A `fetch()` vagy más adatlekérő módszerek segítségével tölts be JSON fájlt.
    - A JSON elemeit különböző JavaScript ciklusokkal (pl. `forEach`, `map`) jelenítsd meg táblázat soronként.
    - Fontos: Ha nem működik a fetch (például CORS vagy elérési gondok miatt), akkor közvetlenül JS tömbként másold be az adatokat a fájlba, így is meg tudod jeleníteni az információt.
- **Időmenedzsment**:
    - A vizsgán/rövid idő alatt összetett megoldást írni nagy kihívás. Prioritás: működő alapstruktúra, majd utána a részletek.
- **Problémamegoldás**:
    - Ha valami nem működik (pl. fetch), alkalmazz alternatív megoldást, ne akadjon el a fejlesztés!
- **HTML és JS szétválasztása**:
    - Törekedj arra, hogy a HTML szerkezet és a JavaScript logika jól elkülönüljön egymástól, így átláthatóbb és könnyebben karbantartható lesz a kód.
- **Szűrések, feldolgozások JavaScript-ben**:
    - A JSON feldolgozás után tudnod kell egyszerű szűréseket, például a legkevesebbet kereső dolgozó keresése, vagy társai.
    - Ezekhez olyan JS tömbműveleti függvényeket kell ismerni, mint: `filter`, `find`, `sort`, `reduce`.
- **Classok helyes megadása**:
    - Több class felsorolásakor NINCS vessző a class-ok között.

```html
<div></div>
```

- **Async/await ismerete**:
    - Az aszinkron adatkezelés modern JavaScript-ben alap. Ismerd az `async/await` használatát, működését, és tipikus hibáit!
- **Inline CSS**:
    - Kivételes esetben (egy-egy elemhez) használható, de inkább külön CSS fájlban vagy `&lt;style&gt;` blokkban add meg a stílusokat!
- **JS: createElement és innerText nem láncolható**:
    - Például hibás:

```js
document.createElement('div').innerText = 'szöveg';
```

    - Helyesen:

```js
const elem = document.createElement('div');
elem.innerText = 'szöveg';
```

    - Az utasításokat külön sorban, egymás után írd le, ne láncold össze őket.

---

## Elméleti részek kiegészítése

### Callback függvények

- **Callback függvényeket nem returnoljuk, hanem meghívjuk**:
Egy callback függvény lényege, hogy egy másik függvény hívja meg, amikor valamilyen esemény bekövetkezik vagy egy adott művelet befejeződik.
Példa:

```js
function doSomething(callback) {
  // valamilyen logika
  callback(); // Meghívás, nem return
}
```


### Ábrák szerepe

- **Ábrák nagyon fontosak**:
Elméleti anyaghoz mindig jó, ha a magyarázatokat ábrákkal is támogatod. Ha nem tudsz ábrát rajzolni, keress netről szemléletes diagramokat (pl. Google Képek: "JavaScript event loop diagram").


### Szemléletes kódpéldák

- **Szemléletes kódpélda minden elméleti magyarázathoz**:
Egy jó kódpélda segít megérteni az elmélet gyakorlati alkalmazását.
- **Optimalizált szó jelentése**:
Az "optimalizált" azt jelenti, hogy egy megoldás már a lehetőségekhez képest a legjobb állapotban van. Nincs olyan, hogy "optimalizáltabb", mert az optimalizált abszolút: vagy elérted az optimumot, vagy nem.


### Tanulási módszerek

- **Probléma a csak ChatGPT-vel való tanulással**:
Ha csak AI-tól tanulsz, könnyen előfordulhat, hogy nem érted meg a mögöttes problémát, csak másolsz. A Google-nél céltudatos kereséssel jutsz el a lényegi válaszokhoz és közben magad kell kiválasztani, értelmezni, kipróbálni a megoldást.
- **Saját feladatok gyártása**:
Önállóan alkoss feladatokat és próbáld azokat megoldani! Ez segít a mélyebb megértésben és kreatív gondolkodásban.


### Szakmai kommunikáció és záróvizsga

- **Záróvizsgán szóban kell magyarázni**:
Ismerned kell a szakmai szókincset, tudnod kell magyarázni ábrákat, folyamatokat. Nem elég a leírás, gyakorold a szóbeli magyarázatot is!


### Kódolvasás és -értelmezés

- **Kód olvasása/értelmezése nem elég!**
    - Töltsd le a mintakódokat, futtasd le őket!
    - Módosítsd a kódot, egészítsd ki, cseréld ki részeket, hogy valóban megértsd a működését.
    - A kód aktív eszköz, nem csak olvasmány!


### `fetch` szintaxisa

- **Alaposan tanuld meg a `fetch` hívás pontos szintaxisát**:
Vizsgán nincs Google, tehát tudnod kell fejből!
Példa:

```js
fetch('adatok.json')
  .then(response =&gt; response.json())
  .then(data =&gt; console.log(data))
  .catch(error =&gt; console.error(error));
```

- **Kihívás**: Légy tisztában az aszinkron működéssel, hibakezeléssel (`catch`), és a JSON feldolgozásával.


### Szakszerű megfogalmazás

- **Pontos szakmai fogalmazás**
Legyél képes egyszerűen és pontosan leírni, hogy egy adott fogalom (pl. event loop, async/await) mit jelent, hogyan működik, miért fontos.

---

## Event Loop részletesen

### Mi az Event Loop?

Az **event loop (eseményciklus)** a JavaScript motor egyik alapvető része, amely lehetővé teszi a nem-blokkoló, aszinkron műveletek végrehajtását egyetlen szálon (single-threaded környezetben).

### Hogyan működik?

1. **Call Stack (Hívási verem)**:
Ide kerülnek a szinkron műveletek (függvényhívások, változók, stb.). Mindig csak egy függvény fut egyszerre.
2. **Web APIs / Background APIs**:
Az aszinkron kódokat (pl. setTimeout, fetch, event listener) a böngésző motor kezeli a háttérben.
3. **Callback Queue (Várakozó sor)**:
A háttérben lefutó aszinkron műveletek befejezése után azok callback-jait ide helyezi a rendszer.
4. **Event Loop**:
Az event loop folyamatosan figyeli, hogy a call stack üres-e. Ha igen, a callback queue első elemét átteszi a call stack-be, és az elindulhat.

### Ábra (keresd netről: “event loop diagram”):

[MDN Event Loop Ábra](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop#the_event_loop)

```
[ Call Stack ] &lt;-- Event Loop &lt;-- [ Callback Queue ]
        ^                                   |
        +------ Web APIs ---- fetch, setTimeout, stb. 
```


### Példakód:

```js
console.log('Első');

setTimeout(() =&gt; {
  console.log('Második (asynchronous)');
}, 0);

console.log('Harmadik');
```

**Várható kimenet:**

```
Első
Harmadik
Második (asynchronous)
```

**Magyarázat**:
A `setTimeout` callback-je a Web API-hoz kerül, majd a callback queue-ba helyezi az event loop, miután a call stack kiürült.

### Miért fontos?

- Lehetővé teszi, hogy felhasználói interakciók, szerverválaszok vagy egyéb aszinkron események ne állítsák meg a fő futási szálat.
- Ha nem érted, mi történik a háttérben, könnyen hibás aszinkron kódot írhatsz (pl. race condition, deadlock).
