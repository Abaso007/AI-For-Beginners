<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "d9de7847385eeeda67cfdcce1640ab72",
  "translation_date": "2025-08-25T21:43:57+00:00",
  "source_file": "lessons/5-NLP/17-GenerativeNetworks/README.md",
  "language_code": "cs"
}
-->
# Generativní sítě

## [Kvíz před přednáškou](https://ff-quizzes.netlify.app/en/ai/quiz/33)

Rekurentní neuronové sítě (RNN) a jejich varianty s bránovými buňkami, jako jsou Long Short Term Memory Cells (LSTM) a Gated Recurrent Units (GRU), poskytují mechanismus pro modelování jazyka, protože se dokážou naučit pořadí slov a předpovídat další slovo v sekvenci. To nám umožňuje používat RNN pro **generativní úlohy**, jako je generování běžného textu, strojový překlad nebo dokonce popisování obrázků.

> ✅ Zamyslete se nad všemi situacemi, kdy jste využili generativní úlohy, například při doplňování textu během psaní. Prozkoumejte své oblíbené aplikace a zjistěte, zda využívají RNN.

V architektuře RNN, kterou jsme probírali v předchozí kapitole, každá jednotka RNN produkovala další skrytý stav jako výstup. Můžeme však také přidat další výstup ke každé rekurentní jednotce, což nám umožní generovat **sekvenci** (která má stejnou délku jako původní sekvence). Navíc můžeme použít RNN jednotky, které nepřijímají vstup na každém kroku, ale pouze počáteční stavový vektor, a poté generují sekvenci výstupů.

To umožňuje různé neuronové architektury, jak je znázorněno na obrázku níže:

![Obrázek ukazující běžné vzory rekurentních neuronových sítí.](../../../../../translated_images/unreasonable-effectiveness-of-rnn.541ead816778f42dce6c42d8a56c184729aa2378d059b851be4ce12b993033df.cs.jpg)

