<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "5abc5f7978919be90cd313f0c20e8228",
  "translation_date": "2025-09-07T14:33:21+00:00",
  "source_file": "lessons/3-NeuralNetworks/README.md",
  "language_code": "da"
}
-->
# Introduktion til Neurale Netværk

![Oversigt over Intro Neural Networks indhold i en doodle](../../../../translated_images/ai-neuralnetworks.1c687ae40bc86e834f497844866a26d3e0886650a67a4bbe29442e2f157d3b18.da.png)

Som vi diskuterede i introduktionen, er en af måderne at opnå intelligens på at træne en **computermodel** eller en **kunstig hjerne**. Siden midten af det 20. århundrede har forskere prøvet forskellige matematiske modeller, indtil denne retning i de seneste år har vist sig at være enormt succesfuld. Sådanne matematiske modeller af hjernen kaldes **neurale netværk**.

> Nogle gange kaldes neurale netværk for *Artificial Neural Networks*, ANNs, for at indikere, at vi taler om modeller og ikke rigtige netværk af neuroner.

## Maskinlæring

Neurale netværk er en del af en større disciplin kaldet **Maskinlæring**, hvis mål er at bruge data til at træne computermodeller, der kan løse problemer. Maskinlæring udgør en stor del af Kunstig Intelligens, men vi dækker ikke klassisk ML i dette pensum.

> Besøg vores separate **[Maskinlæring for begyndere](http://github.com/microsoft/ml-for-beginners)** pensum for at lære mere om klassisk maskinlæring.

I maskinlæring antager vi, at vi har et datasæt med eksempler **X** og tilsvarende outputværdier **Y**. Eksempler er ofte N-dimensionelle vektorer, der består af **features**, og outputs kaldes **labels**.

Vi vil se på de to mest almindelige maskinlæringsproblemer:

* **Klassifikation**, hvor vi skal klassificere et inputobjekt i to eller flere klasser.
* **Regression**, hvor vi skal forudsige et numerisk tal for hver af inputprøverne.

> Når inputs og outputs repræsenteres som tensorer, er inputdatasættet en matrix af størrelse M×N, hvor M er antallet af prøver, og N er antallet af features. Output labels Y er vektoren af størrelse M.

I dette pensum vil vi kun fokusere på neurale netværksmodeller.

## En model af en neuron

Fra biologien ved vi, at vores hjerne består af nerveceller, som hver har flere "inputs" (axoner) og et output (dendrit). Axoner og dendritter kan lede elektriske signaler, og forbindelserne mellem axoner og dendritter kan udvise forskellige grader af ledningsevne (kontrolleret af neuromediatorer).

![Model af en neuron](../../../../translated_images/synapse-wikipedia.ed20a9e4726ea1c6a3ce8fec51c0b9bec6181946dca0fe4e829bc12fa3bacf01.da.jpg) | ![Model af en neuron](../../../../translated_images/artneuron.1a5daa88d20ebe6f5824ddb89fba0bdaaf49f67e8230c1afbec42909df1fc17e.da.png)
----|----
Rigtig neuron *([Billede](https://en.wikipedia.org/wiki/Synapse#/media/File:SynapseSchematic_lines.svg) fra Wikipedia)* | Kunstig neuron *(Billede af forfatter)*

Den simpleste matematiske model af en neuron indeholder derfor flere inputs X<sub>1</sub>, ..., X<sub>N</sub> og et output Y samt en række vægte W<sub>1</sub>, ..., W<sub>N</sub>. Output beregnes som:

<img src="images/netout.png" alt="Y = f\left(\sum_{i=1}^N X_iW_i\right)" width="131" height="53" align="center"/>

hvor f er en ikke-lineær **aktiveringsfunktion**.

> Tidlige modeller af neuroner blev beskrevet i den klassiske artikel [A logical calculus of the ideas immanent in nervous activity](https://www.cs.cmu.edu/~./epxing/Class/10715/reading/McCulloch.and.Pitts.pdf) af Warren McCullock og Walter Pitts i 1943. Donald Hebb foreslog i sin bog "[The Organization of Behavior: A Neuropsychological Theory](https://books.google.com/books?id=VNetYrB8EBoC)" hvordan disse netværk kan trænes.

## I denne sektion

I denne sektion vil vi lære om:
* [Perceptron](03-Perceptron/README.md), en af de tidligste neurale netværksmodeller til to-klasse klassifikation
* [Multi-lags netværk](04-OwnFramework/README.md) med en tilhørende notebook [hvordan man bygger vores eget framework](04-OwnFramework/OwnFramework.ipynb)
* [Neurale netværksframeworks](05-Frameworks/README.md), med disse notebooks: [PyTorch](05-Frameworks/IntroPyTorch.ipynb) og [Keras/Tensorflow](05-Frameworks/IntroKerasTF.ipynb)
* [Overfitting](../../../../lessons/3-NeuralNetworks/05-Frameworks)

---

**Ansvarsfraskrivelse**:  
Dette dokument er blevet oversat ved hjælp af AI-oversættelsestjenesten [Co-op Translator](https://github.com/Azure/co-op-translator). Selvom vi bestræber os på nøjagtighed, skal du være opmærksom på, at automatiserede oversættelser kan indeholde fejl eller unøjagtigheder. Det originale dokument på dets oprindelige sprog bør betragtes som den autoritative kilde. For kritisk information anbefales professionel menneskelig oversættelse. Vi er ikke ansvarlige for eventuelle misforståelser eller fejltolkninger, der måtte opstå som følge af brugen af denne oversættelse.