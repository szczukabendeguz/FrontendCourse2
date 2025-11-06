# Angular2 1.hét 1.óra

## TANANYAG: menetrend

6. hét konzultáció
7. hét cs-p szünet
8. hét 1.zh elméleti+gyakorlat
11. hét rektori hét szünet
12. hét 2.zh + elméleti+gyakorlat, de lehet hogy ez főként elméleti lesz
13. konzultáció
14. pót zh
Nincs féléves feladat

10:30-tól fog kezdődni az óra

## TANANYAG: environments

Eddig ezeket használtuk:
```cmd
ng new appname --standalone-false
ng g s ...
ng g c ...
ng g class ...
```

Most bevezetünk egy újat:
```cmd
ng g environments
```
Ide szervezzük ki pl az api url-t és az api kulcsokat

# Angular 2. hét, 2. óra
 
## TANANYAG: Ismétlés

### Mobile first vs Desktop first
Ha M.F.-ben elsőnek megnyitjuk telefonos nézetben és elkészítjük a megfelelő css fájlt. De amikor átmegyünk desktopra akkor nem fog jól kinézni
- "A" opció, hogy így ahhoz készítünk egy külön css-t, és js ami le tudja kérni a kijelző méretét, eldönti, hogy melyik css kell
- "B" opció, hogy media query-kel ugyanabban a css fájlban megírjuk a desktopra megfelelő css-t

**css box model:** *`tartalom -> padding -> border -> margin`* (belülről kifele, mint egy hagyma)
 

## TANANYAG: [komponensek haladó szintű kezelése](https://github.com/siposm/bprof-frontend-weekly/tree/master/angular/angular-component-io)

```bash
ng new angular-componenet-io --standole=false
```

### Megnézzük az input-output kezelést

```bash
ng g c parent
ng g c child
```

> A komponensek ugyanannyira univerzálisan felhasználható mint pl c#-ban egy osztály


### @Input - @Output:
__Input:__ Amikor a parent komponensbe belerakjok a child komponenst, akkor a child komponensbe bele tudunk olyan elemeket rakni amik a parent komponenesben találhatóak meg.

__Output:__ A child komponensben van egy gomb de azt szeretnémhogy a parent komponsensen történjen valami, és egy ottani függvény fusson le.

---
`MyObject class`:
```ts MyObject class
export class MyObject {
  content: string = ""
  priority: number = 0
  constructor(content: string = "", priority: number = 0) {
    this.content = content
    this.priority = priority
  }
}
```
---
`ts parent:`
```ts parent
dataItems: MyObject[] = []
constructor() {
    this.dataItems.push(new MyObject("alma", 3))
    this.dataItems.push(new MyObject("körte", 5))
    this.dataItems.push(new MyObject("szilva", 10))
    this.dataItems.push(new MyObject("barack", 2))
}
hello(message: MyObject): void {
    console.log(message)
}

```
---
`html parent:`
```html parent
<div>
    <h1>PARENT</h1>
    <app-child *ngFor="let item of dataItems"
        [item]="item"
        (message)="hello($event)"
    ></app-child>
</div>
```
---
`ts child:`
```ts child
  @Input() item: MyObject = new MyObject()
  @Output() message: EventEmitter<MyObject>= new EventEmitter<MyObject>()

  childHello(): void {
    this.message.emit(this.item)
  }
```
---
`html child:`
```html child
<div>
    <h5>{{ item.content }} - {{ item.priority }}</h5>
    <button (click)="childHello()">Child says hello</button>
</div>
```

---

