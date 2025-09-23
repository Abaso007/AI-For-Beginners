<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "0c84b280e654e05ed658023021a6a975",
  "translation_date": "2025-09-23T11:14:52+00:00",
  "source_file": "lessons/1-Intro/README.md",
  "language_code": "hu"
}
-->
# Bevezetés az MI-be

![Az MI bevezetésének összefoglalása egy rajzban](../../../../translated_images/ai-intro.bf28d1ac4235881c096f0ffdb320ba4102940eafcca4e9d7a55a03914361f8f3.hu.png)

> Sketchnote készítette: [Tomomi Imura](https://twitter.com/girlie_mac)

## [Előadás előtti kvíz](https://ff-quizzes.netlify.app/en/ai/quiz/1)

**Mesterséges Intelligencia** egy izgalmas tudományág, amely azt vizsgálja, hogyan lehet számítógépeket intelligens viselkedésre bírni, például olyan dolgokra, amelyekben az emberek jók.

Eredetileg a számítógépeket [Charles Babbage](https://en.wikipedia.org/wiki/Charles_Babbage) találta fel, hogy számokkal dolgozzanak egy jól meghatározott eljárás – algoritmus – alapján. A modern számítógépek, bár jelentősen fejlettebbek, mint a 19. században javasolt eredeti modell, még mindig ugyanazt az irányított számítási elvet követik. Ezért lehetséges egy számítógépet programozni, hogy valamit elvégezzen, ha pontosan ismerjük azokat a lépéseket, amelyeket a cél eléréséhez meg kell tenni.

![Egy személy fotója](../../../../translated_images/dsh_age.d212a30d4e54fb5f68b94a624aad64bc086124bcbbec9561ae5bd5da661e22d8.hu.png)

> Fotó: [Vickie Soshnikova](http://twitter.com/vickievalerie)

> ✅ Egy személy életkorának meghatározása a fényképe alapján olyan feladat, amelyet nem lehet kifejezetten programozni, mert nem tudjuk pontosan, hogyan jutunk el egy számhoz a fejünkben, amikor ezt tesszük.

---

Vannak azonban olyan feladatok, amelyeket nem tudunk kifejezetten megoldani. Vegyük például egy személy életkorának meghatározását a fényképe alapján. Valahogy megtanuljuk ezt, mert sok példát láttunk különböző korú emberekről, de nem tudjuk pontosan megmagyarázni, hogyan csináljuk, és nem tudjuk programozni a számítógépet, hogy megtegye. Pontosan az ilyen feladatok érdeklik a **Mesterséges Intelligenciát** (röviden MI).

✅ Gondolj néhány feladatra, amelyet átadhatnál egy számítógépnek, és amely az MI segítségével előnyös lenne. Fontold meg a pénzügyek, az orvostudomány és a művészetek területét – hogyan profitálnak ezek a területek ma az MI-ből?

## Gyenge MI vs. Erős MI

Gyenge MI | Erős MI
---------------------------------------|-------------------------------------
A gyenge MI olyan rendszerekre utal, amelyeket egy adott feladatra vagy szűk feladatkörre terveztek és képeztek ki.|Az erős MI, vagy Mesterséges Általános Intelligencia (AGI), olyan rendszerekre utal, amelyek emberi szintű intelligenciával és megértéssel rendelkeznek.
Ezek a rendszerek nem általánosan intelligensek; kiválóan teljesítenek egy előre meghatározott feladatban, de hiányzik belőlük a valódi megértés vagy tudatosság.|Ezek a rendszerek képesek bármilyen szellemi feladatot elvégezni, amit egy ember is meg tud, alkalmazkodni különböző területekhez, és egyfajta tudatossággal vagy önismerettel rendelkeznek.
A gyenge MI példái közé tartoznak a virtuális asszisztensek, mint Siri vagy Alexa, a streaming szolgáltatások ajánlási algoritmusai, és az ügyfélszolgálati chatbotok.|Az erős MI elérése az MI kutatásának hosszú távú célja, amely olyan rendszerek fejlesztését igényli, amelyek képesek érvelni, tanulni, megérteni és alkalmazkodni széles körű feladatokhoz és kontextusokhoz.
A gyenge MI erősen specializált, és nem rendelkezik emberi szintű kognitív képességekkel vagy általános problémamegoldó képességekkel a szűk területén kívül.|Az erős MI jelenleg elméleti koncepció, és egyetlen MI rendszer sem érte el ezt az általános intelligencia szintet.

További információért lásd **[Mesterséges Általános Intelligencia](https://en.wikipedia.org/wiki/Artificial_general_intelligence)** (AGI).

## Az intelligencia definíciója és a Turing-teszt

Az egyik probléma az **[Intelligencia](https://en.wikipedia.org/wiki/Intelligence)** kifejezéssel kapcsolatban az, hogy nincs egyértelmű definíciója. Egyesek szerint az intelligencia az **absztrakt gondolkodáshoz** vagy az **önismerethez** kapcsolódik, de nem tudjuk megfelelően meghatározni.

![Macska fotója](../../../../translated_images/photo-cat.8c8e8fb760ffe45725c5b9f6b0d954e9bf114475c01c55adf0303982851b7eae.hu.jpg)

> [Fotó](https://unsplash.com/photos/75715CVEJhI) készítette: [Amber Kipp](https://unsplash.com/@sadmax) az Unsplash-ről

Az *intelligencia* kifejezés kétértelműségét szemléltetve próbálj meg válaszolni a kérdésre: "Intelligens-e egy macska?". Különböző emberek hajlamosak különböző válaszokat adni erre a kérdésre, mivel nincs univerzálisan elfogadott teszt, amely bizonyítaná az állítás igazságát vagy hamisságát. És ha úgy gondolod, hogy van – próbáld meg lefuttatni a macskádat egy IQ-teszten...

✅ Gondolkodj el egy percig arról, hogyan határozod meg az intelligenciát. Intelligens-e egy varjú, amely képes megoldani egy labirintust, hogy hozzáférjen az ételhez? Intelligens-e egy gyerek?

---

Amikor az AGI-ról beszélünk, szükségünk van egy módszerre, hogy megállapítsuk, valóban intelligens rendszert hoztunk-e létre. [Alan Turing](https://en.wikipedia.org/wiki/Alan_Turing) javasolt egy módszert, amelyet **[Turing-teszt](https://en.wikipedia.org/wiki/Turing_test)** néven ismerünk, és amely egyben az intelligencia definíciójaként is szolgál. A teszt összehasonlítja az adott rendszert valami veleszületetten intelligens dologgal – egy valódi emberrel, és mivel bármilyen automatikus összehasonlítást megkerülhet egy számítógépes program, emberi kérdezőt használunk. Tehát, ha egy ember nem képes megkülönböztetni egy valódi személyt és egy számítógépes rendszert szöveges párbeszédben – a rendszert intelligensnek tekintjük.

> Egy [Eugene Goostman](https://en.wikipedia.org/wiki/Eugene_Goostman) nevű chatbot, amelyet Szentpéterváron fejlesztettek, 2014-ben közel került a Turing-teszt teljesítéséhez egy ügyes személyiségtrükk segítségével. Előre bejelentette, hogy egy 13 éves ukrán fiú, ami megmagyarázta a tudás hiányát és néhány szövegbeli eltérést. A bot meggyőzte a bírák 30%-át, hogy ember, egy 5 perces párbeszéd után, egy olyan mérőszámot, amelyet Turing úgy gondolt, hogy egy gép képes lesz teljesíteni 2000-re. Azonban meg kell érteni, hogy ez nem jelenti azt, hogy intelligens rendszert hoztunk létre, vagy hogy egy számítógépes rendszer becsapta az emberi kérdezőt – nem a rendszer csapta be az embereket, hanem a bot készítői!

✅ Téged valaha becsapott egy chatbot, hogy azt hidd, emberrel beszélsz? Hogyan győzött meg?

## Különböző megközelítések az MI-hez

Ha azt akarjuk, hogy egy számítógép úgy viselkedjen, mint egy ember, valahogy modelleznünk kell a számítógépben a gondolkodásunk módját. Következésképpen meg kell próbálnunk megérteni, mi teszi az embert intelligenssé.

> Ahhoz, hogy intelligenciát programozzunk egy gépbe, meg kell értenünk, hogyan működnek a saját döntéshozatali folyamataink. Ha egy kis önvizsgálatot végzel, rájössz, hogy vannak olyan folyamatok, amelyek tudat alatt zajlanak – például meg tudjuk különböztetni a macskát a kutyától anélkül, hogy gondolkodnánk rajta –, míg mások érvelést igényelnek.

Két lehetséges megközelítés létezik:

Felülről lefelé irányuló megközelítés (Szimbolikus érvelés) | Alulról felfelé irányuló megközelítés (Neurális hálózatok)
---------------------------------------|-------------------------------------
A felülről lefelé irányuló megközelítés modellezi, hogyan érvel egy személy egy probléma megoldásához. Ez magában foglalja az emberi **tudás** kinyerését és számítógéppel olvasható formában történő ábrázolását. Emellett ki kell fejlesztenünk egy módot az **érvelés** modellezésére a számítógépben. | Az alulról felfelé irányuló megközelítés modellezi az emberi agy szerkezetét, amely számos egyszerű egységből, úgynevezett **neuronokból** áll. Minden neuron úgy működik, mint a bemeneteinek súlyozott átlaga, és egy neuronhálózatot hasznos problémák megoldására taníthatunk **tanulási adatok** biztosításával.

Vannak más lehetséges megközelítések is az intelligenciához:

* Az **Emergens**, **Szinergikus** vagy **multi-ügynök megközelítés** azon az elven alapul, hogy az összetett intelligens viselkedés számos egyszerű ügynök interakciójából származhat. Az [evolúciós kibernetika](https://en.wikipedia.org/wiki/Global_brain#Evolutionary_cybernetics) szerint az intelligencia *kialakulhat* egyszerűbb, reaktív viselkedésből a *metarendszer átmenet* folyamatában.

* Az **Evolúciós megközelítés**, vagy **genetikus algoritmus** egy optimalizációs folyamat, amely az evolúció elvein alapul.

Ezeket a megközelítéseket később fogjuk megvizsgálni a kurzus során, de most két fő irányra összpontosítunk: felülről lefelé és alulról felfelé.

### A Felülről Lefelé Irányuló Megközelítés

A **felülről lefelé irányuló megközelítésben** megpróbáljuk modellezni az érvelésünket. Mivel követni tudjuk a gondolatainkat, amikor érvelünk, megpróbálhatjuk formalizálni ezt a folyamatot, és programozni a számítógépbe. Ezt **szimbolikus érvelésnek** nevezzük.

Az emberek hajlamosak bizonyos szabályokat követni a fejükben, amelyek irányítják döntéshozatali folyamataikat. Például, amikor egy orvos diagnosztizál egy beteget, rájöhet, hogy az illetőnek láza van, és így valószínűleg valamilyen gyulladás zajlik a testben. Egy nagy szabályhalmaz alkalmazásával egy adott problémára az orvos képes lehet a végső diagnózisra jutni.

Ez a megközelítés erősen támaszkodik a **tudásábrázolásra** és az **érvelésre**. A tudás kinyerése egy emberi szakértőtől lehet a legnehezebb rész, mert az orvos sok esetben nem tudja pontosan, miért jut egy adott diagnózishoz. Néha a megoldás egyszerűen csak megjelenik a fejében anélkül, hogy kifejezetten gondolkodna. Néhány feladat, például egy személy életkorának meghatározása egy fényképről, egyáltalán nem redukálható a tudás manipulálására.

### Alulról Felfelé Irányuló Megközelítés

Alternatívaként megpróbálhatjuk modellezni az agyunk legegyszerűbb elemeit – a neuront. Létrehozhatunk egy úgynevezett **mesterséges neurális hálózatot** a számítógépben, majd megpróbálhatjuk megtanítani problémák megoldására példák bemutatásával. Ez a folyamat hasonló ahhoz, ahogyan egy újszülött gyermek tanul a környezetéről megfigyelések révén.

✅ Végezz egy kis kutatást arról, hogyan tanulnak a csecsemők. Mik az alapvető elemei egy csecsemő agyának?

> | Mi a helyzet az ML-lel?         |      |
> |--------------|-----------|
> | A mesterséges intelligencia azon része, amely azon alapul, hogy a számítógép megtanulja megoldani a problémát bizonyos adatok alapján, **gépi tanulásnak** nevezzük. Ebben a kurzusban nem foglalkozunk a klasszikus gépi tanulással – erre külön [Gépi Tanulás Kezdőknek](http://aka.ms/ml-beginners) tananyagot ajánlunk. |   ![ML Kezdőknek](../../../../translated_images/ml-for-beginners.9e4fed176fd5817d7d1f7d358302515186579cbf09b2a6c5bd8092b345da7f22.hu.png)    |

## Az MI Rövid Története

A mesterséges intelligencia mint terület a huszadik század közepén indult. Kezdetben a szimbolikus érvelés volt az uralkodó megközelítés, és számos fontos sikert eredményezett, például szakértői rendszereket – számítógépes programokat, amelyek képesek voltak szakértőként működni bizonyos korlátozott problématerületeken. Azonban hamar világossá vált, hogy ez a megközelítés nem skálázható jól. A tudás kinyerése egy szakértőtől, annak számítógépes ábrázolása és a tudásbázis pontosan tartása rendkívül összetett és sok esetben túl drága feladatnak bizonyult. Ez az úgynevezett [MI Tél](https://en.wikipedia.org/wiki/AI_winter) időszakához vezetett az 1970-es években.

<img alt="Az MI rövid története" src="images/history-of-ai.png" width="70%"/>

> Kép: [Dmitry Soshnikov](http://soshnikov.com)

Ahogy telt az idő, a számítástechnikai erőforrások olcsóbbá váltak, és több adat vált elérhetővé, így a neurális hálózati megközelítések nagy teljesítményt kezdtek mutatni az emberi lényekkel való versenyben számos területen, például a számítógépes látásban vagy a beszédértésben. Az elmúlt évtizedben a mesterséges intelligencia kifejezést leginkább a neurális hálózatok szinonimájaként használták, mivel az MI sikerei, amelyekről hallunk, többnyire ezekre épülnek.

Megfigyelhetjük, hogyan változtak a megközelítések például egy sakkjátszó számítógépes program létrehozásában:

* A korai sakkprogramok keresésen alapultak – a program kifejezetten megpróbálta megbecsülni az ellenfél lehetséges lépéseit egy adott számú következő lépésre, és kiválasztotta az optimális lépést az alapján, hogy milyen optimális pozíció érhető el néhány lépésben. Ez vezetett az úgynevezett [alfa-béta metszés](https://en.wikipedia.org/wiki/Alpha%E2%80%93beta_pruning) keresési algoritmus kifejlesztéséhez.
* A keresési stratégiák jól működnek a játék végén, ahol a keresési tér korlátozott a lehetséges lépések kis számával. Azonban a játék elején a keresési tér hatalmas, és az algoritmus javítható az emberi játékosok közötti meglévő mérkőzésekből való tanulással. A későbbi kísérletek úgynevezett [esetalapú érvelést](https://en.wikipedia.org/wiki/Case-based_reasoning) alkalmaztak, ahol a program olyan eseteket keresett a tudásbázisban, amelyek nagyon hasonlóak a játék aktuális pozíciójához.
* A modern programok, amelyek legyőzik az emberi játékosokat, neurális hálózatokon és [megerősítéses tanuláson](https://en.wikipedia.org/wiki/Reinforcement_learning
> Kép Dmitry Soshnikovtól, [fotó](https://unsplash.com/photos/r8LmVbUKgns) Marina Abrosimovától, [Unsplash](https://unsplash.com/@abrosimova_marina_foto)

## Legújabb AI Kutatások

A neurális hálózatok kutatásának hatalmas növekedése körülbelül 2010-ben kezdődött, amikor nagy nyilvános adatbázisok váltak elérhetővé. Egy hatalmas képgyűjtemény, az [ImageNet](https://en.wikipedia.org/wiki/ImageNet), amely körülbelül 14 millió annotált képet tartalmaz, életre hívta az [ImageNet Large Scale Visual Recognition Challenge](https://image-net.org/challenges/LSVRC/) versenyt.

![ILSVRC Pontosság](../../../../lessons/1-Intro/images/ilsvrc.gif)

> Kép [Dmitry Soshnikovtól](http://soshnikov.com)

2012-ben először használták a [Konvolúciós Neurális Hálózatokat](../4-ComputerVision/07-ConvNets/README.md) képosztályozásra, ami jelentős csökkenést eredményezett az osztályozási hibákban (majdnem 30%-ról 16,4%-ra). 2015-ben a Microsoft Research ResNet architektúrája [emberi szintű pontosságot ért el](https://doi.org/10.1109/ICCV.2015.123).

Azóta a neurális hálózatok számos feladatban rendkívül sikeresnek bizonyultak:

---

Év | Emberi szintű teljesítmény elérése
-----|--------
2015 | [Képosztályozás](https://doi.org/10.1109/ICCV.2015.123)
2016 | [Beszédfelismerés](https://arxiv.org/abs/1610.05256)
2018 | [Automatikus gépi fordítás](https://arxiv.org/abs/1803.05567) (kínai-angol)
2020 | [Képaláírás generálás](https://arxiv.org/abs/2009.13682)

Az elmúlt években hatalmas sikereket láthattunk a nagy nyelvi modellekkel, mint például a BERT és a GPT-3. Ez főként annak köszönhető, hogy rengeteg általános szöveges adat áll rendelkezésre, amely lehetővé teszi, hogy modelleket képezzünk a szövegek szerkezetének és jelentésének megragadására, általános szöveggyűjteményeken előképzésre, majd ezeknek a modelleknek a specializálására konkrétabb feladatokra. A kurzus későbbi részében többet fogunk tanulni a [Természetes Nyelvfeldolgozásról](../5-NLP/README.md).

## 🚀 Kihívás

Tegyél egy internetes körutat, hogy meghatározd, véleményed szerint hol használják az AI-t a leghatékonyabban. Egy térképező alkalmazásban, egy beszéd-szöveg szolgáltatásban vagy egy videojátékban? Kutasd fel, hogyan építették fel a rendszert.

## [Előadás utáni kvíz](https://ff-quizzes.netlify.app/en/ai/quiz/2)

## Áttekintés és Önálló Tanulás

Tekintsd át az AI és ML történetét, olvasd el [ezt a leckét](https://github.com/microsoft/ML-For-Beginners/tree/main/1-Introduction/2-history-of-ML). Válassz ki egy elemet a sketchnote-ból ennek a leckének az elején vagy ebből, és kutasd mélyebben, hogy megértsd a kulturális kontextust, amely befolyásolta annak fejlődését.

**Feladat**: [Game Jam](assignment.md)

---

