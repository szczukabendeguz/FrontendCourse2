
# jegyzet a JavaScript működéséről és webes technológiákról

## 1. JavaScript Engine alapjai

A JavaScript engine feladata a JavaScript kód futtatása és végrehajtása. Minden böngésző saját JavaScript motort használ (pl. V8 a Chrome-ban, SpiderMonkey a Firefox-ban).

**Alapvető működési fázisok:**

- **Parsing (Elemzés):** A kód szöveges formájának feldolgozása és AST (Abstract Syntax Tree) létrehozása
- **Bytecode generálás:** Az AST alapján bytecode készül
- **JIT fordítás:** A gyakran futtatott részek natív gépi kóddá fordítása
- **Végrehajtás:** A gépi kód futtatása a CPU által

**Példa JavaScript motorok:**

- V8 (Google Chrome, Node.js)
- SpiderMonkey (Firefox)
- JavaScriptCore (Safari)
- Chakra (régebbi Edge)


## 2. Primitív típusok JavaScriptben

A primitív típusok olyan alapvető adattípusok, amelyek közvetlenül tárolják az értékeket és nem rendelkeznek metódusokkal.

**JavaScript primitív típusai:**

- **Number:** Számok tárolására (pl. `let x = 42;`)
- **String:** Szövegek tárolására (pl. `let text = "Hello";`)
- **Boolean:** Logikai értékek: `true` vagy `false`
- **Null:** Egy üres vagy nemlétező érték
- **Undefined:** Egy értéket nem kapott változó alapértelmezett állapota
- **BigInt:** Nagy egész számok (pl. `123456789012345678901234567890n`)
- **Symbol:** Egyedi azonosítók (pl. `Symbol("id")`)

**Jellemzők:**

- Érték szerint másolódnak (nem referencia szerint)
- Megváltoztathatatlanok (immutable)


## 3. Execution Context (Végrehajtási környezet)

Az execution context a JavaScript futtatási környezete, amely meghatározza, hogy a kód hogyan kerül végrehajtásra.

**Típusai:**

- **Global Execution Context (GEC):** Alap végrehajtási környezet, minden JavaScript fájl betöltésekor létrejön
- **Function Execution Context (FEC):** Minden függvényhíváskor új környezet jön létre
- **Eval Execution Context:** Az `eval()` függvény által futtatott kódhoz tartozó környezet

**Fázisai:**

- **Létrehozási fázis (Creation Phase):** Memória foglalás, változók és függvények hoisting-ja
- **Végrehajtási fázis (Execution Phase):** Kód soronkénti végrehajtása

**Call Stack (Hívási verem):** Kezeli az execution context-eket és a függvényhívások sorrendjét.

## 4. JavaScript Runtime

A JavaScript runtime egy környezet, amely lehetővé teszi a JavaScript kód futtatását, és kiegészíti a JavaScript motort különböző funkciókkal.

**Komponensei:**

- **JavaScript motor:** Végrehajtja a kódot, tartalmazza a call stack-et és a heap-et
- **Web API-k:** Böngészőspecifikus funkciók (DOM manipuláció, fetch, setTimeout)
- **Callback queue:** Tárolja a végrehajtásra váró aszinkron műveleteket
- **Event loop:** Átadja a callback queue-ból a függvényeket a call stack-nek

**Különböző JavaScript runtime környezetek:**

- **Böngésző runtime:** Weboldalak JavaScript kódjának futtatására
- **Node.js runtime:** Szerveroldali JavaScript futtatására


## 5. Callback Queue és Event Loop

**Callback Queue (Visszahívási sor):**

- FIFO (First In, First Out) adatszerkezet
- Tárolja az aszinkron műveletek (pl. setTimeout, AJAX) callback függvényeit
- A callback-ek várnak arra, hogy a call stack kiürüljön

**Event Loop (Eseményhurok):**

- Folyamatosan figyeli a call stack-et és a callback queue-t
- Ha a call stack üres, kiveszi a callback queue első elemét és a call stack-re helyezi
- Prioritást ad a microtask queue-nak (pl. Promise-ok callback-jei) a callback queue előtt

