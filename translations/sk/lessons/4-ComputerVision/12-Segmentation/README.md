<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "d7f8a25ff13cfe9f4cd671cc23351fad",
  "translation_date": "2025-08-25T22:34:08+00:00",
  "source_file": "lessons/4-ComputerVision/12-Segmentation/README.md",
  "language_code": "sk"
}
-->
# Segmentácia

Predtým sme sa naučili o detekcii objektov, ktorá nám umožňuje lokalizovať objekty na obrázku predpovedaním ich *ohraničujúcich boxov*. Pre niektoré úlohy však nestačia len ohraničujúce boxy, ale potrebujeme presnejšiu lokalizáciu objektov. Táto úloha sa nazýva **segmentácia**.

## [Kvíz pred prednáškou](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/112)

Segmentáciu môžeme vnímať ako **klasifikáciu pixelov**, kde pre **každý** pixel obrázka musíme predpovedať jeho triedu (*pozadie* je jednou z tried). Existujú dva hlavné algoritmy segmentácie:

* **Semantická segmentácia** určuje iba triedu pixelu a nerozlišuje medzi rôznymi objektmi tej istej triedy.
* **Inštančná segmentácia** rozdeľuje triedy na rôzne inštancie.

Pri inštančnej segmentácii sú tieto ovce rôznymi objektmi, ale pri semantickej segmentácii sú všetky ovce reprezentované jednou triedou.

<img src="images/instance_vs_semantic.jpeg" width="50%">

> Obrázok z [tohto blogového príspevku](https://nirmalamurali.medium.com/image-classification-vs-semantic-segmentation-vs-instance-segmentation-625c33a08d50)

Existujú rôzne neurónové architektúry pre segmentáciu, ale všetky majú rovnakú štruktúru. Istým spôsobom je to podobné autoenkóderu, o ktorom ste sa už učili, ale namiesto rekonštrukcie pôvodného obrázka je naším cieľom rekonštruovať **masku**. Segmentačná sieť má teda nasledujúce časti:

* **Encoder** extrahuje vlastnosti z vstupného obrázka.
* **Decoder** transformuje tieto vlastnosti do **obrázka masky**, ktorý má rovnakú veľkosť a počet kanálov zodpovedajúci počtu tried.

<img src="images/segm.png" width="80%">

> Obrázok z [tejto publikácie](https://arxiv.org/pdf/2001.05566.pdf)

Osobitne by sme mali spomenúť stratovú funkciu, ktorá sa používa pri segmentácii. Pri použití klasických autoenkóderov musíme merať podobnosť medzi dvoma obrázkami, na čo môžeme použiť strednú kvadratickú chybu (MSE). Pri segmentácii každý pixel v cieľovom obrázku masky predstavuje číslo triedy (one-hot-enkódované pozdĺž tretej dimenzie), takže musíme použiť stratové funkcie špecifické pre klasifikáciu - krížovú entropiu, spriemerovanú cez všetky pixely. Ak je maska binárna, používa sa **binárna krížová entropia** (BCE).

> ✅ One-hot enkódovanie je spôsob, ako zakódovať triedu do vektora s dĺžkou rovnou počtu tried. Pozrite si [tento článok](https://datagy.io/sklearn-one-hot-encode/) o tejto technike.

## Segmentácia v medicínskom zobrazovaní

V tejto lekcii uvidíme segmentáciu v praxi tým, že natrénujeme sieť na rozpoznávanie ľudských névov (známych aj ako znamienka) na medicínskych obrázkoch. Budeme používať <a href="https://www.fc.up.pt/addi/ph2%20database.html">PH<sup>2</sup> databázu</a> dermoskopických obrázkov ako zdroj obrázkov. Táto databáza obsahuje 200 obrázkov troch tried: typický névus, atypický névus a melanóm. Všetky obrázky obsahujú aj zodpovedajúcu **masku**, ktorá ohraničuje névus.

> ✅ Táto technika je obzvlášť vhodná pre tento typ medicínskeho zobrazovania, ale aké ďalšie reálne aplikácie si viete predstaviť?

<img alt="navi" src="images/navi.png"/>

> Obrázok z PH<sup>2</sup> databázy

Natrénujeme model na segmentáciu akéhokoľvek névusu z jeho pozadia.

## ✍️ Cvičenia: Semantická segmentácia

Otvorte nižšie uvedené notebooky, aby ste sa dozvedeli viac o rôznych architektúrach semantickej segmentácie, precvičili si prácu s nimi a videli ich v akcii.

* [Semantická segmentácia Pytorch](../../../../../lessons/4-ComputerVision/12-Segmentation/SemanticSegmentationPytorch.ipynb)
* [Semantická segmentácia TensorFlow](../../../../../lessons/4-ComputerVision/12-Segmentation/SemanticSegmentationTF.ipynb)

## [Kvíz po prednáške](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/212)

## Záver

Segmentácia je veľmi silná technika pre klasifikáciu obrázkov, ktorá ide nad rámec ohraničujúcich boxov až po klasifikáciu na úrovni pixelov. Táto technika sa používa v medicínskom zobrazovaní a v mnohých ďalších aplikáciách.

## 🚀 Výzva

Segmentácia tela je len jednou z bežných úloh, ktoré môžeme vykonávať s obrázkami ľudí. Ďalšie dôležité úlohy zahŕňajú **detekciu kostry** a **detekciu póz**. Vyskúšajte knižnicu [OpenPose](https://github.com/CMU-Perceptual-Computing-Lab/openpose), aby ste videli, ako sa dá detekcia póz využiť.

## Prehľad a samostatné štúdium

Tento [článok na Wikipédii](https://wikipedia.org/wiki/Image_segmentation) ponúka dobrý prehľad o rôznych aplikáciách tejto techniky. Zistite viac o poddoménach inštančnej segmentácie a panoptickej segmentácie v tejto oblasti výskumu.

## [Úloha](lab/README.md)

V tomto laboratóriu si vyskúšajte **segmentáciu ľudského tela** pomocou [Segmentation Full Body MADS Dataset](https://www.kaggle.com/datasets/tapakah68/segmentation-full-body-mads-dataset) z Kaggle.

**Zrieknutie sa zodpovednosti**:  
Tento dokument bol preložený pomocou služby AI prekladu [Co-op Translator](https://github.com/Azure/co-op-translator). Hoci sa snažíme o presnosť, prosím, berte na vedomie, že automatizované preklady môžu obsahovať chyby alebo nepresnosti. Pôvodný dokument v jeho rodnom jazyku by mal byť považovaný za autoritatívny zdroj. Pre kritické informácie sa odporúča profesionálny ľudský preklad. Nie sme zodpovední za akékoľvek nedorozumenia alebo nesprávne interpretácie vyplývajúce z použitia tohto prekladu.