![input-output.png](https://github.com/oli-tolnai/Angular2/blob/main/kepek/input-output.jpg)


Ezekkel lehetőségünk van például a bootstrap cardokhoz hasonlóakat csinálni. Létrehozhatunk egy sablon komponenst, aminek a tulajdonságait egy másik komponensen belül adjuk meg. Erre példa az [angular-button-component](https://github.com/siposm/bprof-frontend-weekly/tree/master/angular/angular-button-component), ahol van egy `button` komponensünk, amit beleillesztünk az `app` komponensbe, ahol megadjuk neki, hogy mi legyen a felirat, milyen stílusú legyen stb. És ehhez elegendő nekünk az `@Input`-ot használni

# Angular2 3.hét 3.óra

## TANANYAG: [Viewchild](https://github.com/siposm/bprof-frontend-weekly/tree/master/angular/viewchild)

**Folytatjuk azt a témát ahol azt nézzük át, hogyan tudnak komponensek kommunikálni, és adatokat átadni egymás között**

![angular2_3_1_uj.png](https://github.com/oli-tolnai/Angular2/blob/main/kepek/angular2_3_1_uj.png)

**1.) I/O komponens** <br>
Előző órán tanultuk az `I/O`-t a komponenseknél. Ahol például az `@Input` használatánál a szülő komponens csak annyit tud, hogy van  egy változó a gyermek komponensben aminek át tud adni értéket. Tehát az A komponens ad valamit a B komponensnek, de az A nem tudja hogy a B mit fog azzal csinálni, és a B komponens sem tudja hogy az A komponens mire való és mit csinál.

![angular2_3_InputOutput](https://github.com/oli-tolnai/Angular2/blob/main/kepek/angular2_3_InputOutput.png)

**2.) viewchild** <br>
Másik módszer a `viewchild` használata. Itt a szülő komponens teljes rálátást kap a gyermek komponensre.  
Teháát az A komponens teljes mértékben eléri a B-t (körülölei)

![`angular2_3_viewchild`](https://github.com/oli-tolnai/Angular2/blob/main/kepek/angular2_3_viewchild.png)

Ennek bemutatásához készítünk egy card komponenst, amit `"template"`-ként tudunk majd használni.

<br>

`ts card.component.ts:`
```ts card.component.ts
export class CardComponent {

  message: string = "Lorem ipsum dolor sit amet"
  secret: string = "valami titkos üzenet"

  changeMessage(): void {
    this.message = "**NEW CONTENT**"
  }
}
```
<br>

`html card.component.html:`
```html card.component.html
<p>{{message}}</p>  
```

>Létrehoztuk a card komponenst, ami kiír egy üzenetet ami a `message` változóban van. A `secret` változót csak azért hoztuk létre, hogy lássuk, hogy a szülő komponenst azt is eléri majd. Emellett egy `changeMessage()` metódust is csináltunk ami megváltoztatja az üzenet tartalmát  
---
<br>

> Alábbi példakód a **template reference** változók és a **@ViewChild dekorátor** használatát mutatja be, amelyek lehetővé teszik a szülő komponens és gyermek komponens közötti közvetlen kommunikációt.


`ts app.component.ts:`
```ts app.component.ts
export class AppComponent {
  
  @ViewChild("card") cardComp !: CardComponent

  update(): void {
    console.log(this.cardComp.secret)
    this.cardComp.changeMessage()
  }
```
>A TypeScript fájlban a `@ViewChild("card")` dekorátor egy hivatkozást hoz létre a gyermek komponens példányára. A dekorátor paraméterként a `"card"` stringet kapja, ami megfelel a HTML sablonban definiált `#card` template reference változónak. A `cardComp` tulajdonság fogja tárolni a tényleges `CardComponent` példány hivatkozását, miután az Angular inicializálta azt.

>Az `update()` metódus bemutatja a közvetlen szülő-gyermek kommunikációt azáltal, hogy hozzáfér a gyermek komponens tulajdonságaihoz és metódusaihoz. Kiírja a gyermek komponens `secret `tulajdonságát a konzolra, és meghívja a gyermek `changeMessage()`metódusát. Ez demonstrálja, hogy a `@ViewChild` hogyan teszi lehetővé a szülő számára, hogy programozottan interakcióba lépjen a gyermek komponenssel.

<br>

`html app.component.html:`
```html app.component.html
<h1>App component</h1>

<button (click)="update()">Update</button>

<app-card #card></app-card>
```

>A HTML sablonban a `<app-card #card></app-card>` elem létrehozza a gyermek komponenst és hozzárendeli a `#card` template reference változót. Ez a referencia változó az, ami összeköti a gyermek komponens példányát a TypeScript kódban lévő `@ViewChild` dekorátorral. A gomb click eseménye az update() metódushoz van kötve, így interaktív módon lehet kiváltani a szülő-gyermek kommunikációt.

 

**Kérdés**: <br>
*Melyiket érdemes használni? Az `I/O` vagy a `viewchild` a jobb?* <br>
Összességében ha lehet, inkább `I/O`-t használjunk, ugyanis az átláthatóbb, és professzionálisabb. A `viewchild` használata során könnyebben alakulhat ki káosz.








## TANANYAG: [Content-projection](https://github.com/siposm/bprof-frontend-weekly/tree/master/angular/content-projection)

**Content-projection** egy harmadik mód lesz a komponensek közötti kommunikációra, az eddig tanult I/O és viewchild-on kívül. <br>
Ennek az a lényege, hogy pl a `card` komponensen belül van egy olyan hogy `ng-content`, ami azért speciális mert van benne egy selector, ami abba a komponensbe fog föl referálni ahol meghívjuk ezt a komponenst, tehát a példánkban most az app komponsensbe.

_Azért ez a neve, mert a tartalom fönt van definiálva és az bele van projektálva a lentebbi részbe_

A **Content-projection** sablon építésre lesz jó, és a fókusz most főleg a `html`-en és a `css`-en lesz.

<br>

`card.component.html:`
```html card.component.html
<div>
    <h1><ng-content select="[title]"></ng-content></h1>
    <h5><ng-content select="[year]"></ng-content></h5>
    <p><ng-content select="[intro]"></ng-content></p>
</div>
```

> A `ng-content` egy speciális Angular direktíva, amely lehetővé teszi a tartalom beillesztését egy komponens sablonjába. Ez a direktíva helyőrzőként működik, amelybe a szülő komponensből származó tartalom kerül beillesztésre. A `select` attribútum segítségével meghatározhatjuk, hogy mely elemek kerüljenek beillesztésre az adott helyőrzőbe.


<br>

`card.component.sass:`
```css card.component.sass
div
    width: 300px
    border: 5px solid red
    border-radius: 10px
    padding: 10px 30px
    margin: 0 auto
    margin-bottom: 5px
    text-align: center
```

> A `card.component.sass` fájlban a stílusokat definiáljuk a card komponens számára. A `div` elemre vonatkozó stílusok meghatározzák a szélességet, a keretet, a lekerekített sarkokat, a belső és külső margókat, valamint a szöveg igazítását. A `margin: 0 auto` középre igazítja a komponenst vízszintesen, emellett minden margint felülír, ezért külön meg kell adni a `margin-bottom` értékét is.

---


Csinálunk egy movie osztályt is:
<br>

`movie.ts:`
```ts movie.ts
export class Movie {
    title: string = ""
    year: number = 0
    intro: string = ""

    constructor(title: string = "", year: number = 0, intro: string = "") {
        this.title = title
        this.year = year
        this.intro = intro
    }
}
```

> Ez egy egyszerű TypeScript osztály, amely egy filmet reprezentál három tulajdonsággal: `title`, `year` és `intro`. 


<br>

`app.component.ts:`
```ts app.component.ts
export class AppComponent implements OnInit {
  movies: Movie[] = []

  ngOnInit(): void {
    this.movies.push(
      new Movie("The Matrix", 1999, "Lorem ipsum dolor sit amet..."),
      new Movie("Inception", 2010, "Lorem ipsumamet..."),
      new Movie("Interstellar", 2014, "Lorem ipsum dolor sit ipsum dolor sit ipsum dolor sit amet..."),
      new Movie("The Dark Knight", 2008, "Lorem ipsum dolor ..."),
    )
  }
}
```

> Egy `movies` nevű tömböt hozunk létre, ami `Movie` objektumokat tartalmaz. Az `ngOnInit()` életciklus metódusban feltöltjük a tömböt néhány példányosított `Movie` objektummal. `ngOnInit()` helyett konstruktort is használhatnánk.

<br>
A card komponenst beillesztjük az app komponensbe:

`app.component.html:`
```html app.component.html
<app-card *ngFor="let item of movies">
  <div title>
    <u>
      <i>
        {{ item.title }}
      </i>
    </u>
    <span *ngIf="item.year > 2010" style="background-color: aqua;">*</span>
  </div>
  <div year>{{item.year}}</div>
  <div intro>{{item.intro}}</div>
</app-card>
```

> Itt a `*ngFor` direktívával iterálunk a `movies` tömb elemein, és minden egyes filmhez létrehozunk egy `app-card` komponenst. A `div` elemekben a `title`, `year`, és `intro` attribútumokat használjuk, hogy a megfelelő tartalmat átadjuk a `card` komponensnek a `ng-content` segítségével. Az `*ngIf` direktíva pedig feltételesen jelenít meg egy csillagot, ha a film éve nagyobb, mint 2010.


> Content-projection fontos része még, hogy nem csak egyszerűen tudunk átadni dolgokat hanem tudunk extrázni, pl a title-nél meg tudjuk azt csinálni. hogy nem csak nyersen a tartalmat adhatjuk át, hanem stílust is, mert mindent át ad ami a selectoros div-en belül van.
Tehát a div-en belül ha még adunk neki félkövéret, dölt stílust stb. akkor azok is mind átkerülnek.
<br> **Teljes html kódokat bele lehet projektálni nem csak a tartalmat.**








## TANANYAG: templateRef és viewcontainerRef
Ezt a két dolgot nem tanuljuk részletesebben, de igény szerint utána lehet nénzi.

A **TemplateRef** egy Angular template (sablon) hivatkozását jelenti - gyakorlatilag egy tervrajzot, amiből nézetek (view-k) hozhatók létre. Ez egy beágyazott sablon, ami többször példányosítható különböző view példányok létrehozására.

A **ViewContainerRef** ezzel szemben egy tárolót jelent, ahol egy vagy több nézet csatolható. Gondolhatunk rá úgy, mint egy helyfoglalóra a DOM-ban, ahová az Angular dinamikusan beszúrhat, eltávolíthat vagy manipulálhat nézeteket.

> Mind a TemplateRef, mind a ViewContainerRef a **@ViewChild dekorátort** használja a háttérben. Ez logikus, mivel a @ViewChild az Angular elsődleges mechanizmusa arra, hogy hivatkozásokat kapjunk template elemekre, komponensekre vagy direktívákra. Amikor dinamikusan szeretnénk manipulálni sablonokat vagy tárolókat, általában először @ViewChild segítségével kell rájuk hivatkozást szereznünk.








## TANANYAG: [Életciklusok `lifecycle`](https://github.com/siposm/bprof-frontend-weekly/tree/master/angular/lifecycles)

> Az életciklusok azok a pontok egy komponens életében, amikor az Angular értesíti a komponenst, hogy valami fontos dolog történt vele. Ezeket úgy kell elképzelni, mint eseményeket vagy állapotváltozásokat, amelyek során a komponens különböző metódusokat hív meg.

**Az életciklusokat és a hozzájuk tartozó metódusokat interfészeken keresztül tudjok elérni.**


Eddig mikor seed adatokat akartunk létrehozni akkor konstruktort használtunk, de sokkal jobb helyük van az `ngOnInit()`-ben. 

Az alábbi honlapon megtalálhatóak milyen életciklusok vannak: [angular lifecycle](https://angular.dev/guide/components/lifecycle).
Azonban itt van a magyarra lefordított változat is: 

# Lifecycle hooks

| **Fázis** | **Metódus neve** | **Mikor fut le** | **Tipikus Példa** |
| --- | --- | --- | --- |
| **Creation** | `constructor` | Lefut, amikor Angular példányosítja a komponenst.  | Szolgáltatás injektálása, property-k alapértékre állítása.    |
| **Change Detection** | `ngOnInit`   | Egyszer fut le, miután az összes input inicializálva lett.   | Kezdeti adatbetöltés, API-hívás indítása, form alapállapotának felépítése, egyszeri inicializálás.    |
|  | `ngOnChanges` | Minden alkalommal lefut, amikor egy `@Input` értéke megváltozik (az első beállításkor is). | Input alapján belső állapot frissítése (pl. számított mező kiszámítása, log transform).   |
|  | `ngDoCheck`  | Minden change detection ciklusban lefut.   | Saját, optimalizált változásdetektáló logika írása (pl. nagy listák diffelése, teljesítmény-optimalizáció).  |
|  | `ngAfterContentInit`  | Egyszer fut, miután a projectált tartalom (`<ng-content>`) inicializálva lett.| Ellenőrzés, hogy a kötelező projected content tényleg bekerült-e (pl. slot-validáció).   |
|  | `ngAfterContentChecked` | Minden content change detection után lefut.  | Projectált tartalom figyelése, amikor belső logikát kell futtatni content-változáskor.   |
|  | `ngAfterViewInit`    | Egyszer fut, miután a komponens nézete és a gyerek komponensek nézete inicializálódott.  | DOM-méretek lekérése, 3rd-party UI lib inicializálása, `@ViewChild` komponens meghívása.  |
|  | `ngAfterViewChecked`  | Minden view change detection után lefut.   | Layout finomhangolása, animáció elindítása a DOM végleges állapota után. (Óvatosan használni, nehogy végtelen ciklust okozzon!) |
| **Rendering**    | `afterNextRender`    | Egyszer fut, amikor a teljes DOM render befejeződött. | Egyedi mérés vagy animáció, amihez a teljes oldalt készen kell látni (pl. scroll pozíció beállítása).|
|  | `afterEveryRender`   | Minden DOM render után lefut.    | Globális UI-szinkron (pl. sticky header pozíció frissítése minden render után).  |
| **Destruction**   | `ngOnDestroy` | Egyszer fut, mielőtt a komponens megsemmisül. | Subscribek leiratása, interval/timeouts leállítása, DOM események leválasztása.  |

_Az `ngOnInit`-et lehetne a creationbe is rakni, de a changedetectionbe van._

Az alábbi képen azt is láthatjuk hogy milyen sorrendben futnak le:
![lifecycle sorrend](https://github.com/oli-tolnai/Angular2/blob/main/kepek/angular2_3_lifecycle-hooks.png)


*Alapvetően a constructor nem egy hook mint a többi.*


---
### Most megnézünk párat, amiket fontos tudni.

Ehhez 3 komponenst készítünk: A, B és child és még egy stringContent classt is.

> *Fontos most megemlíteni, de később majd részletezzük hogy a lifecycle-ben, hogy az ngFor-nak más a viselkedése, hogy ha objektumon hívjuk meg mintha csak egy primitív típuson hívnánk meg. Éppen ezért mi most készíteni fogunk egy `string-content` osztályt*

<br>

`string-content.ts:`
```ts string-content.ts
export class StringContent {
    content: string = ""
    constructor(content: string = "") {
        this.content = content
    }
}
```

<br>

app-routingba megyünk és beállítjuk a routingot hogy az A és B komponens között tudjunk váltani

`app-routing.module.ts:`
```ts app-routing.module.ts
const routes: Routes = [
  { path: "compa", component: ComponentAComponent },
  { path: "compb", component: ComponentBComponent },
];
```

<br>

app-component html-be megyünk, létrehozunk kettő gombot ami routerlinkes és beszúrjuk a router-outletet


`app.component.html:`
```html app.component.html
<h1>Main app component</h1>
<hr>
<button routerLink="compa">Component A</button>
<button routerLink="compb">Component B</button>
<hr>
<router-outlet></router-outlet>
```

<br>

### Ezután elkészítjük az A komponest

`component-a.component.ts:`
```ts component-a.component.ts
export class ComponentAComponent implements OnInit, OnDestroy {
  constructor() {
    console.log("Comp A constructor runs")
  }

  ngOnDestroy(): void {
    console.log("Comp A OnDestroy runs")
  }
  
  ngOnInit(): void {
    console.log("Comp A OnInit runs")
  }
}
```

> Itt az `OnInit` és `OnDestroy` interfészeket implementáljuk, hogy használhassuk az `ngOnInit()` és `ngOnDestroy()` életciklus metódusokat. A konstruktorban, valamint az `ngOnInit()` és `ngOnDestroy()` metódusokban konzol üzeneteket írunk ki, hogy lássuk, mikor futnak le ezek a metódusok a komponens életciklusa során.

<br>

`component-a.component.html:`
```html component-a.component.html
<div>
    <h4>Component A</h4>
</div>
```

---
### Elkészítjük a B komponenst is:
`component-b.component.ts:`
```ts component-b.component.ts
export class ComponentBComponent {
  contents: StringContent[] = []
  message: string = "This is my welcome message"

  constructor() {
    console.log("Component B constructor runs")
    this.contents.push(new StringContent("Lorem ipsum"))
    this.contents.push(new StringContent("Dolor sit"))
    this.contents.push(new StringContent("Amet ipsum dolor"))
  }

  changeItem(): void {
    this.message = this.message.replace("welcome", "goodbye")
  }
}
```

> Itt a `ComponentBComponent` osztályban egy `contents` nevű tömböt hozunk létre, ami `StringContent` objektumokat tartalmaz. A konstruktorban feltöltjük ezt a tömböt néhány példányosított `StringContent` objektummal, és egy `message` változót is definiálunk, ami egy üzenetet tárol. Emellett van egy `changeItem()` metódusunk, ami megváltoztatja az üzenet tartalmát.

<br>

`component-b.component.html:`
```html component-b.component.html
<div>
    <h4>Component B</h4>
    <button (click)="changeItem()">Change message</button>
    <app-child *ngFor="let item of contents"
        [content]="item"
        [message]="message"
    ></app-child>
</div>
```

> A HTML sablonban egy gombot hozunk létre, ami a `changeItem()` metódust hívja meg kattintásra. Emellett egy `ngFor` direktívát használunk, hogy iteráljunk a `contents` tömb elemein, és minden egyes elemhez létrehozunk egy `app-child` komponenst. Az `app-child` komponensnek átadjuk a `content` és `message` változókat inputként.

---

### Végül elkészítjük a child komponenst is:

`child.component.ts:`
```ts child.component.ts
export class ChildComponent implements OnChanges {
  @Input() content: StringContent = new StringContent()
  @Input() message: string = ""

  constructor() {
    console.log("Child constructor runs")
  }

  ngOnChanges(changes: SimpleChanges): void {
    console.log("Child OnChanges runs")
  }
}
```

> Itt a `ChildComponent` osztályban két `@Input` dekorátorral ellátott változót definiálunk: `content`, ami egy `StringContent` objektum, és `message`, ami egy string. A konstruktorban és az `ngOnChanges()` metódusban konzol üzeneteket írunk ki, hogy lássuk, mikor futnak le ezek a metódusok a komponens életciklusa során. Az `ngOnChanges()` metódus akkor fut le, amikor bármelyik input változó értéke megváltozik.

<br>

`child.component.html:`
```html child.component.html
<div>
    <h4>{{ message }}</h4>
    <p>{{ content.content }}</p>
</div>
```

<br>

**Összefoglalva a projekt működése:**
- Az app komponensben két gomb van, amik az A és B komponensek között váltanak.
- Az A komponens csak egy egyszerű üzenetet jelenít meg, és az életciklus metódusokat használja, hogy lássuk mikor jön létre és mikor semmisül meg.
- A B komponens egy gombot és egy listát jelenít meg, ahol a listában child komponensek vannak.
- A child komponens két inputot kap a B komponenstől: egy `StringContent` objektumot és egy üzenetet.
- A child komponens az `OnChanges` életciklus metódust használja, hogy lássuk mikor változnak meg az inputok.


**Érdekesség**, hogy ha `ngfor`-ral rakosgassuk ki az elemeket és primitív típussal dolgozunk, akkor az ngfor a gyerek kmoponenst kiveszi (eltünteti) azaz lefut a ondestroy is és újra lerakja és lefut a constructor, onchanges és oninit is újra a gyerek komponensben. Azonban ha objektumon hívjuk meg akkor csak az onchanges és oninit fut le újra, a constructor és ondestroy nem. Ez azért van mert az ngfor látja hogy ugyanaz az objektum így nem veszi ki a gyerek komponenst csak frissíti az értékét. Ezért csináltuk meg a stringcontent osztályt. Primitív típusnál ez nem így van mert az egy érték típus és az ngfor nem látja hogy ugyanaz az érték így kiveszi és újra beteszi a gyerek komponenst.



### Servicek életciklusa
Eddig csak a komponensek életciklusáról beszéltünk és a service-kről még nem beszéltünk nem is véletlen. A service-knek egyszerű az életciklusuk.

A servicek alapvetően `singleton`-ként jönnek létre. Tehát mindig ugyanazt az egy példányt kapjuk vissza. Ha van egy service-em és 8 komponens használja akkor nem jön létre újra és újra a service. *Ez átállítható hogy ne singleton legyen de az ritka, hogy ilyen kelljen nekünk.*

A servicek először akkor jönnek létre, ahol/amior dependecy injectionnal megkapja egy komponenens.<br>
Így ezekután nem nagyon beszélhetünk életciklusokról.


A servicek életciklusát az IOC konténerek kezelik.<br>
`IOC` = `inversion of control` 
<br>
Ez azt jelenti hogy a servicek életciklusát nem mi kezeljük hanem az IOC konténer. Az IOC konténer egy olyan hely ahol a servicek létre jönnek és megsemmisülnek. Az IOC konténer feladata hogy létrehozza a serviceket és megsemmisítse őket amikor már nincs rájuk szükség.





## TANANYAG: [Authetication - simple token](https://github.com/siposm/bprof-frontend-weekly/tree/master/angular/auth-login-simple-token)


Backenden olyan volt ez, hogy voltak api végpontok és voltak ahol voltak lakatok, amit csak bejelentkezett felhasználk tudták használni.
<br>Frontend küld pl egy login api hívást, a backend leellenőrzte, hogy beléphet e, ha igen akkor visszaküld egy tokent (pl jwt).

A feladatunk az tehát hogy a frontend megkapja a tokent, és azt el kell tárolnunk és utána tudjuk meghívni a többi api-t, amihez már kell a token.

![authentication](https://github.com/oli-tolnai/Angular2/blob/main/kepek/angular2_3_3auth_uj.png)

A projektünkhoz fog kelleni egy login és logout komponens (utóbbi elhagyható) és kell még demoCompA és demoCompB komponensek. És persze az app component is kell.

<br>

### *A lépések be vannak számozva. Ezek mentén haladj, ha olvasod a jegyzetet.*


**2.)** A username és password-ot valahol tárolnunk is kell, ezért csinálunk egy loginModel osztályt, amiben tároljuk ezt a két változót.
És ezt a loginModelt példányosítani tudjuk a login komponensben és utána NgModellel összekötjük, és a gombnyomásra átadjuk a service-nek a loginmodel példányunkat.


`login.model.ts:`
```ts login.model.ts
export class LoginModel {
    username: string = ""
    password: string = ""
}
```

<br>

>**LoginModel**: Ez az osztály a bejelentkezési adatokat tárolja, nevezetesen a felhasználónevet és a jelszót.

---

<br>

`login.component.ts:`
```ts login.component.ts
export class LoginComponent {
  loginModel: LoginModel = new LoginModel()
  
  constructor(public authService: AuthService) { }

  inputCheck(): boolean {
    return !(this.loginModel.username.length > 3 && this.loginModel.password.length > 3)
  }
}
```


<br>

`login.component.html:`
```html login.component.html
<input type="text" placeholder="username" [(ngModel)]="loginModel.username">
<input type="password" placeholder="password" [(ngModel)]="loginModel.password">
<button (click)="authService.login(loginModel)" [disabled]="inputCheck()">Login</button>
```

<br>

> **LoginComponent**: Ez a komponens kezeli a felhasználói bejelentkezést. Tartalmaz egy `loginModel` objektumot, amely a felhasználó által megadott felhasználónevet és jelszót tárolja. A `inputCheck()` metódus ellenőrzi, hogy a felhasználónév és jelszó legalább 4 karakter hosszú-e, és ennek megfelelően engedélyezi vagy tiltja a bejelentkezés gombot. A bejelentkezési folyamatot az `AuthService` `login()` metódusa végzi.

---

<br>

**6.)** Most megnézzük a logout. Annyira gyorsan lefut hogy fölösleges egy komponens, de a itt csinálunk több dolgot, pl megnézi nincs e folyamatba valami és felugrik egy ablak hogy biztos ki akarsz a lépni. Logout igazából csak egyetlen metódus hívás ezért fölösleges külön komponenes neki.
Ez a logout lényegében annyi hogy auth service-ben egy metódussal kitöröljük a locastorage-ben eltárolt tokent


`logout.component.ts:`
```ts logout.component.ts
export class LogoutComponent {

  constructor(private authService: AuthService, private router: Router) {
    authService.logout()
    this.router.navigate(["login"])
  }
}
```

<br>

>**LogoutComponent**: Ez a komponens kezeli a felhasználói kijelentkezést. A komponens konstruktorában meghívja az `AuthService` `logout()` metódusát, amely eltávolítja a hitelesítési tokent a helyi tárolóból, majd átirányítja a felhasználót a bejelentkezési oldalra.


---

<br>

`demo-comp-a.component.html:`
```html demo-comp-a.component.html
<div>
    <h1>Demo Component -A-</h1>
    <p>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Voluptate ab perspiciatis soluta magnam sequi odit adipisci voluptas possimus nihil! Blanditiis neque earum porro voluptates. Neque quaerat quia assumenda dolore ipsam?</p>
    <p>Lorem ipsum dolor sit.</p>
</div>
```

<br>

>**DemoCompAComponent**: Ez egy egyszerű bemutató komponens, amely statikus tartalmat jelenít meg. Nincs benne speciális logika vagy interakció.

---

<br>

`demo-comp-b.component.ts:`
```ts demo-comp-b.component.ts
export class DemoCompBComponent {
  jobId: string = ""
  constructor(private http: HttpClient) { }
  deleteJob(): void {

    const token = JSON.parse(localStorage.getItem(environment.tokenKey)!).token

    const headers = new HttpHeaders()
      .set("Authorization", `Bearer ${token}`)
      .set("Content-Type", "application/json")

    this.http.delete(`${environment.apis.job}`, {
      headers,
      body: { id: this.jobId }
    }).subscribe(x => {
      console.log(x)
    })
  }
}
```

<br>

`demo-comp-b.component.html:`
```html demo-comp-b.component.html
<div>
    <h1>Demo Component -B-</h1>
    <p>f5e6d7c8-1234-5678-9101-1121-314151617181</p>
    <input type="text" [(ngModel)]="jobId" placeholder="job's id">
    <button (click)="deleteJob()">Delete job</button>
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Deserunt, culpa at? Mollitia cupiditate, deserunt expedita a, provident dolorem suscipit dolorum quia eligendi libero cum cumque ipsum quo! Minus, voluptatem cum.</p>
</div>
```

<br>

>**DemoCompBComponent**: Ez a komponens egy bemutató funkciót valósít meg, amely lehetővé teszi a felhasználó számára, hogy egy adott azonosító alapján töröljön egy munkát. A komponens tartalmaz egy `jobId` változót, amely a felhasználó által megadott azonosítót tárolja. A `deleteJob()` metódus lekéri a hitelesítési tokent a helyi tárolóból, majd egy HTTP DELETE kérést küld az API-nak a megadott azonosítóval.


---

<br>

`app-routing.module.ts:`
```ts app-routing.module.ts
const routes: Routes = [
  { path: "", redirectTo: "login", pathMatch: "full" },
  { path: "compa", component: DemoCompAComponent },
  { path: "compb", component: DemoCompBComponent, canActivate: [authGuard] },
  { path: "login", component: LoginComponent }, 
  { path: "logout", component: LogoutComponent },
  { path: "**", redirectTo: "login", pathMatch: "full" }
];
```

<br>

>**AppRoutingModule**: Ez a modul kezeli az alkalmazás útvonalait. Meghatározza, hogy melyik komponens melyik útvonalhoz tartozik, és beállítja az útvonalvédelmet a `DemoCompBComponent` számára az `AuthGuard` segítségével, amely biztosítja, hogy csak hitelesített felhasználók férhessenek hozzá ehhez a komponenshez.

---

<br>

`app.component.html:`
```html app.component.html
<h1>Login demo</h1>

<hr>

<ul>
  <li *ngIf="!authService.isLoggedIn(); else logOutSection"><a routerLink="login">Login</a></li>
  <ng-template #logOutSection>
    <li><a routerLink="logout">Logout</a></li>
  </ng-template>
  <li><a routerLink="compa">Component A</a></li>
  <li><a routerLink="compb">Component B</a></li>
</ul>

<hr>

<router-outlet></router-outlet>
```

<br>

`app.component.ts:`
```ts app.component.ts
export class AppComponent {
  constructor(public authService: AuthService) { }
}
```

<br>

>**AppComponent**: Ez a fő alkalmazás komponens, amely tartalmazza a navigációs menüt és a router outlet-et. A menüben feltételesen jeleníti meg a bejelentkezési vagy kijelentkezési linket az `AuthService` `isLoggedIn()` metódusa alapján.

---

<br>

`auth.token.ts:`
```ts auth.token.ts
export class AuthToken {
}
```

<br>

>**AuthToken**: Ez egy egyszerű osztály, amely a hitelesítési tokent reprezentálja. Jelenleg nincs benne mező, de később bővíthető a tokennel kapcsolatos információkkal.

---

<br>

**10.)** Végül pedig a routing védelmét nézzük meg. Ezt a routing modulban tudjuk megtenni a canActivate-vel. Itt most egy egyszerű logikát használunk, hogy megnézzük van e token a localstorage-ben és ha van akkor engedélyezzük a routingot. Ez egy egyszerűbb megoldás, de lehetne bonyolultabb is pl ellenőrizhetnénk a tokent hogy lejárt e stb.


`auth.guard.ts`
```ts auth.guard.ts
export const authGuard: CanActivateFn = (route, state) => {
  const value = localStorage.getItem(environment.tokenKey)
  if (!value) return false
  return value.length > 10
};
```

<br>

>**AuthGuard**: Ez egy útvonalvédelmi őr, amely megakadályozza, hogy nem hitelesített felhasználók hozzáférjenek bizonyos útvonalakhoz. A `canActivate` metódus ellenőrzi, hogy van-e érvényes hitelesítési token a helyi tárolóban.

```cmd
hg generate guard Auth
```

---



<br>

**5.)** csinálunk environmentset is amibe kirakjuk az apit ha már tanultunk ilyet. A tokent is kirakjuk ide egy környezeti változóba.

`environment.development.ts`
```ts environment.development.ts
export const environment = {
    apis: {
        login: "https://api.siposm.hu/login",
        developer: "https://api.siposm.hu/getDevelopers",
        job: "https://api.siposm.hu/job",
    },
    tokenKey: "my-custom-token-key"
};
```

<br>

>**Environment Configuration**: Ez a konfigurációs fájl tartalmazza az API végpontokat és a hitelesítési token kulcsát, amelyet a helyi tárolóban használnak. 


---

<br>

**1.)** Csinálunk egy külön servicet-t ahhoz hogy kezeljük a bejelentkezést: login metódus. És ezt a metódust meghívjuk a login kompononsben.

**3.)** A következő lépés a backend meghívása. amihez az api.siposm-et használjuk. A service-ben most lekódoljuk a login methódust. És a megkapott tokent localstoreage-ben eltároljuk.