**Példa prioritásokra:**

```javascript
console.log("Start");
setTimeout(() =&gt; console.log("Timeout"), 0);
Promise.resolve().then(() =&gt; console.log("Promise"));
console.log("End");
// Kimenet: Start → End → Promise → Timeout
```


## 6. Interpretált és Fordított JavaScript

A JavaScript mind interpretált, mind fordított (compiled) nyelv, mivel modern motorjai kombinálják mindkét megközelítést a JIT fordítás segítségével.

**Interpretált jellemzők:**

- Az interpreter soronként elemzi és hajtja végre a kódot
- Gyors indulást biztosít komplex fordítás nélkül

**Compiled jellemzők (JIT által):**

- A gyakran futtatott kódrészek natív gépi kóddá fordítódnak
- Teljesítményoptimalizáció a hosszú távú futás érdekében

**A JavaScript JIT folyamata:**

1. Bytecode generálás az AST-ből (interpretáció)
2. Gyakran futtatott részek azonosítása
3. Gépi kóddá fordítás és optimalizáció

## 7. Parsing és Compilation

**Parsing (Elemzés):**

1. **Tokenizálás (Lexical Analysis):** A kód tokenekre bontása (kulcsszavak, operátorok, azonosítók)
2. **AST generálás:** Fa-szerű adatstruktúra létrehozása a kód szerkezetének reprezentálására

**Compilation (Fordítás):**

1. **Bytecode generálás:** Az AST-ből köztes kód készítése
2. **JIT fordítás:** Gépi kód generálása a gyakran használt részekből

**Példa:**

```javascript
let x = 5 + 3;
```

- **Tokenek:** `let`, `x`, `=`, `5`, `+`, `3`, `;`
- **AST:** Egy fa, amely ábrázolja a változódeklarációt és a kifejezést


## 8. JIT (Just-In-Time) fordítás

**JavaScriptben:**

- A JIT fordító futás közben fordítja le a bytecode-ot natív gépi kódra
- Figyeli a "hot code path"-eket (gyakran futtatott kódrészeket)
- Optimalizációkat végez a teljesítmény javítása érdekében
- Deoptimalizációt hajt végre, ha feltételei sérülnek

**Java-ban:**

- A Java szintén JIT fordítót használ a Java Virtual Machine (JVM) részeként
- A Java forrás először bytecode-dá fordul (javac által)
- A JIT futásidőben fordítja a gyakran használt metódusokat
- Optimalizációkat végez a hardver és a futási mintázatok alapján

**JIT optimalizációs technikák:**

- Inline-olás (gyakran hívott függvények beágyazása)
- Hurok optimalizáció (pl. hurok kifordítása)
- Típus-specializáció (típusinformációk alapján)
- Dead code elimination (nem használt kód eltávolítása)


## 9. AST és Tokenizáció

Az **AST (Abstract Syntax Tree)** a tokenizáció utáni lépésben jön létre.

**Tokenizáció (Lexikális elemzés):**

- A forráskód tokenekre bontása (pl. kulcsszavak, azonosítók, operátorok)
- Tokenek: a kód legkisebb jelentéssel bíró egységei

**AST generálás (Szintaktikai elemzés):**

- A tokenekből fa-szerű struktúra építése
- Minden csomópont egy programnyelvi elemnek felel meg
- Az AST ábrázolja a kód szerkezetét és hierarchiáját

**Példa AST:**

```
Program
└── VariableDeclaration
    ├── Identifier: x  
    └── BinaryExpression  
        ├── Literal: 5  
        └── Literal: 3  
```


## 10. Scope Chain (Hatókör-lánc)

A scope chain határozza meg, hogy a változók és függvények hogyan érhetők el egy adott kódrészletben.

**Működése:**

- Minden függvény létrehoz egy hatókört (scope)
- Ha egy változó nem található az aktuális hatókörben, a motor a külső hatókörökben keres
- A keresés belülről kifelé történik, a legbelső hatókörtől a globális felé

**Hatókör típusai:**

