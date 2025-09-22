<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "717775c4050ccbffbe0c961ad8bf7bf7",
  "translation_date": "2025-08-26T07:29:57+00:00",
  "source_file": "lessons/4-ComputerVision/08-TransferLearning/README.md",
  "language_code": "tr"
}
-->
# Önceden Eğitilmiş Ağlar ve Transfer Öğrenimi

CNN'leri eğitmek çok zaman alabilir ve bu görev için çok fazla veri gereklidir. Ancak, bu sürenin büyük bir kısmı, bir ağın görüntülerden desenler çıkarmak için kullanabileceği en iyi düşük seviyeli filtreleri öğrenmekle geçer. Doğal olarak şu soru ortaya çıkar: Bir veri kümesinde eğitilmiş bir sinir ağını kullanıp, tamamen yeni bir eğitim sürecine gerek kalmadan farklı görüntüleri sınıflandırmak için uyarlayabilir miyiz?

## [Ders Öncesi Test](https://ff-quizzes.netlify.app/en/ai/quiz/15)

Bu yaklaşım **transfer öğrenimi** olarak adlandırılır, çünkü bir sinir ağı modelinden diğerine bir miktar bilgi aktarırız. Transfer öğreniminde genellikle **ImageNet** gibi büyük bir görüntü veri kümesinde eğitilmiş bir önceden eğitilmiş modelle başlarız. Bu modeller, genel görüntülerden farklı özellikler çıkarmada zaten iyi bir iş çıkarabilir ve çoğu durumda bu çıkarılan özelliklerin üzerine bir sınıflandırıcı inşa etmek iyi sonuçlar verebilir.

> ✅ Transfer Öğrenimi, Eğitim gibi diğer akademik alanlarda da karşılaşabileceğiniz bir terimdir. Bir alandaki bilgiyi alıp başka bir alana uygulama sürecini ifade eder.

## Önceden Eğitilmiş Modelleri Özellik Çıkarıcı Olarak Kullanma

Önceki bölümde bahsettiğimiz evrişimli ağlar, görüntüden özellikler çıkarmak için tasarlanmış bir dizi katman içerir. Bu katmanlar, düşük seviyeli piksel kombinasyonlarından (örneğin yatay/dikey çizgi veya vuruş) başlayarak, bir alevin gözü gibi daha yüksek seviyeli özellik kombinasyonlarına kadar çıkarım yapar. Eğer CNN'i yeterince büyük ve çeşitli bir görüntü veri kümesinde eğitirsek, ağ bu ortak özellikleri çıkarmayı öğrenmelidir.

Hem Keras hem de PyTorch, ImageNet görüntüleri üzerinde eğitilmiş bazı yaygın mimariler için önceden eğitilmiş sinir ağı ağırlıklarını kolayca yüklemek için işlevler içerir. En sık kullanılanlar, önceki dersteki [CNN Mimarıları](../07-ConvNets/CNN_Architectures.md) sayfasında açıklanmıştır. Özellikle aşağıdakilerden birini kullanmayı düşünebilirsiniz:

* **VGG-16/VGG-19**, nispeten basit modellerdir ve yine de iyi doğruluk sağlar. Transfer öğreniminin nasıl çalıştığını görmek için genellikle VGG'yi ilk deneme olarak kullanmak iyi bir seçimdir.
* **ResNet**, Microsoft Research tarafından 2015 yılında önerilen bir model ailesidir. Daha fazla katmana sahiptirler ve dolayısıyla daha fazla kaynak gerektirirler.
* **MobileNet**, mobil cihazlar için uygun, boyutu azaltılmış bir model ailesidir. Eğer kaynaklarınız sınırlıysa ve biraz doğruluk kaybını göze alabiliyorsanız, bunları kullanabilirsiniz.

İşte VGG-16 ağı tarafından bir kedi resminden çıkarılan örnek özellikler:

![VGG-16 tarafından çıkarılan özellikler](../../../../../translated_images/features.6291f9c7ba3a0b951af88fc9864632b9115365410765680680d30c927dd67354.tr.png)

## Kediler ve Köpekler Veri Kümesi

