Az alábbi 50 elméleti kérdés-válasz páros általános JavaScript és webes működési ismereteket fed le, mivel a hivatkozott GitHub-oldal tartalma jelenleg nem érhető el közvetlenül; ha szükséges, a kérdéslistát pontosítható a saját jegyzet szövegéhez igazítva. 

### Alapfogalmak

- Mi a különbség a statikus és dinamikus típusosság között JavaScriptben?
  A JavaScript dinamikusan típusos nyelv, tehát a változók típusa futásidőben dől el, és egy változó különböző időpontokban különböző típusú értéket is kaphat. 

- Mit jelent, hogy a JavaScript prototípus-alapú?
  Az objektumok más objektumoktól örökölnek egy prototípusláncon keresztül, nem osztályok klasszikus hierarchiáján; a metódusok és tulajdonságok feloldása a prototípuslánc mentén történik. 

- Mi az ECMAScript és hogyan viszonyul a JavaScripthoz?
  Az ECMAScript a nyelvi szabvány, amelyet a JavaScript implementál; a különböző ECMAScript kiadások (pl. ES6/ES2015) határozzák meg az új nyelvi funkciókat. 

- Mit jelent a „strict mode” és hogyan kapcsolható be?
  A "use strict" direktívával bekapcsolt szigorú mód szigorúbb hibadetektálást és biztonságosabb szintaxist ad (pl. néma hibák kiváltása kivétellé). 

- Mi az a JavaScript futásidejű környezet?
  A környezet biztosítja a motor (pl. V8), a Web API-k (böngészőben), és a host-objektumok (pl. window, document) elérhetőségét és végrehajtási modellt. 

### Változók és hatókör

- Miben különbözik a var, let és const?
  A var függvény-szintű hatókörű és hoistingolt, a let/const blokk-szintű és időbeli halott zónával rendelkezik; a const újraértékadását tiltja. 

- Mi az a hoisting?
  A deklarációk a hatókör tetejére kerülnek logikailag; var és függvénydeklarációk érintettek, míg let/const a TDZ miatt nem használható deklaráció előtt. 

- Mi a blokk-szintű hatókör?
  A kapcsos zárójelek közötti kódblokk külön hatókört képez let/const változók számára; a var továbbra is függvény-szintű. 

- Mi az időbeli halott zóna (TDZ)?
  A let/const változók a deklarációs sorukig nem hozzáférhetők, még ha a blokk elején hoisting megtörtént is. 

- Mi a különbség a globális objektum és a modulok között?
  Script módban a felső szintű this a globális objektumra mutathat, míg modulok izolált modul-hatókörrel és strict móddal futnak implicit. 

### Típusok és konverzió

- Mik az alapvető primitív típusok?
  String, Number, BigInt, Boolean, null, undefined, Symbol; minden más objektum típusnak számít. 

- Mi a különbség null és undefined között?
  Az undefined a deklarált, de értéket nem kapott változó „nincs érték” állapota; a null szándékos üres érték. 

- Hogyan működik a laza (==) és szigorú (===) egyenlőség?
  A === típuskonverzió nélkül hasonlít össze, míg a == konverziót végez, ami meglepő eredményeket adhat. 

- Mit csinál a Number.isNaN vs isNaN?
  A Number.isNaN csak a NaN-t azonosítja, míg az isNaN előbb számmá konvertál, így szélesebb körben igaz lehet. 

- Mi a különbség a Number és BigInt között?
  A Number IEEE-754 dupla pontosságú lebegőpontos, a BigInt egész számokat kezel tetszőleges pontossággal, de nem keverhető Numberrel műveletben. 

### Függvények és this

- Hogyan kötődik a this értéke?
  A this értéke a hívási kontextustól függ (metódushívás, call/apply/bind, new, nyílfüggvény lexikális this). 

- Mi a különbség a normál és a nyílfüggvény között?
  A nyílfüggvény nem rendelkezik saját this/arguments/bind-olhatósággal, és a környező lexikális this-t használja. 

- Mire jó a Function.prototype.bind?
  Visszaad egy új függvényt rögzített this-szel és opcionálisan előre rögzített argumentumokkal részleges alkalmazáshoz. 

- Mi a konstruktor függvény és a new operátor szerepe?
  A new létrehoz egy új objektumot, beállítja a prototípust és meghívja a konstruktort a this-szel a példány inicializálására. 

- Mi az IIFE és miért használják?
  Azonnal meghívott függvénykifejezés izolált hatókört ad, régebben névütközések elkerülésére használták modulok előtt. 

### Objektumok és prototípusok

- Hogyan működik a prototípuslánc?
  Tulajdonságkeresés először a saját tulajdonságokon, majd a [[Prototype]] láncon felfelé halad a null prototípusig. 

- Mi a különbség az own property és a prototype property között?
  Az own property közvetlenül az objektumon van, míg a prototype property a prototípuson érhető el örökléssel. 

- Mire szolgál az Object.create?
  Új objektumot hoz létre megadott prototípussal, így finoman szabályozható az öröklés. 

- Mi az a property descriptor?
  Meghatározza egy tulajdonság írás/olvasási és enumerálhatósági beállításait, illetve getter/setter viselkedését. 

- Mi a különbség a shallow és deep copy között?
  A sekély másolat csak a felső szintet másolja, a beágyazott objektum referenciák megmaradnak; a mély másolat rekurzívan másol. 

### Aszinkron modell

- Mi az eseményciklus (event loop)?
  A JavaScript egyetlen szálon fut, az event loop kezeli a call stacket és az üzenetsorokat a feladatok ütemezéséhez. 

