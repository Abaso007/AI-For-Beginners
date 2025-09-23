<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "d85c8b08f6d1b48fd7f35b99f93c1138",
  "translation_date": "2025-08-26T09:21:27+00:00",
  "source_file": "lessons/4-ComputerVision/11-ObjectDetection/README.md",
  "language_code": "mr"
}
-->
# ऑब्जेक्ट डिटेक्शन

आतापर्यंत आपण ज्या इमेज क्लासिफिकेशन मॉडेल्सचा अभ्यास केला आहे, ते एका इमेजवर प्रक्रिया करून एक वर्गीकृत परिणाम देतात, जसे की MNIST समस्येमध्ये 'संख्या' वर्ग. परंतु, अनेक वेळा आपल्याला फक्त हे जाणून घ्यायचे नसते की एखाद्या चित्रात वस्तू आहेत, तर आपल्याला त्यांच्या अचूक स्थानाचा अंदाज लावायचा असतो. **ऑब्जेक्ट डिटेक्शन** याच उद्देशासाठी आहे.

## [पूर्व-व्याख्यान प्रश्नमंजुषा](https://ff-quizzes.netlify.app/en/ai/quiz/21)

![ऑब्जेक्ट डिटेक्शन](../../../../../translated_images/Screen_Shot_2016-11-17_at_11.14.54_AM.b4bb3769353287be1b905373ed9c858102c054b16e4595c76ec3f7bba0feb549.mr.png)