- **Globális hatókör:** A program indításakor létrejön
- **Függvény hatókör:** Függvények által létrehozott hatókör
- **Blokk hatókör:** `let` és `const` változók esetén létrejön blokkokban (pl. `if`, `for`)

**Példa closure-ra (lezárásra):**

```javascript
function createCounter() {
  let count = 0;
  return function() {
    count++;
    return count;
  };
}
const counter = createCounter();
// A függvény megtartja a külső hatókör változóihoz való hozzáférést
```


## 11. var és let közötti különbségek

**Hatókör:**

- **var:** Függvény-hatókörű
- **let:** Blokk-hatókörű (pl. `if`, `for` blokkok)

**Újradeklarálás:**

- **var:** Megengedett
- **let:** Hibát okoz

**Hoisting:**

- **var:** Deklaráció hoistingolódik, `undefined` értékkel inicializálódik
- **let:** Deklaráció hoistingolódik, de Temporal Dead Zone (TDZ) miatt nem érhető el inicializálás előtt

**Globális objektum:**

- **var:** Hozzáadódik a `window` objektumhoz (böngészőben)
- **let:** Nem kerül a `window` objektumba

**Blokkszintű hatókör:** A `var` **nem képes** kielégíteni a blokkszintű hatókört, míg a `let` igen.

## 12. Webapp és Weblap közötti különbségek

**Weblap:**

- Főleg statikus tartalom
- Egyszerű struktúra (HTML, CSS, egyszerű JavaScript)
- Korlátozott interaktivitás
- Ritkán frissül
- Példák: Blogok, céges weboldalak

**Webapp (Webalkalmazás):**

- Dinamikus, interaktív tartalom
- Komplex struktúra (modern front-end és back-end technológiák)
- Gazdag funkcionalitás
- Valós idejű frissítések
- Példák: Gmail, Facebook, banki alkalmazások

**Főbb különbségek:** Interaktivitás szintje, komplexitás, frissítési gyakoriság, fejlesztési idő.

## 13-14. Graceful Degradation és Progressive Enhancement

**Graceful Degradation (Kecses leépülés):**

- A legmodernebb technológiákra épít
- Ha egy régebbi böngésző nem támogat funkciókat, egyszerűbb változatra redukálódik
- A modern funkcióktól halad az egyszerűbb felé
- Példa: Modern animációk, amelyek régebbi böngészőkben nem jelennek meg
- Top-down elv

**Progressive Enhancement (Fokozatos bővítés):**

- Az alapvető funkcionalitással kezd
- Fokozatosan bővíti a funkciókat a modern böngészőkben
- Az alap funkcionalitástól halad a komplexebb felé
- Példa: Alap HTML űrlap, amely modern böngészőben JavaScript validációval bővül
- Bottom up elv

**Főbb különbségek:**

- **Kiindulópont:** Graceful degradation a modern technológiákból indul, progressive enhancement az alapokból
- **Fejlesztési fókusz:** Graceful degradation a modern funkciókat implementálja először, progressive enhancement az alapfunkciókat
- **Felhasználói élmény:** Graceful degradation csökkentett élményt nyújt régebbi rendszereken, progressive enhancement mindenkinek biztosítja az alapélményt

**Mikor melyiket érdemes használni:**

- Graceful degradation: Modern webalkalmazásoknál, ahol a felhasználók főként újabb eszközöket használnak
- Progressive enhancement: Széles felhasználói bázist célzó weboldalaknál, ahol fontos az univerzális hozzáférés

## **15-16. Imperatív és Deklaratív UI kezelés**

Az **imperatív** és **deklaratív** UI-kezelés két különböző programozási paradigma, amelyek eltérő megközelítést alkalmaznak a felhasználói felületek (UI) létrehozására és kezelésére. Ezek a paradigmák meghatározzák, hogyan írjuk meg a kódot, hogyan kezeljük az állapotokat, és hogyan reagálunk a felhasználói interakciókra.



### **Imperatív UI-kezelés**