>**4.)** Post után <>-ilyenbe fel tudjuk készíteni hogy milyen választ várunk.
Ehhez létrehozunk egy AuthToken class-t. Ez akkor fontos ha több infót is kapunk pl mikor jár le és nem csak egy stringet kapunk.

**7.)** Azt is meg kell oldanunk, hogy ha nem vagyunk belépve akkor a logint lássuk ha pedig be vagyunk lépve akkor logout-ot lássuk. Ezt az auth service-ben nézzük, amiben a localstorage-ban megnézzük hogy üres e a tokenünk és ngIf-vel döntjük el hogy melyik jelenjen meg.


> **8b.)** Ha egy menüpontot pl ugyanígy megoldjuk ngIf-vel hogy el legyen rejte valami akkor rárakhatnánk ugyanezt, viszont ez nem jó mert url-ből elérhető így biztonságilag ez nem jó.
Ezért az auth serviceben csinálunk egy olyat, hogy "canActivet()" ami megnézi hogy be van e lépve, majd a app routing-ben rárakunk egy pathra egy canActive-et és átadjuk negi [AuthService]. Ez csak akkorműködik ha auth serviceben is canActive a neve!!!!


> **9.)** Két részre kell bontani hogy rooting alapján elérem e és azt is hogy látom e.  A canActivate neve: "auth Guard"
Azonban ezt is lehet egy kicsit szebben csinálni. Ugyanis a service-nek nem egészen feladata a rooting levédése.
Szóval `ng g guard auth` és ha regeneráljuk akkor felkínál egy interakciós fület. Nekünk a canActivate-kell. és ide illeszük be a logikát ami nézi hogy be vagyunk e jelentkezve. Ezután az approutingban a AuthService helyette az AuthGardot adjuk át a canActivate-nek.