> चित्र [YOLO v2 वेबसाइट](https://pjreddie.com/darknet/yolov2/) वरून

## ऑब्जेक्ट डिटेक्शनसाठी साधा दृष्टिकोन

समजा आपल्याला एखाद्या चित्रात मांजर शोधायची आहे, तर ऑब्जेक्ट डिटेक्शनसाठी एक साधा दृष्टिकोन असा असू शकतो:

1. चित्राला अनेक टाइल्समध्ये विभागा.
2. प्रत्येक टाइलवर इमेज क्लासिफिकेशन चालवा.
3. ज्या टाइल्समध्ये पुरेशी उच्च सक्रियता दिसून येते, त्या टाइल्समध्ये संबंधित वस्तू असल्याचे मानले जाऊ शकते.

![साधा ऑब्जेक्ट डिटेक्शन](../../../../../translated_images/naive-detection.e7f1ba220ccd08c68a2ea8e06a7ed75c3fcc738c2372f9e00b7f4299a8659c01.mr.png)

> *चित्र [व्यायाम नोटबुक](../../../../../lessons/4-ComputerVision/11-ObjectDetection/ObjectDetection-TF.ipynb) मधून*

तथापि, हा दृष्टिकोन आदर्श नाही, कारण तो वस्तूच्या बॉक्सचे स्थान अचूकपणे शोधण्यास सक्षम नाही. अधिक अचूक स्थानासाठी, आपल्याला **रेग्रेशन** वापरून बॉक्सचे समन्वय अंदाज लावावे लागतात - आणि त्यासाठी विशिष्ट डेटासेट्स आवश्यक असतात.

## ऑब्जेक्ट डिटेक्शनसाठी रेग्रेशन

[हा ब्लॉग पोस्ट](https://towardsdatascience.com/object-detection-with-neural-networks-a4e2c46b4491) आकार शोधण्यासाठी एक चांगली सुरुवात देते.

## ऑब्जेक्ट डिटेक्शनसाठी डेटासेट्स

या कार्यासाठी तुम्हाला खालील डेटासेट्स सापडू शकतात:

* [PASCAL VOC](http://host.robots.ox.ac.uk/pascal/VOC/) - 20 वर्ग
* [COCO](http://cocodataset.org/#home) - कॉमन ऑब्जेक्ट्स इन कॉन्टेक्स्ट. 80 वर्ग, बॉक्सेस आणि सेगमेंटेशन मास्क

![COCO](../../../../../translated_images/coco-examples.71bc60380fa6cceb7caad48bd09e35b6028caabd363aa04fee89c414e0870e86.mr.jpg)

## ऑब्जेक्ट डिटेक्शन मेट्रिक्स

### इंटरसेक्शन ओव्हर युनियन

इमेज क्लासिफिकेशनसाठी अल्गोरिदम किती चांगले कार्य करते हे मोजणे सोपे आहे, परंतु ऑब्जेक्ट डिटेक्शनसाठी वर्गाची अचूकता आणि बॉक्सच्या स्थानाची अचूकता दोन्ही मोजणे आवश्यक आहे. यासाठी **इंटरसेक्शन ओव्हर युनियन** (IoU) वापरले जाते, जे दोन बॉक्सेस (किंवा दोन क्षेत्रे) किती चांगले ओव्हरलॅप होतात हे मोजते.

![IoU](../../../../../translated_images/iou_equation.9a4751d40fff4e119ecd0a7bcca4e71ab1dc83e0d4f2a0d66ff0859736f593cf.mr.png)

> *चित्र 2 [या उत्कृष्ट ब्लॉग पोस्टवरून IoU बद्दल](https://pyimagesearch.com/2016/11/07/intersection-over-union-iou-for-object-detection/)*

संकल्पना सोपी आहे - दोन आकृत्यांच्या ओव्हरलॅप क्षेत्राला त्यांच्या युनियन क्षेत्राने विभाजित करतो. दोन समान क्षेत्रांसाठी IoU 1 असेल, तर पूर्णपणे वेगळ्या क्षेत्रांसाठी ते 0 असेल. अन्यथा, ते 0 ते 1 दरम्यान बदलते. आम्ही सामान्यतः फक्त त्या बॉक्सेस विचारात घेतो ज्यांचे IoU विशिष्ट मूल्यापेक्षा जास्त असते.

### सरासरी अचूकता (Average Precision)

समजा आपल्याला एखाद्या वर्गातील वस्तू $C$ किती चांगल्या प्रकारे ओळखल्या जातात हे मोजायचे आहे. यासाठी **सरासरी अचूकता** मेट्रिक्स वापरली जाते, जी खालीलप्रमाणे गणना केली जाते:

1. प्रिसिजन-रिकॉल वक्र ओळख थ्रेशोल्ड मूल्यावर (0 ते 1 पर्यंत) अवलंबून अचूकता दर्शवते.
2. थ्रेशोल्डनुसार, आपल्याला चित्रात अधिक किंवा कमी वस्तू सापडतील, आणि प्रिसिजन व रिकॉलचे वेगवेगळे मूल्य मिळेल.
3. वक्र असे दिसेल:

<img src="https://github.com/shwars/NeuroWorkshop/raw/master/images/ObjDetectionPrecisionRecall.png"/>

> *चित्र [NeuroWorkshop](http://github.com/shwars/NeuroWorkshop) मधून*

वर्ग $C$ साठी सरासरी अचूकता म्हणजे या वक्राखालील क्षेत्र. अधिक अचूकपणे, रिकॉल अक्ष सामान्यतः 10 भागांमध्ये विभागली जाते, आणि प्रिसिजन सर्व त्या बिंदूंवर सरासरी केली जाते:

$$
AP = {1\over11}\sum_{i=0}^{10}\mbox{Precision}(\mbox{Recall}={i\over10})
$$

### AP आणि IoU

आम्ही फक्त त्या ओळखींवर विचार करू, ज्यांचे IoU विशिष्ट मूल्यापेक्षा जास्त आहे. उदाहरणार्थ, PASCAL VOC डेटासेटमध्ये सामान्यतः $\mbox{IoU Threshold} = 0.5$ मानले जाते, तर COCO मध्ये AP वेगवेगळ्या $\mbox{IoU Threshold}$ मूल्यांसाठी मोजले जाते.

<img src="https://github.com/shwars/NeuroWorkshop/raw/master/images/ObjDetectionPrecisionRecallIoU.png"/>

> *चित्र [NeuroWorkshop](http://github.com/shwars/NeuroWorkshop) मधून*

### सरासरी अचूकता - mAP

ऑब्जेक्ट डिटेक्शनसाठी मुख्य मेट्रिक **मीन अॅव्हरेज प्रिसिजन** किंवा **mAP** आहे. हे सर्व वर्गांसाठी सरासरी अचूकतेचे मूल्य आहे, आणि कधीकधी $\mbox{IoU Threshold}$ वर देखील सरासरी केली जाते. अधिक तपशीलवार, **mAP** कसे गणना करायचे याचे वर्णन [या ब्लॉग पोस्टमध्ये](https://medium.com/@timothycarlen/understanding-the-map-evaluation-metric-for-object-detection-a07fe6962cf3) केले आहे, आणि [इथे कोडसह](https://gist.github.com/tarlen5/008809c3decf19313de216b9208f3734) देखील.

## ऑब्जेक्ट डिटेक्शनसाठी विविध दृष्टिकोन

ऑब्जेक्ट डिटेक्शन अल्गोरिदम्सचे दोन मुख्य प्रकार आहेत:

* **Region Proposal Networks** (R-CNN, Fast R-CNN, Faster R-CNN). मुख्य कल्पना म्हणजे **Regions of Interests** (ROI) तयार करणे आणि त्यावर CNN चालवणे, जास्तीत जास्त सक्रियता शोधण्यासाठी. हे साध्या दृष्टिकोनासारखे आहे, परंतु ROIs अधिक हुशारीने तयार केले जातात. अशा पद्धतींचा मुख्य तोटा म्हणजे त्या हळू असतात, कारण चित्रावर CNN क्लासिफायरचे अनेक पासेस आवश्यक असतात.
* **One-pass** (YOLO, SSD, RetinaNet) पद्धती. या आर्किटेक्चरमध्ये वर्ग आणि ROIs एका पासमध्ये अंदाज लावण्यासाठी नेटवर्क डिझाइन केले जाते.

### R-CNN: Region-Based CNN

[R-CNN](http://islab.ulsan.ac.kr/files/announcement/513/rcnn_pami.pdf) [Selective Search](http://www.huppelen.nl/publications/selectiveSearchDraft.pdf) वापरते ROI क्षेत्रांची संरचना तयार करण्यासाठी, जी नंतर CNN फीचर एक्स्ट्रॅक्टर्स आणि SVM-क्लासिफायर्सद्वारे वस्तूचा वर्ग निश्चित करण्यासाठी आणि *बॉक्स* समन्वय निश्चित करण्यासाठी रेषीय रेग्रेशनद्वारे प्रक्रिया केली जाते. [अधिकृत पेपर](https://arxiv.org/pdf/1506.01497v1.pdf)

![RCNN](../../../../../translated_images/rcnn1.cae407020dfb1d1fb572656e44f75cd6c512cc220591c116c506652c10e47f26.mr.png)

> *चित्र van de Sande et al. ICCV’11*

![RCNN-1](../../../../../translated_images/rcnn2.2d9530bb83516484ec65b250c22dbf37d3d23244f32864ebcb91d98fe7c3112c.mr.png)

> *चित्र [या ब्लॉगमधून](https://towardsdatascience.com/r-cnn-fast-r-cnn-faster-r-cnn-yolo-object-detection-algorithms-36d53571365e)*

### F-RCNN - Fast R-CNN

हा दृष्टिकोन R-CNN सारखाच आहे, परंतु क्षेत्रे कॉन्व्होल्यूशन लेयर्स लागू केल्यानंतर निश्चित केली जातात.

![FRCNN](../../../../../translated_images/f-rcnn.3cda6d9bb41888754037d2d9763e2298a96de5d9bc2a21db3147357aa5da9b1a.mr.png)

> चित्र [अधिकृत पेपर](https://www.cv-foundation.org/openaccess/content_iccv_2015/papers/Girshick_Fast_R-CNN_ICCV_2015_paper.pdf), [arXiv](https://arxiv.org/pdf/1504.08083.pdf), 2015

### Faster R-CNN

या दृष्टिकोनाची मुख्य कल्पना म्हणजे ROIs अंदाज लावण्यासाठी न्यूरल नेटवर्क वापरणे - ज्याला *Region Proposal Network* म्हणतात. [पेपर](https://arxiv.org/pdf/1506.01497.pdf), 2016

![FasterRCNN](../../../../../translated_images/faster-rcnn.8d46c099b87ef30ab2ea26dbc4bdd85b974a57ba8eb526f65dc4cd0a4711de30.mr.png)

> चित्र [अधिकृत पेपर](https://arxiv.org/pdf/1506.01497.pdf)

### R-FCN: Region-Based Fully Convolutional Network

हा अल्गोरिदम Faster R-CNN पेक्षा अधिक वेगवान आहे. मुख्य कल्पना अशी आहे:

1. ResNet-101 वापरून फीचर्स काढणे.
1. फीचर्स **Position-Sensitive Score Map** द्वारे प्रक्रिया केली जातात. $C$ वर्गांमधील प्रत्येक वस्तू $k\times k$ क्षेत्रांमध्ये विभागली जाते, आणि वस्तूंचे भाग अंदाज लावण्यासाठी प्रशिक्षण दिले जाते.
1. $k\times k$ क्षेत्रांमधील प्रत्येक भागासाठी सर्व नेटवर्क्स वस्तू वर्गांसाठी मतदान करतात, आणि जास्तीत जास्त मत असलेला वर्ग निवडला जातो.

![r-fcn image](../../../../../translated_images/r-fcn.13eb88158b99a3da50fa2787a6be5cb310d47f0e9655cc93a1090dc7aab338d1.mr.png)

> चित्र [अधिकृत पेपर](https://arxiv.org/abs/1605.06409)

### YOLO - You Only Look Once

YOLO हा रिअलटाइम एक-पास अल्गोरिदम आहे. मुख्य कल्पना अशी आहे:

 * चित्र $S\times S$ क्षेत्रांमध्ये विभागले जाते.
 * प्रत्येक क्षेत्रासाठी, **CNN** $n$ शक्य वस्तू, *बॉक्स* समन्वय आणि *कॉन्फिडन्स*=*प्रॉबॅबिलिटी* * IoU अंदाज लावते.

 ![YOLO](../../../../../translated_images/yolo.a2648ec82ee8bb4ea27537677adb482fd4b733ca1705c561b6a24a85102dced5.mr.png)

> चित्र [अधिकृत पेपर](https://arxiv.org/abs/1506.02640)

### इतर अल्गोरिदम्स

* RetinaNet: [अधिकृत पेपर](https://arxiv.org/abs/1708.02002)
   - [Torchvision मधील PyTorch अंमलबजावणी](https://pytorch.org/vision/stable/_modules/torchvision/models/detection/retinanet.html)
   - [Keras अंमलबजावणी](https://github.com/fizyr/keras-retinanet)
   - [RetinaNet वापरून ऑब्जेक्ट डिटेक्शन](https://keras.io/examples/vision/retinanet/) Keras Samples मध्ये
* SSD (Single Shot Detector): [अधिकृत पेपर](https://arxiv.org/abs/1512.02325)

## ✍️ व्यायाम: ऑब्जेक्ट डिटेक्शन

खालील नोटबुकमध्ये तुमचे शिक्षण सुरू ठेवा:

[ObjectDetection.ipynb](../../../../../lessons/4-ComputerVision/11-ObjectDetection/ObjectDetection.ipynb)

## निष्कर्ष

या धड्यात तुम्ही ऑब्जेक्ट डिटेक्शन साध्य करण्याच्या विविध पद्धतींचा झपाट्याने आढावा घेतला!

## 🚀 आव्हान

या लेख आणि नोटबुक्स वाचा आणि YOLO स्वतः वापरून पहा:

* [YOLO बद्दल चांगला ब्लॉग पोस्ट](https://www.analyticsvidhya.com/blog/2018/12/practical-guide-object-detection-yolo-framewor-python/)
 * [अधिकृत साइट](https://pjreddie.com/darknet/yolo/)
 * YOLO: [Keras अंमलबजावणी](https://github.com/experiencor/keras-yolo2), [स्टेप-बाय-स्टेप नोटबुक](https://github.com/experiencor/basic-yolo-keras/blob/master/Yolo%20Step-by-Step.ipynb)
 * YOLO v2: [Keras अंमलबजावणी](https://github.com/experiencor/keras-yolo2), [स्टेप-बाय-स्टेप नोटबुक](https://github.com/experiencor/keras-yolo2/blob/master/Yolo%20Step-by-Step.ipynb)

## [व्याख्यानानंतर प्रश्नमंजुषा](https://ff-quizzes.netlify.app/en/ai/quiz/22)

## पुनरावलोकन आणि स्व-अभ्यास

* [ऑब्जेक्ट डिटेक्शन](https://tjmachinelearning.com/lectures/1718/obj/) निखिल सरदाना यांच्याकडून
* [ऑब्जेक्ट डिटेक्शन अल्गोरिदम्सची चांगली तुलना](https://lilianweng.github.io/lil-log/2018/12/27/object-detection-part-4.html)
* [ऑब्जेक्ट डिटेक्शनसाठी डीप लर्निंग अल्गोरिदम्सचा आढावा](https://medium.com/comet-app/review-of-deep-learning-algorithms-for-object-detection-c1f3d437b852)
* [ऑब्जेक्ट डिटेक्शन अल्गोरिदम्ससाठी स्टेप-बाय-स्टेप परिचय](https://www.analyticsvidhya.com/blog/2018/10/a-step-by-step-introduction-to-the-basic-object-detection-algorithms-part-1/)
* [Python मध्ये Faster R-CNN वापरून ऑब्जेक्ट डिटेक्शनची अंमलबजावणी](https://www.analyticsvidhya.com/blog/2018/11/implementation-faster-r-cnn-python-object-detection/)

## [असाइनमेंट: ऑब्जेक्ट डिटेक्शन](lab/README.md)

**अस्वीकरण**:  
हा दस्तऐवज AI भाषांतर सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) चा वापर करून भाषांतरित करण्यात आला आहे. आम्ही अचूकतेसाठी प्रयत्नशील असलो तरी, कृपया लक्षात घ्या की स्वयंचलित भाषांतरांमध्ये त्रुटी किंवा अचूकतेचा अभाव असू शकतो. मूळ भाषेतील मूळ दस्तऐवज हा अधिकृत स्रोत मानला जावा. महत्त्वाच्या माहितीसाठी, व्यावसायिक मानवी भाषांतराची शिफारस केली जाते. या भाषांतराचा वापर केल्यामुळे उद्भवलेल्या कोणत्याही गैरसमज किंवा चुकीच्या अर्थासाठी आम्ही जबाबदार राहणार नाही.