Az imperatív programozásban részletes utasításokat adunk meg arról, hogy **hogyan** kell a felhasználói felületet létrehozni és frissíteni. Ez a megközelítés teljes kontrollt biztosít a fejlesztő számára, de gyakran bonyolultabb és több kódot igényel.

#### **Jellemzők:**

1. **Explicit kontroll:** A fejlesztő határozza meg minden egyes lépést.
2. **Állapotkezelés:** Az állapotot manuálisan kell követni és frissíteni.
3. **Eseményvezérelt:** Az események (pl. kattintás) explicit módon kezelendők.
4. **Procedurális logika:** A UI létrehozása és frissítése lépésről lépésre történik.

#### **Példa: Imperatív UI Androidon (Java):**

```java
Button button = findViewById(R.id.my_button);

button.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        button.setText("Clicked!"); // A gomb szövegének manuális frissítése
    }
});
```

- Itt a fejlesztő explicit módon definiálja, hogy mi történjen kattintáskor (eseménykezelés), és manuálisan frissíti az UI-t.


#### **Előnyök:**

- Teljes kontroll az UI felett.
- Alkalmas komplex, finomhangolt interakciókhoz és animációkhoz.
- Hasznos teljesítménykritikus alkalmazásoknál.


#### **Hátrányok:**

- Több boilerplate kódot igényel.
- Nehezebb karbantartani nagyobb projektekben.
- Az állapotok szinkronizálása manuális, ami hibalehetőségeket okozhat.



### **Deklaratív UI-kezelés**

A deklaratív programozásban a fejlesztő azt írja le, hogy a felhasználói felületnek **milyennek kell lennie**, nem pedig azt, hogy hogyan kell létrehozni vagy frissíteni. A keretrendszer automatikusan kezeli az állapotváltozásokat és az ezekből következő UI-frissítéseket.

#### **Jellemzők:**

1. **Magasabb absztrakciós szint:** A fejlesztő az eredményt írja le, nem a folyamatot.
2. **Automatikus állapotkezelés:** Az UI automatikusan frissül az állapotváltozások alapján.
3. **Reaktivitás:** A deklarált UI mindig tükrözi az aktuális állapotot.
4. **Egyszerűség:** Kevesebb boilerplate kód, olvashatóbb logika.

#### **Példa: Deklaratív UI React-ben:**

```javascript
function ButtonComponent() {
  const [text, setText] = React.useState("Click me");

  return (
    &lt;button onClick={() =&gt; setText("Clicked!")}&gt;
      {text}
    &lt;/button&gt;
  );
}
```

- Itt a gomb szövege automatikusan frissül az állapot (`text`) változásával, anélkül hogy manuálisan kellene kezelni az események hatásait.


#### **Előnyök:**

- Egyszerűbb kódstruktúra és kevesebb hiba lehetősége.
- Könnyebb karbantartani és skálázni nagy projekteket.
- Automatikus újrarenderelés állapotváltozások esetén.


#### **Hátrányok:**

- Kevésbé alkalmas finomhangolt kontrollt igénylő alkalmazásokhoz.
- A keretrendszer mögötti "mágia" nehezebben érthető lehet kezdők számára.
- Teljesítményproblémák léphetnek fel nagyobb adathalmazok vagy komplex reaktív rendszerek esetén.



### **Kulcsfontosságú különbségek**

| Tulajdonság | Imperatív UI | Deklaratív UI |
| :-- | :-- | :-- |
| **Megközelítés** | Hogyan érjük el az eredményt | Mit szeretnénk elérni |
| **Kontroll** | Teljes kontroll minden részlet felett | A keretrendszer kezeli a részleteket |
| **Állapotkezelés** | Manuális | Automatikus |
| **Kód mennyisége** | Több boilerplate kód | Kevesebb kód |
| **Reaktivitás** | Nem automatikus | Inherensen reaktív |
| **Olvashatóság** | Kevésbé olvasható | Könnyen olvasható |



### **Mikor használjunk imperatív vagy deklaratív megközelítést?**

#### Imperatív:

- Ha teljes kontrollra van szükség (pl. egyedi animációk vagy komplex interakciók).
- Ha finomhangolt teljesítményoptimalizációra van szükség.
- Ha egy régebbi technológiát használunk (pl. Android `UIKit`).


#### Deklaratív:

- Ha gyors fejlesztési időre van szükség.
- Ha fontos a kód olvashatósága és karbantarthatósága.
- Ha modern keretrendszereket használunk (pl. React, SwiftUI).



### Példák különböző technológiákban

| Technológia | Imperatív példák | Deklaratív példák |
| :-- | :-- | :-- |
| Android | Java + XML (Android Studio) | Jetpack Compose |
| iOS | UIKit | SwiftUI |
| Webfejlesztés | jQuery | React, Vue.js |

## **17. Cors and cors errors**

A **CORS (Cross-Origin Resource Sharing)** egy biztonsági mechanizmus, amely lehetővé teszi, hogy egy weboldal erőforrásokat kérjen le egy másik domain-ről (kereszt-domain kérések), miközben betartja a böngészők **same-origin policy** szabályát. A CORS hibák akkor fordulnak elő, ha a szerver nem megfelelően van konfigurálva a kereszt-domain kérések engedélyezésére.



 **Same-Origin Policy és CORS szerepe**

#### **Same-Origin Policy:**

- Ez egy böngészőbiztonsági szabály, amely megakadályozza, hogy egy weboldal hozzáférjen más domain-ről származó erőforrásokhoz.
- Az "origin" három részből áll: **protokoll**, **domain**, és **port**. Ha ezek közül bármelyik eltér, akkor más origin-ről van szó.


#### **CORS célja:**

- A CORS lehetővé teszi, hogy bizonyos kereszt-domain kérések biztonságosan végrehajthatók legyenek.
- A szerver válaszában speciális HTTP fejlécet (`Access-Control-Allow-Origin`) küld, amely meghatározza, hogy mely domainek férhetnek hozzá az erőforrásokhoz.



 **CORS működése**

1. **Origin fejléc:**
    - A böngésző minden kereszt-domain kéréshez hozzáad egy `Origin` fejlécet, amely tartalmazza a kérés forrásának domain-jét.
    - Példa:

```
Origin: http://example.com
```

2. **Szerver válasza:**
    - Ha a szerver engedélyezi az adott origin-t, akkor az `Access-Control-Allow-Origin` fejlécet küldi vissza.
    - Példa:

```
Access-Control-Allow-Origin: http://example.com
```

3. **Preflight kérések:**
    - Bizonyos esetekben a böngésző egy előzetes `OPTIONS` kérést küld a szervernek, hogy ellenőrizze, engedélyezett-e a kereszt-domain kérés.
    - A szerver válasza tartalmazza az engedélyezett HTTP metódusokat (`Access-Control-Allow-Methods`) és fejléc típusokat (`Access-Control-Allow-Headers`).



 **CORS hibák okai**

1. **Hiányzó vagy helytelen `Access-Control-Allow-Origin` fejléc:**
    - Ha a szerver nem küldi vissza ezt a fejlécet, vagy az origin nem egyezik meg a kliens domain-jével.
    - Hibaüzenet:

```
No 'Access-Control-Allow-Origin' header is present on the requested resource.
```

2. **Preflight kérés sikertelensége:**
    - Ha az `OPTIONS` kérésre adott válasz nem tartalmazza az elvárt CORS fejlécet.
    - Hibaüzenet:

```
Response to preflight request doesn't pass access control check.
```

3. **Két origin eltérése:**
    - Ha az origin (protokoll, domain vagy port) eltér a kliens és a szerver között.
4. **Nem megfelelő HTTP metódus vagy fejléc:**
    - Ha a szerver nem engedélyezi az adott HTTP metódust (`PUT`, `DELETE`, stb.) vagy egyedi fejléceket (pl. `Authorization`).
    - Hibaüzenet:

```
Method PUT is not allowed by Access-Control-Allow-Methods in preflight response.
```

5. **Hitelesítési problémák:**
    - Ha a kliens hitelesítési adatokat küld (`credentials: include`), de a szerver nem támogatja ezt.