`auth.service.ts:`
```ts auth.service.ts
export class AuthService {

  constructor(private http: HttpClient) { }

  // canActivate(): boolean {
  //   return this.isLoggedIn()
  // }

  isLoggedIn(): boolean {
    const value = localStorage.getItem(environment.tokenKey)
    if (!value) return false
    return value.length > 10
  }

  login(loginModel: LoginModel): void {
    this.http.post<AuthToken>(environment.apis.login, loginModel).subscribe(token => {
      // check and set token expiration etc. here
      localStorage.setItem(environment.tokenKey, JSON.stringify(token))
    })
  }

  logout(): void {
    localStorage.removeItem(environment.tokenKey)
    // call backend logout etc.
  }
}
```

<br>

>**AuthService**: Ez a szolgáltatás kezeli a hitelesítési folyamatokat, beleértve a bejelentkezést, kijelentkezést és a hitelesítési állapot ellenőrzését. A `login()` metódus egy HTTP POST kérést küld az API-nak a bejelentkezési adatokkal, és a válaszként kapott tokent eltárolja a helyi tárolóban. A `logout()` metódus eltávolítja a tokent, míg az `isLoggedIn()` metódus ellenőrzi, hogy van-e érvényes token.

---

### Lépések összefoglalva:
1. Csinálunk egy külön servicet-t ahhoz hogy kezeljük a bejelentkezést: login metódus. És ezt a metódust meghívjuk a login kompononsben.
2. A username és password-ot valahol tárolnunk is kell, ezért csinálunk egy loginModel osztályt, amiben tároljuk ezt a két változót.
3. A következő lépés a backend meghívása. amihez az api.siposm-et használjuk. A service-ben most lekódoljuk a login methódust. És a megkapott tokent localstoreage-ben eltároljuk.
4. Post után <>-ilyenbe fel tudjuk készíteni hogy milyen választ várunk.
5. Csinálunk environmentset is amibe kirakjuk az apit ha már tanultunk ilyet. A tokent is kirakjuk ide egy környezeti változóba.
6. Most megnézzük a logout. Annyira gyorsan lefut hogy fölösleges egy komponens, de a itt csinálunk több dolgot, pl megnézi nincs e folyamatba valami és felugrik egy ablak hogy biztos ki akarsz a lépni. Logout igazából csak egyetlen metódus hívás ezért fölösleges külön komponenes neki.
7. Azt is meg kell oldanunk, hogy ha nem vagyunk belépve akkor a logint lássuk ha pedig be vagyunk lépve akkor logout-ot lássuk. Ezt az auth service-ben nézzük, amiben a localstorage-ban megnézzük hogy üres e a tokenünk és ngIf-vel döntjük el hogy melyik jelenjen meg.
8. Csinálunk egy auth guardot ami megvédi a routingot. Ezt a routing modulban tudjuk megtenni a canActivate-vel. Itt most egy egyszerű logikát használunk, hogy megnézzük van e token a localstorage-ben és ha van akkor engedélyezzük a routingot. Ez egy egyszerűbb megoldás, de lehetne bonyolultabb is pl ellenőrizhetnénk a tokent hogy lejárt e stb.
9. Két részre kell bontani hogy rooting alapján elérem e és azt is hogy látom e.  A canActivate neve: "auth Guard"
10. Végül pedig a routing védelmét nézzük meg. Ezt a routing modulban tudjuk megtenni a canActivate-vel. Itt most egy egyszerű logikát használunk, hogy megnézzük van e token a localstorage-ben és ha van akkor engedélyezzük a routingot. Ez egy egyszerűbb megoldás, de lehetne bonyolultabb is pl ellenőrizhetnéka tokent hogy lejárt e stb.
---




### S.H.
S.H. -> session hijack <br>
A hijack jelentése eltérítés. <br>
Ha valakinek a gépéről ki tudom nyerni a tokenét, akkor utána a saját gépemen a localstorage-be csak beírok a keyt és az értékét.

# Angular2 4.hét 4.óra