- Miben különbözik a makró- és mikrotask queue?
  Makrotaskok pl. setTimeout, I/O; mikrotaskok pl. Promise.then és MutationObserver, melyek előbb futnak ütemezéskor. 

- Mit jelent a non-blocking I/O?
  A hosszú műveleteket a host környezet kezeli háttérben, és később callback-kel tér vissza blokkolás nélkül. 

- Mi a Promise állapotgépe?
  A Promise pendingből resolved (fulfilled) vagy rejected állapotba kerül, és állapotváltás után immutábilis. 

- Mi a különbség az async/await és a then-chaining között?
  Az async/await szintaktikus cukor a Promise-ra, lineáris kódstílussal; a then-chaining explicit láncolást használ. 

### Modulok és csomagkezelés

- Mi a különbség az ES modulok és a CommonJS között?
  ES modulok statikus import/export, top-level await támogatás; CommonJS dinamikus require/module.exports Node-ban. 

- Mi az a tree shaking?
  A statikusan elemezhető modulimportokból a használaton kívüli exportok eltávolítása build időben a kisebb bundle érdekében. 

- Mi a side-effect és hogyan jelöljük?
  A modul betöltésekor futó, külső állapotot érintő kód; a package.json "sideEffects" mező segít a bundlereknek. 

- Mi a bundler és miért használjuk?
  Eszköz (pl. Webpack, Rollup, Vite) a modulok összefűzésére, transzpilálására, optimalizálására produkciós célra. 

- Mi a transzpilálás (Babel)?
  Új nyelvi funkciók visszafordítása régebbi runtime-okkal kompatibilis kóddá, polyfillekkel kiegészítve szükség esetén. 

### Böngésző API-k

- Mi a DOM és hogyan különbözik a BOM-tól?
  A DOM a dokumentum objektummodell, a BOM a böngésző környezeti objektumai (window, history, location). 

- Hogyan működik az eseménydelegálás?
  A buborékoló eseményeket egy szülő elemre hallgatva kezeljük, így kevesebb listener és dinamikus elemek támogatása érhető el. 

- Mi a capturing és bubbling fázis?
  Az esemény lefelé halad (capturing), majd felfelé buborékol (bubbling); a listener opcióval szabályozható a fázis. 

- Mi a difference az innerHTML és textContent között?
  Az innerHTML HTML-t is értelmez és beilleszt, a textContent csak sima szöveget ír be XSS kockázat nélkül. 

- Mi az a Shadow DOM?
  Izolált DOM-fa komponensekhez kapszulációval és stílus-izolációval, webkomponensek alapja. 

### Teljesítmény és memóriamodell

- Mi a garbage collection alapelve?
  A nem elérhető objektumok memóriája felszabadul; elérhetőség-analízist alkalmaz a motor (mark-and-sweep). 

- Mi az a memory leak tipikus oka?
  Feleslegesen élő referenciák (globálok, cache, lezárások), eseménykezelők le nem választása, detached DOM. 

- Hogyan mérhető a teljesítmény böngészőben?
  Performance API, Lighthouse, devtools profiler, időbélyeg és mark/measure használatával. 

- Mi a debouncing és throttling?
  Debounce késlelteti a hívást inaktív időablakig; throttle rögzíti a hívások maximális gyakoriságát időegységenként. 

- Mi az immutabilitás előnye?
  Könnyebb állapotkövetés, kevesebb mellékhatás, optimalizálható összehasonlítások (pl. referenciaváltozás-alapú diff). 

### Biztonság

- Mi az XSS és hogyan védekezünk ellene?
  Kódbefecskendezés, amikor nem biztonságosan jelenítünk meg felhasználói inputot; escaped output és CSP használata szükséges. 

- Mi a CSRF és a védekezés?
  Kereszt-eredetű kérések hamisítása; védelem: same-site cookie, CSRF token, origin/Referer ellenőrzés. 

- Mi a CORS lényege?
  Eredetközi erőforrás-megosztás szabályozása válaszfejlécekkel; preflight OPTIONS kérés bizonyos esetekben. 

- Mi az a Clickjacking és védekezés?
  Láthatatlan iframe-be ágyazott felület manipulációja; védelem: X-Frame-Options, CSP frame-ancestors. 

- Mi a Samesite cookie attribútum?
  Meghatározza, mikor küldhető cookie cross-site kérésekkel (Lax/Strict/None + Secure). 

### Haladó nyelvi témák

- Mi az iterátor és iterálható protokoll?
  Iterátor: next() interfész; iterálható: [Symbol.iterator] megvalósítással használható for..of és spread esetén. 

- Mi a generator függvény előnye?
  Szabályozható végrehajtás yield pontokkal, lazy szekvenciák és kooperatív aszinkron minták támogatására. 

- Mi a proxy és mire használható?
  Object Proxy handler csapdákkal (get/set/has) metaprogramozáshoz, loggolásra, validációra, virtualizációra. 

- Mi az a Reflect API szerepe?
  Csapdák alapműveleteinek standardizált elérése; proxy műveletek konzisztens implementálására szolgál. 

- Mi a WeakMap/WeakSet különlegessége?
  Gyenge referenciák kulcsként objektumokra, garbage collector felszabadíthatja elemeket, nem iterálhatók. 

Megjegyzés: a kérdés-válaszok testreszabhatók a konkrét jegyzet fejezeteihez, ha a tartalom elérését sikerül biztosítani vagy a fájl szövegét ide beillesztve pontosítható.

Sources
