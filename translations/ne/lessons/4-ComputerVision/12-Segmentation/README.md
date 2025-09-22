<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "d7f8a25ff13cfe9f4cd671cc23351fad",
  "translation_date": "2025-08-26T09:10:46+00:00",
  "source_file": "lessons/4-ComputerVision/12-Segmentation/README.md",
  "language_code": "ne"
}
-->
# खण्डीकरण

हामीले पहिले **Object Detection** को बारेमा सिकेका थियौं, जसले हामीलाई तस्बिरमा वस्तुहरूको *bounding boxes* भविष्यवाणी गरेर तिनीहरूको स्थान पत्ता लगाउन मद्दत गर्दछ। तर, केही कार्यहरूको लागि हामीलाई केवल bounding boxes मात्र होइन, वस्तुको अझ सटीक स्थान पत्ता लगाउन आवश्यक हुन्छ। यस कार्यलाई **segmentation** भनिन्छ।

## [Pre-lecture quiz](https://ff-quizzes.netlify.app/en/ai/quiz/23)

Segmentation लाई **pixel classification** को रूपमा हेर्न सकिन्छ, जहाँ तस्बिरको **प्रत्येक** पिक्सेलको वर्ग (*background* पनि एक वर्ग हो) भविष्यवाणी गर्नुपर्छ। मुख्य दुई प्रकारका segmentation एल्गोरिदमहरू छन्:

* **Semantic segmentation** ले केवल पिक्सेलको वर्ग बताउँछ, तर एउटै वर्गका विभिन्न वस्तुहरू बीच भिन्नता गर्दैन।
* **Instance segmentation** वर्गहरूलाई विभिन्न instances मा विभाजन गर्दछ।

उदाहरणका लागि, instance segmentation मा यी भेडाहरू अलग-अलग वस्तुहरू हुन्, तर semantic segmentation मा सबै भेडाहरूलाई एउटै वर्गले प्रतिनिधित्व गर्दछ।

<img src="images/instance_vs_semantic.jpeg" width="50%">

