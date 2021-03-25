# Ahrefování
Přehled věcí, co jsme zatím probírali (a občas něco navíc).

- [Ahrefování](#ahrefování)
  - [Obecně](#obecně)
  - [HTML](#html)
    - [Základní pravidla](#základní-pravidla)
    - [Základní struktura](#základní-struktura)
      - [Odsazení (indentation)](#odsazení-indentation)
    - [Tagy](#tagy)
      - [Strukturní](#strukturní)
      - [Metadata](#metadata)
      - [Obsahové - blokové](#obsahové---blokové)
      - [Obsahové - inline](#obsahové---inline)
      - [Multimédia](#multimédia)
      - [Tabulky](#tabulky)
      - [Formuláře](#formuláře)
    - [Atributy](#atributy)
  - [CSS](#css)
  - [JavaScript](#javascript)
  - [Programy a nástroje](#programy-a-nástroje)
    - [DevTools (F12 v prohlížeči)](#devtools-f12-v-prohlížeči)
    - [Visual Studio Code (VSCode)](#visual-studio-code-vscode)
    - [Git](#git)
      - [Základní git flow](#základní-git-flow)
    - [node.js](#nodejs)
      - [NPM](#npm)
    - [ESLint](#eslint)

## Obecně
Webové programovaní se dnes prakticky odehrává ve třech různých jazycích. Každý má svůj účel:

- **HTML** (HyperText Markup Language, soubory s příponou `.html`) je _značkovací jazyk_. Definujeme s ním kostru **dokumentu** (tj. webové stránky). 
  - Dokument se skládá z jednotlivých **tagů**. Tag vypadá takhle: `<html>`. 
  - Většina tagů je **párových** (počáteční tag `<html>` musí doplňovat koncový `</html>`), některé jsou ale nepárové.
  - HTML neurčuje, jak bude dokument vypadat - říká jen "tohle je nadpis", "tohle je obrázek" - značení je **sémantické**. Správně napsané HTML pak umí zpracovat třeba slepecké čtečky.
  - HTML soubor si prohlížeč "schroustá" do takzvaného **DOM** (Document Object Model). "Texťák" s tagy se tak převede do stromové struktury, která se skládá z jednotlivých **prvků (elements)**. K DOM pak přistupujeme přes další dva jazyky.
- **CSS** (Cascading Style Sheets, soubory s příponou `.css`) je _stylovací jazyk_. Definujeme s ním, jak bude dokument napsaný v HTML vypadat. 
  - Jednotlivé prvky vybíráme přes takzvané **selektory**. Prvkům pak určujeme **vlastnosti (properties)**. Sadě selektoru a vlastností se říká **pravidlo**. Pravidlo vypadá takhle:
    ```
    html {
      font-weight: bold;
    }
    ```
  - Jednotlivých vlastností existuje několik stovek a řídí se jimi celý vzhled dokumentu - od tučnosti písma po **layout** - rozvržení stránky, kde bude jaké menu a podobně.
  - Z historických (tag `<b>` dřív znamenal vzhledové "je to tučně", ne sémantické "na tohle dávám důraz" jako dnes) i praktických (psát pořád dokola stejné základní CSS by byla pruda) důvodů mají prohlížeče pro jednotlivé tagy **výchozí styly**. Proto bude třeba tag `<b>` tučně, i když jsem si na to nenapsal pravidlo. Výchozí styly ale jdou libovolně přepsat vlastními pravidly.
- **JavaScript** (JS, soubory s příponou `.js`). je _programovací jazyk_. Umí stejné věci, co jiné programovaci jazyky - matematiku, práci s daty... Speciální je v tom, že je zabudovaný přímo do webových prohlížečů a můžeme s ním tak přistupovat k DOM a ovládat ho - JavaScript **oživuje webové stránky**.
  - JavaScript je **imperativní** - to znamená, že v něm píšeme sérii příkazů, které pak prohlížeč odshora dolů chroustá a provádí je. Příkaz vypadá třeba takhle: `const x = 2;`
  - Pozor, existuje i pořád celkem používaný jazyk Java, ale ten s JavaScriptem vůbec nesouvisí! JavaScript se původně jmenoval LiveScript, ale jeho tvůrci se v 90. letech rozhodli, že ho přejmenují podle tehdy masově populární Javy, což mělo k JavaScriptu nalákat programátory.
- Jedna z nejdůležitějších schopností při programování je orientace v dokumentaci. Všechny tři jazyky detailně dokumentuje web **[MDN (Mozilla Developer Network)](https://developer.mozilla.org/en-US/docs/Web)**. Ostatní zdroje (třeba W3Schools, které bývají první ve výsledcích na Googlu) jsou občas přívětivější, ale často nepřesné nebo zastaralé.

## HTML
Historie HTML byla plná mrzení, kdy se nikdo nemohl dohodnout, k čemu HTML vlastně bude, a každý prohlížeč si je zobrazoval jinak, ale na dnes aktuální verzi <b>HTML5</b> z roku 2014 je shoda a podoba HTML se tak naštěstí ustálila. Má i vlastní ošklivé logo:

![](img/html5logo.png)
### Základní pravidla
- Dokument má **stromovou strukturu**: i pokud bychom zmatlali HTML kód, třeba zapomenutím koncového tagu, a strom by byl rozbitý, prohlížeč ho při tvorbě DOM opraví.
- Dokument píšeme tak, že jeho obsah obalujeme do sémantických **tagů**. Tagy jsou buď párové, nebo nepárové, a můžou mít **atributy**, které definují další vlastnosti - třeba unikátní ID prvku (to se používá hlavně v JavaScriptu), třídu (ta zase v CSS) nebo nutný doplněk tagu, třeba adresu obrázku pro tag `<img>`. **Hodnota** atributu je vždy ve dvojitých uvozovkách.
- Takhle takový tag s atributy vypadá:
  `<img id="main-image" class="full-width" src="img/hlavni.jpg">`
- Do HTML můžu psát taky **komentáře**. Prohlížeč je při sestavování DOM bude ignorovat, takže si do nich můžu psát libovolné poznámky. Můžou být na víc řádků a uvozují se takhle:
  ```
  <!-- jednořádkový komentář -->
  <!-- 
    komentář na víc řádků!
    jupí!
  -->
  ```
  VSCode mi komentářové znaky automaticky vloží zkratkou `Alt+Shift+A` - to platí i pro další jazyky.
- To je vlastně všechno: celý HTML soubor je mix různých tagů s atributy a jejich obsahu, případně komentářů. Znalost HTML spočívá ve znalosti toho, který tag kdy použít a jaké má a nemá atributy.

### Základní struktura
Takhle vypadá základní HTML kostra (včetně tagů pro vložení stylu a skriptu - hodí se):

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Název stránky</title>
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <p>Text v odstavci.</p>
    <script src="script.js"></script>
  </body>
</html> 
```

Postupně:
- `<!DOCTYPE html>` je _deklarace_ typu dokumentu. Musí být na začátku každého HTML souboru. Říkáme s ní prohlížeči, že **používáme HTML5**. Bez deklarace si prohlížeč může vytvořit DOM všelijak, většinou špatně.
- Párový `<html>` uvozuje celý dokument.
- Párový `<head>` uvozuje doplňující informace o dokumentu - nejsou vidět na samotné stránce.
- `<meta charset="utf-8">` je další povinný tag. Říká, že dokument používá univerzální znakovou sadu UTF-8, což znamená, že můžeme bezpečně používat české znaky nebo třeba emoji.
- Párový `<title>` uvozuje název stránky, který je v prohlížeči vidět v horní liště jako název tabu.
- `<link>` je tag pro vkládání _externích zdrojů_. Můžou to být třeba písma nebo náhledové ikonky, v našem případě to ale bude CSS soubor (to určuje atribut `rel` - _relationship_). Umístění ve složce se zadává do atributu `href`.
- Párový `<body>` uvozuje obsah dokumentu - to, co je vidět na stránce.
- Párový `<p>` (**paragraph**) je jeden ze základních obsahových tagů, uvozuje odstavec. 
- `<script>`se používá na vkládání JS (atribut `src` určuje umístění ve složce). Takhle použitý je sice prázdný, ale musí být párový. `<script>` patří tradičně vždy **na konec** `<body>` - je to proto, že se v něm manipuluje s DOM a prohlížeč ho tak musí "přečíst" až na konec, když je zbytek DOM vytvořený. (Existuje několik modernějších způsobů, jak toho docílit, ale tenhle je jednoduchý a funguje.)

#### Odsazení (indentation)
V HTML (ale i v CSS a JS) je počítači jedno, jak budou jednotlivé řádky odsazené - celý kód by klidně mohl být na jednom řádku. Správné odsazení je nutné kvůli čitelnosti! U HTML je navíc logické, protože kopíruje stromovou strukturu DOM. `Shift+Alt+F` ve VSCode odsadí kód automaticky.

### Tagy
Tagů je spousta (něco přes stovku), tady je přehled nejdůležitějších. Celý seznam je na [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element). (U **nepárových** tagů je upozornění, zbytek je párový.)

#### Strukturní
`<html>`, `<head>` a `<body>` - všechny párové a popsané výš.
#### Metadata
Píšou se do `<head>` a všechny jsou popsané výš: `<meta>`, `<title>`, `<link>` a `<style>`.

#### Obsahové - blokové
Píšou se do `<body>` a označují nebo oddělují **bloky** obsahu. "Blok" v praxi znamená, že se obsah blokových tagů odskočí na nový řádek. (Zajišťuje to výchozí CSS pravidlo `display: block;`).
- `<div>` (_division_) je **neutrální blokový tag**. Používá se, když se nehodí nic jiného, a prohlížeče mu kromě zmíněného `display: block;` nepřiřazují žádný výchozí styl.
- `<p>` (_paragraph_) značí **odstavec textu**. Zatímco `<div>` může obsahovat cokoliv - obrázky, tabulky, formuláře, další `<div>` - `<p>` se používá čistě pro text.
- `<hr>` (původně _horizontal rule_, nepárový) značí **tématický předěl**. Prohlížeče tagu z historických důvodů přiřazují vodorovnou čáru, ale jako všude platí, že se na to nemůžeme spolehnout a tag má čistě sémantický význam, který musíme doplnit CSS.
- `<ul>` a `<ol>` (_un/ordered list_) uvozují **seznamy** - ty v `<ol>` jsou typicky číslované. **Položky** v seznamu se uvozují párovým `<li>`.

#### Obsahové - inline
Píšou se do `<body>` a označují vlastnosti částí textu v bloku. V praxi zůstane text označený inline tagem na stejném řádku jako obsah před ním - tagy mají výchozí CSS pravidlo `display: inline;`.
- `<span>` je **neutrální inline tag**. Je to inline obdoba `<div>` - používá se, když se nehodí nic jiného, třeba když chci nějakému úseku textu přidat třídu.
- `<a>` (_anchor_) je **odkaz**. Má povinný atribut `href`, který určuje, kam odkaz povede.
- `<br>` (_break_, nepárový) značí **konec řádku**. Častá chyba je používat jedno nebo několik `<br>` za sebou na "odražení" odstavce od předchozího - odstavce mají správně být obaleny tagem `<p>`, kterému můžeme přiřadit CSS pravidlo `margin-bottom`.
- `<b>` (původně _bold_) a `<strong>` označují **výrazný text**. Sémanticky je mezi nimi rozdíl (viz [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/strong#%3Cb%3E_vs._%3Cstrong%3E)), ale v praxi se docela zaměňují. Prohlížeče jejich obsah defaultně ztučňují (`font-weight: bold;`).
- `<em>` (_emphasis_) a `<i>` (_idiomatic_, původně _italics_) značí **zdůrazněný text**. Výchozí styl obou tagů je kurzíva (`font-style: italic;`), ale stejně jako u `<b>`/`<strong>` platí, že je mezi nimi sémantický rozdíl (viz [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/em#%3Ci%3E_vs._%3Cem%3E)) a CSS pravidla bychom jim měli nastavit sami.

#### Multimédia
- `<img>` (_image_m nepárový) vkládá obrázek. Má povinný atribut `src`, který určuje umístění obrázku, a neměl by chybět ani atribut `alt` - popisek toho, co na obrázku je, třeba pro čtečky.
- Existují taky nepárové tagy `<audio>` a `<video>`, kterými prohlížeče automaticky opatří vložený obsah audio/video přehrávačem. Dokumentace je na [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element#image_and_multimedia).

#### Tabulky
Nejjednodušší je ukázat tabulkové tagy v praxi. Kód:

```
<table>
  <thead>
    <tr>
      <td>Jméno</td>
      <td>Příjmení</td>
      <td>Počet bodů</td>
    </tr>
  </thead>
    <thead>
    <tr>
      <td>Jana</td>
      <td>Nováková</td>
      <td>10</td>
    </tr>
    <tr>
      <td>Dana</td>
      <td>Horáková</td>
      <td>12</td>
    </tr>
  </thead>
</table>
```

se defaultně zobrazí jako:

<table>
  <thead>
    <tr>
      <td>Jméno</td>
      <td>Příjmení</td>
      <td>Počet bodů</td>
    </tr>
  </thead>
    <thead>
    <tr>
      <td>Jana</td>
      <td>Nováková</td>
      <td>10</td>
    </tr>
    <tr>
      <td>Dana</td>
      <td>Horáková</td>
      <td>12</td>
    </tr>
  </thead>
</table>

#### Formuláře
Formulářových prvků je v HTML [spousta](https://developer.mozilla.org/en-US/docs/Web/HTML/Element#forms), my jsme zatím používali dva nejdůležitější.

- `<button>` 
  <button>Defaultní tlačíko</button>
- `<input>`

### Atributy

## CSS

## JavaScript

## Programy a nástroje
V praxi se pro psaní kódu i jeho spouštění používá bambilion různých programů a nástrojů. S čím jsme se zatím potkali:

### DevTools (F12 v prohlížeči)
Největší pomocník každého webového programátora. V panelu **Elements/Inspector** vidíte DOM a je zároveň možné ho upravovat. V boxíku dole jde editovat styly - je dobré si stylování zkoušet v DevTools, než je napíšu do kódu. V panelu **Console** vidím výstupy z JavaScriptu a můžu tam taky rovnou psát a zkoušet javascriptový kód.

### Visual Studio Code (VSCode)
Editor od Microsoftu, který je napsaný ve variantě JavaScriptu a běží jako program ve Windows i jinde prostřednictvím nástroje **Electron** - v zásadě je to okno prohlížeče, které se tváří, že to není okno prohlížeče. (Fungují tak i třeba MS Teams nebo Discord.) Prostřednictvím tuny rozšíření podporuje spoustu vychytávek pro všechny možné programovací jazyky, má zabudovanou podporu Gitu.

VSCode i bez rozšíření umí spoustu klávesových zkratek, které zjednodušují psaní kódu. Nám se teď nejvíc hodí `Alt+Shift+F` - automatické naformátování souboru. Komentářové znaky vloží `Alt+Shift+A`.

### Git
Systém na **verzování** - správu verzí programu (ale i čehokoliv jiného). Historicky byla dost pruda spolupracovat na kódu a správně zaznamenávat změny po verzích. Git všechno tohle řeší a dnes už se prakticky nepoužívá nic jiného. Jednotlivým "složkám" s projekty se říká **repozitáře** (repositories). Je to děsně složitý nástroj, ale my z něj naštěstí potřebujeme jen pár věcí a VSCode ho přímo podporuje (ikonka Source control v panelu nalevo).

![](img/git_vscode.jpg)

#### Základní git flow
* **Repozitář** mám jednak u sebe, jednak mám jeho dálkovou kopii - my k tomu používáme **GitHub**, hodně populární free službu od Microsoftu, která nám mj. umožňuje automaticky na web publikovat obsah repozitáře
* Jednotlivým verzím kódu se říká **commit**. Změny, které jsem udělal od předchozího commitu, vidím v git panelu ve VSCode jako *Changes*. 
* Když u nich kliknu na plusko, tak je takzvaně **stagenu** - staged soubory jsou "připravené na uložení". V panelu se přesunou do *Staged Changes*.
* Samotný commit by měl mít stručný komentář (**commit message**), kde shrnu, co v něm je. Ten se píše v panelu do boxíku nahoře. Když pak dám `Ctrl+Enter` nebo kliknu na fajfku nad boxíkem, commitou se všechny *Staged Changes* a pokud žádné nemám a všechno jsou jen *Changes*, automaticky se s tím všechny stagenou.
* Tím jsem změny uložil do svého repozitáře. V dolní liště vedle popisku "main" je pak ikonka, kde bude `↑ 1`, tzn. mám jeden commit k odeslání - **pushnutí** - do vzdáleného repozitáře (tj. na GitHubu). Když na ni kliknu, commit se pushne (a nám se i brzy publikuje na webu).

### node.js
JavaScript původně vznikl jako jazyk čistě pro prohlížeče. Pak se ale stalo, že ho uměli všichni a chtěli ho začít používat i jinde - pro programy, co běží přímo na počítači. Proto vznikl  **node.js** (nebo jen Node), který přesně tohle umožňuje. My ho používáme hlavně kvůli **NPM**:

#### NPM
Zkratka z _Node Package Manager_. Je to databáze **knihoven** - "nesamostatných" programů, které můžu přidávat do svého repozitáře a které dělají různé věci. Může to být třeba knihovna na kombinatorické výpočty, knihovna, která dokáže ze vstupních dat dělat grafy, ale i různé pomocné knihovny, které programátorům usnadňují život.

NPM je zároveň program, který knihovny instaluje. V repozitářích si můžete všimnout souboru `package.json`, když ho otevřete, uvidíte kromě jiného seznam použitých knihoven. (Pak je ještě pomocný `package-lock.json`, který se generuje automaticky, ten zajišťuje, aby se knihovny správně instalovaly.)

### ESLint
Jediná knihovna, co zatím používáme. Kontroluje **správnost i "styl" JS kódu** podle toho, jak si ho nastavíme. My používáme jedno z nejpopulárnějších nastavení od **Airbnb** (zlí kapitalisté, dobří programátoři). Díky propojení s VSCode pak přímo v kódu vidíme červeně podtržené chyby a můžeme je často i automaticky opravit (kliknutím na `Quick Fix`).
