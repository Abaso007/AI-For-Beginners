<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "2f7b97b375358cb51a1e098df306bf73",
  "translation_date": "2025-08-25T22:56:51+00:00",
  "source_file": "lessons/4-ComputerVision/07-ConvNets/CNN_Architectures.md",
  "language_code": "sl"
}
-->
# Dobro poznane arhitekture CNN

### VGG-16

VGG-16 je mreža, ki je leta 2014 dosegla 92,7 % natančnost pri razvrščanju top-5 na ImageNet. Ima naslednjo strukturo slojev:

![ImageNet Layers](../../../../../translated_images/vgg-16-arch1.d901a5583b3a51baeaab3e768567d921e5d54befa46e1e642616c5458c934028.sl.jpg)

Kot lahko vidite, VGG sledi tradicionalni piramidni arhitekturi, ki je zaporedje slojev konvolucije in združevanja (pooling).

![ImageNet Pyramid](../../../../../translated_images/vgg-16-arch.64ff2137f50dd49fdaa786e3f3a975b3f22615efd13efb19c5d22f12e01451a1.sl.jpg)

> Slika iz [Researchgate](https://www.researchgate.net/figure/Vgg16-model-structure-To-get-the-VGG-NIN-model-we-replace-the-2-nd-4-th-6-th-7-th_fig2_335194493)

### ResNet

ResNet je družina modelov, ki jih je leta 2015 predlagal Microsoft Research. Glavna ideja ResNet-a je uporaba **rezidualnih blokov**:

<img src="images/resnet-block.png" width="300"/>

> Slika iz [tega članka](https://arxiv.org/pdf/1512.03385.pdf)

Razlog za uporabo identitetnega prehoda je, da sloj napove **razliko** med rezultatom prejšnjega sloja in izhodom rezidualnega bloka - od tod ime *rezidual*. Ti bloki so veliko lažji za treniranje, kar omogoča gradnjo mrež s stotinami teh blokov (najpogostejše različice so ResNet-52, ResNet-101 in ResNet-152).

To mrežo si lahko predstavljate tudi kot sposobno prilagajanja svoje kompleksnosti podatkovnemu naboru. Na začetku, ko začnete trenirati mrežo, so vrednosti uteži majhne, večina signala pa gre skozi identitetne sloje. Ko se trening nadaljuje in uteži postanejo večje, se poveča pomen parametrov mreže, mreža pa se prilagodi, da doseže potrebno izrazno moč za pravilno razvrščanje slik iz treninga.

### Google Inception

Arhitektura Google Inception to idejo nadgradi in zgradi vsak sloj mreže kot kombinacijo več različnih poti:

<img src="images/inception.png" width="400"/>

> Slika iz [Researchgate](https://www.researchgate.net/figure/Inception-module-with-dimension-reductions-left-and-schema-for-Inception-ResNet-v1_fig2_355547454)

Tukaj je treba poudariti vlogo konvolucij 1x1, saj na prvi pogled nimajo smisla. Zakaj bi potrebovali filter velikosti 1x1 za obdelavo slike? Vendar pa morate upoštevati, da konvolucijski filtri delujejo tudi z več globinskimi kanali (sprva - RGB barve, v nadaljnjih slojih - kanali za različne filtre), konvolucija 1x1 pa se uporablja za mešanje teh vhodnih kanalov z različnimi učljivimi utežmi. To lahko razumemo tudi kot vzorčenje navzdol (pooling) po dimenziji kanalov.

Tukaj je [dober blog prispevek](https://medium.com/analytics-vidhya/talented-mr-1x1-comprehensive-look-at-1x1-convolution-in-deep-learning-f6b355825578) na to temo in [izvirni članek](https://arxiv.org/pdf/1312.4400.pdf).

### MobileNet

MobileNet je družina modelov z zmanjšano velikostjo, primernih za mobilne naprave. Uporabite jih, če imate omejene vire in lahko žrtvujete nekaj natančnosti. Glavna ideja teh modelov je tako imenovana **globinska ločljiva konvolucija**, ki omogoča predstavitev konvolucijskih filtrov kot sestavo prostorskih konvolucij in konvolucije 1x1 po globinskih kanalih. To bistveno zmanjša število parametrov, kar naredi mrežo manjšo in tudi lažjo za treniranje z manj podatki.

Tukaj je [dober blog prispevek o MobileNet](https://medium.com/analytics-vidhya/image-classification-with-mobilenet-cc6fbb2cd470).

## Zaključek

V tej enoti ste spoznali glavni koncept nevronskih mrež za računalniški vid - konvolucijske mreže. Arhitekture iz resničnega sveta, ki poganjajo razvrščanje slik, zaznavanje objektov in celo generiranje slik, so vse osnovane na CNN-jih, le z več sloji in nekaterimi dodatnimi triki pri treniranju.

## 🚀 Izziv

V priloženih zvezkih so na dnu zapiski o tem, kako doseči večjo natančnost. Naredite nekaj eksperimentov, da preverite, ali lahko dosežete višjo natančnost.

## [Kvizi po predavanju](https://ff-quizzes.netlify.app/en/ai/quiz/14)

## Pregled in samostojno učenje

Čeprav se CNN-ji najpogosteje uporabljajo za naloge računalniškega vida, so na splošno dobri za ekstrakcijo vzorcev fiksne velikosti. Na primer, če obdelujemo zvoke, lahko uporabimo CNN-je za iskanje specifičnih vzorcev v avdio signalu - v tem primeru bi bili filtri enodimenzionalni (in ta CNN bi se imenoval 1D-CNN). Prav tako se včasih uporablja 3D-CNN za ekstrakcijo značilnosti v večdimenzionalnem prostoru, kot so določeni dogodki, ki se pojavljajo na videoposnetku - CNN lahko zajame določene vzorce spreminjanja značilnosti skozi čas. Naredite pregled in samostojno učenje o drugih nalogah, ki jih je mogoče opraviti s CNN-ji.

## [Naloga](lab/README.md)

V tej laboratorijski nalogi boste razvrščali različne pasme mačk in psov. Te slike so bolj kompleksne kot podatkovni nabor MNIST, imajo višje dimenzije in več kot 10 razredov.

**Omejitev odgovornosti**:  
Ta dokument je bil preveden z uporabo storitve AI za prevajanje [Co-op Translator](https://github.com/Azure/co-op-translator). Čeprav si prizadevamo za natančnost, vas prosimo, da upoštevate, da lahko avtomatizirani prevodi vsebujejo napake ali netočnosti. Izvirni dokument v njegovem maternem jeziku je treba obravnavati kot avtoritativni vir. Za ključne informacije priporočamo profesionalni človeški prevod. Ne odgovarjamo za morebitna nesporazumevanja ali napačne razlage, ki bi nastale zaradi uporabe tega prevoda.