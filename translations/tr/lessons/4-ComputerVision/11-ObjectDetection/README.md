<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "d85c8b08f6d1b48fd7f35b99f93c1138",
  "translation_date": "2025-08-26T07:26:56+00:00",
  "source_file": "lessons/4-ComputerVision/11-ObjectDetection/README.md",
  "language_code": "tr"
}
-->
# Nesne Tespiti

Bugüne kadar ele aldığımız görüntü sınıflandırma modelleri, bir görüntüyü alıp MNIST problemindeki 'sayı' sınıfı gibi kategorik bir sonuç üretmiştir. Ancak, birçok durumda bir resmin nesneleri tasvir ettiğini bilmek yeterli değildir - nesnelerin tam konumlarını belirlemek isteriz. İşte **nesne tespiti** tam olarak bu noktada devreye girer.

## [Ders Öncesi Test](https://ff-quizzes.netlify.app/en/ai/quiz/21)

![Nesne Tespiti](../../../../../translated_images/Screen_Shot_2016-11-17_at_11.14.54_AM.b4bb3769353287be1b905373ed9c858102c054b16e4595c76ec3f7bba0feb549.tr.png)

> Görsel [YOLO v2 web sitesi](https://pjreddie.com/darknet/yolov2/) üzerinden alınmıştır.

## Nesne Tespiti için Naif Bir Yaklaşım

Bir resimde bir kediyi bulmak istediğimizi varsayalım, nesne tespiti için oldukça basit bir yaklaşım şu şekilde olabilir:

1. Resmi bir dizi kareye bölmek.
2. Her bir karede görüntü sınıflandırması çalıştırmak.
3. Yeterince yüksek aktivasyon veren karelerin, ilgili nesneyi içerdiği kabul edilebilir.

![Naif Nesne Tespiti](../../../../../translated_images/naive-detection.e7f1ba220ccd08c68a2ea8e06a7ed75c3fcc738c2372f9e00b7f4299a8659c01.tr.png)

> *Görsel [Egzersiz Not Defteri](../../../../../lessons/4-ComputerVision/11-ObjectDetection/ObjectDetection-TF.ipynb) üzerinden alınmıştır.*

Ancak, bu yaklaşım ideal olmaktan uzaktır çünkü algoritmanın nesnenin sınır kutusunu çok hassas bir şekilde belirlemesine izin vermez. Daha hassas bir konum belirlemek için, sınır kutularının koordinatlarını tahmin etmek üzere bir tür **regresyon** çalıştırmamız gerekir - bunun için de özel veri setlerine ihtiyaç duyarız.

## Nesne Tespiti için Regresyon

[Bu blog yazısı](https://towardsdatascience.com/object-detection-with-neural-networks-a4e2c46b4491), şekilleri tespit etmeye dair harika bir giriş sunmaktadır.

## Nesne Tespiti için Veri Setleri

Bu görev için aşağıdaki veri setleriyle karşılaşabilirsiniz:

* [PASCAL VOC](http://host.robots.ox.ac.uk/pascal/VOC/) - 20 sınıf
* [COCO](http://cocodataset.org/#home) - Bağlamda Yaygın Nesneler. 80 sınıf, sınır kutuları ve segmentasyon maskeleri

![COCO](../../../../../translated_images/coco-examples.71bc60380fa6cceb7caad48bd09e35b6028caabd363aa04fee89c414e0870e86.tr.jpg)

## Nesne Tespiti Metrikleri

### Kesişim Bölü Birleşim (Intersection over Union)

Görüntü sınıflandırması için algoritmanın ne kadar iyi performans gösterdiğini ölçmek kolaydır, ancak nesne tespiti için hem sınıfın doğruluğunu hem de tahmin edilen sınır kutusu konumunun hassasiyetini ölçmemiz gerekir. İkincisi için, **Kesişim Bölü Birleşim** (IoU) adı verilen bir ölçüm kullanırız; bu, iki kutunun (veya iki rastgele alanın) ne kadar iyi örtüştüğünü ölçer.

![IoU](../../../../../translated_images/iou_equation.9a4751d40fff4e119ecd0a7bcca4e71ab1dc83e0d4f2a0d66ff0859736f593cf.tr.png)

> *[IoU hakkında bu mükemmel blog yazısından](https://pyimagesearch.com/2016/11/07/intersection-over-union-iou-for-object-detection/) alınan Şekil 2.*

Fikir basittir - iki şekil arasındaki kesişim alanını birleşim alanına böleriz. İki özdeş alan için IoU 1 olurken, tamamen ayrık alanlar için 0 olacaktır. Diğer durumlarda 0 ile 1 arasında değişir. Genellikle IoU belirli bir değerin üzerinde olan sınır kutularını dikkate alırız.

### Ortalama Hassasiyet (Average Precision)

Bir nesne sınıfı $C$'nin ne kadar iyi tanındığını ölçmek istediğimizi varsayalım. Bunu ölçmek için **Ortalama Hassasiyet** metriğini kullanırız, bu şu şekilde hesaplanır:

1. Hassasiyet-Tekrar Çağırma eğrisi, algılama eşik değerine (0'dan 1'e kadar) bağlı olarak doğruluğu gösterir.
2. Eşik değerine bağlı olarak, görüntüde daha fazla veya daha az nesne algılanır ve farklı hassasiyet ve tekrar çağırma değerleri elde edilir.
3. Eğri şu şekilde görünür:

<img src="https://github.com/shwars/NeuroWorkshop/raw/master/images/ObjDetectionPrecisionRecall.png"/>

> *Görsel [NeuroWorkshop](http://github.com/shwars/NeuroWorkshop) üzerinden alınmıştır.*

Belirli bir sınıf $C$ için Ortalama Hassasiyet, bu eğrinin altındaki alandır. Daha kesin olarak, Tekrar Çağırma ekseni genellikle 10 parçaya bölünür ve Hassasiyet bu noktaların tümü üzerinde ortalanır:

$$
AP = {1\over11}\sum_{i=0}^{10}\mbox{Precision}(\mbox{Recall}={i\over10})
$$

### AP ve IoU

Sadece IoU belirli bir değerin üzerinde olan algılamaları dikkate alacağız. Örneğin, PASCAL VOC veri setinde genellikle $\mbox{IoU Threshold} = 0.5$ kabul edilirken, COCO'da AP farklı $\mbox{IoU Threshold}$ değerleri için ölçülür.

<img src="https://github.com/shwars/NeuroWorkshop/raw/master/images/ObjDetectionPrecisionRecallIoU.png"/>

> *Görsel [NeuroWorkshop](http://github.com/shwars/NeuroWorkshop) üzerinden alınmıştır.*

### Ortalama Ortalama Hassasiyet - mAP

Nesne Tespiti için ana metrik **Ortalama Ortalama Hassasiyet** veya **mAP** olarak adlandırılır. Bu, tüm nesne sınıfları ve bazen de $\mbox{IoU Threshold}$ üzerinde ortalanmış Ortalama Hassasiyet değeridir. **mAP** hesaplama süreci daha ayrıntılı olarak [bu blog yazısında](https://medium.com/@timothycarlen/understanding-the-map-evaluation-metric-for-object-detection-a07fe6962cf3) ve ayrıca [kod örnekleriyle burada](https://gist.github.com/tarlen5/008809c3decf19313de216b9208f3734) açıklanmıştır.

## Farklı Nesne Tespiti Yaklaşımları

Nesne tespiti algoritmaları iki geniş sınıfa ayrılır:

* **Bölge Öneri Ağları** (R-CNN, Fast R-CNN, Faster R-CNN). Ana fikir, **İlgi Alanları** (ROI) oluşturmak ve maksimum aktivasyonu aramak için CNN çalıştırmaktır. Bu, naif yaklaşıma biraz benzer, ancak ROI'ler daha akıllıca oluşturulur. Bu tür yöntemlerin en büyük dezavantajlarından biri, yavaş olmalarıdır çünkü görüntü üzerinde CNN sınıflandırıcısının birçok geçişine ihtiyaç duyarız.
* **Tek geçiş** (YOLO, SSD, RetinaNet) yöntemleri. Bu mimarilerde, ağ hem sınıfları hem de ROI'leri tek bir geçişte tahmin edecek şekilde tasarlanır.

### R-CNN: Bölge Tabanlı CNN

[R-CNN](http://islab.ulsan.ac.kr/files/announcement/513/rcnn_pami.pdf), ROI bölgelerinin hiyerarşik yapısını oluşturmak için [Selective Search](http://www.huppelen.nl/publications/selectiveSearchDraft.pdf) kullanır. Bu bölgeler daha sonra CNN özellik çıkarıcıları ve SVM sınıflandırıcıları aracılığıyla nesne sınıfını belirlemek ve *sınır kutusu* koordinatlarını belirlemek için doğrusal regresyon ile işlenir. [Resmi Makale](https://arxiv.org/pdf/1506.01497v1.pdf)

![RCNN](../../../../../translated_images/rcnn1.cae407020dfb1d1fb572656e44f75cd6c512cc220591c116c506652c10e47f26.tr.png)

> *Görsel van de Sande ve ark. ICCV’11'dan alınmıştır.*

![RCNN-1](../../../../../translated_images/rcnn2.2d9530bb83516484ec65b250c22dbf37d3d23244f32864ebcb91d98fe7c3112c.tr.png)

> *Görseller [bu blogdan](https://towardsdatascience.com/r-cnn-fast-r-cnn-faster-r-cnn-yolo-object-detection-algorithms-36d53571365e) alınmıştır.*

### F-RCNN - Hızlı R-CNN

Bu yaklaşım R-CNN'e benzer, ancak bölgeler konvolüsyon katmanları uygulandıktan sonra tanımlanır.

![FRCNN](../../../../../translated_images/f-rcnn.3cda6d9bb41888754037d2d9763e2298a96de5d9bc2a21db3147357aa5da9b1a.tr.png)

> Görsel [Resmi Makale](https://www.cv-foundation.org/openaccess/content_iccv_2015/papers/Girshick_Fast_R-CNN_ICCV_2015_paper.pdf), [arXiv](https://arxiv.org/pdf/1504.08083.pdf), 2015 üzerinden alınmıştır.

### Daha Hızlı R-CNN

Bu yaklaşımın ana fikri, ROI'leri tahmin etmek için sinir ağı kullanmaktır - *Bölge Öneri Ağı* olarak adlandırılır. [Makale](https://arxiv.org/pdf/1506.01497.pdf), 2016

![FasterRCNN](../../../../../translated_images/faster-rcnn.8d46c099b87ef30ab2ea26dbc4bdd85b974a57ba8eb526f65dc4cd0a4711de30.tr.png)

> Görsel [Resmi Makale](https://arxiv.org/pdf/1506.01497.pdf) üzerinden alınmıştır.

### R-FCN: Bölge Tabanlı Tam Konvolüsyonel Ağ

Bu algoritma, Daha Hızlı R-CNN'den bile daha hızlıdır. Ana fikir şu şekildedir:

1. Özellikler ResNet-101 kullanılarak çıkarılır.
1. Özellikler **Konum-Duyarlı Skor Haritası** tarafından işlenir. $C$ sınıflarından her bir nesne $k\times k$ bölgelere bölünür ve nesne parçalarını tahmin etmek için eğitim yapılır.
1. $k\times k$ bölgelerden her bir parça için tüm ağlar nesne sınıfları için oy kullanır ve maksimum oyu alan nesne sınıfı seçilir.

![r-fcn image](../../../../../translated_images/r-fcn.13eb88158b99a3da50fa2787a6be5cb310d47f0e9655cc93a1090dc7aab338d1.tr.png)

> Görsel [Resmi Makale](https://arxiv.org/abs/1605.06409) üzerinden alınmıştır.

### YOLO - Sadece Bir Kez Bak

YOLO, gerçek zamanlı bir tek geçiş algoritmasıdır. Ana fikir şu şekildedir:

 * Görüntü $S\times S$ bölgelere ayrılır.
 * Her bölge için **CNN**, $n$ olası nesneleri, *sınır kutusu* koordinatlarını ve *güven* = *olasılık* * IoU tahmin eder.

 ![YOLO](../../../../../translated_images/yolo.a2648ec82ee8bb4ea27537677adb482fd4b733ca1705c561b6a24a85102dced5.tr.png)

> Görsel [Resmi Makale](https://arxiv.org/abs/1506.02640) üzerinden alınmıştır.

### Diğer Algoritmalar

* RetinaNet: [Resmi Makale](https://arxiv.org/abs/1708.02002)
   - [Torchvision'da PyTorch Uygulaması](https://pytorch.org/vision/stable/_modules/torchvision/models/detection/retinanet.html)
   - [Keras Uygulaması](https://github.com/fizyr/keras-retinanet)
   - [Keras Örneklerinde RetinaNet ile Nesne Tespiti](https://keras.io/examples/vision/retinanet/)
* SSD (Tek Atış Dedektörü): [Resmi Makale](https://arxiv.org/abs/1512.02325)

## ✍️ Egzersizler: Nesne Tespiti

Öğreniminize aşağıdaki not defterinde devam edin:

[ObjectDetection.ipynb](../../../../../lessons/4-ComputerVision/11-ObjectDetection/ObjectDetection.ipynb)

## Sonuç

Bu derste, nesne tespitinin çeşitli yollarını kapsayan hızlı bir tur yaptınız!

## 🚀 Meydan Okuma

YOLO ile ilgili bu makaleleri ve not defterlerini okuyun ve kendiniz deneyin:

* [YOLO'yu açıklayan iyi bir blog yazısı](https://www.analyticsvidhya.com/blog/2018/12/practical-guide-object-detection-yolo-framewor-python/)
 * [Resmi site](https://pjreddie.com/darknet/yolo/)
 * Yolo: [Keras uygulaması](https://github.com/experiencor/keras-yolo2), [adım adım not defteri](https://github.com/experiencor/basic-yolo-keras/blob/master/Yolo%20Step-by-Step.ipynb)
 * Yolo v2: [Keras uygulaması](https://github.com/experiencor/keras-yolo2), [adım adım not defteri](https://github.com/experiencor/keras-yolo2/blob/master/Yolo%20Step-by-Step.ipynb)

## [Ders Sonrası Test](https://ff-quizzes.netlify.app/en/ai/quiz/22)

## İnceleme ve Kendi Kendine Çalışma

* [Nesne Tespiti](https://tjmachinelearning.com/lectures/1718/obj/) - Nikhil Sardana
* [Nesne tespiti algoritmalarının iyi bir karşılaştırması](https://lilianweng.github.io/lil-log/2018/12/27/object-detection-part-4.html)
* [Nesne Tespiti için Derin Öğrenme Algoritmalarının İncelemesi](https://medium.com/comet-app/review-of-deep-learning-algorithms-for-object-detection-c1f3d437b852)
* [Temel Nesne Tespiti Algoritmalarına Adım Adım Giriş](https://www.analyticsvidhya.com/blog/2018/10/a-step-by-step-introduction-to-the-basic-object-detection-algorithms-part-1/)
* [Python'da Nesne Tespiti için Daha Hızlı R-CNN Uygulaması](https://www.analyticsvidhya.com/blog/2018/11/implementation-faster-r-cnn-python-object-detection/)

## [Ödev: Nesne Tespiti](lab/README.md)

**Feragatname**:  
Bu belge, AI çeviri hizmeti [Co-op Translator](https://github.com/Azure/co-op-translator) kullanılarak çevrilmiştir. Doğruluk için çaba göstersek de, otomatik çevirilerin hata veya yanlışlık içerebileceğini lütfen unutmayın. Belgenin orijinal dili, yetkili kaynak olarak kabul edilmelidir. Kritik bilgiler için profesyonel insan çevirisi önerilir. Bu çevirinin kullanımından kaynaklanan yanlış anlamalar veya yanlış yorumlamalar için sorumluluk kabul etmiyoruz.