<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "d76a7eda28de5210c8b1ba50a6216c69",
  "translation_date": "2025-09-23T06:42:40+00:00",
  "source_file": "lessons/4-ComputerVision/11-ObjectDetection/README.md",
  "language_code": "ur"
}
-->
# آبجیکٹ ڈیٹیکشن

اب تک ہم نے جو امیج کلاسیفیکیشن ماڈلز دیکھے ہیں، وہ ایک تصویر لیتے ہیں اور ایک کیٹیگریکل نتیجہ دیتے ہیں، جیسے MNIST مسئلے میں کلاس 'نمبر'۔ لیکن اکثر ہمیں صرف یہ جاننا نہیں ہوتا کہ تصویر میں اشیاء موجود ہیں، بلکہ ہم ان کی درست جگہ کا تعین کرنا چاہتے ہیں۔ یہی **آبجیکٹ ڈیٹیکشن** کا مقصد ہے۔

## [لیکچر سے پہلے کا کوئز](https://ff-quizzes.netlify.app/en/ai/quiz/21)

![آبجیکٹ ڈیٹیکشن](../../../../../translated_images/Screen_Shot_2016-11-17_at_11.14.54_AM.b4bb3769353287be1b905373ed9c858102c054b16e4595c76ec3f7bba0feb549.ur.png)

