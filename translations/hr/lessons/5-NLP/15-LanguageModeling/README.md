<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "31b46ba1f3aa78578134d4829f88be53",
  "translation_date": "2025-08-25T21:56:49+00:00",
  "source_file": "lessons/5-NLP/15-LanguageModeling/README.md",
  "language_code": "hr"
}
-->
# Modeliranje jezika

Semantičke ugrađene reprezentacije, poput Word2Vec i GloVe, zapravo su prvi korak prema **modeliranju jezika** - stvaranju modela koji na neki način *razumiju* (ili *predstavljaju*) prirodu jezika.

## [Kviz prije predavanja](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/115)

Glavna ideja modeliranja jezika je treniranje na nepodacima bez oznaka na nesuperviziran način. Ovo je važno jer imamo ogromne količine teksta bez oznaka, dok bi količina teksta s oznakama uvijek bila ograničena trudom koji možemo uložiti u označavanje. Najčešće možemo izgraditi modele jezika koji mogu **predvidjeti nedostajuće riječi** u tekstu, jer je lako sakriti nasumičnu riječ u tekstu i koristiti je kao uzorak za treniranje.

## Treniranje ugrađenih reprezentacija

U našim prethodnim primjerima koristili smo unaprijed trenirane semantičke ugrađene reprezentacije, ali zanimljivo je vidjeti kako se te reprezentacije mogu trenirati. Postoji nekoliko mogućih ideja koje se mogu koristiti:

* **N-Gram** modeliranje jezika, gdje predviđamo token gledajući N prethodnih tokena (N-gram)
* **Kontinuirana vreća riječi** (CBoW), gdje predviđamo srednji token $W_0$ u nizu tokena $W_{-N}$, ..., $W_N$.
* **Skip-gram**, gdje predviđamo skup susjednih tokena {$W_{-N},\dots, W_{-1}, W_1,\dots, W_N$} iz srednjeg tokena $W_0$.

![slika iz rada o pretvaranju riječi u vektore](../../../../../translated_images/example-algorithms-for-converting-words-to-vectors.fbe9207a726922f6f0f5de66427e8a6eda63809356114e28fb1fa5f4a83ebda7.hr.png)

> Slika iz [ovog rada](https://arxiv.org/pdf/1301.3781.pdf)

## ✍️ Primjeri bilježnica: Treniranje CBoW modela

Nastavite učiti kroz sljedeće bilježnice:

* [Treniranje CBoW Word2Vec s TensorFlowom](../../../../../lessons/5-NLP/15-LanguageModeling/CBoW-TF.ipynb)
* [Treniranje CBoW Word2Vec s PyTorchom](../../../../../lessons/5-NLP/15-LanguageModeling/CBoW-PyTorch.ipynb)

## Zaključak

U prethodnoj lekciji vidjeli smo da ugrađene reprezentacije riječi djeluju poput magije! Sada znamo da treniranje ugrađenih reprezentacija riječi nije vrlo složen zadatak, i trebali bismo biti u mogućnosti trenirati vlastite ugrađene reprezentacije za tekst specifičan za određeno područje ako je potrebno.

## [Kviz nakon predavanja](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/215)

## Pregled i samostalno učenje

* [Službeni PyTorch vodič o modeliranju jezika](https://pytorch.org/tutorials/beginner/nlp/word_embeddings_tutorial.html).
* [Službeni TensorFlow vodič o treniranju Word2Vec modela](https://www.TensorFlow.org/tutorials/text/word2vec).
* Korištenje okvira **gensim** za treniranje najčešće korištenih ugrađenih reprezentacija u nekoliko linija koda opisano je [u ovoj dokumentaciji](https://pytorch.org/tutorials/beginner/nlp/word_embeddings_tutorial.html).

## 🚀 [Zadatak: Trenirajte Skip-Gram model](lab/README.md)

U laboratoriju vas izazivamo da izmijenite kod iz ove lekcije kako biste trenirali Skip-Gram model umjesto CBoW. [Pročitajte detalje](lab/README.md)

**Odricanje od odgovornosti**:  
Ovaj dokument je preveden pomoću AI usluge za prevođenje [Co-op Translator](https://github.com/Azure/co-op-translator). Iako nastojimo osigurati točnost, imajte na umu da automatski prijevodi mogu sadržavati pogreške ili netočnosti. Izvorni dokument na izvornom jeziku treba smatrati autoritativnim izvorom. Za kritične informacije preporučuje se profesionalni prijevod od strane čovjeka. Ne preuzimamo odgovornost za nesporazume ili pogrešna tumačenja koja mogu proizaći iz korištenja ovog prijevoda.