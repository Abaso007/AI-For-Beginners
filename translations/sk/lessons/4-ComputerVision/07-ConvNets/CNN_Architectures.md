<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "2f7b97b375358cb51a1e098df306bf73",
  "translation_date": "2025-08-25T22:55:16+00:00",
  "source_file": "lessons/4-ComputerVision/07-ConvNets/CNN_Architectures.md",
  "language_code": "sk"
}
-->
# Známe architektúry CNN

### VGG-16

VGG-16 je sieť, ktorá dosiahla presnosť 92,7 % v klasifikácii ImageNet top-5 v roku 2014. Má nasledujúcu štruktúru vrstiev:

![ImageNet Layers](../../../../../translated_images/vgg-16-arch1.d901a5583b3a51baeaab3e768567d921e5d54befa46e1e642616c5458c934028.sk.jpg)

Ako môžete vidieť, VGG nasleduje tradičnú pyramídovú architektúru, ktorá je sekvenciou vrstiev konvolúcie a pooling.

![ImageNet Pyramid](../../../../../translated_images/vgg-16-arch.64ff2137f50dd49fdaa786e3f3a975b3f22615efd13efb19c5d22f12e01451a1.sk.jpg)

> Obrázok z [Researchgate](https://www.researchgate.net/figure/Vgg16-model-structure-To-get-the-VGG-NIN-model-we-replace-the-2-nd-4-th-6-th-7-th_fig2_335194493)

### ResNet

ResNet je rodina modelov navrhnutá spoločnosťou Microsoft Research v roku 2015. Hlavnou myšlienkou ResNet je použitie **reziduálnych blokov**:

<img src="images/resnet-block.png" width="300"/>

> Obrázok z [tohto článku](https://arxiv.org/pdf/1512.03385.pdf)

Dôvodom použitia identity pass-through je, aby naša vrstva predpovedala **rozdiel** medzi výsledkom predchádzajúcej vrstvy a výstupom reziduálneho bloku - odtiaľ názov *reziduálny*. Tieto bloky sa trénujú oveľa ľahšie a je možné vytvoriť siete s niekoľkými stovkami týchto blokov (najbežnejšie varianty sú ResNet-52, ResNet-101 a ResNet-152).

Túto sieť si môžete predstaviť aj ako schopnú prispôsobiť svoju komplexnosť dátam. Na začiatku, keď začínate trénovať sieť, hodnoty váh sú malé a väčšina signálu prechádza cez identity vrstvy. Ako tréning pokračuje a váhy sa zväčšujú, význam parametrov siete rastie a sieť sa prispôsobuje, aby poskytla potrebnú expresívnu silu na správnu klasifikáciu tréningových obrázkov.

### Google Inception

Architektúra Google Inception posúva túto myšlienku o krok ďalej a buduje každú vrstvu siete ako kombináciu niekoľkých rôznych ciest:

<img src="images/inception.png" width="400"/>

> Obrázok z [Researchgate](https://www.researchgate.net/figure/Inception-module-with-dimension-reductions-left-and-schema-for-Inception-ResNet-v1_fig2_355547454)

Tu je potrebné zdôrazniť úlohu konvolúcií 1x1, pretože na prvý pohľad nedávajú zmysel. Prečo by sme mali prechádzať obrázok s filtrom 1x1? Musíte si však uvedomiť, že konvolučné filtre pracujú aj s viacerými hĺbkovými kanálmi (pôvodne - RGB farby, v následných vrstvách - kanály pre rôzne filtre) a konvolúcia 1x1 sa používa na miešanie týchto vstupných kanálov pomocou rôznych trénovateľných váh. Môže byť tiež vnímaná ako downsampling (pooling) cez dimenziu kanálov.

Tu je [dobrý blogový príspevok](https://medium.com/analytics-vidhya/talented-mr-1x1-comprehensive-look-at-1x1-convolution-in-deep-learning-f6b355825578) na túto tému a [pôvodný článok](https://arxiv.org/pdf/1312.4400.pdf).

### MobileNet

MobileNet je rodina modelov so zmenšenou veľkosťou, vhodná pre mobilné zariadenia. Použite ich, ak máte obmedzené zdroje a môžete obetovať trochu presnosti. Hlavnou myšlienkou za nimi je tzv. **depthwise separable convolution**, ktorá umožňuje reprezentovať konvolučné filtre ako kompozíciu priestorových konvolúcií a konvolúcie 1x1 cez hĺbkové kanály. To výrazne znižuje počet parametrov, čím sa sieť zmenšuje a je tiež ľahšie trénovateľná s menším množstvom dát.

Tu je [dobrý blogový príspevok o MobileNet](https://medium.com/analytics-vidhya/image-classification-with-mobilenet-cc6fbb2cd470).

## Záver

V tejto jednotke ste sa naučili hlavný koncept za neurónovými sieťami pre počítačové videnie - konvolučné siete. Architektúry z reálneho života, ktoré poháňajú klasifikáciu obrázkov, detekciu objektov a dokonca aj siete na generovanie obrázkov, sú všetky založené na CNN, len s viacerými vrstvami a niektorými dodatočnými trikmi pri tréningu.

## 🚀 Výzva

V sprievodných notebookoch sú poznámky na spodku o tom, ako dosiahnuť vyššiu presnosť. Urobte niekoľko experimentov a zistite, či dokážete dosiahnuť vyššiu presnosť.

## [Kvíz po prednáške](https://ff-quizzes.netlify.app/en/ai/quiz/14)

## Prehľad a samostatné štúdium

Aj keď sa CNN najčastejšie používajú na úlohy počítačového videnia, vo všeobecnosti sú dobré na extrakciu vzorov s pevnou veľkosťou. Napríklad, ak pracujeme so zvukmi, môžeme tiež chcieť použiť CNN na hľadanie špecifických vzorov v audio signále - v takom prípade by filtre boli 1-dimenzionálne (a táto CNN by sa nazývala 1D-CNN). Niekedy sa tiež používa 3D-CNN na extrakciu vlastností v multidimenzionálnom priestore, ako sú určité udalosti odohrávajúce sa vo videu - CNN dokáže zachytiť určité vzory zmien vlastností v priebehu času. Urobte si prehľad a samostatné štúdium o ďalších úlohách, ktoré je možné vykonávať pomocou CNN.

## [Úloha](lab/README.md)

V tomto laboratóriu máte za úlohu klasifikovať rôzne plemená mačiek a psov. Tieto obrázky sú zložitejšie ako dataset MNIST, majú vyššie rozmery a je tu viac ako 10 tried.

**Upozornenie**:  
Tento dokument bol preložený pomocou služby AI prekladu [Co-op Translator](https://github.com/Azure/co-op-translator). Aj keď sa snažíme o presnosť, prosím, berte na vedomie, že automatizované preklady môžu obsahovať chyby alebo nepresnosti. Pôvodný dokument v jeho rodnom jazyku by mal byť považovaný za autoritatívny zdroj. Pre kritické informácie sa odporúča profesionálny ľudský preklad. Nenesieme zodpovednosť za akékoľvek nedorozumenia alebo nesprávne interpretácie vyplývajúce z použitia tohto prekladu.