> Obrázek z blogového příspěvku [Unreasonable Effectiveness of Recurrent Neural Networks](http://karpathy.github.io/2015/05/21/rnn-effectiveness/) od [Andreje Karpatyho](http://karpathy.github.io/)

* **One-to-one** je tradiční neuronová síť s jedním vstupem a jedním výstupem.
* **One-to-many** je generativní architektura, která přijímá jednu vstupní hodnotu a generuje sekvenci výstupních hodnot. Například pokud chceme trénovat síť pro **popisování obrázků**, která by vytvořila textový popis obrázku, můžeme jako vstup použít obrázek, zpracovat jej pomocí CNN pro získání skrytého stavu a poté nechat rekurentní řetězec generovat popis slovo po slovu.
* **Many-to-one** odpovídá architekturám RNN, které jsme popsali v předchozí kapitole, například klasifikace textu.
* **Many-to-many**, nebo **sekvence na sekvenci**, odpovídá úlohám, jako je **strojový překlad**, kde první RNN shromáždí všechny informace ze vstupní sekvence do skrytého stavu a další řetězec RNN tento stav rozvine do výstupní sekvence.

V této kapitole se zaměříme na jednoduché generativní modely, které nám pomohou generovat text. Pro zjednodušení použijeme tokenizaci na úrovni znaků.

Budeme trénovat tuto RNN, aby generovala text krok za krokem. Na každém kroku vezmeme sekvenci znaků o délce `nchars` a požádáme síť, aby pro každý vstupní znak vygenerovala další výstupní znak:

![Obrázek ukazující příklad generování slova 'HELLO' pomocí RNN.](../../../../../translated_images/rnn-generate.56c54afb52f9781d63a7c16ea9c1b86cb70e6e1eae6a742b56b7b37468576b17.cs.png)

Při generování textu (během inferencí) začneme s nějakým **podnětem**, který je předán přes RNN buňky pro vytvoření mezistavu, a poté z tohoto stavu začíná generování. Generujeme jeden znak po druhém a předáváme stav a vygenerovaný znak další RNN buňce, aby vygenerovala další znak, dokud nevygenerujeme dostatek znaků.

<img src="images/rnn-generate-inf.png" width="60%"/>

> Obrázek od autora

## ✍️ Cvičení: Generativní sítě

Pokračujte ve svém učení v následujících noteboocích:

* [Generativní sítě s PyTorch](../../../../../lessons/5-NLP/17-GenerativeNetworks/GenerativePyTorch.ipynb)
* [Generativní sítě s TensorFlow](../../../../../lessons/5-NLP/17-GenerativeNetworks/GenerativeTF.ipynb)

## Měkké generování textu a teplota

Výstup každé RNN buňky je pravděpodobnostní rozdělení znaků. Pokud bychom vždy vybrali znak s nejvyšší pravděpodobností jako další znak v generovaném textu, text by se často mohl "zacyklit" mezi stejnými sekvencemi znaků znovu a znovu, jako v tomto příkladu:

```
today of the second the company and a second the company ...
```

Pokud se však podíváme na pravděpodobnostní rozdělení pro další znak, může se stát, že rozdíl mezi několika nejvyššími pravděpodobnostmi není velký, např. jeden znak může mít pravděpodobnost 0,2, jiný 0,19 atd. Například při hledání dalšího znaku v sekvenci '*play*' může být dalším znakem stejně dobře mezera nebo **e** (jako ve slově *player*).

To nás vede k závěru, že není vždy "spravedlivé" vybrat znak s nejvyšší pravděpodobností, protože výběr druhého nejvyššího může stále vést k smysluplnému textu. Je moudřejší **vzorkovat** znaky z pravděpodobnostního rozdělení daného výstupem sítě. Můžeme také použít parametr **teplota**, který vyhladí pravděpodobnostní rozdělení, pokud chceme přidat více náhodnosti, nebo jej udělat strmějším, pokud chceme více dodržovat znaky s nejvyšší pravděpodobností.

Prozkoumejte, jak je toto měkké generování textu implementováno v noteboocích uvedených výše.

## Závěr

Ačkoli generování textu může být užitečné samo o sobě, hlavní přínosy přicházejí ze schopnosti generovat text pomocí RNN z nějakého počátečního vektorového znaku. Například generování textu se používá jako součást strojového překladu (sekvence na sekvenci, v tomto případě se stavový vektor z *enkodéru* používá k vytvoření nebo *dekódování* přeložené zprávy) nebo generování textového popisu obrázku (v tomto případě pochází vektor znaků z extraktoru CNN).

## 🚀 Výzva

Absolvujte některé lekce na Microsoft Learn na toto téma:

* Generování textu s [PyTorch](https://docs.microsoft.com/learn/modules/intro-natural-language-processing-pytorch/6-generative-networks/?WT.mc_id=academic-77998-cacaste)/[TensorFlow](https://docs.microsoft.com/learn/modules/intro-natural-language-processing-tensorflow/5-generative-networks/?WT.mc_id=academic-77998-cacaste)

## [Kvíz po přednášce](https://ff-quizzes.netlify.app/en/ai/quiz/34)

## Přehled a samostudium

Zde jsou některé články pro rozšíření vašich znalostí:

* Různé přístupy k generování textu pomocí Markovova řetězce, LSTM a GPT-2: [blogový příspěvek](https://towardsdatascience.com/text-generation-gpt-2-lstm-markov-chain-9ea371820e1e)
* Ukázka generování textu v [dokumentaci Keras](https://keras.io/examples/generative/lstm_character_level_text_generation/)

## [Úkol](lab/README.md)

Viděli jsme, jak generovat text znak po znaku. V laboratoři budete zkoumat generování textu na úrovni slov.

**Prohlášení:**  
Tento dokument byl přeložen pomocí služby pro automatický překlad [Co-op Translator](https://github.com/Azure/co-op-translator). Ačkoli se snažíme o přesnost, mějte prosím na paměti, že automatické překlady mohou obsahovat chyby nebo nepřesnosti. Původní dokument v jeho původním jazyce by měl být považován za autoritativní zdroj. Pro důležité informace se doporučuje profesionální lidský překlad. Neodpovídáme za žádná nedorozumění nebo nesprávné interpretace vzniklé v důsledku použití tohoto překladu.