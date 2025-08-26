<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "4522e22e150be0845e03aa41209a39d5",
  "translation_date": "2025-08-25T21:52:18+00:00",
  "source_file": "lessons/5-NLP/13-TextRep/README.md",
  "language_code": "sl"
}
-->
# Predstavljanje besedila kot tenzorjev

## [Predhodni kviz](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/113)

## Razvrščanje besedila

V prvem delu tega poglavja se bomo osredotočili na nalogo **razvrščanja besedila**. Uporabili bomo [AG News](https://www.kaggle.com/amananandrai/ag-news-classification-dataset) podatkovni niz, ki vsebuje novice, kot je naslednja:

* Kategorija: Znanost/Tehnologija
* Naslov: Ky. podjetje prejme subvencijo za raziskovanje peptidov (AP)
* Telo: AP - Podjetje, ki ga je ustanovil raziskovalec kemije na Univerzi v Louisvilleu, je prejelo subvencijo za razvoj...

Naš cilj bo razvrstiti novico v eno od kategorij na podlagi besedila.

## Predstavljanje besedila

Če želimo reševati naloge obdelave naravnega jezika (NLP) z nevronskimi mrežami, potrebujemo način za predstavitev besedila kot tenzorjev. Računalniki že predstavljajo besedilne znake kot številke, ki se preslikajo v pisave na vašem zaslonu, z uporabo kodiranj, kot sta ASCII ali UTF-8.

<img alt="Slika prikazuje diagram, ki preslika znak v ASCII in binarno predstavitev" src="images/ascii-character-map.png" width="50%"/>

> [Vir slike](https://www.seobility.net/en/wiki/ASCII)

Kot ljudje razumemo, kaj vsak znak **predstavlja**, in kako se vsi znaki združijo v besede stavka. Računalniki pa sami po sebi nimajo takšnega razumevanja, zato mora nevronska mreža pomen naučiti med treningom.

Zato lahko uporabimo različne pristope pri predstavljanju besedila:

* **Predstavitev na ravni znakov**, kjer besedilo predstavljamo tako, da vsak znak obravnavamo kot številko. Če imamo *C* različnih znakov v našem korpusu besedila, bi bila beseda *Hello* predstavljena kot 5x*C* tenzor. Vsaka črka bi ustrezala stolpcu tenzorja v enovrstični kodiranju.
* **Predstavitev na ravni besed**, kjer ustvarimo **besedišče** vseh besed v našem besedilu in nato besede predstavimo z enovrstičnim kodiranjem. Ta pristop je nekoliko boljši, saj posamezna črka sama po sebi nima velikega pomena, zato z uporabo višjih semantičnih konceptov - besed - poenostavimo nalogo za nevronsko mrežo. Vendar pa moramo zaradi velikega slovarja obravnavati visokodimenzionalne redke tenzorje.

Ne glede na predstavitev moramo najprej pretvoriti besedilo v zaporedje **tokenov**, pri čemer je en token lahko znak, beseda ali včasih celo del besede. Nato token pretvorimo v številko, običajno z uporabo **besedišča**, in to številko lahko vnesemo v nevronsko mrežo z enovrstičnim kodiranjem.

## N-grami

V naravnem jeziku je natančen pomen besed mogoče določiti le v kontekstu. Na primer, pomena *nevronska mreža* in *ribiška mreža* sta popolnoma različna. Eden od načinov, kako to upoštevati, je, da naš model zgradimo na parih besed in obravnavamo pare besed kot ločene tokene besedišča. Na ta način bo stavek *Rad grem na ribolov* predstavljen z naslednjim zaporedjem tokenov: *Rad grem*, *grem na*, *na ribolov*. Težava pri tem pristopu je, da se velikost slovarja znatno poveča, kombinacije, kot sta *na ribolov* in *na nakupovanje*, pa so predstavljene z različnimi tokeni, ki ne delijo nobene semantične podobnosti kljub istemu glagolu.

V nekaterih primerih lahko razmislimo o uporabi tri-gramov -- kombinacij treh besed -- prav tako. Ta pristop se pogosto imenuje **n-grami**. Smiselno je tudi uporabljati n-grame pri predstavitvi na ravni znakov, kjer n-grami približno ustrezajo različnim zlogom.

## Vreča besed in TF/IDF

Pri reševanju nalog, kot je razvrščanje besedila, moramo biti sposobni predstaviti besedilo z enim vektorjem fiksne velikosti, ki ga bomo uporabili kot vhod za končni gosti klasifikator. Eden najpreprostejših načinov za to je združiti vse posamezne predstavitve besed, npr. z njihovim seštevanjem. Če seštejemo enovrstična kodiranja vsake besede, dobimo vektor frekvenc, ki prikazuje, kolikokrat se vsaka beseda pojavi v besedilu. Takšna predstavitev besedila se imenuje **vreča besed** (BoW).

<img src="images/bow.png" width="90%"/>

> Slika avtorja

BoW v bistvu predstavlja, katere besede se pojavijo v besedilu in v kakšnih količinah, kar je lahko dober pokazatelj, o čem govori besedilo. Na primer, novica o politiki bo verjetno vsebovala besede, kot sta *predsednik* in *država*, medtem ko bo znanstvena publikacija imela nekaj, kot sta *trkalnik*, *odkritje* itd. Tako lahko frekvence besed v mnogih primerih dobro nakazujejo vsebino besedila.

Težava pri BoW je, da se določene pogoste besede, kot sta *in* in *je*, pojavljajo v večini besedil in imajo najvišje frekvence, kar zakrije besede, ki so resnično pomembne. Pomembnost teh besed lahko zmanjšamo tako, da upoštevamo frekvenco, s katero se besede pojavljajo v celotni zbirki dokumentov. To je glavna ideja pristopa TF/IDF, ki je podrobneje obravnavan v priloženih zvezkih k tej lekciji.

Vendar pa noben od teh pristopov ne more v celoti upoštevati **semantike** besedila. Za to potrebujemo močnejše modele nevronskih mrež, o katerih bomo razpravljali kasneje v tem poglavju.

## ✍️ Vaje: Predstavitev besedila

Nadaljujte z učenjem v naslednjih zvezkih:

* [Predstavitev besedila s PyTorch](../../../../../lessons/5-NLP/13-TextRep/TextRepresentationPyTorch.ipynb)
* [Predstavitev besedila s TensorFlow](../../../../../lessons/5-NLP/13-TextRep/TextRepresentationTF.ipynb)

## Zaključek

Do sedaj smo preučili tehnike, ki lahko dodajo frekvenčno težo različnim besedam. Vendar pa te tehnike ne morejo predstaviti pomena ali vrstnega reda. Kot je slavni lingvist J. R. Firth dejal leta 1935: "Popolni pomen besede je vedno kontekstualen, in nobena študija pomena brez konteksta ne more biti resna." Kasneje v tečaju se bomo naučili, kako zajeti kontekstualne informacije iz besedila z uporabo jezikovnega modeliranja.

## 🚀 Izziv

Preizkusite nekaj drugih vaj z uporabo vreče besed in različnih podatkovnih modelov. Navdih lahko najdete v tem [tekmovanju na Kagglu](https://www.kaggle.com/competitions/word2vec-nlp-tutorial/overview/part-1-for-beginners-bag-of-words).

## [Naknadni kviz](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/213)

## Pregled in samostojno učenje

Vadite svoje veščine z vgrajevanjem besedila in tehnikami vreče besed na [Microsoft Learn](https://docs.microsoft.com/learn/modules/intro-natural-language-processing-pytorch/?WT.mc_id=academic-77998-cacaste)

## [Naloga: Zvezki](assignment.md)

**Omejitev odgovornosti**:  
Ta dokument je bil preveden z uporabo storitve AI za prevajanje [Co-op Translator](https://github.com/Azure/co-op-translator). Čeprav si prizadevamo za natančnost, vas prosimo, da upoštevate, da lahko avtomatizirani prevodi vsebujejo napake ali netočnosti. Izvirni dokument v njegovem maternem jeziku je treba obravnavati kot avtoritativni vir. Za ključne informacije priporočamo profesionalni človeški prevod. Ne prevzemamo odgovornosti za morebitna nesporazumevanja ali napačne razlage, ki izhajajo iz uporabe tega prevoda.