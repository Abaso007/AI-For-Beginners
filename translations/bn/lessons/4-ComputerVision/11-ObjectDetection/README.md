<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "d85c8b08f6d1b48fd7f35b99f93c1138",
  "translation_date": "2025-08-26T09:20:42+00:00",
  "source_file": "lessons/4-ComputerVision/11-ObjectDetection/README.md",
  "language_code": "bn"
}
-->
# অবজেক্ট ডিটেকশন

যে ইমেজ ক্লাসিফিকেশন মডেলগুলো আমরা এখন পর্যন্ত ব্যবহার করেছি, সেগুলো একটি ইমেজ নিয়ে একটি ক্যাটেগরিক্যাল ফলাফল প্রদান করত, যেমন MNIST সমস্যায় 'সংখ্যা' ক্লাস। তবে, অনেক ক্ষেত্রে আমরা শুধু জানতে চাই না যে একটি ছবি কোনো বস্তু প্রদর্শন করছে - আমরা তাদের সঠিক অবস্থান নির্ধারণ করতে চাই। **অবজেক্ট ডিটেকশন** ঠিক এই কাজটি করে।

## [প্রাক-লেকচার কুইজ](https://ff-quizzes.netlify.app/en/ai/quiz/21)

![অবজেক্ট ডিটেকশন](../../../../../translated_images/Screen_Shot_2016-11-17_at_11.14.54_AM.b4bb3769353287be1b905373ed9c858102c054b16e4595c76ec3f7bba0feb549.bn.png)

