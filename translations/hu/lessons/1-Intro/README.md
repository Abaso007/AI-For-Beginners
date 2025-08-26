<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "5d1cbc67a9690adb5b33adf297794087",
  "translation_date": "2025-08-25T22:16:18+00:00",
  "source_file": "lessons/1-Intro/README.md",
  "language_code": "hu"
}
-->
# Bevezetés az MI-hez

![Az MI bevezetésének összefoglalása egy rajzban](../../../../translated_images/ai-intro.bf28d1ac4235881c096f0ffdb320ba4102940eafcca4e9d7a55a03914361f8f3.hu.png)

> Sketchnote készítette: [Tomomi Imura](https://twitter.com/girlie_mac)

## [Előadás előtti kvíz](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/101)

**Mesterséges Intelligencia** egy izgalmas tudományág, amely azt vizsgálja, hogyan lehet számítógépeket intelligens viselkedésre bírni, például olyan dolgokra, amelyekben az emberek jók.

Eredetileg a számítógépeket [Charles Babbage](https://en.wikipedia.org/wiki/Charles_Babbage) találta fel, hogy számokat kezeljenek egy jól meghatározott eljárás – algoritmus – alapján. A modern számítógépek, bár jelentősen fejlettebbek, mint a 19. században javasolt eredeti modell, még mindig ugyanazt az irányított számítási elvet követik. Ezért lehetséges egy számítógépet programozni, hogy valamit elvégezzen, ha pontosan ismerjük a cél eléréséhez szükséges lépések sorrendjét.

![Egy személy fotója](../../../../translated_images/dsh_age.d212a30d4e54fb5f68b94a624aad64bc086124bcbbec9561ae5bd5da661e22d8.hu.png)

> Fotó: [Vickie Soshnikova](http://twitter.com/vickievalerie)

> ✅ Egy személy életkorának meghatározása a fényképe alapján olyan feladat, amelyet nem lehet kifejezetten programozni, mert nem tudjuk pontosan, hogyan jutunk el egy számhoz a fejünkben, amikor ezt tesszük.

---

Vannak azonban olyan feladatok, amelyeket nem tudunk kifejezetten megoldani. Vegyük például egy személy életkorának meghatározását a fényképe alapján. Valahogy megtanuljuk ezt, mert sok példát láttunk különböző korú emberekről, de nem tudjuk pontosan megmagyarázni, hogyan csináljuk, és nem tudjuk programozni a számítógépet, hogy megtegye. Pontosan az ilyen feladatok érdeklik a **Mesterséges Intelligenciát** (röviden MI).

✅ Gondolj néhány feladatra, amelyet átruházhatnál egy számítógépre, és amely az MI segítségével előnyös lenne. Fontold meg a pénzügy, az orvostudomány és a művészetek területeit – hogyan profitálnak ezek a területek ma az MI-ből?

## Gyenge MI vs. Erős MI

Gyenge MI | Erős MI
---------------------------------------|-------------------------------------
A gyenge MI olyan rendszerekre utal, amelyeket egy adott feladatra vagy szűk feladatkörre terveztek és képeztek ki.|Az erős MI, vagy Mesterséges Általános Intelligencia (AGI), olyan rendszerekre utal, amelyek emberi szintű intelligenciával és megértéssel rendelkeznek.
Ezek a rendszerek nem általánosan intelligensek; kiválóan teljesítenek egy előre meghatározott feladatban, de hiányzik belőlük a valódi megértés vagy tudatosság.|Ezek a rendszerek képesek bármilyen szellemi feladatot elvégezni, amit egy ember meg tud tenni, alkalmazkodni különböző területekhez, és rendelkeznek egyfajta tudatossággal vagy önismerettel.
A gyenge MI példái közé tartoznak a virtuális asszisztensek, mint Siri vagy Alexa, a streaming szolgáltatások ajánlási algoritmusai, és az ügyfélszolgálati feladatokra tervezett chatbotok.|Az erős MI elérése az MI kutatásának hosszú távú célja, amely olyan rendszerek fejlesztését igényli, amelyek képesek érvelni, tanulni, megérteni és alkalmazkodni széles körű feladatokhoz és kontextusokhoz.
A gyenge MI erősen specializált, és nem rendelkezik emberi szintű kognitív képességekkel vagy általános problémamegoldó képességekkel a szűk területén kívül.|Az erős MI jelenleg elméleti koncepció, és egyetlen MI rendszer sem érte el ezt az általános intelligencia szintet.

További információért lásd **[Mesterséges Általános Intelligencia](https://en.wikipedia.org/wiki/Artificial_general_intelligence)** (AGI).

## Az intelligencia meghatározása és a Turing-teszt

Az egyik probléma az **[Intelligencia](https://en.wikipedia.org/wiki/Intelligence)** kifejezéssel kapcsolatban az, hogy nincs egyértelmű meghatározása ennek a fogalomnak. Egyesek szerint az intelligencia az **absztrakt gondolkodáshoz** vagy az **önismerethez** kapcsolódik, de nem tudjuk megfelelően definiálni.

![Macska fotója](../../../../translated_images/photo-cat.8c8e8fb760ffe45725c5b9f6b0d954e9bf114475c01c55adf0303982851b7eae.hu.jpg)

> [Fotó](https://unsplash.com/photos/75715CVEJhI) készítette: [Amber Kipp](https://unsplash.com/@sadmax) az Unsplash-en

Az *intelligencia* kifejezés kétértelműségét szemléltetve próbálj meg válaszolni egy kérdésre: "Intelligens-e egy macska?". Különböző emberek hajlamosak különböző válaszokat adni erre a kérdésre, mivel nincs univerzálisan elfogadott teszt annak bizonyítására, hogy az állítás igaz-e vagy sem. És ha úgy gondolod, hogy van – próbáld meg lefuttatni a macskádat egy IQ-teszten...

✅ Gondolkodj el egy percig arról, hogyan határozod meg az intelligenciát. Intelligens-e egy varjú, amely képes megoldani egy labirintust, hogy elérjen az ételhez? Intelligens-e egy gyerek?

---

Amikor az AGI-ról beszélünk, szükségünk van valamilyen módra, hogy megállapítsuk, valóban intelligens rendszert hoztunk-e létre. [Alan Turing](https://en.wikipedia.org/wiki/Alan_Turing) javasolt egy módszert, amelyet **[Turing-teszt](https://en.wikipedia.org/wiki/Turing_test)** néven ismerünk, és amely egyben az intelligencia definíciójaként is szolgál. A teszt egy adott rendszert összehasonlít valami eredendően intelligens dologgal – egy valódi emberrel, és mivel bármilyen automatikus összehasonlítást megkerülhet egy számítógépes program, emberi kérdezőt használunk. Tehát, ha egy ember nem képes megkülönböztetni egy valódi személyt és egy számítógépes rendszert szöveges párbeszédben – a rendszert intelligensnek tekintjük.

> Egy [Eugene Goostman](https://en.wikipedia.org/wiki/Eugene_Goostman) nevű chatbot, amelyet Szentpéterváron fejlesztettek, 2014-ben közel került a Turing-teszt teljesítéséhez egy ügyes személyiségtrükk segítségével. Előre bejelentette, hogy egy 13 éves ukrán fiú, ami megmagyarázta a tudás hiányát és néhány eltérést a szövegben. A bot meggyőzte a bírák 30%-át arról, hogy ember, egy 5 perces párbeszéd után, egy olyan mérőszámot, amelyet Turing szerint egy gép képes lenne teljesíteni 2000-re. Azonban meg kell érteni, hogy ez nem jelenti azt, hogy intelligens rendszert hoztunk létre, vagy hogy egy számítógépes rendszer megtévesztette az emberi kérdezőt – nem a gép tévesztette meg az embereket, hanem a bot készítői!

✅ Téged valaha megtévesztett egy chatbot, hogy azt hidd, emberrel beszélsz? Hogyan győzött meg?

## Különböző megközelítések az MI-hez

Ha azt akarjuk, hogy egy számítógép úgy viselkedjen, mint egy ember, valahogy modelleznünk kell a számítógépben a gondolkodásunk módját. Ennek megfelelően meg kell próbálnunk megérteni, mi teszi az embert intelligenssé.

> Ahhoz, hogy intelligenciát programozzunk egy gépbe, meg kell értenünk, hogyan működnek a saját döntéshozatali folyamataink. Ha egy kicsit önvizsgálatot végzel, rájössz, hogy vannak olyan folyamatok, amelyek tudat alatt zajlanak – például meg tudjuk különböztetni a macskát a kutyától anélkül, hogy gondolkodnánk rajta –, míg mások érvelést igényelnek.

Két lehetséges megközelítés létezik:

Felülről lefelé irányuló megközelítés (Szimbolikus érvelés) | Alulról felfelé irányuló megközelítés (Neurális hálózatok)
---------------------------------------|-------------------------------------
A felülről lefelé irányuló megközelítés modellezi azt, ahogyan egy ember érvel egy probléma megoldásához. Ez magában foglalja az emberi **tudás** kinyerését és számítógéppel olvasható formában történő ábrázolását. Emellett ki kell fejlesztenünk egy módot az **érvelés** modellezésére a számítógépben. | Az alulról felfelé irányuló megközelítés modellezi az emberi agy szerkezetét, amely hatalmas számú egyszerű egységből, úgynevezett **neuronokból** áll. Minden neuron a bemeneteinek súlyozott átlagaként működik, és egy neuronhálózatot hasznos problémák megoldására taníthatunk **tanulási adatok** biztosításával.

Vannak más lehetséges megközelítések is az intelligenciához:

* Az **Emergens**, **Szinergikus** vagy **többügynökös megközelítés** azon az elven alapul, hogy összetett intelligens viselkedés érhető el számos egyszerű ügynök interakciójával. Az [evolúciós kibernetika](https://en.wikipedia.org/wiki/Global_brain#Evolutionary_cybernetics) szerint az intelligencia *kialakulhat* egyszerűbb, reaktív viselkedésből a *metarendszer átmenet* folyamatában.

* Az **Evolúciós megközelítés**, vagy **genetikus algoritmus** egy optimalizációs folyamat, amely az evolúció elvein alapul.

Ezeket a megközelítéseket később fogjuk megvizsgálni a kurzus során, de most két fő irányra összpontosítunk: felülről lefelé és alulról felfelé.

### Felülről lefelé irányuló megközelítés

A **felülről lefelé irányuló megközelítésben** megpróbáljuk modellezni az érvelésünket. Mivel követni tudjuk a gondolatainkat, amikor érvelünk, megpróbálhatjuk formalizálni ezt a folyamatot, és programozni a számítógépbe. Ezt **szimbolikus érvelésnek** nevezzük.

Az emberek hajlamosak bizonyos szabályokat tartani a fejükben, amelyek irányítják döntéshozatali folyamataikat. Például, amikor egy orvos diagnosztizál egy beteget, rájöhet, hogy az illetőnek láza van, és így valószínűleg valamilyen gyulladás zajlik a testben. Egy nagy szabályhalmaz alkalmazásával egy adott problémára az orvos képes lehet végleges diagnózist felállítani.

Ez a megközelítés erősen támaszkodik a **tudásábrázolásra** és az **érvelésre**. A tudás kinyerése egy emberi szakértőtől lehet a legnehezebb rész, mert egy orvos sok esetben nem tudja pontosan, miért jut egy adott diagnózishoz. Néha a megoldás egyszerűen csak megjelenik a fejében anélkül, hogy kifejezetten gondolkodna. Néhány feladat, például egy személy életkorának meghatározása egy fényképről, egyáltalán nem redukálható a tudás manipulálására.

### Alulról felfelé irányuló megközelítés

Alternatívaként megpróbálhatjuk modellezni az agyunk legegyszerűbb elemeit – a neuront. Létrehozhatunk egy úgynevezett **mesterséges neurális hálózatot** a számítógépben, majd megpróbálhatjuk megtanítani problémák megoldására példák bemutatásával. Ez a folyamat hasonló ahhoz, ahogyan egy újszülött gyermek tanul a környezetéről megfigyelések révén.

✅ Kutass egy kicsit arról, hogyan tanulnak a csecsemők. Mik az alapvető elemei egy csecsemő agyának?

> | Mi a helyzet az ML-lel?         |      |
> |--------------|-----------|
> | Az MI azon része, amely azon alapul, hogy a számítógép megtanulja megoldani egy problémát bizonyos adatok alapján, **gépi tanulásnak** nevezzük. Ebben a kurzusban nem foglalkozunk a klasszikus gépi tanulással – erre külön [Gépi Tanulás Kezdőknek](http://aka.ms/ml-beginners) tananyagot ajánlunk. |   ![ML Kezdőknek](../../../../translated_images/ml-for-beginners.9e4fed176fd5817d7d1f7d358302515186579cbf09b2a6c5bd8092b345da7f22.hu.png)    |

## Az MI rövid története

A mesterséges intelligencia mint terület a huszadik század közepén indult. Kezdetben a szimbolikus érvelés volt a domináns megközelítés, és számos fontos sikert eredményezett, például szakértői rendszereket – számítógépes programokat, amelyek képesek voltak szakértőként működni bizonyos korlátozott problématerületeken. Azonban hamar világossá vált, hogy ez a megközelítés nem skálázható jól. A tudás kinyerése egy szakértőtől, annak számítógépes ábrázolása és a tudásbázis pontosan tartása rendkívül összetett és sok esetben túl drága feladatnak bizonyult. Ez az úgynevezett [MI Tél](https://en.wikipedia.org/wiki/AI_winter) időszakához vezetett az 1970-es években.

> Kép készítette: [Dmitry Soshnikov](http://soshnikov.com)

Ahogy telt az idő, a számítástechnikai erőforrások olcsóbbá váltak, és több adat vált elérhetővé, így a neurális hálózati megközelítések elkezdtek kiváló teljesítményt mutatni az emberi versenytársakkal szemben számos területen, például a számítógépes látásban vagy a beszédértésben. Az elmúlt évtizedben a mesterséges intelligencia kifejezést leginkább a neurális hálózatok szinonimájaként használták, mivel az MI sikerei, amelyeket hallunk, többnyire ezekre épülnek.

Megfigyelhetjük, hogyan változtak a megközelítések például egy sakkjátszó számítógépes program létrehozásában:

* A korai sakkprogramok keresésen alapultak – a program kifejezetten megpróbálta megbecsülni az ellenfél lehetséges lépéseit egy adott számú következő lépésre, és kiválasztotta az optimális lépést az alapján, hogy milyen optimális pozíció érhető el néhány lépésben. Ez vezetett az úgynevezett [alfa-béta metszés](https://en.wikipedia.org/wiki/Alpha%E2%80%93beta_pruning) keresési algoritmus kifejlesztéséhez.
* A keresési stratégiák jól működnek a játék végén, ahol a keresési tér korlátozott a kevés lehetséges lépés által. Azonban a játék elején a keresési tér hatalmas, és az algoritmus javítható az emberi játékosok közötti meglévő mérkőzésekből való tanulással. A későbbi kísérletek úgynevezett [esetalapú érvelést](https://en.wikipedia.org/wiki/Case-based_reasoning) alkalmaztak, ahol a program olyan eseteket keresett a tudásbázisban, amelyek nagyon hasonlóak az aktuális pozícióhoz a játékban.
* A modern programok, amelyek legyőzik az emberi játékosokat, neurális hálózatokon és [megerősítéses tanuláson](https://en.wikipedia.org/wiki/Reinforcement_learning) alapulnak, ahol a programok kizárólag azáltal

> Kép Dmitry Soshnikovtól, [fotó](https://unsplash.com/photos/r8LmVbUKgns) Marina Abrosimovától, [Unsplash](https://unsplash.com/@abrosimova_marina_foto)

## Legújabb AI Kutatások

A neurális hálózatok kutatásának hatalmas növekedése körülbelül 2010-ben kezdődött, amikor nagy nyilvános adatbázisok váltak elérhetővé. Egy hatalmas képgyűjtemény, az úgynevezett [ImageNet](https://en.wikipedia.org/wiki/ImageNet), amely körülbelül 14 millió annotált képet tartalmaz, életre hívta az [ImageNet Large Scale Visual Recognition Challenge](https://image-net.org/challenges/LSVRC/) versenyt.

![ILSVRC Pontosság](../../../../lessons/1-Intro/images/ilsvrc.gif)

> Kép [Dmitry Soshnikovtól](http://soshnikov.com)

2012-ben először használták a [Konvolúciós Neurális Hálózatokat](../4-ComputerVision/07-ConvNets/README.md) képosztályozásra, ami jelentős csökkenést eredményezett az osztályozási hibákban (majdnem 30%-ról 16,4%-ra). 2015-ben a Microsoft Research ResNet architektúrája [emberi szintű pontosságot ért el](https://doi.org/10.1109/ICCV.2015.123).

Azóta a neurális hálózatok számos feladatban rendkívül sikeresek voltak:

---

Év | Emberi szintű teljesítmény elérése
-----|--------
2015 | [Képosztályozás](https://doi.org/10.1109/ICCV.2015.123)
2016 | [Beszédfelismerés](https://arxiv.org/abs/1610.05256)
2018 | [Automatikus gépi fordítás](https://arxiv.org/abs/1803.05567) (kínai-angol)
2020 | [Képaláírás generálás](https://arxiv.org/abs/2009.13682)

Az elmúlt néhány évben hatalmas sikereket láthattunk a nagy nyelvi modellekkel, mint például a BERT és a GPT-3. Ez főként annak köszönhető, hogy rengeteg általános szöveges adat áll rendelkezésre, amely lehetővé teszi, hogy modelleket képezzünk a szövegek szerkezetének és jelentésének megragadására, általános szöveggyűjteményeken előképzést végezzünk, majd ezeket a modelleket specifikusabb feladatokra specializáljuk. A [Természetes Nyelvfeldolgozásról](../5-NLP/README.md) később többet fogunk tanulni ebben a kurzusban.

## 🚀 Kihívás

Tegyél egy internetes körutat, hogy meghatározd, véleményed szerint hol használják az AI-t a leghatékonyabban. Egy térképező alkalmazásban, egy beszéd-szöveg szolgáltatásban vagy egy videojátékban? Kutasd fel, hogyan építették fel a rendszert.

## [Előadás utáni kvíz](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/201)

## Áttekintés és Önálló Tanulás

Tekintsd át az AI és ML történetét, olvasd el [ezt a leckét](https://github.com/microsoft/ML-For-Beginners/tree/main/1-Introduction/2-history-of-ML). Válassz ki egy elemet a sketchnote-ból ennek a leckének az elején vagy ebből, és kutasd mélyebben, hogy megértsd a kulturális kontextust, amely befolyásolta annak fejlődését.

**Feladat**: [Game Jam](assignment.md)

**Felelősség kizárása**:  
Ez a dokumentum az AI fordítási szolgáltatás [Co-op Translator](https://github.com/Azure/co-op-translator) segítségével lett lefordítva. Bár törekszünk a pontosságra, kérjük, vegye figyelembe, hogy az automatikus fordítások hibákat vagy pontatlanságokat tartalmazhatnak. Az eredeti dokumentum az eredeti nyelvén tekintendő hiteles forrásnak. Fontos információk esetén javasolt professzionális emberi fordítást igénybe venni. Nem vállalunk felelősséget semmilyen félreértésért vagy téves értelmezésért, amely a fordítás használatából eredhet.