Bu örnekte, gerçek hayattaki bir görüntü sınıflandırma senaryosuna çok yakın olan [Kediler ve Köpekler](https://www.microsoft.com/download/details.aspx?id=54765&WT.mc_id=academic-77998-cacaste) veri kümesini kullanacağız.

## ✍️ Alıştırma: Transfer Öğrenimi

Transfer öğrenimini ilgili not defterlerinde uygulamada görelim:

* [Transfer Öğrenimi - PyTorch](../../../../../lessons/4-ComputerVision/08-TransferLearning/TransferLearningPyTorch.ipynb)
* [Transfer Öğrenimi - TensorFlow](../../../../../lessons/4-ComputerVision/08-TransferLearning/TransferLearningTF.ipynb)

## Adversaryal Kedi Görselleştirme

Önceden eğitilmiş bir sinir ağı, "ideal kedi" (aynı zamanda ideal köpek, ideal zebra vb.) gibi farklı desenleri "beyninde" barındırır. Bu görüntüyü bir şekilde **görselleştirmek** ilginç olurdu. Ancak bu basit değildir, çünkü desenler ağ ağırlıkları boyunca yayılmıştır ve ayrıca hiyerarşik bir yapıda organize edilmiştir.

Alabileceğimiz bir yaklaşım, rastgele bir görüntüyle başlamak ve ardından **gradyan iniş optimizasyonu** tekniğini kullanarak bu görüntüyü ağın bir kedi olduğunu düşünmesini sağlayacak şekilde ayarlamaktır.

![Görüntü Optimizasyon Döngüsü](../../../../../translated_images/ideal-cat-loop.999fbb8ff306e044f997032f4eef9152b453e6a990e449bbfb107de2493cc37e.tr.png)

Ancak bunu yaparsak, rastgele bir gürültüye çok benzeyen bir şey elde ederiz. Bunun nedeni, *ağın giriş görüntüsünü bir kedi olarak düşünmesini sağlamanın birçok yolu olmasıdır*, bunların bazıları görsel olarak anlamlı değildir. Bu görüntüler, bir kedi için tipik olan birçok deseni içerir, ancak görsel olarak ayırt edici olmalarını sağlayacak bir kısıtlama yoktur.

Sonucu iyileştirmek için kayıp fonksiyonuna **varyasyon kaybı** adı verilen başka bir terim ekleyebiliriz. Bu, görüntünün komşu piksellerinin ne kadar benzer olduğunu gösteren bir metriktir. Varyasyon kaybını minimize etmek, görüntüyü daha düzgün hale getirir ve gürültüyü ortadan kaldırır - böylece daha görsel olarak çekici desenler ortaya çıkar. İşte yüksek olasılıkla kedi ve zebra olarak sınıflandırılan bu "ideal" görüntülerin bir örneği:

![İdeal Kedi](../../../../../translated_images/ideal-cat.203dd4597643d6b0bd73038b87f9c0464322725e3a06ab145d25d4a861c70592.tr.png) | ![İdeal Zebra](../../../../../translated_images/ideal-zebra.7f70e8b54ee15a7a314000bb5df38a6cfe086ea04d60df4d3ef313d046b98a2b.tr.png)
-----|-----
 *İdeal Kedi* | *İdeal Zebra*

Benzer bir yaklaşım, sinir ağına karşı **adversaryal saldırılar** gerçekleştirmek için kullanılabilir. Diyelim ki bir sinir ağını kandırmak ve bir köpeği kedi gibi göstermek istiyoruz. Eğer ağ tarafından köpek olarak tanınan bir köpek görüntüsü alırsak, bunu biraz gradyan iniş optimizasyonu kullanarak ayarlayabiliriz, ta ki ağ bunu kedi olarak sınıflandırana kadar:

![Köpek Resmi](../../../../../translated_images/original-dog.8f68a67d2fe0911f33041c0f7fce8aa4ea919f9d3917ec4b468298522aeb6356.tr.png) | ![Kedi olarak sınıflandırılan köpek resmi](../../../../../translated_images/adversarial-dog.d9fc7773b0142b89752539bfbf884118de845b3851c5162146ea0b8809fc820f.tr.png)
-----|-----
*Orijinal köpek resmi* | *Kedi olarak sınıflandırılan köpek resmi*

Yukarıdaki sonuçları yeniden üretmek için kodu şu not defterinde görebilirsiniz:

* [İdeal ve Adversaryal Kedi - TensorFlow](../../../../../lessons/4-ComputerVision/08-TransferLearning/AdversarialCat_TF.ipynb)

## Sonuç

Transfer öğrenimi kullanarak, özel bir nesne sınıflandırma görevi için hızlı bir şekilde bir sınıflandırıcı oluşturabilir ve yüksek doğruluk elde edebilirsiniz. Daha karmaşık görevlerin artık daha yüksek hesaplama gücü gerektirdiğini ve CPU üzerinde kolayca çözülemeyeceğini görebilirsiniz. Bir sonraki birimde, aynı modeli daha düşük hesaplama kaynakları kullanarak eğitmek için daha hafif bir uygulama kullanmayı deneyeceğiz, bu da sadece biraz daha düşük doğrulukla sonuçlanır.

## 🚀 Meydan Okuma

Eşlik eden not defterlerinde, transfer bilginin en iyi şekilde benzer eğitim verileriyle (örneğin yeni bir hayvan türü) çalıştığına dair notlar bulunmaktadır. Tamamen yeni türdeki görüntülerle biraz deney yaparak transfer bilgi modellerinizin ne kadar iyi veya kötü performans gösterdiğini görün.

## [Ders Sonrası Test](https://ff-quizzes.netlify.app/en/ai/quiz/16)

## Gözden Geçirme ve Kendi Kendine Çalışma

Modellerinizi eğitmenin diğer yollarını öğrenmek için [TrainingTricks.md](TrainingTricks.md) dosyasını okuyun.

## [Ödev](lab/README.md)

Bu laboratuvarda, gerçek hayattaki [Oxford-IIIT](https://www.robots.ox.ac.uk/~vgg/data/pets/) evcil hayvan veri kümesini kullanacağız. Bu veri kümesi 35 kedi ve köpek türünü içerir ve bir transfer öğrenimi sınıflandırıcısı oluşturacağız.

**Feragatname**:  
Bu belge, AI çeviri hizmeti [Co-op Translator](https://github.com/Azure/co-op-translator) kullanılarak çevrilmiştir. Doğruluk için çaba göstersek de, otomatik çevirilerin hata veya yanlışlık içerebileceğini lütfen unutmayın. Belgenin orijinal dili, yetkili kaynak olarak kabul edilmelidir. Kritik bilgiler için profesyonel insan çevirisi önerilir. Bu çevirinin kullanımından kaynaklanan yanlış anlamalar veya yanlış yorumlamalar için sorumluluk kabul etmiyoruz.