6. **Nem HTTP protokoll használata:**
    - Ha az erőforrást nem HTTP/HTTPS protokollon keresztül próbálják elérni (pl. `file://` protokoll).



 **Példák CORS hibákra**

#### 1. Hiányzó `Access-Control-Allow-Origin`

- Kliens hibaüzenet:

```
Access to fetch at 'https://api.example.com/data' from origin 'http://localhost:3000' has been blocked by CORS policy.
```


#### 2. Preflight kérés sikertelensége

- Kliens hibaüzenet:

```
Response to preflight request doesn't pass access control check: No 'Access-Control-Allow-Headers' header is present on the requested resource.
```


#### 3. Nem megfelelő HTTP metódus

- Kliens hibaüzenet:

```
Method DELETE is not allowed by Access-Control-Allow-Methods in preflight response.
```




 **CORS hibák megoldása**

#### Szerveroldali megoldások:

1. **Helyes CORS fejlécek beállítása:**
    - Engedélyezni kell az adott origin-t:

```javascript
res.setHeader('Access-Control-Allow-Origin', 'http://example.com');
```

2. **Preflight kérések kezelése:**
    - Az `OPTIONS` metódusra adott válaszban meg kell adni az engedélyezett metódusokat és fejléceket:

```javascript
res.setHeader('Access-Control-Allow-Methods', 'GET, POST, PUT, DELETE');
res.setHeader('Access-Control-Allow-Headers', 'Content-Type, Authorization');
```

3. **Hitelesítési adatok engedélyezése:**
    - Ha hitelesítési adatok szükségesek (`credentials: include`):

```javascript
res.setHeader('Access-Control-Allow-Credentials', 'true');
```

4. **Wildcard használatának kerülése zárt API-k esetén:**
    - Nyilvános API-k esetén használható:

```javascript
res.setHeader('Access-Control-Allow-Origin', '*');
```

    - Zárt API-k esetén pontos origin-t kell megadni.

#### Kliensoldali megoldások:

1. Ellenőrizd, hogy a Fetch API vagy AJAX kéréseid helyesen vannak konfigurálva (pl. ne legyenek felesleges egyedi fejlécek).
2. Használj HTTPS protokollt mind kliens-, mind szerveroldalon.



### **Eszközök CORS hibák diagnosztizálására**

1. **Böngésző fejlesztői eszközök (DevTools):**
    - Ellenőrizd a hálózati kéréseket és válaszokat.
2. **Postman:**
    - Teszteld az API-kat közvetlenül CORS nélkül.
3. **CORS böngészőbővítmények:**
    - Ideiglenesen tilthatod a CORS szabályokat fejlesztés közben (nem ajánlott éles környezetben).

### **18. JavaScript Modulok**


A JavaScript modulok lehetővé teszik a kód logikai részekre bontását, hogy az könnyebben kezelhető, újrahasználható és karbantartható legyen. A modulok használatához az **`import`** és **`export`** kulcsszavakat alkalmazzuk. Az alábbiakban részletesen bemutatom, hogyan működnek a modulok.



### **Mi az a modul?**

- Egy **modul** egy JavaScript fájl, amely tartalmazhat változókat, függvényeket, osztályokat vagy más logikai egységeket.
- A modulok egymástól függetlenek, és csak explicit módon megosztott elemeket (exportokat) tudnak használni.
- A modulok segítségével a nagyobb programokat kisebb, kezelhetőbb részekre bonthatjuk.



### **Exportálás (Export)**

Az `export` kulcsszóval tehetünk elérhetővé változókat, függvényeket vagy osztályokat más modulok számára.

 **1. Named Export (Név szerinti exportálás)**

- Több elem is exportálható egy modulból név szerint.
- Az importáláskor meg kell adni az elemek pontos nevét.

**Példa:**

```javascript
// 📁 math.js
export function add(a, b) {
  return a + b;
}

export function subtract(a, b) {
  return a - b;
}
```

**Importálás:**

