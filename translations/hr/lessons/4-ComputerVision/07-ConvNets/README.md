<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "088837b42b7d99198bf62db8a42411e0",
  "translation_date": "2025-08-25T22:53:21+00:00",
  "source_file": "lessons/4-ComputerVision/07-ConvNets/README.md",
  "language_code": "hr"
}
-->
# Konvolucijske neuronske mreže

Već smo vidjeli da su neuronske mreže prilično dobre u obradi slika, pa čak i perceptron s jednim slojem može prepoznati rukom pisane znamenke iz MNIST skupa podataka s razumnom točnošću. Međutim, MNIST skup podataka je vrlo specifičan, jer su sve znamenke centrirane unutar slike, što zadatak čini jednostavnijim.

## [Kviz prije predavanja](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/107)

U stvarnom životu želimo biti sposobni prepoznati objekte na slici bez obzira na njihovu točnu lokaciju unutar slike. Računalni vid razlikuje se od generičke klasifikacije, jer kada pokušavamo pronaći određeni objekt na slici, skeniramo sliku tražeći specifične **uzorke** i njihove kombinacije. Na primjer, kada tražimo mačku, prvo možemo tražiti horizontalne linije koje mogu oblikovati brkove, a zatim određena kombinacija brkova može ukazati na to da je riječ o slici mačke. Relativni položaj i prisutnost određenih uzoraka su važni, a ne njihova točna pozicija na slici.

Za izdvajanje uzoraka koristit ćemo pojam **konvolucijskih filtera**. Kao što znate, slika je predstavljena 2D-matricom ili 3D-tenzorom s dubinom boje. Primjena filtera znači da uzimamo relativno malu matricu **jezgre filtera**, i za svaki piksel u originalnoj slici izračunavamo ponderirani prosjek s okolnim točkama. To možemo zamisliti kao mali prozor koji klizi preko cijele slike i izračunava prosjek svih piksela prema težinama u matrici jezgre filtera.

![Filter za vertikalne rubove](../../../../../translated_images/filter-vert.b7148390ca0bc356ddc7e55555d2481819c1e86ddde9dce4db5e71a69d6f887f.hr.png) | ![Filter za horizontalne rubove](../../../../../translated_images/filter-horiz.59b80ed4feb946efbe201a7fe3ca95abb3364e266e6fd90820cb893b4d3a6dda.hr.png)
----|----

> Slika: Dmitry Soshnikov

Na primjer, ako primijenimo 3x3 filter za vertikalne rubove i filter za horizontalne rubove na znamenke iz MNIST skupa podataka, možemo dobiti istaknute dijelove (npr. visoke vrijednosti) gdje postoje vertikalni i horizontalni rubovi u našoj originalnoj slici. Tako se ta dva filtera mogu koristiti za "traženje" rubova. Slično tome, možemo dizajnirati različite filtere za traženje drugih osnovnih uzoraka:

> Slika [Leung-Malik Filter Bank](https://www.robots.ox.ac.uk/~vgg/research/texclass/filters.html)

Međutim, dok možemo ručno dizajnirati filtere za izdvajanje nekih uzoraka, možemo također dizajnirati mrežu na način da ona automatski uči uzorke. To je jedna od glavnih ideja iza CNN-a.

## Glavne ideje iza CNN-a

Način na koji CNN funkcionira temelji se na sljedećim važnim idejama:

* Konvolucijski filteri mogu izdvajati uzorke
* Možemo dizajnirati mrežu na način da se filteri automatski treniraju
* Isti pristup možemo koristiti za pronalaženje uzoraka u visokim razinama značajki, ne samo u originalnoj slici. Tako ekstrakcija značajki u CNN-u radi na hijerarhiji značajki, počevši od kombinacija piksela niske razine, pa sve do kombinacija dijelova slike na višim razinama.

![Hijerarhijska ekstrakcija značajki](../../../../../translated_images/FeatureExtractionCNN.d9b456cbdae7cb643fde3032b81b2940e3cf8be842e29afac3f482725ba7f95c.hr.png)

> Slika iz [rada Hislop-Lynch](https://www.semanticscholar.org/paper/Computer-vision-based-pedestrian-trajectory-Hislop-Lynch/26e6f74853fc9bbb7487b06dc2cf095d36c9021d), temeljenog na [njihovom istraživanju](https://dl.acm.org/doi/abs/10.1145/1553374.1553453)

## ✍️ Vježbe: Konvolucijske neuronske mreže

Nastavimo istraživati kako konvolucijske neuronske mreže funkcioniraju i kako možemo postići trenirajuće filtere, radeći kroz odgovarajuće bilježnice:

* [Konvolucijske neuronske mreže - PyTorch](../../../../../lessons/4-ComputerVision/07-ConvNets/ConvNetsPyTorch.ipynb)
* [Konvolucijske neuronske mreže - TensorFlow](../../../../../lessons/4-ComputerVision/07-ConvNets/ConvNetsTF.ipynb)

## Piramidalna arhitektura

Većina CNN-a koji se koriste za obradu slika slijedi tzv. piramidalnu arhitekturu. Prvi konvolucijski sloj primijenjen na originalne slike obično ima relativno mali broj filtera (8-16), koji odgovaraju različitim kombinacijama piksela, poput horizontalnih/vertikalnih linija ili poteza. Na sljedećoj razini smanjujemo prostornu dimenziju mreže i povećavamo broj filtera, što odgovara većem broju mogućih kombinacija jednostavnih značajki. Sa svakim slojem, kako se približavamo završnom klasifikatoru, prostorne dimenzije slike se smanjuju, a broj filtera raste.

Kao primjer, pogledajmo arhitekturu VGG-16, mreže koja je postigla 92.7% točnosti u top-5 klasifikaciji ImageNet-a 2014. godine:

![Slojevi ImageNet-a](../../../../../translated_images/vgg-16-arch1.d901a5583b3a51baeaab3e768567d921e5d54befa46e1e642616c5458c934028.hr.jpg)

![Piramida ImageNet-a](../../../../../translated_images/vgg-16-arch.64ff2137f50dd49fdaa786e3f3a975b3f22615efd13efb19c5d22f12e01451a1.hr.jpg)

> Slika s [Researchgate](https://www.researchgate.net/figure/Vgg16-model-structure-To-get-the-VGG-NIN-model-we-replace-the-2-nd-4-th-6-th-7-th_fig2_335194493)

## Najpoznatije CNN arhitekture

[Nastavite svoje učenje o najpoznatijim CNN arhitekturama](CNN_Architectures.md)

**Odricanje od odgovornosti**:  
Ovaj dokument je preveden pomoću AI usluge za prevođenje [Co-op Translator](https://github.com/Azure/co-op-translator). Iako nastojimo osigurati točnost, imajte na umu da automatski prijevodi mogu sadržavati pogreške ili netočnosti. Izvorni dokument na izvornom jeziku treba smatrati autoritativnim izvorom. Za ključne informacije preporučuje se profesionalni prijevod od strane čovjeka. Ne preuzimamo odgovornost za nesporazume ili pogrešna tumačenja koja mogu proizaći iz korištenja ovog prijevoda.