> ছবি [YOLO v2 ওয়েবসাইট](https://pjreddie.com/darknet/yolov2/) থেকে

## অবজেক্ট ডিটেকশনের একটি সরল পদ্ধতি

ধরা যাক আমরা একটি ছবিতে একটি বিড়াল খুঁজতে চাই। অবজেক্ট ডিটেকশনের একটি খুবই সরল পদ্ধতি হতে পারে নিম্নরূপ:

1. ছবিটিকে অনেকগুলো টাইলসে ভাগ করুন।
2. প্রতিটি টাইলের উপর ইমেজ ক্লাসিফিকেশন চালান।
3. যেসব টাইল যথেষ্ট উচ্চ অ্যাক্টিভেশন দেখায়, সেগুলোতে কাঙ্ক্ষিত বস্তুটি আছে বলে বিবেচনা করুন।

![সরল অবজেক্ট ডিটেকশন](../../../../../translated_images/naive-detection.e7f1ba220ccd08c68a2ea8e06a7ed75c3fcc738c2372f9e00b7f4299a8659c01.bn.png)

> *ছবি [এক্সারসাইজ নোটবুক](../../../../../lessons/4-ComputerVision/11-ObjectDetection/ObjectDetection-TF.ipynb) থেকে*

তবে, এই পদ্ধতি আদর্শ নয়, কারণ এটি বস্তুটির বাউন্ডিং বক্স খুবই অযথাযথভাবে নির্ধারণ করতে পারে। আরও সঠিক অবস্থান নির্ধারণের জন্য, আমাদের **রিগ্রেশন** চালিয়ে বাউন্ডিং বক্সের কোঅর্ডিনেট প্রেডিক্ট করতে হবে - এবং এর জন্য আমাদের নির্দিষ্ট ডেটাসেট প্রয়োজন।

## অবজেক্ট ডিটেকশনের জন্য রিগ্রেশন

[এই ব্লগ পোস্ট](https://towardsdatascience.com/object-detection-with-neural-networks-a4e2c46b4491) একটি চমৎকার পরিচিতি প্রদান করে।

## অবজেক্ট ডিটেকশনের জন্য ডেটাসেট

এই কাজের জন্য আপনি নিম্নলিখিত ডেটাসেটগুলো দেখতে পারেন:

* [PASCAL VOC](http://host.robots.ox.ac.uk/pascal/VOC/) - ২০টি ক্লাস
* [COCO](http://cocodataset.org/#home) - সাধারণ বস্তুসমূহের প্রসঙ্গ। ৮০টি ক্লাস, বাউন্ডিং বক্স এবং সেগমেন্টেশন মাস্ক।

![COCO](../../../../../translated_images/coco-examples.71bc60380fa6cceb7caad48bd09e35b6028caabd363aa04fee89c414e0870e86.bn.jpg)

## অবজেক্ট ডিটেকশন মেট্রিকস

### ইন্টারসেকশন ওভার ইউনিয়ন

যেখানে ইমেজ ক্লাসিফিকেশনের ক্ষেত্রে অ্যালগরিদমের কার্যকারিতা পরিমাপ করা সহজ, অবজেক্ট ডিটেকশনের ক্ষেত্রে আমাদের ক্লাসের সঠিকতা এবং বাউন্ডিং বক্সের অবস্থানের নির্ভুলতা উভয়ই পরিমাপ করতে হবে। এর জন্য আমরা **ইন্টারসেকশন ওভার ইউনিয়ন** (IoU) ব্যবহার করি, যা দুটি বক্স (বা দুটি এলাকা) কতটা ওভারল্যাপ করে তা পরিমাপ করে।

![IoU](../../../../../translated_images/iou_equation.9a4751d40fff4e119ecd0a7bcca4e71ab1dc83e0d4f2a0d66ff0859736f593cf.bn.png)

> *[এই চমৎকার ব্লগ পোস্ট](https://pyimagesearch.com/2016/11/07/intersection-over-union-iou-for-object-detection/) থেকে ফিগার ২*

আইডিয়াটি সহজ - আমরা দুটি ফিগারের ইন্টারসেকশন এলাকার আয়তনকে তাদের ইউনিয়ন এলাকার আয়তন দ্বারা ভাগ করি। দুটি অভিন্ন এলাকার জন্য IoU হবে ১, আর সম্পূর্ণ পৃথক এলাকার জন্য এটি হবে ০। অন্যথায় এটি ০ থেকে ১ এর মধ্যে পরিবর্তিত হবে। আমরা সাধারণত শুধুমাত্র সেই বাউন্ডিং বক্সগুলো বিবেচনা করি যেগুলোর IoU একটি নির্দিষ্ট মানের উপরে থাকে।

### গড় নির্ভুলতা (Average Precision)

ধরা যাক আমরা একটি নির্দিষ্ট ক্লাসের বস্তু $C$ কতটা ভালোভাবে শনাক্ত হচ্ছে তা পরিমাপ করতে চাই। এর জন্য আমরা **গড় নির্ভুলতা** মেট্রিকস ব্যবহার করি, যা নিম্নরূপে গণনা করা হয়:

1. প্রিসিশন-রিকল কার্ভটি দেখায় যে শনাক্তকরণের থ্রেশহোল্ড মান (০ থেকে ১) অনুযায়ী সঠিকতা কেমন।
2. থ্রেশহোল্ডের উপর নির্ভর করে, আমরা ছবিতে বেশি বা কম বস্তু শনাক্ত করব এবং প্রিসিশন ও রিকলের বিভিন্ন মান পাব।
3. কার্ভটি এরকম দেখাবে:

<img src="https://github.com/shwars/NeuroWorkshop/raw/master/images/ObjDetectionPrecisionRecall.png"/>

> *ছবি [NeuroWorkshop](http://github.com/shwars/NeuroWorkshop) থেকে*

একটি নির্দিষ্ট ক্লাস $C$ এর জন্য গড় নির্ভুলতা হলো এই কার্ভের নিচের এলাকা। আরও নির্দিষ্টভাবে, রিকল অক্ষ সাধারণত ১০টি অংশে বিভক্ত হয় এবং প্রিসিশন এই পয়েন্টগুলোর উপর গড় করা হয়:

$$
AP = {1\over11}\sum_{i=0}^{10}\mbox{Precision}(\mbox{Recall}={i\over10})
$$

### AP এবং IoU

আমরা শুধুমাত্র সেই শনাক্তকরণগুলো বিবেচনা করব, যেগুলোর IoU একটি নির্দিষ্ট মানের উপরে। উদাহরণস্বরূপ, PASCAL VOC ডেটাসেটে সাধারণত $\mbox{IoU Threshold} = 0.5$ ধরা হয়, যেখানে COCO ডেটাসেটে বিভিন্ন $\mbox{IoU Threshold}$ এর জন্য AP পরিমাপ করা হয়।

<img src="https://github.com/shwars/NeuroWorkshop/raw/master/images/ObjDetectionPrecisionRecallIoU.png"/>

> *ছবি [NeuroWorkshop](http://github.com/shwars/NeuroWorkshop) থেকে*

### গড় গড় নির্ভুলতা - mAP

অবজেক্ট ডিটেকশনের প্রধান মেট্রিক হলো **গড় গড় নির্ভুলতা**, বা **mAP**। এটি হলো গড় নির্ভুলতার মান, যা সমস্ত অবজেক্ট ক্লাসের উপর গড় করা হয়, এবং কখনও কখনও $\mbox{IoU Threshold}$ এর উপরও গড় করা হয়। **mAP** গণনার বিস্তারিত প্রক্রিয়া
[এই ব্লগ পোস্টে](https://medium.com/@timothycarlen/understanding-the-map-evaluation-metric-for-object-detection-a07fe6962cf3) এবং [কোড উদাহরণসহ এখানে](https://gist.github.com/tarlen5/008809c3decf19313de216b9208f3734) বর্ণনা করা হয়েছে।

## বিভিন্ন অবজেক্ট ডিটেকশন পদ্ধতি

অবজেক্ট ডিটেকশন অ্যালগরিদমের দুটি প্রধান শ্রেণি রয়েছে:

* **রিজন প্রপোজাল নেটওয়ার্কস** (R-CNN, Fast R-CNN, Faster R-CNN)। মূল ধারণাটি হলো **রিজনস অফ ইন্টারেস্ট** (ROI) তৈরি করা এবং সেগুলোর উপর CNN চালানো, সর্বোচ্চ অ্যাক্টিভেশন খুঁজে বের করার জন্য। এটি সরল পদ্ধতির মতো, তবে ROI আরও বুদ্ধিমানের সাথে তৈরি করা হয়। এই পদ্ধতির একটি বড় সমস্যা হলো এটি ধীর, কারণ ছবির উপর CNN ক্লাসিফায়ার অনেকবার চালাতে হয়।
* **ওয়ান-পাস** (YOLO, SSD, RetinaNet) পদ্ধতি। এই আর্কিটেকচারে আমরা নেটওয়ার্ক ডিজাইন করি যাতে এটি একবারে ক্লাস এবং ROI উভয়ই প্রেডিক্ট করতে পারে।

### R-CNN: রিজন-বেসড CNN

[R-CNN](http://islab.ulsan.ac.kr/files/announcement/513/rcnn_pami.pdf) [Selective Search](http://www.huppelen.nl/publications/selectiveSearchDraft.pdf) ব্যবহার করে ROI অঞ্চলের একটি হায়ারারকিকাল স্ট্রাকচার তৈরি করে, যা পরে CNN ফিচার এক্সট্রাক্টর এবং SVM-ক্লাসিফায়ারগুলোর মাধ্যমে বস্তু ক্লাস নির্ধারণ করে এবং লিনিয়ার রিগ্রেশন ব্যবহার করে *বাউন্ডিং বক্স* এর কোঅর্ডিনেট নির্ধারণ করে। [অফিশিয়াল পেপার](https://arxiv.org/pdf/1506.01497v1.pdf)

![RCNN](../../../../../translated_images/rcnn1.cae407020dfb1d1fb572656e44f75cd6c512cc220591c116c506652c10e47f26.bn.png)

> *ছবি van de Sande et al. ICCV’11*

![RCNN-1](../../../../../translated_images/rcnn2.2d9530bb83516484ec65b250c22dbf37d3d23244f32864ebcb91d98fe7c3112c.bn.png)

> *ছবি [এই ব্লগ](https://towardsdatascience.com/r-cnn-fast-r-cnn-faster-r-cnn-yolo-object-detection-algorithms-36d53571365e) থেকে*

### F-RCNN - ফাস্ট R-CNN

এই পদ্ধতি R-CNN এর মতোই, তবে রিজনগুলো কনভোলিউশন লেয়ার প্রয়োগ করার পরে নির্ধারণ করা হয়।

![FRCNN](../../../../../translated_images/f-rcnn.3cda6d9bb41888754037d2d9763e2298a96de5d9bc2a21db3147357aa5da9b1a.bn.png)

> ছবি [অফিশিয়াল পেপার](https://www.cv-foundation.org/openaccess/content_iccv_2015/papers/Girshick_Fast_R-CNN_ICCV_2015_paper.pdf), [arXiv](https://arxiv.org/pdf/1504.08083.pdf), ২০১৫

### Faster R-CNN

এই পদ্ধতির মূল ধারণা হলো রিজন প্রেডিক্ট করতে নিউরাল নেটওয়ার্ক ব্যবহার করা - যাকে *রিজন প্রপোজাল নেটওয়ার্ক* বলা হয়। [পেপার](https://arxiv.org/pdf/1506.01497.pdf), ২০১৬

![FasterRCNN](../../../../../translated_images/faster-rcnn.8d46c099b87ef30ab2ea26dbc4bdd85b974a57ba8eb526f65dc4cd0a4711de30.bn.png)

> ছবি [অফিশিয়াল পেপার](https://arxiv.org/pdf/1506.01497.pdf) থেকে

### R-FCN: রিজন-বেসড ফুলি কনভোলিউশনাল নেটওয়ার্ক

এই অ্যালগরিদম Faster R-CNN এর চেয়েও দ্রুত। মূল ধারণাটি হলো:

1. আমরা ResNet-101 ব্যবহার করে ফিচার এক্সট্রাক্ট করি।
2. ফিচারগুলো **পজিশন-সেনসিটিভ স্কোর ম্যাপ** দ্বারা প্রক্রিয়াকৃত হয়। $C$ ক্লাসের প্রতিটি অবজেক্টকে $k\times k$ অঞ্চলে ভাগ করা হয় এবং আমরা অবজেক্টের অংশগুলো প্রেডিক্ট করতে প্রশিক্ষণ দিই।
3. $k\times k$ অঞ্চলের প্রতিটি অংশের জন্য সমস্ত নেটওয়ার্ক অবজেক্ট ক্লাসের জন্য ভোট দেয় এবং সর্বোচ্চ ভোটপ্রাপ্ত ক্লাসটি নির্বাচিত হয়।

![r-fcn image](../../../../../translated_images/r-fcn.13eb88158b99a3da50fa2787a6be5cb310d47f0e9655cc93a1090dc7aab338d1.bn.png)

> ছবি [অফিশিয়াল পেপার](https://arxiv.org/abs/1605.06409) থেকে

### YOLO - ইউ অনলি লুক ওন্স

YOLO একটি রিয়েলটাইম ওয়ান-পাস অ্যালগরিদম। মূল ধারণাটি হলো:

 * ছবিটিকে $S\times S$ অঞ্চলে ভাগ করা হয়।
 * প্রতিটি অঞ্চলের জন্য, **CNN** $n$ সম্ভাব্য অবজেক্ট, *বাউন্ডিং বক্স* এর কোঅর্ডিনেট এবং *কনফিডেন্স*=*প্রোবাবিলিটি* * IoU প্রেডিক্ট করে।

 ![YOLO](../../../../../translated_images/yolo.a2648ec82ee8bb4ea27537677adb482fd4b733ca1705c561b6a24a85102dced5.bn.png)

> ছবি [অফিশিয়াল পেপার](https://arxiv.org/abs/1506.02640) থেকে

### অন্যান্য অ্যালগরিদম

* RetinaNet: [অফিশিয়াল পেপার](https://arxiv.org/abs/1708.02002)
   - [Torchvision-এ PyTorch ইমপ্লিমেন্টেশন](https://pytorch.org/vision/stable/_modules/torchvision/models/detection/retinanet.html)
   - [Keras ইমপ্লিমেন্টেশন](https://github.com/fizyr/keras-retinanet)
   - [Keras উদাহরণে Object Detection with RetinaNet](https://keras.io/examples/vision/retinanet/)
* SSD (Single Shot Detector): [অফিশিয়াল পেপার](https://arxiv.org/abs/1512.02325)

## ✍️ এক্সারসাইজ: অবজেক্ট ডিটেকশন

নিম্নলিখিত নোটবুকে আপনার শেখা চালিয়ে যান:

[ObjectDetection.ipynb](../../../../../lessons/4-ComputerVision/11-ObjectDetection/ObjectDetection.ipynb)

## উপসংহার

এই পাঠে আপনি অবজেক্ট ডিটেকশন সম্পন্ন করার বিভিন্ন পদ্ধতির একটি দ্রুত পর্যালোচনা করেছেন!

## 🚀 চ্যালেঞ্জ

এই আর্টিকেল এবং নোটবুকগুলো পড়ুন এবং YOLO নিজে চেষ্টা করুন:

* [YOLO সম্পর্কে একটি ভালো ব্লগ পোস্ট](https://www.analyticsvidhya.com/blog/2018/12/practical-guide-object-detection-yolo-framewor-python/)
 * [অফিশিয়াল সাইট](https://pjreddie.com/darknet/yolo/)
 * YOLO: [Keras ইমপ্লিমেন্টেশন](https://github.com/experiencor/keras-yolo2), [স্টেপ-বাই-স্টেপ নোটবুক](https://github.com/experiencor/basic-yolo-keras/blob/master/Yolo%20Step-by-Step.ipynb)
 * YOLO v2: [Keras ইমপ্লিমেন্টেশন](https://github.com/experiencor/keras-yolo2), [স্টেপ-বাই-স্টেপ নোটবুক](https://github.com/experiencor/keras-yolo2/blob/master/Yolo%20Step-by-Step.ipynb)

## [পোস্ট-লেকচার কুইজ](https://ff-quizzes.netlify.app/en/ai/quiz/22)

## পর্যালোচনা ও স্ব-অধ্যয়ন

* [অবজেক্ট ডিটেকশন](https://tjmachinelearning.com/lectures/1718/obj/) নিখিল সারদানার দ্বারা
* [অবজেক্ট ডিটেকশন অ্যালগরিদমের একটি ভালো তুলনা](https://lilianweng.github.io/lil-log/2018/12/27/object-detection-part-4.html)
* [অবজেক্ট ডিটেকশনের জন্য ডিপ লার্নিং অ্যালগরিদমের পর্যালোচনা](https://medium.com/comet-app/review-of-deep-learning-algorithms-for-object-detection-c1f3d437b852)
* [অবজেক্ট ডিটেকশন অ্যালগরিদমের একটি স্টেপ-বাই-স্টেপ পরিচিতি](https://www.analyticsvidhya.com/blog/2018/10/a-step-by-step-introduction-to-the-basic-object-detection-algorithms-part-1/)
* [Python-এ Faster R-CNN ইমপ্লিমেন্টেশন](https://www.analyticsvidhya.com/blog/2018/11/implementation-faster-r-cnn-python-object-detection/)

## [অ্যাসাইনমেন্ট: অবজেক্ট ডিটেকশন](lab/README.md)

**অস্বীকৃতি**:  
এই নথিটি AI অনুবাদ পরিষেবা [Co-op Translator](https://github.com/Azure/co-op-translator) ব্যবহার করে অনুবাদ করা হয়েছে। আমরা যথাসম্ভব সঠিক অনুবাদের চেষ্টা করি, তবে অনুগ্রহ করে মনে রাখবেন যে স্বয়ংক্রিয় অনুবাদে ত্রুটি বা অসঙ্গতি থাকতে পারে। নথিটির মূল ভাষায় লেখা সংস্করণটিকেই প্রামাণিক উৎস হিসেবে বিবেচনা করা উচিত। গুরুত্বপূর্ণ তথ্যের জন্য, পেশাদার মানব অনুবাদ ব্যবহার করার পরামর্শ দেওয়া হচ্ছে। এই অনুবাদ ব্যবহারের ফলে সৃষ্ট কোনো ভুল বোঝাবুঝি বা ভুল ব্যাখ্যার জন্য আমরা দায়ী নই।