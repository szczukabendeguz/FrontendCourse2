# Frontend Course 2 - Study Materials

A personal learning repository containing comprehensive study notes and practice materials for frontend development, focusing on **JavaScript**, **TypeScript**, and **Angular**.

> **Note:** This repository is primarily for personal study purposes. Materials are based on the excellent teaching of [Sipos Miklós](https://github.com/siposm) - thank you for the outstanding content delivery! 🙏

## ⚠️ Language Note

**Please note:** Most materials in this repository are written in **Hungarian** (Magyar). If you're reading this and don't speak Hungarian, be prepared for mixed-language content.

---

# Frontend Course 2 - Tanulási Anyagok

Személyes tanulási repository, amely átfogó jegyzeteket és gyakorlati anyagokat tartalmaz frontend fejlesztéshez, **JavaScript**, **TypeScript** és **Angular** témakörökben.

> **Megjegyzés:** Ez a repository elsősorban személyes tanulási célokat szolgál. Az anyagok [Sipos Miklós](https://github.com/siposm) kiváló oktatására épülnek - köszönöm a kiváló tartalomátadást! 🙏

## 📚 Tartalom Áttekintés

Ez a repository kurzusjegyzeteket és gyakorlati anyagokat tartalmaz **magyar** nyelven, különböző frontend fejlesztési témákban.

### Tanulási Jegyzetek & Dokumentáció

| Fájl | Téma | Leírás |
|------|------|--------|
| `Angular2.md` | Angular 2 Kurzusjegyzetek | Átfogó jegyzetek Angular komponensekről (I/O, ViewChild, Content Projection), lifecycle hookokról, authentication-ről, routing-ról és még sok másról (85KB) |
| `js1-kerdesek.md` | JavaScript Interjúkérdések | JavaScript koncepciók és interjúkérdések gyűjteménye alapoktól a haladó témákig |
| `typescript_round_two.md` | TypeScript Haladó | TypeScript haladó koncepciók és minták |
| `typscript_angular_1.md` | TypeScript & Angular Alapok | Bevezetés a TypeScript és Angular integrációba |
| `ZH tapasztalatok.md` | Vizsgatapasztalatok | Jegyzetek és tapasztalatok a kurzus vizsgáiról |
| `zh_help_me_remember.md` | Tanulási Emlékeztetők | Gyors referencia és memóriasegédletek vizsgafelkészüléshez |
| `Átfogó jegyzet a JavaScript működéséről és webes t.md` | Átfogó JavaScript Útmutató | Mélyreható jegyzetek JavaScript mechanikákról és webes technológiákról |

### Gyakorlati Kód

| Fájl | Leírás |
|------|---------|
| `index.html` | HTML Elemek Demo - Gyakorló oldal különböző HTML elemek bemutatására (formok, táblázatok, listák, navigáció) |
| `style.css` | A demo oldal stíluslapja CSS változókkal, reszponzív designnal és komponens-alapú stílusokkal |

## 🎯 Érintett Témák

### JavaScript
- **Alapok:** Változók (var/let/const), hoisting, hatókör, típusok, típuskonverzió
- **Függvények:** this binding, arrow function-ök, konstruktorok, IIFE
- **Objektumok:** Prototípusok, öröklés, property descriptor-ok, shallow/deep copy
- **Aszinkron:** Event loop, Promise-ok, async/await, microtask vs macrotask
- **Modulok:** ES Module vs CommonJS, bundling, tree shaking
- **Browser API-k:** DOM/BOM, event delegation, capturing/bubbling
- **Teljesítmény:** Memóriakezelés, garbage collection, debouncing/throttling
- **Biztonság:** XSS, CSRF, CORS, Clickjacking
- **Haladó:** Iterator-ok, generator-ok, Proxy, Reflect, WeakMap/WeakSet

### TypeScript
- Típusrendszer és típusannotációk
- Interface-ek és haladó típusok
- Angular integráció

### Angular
- **Komponens Kommunikáció:**
  - `@Input` / `@Output` dekorátorok
  - `@ViewChild` szülő-gyermek interakcióhoz
  - Content Projection `<ng-content>` használatával
- **Lifecycle Hook-ok:**
  - Létrehozás: `constructor`
  - Change Detection: `ngOnInit`, `ngOnChanges`, `ngDoCheck`
  - Content: `ngAfterContentInit`, `ngAfterContentChecked`
  - View: `ngAfterViewInit`, `ngAfterViewChecked`
  - Rendering: `afterNextRender`, `afterEveryRender`
  - Megsemmisítés: `ngOnDestroy`
- **Authentication:** Token-alapú auth, route guard-ok (`canActivate`), localStorage
- **Routing:** Route konfiguráció, navigáció, védett route-ok
- **Service-ek:** Dependency injection, singleton minta, IOC container-ek

## 🛠️ Tech Stack

[![Tech Stack](https://skillicons.dev/icons?i=html,css,js,ts,angular)](https://skillicons.dev)

## 🙏 Köszönetnyilvánítás

Külön köszönet **[Sipos Miklós](https://github.com/siposm)** oktatónak a kiváló tananyagokért és a kurzus leadásáért. Az ebben a kurzusban megosztott tudás felbecsülhetetlen értékű volt.


**Happy Learning! / Jó Tanulást!** 🚀📖
