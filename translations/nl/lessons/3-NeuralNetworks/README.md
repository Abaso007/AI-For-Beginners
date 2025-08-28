<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "1c6b8c7c1778a35fc1139b7f2aecb7b3",
  "translation_date": "2025-08-28T19:45:43+00:00",
  "source_file": "lessons/3-NeuralNetworks/README.md",
  "language_code": "nl"
}
-->
# Introductie tot Neurale Netwerken

![Samenvatting van Intro Neural Networks inhoud in een schets](../../../../translated_images/ai-neuralnetworks.1c687ae40bc86e834f497844866a26d3e0886650a67a4bbe29442e2f157d3b18.nl.png)

Zoals we in de introductie hebben besproken, is een van de manieren om intelligentie te bereiken het trainen van een **computermodel** of een **kunstmatig brein**. Sinds het midden van de 20e eeuw hebben onderzoekers verschillende wiskundige modellen geprobeerd, totdat deze richting de afgelopen jaren enorm succesvol bleek te zijn. Dergelijke wiskundige modellen van het brein worden **neurale netwerken** genoemd.

> Soms worden neurale netwerken *Kunstmatige Neurale Netwerken* genoemd, ANNs, om aan te geven dat we het hebben over modellen en niet over echte netwerken van neuronen.

## Machine Learning

Neurale netwerken maken deel uit van een bredere discipline genaamd **Machine Learning**, waarvan het doel is om gegevens te gebruiken om computermodellen te trainen die problemen kunnen oplossen. Machine Learning vormt een groot deel van Kunstmatige Intelligentie, maar we behandelen klassieke ML niet in deze leerstof.

> Bezoek ons aparte **[Machine Learning voor Beginners](http://github.com/microsoft/ml-for-beginners)** curriculum om meer te leren over klassieke Machine Learning.

In Machine Learning gaan we ervan uit dat we een dataset hebben met voorbeelden **X** en bijbehorende uitvoerwaarden **Y**. Voorbeelden zijn vaak N-dimensionale vectoren die bestaan uit **kenmerken**, en uitvoerwaarden worden **labels** genoemd.

We zullen de twee meest voorkomende problemen in Machine Learning bekijken:

* **Classificatie**, waarbij we een invoerobject moeten indelen in twee of meer klassen.
* **Regressie**, waarbij we een numerieke waarde moeten voorspellen voor elk van de invoerobjecten.

> Bij het representeren van invoer en uitvoer als tensors is de invoerdataset een matrix van grootte M×N, waarbij M het aantal voorbeelden is en N het aantal kenmerken. Uitvoerlabels Y zijn de vector van grootte M.

In dit curriculum richten we ons uitsluitend op modellen van neurale netwerken.

## Een Model van een Neuron

Uit de biologie weten we dat ons brein bestaat uit neurale cellen, die elk meerdere "inputs" (axonen) en een output (dendriet) hebben. Axonen en dendrieten kunnen elektrische signalen geleiden, en verbindingen tussen axonen en dendrieten kunnen verschillende graden van geleiding vertonen (gereguleerd door neurotransmitters).

![Model van een Neuron](../../../../translated_images/synapse-wikipedia.ed20a9e4726ea1c6a3ce8fec51c0b9bec6181946dca0fe4e829bc12fa3bacf01.nl.jpg) | ![Model van een Neuron](../../../../translated_images/artneuron.1a5daa88d20ebe6f5824ddb89fba0bdaaf49f67e8230c1afbec42909df1fc17e.nl.png)
----|----
Echte Neuron *([Afbeelding](https://en.wikipedia.org/wiki/Synapse#/media/File:SynapseSchematic_lines.svg) van Wikipedia)* | Kunstmatige Neuron *(Afbeelding door Auteur)*

Het eenvoudigste wiskundige model van een neuron bevat dus meerdere inputs X<sub>1</sub>, ..., X<sub>N</sub> en een output Y, en een reeks gewichten W<sub>1</sub>, ..., W<sub>N</sub>. Een output wordt berekend als:

<img src="images/netout.png" alt="Y = f\left(\sum_{i=1}^N X_iW_i\right)" width="131" height="53" align="center"/>

waarbij f een niet-lineaire **activatiefunctie** is.

> Vroege modellen van neuronen werden beschreven in het klassieke artikel [A logical calculus of the ideas immanent in nervous activity](https://www.cs.cmu.edu/~./epxing/Class/10715/reading/McCulloch.and.Pitts.pdf) door Warren McCullock en Walter Pitts in 1943. Donald Hebb stelde in zijn boek "[The Organization of Behavior: A Neuropsychological Theory](https://books.google.com/books?id=VNetYrB8EBoC)" een manier voor waarop deze netwerken kunnen worden getraind.

## In deze Sectie

In deze sectie leren we over:
* [Perceptron](03-Perceptron/README.md), een van de vroegste neurale netwerkmodellen voor tweeklassenclassificatie
* [Multi-layered netwerken](04-OwnFramework/README.md) met een bijbehorend notebook [hoe we ons eigen framework kunnen bouwen](04-OwnFramework/OwnFramework.ipynb)
* [Neurale Netwerk Frameworks](05-Frameworks/README.md), met deze notebooks: [PyTorch](05-Frameworks/IntroPyTorch.ipynb) en [Keras/Tensorflow](05-Frameworks/IntroKerasTF.ipynb)
* [Overfitting](../../../../lessons/3-NeuralNetworks/05-Frameworks)

---

**Disclaimer**:  
Dit document is vertaald met behulp van de AI-vertalingsservice [Co-op Translator](https://github.com/Azure/co-op-translator). Hoewel we streven naar nauwkeurigheid, dient u zich ervan bewust te zijn dat geautomatiseerde vertalingen fouten of onnauwkeurigheden kunnen bevatten. Het originele document in zijn oorspronkelijke taal moet worden beschouwd als de gezaghebbende bron. Voor cruciale informatie wordt professionele menselijke vertaling aanbevolen. Wij zijn niet aansprakelijk voor eventuele misverstanden of verkeerde interpretaties die voortvloeien uit het gebruik van deze vertaling.