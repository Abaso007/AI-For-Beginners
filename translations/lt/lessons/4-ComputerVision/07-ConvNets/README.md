<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a560d5b845962cf33dc102266e409568",
  "translation_date": "2025-09-23T15:41:50+00:00",
  "source_file": "lessons/4-ComputerVision/07-ConvNets/README.md",
  "language_code": "lt"
}
-->
# Konvoliuciniai neuroniniai tinklai

Anksčiau matėme, kad neuroniniai tinklai gana gerai dirba su vaizdais, ir net vieno sluoksnio perceptronas sugeba atpažinti ranka rašytus skaitmenis iš MNIST duomenų rinkinio su pakankamu tikslumu. Tačiau MNIST duomenų rinkinys yra labai specifinis – visi skaitmenys yra centruoti vaizde, todėl užduotis tampa paprastesnė.

## [Klausimai prieš paskaitą](https://ff-quizzes.netlify.app/en/ai/quiz/13)

Realiame gyvenime norime atpažinti objektus nuotraukoje, nepaisant jų tikslios vietos vaizde. Kompiuterinis matymas skiriasi nuo bendro klasifikavimo, nes bandydami rasti tam tikrą objektą nuotraukoje, skenuojame vaizdą ieškodami specifinių **raštų** ir jų kombinacijų. Pavyzdžiui, ieškodami katės, pirmiausia galime ieškoti horizontalių linijų, kurios gali sudaryti ūsus, o tam tikra ūsų kombinacija gali pasakyti, kad tai iš tiesų yra katės nuotrauka. Svarbi yra santykinė tam tikrų raštų padėtis ir buvimas, o ne jų tiksli vieta vaizde.

Norėdami išgauti raštus, naudosime **konvoliucinių filtrų** sąvoką. Kaip žinote, vaizdas yra pateikiamas kaip 2D-matrica arba 3D-tensoras su spalvų gylio dimensija. Filtrą taikyti reiškia, kad imame palyginti mažą **filtrų branduolio** matricą ir kiekvienam pikseliui originaliame vaizde apskaičiuojame svertinį vidurkį su kaimyniniais taškais. Galime tai įsivaizduoti kaip mažą langą, kuris slysta per visą vaizdą ir vidutiniškai apskaičiuoja pikselius pagal filtrų branduolio matricos svorius.

![Vertikalus kraštų filtras](../../../../../translated_images/filter-vert.b7148390ca0bc356ddc7e55555d2481819c1e86ddde9dce4db5e71a69d6f887f.lt.png) | ![Horizontalus kraštų filtras](../../../../../translated_images/filter-horiz.59b80ed4feb946efbe201a7fe3ca95abb3364e266e6fd90820cb893b4d3a6dda.lt.png)
----|----

> Vaizdas: Dmitry Soshnikov

Pavyzdžiui, jei taikome 3x3 vertikalų ir horizontalų kraštų filtrus MNIST skaitmenims, galime išryškinti (pvz., gauti aukštas reikšmes) vietas, kuriose yra vertikalūs ir horizontalūs kraštai originaliame vaizde. Taigi šiuos du filtrus galima naudoti "ieškant" kraštų. Panašiai galime sukurti skirtingus filtrus, kad ieškotume kitų žemo lygio raštų:

<img src="images/lmfilters.jpg" width="500" align="center"/>

> Vaizdas: [Leung-Malik filtrų rinkinys](https://www.robots.ox.ac.uk/~vgg/research/texclass/filters.html)

Tačiau, nors galime rankiniu būdu sukurti filtrus tam tikrų raštų išgavimui, galime sukurti tinklą taip, kad jis automatiškai išmoktų raštus. Tai yra viena pagrindinių CNN idėjų.

## Pagrindinės CNN idėjos

CNN veikimas grindžiamas šiomis svarbiomis idėjomis:

* Konvoliuciniai filtrai gali išgauti raštus
* Galime sukurti tinklą taip, kad filtrai būtų mokomi automatiškai
* Galime naudoti tą patį metodą aukšto lygio savybių raštų paieškai, ne tik originaliame vaizde. Taigi CNN savybių išgavimas veikia hierarchijos principu – pradedant nuo žemo lygio pikselių kombinacijų iki aukšto lygio vaizdo dalių kombinacijų.

![Hierarchinis savybių išgavimas](../../../../../translated_images/FeatureExtractionCNN.d9b456cbdae7cb643fde3032b81b2940e3cf8be842e29afac3f482725ba7f95c.lt.png)

> Vaizdas iš [Hislop-Lynch straipsnio](https://www.semanticscholar.org/paper/Computer-vision-based-pedestrian-trajectory-Hislop-Lynch/26e6f74853fc9bbb7487b06dc2cf095d36c9021d), remiantis [jų tyrimu](https://dl.acm.org/doi/abs/10.1145/1553374.1553453)

## ✍️ Pratimai: Konvoliuciniai neuroniniai tinklai

Tęskime tyrinėjimą, kaip veikia konvoliuciniai neuroniniai tinklai ir kaip galime pasiekti mokomus filtrus, dirbdami su atitinkamais užrašais:

* [Konvoliuciniai neuroniniai tinklai - PyTorch](ConvNetsPyTorch.ipynb)
* [Konvoliuciniai neuroniniai tinklai - TensorFlow](ConvNetsTF.ipynb)

## Piramidės architektūra

Dauguma CNN, naudojamų vaizdų apdorojimui, seka vadinamąją piramidės architektūrą. Pirmasis konvoliucinis sluoksnis, taikomas originaliems vaizdams, paprastai turi palyginti mažą filtrų skaičių (8-16), kurie atitinka skirtingas pikselių kombinacijas, tokias kaip horizontalios/vertikalios linijos ar brūkšniai. Kitame lygyje sumažiname tinklo erdvinę dimensiją ir padidiname filtrų skaičių, kuris atitinka daugiau galimų paprastų savybių kombinacijų. Kiekviename sluoksnyje, judant link galutinio klasifikatoriaus, vaizdo erdvinės dimensijos mažėja, o filtrų skaičius auga.

Pavyzdžiui, pažvelkime į VGG-16 architektūrą – tinklą, kuris 2014 m. pasiekė 92,7% tikslumą ImageNet top-5 klasifikacijoje:

![ImageNet sluoksniai](../../../../../translated_images/vgg-16-arch1.d901a5583b3a51baeaab3e768567d921e5d54befa46e1e642616c5458c934028.lt.jpg)

![ImageNet piramidė](../../../../../translated_images/vgg-16-arch.64ff2137f50dd49fdaa786e3f3a975b3f22615efd13efb19c5d22f12e01451a1.lt.jpg)

> Vaizdas iš [Researchgate](https://www.researchgate.net/figure/Vgg16-model-structure-To-get-the-VGG-NIN-model-we-replace-the-2-nd-4-th-6-th-7-th_fig2_335194493)

## Geriausiai žinomos CNN architektūros

[Tęskite mokymąsi apie geriausiai žinomas CNN architektūras](CNN_Architectures.md)

---

