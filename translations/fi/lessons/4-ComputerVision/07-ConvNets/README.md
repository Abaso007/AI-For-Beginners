<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a560d5b845962cf33dc102266e409568",
  "translation_date": "2025-09-23T09:56:03+00:00",
  "source_file": "lessons/4-ComputerVision/07-ConvNets/README.md",
  "language_code": "fi"
}
-->
# Konvoluutionaaliset neuroverkot

Olemme aiemmin nähneet, että neuroverkot ovat varsin hyviä käsittelemään kuvia, ja jopa yksikerroksinen perceptron pystyy tunnistamaan käsinkirjoitettuja numeroita MNIST-datasta kohtuullisella tarkkuudella. MNIST-datasetti on kuitenkin hyvin erityinen, sillä kaikki numerot on keskitetty kuvan sisälle, mikä tekee tehtävästä yksinkertaisemman.

## [Esiluentovisa](https://ff-quizzes.netlify.app/en/ai/quiz/13)

Todellisessa elämässä haluamme pystyä tunnistamaan esineitä kuvasta niiden tarkasta sijainnista riippumatta. Tietokonenäkö eroaa yleisestä luokittelusta, koska kun yritämme löytää tiettyä esinettä kuvasta, skannaamme kuvaa etsien tiettyjä **kuvioita** ja niiden yhdistelmiä. Esimerkiksi, kun etsimme kissaa, voimme ensin etsiä vaakasuoria viivoja, jotka voivat muodostaa viikset, ja sitten tietty viiksien yhdistelmä voi kertoa meille, että kyseessä on kuva kissasta. Tiettyjen kuvioiden suhteellinen sijainti ja läsnäolo ovat tärkeitä, mutta niiden tarkka sijainti kuvassa ei ole.

Kuvioiden tunnistamiseen käytämme **konvoluutiokertoimia**. Kuten tiedät, kuva esitetään 2D-matriisina tai 3D-tensorina värisyvyyden kanssa. Suodattimen soveltaminen tarkoittaa, että otamme suhteellisen pienen **suodatinytimen** matriisin, ja alkuperäisen kuvan jokaiselle pikselille laskemme painotetun keskiarvon naapuripisteiden kanssa. Voimme ajatella tämän olevan kuin pieni ikkuna, joka liukuu koko kuvan yli ja tasoittaa kaikki pikselit suodatinytimen matriisin painojen mukaan.

![Pystysuuntainen reunasuodatin](../../../../../translated_images/filter-vert.b7148390ca0bc356ddc7e55555d2481819c1e86ddde9dce4db5e71a69d6f887f.fi.png) | ![Vaakasuuntainen reunasuodatin](../../../../../translated_images/filter-horiz.59b80ed4feb946efbe201a7fe3ca95abb3364e266e6fd90820cb893b4d3a6dda.fi.png)
----|----

> Kuva: Dmitry Soshnikov

Esimerkiksi, jos sovellamme 3x3 pystysuuntaista ja vaakasuuntaista reunasuodatinta MNIST-numeroihin, voimme saada korostuksia (esim. korkeita arvoja) kohtiin, joissa alkuperäisessä kuvassa on pystysuuntaisia ja vaakasuuntaisia reunoja. Näin ollen näitä kahta suodatinta voidaan käyttää "etsimään" reunoja. Samalla tavalla voimme suunnitella erilaisia suodattimia etsimään muita matalan tason kuvioita:

<img src="images/lmfilters.jpg" width="500" align="center"/>

> Kuva [Leung-Malik-suodatinpankista](https://www.robots.ox.ac.uk/~vgg/research/texclass/filters.html)

Vaikka voimme suunnitella suodattimia manuaalisesti tiettyjen kuvioiden tunnistamiseen, voimme myös suunnitella verkon siten, että se oppii kuviot automaattisesti. Tämä on yksi CNN:n keskeisistä ideoista.

## CNN:n pääideat

CNN:ien toiminta perustuu seuraaviin tärkeisiin ideoihin:

* Konvoluutiokertoimet voivat tunnistaa kuvioita
* Voimme suunnitella verkon siten, että suodattimet koulutetaan automaattisesti
* Voimme käyttää samaa lähestymistapaa löytääksemme kuvioita korkeamman tason ominaisuuksista, ei vain alkuperäisestä kuvasta. Näin CNN:n ominaisuuksien tunnistus toimii hierarkiana, alkaen matalan tason pikseliyhdistelmistä ja päätyen korkeamman tason kuvan osien yhdistelmiin.

![Hierarkkinen ominaisuuksien tunnistus](../../../../../translated_images/FeatureExtractionCNN.d9b456cbdae7cb643fde3032b81b2940e3cf8be842e29afac3f482725ba7f95c.fi.png)

> Kuva [Hislop-Lynchin artikkelista](https://www.semanticscholar.org/paper/Computer-vision-based-pedestrian-trajectory-Hislop-Lynch/26e6f74853fc9bbb7487b06dc2cf095d36c9021d), perustuen [heidän tutkimukseensa](https://dl.acm.org/doi/abs/10.1145/1553374.1553453)

## ✍️ Harjoitukset: Konvoluutionaaliset neuroverkot

Jatketaan tutkimista, miten konvoluutionaaliset neuroverkot toimivat ja miten voimme saavuttaa koulutettavat suodattimet, työstämällä vastaavia muistikirjoja:

* [Konvoluutionaaliset neuroverkot - PyTorch](ConvNetsPyTorch.ipynb)
* [Konvoluutionaaliset neuroverkot - TensorFlow](ConvNetsTF.ipynb)

## Pyramidirakenne

Useimmat kuvankäsittelyyn käytetyt CNN:t noudattavat niin sanottua pyramidirakennetta. Ensimmäinen alkuperäisiin kuviin sovellettu konvoluutiokerros sisältää tyypillisesti suhteellisen pienen määrän suodattimia (8-16), jotka vastaavat erilaisia pikseliyhdistelmiä, kuten vaakasuoria/pystysuoria viivoja tai vetoja. Seuraavalla tasolla pienennämme verkon spatiaalista ulottuvuutta ja lisäämme suodattimien määrää, mikä vastaa yksinkertaisten ominaisuuksien monimutkaisempia yhdistelmiä. Jokaisella kerroksella, kun siirrymme kohti lopullista luokittelijaa, kuvan spatiaalinen ulottuvuus pienenee ja suodattimien määrä kasvaa.

Esimerkiksi tarkastellaan VGG-16-arkkitehtuuria, verkkoa, joka saavutti 92,7 % tarkkuuden ImageNetin top-5-luokittelussa vuonna 2014:

![ImageNet-kerrokset](../../../../../translated_images/vgg-16-arch1.d901a5583b3a51baeaab3e768567d921e5d54befa46e1e642616c5458c934028.fi.jpg)

![ImageNet-pyramidi](../../../../../translated_images/vgg-16-arch.64ff2137f50dd49fdaa786e3f3a975b3f22615efd13efb19c5d22f12e01451a1.fi.jpg)

> Kuva [Researchgate-sivustolta](https://www.researchgate.net/figure/Vgg16-model-structure-To-get-the-VGG-NIN-model-we-replace-the-2-nd-4-th-6-th-7-th_fig2_335194493)

## Tunnetuimmat CNN-arkkitehtuurit

[Jatka opiskelua tunnetuimmista CNN-arkkitehtuureista](CNN_Architectures.md)

---

