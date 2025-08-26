<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "d85c8b08f6d1b48fd7f35b99f93c1138",
  "translation_date": "2025-08-25T22:44:18+00:00",
  "source_file": "lessons/4-ComputerVision/11-ObjectDetection/README.md",
  "language_code": "sk"
}
-->
# Detekcia objektov

Modely klasifikácie obrázkov, s ktorými sme sa doteraz zaoberali, brali obrázok a produkovali kategóriálny výsledok, ako napríklad triedu 'číslo' v probléme MNIST. Avšak v mnohých prípadoch nechceme len vedieť, že obrázok zobrazuje objekty – chceme byť schopní určiť ich presnú polohu. Toto je presne cieľom **detekcie objektov**.

## [Pre-quiz pred prednáškou](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/111)

![Detekcia objektov](../../../../../translated_images/Screen_Shot_2016-11-17_at_11.14.54_AM.b4bb3769353287be1b905373ed9c858102c054b16e4595c76ec3f7bba0feb549.sk.png)

> Obrázok z [webovej stránky YOLO v2](https://pjreddie.com/darknet/yolov2/)

## Naivný prístup k detekcii objektov

Predpokladajme, že chceme nájsť mačku na obrázku. Veľmi naivný prístup k detekcii objektov by bol nasledovný:

1. Rozdeliť obrázok na množstvo dlaždíc.
2. Spustiť klasifikáciu obrázkov na každej dlaždici.
3. Dlaždice, ktoré majú dostatočne vysokú aktiváciu, môžeme považovať za obsahujúce hľadaný objekt.

![Naivná detekcia objektov](../../../../../translated_images/naive-detection.e7f1ba220ccd08c68a2ea8e06a7ed75c3fcc738c2372f9e00b7f4299a8659c01.sk.png)

> *Obrázok z [cvičebného notebooku](../../../../../lessons/4-ComputerVision/11-ObjectDetection/ObjectDetection-TF.ipynb)*

Tento prístup však nie je ideálny, pretože umožňuje algoritmu lokalizovať ohraničujúci rámec objektu veľmi nepresne. Pre presnejšiu lokalizáciu potrebujeme spustiť určitý typ **regresie**, aby sme predpovedali súradnice ohraničujúcich rámcov – a na to potrebujeme špecifické datasety.

## Regresia pre detekciu objektov

[Tento blogový príspevok](https://towardsdatascience.com/object-detection-with-neural-networks-a4e2c46b4491) ponúka skvelý úvod do detekcie tvarov.

## Datasety pre detekciu objektov

Pri tejto úlohe sa môžete stretnúť s nasledujúcimi datasetmi:

* [PASCAL VOC](http://host.robots.ox.ac.uk/pascal/VOC/) – 20 tried
* [COCO](http://cocodataset.org/#home) – Common Objects in Context. 80 tried, ohraničujúce rámce a segmentačné masky

![COCO](../../../../../translated_images/coco-examples.71bc60380fa6cceb7caad48bd09e35b6028caabd363aa04fee89c414e0870e86.sk.jpg)

## Metriky detekcie objektov

### Prienik cez zjednotenie (Intersection over Union)

Zatiaľ čo pri klasifikácii obrázkov je jednoduché merať, ako dobre algoritmus funguje, pri detekcii objektov musíme merať správnosť triedy, ako aj presnosť lokalizácie predpokladaného ohraničujúceho rámca. Na tento účel používame tzv. **Prienik cez zjednotenie** (IoU), ktorý meria, ako dobre sa dva rámce (alebo dve ľubovoľné oblasti) prekrývajú.

![IoU](../../../../../translated_images/iou_equation.9a4751d40fff4e119ecd0a7bcca4e71ab1dc83e0d4f2a0d66ff0859736f593cf.sk.png)

> *Obrázok 2 z [tohto výborného blogového príspevku o IoU](https://pyimagesearch.com/2016/11/07/intersection-over-union-iou-for-object-detection/)*

Myšlienka je jednoduchá – vydelíme plochu prieniku medzi dvoma útvarmi plochou ich zjednotenia. Pre dve identické oblasti by IoU bolo 1, zatiaľ čo pre úplne oddelené oblasti bude 0. Inak sa bude pohybovať od 0 do 1. Typicky berieme do úvahy iba tie ohraničujúce rámce, pre ktoré je IoU nad určitú hodnotu.

### Priemerná presnosť (Average Precision)

Predpokladajme, že chceme merať, ako dobre je rozpoznaná daná trieda objektov $C$. Na jej meranie používame metriku **Priemerná presnosť**, ktorá sa vypočíta nasledovne:

1. Zvážime krivku presnosti a odvolania, ktorá ukazuje presnosť v závislosti od hodnoty prahu detekcie (od 0 do 1).
2. V závislosti od prahu získame viac alebo menej detekovaných objektov na obrázku a rôzne hodnoty presnosti a odvolania.
3. Krivka bude vyzerať takto:

<img src="https://github.com/shwars/NeuroWorkshop/raw/master/images/ObjDetectionPrecisionRecall.png"/>

> *Obrázok z [NeuroWorkshop](http://github.com/shwars/NeuroWorkshop)*

Priemerná presnosť pre danú triedu $C$ je plocha pod touto krivkou. Presnejšie, os odvolania je typicky rozdelená na 10 častí a presnosť sa spriemeruje cez všetky tieto body:

$$
AP = {1\over11}\sum_{i=0}^{10}\mbox{Precision}(\mbox{Recall}={i\over10})
$$

### AP a IoU

Zvážime iba tie detekcie, pre ktoré je IoU nad určitú hodnotu. Napríklad v datasete PASCAL VOC sa typicky predpokladá $\mbox{IoU Threshold} = 0.5$, zatiaľ čo v COCO sa AP meria pre rôzne hodnoty $\mbox{IoU Threshold}$.

<img src="https://github.com/shwars/NeuroWorkshop/raw/master/images/ObjDetectionPrecisionRecallIoU.png"/>

> *Obrázok z [NeuroWorkshop](http://github.com/shwars/NeuroWorkshop)*

### Priemerná priemerná presnosť – mAP

Hlavná metrika pre detekciu objektov sa nazýva **Priemerná priemerná presnosť**, alebo **mAP**. Je to hodnota Priemernej presnosti, spriemerovaná cez všetky triedy objektov, a niekedy aj cez $\mbox{IoU Threshold}$. Podrobnejší proces výpočtu **mAP** je opísaný
[v tomto blogovom príspevku](https://medium.com/@timothycarlen/understanding-the-map-evaluation-metric-for-object-detection-a07fe6962cf3)), a tiež [tu s ukážkami kódu](https://gist.github.com/tarlen5/008809c3decf19313de216b9208f3734).

## Rôzne prístupy k detekcii objektov

Existujú dve široké kategórie algoritmov detekcie objektov:

* **Siete na návrh regiónov** (R-CNN, Fast R-CNN, Faster R-CNN). Hlavná myšlienka je generovať **Regióny záujmu** (ROI) a spustiť CNN nad nimi, hľadajúc maximálnu aktiváciu. Je to trochu podobné naivnému prístupu, s výnimkou toho, že ROI sú generované inteligentnejším spôsobom. Jednou z hlavných nevýhod takýchto metód je, že sú pomalé, pretože potrebujeme mnoho prechodov CNN klasifikátora cez obrázok.
* **Jednoprechodové** (YOLO, SSD, RetinaNet) metódy. V týchto architektúrach navrhujeme sieť tak, aby predpovedala triedy aj ROI v jednom prechode.

### R-CNN: CNN založené na regiónoch

[R-CNN](http://islab.ulsan.ac.kr/files/announcement/513/rcnn_pami.pdf) používa [Selektívne vyhľadávanie](http://www.huppelen.nl/publications/selectiveSearchDraft.pdf) na generovanie hierarchickej štruktúry ROI regiónov, ktoré sú potom prechádzané extraktormi funkcií CNN a SVM klasifikátormi na určenie triedy objektu, a lineárnou regresiou na určenie súradníc *ohraničujúceho rámca*. [Oficiálny článok](https://arxiv.org/pdf/1506.01497v1.pdf)

![RCNN](../../../../../translated_images/rcnn1.cae407020dfb1d1fb572656e44f75cd6c512cc220591c116c506652c10e47f26.sk.png)

> *Obrázok od van de Sande et al. ICCV’11*

![RCNN-1](../../../../../translated_images/rcnn2.2d9530bb83516484ec65b250c22dbf37d3d23244f32864ebcb91d98fe7c3112c.sk.png)

> *Obrázky z [tohto blogu](https://towardsdatascience.com/r-cnn-fast-r-cnn-faster-r-cnn-yolo-object-detection-algorithms-36d53571365e)*

### F-RCNN – Rýchle R-CNN

Tento prístup je podobný R-CNN, ale regióny sú definované po aplikovaní konvolučných vrstiev.

![FRCNN](../../../../../translated_images/f-rcnn.3cda6d9bb41888754037d2d9763e2298a96de5d9bc2a21db3147357aa5da9b1a.sk.png)

> Obrázok z [oficiálneho článku](https://www.cv-foundation.org/openaccess/content_iccv_2015/papers/Girshick_Fast_R-CNN_ICCV_2015_paper.pdf), [arXiv](https://arxiv.org/pdf/1504.08083.pdf), 2015

### Faster R-CNN

Hlavná myšlienka tohto prístupu je použiť neurónovú sieť na predpovedanie ROI – tzv. *Sieť na návrh regiónov*. [Článok](https://arxiv.org/pdf/1506.01497.pdf), 2016

![FasterRCNN](../../../../../translated_images/faster-rcnn.8d46c099b87ef30ab2ea26dbc4bdd85b974a57ba8eb526f65dc4cd0a4711de30.sk.png)

> Obrázok z [oficiálneho článku](https://arxiv.org/pdf/1506.01497.pdf)

### R-FCN: Plne konvolučná sieť založená na regiónoch

Tento algoritmus je ešte rýchlejší ako Faster R-CNN. Hlavná myšlienka je nasledovná:

1. Extrahujeme funkcie pomocou ResNet-101.
2. Funkcie sú spracované **Mapou skóre citlivou na polohu**. Každý objekt z $C$ tried je rozdelený na $k\times k$ regióny, a trénujeme na predpovedanie častí objektov.
3. Pre každú časť z $k\times k$ regiónov všetky siete hlasujú za triedy objektov, a trieda objektu s maximálnym počtom hlasov je vybraná.

![r-fcn image](../../../../../translated_images/r-fcn.13eb88158b99a3da50fa2787a6be5cb310d47f0e9655cc93a1090dc7aab338d1.sk.png)

> Obrázok z [oficiálneho článku](https://arxiv.org/abs/1605.06409)

### YOLO – You Only Look Once

YOLO je algoritmus na jednoprechodovú detekciu v reálnom čase. Hlavná myšlienka je nasledovná:

 * Obrázok je rozdelený na $S\times S$ regióny.
 * Pre každý región **CNN** predpovedá $n$ možných objektov, súradnice *ohraničujúceho rámca* a *dôveru*=*pravdepodobnosť* * IoU.

 ![YOLO](../../../../../translated_images/yolo.a2648ec82ee8bb4ea27537677adb482fd4b733ca1705c561b6a24a85102dced5.sk.png)

> Obrázok z [oficiálneho článku](https://arxiv.org/abs/1506.02640)

### Ďalšie algoritmy

* RetinaNet: [oficiálny článok](https://arxiv.org/abs/1708.02002)
   - [Implementácia v PyTorch](https://pytorch.org/vision/stable/_modules/torchvision/models/detection/retinanet.html)
   - [Implementácia v Keras](https://github.com/fizyr/keras-retinanet)
   - [Detekcia objektov pomocou RetinaNet](https://keras.io/examples/vision/retinanet/) v ukážkach Keras
* SSD (Single Shot Detector): [oficiálny článok](https://arxiv.org/abs/1512.02325)

## ✍️ Cvičenia: Detekcia objektov

Pokračujte vo svojom učení v nasledujúcom notebooku:

[ObjectDetection.ipynb](../../../../../lessons/4-ComputerVision/11-ObjectDetection/ObjectDetection.ipynb)

## Záver

V tejto lekcii ste si urobili rýchly prehľad o rôznych spôsoboch, ako je možné dosiahnuť detekciu objektov!

## 🚀 Výzva

Prečítajte si tieto články a notebooky o YOLO a vyskúšajte ich sami:

* [Dobrý blogový príspevok](https://www.analyticsvidhya.com/blog/2018/12/practical-guide-object-detection-yolo-framewor-python/) popisujúci YOLO
 * [Oficiálna stránka](https://pjreddie.com/darknet/yolo/)
 * Yolo: [Implementácia v Keras](https://github.com/experiencor/keras-yolo2), [krok-za-krokom notebook](https://github.com/experiencor/basic-yolo-keras/blob/master/Yolo%20Step-by-Step.ipynb)
 * Yolo v2: [Implementácia v Keras](https://github.com/experiencor/keras-yolo2), [krok-za-krokom notebook](https://github.com/experiencor/keras-yolo2/blob/master/Yolo%20Step-by-Step.ipynb)

## [Post-quiz po prednáške](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/211)

## Prehľad a samostatné štúdium

* [Detekcia objektov](https://tjmachinelearning.com/lectures/1718/obj/) od Nikhila Sardanu
* [Dobrý porovnávací článok o algoritmoch detekcie objektov](https://lilianweng.github.io/lil-log/2018/12/27/object-detection-part-4.html)
* [Prehľad algoritmov hlbokého učenia pre detekciu objektov](https://medium.com/comet-app/review-of-deep-learning-algorithms-for-object-detection-c1f3d437b852)
* [Krok-za-krokom úvod do základných algoritmov detekcie objektov](https://www.analyticsvidhya.com/blog/2018/10/a-step-by-step-introduction-to-the-basic-object-detection-algorithms-part-1/)
* [Implementácia Faster R-CNN v Pythone pre detekciu objektov](https://www.analyticsvidhya.com/blog/2018/11/implementation-faster-r-cnn-python-object-detection/)

## [Úloha: Detekcia objektov](lab/README.md)

**Upozornenie**:  
Tento dokument bol preložený pomocou služby AI prekladu [Co-op Translator](https://github.com/Azure/co-op-translator). Hoci sa snažíme o presnosť, prosím, berte na vedomie, že automatizované preklady môžu obsahovať chyby alebo nepresnosti. Pôvodný dokument v jeho rodnom jazyku by mal byť považovaný za autoritatívny zdroj. Pre kritické informácie sa odporúča profesionálny ľudský preklad. Nie sme zodpovední za žiadne nedorozumenia alebo nesprávne interpretácie vyplývajúce z použitia tohto prekladu.