```javascript
// 📁 main.js
import { add, subtract } from './math.js';

console.log(add(2, 3)); // 5
console.log(subtract(5, 3)); // 2
```


 **Alias használata:**

Az importált elemek átnevezhetők alias segítségével:

```javascript
import { add as sum } from './math.js';
console.log(sum(2, 3)); // 5
```



 **2. Default Export (Alapértelmezett exportálás)**

- Egy modulnak csak egy alapértelmezett exportja lehet.
- Az importáláskor tetszőleges nevet adhatunk az alapértelmezett exportnak.

**Példa:**

```javascript
// 📁 cube.js
export default function cube(x) {
  return x * x * x;
}
```

**Importálás:**

```javascript
// 📁 main.js
import cube from './cube.js';

console.log(cube(3)); // 27
```



 **3. Exportálás közvetlenül deklarációval**

Az `export` kulcsszó közvetlenül használható a változók vagy függvények deklarációjánál:

```javascript
export const PI = 3.14;

export function multiply(a, b) {
  return a * b;
}
```



 **4. Re-export (Újraexportálás)**

Egy modul aggregátorként működhet más modulok exportjainak újraexportálására.

**Példa:**

```javascript
// 📁 moduleA.js
export const foo = 'foo';

// 📁 moduleB.js
export const bar = 'bar';

// 📁 index.js (aggregátor)
export { foo } from './moduleA.js';
export { bar } from './moduleB.js';
```

**Importálás aggregált modulból:**

```javascript
import { foo, bar } from './index.js';
console.log(foo); // 'foo'
console.log(bar); // 'bar'
```



### **Importálás (Import)**

Az `import` kulcsszóval érhetjük el más modulok által exportált elemeket.

 **1. Named Import (Név szerinti importálás)**

Az exportált elemeket név szerint kell importálnunk:

```javascript
import { add, subtract } from './math.js';
```


 **2. Default Import (Alapértelmezett importálás)**

Az alapértelmezett exportot tetszőleges néven importálhatjuk:

```javascript
import cube from './cube.js';
```


 **3. Namespace Import (Névtér importálása)**

Az összes exportált elemet egy objektumba gyűjthetjük:

```javascript
import * as math from './math.js';

console.log(math.add(2, 3)); // 5
console.log(math.subtract(5, 3)); // 2
```


 **4. Side Effect Import (Mellékhatások miatt történő importálás)**

Egy modult csak annak mellékhatásai miatt is importálhatunk anélkül, hogy konkrét elemeket használnánk belőle:

```javascript
import './polyfill.js'; // A polyfill globális változókat ad hozzá.
```



 **Modulok viselkedése**

1. **Saját hatókör:** Minden modul saját hatókörrel rendelkezik; az egyik modulban deklarált változók nem érhetők el automatikusan másikban.
2. **Egyszeri betöltés:** Egy modult csak egyszer tölt be a böngésző vagy futtatókörnyezet; az exportált értékek megosztottak a különböző importáló helyek között.
3. **Strict Mode:** A modulok automatikusan `use strict` módban futnak.



### **Modulok használata böngészőben**

A böngészőkben a modulokat `&lt;script type="module"&gt;` címkével kell betölteni:

```html
&lt;script type="module" src="main.js"&gt;&lt;/script&gt;
```


**Modul-specifikus viselkedés böngészőkben:**

- A szkriptek alapértelmezetten aszinkron töltődnek be (`deferred`).
- Kereszt-domain kérésekhez CORS-támogatás szükséges.



### **Modulok bundlingje**

A nagyobb projektekben gyakran használnak bundlereket (pl. Webpack, Rollup), hogy több modult egyetlen fájlba kombináljanak a teljesítmény javítása érdekében.


### **Összegzés**

| Funkció | Named Export/Import | Default Export/Import |
| :-- | :-- | :-- |
| Szintaxis | `export { name };` | `export default name;` |
| Import szintaxis | `import { name } from './file.js';` | `import name from './file.js';` |
| Több elem | Egyszerre több elem exportálható | Csak egy alapértelmezett elem |
| Alias használata | Lehetséges (`as`) | Nem szükséges |