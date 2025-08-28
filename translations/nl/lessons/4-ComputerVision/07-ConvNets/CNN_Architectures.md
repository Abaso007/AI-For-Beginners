<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "2f7b97b375358cb51a1e098df306bf73",
  "translation_date": "2025-08-28T19:25:11+00:00",
  "source_file": "lessons/4-ComputerVision/07-ConvNets/CNN_Architectures.md",
  "language_code": "nl"
}
-->
# Bekende CNN-Architecturen

### VGG-16

VGG-16 is een netwerk dat in 2014 een nauwkeurigheid van 92,7% behaalde in de ImageNet top-5 classificatie. Het heeft de volgende laagstructuur:

![ImageNet Lagen](../../../../../translated_images/vgg-16-arch1.d901a5583b3a51baeaab3e768567d921e5d54befa46e1e642616c5458c934028.nl.jpg)

Zoals je kunt zien, volgt VGG een traditionele piramide-architectuur, wat een opeenvolging is van convolutie-pooling lagen.

![ImageNet Piramide](../../../../../translated_images/vgg-16-arch.64ff2137f50dd49fdaa786e3f3a975b3f22615efd13efb19c5d22f12e01451a1.nl.jpg)

> Afbeelding van [Researchgate](https://www.researchgate.net/figure/Vgg16-model-structure-To-get-the-VGG-NIN-model-we-replace-the-2-nd-4-th-6-th-7-th_fig2_335194493)

### ResNet

ResNet is een familie van modellen voorgesteld door Microsoft Research in 2015. Het belangrijkste idee van ResNet is het gebruik van **residuele blokken**:

<img src="images/resnet-block.png" width="300"/>

> Afbeelding uit [dit artikel](https://arxiv.org/pdf/1512.03385.pdf)

De reden voor het gebruik van een identiteits-doorvoer is dat de laag **het verschil** voorspelt tussen het resultaat van een vorige laag en de output van het residuele blok - vandaar de naam *residueel*. Deze blokken zijn veel eenvoudiger te trainen, en men kan netwerken bouwen met honderden van deze blokken (de meest voorkomende varianten zijn ResNet-52, ResNet-101 en ResNet-152).

Je kunt dit netwerk ook zien als een systeem dat zijn complexiteit kan aanpassen aan de dataset. Aanvankelijk, wanneer je begint met het trainen van het netwerk, zijn de gewichten klein en gaat het meeste signaal door de identiteitslagen. Naarmate de training vordert en de gewichten groter worden, neemt het belang van de netwerkparameters toe, en past het netwerk zich aan om de benodigde expressieve kracht te bieden om trainingsafbeeldingen correct te classificeren.

### Google Inception

De Google Inception-architectuur gaat nog een stap verder en bouwt elke netwerklaag als een combinatie van verschillende paden:

<img src="images/inception.png" width="400"/>

> Afbeelding van [Researchgate](https://www.researchgate.net/figure/Inception-module-with-dimension-reductions-left-and-schema-for-Inception-ResNet-v1_fig2_355547454)

Hier moeten we de rol van 1x1-convoluties benadrukken, omdat ze in eerste instantie niet logisch lijken. Waarom zouden we een afbeelding doorlopen met een 1x1-filter? Je moet echter onthouden dat convolutiefilters ook werken met meerdere dieptekanalen (oorspronkelijk - RGB-kleuren, in latere lagen - kanalen voor verschillende filters), en 1x1-convolutie wordt gebruikt om deze invoerkanalen samen te voegen met verschillende trainbare gewichten. Het kan ook worden gezien als downsampling (pooling) over de kanaaldimensie.

Hier is [een goed blogartikel](https://medium.com/analytics-vidhya/talented-mr-1x1-comprehensive-look-at-1x1-convolution-in-deep-learning-f6b355825578) over dit onderwerp, en [het originele artikel](https://arxiv.org/pdf/1312.4400.pdf).

### MobileNet

MobileNet is een familie van modellen met een kleinere omvang, geschikt voor mobiele apparaten. Gebruik ze als je beperkte middelen hebt en een beetje nauwkeurigheid kunt opofferen. Het belangrijkste idee achter deze modellen is de zogenaamde **depthwise separable convolution**, waarmee convolutiefilters kunnen worden weergegeven als een samenstelling van ruimtelijke convoluties en 1x1-convolutie over dieptekanalen. Dit vermindert het aantal parameters aanzienlijk, waardoor het netwerk kleiner wordt en ook eenvoudiger te trainen is met minder data.

Hier is [een goed blogartikel over MobileNet](https://medium.com/analytics-vidhya/image-classification-with-mobilenet-cc6fbb2cd470).

## Conclusie

In deze eenheid heb je het belangrijkste concept achter neurale netwerken voor computervisie geleerd - convolutionele netwerken. Architecturen uit de praktijk die beeldclassificatie, objectdetectie en zelfs beeldgeneratie aandrijven, zijn allemaal gebaseerd op CNN's, alleen met meer lagen en enkele extra trainingstechnieken.

## 🚀 Uitdaging

In de bijbehorende notebooks staan notities onderaan over hoe je een hogere nauwkeurigheid kunt behalen. Doe wat experimenten om te zien of je een betere nauwkeurigheid kunt bereiken.

## [Post-lezing quiz](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/207)

## Review & Zelfstudie

Hoewel CNN's meestal worden gebruikt voor computervisie-taken, zijn ze over het algemeen goed in het extraheren van patronen van vaste grootte. Bijvoorbeeld, als we met geluiden werken, willen we misschien ook CNN's gebruiken om specifieke patronen in een audiosignaal te zoeken - in dat geval zouden filters 1-dimensionaal zijn (en dit CNN zou een 1D-CNN worden genoemd). Soms wordt ook een 3D-CNN gebruikt om kenmerken in een multidimensionale ruimte te extraheren, zoals bepaalde gebeurtenissen die plaatsvinden in video's - een CNN kan bepaalde patronen van kenmerkveranderingen in de tijd vastleggen. Doe wat onderzoek en zelfstudie over andere taken die met CNN's kunnen worden uitgevoerd.

## [Opdracht](lab/README.md)

In dit lab krijg je de taak om verschillende katten- en hondenrassen te classificeren. Deze afbeeldingen zijn complexer dan de MNIST-dataset, hebben hogere dimensies en er zijn meer dan 10 klassen.

---

**Disclaimer**:  
Dit document is vertaald met behulp van de AI-vertalingsservice [Co-op Translator](https://github.com/Azure/co-op-translator). Hoewel we streven naar nauwkeurigheid, dient u zich ervan bewust te zijn dat geautomatiseerde vertalingen fouten of onnauwkeurigheden kunnen bevatten. Het originele document in zijn oorspronkelijke taal moet worden beschouwd als de gezaghebbende bron. Voor cruciale informatie wordt professionele menselijke vertaling aanbevolen. Wij zijn niet aansprakelijk voor eventuele misverstanden of verkeerde interpretaties die voortvloeien uit het gebruik van deze vertaling.