## TANANYAG: Ismétlés - authentikáció egyszerű tokennel, nem jwt-vel

Ábrákon keresztül átbeszéltük, hogy hogyan kommunikál a frontend és a backend bejelentkezés majd elemek listázása során.

![angular2_4_1-auth](https://github.com/oli-tolnai/Angular2/blob/main/kepek/angular2_4_1-auth.png)

Az első ábrán a bejelentkezés folyamata látható. Input mezőkbe beírjuk a bejelentkezéshez szükséges adatokat (username, password), majd a submit gombra kattintva elküldjük a bejelentkezési kérést a backendnek. A backend ellenőrzi az adatokat, és ha helyesek, akkor visszaküld egy tokent JSON formátumban, amelyet a frontend elment a böngészőben (pl. localStorage-ben vagy sessionStorage-ben). Ez a token szolgál azonosítóként a későbbi kérésekhez.

![angular2_4_2-auth](https://github.com/oli-tolnai/Angular2/blob/main/kepek/angular2_4_2-auth.png)

A második ábrán egy védett erőforrás elérésének folyamata látható. Amikor a felhasználó megpróbál hozzáférni egy védett erőforráshoz (pl. egy lista megtekintése), a frontend elküldi a kérést a backendnek, és a kérés fejléceiben elküldi a korábban kapott tokent. A backend ellenőrzi a tokent, és ha érvényes, akkor visszaküldi a kért adatokat (pl. egy elemek listáját) JSON formátumban. Ha a token érvénytelen vagy hiányzik, akkor a backend visszaküld egy hibakódot (pl. 401 Unauthorized), és a frontend ennek megfelelően reagál.

---
---
<br>

## TANANYAG: [auth-login-jwt](https://github.com/siposm/bprof-frontend-weekly/tree/master/angular/auth-login-jwt)

> Terminálból a backendet `dotnet run`-nal tudjuk futtatni és nem visual studioban kell megnyitni és onnan futtatni. Ha futtatáskor https-t szeretnénk akkor `dotnet run --launch-profile "https"`-t kell használni. 


**A JWT nem hashelve van hanem az egy kódolás.**
- A hash egy olyan érték, amelyet egy adott bemenetből (például jelszóból) egy speciális algoritmus segítségével generálnak. A hash érték egyedi és fix hosszúságú, és célja, hogy a bemenetet egy rövid, könnyen kezelhető formában reprezentálja. A hash értékek általában nem visszafejthetők, ami azt jelenti, hogy nem lehet visszanyerni az eredeti bemenetet a hash értékből. 

- Visszafejtés helyett a hash értékeket általában összehasonlítják egy másik hash értékkel, amelyet ugyanazzal az algoritmussal generáltak egy adott bemenetre. Ha a két hash érték megegyezik, akkor valószínűleg a bemenetek is megegyeznek.



**Angularban a routing-nál role-okat is be lehet állítani:**
```ts
 // Bejelentkezés szükséges (de nincs role megkötés)
  { path: "compb", component: DemoCompBComponent, canActivate: [authGuard] },
  
  // Csak ADMIN számára elérhető útvonal
  {
    path: 'admin', component: AdminOnlyComponent,
    canActivate: [authGuard],
    data: { roles: ['ADMIN'] }
  },
```

> A routing levédése az authGuard feladata, de kb minden mást az authservice csinál.

authguard-nál fontos az inject(), amit lehet függvényeknél is használni, nem úgy mint a dependency injection-t, amelyet csak osztályoknál lehet használni- Ilyenkor a függvényen belül tudunk szolgáltatásokat injektálni.

```ts
export const authGuard: CanActivateFn = (route, state) => {
  const auth = inject(AuthService)
  const router = inject(Router)

  // 1) be van-e jelentkezve (exp alapján is)
  if (!auth.isLoggedIn()) {
    router.navigate(['/login'], { queryParams: { returnUrl: state.url } })
    return false
  }

  // 2) ha a route megkövetel szerepet
  const required = route.data?.['roles'] as string[] | string | undefined
  if (required && !auth.hasRole(required)) {
    // nincs jogosultság
    router.navigate(['/login'], { queryParams: { reason: 'forbidden' } })
    return false
  }
  return true
}
```

---
---
<br>


## TANANYAG: [Tesztelés](https://github.com/siposm/bprof-frontend-weekly/tree/master/angular/testing)

**Miért kell tesztelni?**
- ne legyen hiba
- kód komplexitás nő -> hiba nő
- teszteset = mit kell csinálnia a programnak
- megismételhetőség
- kód módosítás / refaktorálás

> Minél komplexebb a kód annál nagyobb az esélye hogy hiba lesz benne, ezért is kell tesztelni, mert ha van egy jól megírt teszt akkor a kód módosításakor hamar kiderül hogy valami el lett e rontva.

*Ha valamit módosítok, vagy másvalaki módosít valamit a saját kódján akkor a tesztek alapján hamar kiderül hogy el lett e rontva valami.*

> Tesztekből a kód működését is jól meg lehet érteni, mert ha a jól megírt teszteket végig nézzük akkor abból hamar kiderül hogy egy egy komponensnek mi is a célja, mert a teszteket a fő funkiókra írjuk meg.



**Tesztelés típusok:**
- (edge-case teszt) - ez szélsőséges eseteket néz
- (mock) - ez nem tesztelési módszer, hanem ez unit teszteknél használandó eszköz
- unit = egységteszt
- stressz teszt - nagy terhelés alá, olyanis akár ami nem valószínű hogy be fog következni. pl ha 2000 fővel számolunk hogy kb ennyien fogják használni, akkor leteszteljük pl 5000fővel - ide tartozik a DOS és DDOS támadás
- manuális teszt - nem megismételhető


![tesztelés típusok](https://github.com/oli-tolnai/Angular2/blob/main/kepek/angular2_4_2-testss.png)

Legalul a unit tesztelés van, ez a legkisebb egység tesztelése. Efölé van az integrációs tesztelés, ahol több komponenst együtt tesztelünk. Végül a legfelső szinten van az end to end tesztelés, ahol a teljes alkalmazást teszteljük úgy mintha egy felhasználó használná.

 

 
**Angularban ezeket szoktuk használni**
- service (FRONTEND oldal business logikája)
- komponens
- model -> class, interface, type
    - interface és type esetében nincs értelme tesztelésnek
    - classnál akkor értelmes tesztelni, ha van valami plusz metódus/logika benne
    
> service-nél nem kell tesztelni a httpClient kéréseket, mert akkor ott lényegében a backendet tesztelnénk. **Tesztelésnél az általunk írt logikákat kell tesztelni.**

> amikor egy komponens service-t használ akkor nem azt kell letesztelni hogy benne a service jól működik-e, **hanem a komponensben megírt saját logikákat kell tesztelni.**

### Tesztelés

Tesztelés fontos részei: `describe`, `beforeEach`, `it`, `expect`:
- `describe` -> ez egy teszt csomag, ez alatt vannak a tesztek
- `beforeEach` -> ez egy setup rész, itt lehet előkészíteni dolgokat, ez minden teszt előtt lefut
- `it` -> ez egy teszt eset, ez alatt van maga a teszt
- `expect` -> ez maga a teszt, itt van leírva hogy mit várunk el


#### Tesztek futtatása:
- **`ng test` -> tesztek futtatása**

- Ezután megnyílik egy böngésző amiben látunk több mindent:
    - **Karma** -> Teszt futtató környezet
    - **Jesmie** -> JS teszt környezet

Meglehet csinálni azt hogy a tesztek futtatásakor a böngészőt ne nyissa meg:
- `ng test --watch=false --browsers=ChromeHeadless`-t kell használni.



### **Három 'A'**
- Arrange - előkészít
- Act - konkrétan maga a múvelet
- Assert - konkrétan maga a teszt eredménye 

---
```ts
getAll() : Student[]{
    return [...this.students] // -> ... jelentése hogy nem referenciaként ajda át hanem a másolatát
}
```
> A három pont a `spread operator`, ami azt jelenti hogy a tömb elemeit egyesével kiveszi és egy új tömbbe teszi bele. Így nem referenciaként adja át a tömböt hanem annak egy másolatát.
---

Tesztelésnél fontos, hogy ha egy service nem beágyazott adatokkal dolgozik, hanem gettel szerez adatokat API-val, így azt nem kell tesztelni, mert akkor a htttpClient-et tesztelnénk.<br   >
Ennek ellenére le kell tesztelni a benne lévő metódusokat, szóval jön a kérdés hogy *api hívás nélkül hogyan tesztelem le?*<br>
A válasz az, hogy **a tesztben a beforeEach()-ben létrehozunk seed adatokat.**


### Teszteket kell csinálni ölab-hoz, itt viszont annyira ezt nem tanuljuk 

`test --code-coverage`

`Branches`:
```ts
if (name...)
    [Igaz] <- első ág
else
    [hamis] <- második ág
```
**Ha egy ilyet akarunk tesztelni akkor minden ágat tesztelni kell!**

Alábbi dokumentumban részletesen olvashatunk a tesztelésről: [siposm/testing.md](https://github.com/siposm/bprof-frontend-weekly/blob/master/angular/materials/testing.md)<br>
A dokumentumban a **test double eszköztár** fontos. Ezeknél a legtöbb hasonlít egymásra, kivéve a `spy`.

#### Ölab-on a teszteket generálhatjuk AI-val
Ehhez chatgpt-nek be kell adni a `ts`-t és a `html`-t is, és 5-6 tesztet kérünk tőle és átnézzük, ugyanis sokszor értelmetlen teszteket is készít.

> tesztelésnél ha van olyan function amit több tesztben is használnánk akkor a describe-on belül lehet csinálni functionokat.

# TANANYAG: [reactive forms](https://github.com/siposm/bprof-frontend-weekly/tree/master/angular/reactive-form)

Ezt a részt csak felületesen érintettük, így érdemes letölteni a kódot és átnézni.

# Angular2 5.hét 5.óra

`asp-donte-api-prodcuts` backend programot használjuk

c#-hoz van `echoapi extension` vs code-ban, aminél az api kéréseket tudjuk használni, olyan mint a postman


## TANANYAG: [observable](https://github.com/siposm/bprof-frontend-weekly/tree/master/angular/observables)

### stateless -> állapot mentes
ezt lehet alkalamzás, komponenes és service szinten is nézni

Ha van egy dobozunk akkor abban nincs eltárolva konkrét állapot

ennek ellenkezője a statefull. 

"Mennyire erősen támazkodik egy belső adatszerekezetre, azaz belső állapotra."

A stateless azt mondja, hogy ne csináljuk egy konkrét fizikai állapotot, hanem folyamatosan a backendtől kappjon dolgokat és jelenítse meg, és ne legyen semmilyen lokális állapot.

Ehhez jól illeszkedik az a HTTP protokoll. 

*A HTTP is állapotmentes.*

Konkrét állapot (pl lista) helyett observable-t hozunk létre, aminek szintén megadhajtuk hogy milyen elemek legyenek (pl product).

Ehhez használjuk subscribe-ot és az async pipe-ot


`data.service.ts`-fáljban most konstrukor és dependency injection helyett inject-et használunk

RXJS - függvénykönyvtár, ennek egyik operátora az `of` ami egy observable-t csinál abból amit megadunk neki. És használjuk még a `pipe`-ot is. Ami azért kell mert...
Még egy operátor a `tap`.

tap-pel tudunk logolásokat is belerakni ami hasznos nekünk.

használjuk még a `map` operátort ami itt nem ugyanaz mint a sima javascriptes `map`

Obserrvable-t kicsit hasonlóan kell felofgni mint a promise-okat. "Majd amikor lesz akkor ez lesz"

Van egy cső amiben bele megy a lista, van egy delay, majd tap és két map és ezután ez fog visszaadódni.

delay azért van benne, hogy szimuláljuk mi lenne ha api végontról hívnánk meg.

`data.service.ts`
```ts 
  getProducts(): Observable<Product[]> {
    // of() → egyszerűen Observable-t készít a tömbből
    return of(this.products).pipe(

      // szimulálunk hálózati késleltetést
      delay(2000),

      // mellékhatások kezelése pl. logolás
      tap(() => console.log("Adatok betöltve...")),

      // áremelés 10%-kal
      map(products => products.map(p => ({ ...p, price: p.price * 1.1 }))),

      // csak 100 felettiek
      map(products => products.filter(p => p.price > 100))
    )
  }
```



#### most átmegyünk az app.component.ts-be.
ha itt egy változót meg akarunk jelölni observable-nek akkor kell hozzá a dollár jel.

`app.component.ts`
```ts
products$!: Observable<Product[]>
```

ngOnInit-be megtudjuk hívni a servicen keresztül az observable-ös metódust. 

`app.component.ts`
```ts
  ngOnInit() {
    this.products$ = this.dataService.getProducts()

    // subscribe nélkül sosem fut le
    this.subscription = this.dataService.getProducts2().subscribe(x => {
      console.log(x)
      this.products2 = x
    })

    this.dataService.getProducts3().subscribe(x => console.log(x))
  }
```

azonban hogy ezek működjenek úgymond le kell futtatni is. Ezért ezekre a metódusokra rá kell rakni a subscribe-ot.

Ha obserrvabelem van akkor valahol kötzelező subscribolni különben soha nem fog lefutni. 

Azonban most tegyük egyenlővé a this.products$-val a meghívott observable metódust. 
Ebben az esetben ha html-ben meg akarjuk hívni akkor rá kell rakni az async pipe-ot

`app.component.html`
```html
<ul>
  <li *ngFor="let p of products$ | async">
    {{ p.name }} - {{ p.price | currency:"HUF" }}
  </li>
</ul>
```


A subscribe - amit használtunk az kicsit veszélyes.

**memory leak**:
- van a kódban egy olyan programozási logikai hiba, hogy fölzabálja a memóriát. 

A gond, hogy felcsatlakozik a subscribe de sosing lecsatlakozás (*dispose*-olva nincs). 

http hívásnál nem feltétlen tud memory leak kialakulni. 

***tehát jön a kérdés hogy a dollárjeles a jobb vagy a subsciribe-os?***

csinálnunk kell egy private `subscription`-t

és azt mondjuk hogy a metódus.subscribe kerüljön belele ebbe a subscripiton-ba és az onDestroy-ban a subscriptionról leiratkozunk.

Mivel az angular fejlődik és az emberek lusták, ezért ezt nem akarjuk megcsinálni, mert ha sok subscript van akkor ezt sokszor meg kell csinálni, szóval ezért van az async pipe, ami megcsinálja a feliratkozást is és ha szükséges akkor a leiratkozást is.

**SZÓVAL az async pipe jobb megoldás mint a subscribe!!**


A stateless azért kell hogy ne legyene egy fix álapotunk amiben eltárolunk benne adaokat hanem olyan legyen mintha átfújna rajta a szél, és ehhez használjuk az observable-ket.



- stateless kompoens:
    - nem tárol adatot, hanem mindent @Input / service kap, kezel.
- stateless service:
    - nem tart lokális adatot, mindent API-ról kap.
- statefull service:
    - lokális állapotot tárol (1. BehivorSubject, 2. Signals (ennek semmi köze a signalR-hez))

 observable: mindezt (az említett stateless-es dolgokat) lehetővé teszi

 memory leak: a program a lefoglalt memóriá nem szabadítja fel miután már nem használja.

 rxjs: reactive extensions for javascript
 reaktív programozási könyvtár, aminek segítségével stream-ekkel (adatfolyamokkal, pl: observable) tudunk dolgozni és ezekhez dekleratív (!) módon tudunk logikát írni.


> **A reaktív programozás azt omndja:** *ne kérdezd meg hogy változott e valami, hanem inkább iratkozz fel és reagálj amikor megváltozik.*

## TANANYAG: [signalr-observables-interceptor](https://github.com/siposm/bprof-frontend-weekly/tree/master/angular/signalr-observables-interceptor)

`dotnet restore` majd `dotnet run` 


behavior subject-et használunk 
behaviorsubject-nél a .next új érték kibocsátására alkalmas és a másik fontos dolog a .value

BehaviorSubject:
- next
- value

`product.service.ts`
``` ts product.service.ts
  A BehaviorSubject használatának az a lényege, hogy nem csupán egy adatfolyamot (streamet) biztosít,
  hanem mindig tartalmazza az aktuális értéket is. Ez azt jelenti, hogy bármikor lekérdezhető 
  a legutolsó állapot (.value), és szükség esetén új értéket is lehet kibocsátani a .next() metódus 
  segítségével. A szolgáltatásban ezért szokás egy privát BehaviorSubject-et létrehozni, 
  amely az adatokat kezeli és frissíti, míg a komponensek számára ennek csak az olvasható formáját, 
  azaz az Observable-t tesszük elérhetővé az asObservable() metódussal. 
  Így a komponensek megfigyelhetik az adatváltozásokat, de nem tudják közvetlenül módosítani az 
  állapotot, ami biztonságosabb és átláthatóbb architektúrát eredményez.
```

Ezt úgy tudjuk elkpézelni hogy van egy service amit ketté osztunk, és a hátsó részében van a BehaviorSubject, ami létrehoz stateful jellegű dolgot, amit okosan kezel, mert folyamatosan frissül. És erre jön rá az hogy `as Observable`
a signalR-rel az apin keresztül folyamatosan frissül a stateful behaviorsubject, ami után az `as observable`-n keresztül szól a többieknek hogy változott. És fontos hogy a komponensek vagy async pipe-ot vagy subscribe-ot használjanak.

`product.service.ts`
```ts product.service.ts
  private _products$ = new BehaviorSubject<Product[]>([])
  products$ = this._products$.asObservable()
```

És most megnézzük hogy a komponensek hogyan csatlakoznak erre: [app.component.ts](https://github.com/siposm/bprof-frontend-weekly/blob/master/angular/signalr-observables-interceptor/frontend/src/app/app.component.ts). ngoninit be meghívjuk a service init-jét, majd products$-ba belerakjuk az observable


### TANANYAG: [interceptor](https://github.com/siposm/bprof-frontend-weekly/blob/master/angular/signalr-observables-interceptor/frontend/src/app/error.interceptor.ts)

a programunkban a serviceben a deletenél nem adtuk át headert úgy mint korábban és ez interceptor miatt van.
`ng g interceptor`

ennek feladata, hogy amikor sok különböző api hívásunk van, és nem akarjuk egyesével beírogtanki hogy bearer token..., akkor ez beékelődik minden api hívásba és itt pl most a deletenél berakjuk hogy mi legyen a header. 


`error.interceptor.ts`
```ts error.interceptor.ts
// Bearer token csak a DELETE kérésekhez
  let request = req
  if (req.method === "DELETE") {
    const token = localStorage.getItem(environment.tokenKey)
    if (token) {
      request = req.clone({
        setHeaders: { Authorization: `Bearer ${token}` }
      })
    }
```

Nagyon fontos a throwError rész. az interceptor amikor elküldök egy post kérést az apinak, akkor ezt megnézi az interceptor, nem csinál vele semmit mert nem delete, és amikor jön vissza az api hívás akkor ha hiba van akkor az interceptor ezt továbbdobja és így eljut a service-hez is vagy akár a komponennshez is.

```ts error.interceptor.ts
    return throwError(() => err) // tovább is dobja a hibát, hogy a hívó komponens is tudjon róla
```

nem csak arra jó hogy pl hibákat lekezel, hanem logolni is tudja a ki és bemenő api hívásokat, vagy válaszidő teljesítményt nézni, azt is az interceptor tudja. 

ez egy: _dekorátor tervezési minta_

Hogyan működik a signalR a háttérben: 
A signalR folyamatos kapcsolatot tart fenn. a signalR több technológiát is használ, websockets, server-sent events (SSE) és long polling (lp)

1. ✔ Websocket: állandó kapcsolat, 2 írányú, mindkét fél küldhet (legjobb megoldás ha a backenden és a frontenden is van websocket)
2. SSE: server küld adatokat egyirányúan, HTTP-n keresztül
3. long polling: kliens HTTP kapcsolatot hosszú ideig fentart. Szerver akkor válaszol csak, ha van új adat.


# Web Security

## HTTP és HTTPS

### Alapvető különbségek

A **HTTP** (HyperText Transfer Protocol) és a **HTTPS** (HyperText Transfer Protocol Secure) közötti alapvető különbség a biztonság. A HTTP nem titkosítja az átvitt adatokat, így a protokollon keresztül küldött információk nyílt szövegként utaznak az interneten. Ez különösen veszélyes érzékeny adatok (jelszavak, bankkártyaszámok) esetén.

### Portok

- **HTTP:** 80-as port (alapértelmezett)
- **HTTPS:** 443-as port (alapértelmezett)


### Böngésző viselkedés

A modern böngészők (Google Chrome, Firefox, Safari) a HTTP oldalakat nem biztonságosnak jelölik, és sok esetben figyelmeztetést jelenítenek meg, vagy csak manuális jóváhagyással töltik be az oldalt.

### HTTP biztonsági problémái

A HTTP protokollal az a legnagyobb probléma, hogy a Base64-del kódolt adatok könnyen kinyerhetők és visszafejthetők. Van olyan rendszer, ahol ez kardinális probléma (pl. bankrendszerek, egészségügyi adatok), és van ahol kevésbé kritikus, de így is kockázatos.

### Hasznos eszköz

**Wireshark:** Hálózati forgalom elemző eszköz, amellyel megfigyelhetők a HTTP és HTTPS csomagok, így látható a HTTP sebezhetősége.

## HTTPS és SSL/TLS

### SSL/TLS működése 6 lépésben

1. **ClientHello:** A kliens (böngésző) kapcsolatot kezdeményez a szerverrel, elküldi a támogatott titkosítási algoritmusokat és TLS verziókat
2. **ServerHello:** A szerver kiválasztja a titkosítási módszert és elküldi a digitális tanúsítványát, amely tartalmazza a publikus kulcsot
3. **Tanúsítvány ellenőrzés:** A kliens ellenőrzi a szerver tanúsítványát egy megbízható tanúsítványkiadó (CA - Certificate Authority) segítségével
4. **Kulcscsere:** A kliens generál egy session kulcsot, amit a szerver publikus kulcsával titkosít és elküldi
5. **Session kulcs létrehozása:** Mindkét fél birtokolja a session kulcsot, amit szimmetrikus titkosításhoz használnak
6. **Biztonságos kommunikáció:** A továbbiakban minden adat ezzel a session kulccsal titkosítva utazik a két fél között

## TCP és UDP

### TCP (Transmission Control Protocol)

**Jellemzők:**

- Kapcsolatorientált protokoll
- Garantálja az adatok megérkezését és a helyes sorrendet
- Nincs adatvesztés
- Lassabb, de megbízható

**Használati területek:** Webböngészés (HTTP/HTTPS), email, fájlátvitel (FTP), távoli hozzáférés (SSH)

### UDP (User Datagram Protocol)

**Jellemzők:**

- Kapcsolat nélküli protokoll
- Nem garantálja az adatok megérkezését
- Lehet adatvesztés
- Gyorsabb, de kevésbé megbízható

**Használati területek:** Videóstreamek, online játékok, VoIP (hang- és videóhívások), DNS lekérdezések

### TCP háromágú kézfogás (Three-way handshake)

1. **SYN (Synchronize):** A kliens SYN csomagot küld a szervernek, kapcsolatot kezdeményez
2. **SYN-ACK (Synchronize-Acknowledge):** A szerver válaszol SYN-ACK csomaggal, elfogadja a kapcsolatot
3. **ACK (Acknowledge):** A kliens ACK csomagot küld vissza, megerősíti a kapcsolatot

## Titkosítás

### Protokoll vs. Algoritmus

**Titkosítási algoritmus:** A konkrét matematikai módszer, amely az adatok átalakítását végzi (pl. AES, RSA, DES)

**Titkosítási protokoll:** Szabályrendszer, amely meghatározza, hogyan használjuk az algoritmusokat a kommunikáció során (pl. TLS, SSL, IPsec)

### OSI modell

A hálózati kommunikáció hét rétegű modellje:

1. **Fizikai réteg:** Fizikai adatátvitel (kábelek, jelek)
2. **Adatkapcsolati réteg:** Fizikai címzés (MAC cím)
3. **Hálózati réteg:** Logikai címzés és útválasztás (IP)
4. **Szállítási réteg:** Végpontok közötti kommunikáció (TCP, UDP)
5. **Viszony réteg:** Munkamenetek kezelése
6. **Megjelenítési réteg:** Adatformátum-átalakítás, titkosítás
7. **Alkalmazási réteg:** Felhasználói alkalmazások (HTTP, FTP, SMTP)

## Történelmi titkosítási módszerek

### Caesar-titkosítás

Egyszerű helyettesítő titkosítás, ahol minden betűt eltoló módszerrel helyettesítünk. Például 3 pozícióval eltolva az A betű D-re, a B betű E-re változik.

### Csoportos helyettesítés

Több betű egyszerre történő helyettesítése előre meghatározott szabályok szerint, bonyolultabb mint a Caesar-titkosítás.

### Vigenère-titkosítás

Kulcsszó alapú többszörös Caesar-titkosítás, ahol a kulcsszó betűi határozzák meg az eltolás mértékét minden pozícióban.

## Szimmetrikus kulcsú titkosítás

Ugyanazzal a kulccsal történik a titkosítás és a dekódolás.

**Előnyök:**

- Gyors működés
- Hatékony nagy adatmennyiségnél

**Hátrányok:**

- Nehézkes a kulcs biztonságos megosztása
- Ha kompromittálódik a kulcs, minden adat sebezhető

**Példák:** AES (Advanced Encryption Standard), DES, 3DES

## Aszimmetrikus titkosítás

### Diffie-Hellman kulcscsere

**Működése:**

1. Mindkét fél megegyezik egy nyilvános prímszámban (p) és egy generátorban (g)
2. Mindkét fél generál egy privát kulcsot (a és b)
3. Mindkét fél kiszámítja a saját nyilvános kulcsát: A = g^a mod p és B = g^b mod p
4. Kicserélik a nyilvános kulcsokat
5. Mindkét fél kiszámítja a közös titkos kulcsot: s = B^a mod p (egyik oldal) és s = A^b mod p (másik oldal)
6. Mindkét fél ugyanazt a közös titkos kulcsot kapja anélkül, hogy azt közvetlenül át kellett volna küldeni

### RSA (1977)

**Két kulcsos rendszer:**

- **Publikus kulcs:** Ezzel történik a titkosítás, bárki megismerheti
- **Privát kulcs (Secret key):** Ezzel lehet dekódolni, szigorúan titkos

**Működési elve:** Nagy prímszámok szorzatának faktorizálásának nehézségén alapul. A publikus kulccsal titkosított üzenetet csak a privát kulccsal lehet visszafejteni.

## SSH Key (Secure Shell)

### Lényeg

Olyan, mint egy username+password kombináció, de sokkal biztonságosabb és könnyebb tárolni. Bármilyen helyen használható, ahol hitelesíteni kell magunkat, például Git, távoli szerverek elérése.

### SSH működése 5 lépésben

1. **Kulcspár generálás:** A felhasználó generál egy publikus és egy privát kulcsot
2. **Publikus kulcs feltöltése:** A publikus kulcsot feltöltjük a szerverre (pl. GitHub, távoli szerver)
3. **Kapcsolódás kezdeményezése:** A kliens kapcsolódik a szerverhez
4. **Kihívás-válasz folyamat:** A szerver egy véletlenszerű üzenetet küld, amit a kliens a privát kulcsával aláír
5. **Hitelesítés:** A szerver a publikus kulccsal ellenőrzi az aláírást, ha egyezik, a kapcsolat létrejön

### Hasznos eszköz

**PuTTY Key Generator (PuTTYgen):** SSH kulcspár generálására szolgáló eszköz, ssh-rsa típusú kulcsokat hoz létre.

## Token alapú azonosítás

### JWT (JSON Web Token)

**Három részből áll:**

1. **Header:** Milyen algoritmussal történt a titkosítás (pl. HS256, RS256)
2. **Payload:** A tartalom, az adatok amiket tárolni szeretnénk (user ID, role, stb.)
3. **Verifying Signature (aláírás):** Aláírás, amely hitelesíti a token valódiságát

**Működés:** A szerver generálja a tokent bejelentkezéskor, majd a kliens minden kéréssel együtt elküldi. A szerver ellenőrzi az aláírást, és ha valid, engedélyezi a hozzáférést.

## API Key

### Lényeg

Nem felhasználónak szánva, hanem rendszerek közötti kommunikációhoz.

### Működés

Hasonló a JWT tokenhez, de egyszerűbb struktúra. Általában egy hosszú, véletlenszerű string, amit a rendszer minden API kéréshez csatol. A szerver ellenőrzi, hogy valid-e az API key, és hogy milyen jogosultságok tartoznak hozzá.

**Fő különbség a JWT-től:** Az API key általában hosszabb élettartamú, statikus, míg a JWT token időkorlátos és dinamikus.

## Jelszavak védelme

### Hash függvények

**Jellemzők:**

- Egyirányú folyamat, nem fordítható vissza
- A hash eredmény általában rövidebb mint az eredeti bemenet
- Pici bemeneti eltérés esetén nagy kimeneti eltérés
- Determinisztikus: ugyanaz a bemenet mindig ugyanazt a hasht adja

**Felhasználás:** Jelszavak tárolása, dokumentum eredetiség ellenőrzés, adatintegritás biztosítás

### Hash típusok

**MD5 (Message Digest 5):** Elavult, sérülékeny, nem ajánlott jelszavakhoz

**SHA-2 (Secure Hash Algorithm 2):** Család (SHA-224, SHA-256, SHA-384, SHA-512), jelenleg biztonságos és ajánlott

### Jelszó tárolási módszerek

1. **Plain text (egyszerű szöveg):** A legrosszabb megoldás, a jelszavak olvashatóan vannak tárolva
2. **Titkosított jelszó:** Kicsit jobb, de szükség van kulcsra a dekódoláshoz, ha a kulcs kiszivárog, minden jelszó veszélybe kerül
3. **Hashelés:** Bevett módszer, nem lehet visszafejteni a jelszót a hashből

### Sózás (Salt)

**Mi az a salt:** Minden felhasználóhoz tartozik egy véletlenszerű karaktersorozat (só), amit a plain text jelszó mögé (vagy elé) fűznek hozzá a hashelés előtt.

**Működés:**

- Regisztrációkor: véletlenszerű salt generálás → jelszó + salt → hash → hash és salt tárolása
- Bejelentkezéskor: megadott jelszó + tárolt salt → hash → összehasonlítás a tárolt hash-sel

**Előny:** Két azonos jelszó esetén is különböző lesz a hash, így a rainbow table támadások hatástalanok.

### Borsozás (Pepper)

**Mi az a pepper:** Egy fix karaktert (vagy karaktereket) fűz hozzá minden jelszóhoz a hashelés előtt, de ezt NEM tárolja az adatbázisban.

**Működés normál belépésnél:** A rendszer végigpróbálja az összes lehetséges pepper karaktert (pl. 26 karakter a-z), amíg egyezést nem talál. Ez plusz ~2 másodpercet jelent.

**Előny:** Brute force támadások jelentősen lassulnak, mivel a támadó nem tudja, hogy milyen pepper lett használva.

## Jelszavak támadása és törése

### Gyenge pontok

- Hibás implementáció (gyenge hash algoritmus, hiányzó salt)
- Túl rövid jelszó
- Ismert jelszavak használata


### Hasznos eszköz: Hashcat

**Működés:** Szótárfájlból dolgozik és végigpróbálja az összes jelszót a megfelelő hash algoritmussal. Támogatja a GPU gyorsítást, így nagyon gyors lehet.

**Módszerek:**

- Dictionary attack: Ismert szavak listájából próbálkozik
- Brute force: Minden lehetséges kombinációt végigpróbál
- Hybrid: Kombinálja a dictionary és brute force módszereket


## Jelszavak védelme - Jelszókezelő alkalmazások

**Előnyök:**

- Erős, egyedi jelszavak generálása minden szolgáltatáshoz
- Központi, titkosított tárolás
- Csak egy mester jelszót kell megjegyezni

**Fontos:** Ésszel kell használni őket - erős mester jelszó, kétfaktoros hitelesítés, megbízható szolgáltató választása.

**Példák:** Bitwarden, 1Password, KeePass, LastPass

## Kvantumszámítógépek

### Lényeg

A kvantumszámítógépek párhuzamos számítások hipersebességű végzésére képesek, kihasználva a kvantummechanika jelenségeit (szuperpozíció, összefonódás).

### Veszély a titkosításra

**Shor algoritmus:** Egy kvantumalgoritmus, amely képes nagy számokat hatékonyan faktorizálni. Ez azt jelenti, hogy az RSA titkosítást fel tudja törni, mivel az RSA biztonságosságának alapja a nagy prímszámok faktorizálásának nehézsége.

**Következmények:**

- A jelenleg használt publikus kulcsú titkosítási módszerek (RSA, Diffie-Hellman) sebezhetővé válnak
- Új, kvantumbiztos titkosítási algoritmusok fejlesztése szükséges
- A kriptográfiai közösség már dolgozik post-quantum kriptográfiai megoldásokon


## Támadási típusok

### MITM támadás (Man-in-the-Middle)

**Lényeg:** A hálózat működésén alapul. A kommunikáció folyamatába beállunk mint külső fél, és lehallgatjuk vagy módosítjuk az oda-vissza küldött adatokat.

**Működés:**

1. A támadó a két kommunikáló fél közé helyezi magát
2. Az egyik fél számára a támadó a másik félnek tűnik, és fordítva
3. A támadó lehallgathatja, módosíthatja vagy ellophatja az adatokat
4. A felek nem veszik észre, hogy valaki harmadik fél van közöttük

**Példák:**

- Hotel Wi-Fi hálózati bejelentkező oldal utánzása
- Hamis router üzemeltetése nyilvános helyen
- ARP spoofing a helyi hálózaton


### Védekezés MITM ellen

**Hasznos eszköz: Port scan** - Portok vizsgálata, nyitott és sebezhető portok felderítése.

**Védekezési módszerek:**

- Tűzfal használata
- Megfelelő szerverbeállítások
- HTTPS használata minden kommunikációhoz
- VPN alkalmazása nyilvános hálózatokon
- Tanúsítványok ellenőrzése


## Social Engineering

### Felhasználómenedzsment

**Különböző hozzáférési körök létrehozása:**

**RBAC (Role-Based Access Control):** Szerepkör alapú hozzáférés-vezérlés. A felhasználók jogosultságait a szerepkörük határozza meg (pl. admin, fejlesztő, user).

**ABAC (Attribute-Based Access Control):** Attribútum alapú hozzáférés-vezérlés. A felhasználók jellemzői, környezeti változók és erőforrás attribútumok alapján történik a jogosultságkezelés (pl. időpont, lokáció, projekttag).

### Pszichológiai manipuláció

**Lényeg:** Az emberi tényező kihasználása. A támadók nem technikai sebezhetőségeket használnak, hanem az emberek bizalmát, félelmét vagy tudatlanságát.

**Módszerek:**

- Félrevezetés
- Sürgősség keltése
- Tekintély megszemélyesítése
- Megbízható személy imitálása


### Adathalászat (Phishing)

**Lényeg:** Hamis e-mailek küldése, amelyek megbízható forrásból származónak tűnnek.

**Típusok:**

- **Spear phishing:** Célzott támadás konkrét személyek ellen, személyre szabott üzenetekkel
- **Whaling:** Magas beosztású vezetők elleni támadás
- **Vishing:** Telefonos adathalászat
- **Smishing:** SMS-ben történő adathalászat

**Cél:** Bizalmas információk megszerzése (jelszavak, bankkártya adatok) vagy rosszindulatú program letöltése.

## DNS Poisoning

**Lényeg:** A Domain Name System (DNS) rekordok módosítása, hogy a forgalmat hamis weboldalra irányítsa.

**Példa:** A felhasználó a `nicebank.com` címet írja be, de a meghamisított DNS miatt a `n1cebank.com` (1-es szám az i helyett) hamis oldalra kerül.

**Veszély:** Az áldozat bizalmas információkat ad meg a hamis oldalon, amelyeket a támadó ellophat.

## Host file módosítás

**Lényeg:** Ez lokális DNS-hez hasonló működés. A host fájl közvetlenül a számítógépen tárolja a domain név és IP cím párosításokat.

**Működés:**

1. A támadó hozzáfér az áldozat számítógépéhez (malware vagy fizikai hozzáférés)
2. Módosítja a host fájlt (Windows: `C:\Windows\System32\drivers\etc\hosts`, Linux: `/etc/hosts`)
3. Hamis bejegyzéseket ad hozzá (pl. `192.168.1.100 facebook.com`)
4. Amikor az áldozat megnyitja a domain-t, a hamis IP-re kerül

## DoS és DDoS

### DoS (Denial of Service)

**Lényeg:** Szolgáltatásmegtagadás - nagyon sok kérés küldése egyszerre egy szerverre vagy szolgáltatásra.

**Nem feltétlenül támadás:** Black Friday napján valós userek is okozhatnak túlterhelést a webáruházakban.

### DDoS (Distributed Denial of Service)

**Lényeg:** Elosztott szolgáltatásmegtagadás - több számítógépről vagy eszközről koordinált támadás.

**Működés:**

1. A támadó malware-rel fertőz meg számos számítógépet (botnet létrehozása)
2. Ezeket a gépeket távolról irányítva egyidejűleg küldenek kéréseket
3. A célszerver nem bírja el a terhelést, leáll vagy elérhetetlenné válik

**Támadás típusok:**

- **Volumetrikus támadások:** Hálózati sávszélesség túlterhelése (ICMP flood, UDP flood)
- **Protokoll támadások:** Protokoll sebezhetőségek kihasználása (SYN flood)
- **Alkalmazásréteg támadások:** Webszerverek erőforrásainak kimerítése (HTTP flood)


### SYN Flood

A TCP háromágú kézfogás kihasználása. A támadó sok SYN csomagot küld, de nem válaszol a SYN-ACK csomagokra, így a szerver várakozó kapcsolatokkal telik meg.

## Slow Loris DoS

**Lényeg:** Nagyon lassú HTTP kapcsolatokat küldünk, és ezzel lefoglaljuk a szervert, mert az fenntartja a kapcsolatokat.

**Működés:**

1. A támadó HTTP kéréseket küld, de nagyon lassan
2. Periodikusan küld HTTP headereket, hogy a kapcsolat ne záródjon le
3. A szerver nyitva tartja ezeket a kapcsolatokat, vár a kérés befejezésére
4. Idővel minden szerver szál foglalt lesz, új legitim kéréseket nem tud kiszolgálni

**Előny (támadó szemszéléből):** Kevés sávszélességgel is hatékony, nehezebb észrevenni.

## Session Hijacking

**Lényeg:** Cookie-k ellopása vagy token ellopás (pl. local storage-ből).

**Működés:**

1. **Cookie ellopás:** A támadó XSS vagy MITM támadással megszerzi a felhasználó session cookie-ját
2. **Token ellopás:** JavaScript kóddal kiolvassa a local storage-ből vagy session storage-ből a JWT tokent
3. A támadó ezekkel a hitelesítési adatokkal bejelentkezik az áldozat nevében

**Példák:**

- XSS támadással cookie lopás: `document.cookie`
- Local storage kiolvasa: `localStorage.getItem('token')`
- Session fixation: A támadó előre beállít egy session ID-t

**Védekezés:**

- HttpOnly flag a cookie-kon (JavaScript nem érheti el)
- Secure flag (csak HTTPS-en küldi)
- Token lejárati idő beállítása
- IP cím és user agent ellenőrzés
- CSRF tokenek használata


## SQL Injection

**Lényeg:** Kódot csempészünk egy kérésbe, ami lefut a szerveren és hozzáférést biztosít az adatbázishoz.

**Példa:**

```sql
-- Normál lekérdezés:
SELECT * FROM users WHERE username = 'admin' AND password = 'pass123'

-- SQL injection a username mezőben:
admin' OR '1'='1' --

-- Eredmény lekérdezés:
SELECT * FROM users WHERE username = 'admin' OR '1'='1' --' AND password = 'pass123'
```

A `--` komment jel, így az utána lévő jelszó ellenőrzés nem fut le. Az `'1'='1'` mindig igaz, így a támadó belép admin jogosultsággal.

**Veszélyek:**

- Adatok kiolvasása, módosítása, törlése
- Admin jogosultság megszerzése
- Teljes adatbázis letöltése
- Fájlok feltöltése a szerverre
- Remote code execution bizonyos esetekben
**Védekezés:**

- Prepared statements használata (paraméteres lekérdezések)
- Input validáció és sanitization
- Principle of least privilege (minimális jogosultságok)
- WAF (Web Application Firewall) alkalmazása
- Rendszeres biztonsági audit




















