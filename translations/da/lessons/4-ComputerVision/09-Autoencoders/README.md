<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "0b306c04f5337b6e7430e5c0b16bb5c0",
  "translation_date": "2025-08-28T15:24:03+00:00",
  "source_file": "lessons/4-ComputerVision/09-Autoencoders/README.md",
  "language_code": "da"
}
-->
# Autoencodere

Når man træner CNN'er, er en af udfordringerne, at vi har brug for en stor mængde mærkede data. I tilfælde af billedklassifikation skal vi adskille billeder i forskellige klasser, hvilket kræver manuel indsats.

## [Pre-lecture quiz](https://ff-quizzes.netlify.app/en/ai/quiz/17)

Vi kan dog ønske at bruge rå (umærkede) data til at træne CNN-featureekstraktorer, hvilket kaldes **selv-supervised learning**. I stedet for labels bruger vi træningsbilleder som både netværksinput og output. Hovedideen med en **autoencoder** er, at vi har et **encoder-netværk**, der konverterer inputbilledet til et **latent rum** (normalt er det blot en vektor af mindre størrelse), og derefter et **decoder-netværk**, hvis mål er at rekonstruere det originale billede.

> ✅ En [autoencoder](https://wikipedia.org/wiki/Autoencoder) er "en type kunstigt neuralt netværk, der bruges til at lære effektive kodninger af umærkede data."

Da vi træner en autoencoder til at fange så meget information som muligt fra det originale billede for en præcis rekonstruktion, forsøger netværket at finde den bedste **embedding** af inputbilleder for at fange meningen.

![AutoEncoder Diagram](../../../../../translated_images/autoencoder_schema.5e6fc9ad98a5eb6197f3513cf3baf4dfbe1389a6ae74daebda64de9f1c99f142.da.jpg)

> Billede fra [Keras blog](https://blog.keras.io/building-autoencoders-in-keras.html)

## Scenarier for brug af Autoencodere

Selvom rekonstruktion af originale billeder ikke virker nyttigt i sig selv, er der nogle scenarier, hvor autoencodere er særligt nyttige:

* **Reducering af billeddimensioner til visualisering** eller **træning af billede-embeddings**. Autoencodere giver normalt bedre resultater end PCA, fordi de tager højde for billedernes rumlige natur og hierarkiske features.
* **Denoising**, dvs. fjernelse af støj fra billedet. Da støj indeholder en masse unyttig information, kan autoencoderen ikke passe det hele ind i det relativt lille latente rum og fanger derfor kun den vigtige del af billedet. Når vi træner støjfjernerne, starter vi med originale billeder og bruger billeder med kunstigt tilføjet støj som input til autoencoderen.
* **Super-resolution**, øgning af billedopløsning. Vi starter med billeder i høj opløsning og bruger billeder med lavere opløsning som autoencoderens input.
* **Generative modeller**. Når vi har trænet autoencoderen, kan decoder-delen bruges til at skabe nye objekter ud fra tilfældige latente vektorer.

## Variationsautoencodere (VAE)

Traditionelle autoencodere reducerer dimensionen af inputdata på en eller anden måde og finder de vigtige features i inputbillederne. Dog giver latente vektorer ofte ikke meget mening. Med andre ord, hvis vi tager MNIST-datasættet som eksempel, er det ikke nemt at finde ud af, hvilke cifre der svarer til forskellige latente vektorer, fordi nærliggende latente vektorer ikke nødvendigvis svarer til de samme cifre.

På den anden side er det bedre at have en forståelse af det latente rum, når man træner *generative* modeller. Denne idé fører os til **variationsautoencoder** (VAE).

VAE er en autoencoder, der lærer at forudsige *statistisk fordeling* af de latente parametre, det såkaldte **latente fordeling**. For eksempel kan vi ønske, at latente vektorer er normalt fordelt med en middelværdi z<sub>mean</sub> og standardafvigelse z<sub>sigma</sub> (både middelværdi og standardafvigelse er vektorer med en vis dimensionalitet d). Encoderen i VAE lærer at forudsige disse parametre, og derefter tager decoderen en tilfældig vektor fra denne fordeling for at rekonstruere objektet.

For at opsummere:

 * Fra inputvektoren forudsiger vi `z_mean` og `z_log_sigma` (i stedet for at forudsige selve standardafvigelsen, forudsiger vi dens logaritme)
 * Vi sampler en vektor `sample` fra fordelingen N(z<sub>mean</sub>,exp(z<sub>log\_sigma</sub>))
 * Decoderen forsøger at dekode det originale billede ved hjælp af `sample` som inputvektor

 <img src="images/vae.png" width="50%">

> Billede fra [denne blogpost](https://ijdykeman.github.io/ml/2016/12/21/cvae.html) af Isaak Dykeman

Variationsautoencodere bruger en kompleks tabfunktion, der består af to dele:

* **Rekonstruktionstab** er tabfunktionen, der viser, hvor tæt et rekonstrueret billede er på målet (det kan være Mean Squared Error, eller MSE). Det er den samme tabfunktion som i normale autoencodere.
* **KL-tab**, som sikrer, at den latente variabels fordeling forbliver tæt på normalfordelingen. Det er baseret på begrebet [Kullback-Leibler divergence](https://www.countbayesie.com/blog/2017/5/9/kullback-leibler-divergence-explained) - en metrik til at estimere, hvor ens to statistiske fordelinger er.

En vigtig fordel ved VAE'er er, at de gør det relativt nemt at generere nye billeder, fordi vi ved, hvilken fordeling vi skal sample latente vektorer fra. For eksempel, hvis vi træner VAE med en 2D latent vektor på MNIST, kan vi derefter variere komponenterne i den latente vektor for at få forskellige cifre:

<img alt="vaemnist" src="images/vaemnist.png" width="50%"/>

> Billede af [Dmitry Soshnikov](http://soshnikov.com)

Bemærk, hvordan billederne smelter sammen, når vi begynder at få latente vektorer fra forskellige dele af det latente parameter-rum. Vi kan også visualisere dette rum i 2D:

<img alt="vaemnist cluster" src="images/vaemnist-diag.png" width="50%"/> 

> Billede af [Dmitry Soshnikov](http://soshnikov.com)

## ✍️ Øvelser: Autoencodere

Lær mere om autoencodere i disse tilhørende notebooks:

* [Autoencodere i TensorFlow](AutoencodersTF.ipynb)
* [Autoencodere i PyTorch](AutoEncodersPyTorch.ipynb)

## Egenskaber ved Autoencodere

* **Dataspecifikke** - de fungerer kun godt med den type billeder, de er blevet trænet på. For eksempel, hvis vi træner et super-resolution-netværk på blomster, vil det ikke fungere godt på portrætter. Dette skyldes, at netværket kan producere billeder i højere opløsning ved at tage fine detaljer fra features, der er lært fra træningsdatasættet.
* **Tabsgivende** - det rekonstruerede billede er ikke det samme som det originale billede. Naturen af tabet defineres af den *tabfunktion*, der bruges under træningen.
* Fungerer på **umærkede data**

## [Post-lecture quiz](https://ff-quizzes.netlify.app/en/ai/quiz/18)

## Konklusion

I denne lektion lærte du om de forskellige typer autoencodere, der er tilgængelige for AI-forskeren. Du lærte, hvordan man bygger dem, og hvordan man bruger dem til at rekonstruere billeder. Du lærte også om VAE og hvordan man bruger det til at generere nye billeder.

## 🚀 Udfordring

I denne lektion lærte du om brugen af autoencodere til billeder. Men de kan også bruges til musik! Tjek Magenta-projektets [MusicVAE](https://magenta.tensorflow.org/music-vae) projekt, som bruger autoencodere til at lære at rekonstruere musik. Lav nogle [eksperimenter](https://colab.research.google.com/github/magenta/magenta-demos/blob/master/colab-notebooks/Multitrack_MusicVAE.ipynb) med dette bibliotek for at se, hvad du kan skabe.

## [Post-lecture quiz](https://ff-quizzes.netlify.app/en/ai/quiz/16)

## Gennemgang & Selvstudie

For reference, læs mere om autoencodere i disse ressourcer:

* [Building Autoencoders in Keras](https://blog.keras.io/building-autoencoders-in-keras.html)
* [Blogpost på NeuroHive](https://neurohive.io/ru/osnovy-data-science/variacionnyj-avtojenkoder-vae/)
* [Variational Autoencoders Explained](https://kvfrans.com/variational-autoencoders-explained/)
* [Conditional Variational Autoencoders](https://ijdykeman.github.io/ml/2016/12/21/cvae.html)

## Opgave

I slutningen af [denne notebook med TensorFlow](AutoencodersTF.ipynb) finder du en 'opgave' - brug denne som din opgave.

---

**Ansvarsfraskrivelse**:  
Dette dokument er blevet oversat ved hjælp af AI-oversættelsestjenesten [Co-op Translator](https://github.com/Azure/co-op-translator). Selvom vi bestræber os på at sikre nøjagtighed, skal det bemærkes, at automatiserede oversættelser kan indeholde fejl eller unøjagtigheder. Det originale dokument på dets oprindelige sprog bør betragtes som den autoritative kilde. For kritisk information anbefales professionel menneskelig oversættelse. Vi påtager os ikke ansvar for eventuelle misforståelser eller fejltolkninger, der måtte opstå som følge af brugen af denne oversættelse.