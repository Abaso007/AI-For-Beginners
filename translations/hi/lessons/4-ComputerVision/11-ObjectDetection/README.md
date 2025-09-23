<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "d85c8b08f6d1b48fd7f35b99f93c1138",
  "translation_date": "2025-08-24T09:53:49+00:00",
  "source_file": "lessons/4-ComputerVision/11-ObjectDetection/README.md",
  "language_code": "hi"
}
-->
# वस्तु पहचान

अब तक हमने जिन इमेज क्लासिफिकेशन मॉडल्स का उपयोग किया है, वे एक इमेज लेते हैं और एक श्रेणीबद्ध परिणाम उत्पन्न करते हैं, जैसे कि MNIST समस्या में 'संख्या' वर्ग। हालांकि, कई मामलों में हमें केवल यह जानना नहीं होता कि तस्वीर में वस्तुएं हैं - बल्कि हम उनकी सटीक स्थिति का निर्धारण करना चाहते हैं। यही **वस्तु पहचान** का उद्देश्य है।

## [प्री-लेक्चर क्विज़](https://ff-quizzes.netlify.app/en/ai/quiz/21)

![वस्तु पहचान](../../../../../lessons/4-ComputerVision/11-ObjectDetection/images/Screen_Shot_2016-11-17_at_11.14.54_AM.png)

