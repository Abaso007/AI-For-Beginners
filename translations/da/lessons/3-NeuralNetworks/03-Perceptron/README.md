<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "0c37770bba4fff3c71dc00eb261ee61b",
  "translation_date": "2025-08-28T15:38:59+00:00",
  "source_file": "lessons/3-NeuralNetworks/03-Perceptron/README.md",
  "language_code": "da"
}
-->
# Introduktion til neurale netværk: Perceptron

## [Quiz før forelæsning](https://ff-quizzes.netlify.app/en/ai/quiz/5)

En af de første forsøg på at implementere noget, der minder om et moderne neuralt netværk, blev udført af Frank Rosenblatt fra Cornell Aeronautical Laboratory i 1957. Det var en hardwareimplementering kaldet "Mark-1", designet til at genkende primitive geometriske figurer, såsom trekanter, firkanter og cirkler.

|      |      |
|--------------|-----------|
|<img src='images/Rosenblatt-wikipedia.jpg' alt='Frank Rosenblatt'/> | <img src='images/Mark_I_perceptron_wikipedia.jpg' alt='The Mark 1 Perceptron' />|

> Billeder [fra Wikipedia](https://en.wikipedia.org/wiki/Perceptron)

Et inputbillede blev repræsenteret af et 20x20 fotocelle-array, så det neurale netværk havde 400 inputs og én binær output. Et simpelt netværk indeholdt én neuron, også kaldet en **threshold logic unit**. Vægtene i det neurale netværk fungerede som potentiometre, der krævede manuel justering under træningsfasen.

> ✅ Et potentiometer er en enhed, der giver brugeren mulighed for at justere modstanden i et kredsløb.

> The New York Times skrev om perceptron på det tidspunkt: *embryoet af en elektronisk computer, som [flåden] forventer vil kunne gå, tale, se, skrive, reproducere sig selv og være bevidst om sin egen eksistens.*

## Perceptron-modellen

Antag, at vi har N funktioner i vores model, i hvilket tilfælde inputvektoren ville være en vektor af størrelse N. En perceptron er en **binær klassifikationsmodel**, dvs. den kan skelne mellem to klasser af inputdata. Vi antager, at for hver inputvektor x vil outputtet fra vores perceptron være enten +1 eller -1, afhængigt af klassen. Outputtet beregnes ved hjælp af formlen:

y(x) = f(w<sup>T</sup>x)

hvor f er en step-aktiveringsfunktion

<!-- img src="http://www.sciweavers.org/tex2img.php?eq=f%28x%29%20%3D%20%5Cbegin%7Bcases%7D%0A%20%20%20%20%20%20%20%20%20%2B1%20%26%20x%20%5Cgeq%200%20%5C%5C%0A%20%20%20%20%20%20%20%20%20-1%20%26%20x%20%3C%200%0A%20%20%20%20%20%20%20%5Cend%7Bcases%7D%20%5C%5C%0A&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0" align="center" border="0" alt="f(x) = \begin{cases} +1 & x \geq 0 \\ -1 & x < 0 \end{cases} \\" width="154" height="50" / -->
<img src="images/activation-func.png"/>

## Træning af perceptron

For at træne en perceptron skal vi finde en vægtvektor w, der klassificerer de fleste værdier korrekt, dvs. resulterer i den mindste **fejl**. Denne fejl E er defineret af **perceptron-kriteriet** på følgende måde:

E(w) = -∑w<sup>T</sup>x<sub>i</sub>t<sub>i</sub>

hvor:

* summen tages over de træningsdatapunkter i, der resulterer i en forkert klassifikation
* x<sub>i</sub> er inputdata, og t<sub>i</sub> er enten -1 eller +1 for henholdsvis negative og positive eksempler.

Dette kriterium betragtes som en funktion af vægtene w, og vi skal minimere det. Ofte bruges en metode kaldet **gradient descent**, hvor vi starter med nogle indledende vægte w<sup>(0)</sup>, og derefter opdaterer vægtene ved hver iteration i henhold til formlen:

w<sup>(t+1)</sup> = w<sup>(t)</sup> - η∇E(w)

Her er η den såkaldte **læringsrate**, og ∇E(w) betegner **gradienten** af E. Efter beregning af gradienten ender vi med

w<sup>(t+1)</sup> = w<sup>(t)</sup> + ∑ηx<sub>i</sub>t<sub>i</sub>

Algoritmen i Python ser sådan ud:

```python
def train(positive_examples, negative_examples, num_iterations = 100, eta = 1):

    weights = [0,0,0] # Initialize weights (almost randomly :)
        
    for i in range(num_iterations):
        pos = random.choice(positive_examples)
        neg = random.choice(negative_examples)

        z = np.dot(pos, weights) # compute perceptron output
        if z < 0: # positive example classified as negative
            weights = weights + eta*weights.shape

        z  = np.dot(neg, weights)
        if z >= 0: # negative example classified as positive
            weights = weights - eta*weights.shape

    return weights
```

## Konklusion

I denne lektion lærte du om en perceptron, som er en binær klassifikationsmodel, og hvordan man træner den ved hjælp af en vægtvektor.

## 🚀 Udfordring

Hvis du vil prøve at bygge din egen perceptron, kan du prøve [denne lab på Microsoft Learn](https://docs.microsoft.com/en-us/azure/machine-learning/component-reference/two-class-averaged-perceptron?WT.mc_id=academic-77998-cacaste), som bruger [Azure ML designer](https://docs.microsoft.com/en-us/azure/machine-learning/concept-designer?WT.mc_id=academic-77998-cacaste).

## [Quiz efter forelæsning](https://ff-quizzes.netlify.app/en/ai/quiz/6)

## Gennemgang & Selvstudie

For at se, hvordan vi kan bruge perceptron til at løse både et simpelt problem og virkelige problemer, og for at fortsætte læringen - gå til [Perceptron](Perceptron.ipynb)-notebook.

Her er en interessant [artikel om perceptrons](https://towardsdatascience.com/what-is-a-perceptron-basics-of-neural-networks-c4cfea20c590).

## [Opgave](lab/README.md)

I denne lektion har vi implementeret en perceptron til en binær klassifikationsopgave, og vi har brugt den til at klassificere mellem to håndskrevne cifre. I denne lab bliver du bedt om at løse problemet med cifreklassifikation fuldstændigt, dvs. bestemme hvilket ciffer der sandsynligvis svarer til et givet billede.

* [Instruktioner](lab/README.md)
* [Notebook](lab/PerceptronMultiClass.ipynb)

---

**Ansvarsfraskrivelse**:  
Dette dokument er blevet oversat ved hjælp af AI-oversættelsestjenesten [Co-op Translator](https://github.com/Azure/co-op-translator). Selvom vi bestræber os på nøjagtighed, skal du være opmærksom på, at automatiserede oversættelser kan indeholde fejl eller unøjagtigheder. Det originale dokument på dets oprindelige sprog bør betragtes som den autoritative kilde. For kritisk information anbefales professionel menneskelig oversættelse. Vi påtager os intet ansvar for misforståelser eller fejltolkninger, der måtte opstå som følge af brugen af denne oversættelse.