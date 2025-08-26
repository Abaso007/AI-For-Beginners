<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "4522e22e150be0845e03aa41209a39d5",
  "translation_date": "2025-08-25T21:49:11+00:00",
  "source_file": "lessons/5-NLP/13-TextRep/README.md",
  "language_code": "hu"
}
-->
# Szöveg ábrázolása tenzorokként

## [Előadás előtti kvíz](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/113)

## Szövegklasszifikáció

A szekció első részében a **szövegklasszifikáció** feladatra fogunk összpontosítani. Az [AG News](https://www.kaggle.com/amananandrai/ag-news-classification-dataset) adathalmazt fogjuk használni, amely olyan hírcikkeket tartalmaz, mint például:

* Kategória: Tudomány/Technológia  
* Cím: Ky. cég támogatást nyert peptidek tanulmányozására (AP)  
* Szöveg: AP - Egy, a Louisville-i Egyetem kémiai kutatója által alapított cég támogatást nyert egy fejlesztéshez...

Célunk az lesz, hogy a híreket a szöveg alapján az egyik kategóriába soroljuk.

## Szöveg ábrázolása

Ha neurális hálózatokkal szeretnénk természetes nyelvfeldolgozási (NLP) feladatokat megoldani, szükségünk van egy módszerre, amellyel a szöveget tenzorokként ábrázolhatjuk. A számítógépek már most is számokként ábrázolják a szöveges karaktereket, amelyek a képernyőn megjelenő betűtípusokhoz rendelhetők, például ASCII vagy UTF-8 kódolás segítségével.

<img alt="Kép, amely egy karakter ASCII és bináris ábrázolását mutatja" src="images/ascii-character-map.png" width="50%"/>

> [Kép forrása](https://www.seobility.net/en/wiki/ASCII)

Az emberek megértik, hogy egy-egy betű **mit jelent**, és hogyan állnak össze a karakterek egy mondat szavaivá. A számítógépek azonban önmagukban nem rendelkeznek ilyen megértéssel, és a neurális hálózatnak ezt a jelentést a tanulás során kell elsajátítania.

Ezért különböző megközelítéseket alkalmazhatunk a szöveg ábrázolására:

* **Karakter szintű ábrázolás**, amikor a szöveget úgy ábrázoljuk, hogy minden karaktert egy számként kezelünk. Ha a szövegkorpusznak *C* különböző karaktere van, akkor a *Hello* szó egy 5x*C* méretű tenzorként ábrázolható. Minden betű egy-egy oszlopot jelentene a tenzorban, egy-egy one-hot kódolással.
* **Szó szintű ábrázolás**, amelyben egy **szókincset** hozunk létre a szöveg összes szavából, majd a szavakat one-hot kódolással ábrázoljuk. Ez a megközelítés valamivel jobb, mert az egyes betűk önmagukban nem hordoznak sok jelentést, így a magasabb szintű szemantikai egységek - a szavak - használatával egyszerűsítjük a neurális hálózat feladatát. Azonban a nagy szótárméret miatt magas dimenziójú, ritka tenzorokkal kell dolgoznunk.

Bármelyik ábrázolást is választjuk, először a szöveget **tokenek** sorozatává kell alakítanunk, ahol egy token lehet egy karakter, egy szó, vagy akár egy szó egy része is. Ezután a tokent egy számmá alakítjuk, általában egy **szókincs** segítségével, és ezt a számot one-hot kódolással tápláljuk be a neurális hálózatba.

## N-gramok

A természetes nyelvben a szavak pontos jelentése csak a kontextusban érthető meg. Például a *neurális hálózat* és a *halászháló* jelentése teljesen eltérő. Az egyik módja annak, hogy ezt figyelembe vegyük, ha a modellünket szópárokra építjük, és a szópárokat külön szókincsbeli tokenekként kezeljük. Így a *Szeretek horgászni menni* mondat a következő tokenek sorozataként ábrázolható: *Szeretek horgászni*, *horgászni menni*. Az ezzel a megközelítéssel járó probléma az, hogy a szótár mérete jelentősen megnő, és az olyan kombinációk, mint *horgászni menni* és *vásárolni menni* külön tokenekként jelennek meg, amelyek nem osztoznak semmilyen szemantikai hasonlóságon, annak ellenére, hogy ugyanaz az ige szerepel bennük.

Bizonyos esetekben érdemes lehet tri-gramokat -- három szóból álló kombinációkat -- is használni. Ezért ezt a megközelítést gyakran **n-gramoknak** nevezik. Érdemes lehet n-gramokat karakter szintű ábrázolásnál is használni, ahol az n-gramok nagyjából a különböző szótagoknak felelnek meg.

## Bag-of-Words és TF/IDF

Amikor olyan feladatokat oldunk meg, mint a szövegklasszifikáció, szükségünk van arra, hogy a szöveget egy fix méretű vektorként ábrázoljuk, amelyet bemenetként használhatunk a végső sűrű osztályozóhoz. Az egyik legegyszerűbb módja ennek az, ha az egyes szavak ábrázolásait kombináljuk, például összeadással. Ha minden szó one-hot kódolását összeadjuk, akkor egy gyakorisági vektort kapunk, amely megmutatja, hogy az egyes szavak hányszor fordulnak elő a szövegben. Az ilyen szövegábrázolást **bag-of-words**-nek (BoW) nevezzük.

<img src="images/bow.png" width="90%"/>

> Kép a szerzőtől

A BoW lényegében azt mutatja meg, hogy mely szavak fordulnak elő a szövegben, és milyen mennyiségben, ami valóban jó indikátora lehet annak, hogy miről szól a szöveg. Például egy politikai hírcikk valószínűleg olyan szavakat tartalmaz, mint *elnök* és *ország*, míg egy tudományos publikációban olyan szavak szerepelhetnek, mint *ütköztető*, *felfedezés*, stb. Így a szavak gyakorisága sok esetben jó indikátora lehet a szöveg tartalmának.

A BoW problémája, hogy bizonyos gyakori szavak, mint például *és*, *van*, stb., a legtöbb szövegben előfordulnak, és ezeknek a legmagasabb a gyakorisága, elnyomva az igazán fontos szavakat. Csökkenthetjük ezeknek a szavaknak a fontosságát, ha figyelembe vesszük, hogy milyen gyakran fordulnak elő az egész dokumentumgyűjteményben. Ez a fő ötlete a TF/IDF megközelítésnek, amelyet részletesebben tárgyalunk az ehhez a leckéhez tartozó jegyzetfüzetekben.

Azonban egyik megközelítés sem képes teljes mértékben figyelembe venni a szöveg **szemantikáját**. Ehhez erősebb neurális hálózati modellekre van szükség, amelyeket később tárgyalunk ebben a szekcióban.

## ✍️ Gyakorlatok: Szövegábrázolás

Folytasd a tanulást a következő jegyzetfüzetekben:

* [Szövegábrázolás PyTorch segítségével](../../../../../lessons/5-NLP/13-TextRep/TextRepresentationPyTorch.ipynb)  
* [Szövegábrázolás TensorFlow segítségével](../../../../../lessons/5-NLP/13-TextRep/TextRepresentationTF.ipynb)  

## Összegzés

Eddig olyan technikákat tanulmányoztunk, amelyek súlyt adnak a különböző szavak gyakoriságának. Ezek azonban nem képesek a jelentést vagy a sorrendet ábrázolni. Ahogy a híres nyelvész, J. R. Firth 1935-ben mondta: "Egy szó teljes jelentése mindig kontextuális, és a kontextustól független jelentés tanulmányozása nem vehető komolyan." A kurzus későbbi részében megtanuljuk, hogyan ragadhatjuk meg a szöveg kontextuális információit nyelvi modellezés segítségével.

## 🚀 Kihívás

Próbálj ki más gyakorlatokat a bag-of-words és különböző adatmodellek használatával. Inspirációt meríthetsz ebből a [Kaggle versenyből](https://www.kaggle.com/competitions/word2vec-nlp-tutorial/overview/part-1-for-beginners-bag-of-words).

## [Előadás utáni kvíz](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/213)

## Áttekintés és önálló tanulás

Gyakorold a szövegbeágyazások és a bag-of-words technikák használatát a [Microsoft Learn](https://docs.microsoft.com/learn/modules/intro-natural-language-processing-pytorch/?WT.mc_id=academic-77998-cacaste) oldalon.

## [Feladat: Jegyzetfüzetek](assignment.md)

**Felelősség kizárása**:  
Ez a dokumentum az AI fordítási szolgáltatás [Co-op Translator](https://github.com/Azure/co-op-translator) segítségével lett lefordítva. Bár törekszünk a pontosságra, kérjük, vegye figyelembe, hogy az automatikus fordítások hibákat vagy pontatlanságokat tartalmazhatnak. Az eredeti dokumentum az eredeti nyelvén tekintendő hiteles forrásnak. Kritikus információk esetén javasolt professzionális emberi fordítást igénybe venni. Nem vállalunk felelősséget semmilyen félreértésért vagy téves értelmezésért, amely a fordítás használatából eredhet.