<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "d85c8b08f6d1b48fd7f35b99f93c1138",
  "translation_date": "2025-08-24T10:27:55+00:00",
  "source_file": "lessons/4-ComputerVision/11-ObjectDetection/README.md",
  "language_code": "fa"
}
-->
# تشخیص اشیاء

مدل‌های دسته‌بندی تصویر که تاکنون با آن‌ها کار کرده‌ایم، یک تصویر را گرفته و یک نتیجه‌ی دسته‌بندی، مانند کلاس "عدد" در مسئله‌ی MNIST، تولید می‌کردند. اما در بسیاری از موارد، ما فقط نمی‌خواهیم بدانیم که یک تصویر اشیاء را نشان می‌دهد - بلکه می‌خواهیم مکان دقیق آن‌ها را نیز تعیین کنیم. این دقیقاً هدف **تشخیص اشیاء** است.

## [پیش‌سوالات درس](https://ff-quizzes.netlify.app/en/ai/quiz/21)

![تشخیص اشیاء](../../../../../lessons/4-ComputerVision/11-ObjectDetection/images/Screen_Shot_2016-11-17_at_11.14.54_AM.png)

> تصویر از [وب‌سایت YOLO v2](https://pjreddie.com/darknet/yolov2/)

## یک رویکرد ساده برای تشخیص اشیاء

فرض کنید می‌خواهیم یک گربه را در یک تصویر پیدا کنیم. یک رویکرد بسیار ساده برای تشخیص اشیاء می‌تواند به صورت زیر باشد:

1. تصویر را به تعدادی کاشی تقسیم کنیم.
2. دسته‌بندی تصویر را روی هر کاشی اجرا کنیم.
3. کاشی‌هایی که نتیجه‌ی فعال‌سازی کافی بالایی دارند، می‌توانند حاوی شیء مورد نظر باشند.

![تشخیص ساده](../../../../../lessons/4-ComputerVision/11-ObjectDetection/images/naive-detection.png)

> *تصویر از [دفترچه تمرین](../../../../../lessons/4-ComputerVision/11-ObjectDetection/ObjectDetection-TF.ipynb)*

اما این رویکرد ایده‌آل نیست، زیرا فقط به الگوریتم اجازه می‌دهد که جعبه‌ی محدودکننده‌ی شیء را به‌طور بسیار نادقیق مکان‌یابی کند. برای مکان‌یابی دقیق‌تر، باید نوعی **رگرسیون** اجرا کنیم تا مختصات جعبه‌های محدودکننده را پیش‌بینی کنیم - و برای این کار، به مجموعه داده‌های خاصی نیاز داریم.

## رگرسیون برای تشخیص اشیاء

[این پست وبلاگ](https://towardsdatascience.com/object-detection-with-neural-networks-a4e2c46b4491) مقدمه‌ای عالی و ساده برای تشخیص اشکال ارائه می‌دهد.

## مجموعه داده‌ها برای تشخیص اشیاء

ممکن است با مجموعه داده‌های زیر برای این کار مواجه شوید:

* [PASCAL VOC](http://host.robots.ox.ac.uk/pascal/VOC/) - شامل ۲۰ کلاس
* [COCO](http://cocodataset.org/#home) - اشیاء رایج در زمینه. شامل ۸۰ کلاس، جعبه‌های محدودکننده و ماسک‌های تقسیم‌بندی

![COCO](../../../../../lessons/4-ComputerVision/11-ObjectDetection/images/coco-examples.jpg)

## معیارهای تشخیص اشیاء

### تلاقی بر اتحاد (IoU)

در حالی که برای دسته‌بندی تصویر اندازه‌گیری عملکرد الگوریتم آسان است، برای تشخیص اشیاء باید هم درستی کلاس و هم دقت مکان‌یابی جعبه‌ی محدودکننده‌ی استنتاج‌شده را اندازه‌گیری کنیم. برای مورد دوم، از معیاری به نام **تلاقی بر اتحاد** (IoU) استفاده می‌کنیم که میزان هم‌پوشانی دو جعبه (یا دو ناحیه‌ی دلخواه) را اندازه‌گیری می‌کند.

![IoU](../../../../../lessons/4-ComputerVision/11-ObjectDetection/images/iou_equation.png)

> *شکل ۲ از [این پست وبلاگ عالی درباره‌ی IoU](https://pyimagesearch.com/2016/11/07/intersection-over-union-iou-for-object-detection/)*

ایده ساده است - مساحت تلاقی بین دو شکل را بر مساحت اتحاد آن‌ها تقسیم می‌کنیم. برای دو ناحیه‌ی یکسان، IoU برابر ۱ خواهد بود، در حالی که برای نواحی کاملاً جدا از هم، IoU برابر ۰ خواهد بود. در غیر این صورت، مقدار IoU بین ۰ تا ۱ متغیر خواهد بود. معمولاً فقط جعبه‌های محدودکننده‌ای را در نظر می‌گیریم که IoU آن‌ها بالاتر از یک مقدار مشخص باشد.

### دقت میانگین (Average Precision)

فرض کنید می‌خواهیم اندازه‌گیری کنیم که یک کلاس خاص از اشیاء $C$ چقدر خوب شناسایی شده است. برای اندازه‌گیری آن، از معیار **دقت میانگین** استفاده می‌کنیم که به صورت زیر محاسبه می‌شود:

1. منحنی دقت-بازخوانی (Precision-Recall) را در نظر بگیرید که دقت را بر اساس مقدار آستانه‌ی تشخیص (از ۰ تا ۱) نشان می‌دهد.
2. بسته به آستانه، تعداد بیشتری یا کمتری از اشیاء در تصویر شناسایی می‌شوند و مقادیر مختلفی از دقت و بازخوانی به دست می‌آید.
3. منحنی به این شکل خواهد بود:

<img src="https://github.com/shwars/NeuroWorkshop/raw/master/images/ObjDetectionPrecisionRecall.png"/>

> *تصویر از [NeuroWorkshop](http://github.com/shwars/NeuroWorkshop)*

دقت میانگین برای یک کلاس خاص $C$ مساحت زیر این منحنی است. به طور دقیق‌تر، محور بازخوانی معمولاً به ۱۰ قسمت تقسیم می‌شود و دقت در تمام این نقاط میانگین‌گیری می‌شود:

$$
AP = {1\over11}\sum_{i=0}^{10}\mbox{Precision}(\mbox{Recall}={i\over10})
$$

### AP و IoU

ما فقط آن دسته از تشخیص‌ها را در نظر خواهیم گرفت که IoU آن‌ها بالاتر از یک مقدار مشخص باشد. برای مثال، در مجموعه داده‌ی PASCAL VOC معمولاً $\mbox{IoU Threshold} = 0.5$ فرض می‌شود، در حالی که در COCO، AP برای مقادیر مختلف $\mbox{IoU Threshold}$ اندازه‌گیری می‌شود.

<img src="https://github.com/shwars/NeuroWorkshop/raw/master/images/ObjDetectionPrecisionRecallIoU.png"/>

> *تصویر از [NeuroWorkshop](http://github.com/shwars/NeuroWorkshop)*

### دقت میانگین کلی - mAP

معیار اصلی برای تشخیص اشیاء **دقت میانگین کلی** یا **mAP** نامیده می‌شود. این مقدار دقت میانگین است که به طور میانگین در تمام کلاس‌های اشیاء و گاهی نیز بر اساس $\mbox{IoU Threshold}$ محاسبه می‌شود. جزئیات بیشتر درباره‌ی فرآیند محاسبه‌ی **mAP** در [این پست وبلاگ](https://medium.com/@timothycarlen/understanding-the-map-evaluation-metric-for-object-detection-a07fe6962cf3) و همچنین [اینجا با نمونه کد](https://gist.github.com/tarlen5/008809c3decf19313de216b9208f3734) توضیح داده شده است.

## روش‌های مختلف تشخیص اشیاء

دو دسته کلی از الگوریتم‌های تشخیص اشیاء وجود دارد:

* **شبکه‌های پیشنهاد ناحیه** (R-CNN، Fast R-CNN، Faster R-CNN). ایده اصلی این است که **ناحیه‌های مورد علاقه** (ROI) تولید شوند و CNN روی آن‌ها اجرا شود تا بیشترین فعال‌سازی پیدا شود. این روش کمی شبیه به رویکرد ساده است، با این تفاوت که ROIها به روشی هوشمندانه‌تر تولید می‌شوند. یکی از معایب اصلی این روش‌ها این است که کند هستند، زیرا نیاز به چندین بار عبور از طبقه‌بندی‌کننده‌ی CNN روی تصویر دارند.
* روش‌های **یک‌مرحله‌ای** (YOLO، SSD، RetinaNet). در این معماری‌ها، شبکه به گونه‌ای طراحی شده است که هم کلاس‌ها و هم ROIها را در یک مرحله پیش‌بینی کند.

### R-CNN: شبکه‌ی کانولوشنی مبتنی بر ناحیه

[R-CNN](http://islab.ulsan.ac.kr/files/announcement/513/rcnn_pami.pdf) از [جستجوی انتخابی](http://www.huppelen.nl/publications/selectiveSearchDraft.pdf) برای تولید ساختار سلسله‌مراتبی ناحیه‌های ROI استفاده می‌کند که سپس از طریق استخراج‌کننده‌های ویژگی CNN و طبقه‌بندی‌کننده‌های SVM عبور داده می‌شوند تا کلاس شیء تعیین شود و از رگرسیون خطی برای تعیین مختصات *جعبه‌ی محدودکننده* استفاده شود. [مقاله رسمی](https://arxiv.org/pdf/1506.01497v1.pdf)

![RCNN](../../../../../lessons/4-ComputerVision/11-ObjectDetection/images/rcnn1.png)

> *تصویر از van de Sande et al. ICCV’11*

![RCNN-1](../../../../../lessons/4-ComputerVision/11-ObjectDetection/images/rcnn2.png)

> *تصاویر از [این وبلاگ](https://towardsdatascience.com/r-cnn-fast-r-cnn-faster-r-cnn-yolo-object-detection-algorithms-36d53571365e)*

### F-RCNN - Fast R-CNN

این روش مشابه R-CNN است، اما ناحیه‌ها پس از اعمال لایه‌های کانولوشنی تعریف می‌شوند.

![FRCNN](../../../../../lessons/4-ComputerVision/11-ObjectDetection/images/f-rcnn.png)

> تصویر از [مقاله رسمی](https://www.cv-foundation.org/openaccess/content_iccv_2015/papers/Girshick_Fast_R-CNN_ICCV_2015_paper.pdf)، [arXiv](https://arxiv.org/pdf/1504.08083.pdf)، ۲۰۱۵

### Faster R-CNN

ایده اصلی این روش استفاده از شبکه‌ی عصبی برای پیش‌بینی ROIها است - به اصطلاح *شبکه‌ی پیشنهاد ناحیه*. [مقاله](https://arxiv.org/pdf/1506.01497.pdf)، ۲۰۱۶

![FasterRCNN](../../../../../lessons/4-ComputerVision/11-ObjectDetection/images/faster-rcnn.png)

> تصویر از [مقاله رسمی](https://arxiv.org/pdf/1506.01497.pdf)

### R-FCN: شبکه‌ی کاملاً کانولوشنی مبتنی بر ناحیه

این الگوریتم حتی سریع‌تر از Faster R-CNN است. ایده اصلی به شرح زیر است:

1. ویژگی‌ها با استفاده از ResNet-101 استخراج می‌شوند.
2. ویژگی‌ها توسط **نقشه‌ی امتیاز حساس به موقعیت** پردازش می‌شوند. هر شیء از کلاس‌های $C$ به نواحی $k\times k$ تقسیم می‌شود و ما برای پیش‌بینی بخش‌های اشیاء آموزش می‌بینیم.
3. برای هر بخش از نواحی $k\times k$، تمام شبکه‌ها برای کلاس‌های اشیاء رأی می‌دهند و کلاسی که بیشترین رأی را دارد انتخاب می‌شود.

![r-fcn image](../../../../../lessons/4-ComputerVision/11-ObjectDetection/images/r-fcn.png)

> تصویر از [مقاله رسمی](https://arxiv.org/abs/1605.06409)

### YOLO - فقط یک بار نگاه کن

YOLO یک الگوریتم یک‌مرحله‌ای بلادرنگ است. ایده اصلی به شرح زیر است:

 * تصویر به نواحی $S\times S$ تقسیم می‌شود.
 * برای هر ناحیه، **CNN** $n$ شیء ممکن، مختصات *جعبه‌ی محدودکننده* و *اعتماد* = *احتمال* * IoU را پیش‌بینی می‌کند.

 ![YOLO](../../../../../lessons/4-ComputerVision/11-ObjectDetection/images/yolo.png)

> تصویر از [مقاله رسمی](https://arxiv.org/abs/1506.02640)

### سایر الگوریتم‌ها

* RetinaNet: [مقاله رسمی](https://arxiv.org/abs/1708.02002)
   - [پیاده‌سازی PyTorch در Torchvision](https://pytorch.org/vision/stable/_modules/torchvision/models/detection/retinanet.html)
   - [پیاده‌سازی Keras](https://github.com/fizyr/keras-retinanet)
   - [تشخیص اشیاء با RetinaNet](https://keras.io/examples/vision/retinanet/) در نمونه‌های Keras
* SSD (تشخیص تک‌شات): [مقاله رسمی](https://arxiv.org/abs/1512.02325)

## ✍️ تمرین‌ها: تشخیص اشیاء

یادگیری خود را در دفترچه زیر ادامه دهید:

[ObjectDetection.ipynb](../../../../../lessons/4-ComputerVision/11-ObjectDetection/ObjectDetection.ipynb)

## نتیجه‌گیری

در این درس، مروری سریع بر روش‌های مختلفی که می‌توان برای تشخیص اشیاء استفاده کرد، داشتید!

## 🚀 چالش

این مقالات و دفترچه‌ها درباره‌ی YOLO را بخوانید و خودتان امتحان کنید:

* [پست وبلاگ خوب](https://www.analyticsvidhya.com/blog/2018/12/practical-guide-object-detection-yolo-framewor-python/) که YOLO را توضیح می‌دهد
 * [سایت رسمی](https://pjreddie.com/darknet/yolo/)
 * YOLO: [پیاده‌سازی Keras](https://github.com/experiencor/keras-yolo2)، [دفترچه گام‌به‌گام](https://github.com/experiencor/basic-yolo-keras/blob/master/Yolo%20Step-by-Step.ipynb)
 * YOLO v2: [پیاده‌سازی Keras](https://github.com/experiencor/keras-yolo2)، [دفترچه گام‌به‌گام](https://github.com/experiencor/keras-yolo2/blob/master/Yolo%20Step-by-Step.ipynb)

## [پس‌سوالات درس](https://ff-quizzes.netlify.app/en/ai/quiz/22)

## مرور و مطالعه شخصی

* [تشخیص اشیاء](https://tjmachinelearning.com/lectures/1718/obj/) توسط نیکیل ساردانا
* [مقایسه‌ی خوب الگوریتم‌های تشخیص اشیاء](https://lilianweng.github.io/lil-log/2018/12/27/object-detection-part-4.html)
* [مروری بر الگوریتم‌های یادگیری عمیق برای تشخیص اشیاء](https://medium.com/comet-app/review-of-deep-learning-algorithms-for-object-detection-c1f3d437b852)
* [مقدمه‌ای گام‌به‌گام بر الگوریتم‌های پایه‌ی تشخیص اشیاء](https://www.analyticsvidhya.com/blog/2018/10/a-step-by-step-introduction-to-the-basic-object-detection-algorithms-part-1/)
* [پیاده‌سازی Faster R-CNN در پایتون برای تشخیص اشیاء](https://www.analyticsvidhya.com/blog/2018/11/implementation-faster-r-cnn-python-object-detection/)

## [تکلیف: تشخیص اشیاء](lab/README.md)

**سلب مسئولیت**:  
این سند با استفاده از سرویس ترجمه هوش مصنوعی [Co-op Translator](https://github.com/Azure/co-op-translator) ترجمه شده است. در حالی که ما تلاش می‌کنیم دقت را حفظ کنیم، لطفاً توجه داشته باشید که ترجمه‌های خودکار ممکن است شامل خطاها یا نادرستی‌ها باشند. سند اصلی به زبان اصلی آن باید به عنوان منبع معتبر در نظر گرفته شود. برای اطلاعات حساس، توصیه می‌شود از ترجمه حرفه‌ای انسانی استفاده کنید. ما مسئولیتی در قبال سوء تفاهم‌ها یا تفسیرهای نادرست ناشی از استفاده از این ترجمه نداریم.