<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "06ca1b0138e65b964481ae83275b270e",
  "translation_date": "2025-10-03T08:53:36+00:00",
  "source_file": "lessons/1-Intro/README.md",
  "language_code": "ro"
}
-->
# Introducere în Inteligența Artificială

![Rezumat al conținutului Introducere în AI într-un desen](../../../../translated_images/ai-intro.bf28d1ac4235881c096f0ffdb320ba4102940eafcca4e9d7a55a03914361f8f3.ro.png)

> Desen realizat de [Tomomi Imura](https://twitter.com/girlie_mac)

## [Chestionar înainte de curs](https://ff-quizzes.netlify.app/en/ai/quiz/1)

**Inteligența Artificială** este o disciplină științifică fascinantă care studiază cum putem face computerele să manifeste un comportament inteligent, de exemplu, să realizeze acele lucruri la care oamenii sunt buni.

Inițial, computerele au fost inventate de [Charles Babbage](https://en.wikipedia.org/wiki/Charles_Babbage) pentru a opera pe numere urmând o procedură bine definită - un algoritm. Computerele moderne, deși semnificativ mai avansate decât modelul original propus în secolul al XIX-lea, încă urmează aceeași idee de calcule controlate. Astfel, este posibil să programăm un computer să facă ceva dacă știm exact secvența de pași necesari pentru a atinge scopul.

![Fotografie a unei persoane](../../../../translated_images/dsh_age.d212a30d4e54fb5f68b94a624aad64bc086124bcbbec9561ae5bd5da661e22d8.ro.png)

> Fotografie de [Vickie Soshnikova](http://twitter.com/vickievalerie)

> ✅ Definirea vârstei unei persoane dintr-o fotografie este o sarcină care nu poate fi programată explicit, deoarece nu știm cum ajungem la un număr în mintea noastră atunci când o facem.

---

Există însă unele sarcini pe care nu știm explicit cum să le rezolvăm. Luați în considerare determinarea vârstei unei persoane dintr-o fotografie. Cumva învățăm să facem acest lucru, deoarece am văzut multe exemple de oameni de diferite vârste, dar nu putem explica explicit cum o facem, nici nu putem programa computerul să o facă. Acesta este exact tipul de sarcină care prezintă interes pentru **Inteligența Artificială** (prescurtat AI).

✅ Gândiți-vă la câteva sarcini pe care le-ați putea delega unui computer și care ar beneficia de AI. Luați în considerare domeniile finanțelor, medicinei și artelor - cum beneficiază aceste domenii astăzi de AI?

## AI Slab vs. AI Puternic

AI Slab | AI Puternic
---------------------------------------|-------------------------------------
AI Slab se referă la sisteme AI care sunt proiectate și antrenate pentru o sarcină specifică sau un set restrâns de sarcini. | AI Puternic, sau Inteligența Artificială Generală (AGI), se referă la sisteme AI cu nivel de inteligență și înțelegere similar cu cel uman.
Aceste sisteme AI nu sunt inteligent general; ele excelează în realizarea unei sarcini predefinite, dar le lipsește înțelegerea sau conștiința reală. | Aceste sisteme AI au capacitatea de a realiza orice sarcină intelectuală pe care o poate face un om, de a se adapta la diferite domenii și de a poseda o formă de conștiință sau auto-conștientizare.
Exemple de AI Slab includ asistenți virtuali precum Siri sau Alexa, algoritmi de recomandare utilizați de serviciile de streaming și chatbots proiectați pentru sarcini specifice de servicii pentru clienți. | Realizarea AI Puternic este un obiectiv pe termen lung al cercetării AI și ar necesita dezvoltarea de sisteme AI care pot raționa, învăța, înțelege și se adapta într-o gamă largă de sarcini și contexte.
AI Slab este extrem de specializat și nu posedă abilități cognitive similare cu cele umane sau capacități generale de rezolvare a problemelor dincolo de domeniul său restrâns. | AI Puternic este în prezent un concept teoretic, iar niciun sistem AI nu a atins acest nivel de inteligență generală.

Pentru mai multe informații, consultați **[Inteligența Artificială Generală](https://en.wikipedia.org/wiki/Artificial_general_intelligence)** (AGI).

## Definiția Inteligenței și Testul Turing

Una dintre problemele legate de termenul **[Inteligență](https://en.wikipedia.org/wiki/Intelligence)** este că nu există o definiție clară a acestui termen. Se poate argumenta că inteligența este legată de **gândirea abstractă** sau de **auto-conștientizare**, dar nu o putem defini corect.

![Fotografie a unei pisici](../../../../translated_images/photo-cat.8c8e8fb760ffe45725c5b9f6b0d954e9bf114475c01c55adf0303982851b7eae.ro.jpg)

> [Fotografie](https://unsplash.com/photos/75715CVEJhI) de [Amber Kipp](https://unsplash.com/@sadmax) de pe Unsplash

Pentru a vedea ambiguitatea termenului *inteligență*, încercați să răspundeți la întrebarea: "Este o pisică inteligentă?". Diferite persoane tind să dea răspunsuri diferite la această întrebare, deoarece nu există un test universal acceptat pentru a demonstra că afirmația este adevărată sau nu. Și dacă credeți că există - încercați să supuneți pisica voastră unui test IQ...

✅ Gândiți-vă un minut la cum definiți inteligența. Este o cioară care poate rezolva un labirint pentru a ajunge la mâncare inteligentă? Este un copil inteligent?

---

Când vorbim despre AGI, trebuie să avem o modalitate de a spune dacă am creat un sistem cu adevărat inteligent. [Alan Turing](https://en.wikipedia.org/wiki/Alan_Turing) a propus o metodă numită **[Testul Turing](https://en.wikipedia.org/wiki/Turing_test)**, care acționează și ca o definiție a inteligenței. Testul compară un sistem dat cu ceva inerent inteligent - un om real, și deoarece orice comparație automată poate fi ocolită de un program de computer, folosim un interogator uman. Astfel, dacă o persoană nu poate distinge între o persoană reală și un sistem de computer într-un dialog bazat pe text - sistemul este considerat inteligent.

> Un chatbot numit [Eugene Goostman](https://en.wikipedia.org/wiki/Eugene_Goostman), dezvoltat în St. Petersburg, a fost aproape de a trece testul Turing în 2014 folosind un truc de personalitate ingenios. A anunțat din start că este un băiat ucrainean de 13 ani, ceea ce ar explica lipsa de cunoștințe și unele discrepanțe în text. Botul a convins 30% dintre judecători că este uman după un dialog de 5 minute, o metrică pe care Turing credea că o mașină ar putea să o atingă până în 2000. Totuși, trebuie să înțelegem că acest lucru nu indică faptul că am creat un sistem inteligent sau că un sistem de computer a păcălit interogatorul uman - sistemul nu a păcălit oamenii, ci mai degrabă creatorii botului au făcut-o!

✅ Ați fost vreodată păcălit de un chatbot să credeți că vorbiți cu un om? Cum v-a convins?

## Diferite Abordări ale AI

Dacă dorim ca un computer să se comporte ca un om, trebuie cumva să modelăm în interiorul computerului modul nostru de gândire. În consecință, trebuie să încercăm să înțelegem ce face ca o ființă umană să fie inteligentă.

> Pentru a putea programa inteligența într-o mașină, trebuie să înțelegem cum funcționează propriile noastre procese de luare a deciziilor. Dacă faceți puțină introspecție, veți realiza că există unele procese care se întâmplă subconștient – de exemplu, putem distinge o pisică de un câine fără să ne gândim la asta - în timp ce altele implică raționament.

Există două abordări posibile pentru această problemă:

Abordare de sus în jos (Raționament simbolic) | Abordare de jos în sus (Rețele neuronale)
---------------------------------------|-------------------------------------
O abordare de sus în jos modelează modul în care o persoană raționează pentru a rezolva o problemă. Aceasta implică extragerea **cunoștințelor** de la o ființă umană și reprezentarea lor într-o formă citibilă de computer. De asemenea, trebuie să dezvoltăm o modalitate de a modela **raționamentul** în interiorul unui computer. | O abordare de jos în sus modelează structura creierului uman, formată dintr-un număr mare de unități simple numite **neuroni**. Fiecare neuron acționează ca o medie ponderată a intrărilor sale, iar noi putem antrena o rețea de neuroni să rezolve probleme utile oferindu-i **date de antrenament**.

Există și alte abordări posibile ale inteligenței:

* O abordare **Emergentă**, **Sinergică** sau **multi-agent** se bazează pe faptul că un comportament inteligent complex poate fi obținut prin interacțiunea unui număr mare de agenți simpli. Conform [ciberneticii evolutive](https://en.wikipedia.org/wiki/Global_brain#Evolutionary_cybernetics), inteligența poate *emerge* dintr-un comportament mai simplu, reactiv, în procesul de *tranziție metasistemică*.

* O abordare **Evolutivă**, sau **algoritm genetic**, este un proces de optimizare bazat pe principiile evoluției.

Vom analiza aceste abordări mai târziu în curs, dar acum ne vom concentra pe două direcții principale: de sus în jos și de jos în sus.

### Abordarea de Sus în Jos

Într-o **abordare de sus în jos**, încercăm să modelăm raționamentul nostru. Deoarece putem urmări gândurile noastre atunci când raționăm, putem încerca să formalizăm acest proces și să-l programăm în interiorul computerului. Acest lucru se numește **raționament simbolic**.

Oamenii tind să aibă niște reguli în mintea lor care ghidează procesele lor de luare a deciziilor. De exemplu, atunci când un medic diagnostichează un pacient, el sau ea poate realiza că o persoană are febră și, astfel, ar putea exista o inflamație în corp. Aplicând un set mare de reguli la o problemă specifică, un medic poate ajunge la diagnosticul final.

Această abordare se bazează foarte mult pe **reprezentarea cunoștințelor** și **raționament**. Extragerea cunoștințelor de la un expert uman poate fi cea mai dificilă parte, deoarece un medic, în multe cazuri, nu ar ști exact de ce ajunge la un anumit diagnostic. Uneori soluția pur și simplu apare în mintea lui sau a ei fără gândire explicită. Unele sarcini, cum ar fi determinarea vârstei unei persoane dintr-o fotografie, nu pot fi deloc reduse la manipularea cunoștințelor.

### Abordarea de Jos în Sus

Alternativ, putem încerca să modelăm cele mai simple elemente din creierul nostru – un neuron. Putem construi o așa-numită **rețea neuronală artificială** în interiorul unui computer și apoi să încercăm să o învățăm să rezolve probleme oferindu-i exemple. Acest proces este similar cu modul în care un copil nou-născut învață despre mediul său prin observații.

✅ Faceți puțină cercetare despre cum învață bebelușii. Care sunt elementele de bază ale creierului unui bebeluș?

> | Ce ziceți de ML?         |      |
> |--------------|-----------|
> | Parte a Inteligenței Artificiale care se bazează pe învățarea computerului să rezolve o problemă pe baza unor date se numește **Machine Learning**. Nu vom analiza învățarea automată clasică în acest curs - vă recomandăm un curriculum separat [Machine Learning pentru Începători](http://aka.ms/ml-beginners). |   ![ML pentru Începători](../../../../translated_images/ml-for-beginners.9e4fed176fd5817d7d1f7d358302515186579cbf09b2a6c5bd8092b345da7f22.ro.png)    |

## O Scurtă Istorie a AI

Inteligența Artificială a început ca un domeniu la mijlocul secolului XX. Inițial, raționamentul simbolic a fost o abordare predominantă și a dus la o serie de succese importante, cum ar fi sistemele expert – programe de computer care puteau acționa ca un expert într-un domeniu limitat de probleme. Totuși, s-a dovedit curând că această abordare nu se scalează bine. Extragerea cunoștințelor de la un expert, reprezentarea lor într-un computer și menținerea bazei de cunoștințe exacte se dovedește a fi o sarcină foarte complexă și prea costisitoare pentru a fi practică în multe cazuri. Acest lucru a dus la așa-numita [Iarnă AI](https://en.wikipedia.org/wiki/AI_winter) în anii 1970.

<img alt="Scurtă Istorie a AI" src="../../../../translated_images/history-of-ai.7e83efa70b537f5a0264357672b0884cf3a220fbafe35c65d70b2c3805f7bf5e.ro.png" width="70%"/>

> Imagine de [Dmitry Soshnikov](http://soshnikov.com)

Pe măsură ce timpul a trecut, resursele de calcul au devenit mai ieftine și mai multe date au devenit disponibile, astfel încât abordările bazate pe rețele neuronale au început să demonstreze performanțe excelente în competiția cu ființele umane în multe domenii, cum ar fi viziunea computerizată sau înțelegerea vorbirii. În ultimul deceniu, termenul Inteligență Artificială a fost folosit în mare parte ca sinonim pentru Rețele Neuronale, deoarece majoritatea succeselor AI despre care auzim se bazează pe acestea.

Putem observa cum s-au schimbat abordările, de exemplu, în crearea unui program de computer pentru jocul de șah:

* Programele de șah timpurii se bazau pe căutare – un program încerca explicit să estimeze mișcările posibile ale unui adversar pentru un număr dat de mișcări viitoare și selecta o mișcare optimă pe baza poziției optime care poate fi atinsă în câteva mișcări. Acest lucru a dus la dezvoltarea algoritmului de căutare [alpha-beta pruning](https://en.wikipedia.org/wiki/Alpha%E2%80%93beta_pruning).
* Strategiile de căutare funcționează bine spre sfârșitul jocului, unde spațiul de căutare este limitat de un număr mic de mișcări posibile. Totuși, la începutul jocului, spațiul de căutare este imens, iar algoritmul poate fi îmbunătățit prin învățarea din meciurile existente între jucători umani. Experimentele ulterioare au utilizat așa-numitul [raționament bazat pe cazuri](https://en.wikipedia.org/wiki/Case-based_reasoning), unde programul căuta cazuri în baza de cunoștințe foarte similare cu poziția actuală din joc.
* Programele moderne care câștigă împotriva jucătorilor umani se bazează pe rețele neuronale și [învățare prin întărire](https://en.wikipedia.org/wiki/Reinforcement_learning), unde programele învață să joace doar jucând mult timp împotriva lor însele și învățând din propriile greșeli – la fel cum fac oamenii când învață să joace șah. Totuși, un program de computer poate juca mult mai multe jocuri într-un timp mult mai scurt și, astfel, poate învăța mult mai repede.

✅ Faceți puțină cercetare despre alte jocuri care au fost jucate de AI.

În mod similar, putem vedea cum s-a schimbat abordarea în crearea „programelor de vorbire” (care ar putea trece testul Turing):

* Programele timpurii de acest tip, cum ar fi [Eliza](https://en.wikipedia.org/wiki/ELIZA), se bazau pe reguli gramaticale foarte simple și reformularea propoziției de intrare într-o întrebare.
* Asistenții moderni, cum ar fi Cortana, Siri sau Google Assistant, sunt toate sisteme hibride care folosesc rețele neuronale pentru a converti vorbirea în text și a recunoaște intenția noastră, apoi utilizează un raționament sau algoritmi expliciți pentru a realiza acțiunile necesare.
* În viitor, ne putem aștepta la un model complet bazat pe rețele neuronale care să gestioneze dialogul de unul singur. Familia recentă de rețele neuronale GPT și [Turing-NLG](https://www.microsoft.com/research/blog/turing-nlg-a-17-billion-parameter-language-model-by-microsoft) demonstrează un mare succes în acest sens.

<img alt="evoluția testului Turing" src="../../../../translated_images/turing-test-evol.4184696701293ead6de6e6441a659c62f0b119b342456987f531005f43be0b6d.ro.png" width="70%"/>
> Imagine de Dmitry Soshnikov, [fotografie](https://unsplash.com/photos/r8LmVbUKgns) de [Marina Abrosimova](https://unsplash.com/@abrosimova_marina_foto), Unsplash

## Cercetări recente în domeniul AI

Creșterea masivă a cercetării în rețele neuronale a început în jurul anului 2010, când au devenit disponibile seturi mari de date publice. O colecție uriașă de imagini numită [ImageNet](https://en.wikipedia.org/wiki/ImageNet), care conține aproximativ 14 milioane de imagini adnotate, a dat naștere [Provocării de Recunoaștere Vizuală la Scară Largă ImageNet](https://image-net.org/challenges/LSVRC/).

![Acuratețea ILSVRC](../../../../lessons/1-Intro/images/ilsvrc.gif)

> Imagine de [Dmitry Soshnikov](http://soshnikov.com)

În 2012, [Rețelele Neuronale Convoluționale](../4-ComputerVision/07-ConvNets/README.md) au fost utilizate pentru prima dată în clasificarea imaginilor, ceea ce a dus la o scădere semnificativă a erorilor de clasificare (de la aproape 30% la 16,4%). În 2015, arhitectura ResNet de la Microsoft Research [a atins acuratețea la nivel uman](https://doi.org/10.1109/ICCV.2015.123).

De atunci, rețelele neuronale au demonstrat un comportament foarte eficient în multe sarcini:

---

An | Paritate cu nivelul uman atinsă
-----|--------
2015 | [Clasificarea imaginilor](https://doi.org/10.1109/ICCV.2015.123)
2016 | [Recunoașterea vorbirii conversaționale](https://arxiv.org/abs/1610.05256)
2018 | [Traducerea automată a textelor](https://arxiv.org/abs/1803.05567) (chineză-engleză)
2020 | [Generarea descrierilor pentru imagini](https://arxiv.org/abs/2009.13682)

În ultimii ani, am fost martori la succese uriașe cu modelele de limbaj de mari dimensiuni, cum ar fi BERT și GPT-3. Acest lucru s-a întâmplat în principal datorită faptului că există o cantitate mare de date text generale disponibile, care permit antrenarea modelelor pentru a captura structura și sensul textelor, pre-antrenarea lor pe colecții generale de texte și apoi specializarea acestor modele pentru sarcini mai specifice. Vom învăța mai multe despre [Procesarea Limbajului Natural](../5-NLP/README.md) mai târziu în acest curs.

## 🚀 Provocare

Fă un tur al internetului pentru a determina unde, în opinia ta, AI este utilizată cel mai eficient. Este într-o aplicație de hărți, un serviciu de conversie vorbire-text sau un joc video? Cercetează cum a fost construit sistemul.

## [Quiz după lecție](https://ff-quizzes.netlify.app/en/ai/quiz/2)

## Recapitulare & Studiu individual

Recapitulează istoria AI și ML citind [această lecție](https://github.com/microsoft/ML-For-Beginners/tree/main/1-Introduction/2-history-of-ML). Alege un element din schița de la începutul acelei lecții sau din aceasta și cercetează-l mai în profunzime pentru a înțelege contextul cultural care a influențat evoluția sa.

**Temă**: [Game Jam](assignment.md)

---

**Declinare de responsabilitate**:  
Acest document a fost tradus folosind serviciul de traducere AI [Co-op Translator](https://github.com/Azure/co-op-translator). Deși ne străduim să asigurăm acuratețea, vă rugăm să fiți conștienți că traducerile automate pot conține erori sau inexactități. Documentul original în limba sa maternă ar trebui considerat sursa autoritară. Pentru informații critice, se recomandă traducerea profesională realizată de un specialist uman. Nu ne asumăm responsabilitatea pentru eventualele neînțelegeri sau interpretări greșite care pot apărea din utilizarea acestei traduceri.