> तस्बिर [यस ब्लग पोस्ट](https://nirmalamurali.medium.com/image-classification-vs-semantic-segmentation-vs-instance-segmentation-625c33a08d50) बाट।

Segmentation का लागि विभिन्न neural architectures छन्, तर तिनीहरूको संरचना समान हुन्छ। यो केही हदसम्म तपाईंले पहिले सिकेको autoencoder जस्तै छ, तर मूल तस्बिरलाई deconstruct गर्ने सट्टा, हाम्रो लक्ष्य **mask** लाई deconstruct गर्नु हो। त्यसैले, segmentation नेटवर्कमा निम्न भागहरू हुन्छन्:

* **Encoder** इनपुट तस्बिरबाट features निकाल्छ।
* **Decoder** ती features लाई **mask image** मा रूपान्तरण गर्दछ, जसको आकार र च्यानलहरूको संख्या वर्गहरूको संख्याको अनुरूप हुन्छ।

<img src="images/segm.png" width="80%">

> तस्बिर [यस प्रकाशन](https://arxiv.org/pdf/2001.05566.pdf) बाट।

Segmentation मा प्रयोग हुने loss function विशेष उल्लेखनीय छ। जब classical autoencoders प्रयोग गरिन्छ, हामीले दुई तस्बिरहरू बीचको समानता मापन गर्नुपर्छ, र mean square error (MSE) प्रयोग गर्न सकिन्छ। तर segmentation मा, target mask image को प्रत्येक पिक्सेलले वर्ग संख्या (third dimension मा one-hot-encoded) प्रतिनिधित्व गर्दछ, त्यसैले हामीले classification-specific loss functions प्रयोग गर्नुपर्छ - cross-entropy loss, सबै पिक्सेलहरूमा औसत गरिएको। यदि mask binary छ भने - **binary cross-entropy loss** (BCE) प्रयोग गरिन्छ।

> ✅ One-hot encoding वर्ग label लाई वर्गहरूको संख्याको बराबर लम्बाइको vector मा encode गर्ने तरिका हो। [यस लेख](https://datagy.io/sklearn-one-hot-encode/) मा यो प्रविधि हेर्नुहोस्।

## चिकित्सा तस्बिरहरूको लागि Segmentation

यस पाठमा, हामी segmentation लाई कार्यमा देख्नेछौं, जहाँ नेटवर्कलाई चिकित्सा तस्बिरहरूमा मानव nevi (मोल्स) चिन्हित गर्न प्रशिक्षण दिनेछौं। हामी <a href="https://www.fc.up.pt/addi/ph2%20database.html">PH<sup>2</sup> Database</a> को dermoscopy तस्बिरहरू प्रयोग गर्नेछौं। यस डेटासेटमा तीन वर्गका २०० तस्बिरहरू छन्: typical nevus, atypical nevus, र melanoma। सबै तस्बिरहरूमा **mask** पनि समावेश छ, जसले nevus लाई outline गर्दछ।

> ✅ यो प्रविधि विशेष गरी चिकित्सा तस्बिरहरूको लागि उपयुक्त छ, तर तपाईं अन्य वास्तविक-जीवन अनुप्रयोगहरू के कल्पना गर्न सक्नुहुन्छ?

<img alt="navi" src="images/navi.png"/>

> तस्बिर PH<sup>2</sup> Database बाट।

हामी एक मोडेललाई nevus लाई यसको background बाट अलग गर्न प्रशिक्षण दिनेछौं।

## ✍️ अभ्यास: Semantic Segmentation

तलका notebooks खोल्नुहोस्, विभिन्न semantic segmentation architectures को बारेमा थप जान्न, तिनीहरूसँग काम गर्ने अभ्यास गर्न, र तिनीहरूलाई कार्यमा देख्न।

* [Semantic Segmentation Pytorch](../../../../../lessons/4-ComputerVision/12-Segmentation/SemanticSegmentationPytorch.ipynb)
* [Semantic Segmentation TensorFlow](../../../../../lessons/4-ComputerVision/12-Segmentation/SemanticSegmentationTF.ipynb)

## [Post-lecture quiz](https://ff-quizzes.netlify.app/en/ai/quiz/24)

## निष्कर्ष

Segmentation तस्बिर वर्गीकरणको लागि एक शक्तिशाली प्रविधि हो, bounding boxes बाट अगाडि बढेर पिक्सेल-स्तरको वर्गीकरणसम्म पुग्छ। यो चिकित्सा तस्बिरहरू लगायत अन्य अनुप्रयोगहरूमा प्रयोग गरिन्छ।

## 🚀 चुनौती

शरीर segmentation तस्बिरहरूमा मानिसहरूको साथ गर्न सकिने सामान्य कार्यहरू मध्ये एक हो। अर्को महत्त्वपूर्ण कार्यहरूमा **skeleton detection** र **pose detection** समावेश छन्। [OpenPose](https://github.com/CMU-Perceptual-Computing-Lab/openpose) लाइब्रेरी प्रयास गर्नुहोस् र pose detection कसरी प्रयोग गर्न सकिन्छ हेर्नुहोस्।

## समीक्षा र आत्म-अध्ययन

यो [wikipedia लेख](https://wikipedia.org/wiki/Image_segmentation) ले यस प्रविधिको विभिन्न अनुप्रयोगहरूको राम्रो अवलोकन प्रदान गर्दछ। Instance segmentation र Panoptic segmentation को उप-क्षेत्रहरूको बारेमा थप जान्न आफैं अध्ययन गर्नुहोस्।

## [Assignment](lab/README.md)

यस प्रयोगशालामा, [Segmentation Full Body MADS Dataset](https://www.kaggle.com/datasets/tapakah68/segmentation-full-body-mads-dataset) प्रयोग गरेर **मानव शरीर segmentation** प्रयास गर्नुहोस्।

**अस्वीकरण**:  
यो दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) प्रयोग गरी अनुवाद गरिएको हो। हामी यथासम्भव सटीकता सुनिश्चित गर्न प्रयास गर्छौं, तर कृपया ध्यान दिनुहोस् कि स्वचालित अनुवादहरूमा त्रुटिहरू वा अशुद्धताहरू हुन सक्छन्। यसको मूल भाषामा रहेको मूल दस्तावेज़लाई आधिकारिक स्रोत मानिनुपर्छ। महत्त्वपूर्ण जानकारीका लागि, व्यावसायिक मानव अनुवाद सिफारिस गरिन्छ। यस अनुवादको प्रयोगबाट उत्पन्न हुने कुनै पनि गलतफहमी वा गलत व्याख्याको लागि हामी जिम्मेवार हुने छैनौं।