> تصویر [YOLO v2 ویب سائٹ](https://pjreddie.com/darknet/yolov2/) سے لی گئی ہے۔

## آبجیکٹ ڈیٹیکشن کے لیے ایک سادہ طریقہ

فرض کریں کہ ہم تصویر میں ایک بلی تلاش کرنا چاہتے ہیں، تو آبجیکٹ ڈیٹیکشن کے لیے ایک سادہ طریقہ یہ ہو سکتا ہے:

1. تصویر کو کئی چھوٹے حصوں میں تقسیم کریں۔
2. ہر حصے پر امیج کلاسیفیکیشن چلائیں۔
3. وہ حصے جن میں کافی زیادہ ایکٹیویشن ہو، انہیں مطلوبہ آبجیکٹ کے حامل سمجھا جا سکتا ہے۔

![سادہ آبجیکٹ ڈیٹیکشن](../../../../../translated_images/naive-detection.e7f1ba220ccd08c68a2ea8e06a7ed75c3fcc738c2372f9e00b7f4299a8659c01.ur.png)

> *تصویر [ایکسسرسائز نوٹ بک](ObjectDetection-TF.ipynb) سے لی گئی ہے۔*

لیکن یہ طریقہ مثالی نہیں ہے، کیونکہ یہ آبجیکٹ کے باؤنڈنگ باکس کو بہت غیر درست طریقے سے ظاہر کرتا ہے۔ زیادہ درست جگہ کے لیے ہمیں **ریگریشن** کا استعمال کرنا ہوگا تاکہ باؤنڈنگ باکس کے کوآرڈینیٹس کی پیش گوئی کی جا سکے - اور اس کے لیے مخصوص ڈیٹاسیٹس کی ضرورت ہوتی ہے۔

## آبجیکٹ ڈیٹیکشن کے لیے ریگریشن

[یہ بلاگ پوسٹ](https://towardsdatascience.com/object-detection-with-neural-networks-a4e2c46b4491) شکلوں کی شناخت کے لیے ایک بہترین تعارف فراہم کرتی ہے۔

## آبجیکٹ ڈیٹیکشن کے لیے ڈیٹاسیٹس

آپ درج ذیل ڈیٹاسیٹس کا سامنا کر سکتے ہیں:

* [PASCAL VOC](http://host.robots.ox.ac.uk/pascal/VOC/) - 20 کلاسز
* [COCO](http://cocodataset.org/#home) - عام اشیاء کے سیاق و سباق میں۔ 80 کلاسز، باؤنڈنگ باکسز اور سیگمنٹیشن ماسکس

![COCO](../../../../../translated_images/coco-examples.71bc60380fa6cceb7caad48bd09e35b6028caabd363aa04fee89c414e0870e86.ur.jpg)

## آبجیکٹ ڈیٹیکشن میٹرکس

### انٹرسیکشن اوور یونین

امیج کلاسیفیکیشن کے لیے یہ آسان ہے کہ ہم الگورتھم کی کارکردگی کو ماپ سکیں، لیکن آبجیکٹ ڈیٹیکشن کے لیے ہمیں کلاس کی درستگی کے ساتھ ساتھ باؤنڈنگ باکس کی پیش گوئی کی درستگی کو بھی ماپنا ہوتا ہے۔ اس کے لیے ہم **انٹرسیکشن اوور یونین** (IoU) استعمال کرتے ہیں، جو دو باکسز (یا دو کسی بھی علاقے) کے اوورلیپ کو ماپتا ہے۔

![IoU](../../../../../translated_images/iou_equation.9a4751d40fff4e119ecd0a7bcca4e71ab1dc83e0d4f2a0d66ff0859736f593cf.ur.png)

> *تصویر 2 [اس بہترین بلاگ پوسٹ](https://pyimagesearch.com/2016/11/07/intersection-over-union-iou-for-object-detection/) سے لی گئی ہے۔*

خیال سادہ ہے - ہم دو شکلوں کے درمیان انٹرسیکشن کے علاقے کو ان کے یونین کے علاقے سے تقسیم کرتے ہیں۔ دو ایک جیسے علاقوں کے لیے IoU 1 ہوگا، جبکہ مکمل طور پر الگ الگ علاقوں کے لیے یہ 0 ہوگا۔ ورنہ یہ 0 سے 1 کے درمیان ہوگا۔ ہم عام طور پر صرف ان باؤنڈنگ باکسز کو دیکھتے ہیں جن کے IoU ایک خاص قدر سے زیادہ ہو۔

### ایوریج پریسیژن

فرض کریں کہ ہم کسی دی گئی کلاس $C$ کی شناخت کی کارکردگی کو ماپنا چاہتے ہیں۔ اس کے لیے ہم **ایوریج پریسیژن** میٹرکس استعمال کرتے ہیں، جو درج ذیل طریقے سے حساب کی جاتی ہے:

1. پریسیژن-ریکال گراف دکھاتا ہے کہ ڈیٹیکشن تھریشولڈ ویلیو (0 سے 1 تک) کے مطابق درستگی کیسے تبدیل ہوتی ہے۔
2. تھریشولڈ کے مطابق، ہمیں تصویر میں زیادہ یا کم اشیاء ملیں گی، اور پریسیژن اور ریکال کی مختلف قدریں ہوں گی۔
3. گراف کچھ اس طرح نظر آئے گا:

<img src="https://github.com/shwars/NeuroWorkshop/raw/master/images/ObjDetectionPrecisionRecall.png"/>

> *تصویر [NeuroWorkshop](http://github.com/shwars/NeuroWorkshop) سے لی گئی ہے۔*

دی گئی کلاس $C$ کے لیے ایوریج پریسیژن اس گراف کے نیچے کے علاقے کے برابر ہے۔ زیادہ تفصیل سے، ریکال محور کو عام طور پر 10 حصوں میں تقسیم کیا جاتا ہے، اور پریسیژن کو ان تمام پوائنٹس پر اوسطاً لیا جاتا ہے:

$$
AP = {1\over11}\sum_{i=0}^{10}\mbox{Precision}(\mbox{Recall}={i\over10})
$$

### AP اور IoU

ہم صرف ان ڈیٹیکشنز کو دیکھیں گے جن کے IoU ایک خاص قدر سے زیادہ ہو۔ مثال کے طور پر، PASCAL VOC ڈیٹاسیٹ میں عام طور پر $\mbox{IoU Threshold} = 0.5$ فرض کیا جاتا ہے، جبکہ COCO میں AP مختلف $\mbox{IoU Threshold}$ قدروں کے لیے ماپا جاتا ہے۔

<img src="https://github.com/shwars/NeuroWorkshop/raw/master/images/ObjDetectionPrecisionRecallIoU.png"/>

> *تصویر [NeuroWorkshop](http://github.com/shwars/NeuroWorkshop) سے لی گئی ہے۔*

### مین ایوریج پریسیژن - mAP

آبجیکٹ ڈیٹیکشن کے لیے اہم میٹرک **مین ایوریج پریسیژن** یا **mAP** کہلاتا ہے۔ یہ ایوریج پریسیژن کی قدر ہے، جو تمام آبجیکٹ کلاسز پر اوسطاً لی جاتی ہے، اور کبھی کبھار $\mbox{IoU Threshold}$ پر بھی۔ زیادہ تفصیل سے، **mAP** کا حساب لگانے کا عمل
[اس بلاگ پوسٹ](https://medium.com/@timothycarlen/understanding-the-map-evaluation-metric-for-object-detection-a07fe6962cf3) میں بیان کیا گیا ہے، اور [یہاں کوڈ نمونوں کے ساتھ](https://gist.github.com/tarlen5/008809c3decf19313de216b9208f3734) بھی۔

## مختلف آبجیکٹ ڈیٹیکشن کے طریقے

آبجیکٹ ڈیٹیکشن الگورتھمز کی دو بڑی اقسام ہیں:

* **ریجن پروپوزل نیٹ ورکس** (R-CNN، فاسٹ R-CNN، فاسٹر R-CNN)۔ بنیادی خیال یہ ہے کہ **ریجنز آف انٹرسٹ** (ROI) بنائیں اور ان پر CNN چلائیں، زیادہ سے زیادہ ایکٹیویشن تلاش کرنے کے لیے۔ یہ سادہ طریقے سے ملتا جلتا ہے، سوائے اس کے کہ ROI زیادہ ذہین طریقے سے بنائے جاتے ہیں۔ ایسے طریقوں کا ایک بڑا نقصان یہ ہے کہ یہ سست ہیں، کیونکہ ہمیں تصویر پر CNN کلاسیفائر کے کئی پاسز کی ضرورت ہوتی ہے۔
* **ون پاس** (YOLO، SSD، RetinaNet) طریقے۔ ان آرکیٹیکچرز میں ہم نیٹ ورک کو اس طرح ڈیزائن کرتے ہیں کہ وہ ایک ہی پاس میں کلاسز اور ROI کی پیش گوئی کرے۔

### R-CNN: ریجن بیسڈ CNN

[R-CNN](http://islab.ulsan.ac.kr/files/announcement/513/rcnn_pami.pdf) [سیلیکٹیو سرچ](http://www.huppelen.nl/publications/selectiveSearchDraft.pdf) استعمال کرتا ہے تاکہ ROI ریجنز کی ہائیرارکل ساخت بنائی جا سکے، جنہیں پھر CNN فیچر ایکسٹریکٹرز اور SVM کلاسیفائرز کے ذریعے آبجیکٹ کلاس کا تعین کرنے کے لیے پاس کیا جاتا ہے، اور *باؤنڈنگ باکس* کے کوآرڈینیٹس کا تعین کرنے کے لیے لینیئر ریگریشن استعمال کی جاتی ہے۔ [آفیشل پیپر](https://arxiv.org/pdf/1506.01497v1.pdf)

![RCNN](../../../../../translated_images/rcnn1.cae407020dfb1d1fb572656e44f75cd6c512cc220591c116c506652c10e47f26.ur.png)

> *تصویر van de Sande et al. ICCV’11 سے لی گئی ہے۔*

![RCNN-1](../../../../../translated_images/rcnn2.2d9530bb83516484ec65b250c22dbf37d3d23244f32864ebcb91d98fe7c3112c.ur.png)

> *تصاویر [اس بلاگ](https://towardsdatascience.com/r-cnn-fast-r-cnn-faster-r-cnn-yolo-object-detection-algorithms-36d53571365e) سے لی گئی ہیں۔*

### F-RCNN - فاسٹ R-CNN

یہ طریقہ R-CNN سے ملتا جلتا ہے، لیکن ریجنز کنوولوشن لیئرز کے بعد ڈیفائن کیے جاتے ہیں۔

![FRCNN](../../../../../translated_images/f-rcnn.3cda6d9bb41888754037d2d9763e2298a96de5d9bc2a21db3147357aa5da9b1a.ur.png)

> تصویر [آفیشل پیپر](https://www.cv-foundation.org/openaccess/content_iccv_2015/papers/Girshick_Fast_R-CNN_ICCV_2015_paper.pdf)، [arXiv](https://arxiv.org/pdf/1504.08083.pdf)، 2015 سے لی گئی ہے۔

### فاسٹر R-CNN

اس طریقے کا بنیادی خیال یہ ہے کہ ریجنز کی پیش گوئی کے لیے نیورل نیٹ ورک استعمال کیا جائے - جسے *ریجن پروپوزل نیٹ ورک* کہا جاتا ہے۔ [پیپر](https://arxiv.org/pdf/1506.01497.pdf)، 2016

![FasterRCNN](../../../../../translated_images/faster-rcnn.8d46c099b87ef30ab2ea26dbc4bdd85b974a57ba8eb526f65dc4cd0a4711de30.ur.png)

> تصویر [آفیشل پیپر](https://arxiv.org/pdf/1506.01497.pdf) سے لی گئی ہے۔

### R-FCN: ریجن بیسڈ فل کنوولوشنل نیٹ ورک

یہ الگورتھم فاسٹر R-CNN سے بھی زیادہ تیز ہے۔ بنیادی خیال درج ذیل ہے:

1. ہم ResNet-101 استعمال کرتے ہوئے فیچرز نکالتے ہیں۔
1. فیچرز **پوزیشن سینسیٹو اسکور میپ** کے ذریعے پروسیس کیے جاتے ہیں۔ $C$ کلاسز کے ہر آبجیکٹ کو $k\times k$ ریجنز میں تقسیم کیا جاتا ہے، اور ہم آبجیکٹس کے حصے پیش گوئی کرنے کی تربیت کرتے ہیں۔
1. $k\times k$ ریجنز کے ہر حصے کے لیے تمام نیٹ ورکس آبجیکٹ کلاسز کے لیے ووٹ دیتے ہیں، اور زیادہ سے زیادہ ووٹ کے ساتھ آبجیکٹ کلاس منتخب کی جاتی ہے۔

![r-fcn image](../../../../../translated_images/r-fcn.13eb88158b99a3da50fa2787a6be5cb310d47f0e9655cc93a1090dc7aab338d1.ur.png)

> تصویر [آفیشل پیپر](https://arxiv.org/abs/1605.06409) سے لی گئی ہے۔

### YOLO - یو اونلی لک ونس

YOLO ایک ریئل ٹائم ون پاس الگورتھم ہے۔ بنیادی خیال درج ذیل ہے:

 * تصویر کو $S\times S$ ریجنز میں تقسیم کیا جاتا ہے۔
 * ہر ریجن کے لیے، **CNN** $n$ ممکنہ آبجیکٹس، *باؤنڈنگ باکس* کے کوآرڈینیٹس اور *کانفیڈنس*=*پروببلیٹی* * IoU کی پیش گوئی کرتا ہے۔

 ![YOLO](../../../../../translated_images/yolo.a2648ec82ee8bb4ea27537677adb482fd4b733ca1705c561b6a24a85102dced5.ur.png)

> تصویر [آفیشل پیپر](https://arxiv.org/abs/1506.02640) سے لی گئی ہے۔

### دیگر الگورتھمز

* RetinaNet: [آفیشل پیپر](https://arxiv.org/abs/1708.02002)
   - [Torchvision میں PyTorch امپلیمنٹیشن](https://pytorch.org/vision/stable/_modules/torchvision/models/detection/retinanet.html)
   - [Keras امپلیمنٹیشن](https://github.com/fizyr/keras-retinanet)
   - [Keras Samples میں RetinaNet کے ساتھ آبجیکٹ ڈیٹیکشن](https://keras.io/examples/vision/retinanet/)
* SSD (سنگل شاٹ ڈیٹیکٹر): [آفیشل پیپر](https://arxiv.org/abs/1512.02325)

## ✍️ مشقیں: آبجیکٹ ڈیٹیکشن

اپنی تعلیم کو درج ذیل نوٹ بک میں جاری رکھیں:

[ObjectDetection.ipynb](ObjectDetection.ipynb)

## نتیجہ

اس سبق میں آپ نے آبجیکٹ ڈیٹیکشن کے مختلف طریقوں کا ایک مختصر جائزہ لیا!

## 🚀 چیلنج

ان مضامین اور نوٹ بکس کو پڑھیں جو YOLO کے بارے میں ہیں اور انہیں خود آزمائیں:

* [YOLO کے بارے میں ایک اچھا بلاگ پوسٹ](https://www.analyticsvidhya.com/blog/2018/12/practical-guide-object-detection-yolo-framewor-python/)
 * [آفیشل سائٹ](https://pjreddie.com/darknet/yolo/)
 * YOLO: [Keras امپلیمنٹیشن](https://github.com/experiencor/keras-yolo2)، [اسٹیپ بائی اسٹیپ نوٹ بک](https://github.com/experiencor/basic-yolo-keras/blob/master/Yolo%20Step-by-Step.ipynb)
 * YOLO v2: [Keras امپلیمنٹیشن](https://github.com/experiencor/keras-yolo2)، [اسٹیپ بائی اسٹیپ نوٹ بک](https://github.com/experiencor/keras-yolo2/blob/master/Yolo%20Step-by-Step.ipynb)

## [لیکچر کے بعد کا کوئز](https://ff-quizzes.netlify.app/en/ai/quiz/22)

## جائزہ اور خود مطالعہ

* [آبجیکٹ ڈیٹیکشن](https://tjmachinelearning.com/lectures/1718/obj/) از نکھل سردانا
* [آبجیکٹ ڈیٹیکشن الگورتھمز کا ایک اچھا موازنہ](https://lilianweng.github.io/lil-log/2018/12/27/object-detection-part-4.html)
* [آبجیکٹ ڈیٹیکشن کے لیے ڈیپ لرننگ الگورتھمز کا جائزہ](https://medium.com/comet-app/review-of-deep-learning-algorithms-for-object-detection-c1f3d437b852)
* [آبجیکٹ ڈیٹیکشن الگورتھمز کا ایک مرحلہ وار تعارف](https://www.analyticsvidhya.com/blog/2018/10/a-step-by-step-introduction-to-the-basic-object-detection-algorithms-part-1/)
* [Python میں فاسٹر R-CNN کے ساتھ آبجیکٹ ڈیٹیکشن کا امپلیمنٹیشن](https://www.analyticsvidhya.com/blog/2018/11/implementation-faster-r-cnn-python-object-detection/)

## [اسائنمنٹ: آبجیکٹ ڈیٹیکشن](lab/README.md)

---