> चित्र [YOLO v2 वेबसाइट](https://pjreddie.com/darknet/yolov2/) से लिया गया है

## वस्तु पहचान के लिए एक साधारण दृष्टिकोण

मान लें कि हम एक तस्वीर में बिल्ली को ढूंढना चाहते हैं, तो वस्तु पहचान के लिए एक बहुत ही साधारण दृष्टिकोण निम्नलिखित होगा:

1. तस्वीर को कई टाइल्स में विभाजित करें।
2. प्रत्येक टाइल पर इमेज क्लासिफिकेशन चलाएं।
3. वे टाइल्स जिनमें पर्याप्त उच्च सक्रियता होती है, उन्हें उस वस्तु को समाहित करने वाला माना जा सकता है।

![साधारण वस्तु पहचान](../../../../../lessons/4-ComputerVision/11-ObjectDetection/images/naive-detection.png)

> *चित्र [एक्सरसाइज नोटबुक](../../../../../lessons/4-ComputerVision/11-ObjectDetection/ObjectDetection-TF.ipynb) से लिया गया है*

हालांकि, यह दृष्टिकोण आदर्श नहीं है, क्योंकि यह केवल वस्तु के बॉक्स की स्थिति को बहुत ही अनिश्चित रूप से निर्धारित करने की अनुमति देता है। अधिक सटीक स्थिति के लिए, हमें **रेग्रेशन** का उपयोग करके बॉक्स के निर्देशांक की भविष्यवाणी करनी होगी - और इसके लिए हमें विशिष्ट डेटासेट्स की आवश्यकता होती है।

## वस्तु पहचान के लिए रिग्रेशन

[यह ब्लॉग पोस्ट](https://towardsdatascience.com/object-detection-with-neural-networks-a4e2c46b4491) आकृतियों की पहचान के लिए एक शानदार परिचय प्रदान करता है।

## वस्तु पहचान के लिए डेटासेट्स

आप निम्नलिखित डेटासेट्स का सामना कर सकते हैं:

* [PASCAL VOC](http://host.robots.ox.ac.uk/pascal/VOC/) - 20 वर्ग
* [COCO](http://cocodataset.org/#home) - सामान्य वस्तुएं संदर्भ में। 80 वर्ग, बॉक्स और सेगमेंटेशन मास्क

![COCO](../../../../../lessons/4-ComputerVision/11-ObjectDetection/images/coco-examples.jpg)

## वस्तु पहचान मेट्रिक्स

### इंटरसेक्शन ओवर यूनियन

जहां इमेज क्लासिफिकेशन के लिए यह मापना आसान है कि एल्गोरिदम कितना अच्छा प्रदर्शन करता है, वस्तु पहचान के लिए हमें वर्ग की सहीता के साथ-साथ अनुमानित बॉक्स की स्थिति की सटीकता को भी मापना होता है। इसके लिए, हम **इंटरसेक्शन ओवर यूनियन** (IoU) का उपयोग करते हैं, जो मापता है कि दो बॉक्स (या दो मनमाने क्षेत्र) कितनी अच्छी तरह ओवरलैप करते हैं।

![IoU](../../../../../lessons/4-ComputerVision/11-ObjectDetection/images/iou_equation.png)

> *चित्र 2 [इस उत्कृष्ट ब्लॉग पोस्ट](https://pyimagesearch.com/2016/11/07/intersection-over-union-iou-for-object-detection/) से लिया गया है*

आइडिया सरल है - हम दो आकृतियों के बीच के इंटरसेक्शन क्षेत्र को उनके यूनियन क्षेत्र से विभाजित करते हैं। दो समान क्षेत्रों के लिए, IoU 1 होगा, जबकि पूरी तरह से अलग क्षेत्रों के लिए यह 0 होगा। अन्यथा यह 0 से 1 के बीच भिन्न होगा। हम आमतौर पर केवल उन बॉक्स को मानते हैं जिनके IoU एक निश्चित मान से ऊपर होते हैं।

### औसत सटीकता (Average Precision)

मान लें कि हम किसी दिए गए वर्ग $C$ की वस्तुओं को पहचानने की सटीकता मापना चाहते हैं। इसे मापने के लिए हम **औसत सटीकता** मेट्रिक्स का उपयोग करते हैं, जो निम्नलिखित तरीके से गणना की जाती है:

1. प्रिसिजन-रिकॉल कर्व दिखाता है कि डिटेक्शन थ्रेशहोल्ड मान (0 से 1 तक) के आधार पर सटीकता कैसे बदलती है।
2. थ्रेशहोल्ड के आधार पर, हमें इमेज में अधिक या कम वस्तुएं मिलेंगी, और प्रिसिजन और रिकॉल के अलग-अलग मान मिलेंगे।
3. कर्व इस प्रकार दिखेगा:

<img src="https://github.com/shwars/NeuroWorkshop/raw/master/images/ObjDetectionPrecisionRecall.png"/>

> *चित्र [NeuroWorkshop](http://github.com/shwars/NeuroWorkshop) से लिया गया है*

किसी दिए गए वर्ग $C$ के लिए औसत सटीकता इस कर्व के नीचे का क्षेत्र है। अधिक सटीक रूप से, रिकॉल अक्ष को आमतौर पर 10 भागों में विभाजित किया जाता है, और प्रिसिजन को उन सभी बिंदुओं पर औसत किया जाता है:

$$
AP = {1\over11}\sum_{i=0}^{10}\mbox{Precision}(\mbox{Recall}={i\over10})
$$

### AP और IoU

हम केवल उन डिटेक्शन को मानेंगे जिनके IoU एक निश्चित मान से ऊपर हैं। उदाहरण के लिए, PASCAL VOC डेटासेट में आमतौर पर $\mbox{IoU Threshold} = 0.5$ माना जाता है, जबकि COCO में AP विभिन्न $\mbox{IoU Threshold}$ मानों के लिए मापा जाता है।

<img src="https://github.com/shwars/NeuroWorkshop/raw/master/images/ObjDetectionPrecisionRecallIoU.png"/>

> *चित्र [NeuroWorkshop](http://github.com/shwars/NeuroWorkshop) से लिया गया है*

### मीन औसत सटीकता - mAP

वस्तु पहचान के लिए मुख्य मेट्रिक **मीन औसत सटीकता** या **mAP** कहलाती है। यह औसत सटीकता का मान है, जो सभी वस्तु वर्गों और कभी-कभी $\mbox{IoU Threshold}$ पर भी औसत होता है। अधिक विस्तार से, **mAP** की गणना की प्रक्रिया [इस ब्लॉग पोस्ट](https://medium.com/@timothycarlen/understanding-the-map-evaluation-metric-for-object-detection-a07fe6962cf3) में वर्णित है, और [यहां कोड नमूनों के साथ](https://gist.github.com/tarlen5/008809c3decf19313de216b9208f3734) भी।

## वस्तु पहचान के विभिन्न दृष्टिकोण

वस्तु पहचान एल्गोरिदम की दो व्यापक श्रेणियां हैं:

* **रीजन प्रपोजल नेटवर्क्स** (R-CNN, Fast R-CNN, Faster R-CNN)। मुख्य विचार है **रीजन ऑफ इंटरेस्ट्स** (ROI) उत्पन्न करना और उनके ऊपर CNN चलाना, अधिकतम सक्रियता की तलाश करना। यह साधारण दृष्टिकोण के समान है, सिवाय इसके कि ROI अधिक चतुर तरीके से उत्पन्न किए जाते हैं। ऐसे तरीकों की एक प्रमुख कमी यह है कि वे धीमे होते हैं, क्योंकि हमें इमेज पर CNN क्लासिफायर के कई पास की आवश्यकता होती है।
* **वन-पास** (YOLO, SSD, RetinaNet) विधियां। इन आर्किटेक्चर में हम नेटवर्क को एक ही पास में वर्ग और ROI दोनों की भविष्यवाणी करने के लिए डिज़ाइन करते हैं।

### R-CNN: रीजन-बेस्ड CNN

[R-CNN](http://islab.ulsan.ac.kr/files/announcement/513/rcnn_pami.pdf) [Selective Search](http://www.huppelen.nl/publications/selectiveSearchDraft.pdf) का उपयोग करता है ताकि ROI क्षेत्रों की एक पदानुक्रमित संरचना उत्पन्न की जा सके, जिन्हें फिर CNN फीचर एक्सट्रैक्टर्स और SVM-क्लासिफायर के माध्यम से पास किया जाता है ताकि वस्तु वर्ग निर्धारित किया जा सके, और *बॉक्स* निर्देशांक निर्धारित करने के लिए रिग्रेशन का उपयोग किया जाता है। [आधिकारिक पेपर](https://arxiv.org/pdf/1506.01497v1.pdf)

![RCNN](../../../../../lessons/4-ComputerVision/11-ObjectDetection/images/rcnn1.png)

> *चित्र van de Sande et al. ICCV’11 से लिया गया है*

![RCNN-1](../../../../../lessons/4-ComputerVision/11-ObjectDetection/images/rcnn2.png)

> *चित्र [इस ब्लॉग](https://towardsdatascience.com/r-cnn-fast-r-cnn-faster-r-cnn-yolo-object-detection-algorithms-36d53571365e) से लिया गया है*

### F-RCNN - फास्ट R-CNN

यह दृष्टिकोण R-CNN के समान है, लेकिन क्षेत्रों को तब परिभाषित किया जाता है जब कॉन्वोल्यूशन लेयर्स लागू हो चुकी होती हैं।

![FRCNN](../../../../../lessons/4-ComputerVision/11-ObjectDetection/images/f-rcnn.png)

> चित्र [आधिकारिक पेपर](https://www.cv-foundation.org/openaccess/content_iccv_2015/papers/Girshick_Fast_R-CNN_ICCV_2015_paper.pdf), [arXiv](https://arxiv.org/pdf/1504.08083.pdf), 2015 से लिया गया है

### फास्टर R-CNN

इस दृष्टिकोण का मुख्य विचार है कि ROI की भविष्यवाणी करने के लिए न्यूरल नेटवर्क का उपयोग किया जाए - जिसे *रीजन प्रपोजल नेटवर्क* कहा जाता है। [पेपर](https://arxiv.org/pdf/1506.01497.pdf), 2016

![FasterRCNN](../../../../../lessons/4-ComputerVision/11-ObjectDetection/images/faster-rcnn.png)

> चित्र [आधिकारिक पेपर](https://arxiv.org/pdf/1506.01497.pdf) से लिया गया है

### R-FCN: रीजन-बेस्ड फुली कॉन्वोल्यूशनल नेटवर्क

यह एल्गोरिदम फास्टर R-CNN से भी तेज है। मुख्य विचार निम्नलिखित है:

1. हम ResNet-101 का उपयोग करके फीचर्स निकालते हैं।
2. फीचर्स को **पोजिशन-सेंसिटिव स्कोर मैप** द्वारा प्रोसेस किया जाता है। $C$ वर्गों की प्रत्येक वस्तु को $k\times k$ क्षेत्रों में विभाजित किया जाता है, और हम वस्तुओं के भागों की भविष्यवाणी करने के लिए प्रशिक्षण देते हैं।
3. $k\times k$ क्षेत्रों के प्रत्येक भाग के लिए सभी नेटवर्क वस्तु वर्गों के लिए वोट करते हैं, और अधिकतम वोट वाला वस्तु वर्ग चुना जाता है।

![r-fcn image](../../../../../lessons/4-ComputerVision/11-ObjectDetection/images/r-fcn.png)

> चित्र [आधिकारिक पेपर](https://arxiv.org/abs/1605.06409) से लिया गया है

### YOLO - यू ओनली लुक वन्स

YOLO एक रीयलटाइम वन-पास एल्गोरिदम है। मुख्य विचार निम्नलिखित है:

 * इमेज को $S\times S$ क्षेत्रों में विभाजित किया जाता है।
 * प्रत्येक क्षेत्र के लिए, **CNN** $n$ संभावित वस्तुओं, *बॉक्स* निर्देशांक और *कॉन्फिडेंस*=*संभावना* * IoU की भविष्यवाणी करता है।

 ![YOLO](../../../../../lessons/4-ComputerVision/11-ObjectDetection/images/yolo.png)

> चित्र [आधिकारिक पेपर](https://arxiv.org/abs/1506.02640) से लिया गया है

### अन्य एल्गोरिदम

* RetinaNet: [आधिकारिक पेपर](https://arxiv.org/abs/1708.02002)
   - [Torchvision में PyTorch इम्प्लीमेंटेशन](https://pytorch.org/vision/stable/_modules/torchvision/models/detection/retinanet.html)
   - [Keras इम्प्लीमेंटेशन](https://github.com/fizyr/keras-retinanet)
   - [RetinaNet के साथ वस्तु पहचान](https://keras.io/examples/vision/retinanet/) Keras सैंपल्स में
* SSD (सिंगल शॉट डिटेक्टर): [आधिकारिक पेपर](https://arxiv.org/abs/1512.02325)

## ✍️ अभ्यास: वस्तु पहचान

अगले नोटबुक में अपनी सीख जारी रखें:

[ObjectDetection.ipynb](../../../../../lessons/4-ComputerVision/11-ObjectDetection/ObjectDetection.ipynb)

## निष्कर्ष

इस पाठ में आपने वस्तु पहचान को पूरा करने के विभिन्न तरीकों का संक्षिप्त दौरा किया!

## 🚀 चुनौती

इन लेखों और नोटबुक्स को पढ़ें और YOLO को स्वयं आजमाएं:

* [YOLO का वर्णन करने वाला अच्छा ब्लॉग पोस्ट](https://www.analyticsvidhya.com/blog/2018/12/practical-guide-object-detection-yolo-framewor-python/)
 * [आधिकारिक साइट](https://pjreddie.com/darknet/yolo/)
 * YOLO: [Keras इम्प्लीमेंटेशन](https://github.com/experiencor/keras-yolo2), [स्टेप-बाय-स्टेप नोटबुक](https://github.com/experiencor/basic-yolo-keras/blob/master/Yolo%20Step-by-Step.ipynb)
 * YOLO v2: [Keras इम्प्लीमेंटेशन](https://github.com/experiencor/keras-yolo2), [स्टेप-बाय-स्टेप नोटबुक](https://github.com/experiencor/keras-yolo2/blob/master/Yolo%20Step-by-Step.ipynb)

## [पोस्ट-लेक्चर क्विज़](https://ff-quizzes.netlify.app/en/ai/quiz/22)

## समीक्षा और स्व-अध्ययन

* [वस्तु पहचान](https://tjmachinelearning.com/lectures/1718/obj/) निखिल सरदाना द्वारा
* [वस्तु पहचान एल्गोरिदम की अच्छी तुलना](https://lilianweng.github.io/lil-log/2018/12/27/object-detection-part-4.html)
* [वस्तु पहचान के लिए डीप लर्निंग एल्गोरिदम की समीक्षा](https://medium.com/comet-app/review-of-deep-learning-algorithms-for-object-detection-c1f3d437b852)
* [मूल वस्तु पहचान एल्गोरिदम का चरण-दर-चरण परिचय](https://www.analyticsvidhya.com/blog/2018/10/a-step-by-step-introduction-to-the-basic-object-detection-algorithms-part-1/)
* [Python में Faster R-CNN का इम्प्लीमेंटेशन वस्तु पहचान के लिए](https://www.analyticsvidhya.com/blog/2018/11/implementation-faster-r-cnn-python-object-detection/)

## [असाइनमेंट: वस्तु पहचान](lab/README.md)

**अस्वीकरण**:  
यह दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) का उपयोग करके अनुवादित किया गया है। जबकि हम सटीकता के लिए प्रयासरत हैं, कृपया ध्यान दें कि स्वचालित अनुवाद में त्रुटियां या अशुद्धियां हो सकती हैं। मूल भाषा में उपलब्ध मूल दस्तावेज़ को प्रामाणिक स्रोत माना जाना चाहिए। महत्वपूर्ण जानकारी के लिए, पेशेवर मानव अनुवाद की सिफारिश की जाती है। इस अनुवाद के उपयोग से उत्पन्न किसी भी गलतफहमी या गलत व्याख्या के लिए हम उत्तरदायी नहीं हैं।