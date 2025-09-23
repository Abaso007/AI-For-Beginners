<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "0c84b280e654e05ed658023021a6a975",
  "translation_date": "2025-09-23T08:42:38+00:00",
  "source_file": "lessons/1-Intro/README.md",
  "language_code": "tr"
}
-->
# Yapay Zekaya Giriş

![Yapay Zeka içeriğinin özetini gösteren bir çizim](../../../../translated_images/ai-intro.bf28d1ac4235881c096f0ffdb320ba4102940eafcca4e9d7a55a03914361f8f3.tr.png)

> Çizim notları: [Tomomi Imura](https://twitter.com/girlie_mac)

## [Ders Öncesi Test](https://ff-quizzes.netlify.app/en/ai/quiz/1)

**Yapay Zeka**, bilgisayarların insanlara özgü zeki davranışlar sergilemesini nasıl sağlayabileceğimizi inceleyen heyecan verici bir bilim dalıdır. Örneğin, insanların iyi olduğu şeyleri yapabilmesi.

Bilgisayarlar ilk olarak [Charles Babbage](https://en.wikipedia.org/wiki/Charles_Babbage) tarafından, belirli bir prosedürü - bir algoritmayı - takip ederek sayılar üzerinde işlem yapmak için icat edilmiştir. Modern bilgisayarlar, 19. yüzyılda önerilen orijinal modelden çok daha gelişmiş olmasına rağmen, hala kontrollü hesaplama fikrini takip eder. Bu nedenle, bir hedefe ulaşmak için gereken adımların tam sırasını bildiğimiz sürece bir bilgisayarı bir şey yapması için programlamak mümkündür.

![Bir kişinin fotoğrafı](../../../../translated_images/dsh_age.d212a30d4e54fb5f68b94a624aad64bc086124bcbbec9561ae5bd5da661e22d8.tr.png)

> Fotoğraf: [Vickie Soshnikova](http://twitter.com/vickievalerie)

> ✅ Bir kişinin fotoğrafından yaşını belirlemek, açıkça programlanamayacak bir görevdir, çünkü bunu yaparken kafamızda bir sayı belirlediğimizde nasıl düşündüğümüzü tam olarak bilmiyoruz.

---

Ancak, nasıl çözüleceğini açıkça bilmediğimiz bazı görevler vardır. Örneğin, bir kişinin fotoğrafından yaşını belirlemeyi düşünün. Bunu yapmayı bir şekilde öğreniyoruz, çünkü farklı yaşlardaki birçok insan örneği gördük, ancak bunu nasıl yaptığımızı açıkça açıklayamıyoruz ve bilgisayarı bunu yapması için programlayamıyoruz. İşte tam da bu tür görevler **Yapay Zeka** (kısaca AI) için ilgi çekicidir.

✅ Bilgisayara devredebileceğiniz ve AI'dan faydalanabilecek bazı görevler düşünün. Finans, tıp ve sanat alanlarını göz önünde bulundurun - bu alanlar bugün AI'dan nasıl faydalanıyor?

## Zayıf AI ve Güçlü AI

Zayıf AI | Güçlü AI
---------------------------------------|-------------------------------------
Zayıf AI, belirli bir görev veya dar bir görev seti için tasarlanmış ve eğitilmiş AI sistemlerini ifade eder.|Güçlü AI veya Yapay Genel Zeka (AGI), insan seviyesinde zeka ve anlayışa sahip AI sistemlerini ifade eder.
Bu AI sistemleri genel olarak zeki değildir; tanımlanmış bir görevde mükemmel performans gösterirler ancak gerçek bir anlayış veya bilinçten yoksundurlar.|Bu AI sistemleri, bir insanın yapabileceği herhangi bir entelektüel görevi gerçekleştirme, farklı alanlara uyum sağlama ve bir tür bilinç veya öz farkındalık sahibi olma yeteneğine sahiptir.
Zayıf AI örnekleri arasında Siri veya Alexa gibi sanal asistanlar, akış hizmetleri tarafından kullanılan öneri algoritmaları ve belirli müşteri hizmetleri görevleri için tasarlanmış sohbet botları bulunur.|Güçlü AI'ya ulaşmak, AI araştırmalarının uzun vadeli bir hedefidir ve geniş bir görev ve bağlam yelpazesinde akıl yürütme, öğrenme, anlama ve uyum sağlama yeteneğine sahip AI sistemlerinin geliştirilmesini gerektirir.
Zayıf AI son derece özelleşmiştir ve dar bir alanın ötesinde insan benzeri bilişsel yeteneklere veya genel problem çözme yeteneklerine sahip değildir.|Güçlü AI şu anda teorik bir kavramdır ve hiçbir AI sistemi bu genel zeka seviyesine ulaşmamıştır.

Daha fazla bilgi için **[Yapay Genel Zeka](https://en.wikipedia.org/wiki/Artificial_general_intelligence)** (AGI) sayfasına bakabilirsiniz.

## Zeka Tanımı ve Turing Testi

**[Zeka](https://en.wikipedia.org/wiki/Intelligence)** terimiyle uğraşırken karşılaşılan sorunlardan biri, bu terimin net bir tanımının olmamasıdır. Zekanın **soyut düşünme** veya **öz farkındalık** ile bağlantılı olduğunu iddia edebilirsiniz, ancak bunu doğru bir şekilde tanımlayamayız.

![Bir kedinin fotoğrafı](../../../../translated_images/photo-cat.8c8e8fb760ffe45725c5b9f6b0d954e9bf114475c01c55adf0303982851b7eae.tr.jpg)

> [Fotoğraf](https://unsplash.com/photos/75715CVEJhI): [Amber Kipp](https://unsplash.com/@sadmax) tarafından Unsplash'ta

*Zeka* teriminin belirsizliğini görmek için şu soruyu yanıtlamayı deneyin: "Bir kedi zeki midir?" Farklı insanlar bu soruya farklı yanıtlar verme eğilimindedir, çünkü bu iddianın doğru olup olmadığını kanıtlayacak evrensel olarak kabul edilmiş bir test yoktur. Ve eğer olduğunu düşünüyorsanız - kedinizi bir IQ testinden geçirmeyi deneyin...

✅ Bir dakikanızı ayırıp zekayı nasıl tanımladığınızı düşünün. Bir labirenti çözerek yiyeceğe ulaşabilen bir karga zeki midir? Bir çocuk zeki midir?

---

AGI'den bahsederken, gerçekten zeki bir sistem oluşturup oluşturmadığımızı anlamanın bir yoluna ihtiyacımız var. [Alan Turing](https://en.wikipedia.org/wiki/Alan_Turing), aynı zamanda bir zeka tanımı olarak da işlev gören bir yöntem önerdi: **[Turing Testi](https://en.wikipedia.org/wiki/Turing_test)**. Test, verilen bir sistemi doğal olarak zeki bir şeyle - gerçek bir insanla - karşılaştırır ve herhangi bir otomatik karşılaştırma bir bilgisayar programı tarafından atlatılabileceği için, bir insan sorgulayıcı kullanırız. Yani, bir insan, metin tabanlı bir diyalogda gerçek bir kişi ile bir bilgisayar sistemi arasındaki farkı ayırt edemezse - sistem zeki kabul edilir.

> St. Petersburg'da geliştirilen [Eugene Goostman](https://en.wikipedia.org/wiki/Eugene_Goostman) adlı bir sohbet botu, 2014 yılında Turing testini geçmeye yaklaştı. Bot, zekice bir kişilik hilesi kullanarak kendisini 13 yaşında bir Ukraynalı çocuk olarak tanıttı, bu da bilgi eksikliğini ve metindeki bazı tutarsızlıkları açıklıyordu. Bot, 5 dakikalık bir diyalogdan sonra yargıçların %30'unu insan olduğuna ikna etti, bu Turing'in bir makinenin 2000 yılına kadar geçebileceğine inandığı bir ölçüttü. Ancak, bunun zeki bir sistem oluşturduğumuz anlamına gelmediğini veya bir bilgisayar sisteminin insan sorgulayıcıyı kandırdığı anlamına gelmediğini anlamak gerekir - sistemi kandıran insanlar değil, botun yaratıcılarıydı!

✅ Hiç bir sohbet botunun insan olduğuna inanmanız için sizi kandırdığı oldu mu? Sizi nasıl ikna etti?

## Yapay Zekaya Yaklaşımlar

Bir bilgisayarın insan gibi davranmasını istiyorsak, bir şekilde bilgisayarın içinde düşünme biçimimizi modellememiz gerekir. Dolayısıyla, bir insanı zeki yapan şeyin ne olduğunu anlamaya çalışmamız gerekir.

> Bir makineye zeka programlayabilmek için, kendi karar verme süreçlerimizin nasıl işlediğini anlamamız gerekir. Biraz kendinizi gözlemlediğinizde, bazı süreçlerin bilinçaltında gerçekleştiğini fark edeceksiniz – örneğin, bir kediyi bir köpekten ayırt edebiliriz, ancak bunu düşünmeden yaparız – diğer bazı süreçler ise akıl yürütmeyi içerir.

Bu soruna iki olası yaklaşım vardır:

Üstten Aşağı Yaklaşım (Sembolik Akıl Yürütme) | Alttan Yukarı Yaklaşım (Sinir Ağları)
---------------------------------------|-------------------------------------
Üstten aşağı yaklaşım, bir kişinin bir problemi çözmek için akıl yürütme biçimini modellemeye çalışır. Bu, bir insandan **bilgi** çıkarmayı ve bunu bilgisayar tarafından okunabilir bir biçimde temsil etmeyi içerir. Ayrıca, bilgisayar içinde **akıl yürütmeyi** modellemenin bir yolunu geliştirmemiz gerekir. | Alttan yukarı yaklaşım, insan beyninin yapısını, **nöronlar** adı verilen çok sayıda basit birimden oluşan bir yapıyı modellemeye çalışır. Her nöron, girdilerinin ağırlıklı bir ortalaması gibi davranır ve nöronlardan oluşan bir ağı, **eğitim verileri** sağlayarak faydalı problemleri çözmek için eğitebiliriz.

Ayrıca zekaya yönelik başka olası yaklaşımlar da vardır:

* **Ortaya Çıkan**, **Sinergik** veya **çoklu ajan yaklaşımı**, karmaşık zeki davranışların çok sayıda basit ajanın etkileşimiyle elde edilebileceği gerçeğine dayanır. [Evrimsel sibernetik](https://en.wikipedia.org/wiki/Global_brain#Evolutionary_cybernetics)'e göre, zeka daha basit, tepkisel davranışlardan *metasistem geçişi* sürecinde *ortaya çıkabilir*.

* **Evrimsel yaklaşım** veya **genetik algoritma**, evrim ilkelerine dayanan bir optimizasyon sürecidir.

Bu yaklaşımları kursun ilerleyen bölümlerinde ele alacağız, ancak şu anda iki ana yön üzerinde duracağız: üstten aşağı ve alttan yukarı.

### Üstten Aşağı Yaklaşım

**Üstten aşağı yaklaşımda**, akıl yürütmemizi modellemeye çalışırız. Çünkü akıl yürütürken düşüncelerimizi takip edebiliriz, bu süreci biçimlendirmeye ve bilgisayarın içine programlamaya çalışabiliriz. Buna **sembolik akıl yürütme** denir.

İnsanlar, karar verme süreçlerini yönlendiren bazı kurallara sahip olma eğilimindedir. Örneğin, bir doktor bir hastayı teşhis ederken, kişinin ateşi olduğunu fark edebilir ve bu nedenle vücutta bir iltihaplanma olabileceğini düşünebilir. Bir doktor, belirli bir probleme büyük bir kural seti uygulayarak nihai teşhise ulaşabilir.

Bu yaklaşım büyük ölçüde **bilgi temsili** ve **akıl yürütme**ye dayanır. Bir insan uzmandan bilgi çıkarmak en zor kısım olabilir, çünkü bir doktor birçok durumda belirli bir teşhise neden ulaştığını tam olarak bilmeyebilir. Bazen çözüm açık düşünme olmadan kafasında belirir. Bir kişinin fotoğrafından yaşını belirlemek gibi bazı görevler, bilgi manipülasyonuna hiç indirgenemez.

### Alttan Yukarı Yaklaşım

Alternatif olarak, beynimizdeki en basit öğeleri – bir nöronu – modellemeye çalışabiliriz. Bilgisayarın içinde **yapay bir sinir ağı** oluşturabilir ve ardından ona örnekler vererek problemleri çözmeyi öğretmeye çalışabiliriz. Bu süreç, yeni doğmuş bir çocuğun çevresini gözlem yaparak öğrenmesine benzer.

✅ Bebeklerin nasıl öğrendiği hakkında biraz araştırma yapın. Bir bebeğin beyninin temel unsurları nelerdir?

> | Peki ya ML?         |      |
> |--------------|-----------|
> | Bir problemin bazı verilere dayanarak çözülmesi için bilgisayarın öğrenmesine dayanan Yapay Zeka'nın bir kısmına **Makine Öğrenimi** denir. Bu kursta klasik makine öğrenimini ele almayacağız - sizi ayrı bir [Makine Öğrenimi için Başlangıç](http://aka.ms/ml-beginners) müfredatına yönlendiriyoruz. |   ![Başlangıç için ML](../../../../translated_images/ml-for-beginners.9e4fed176fd5817d7d1f7d358302515186579cbf09b2a6c5bd8092b345da7f22.tr.png)    |

## Yapay Zekanın Kısa Tarihi

Yapay Zeka, yirminci yüzyılın ortalarında bir alan olarak başladı. Başlangıçta, sembolik akıl yürütme yaygın bir yaklaşımdı ve sınırlı problem alanlarında bir uzman gibi davranabilen uzman sistemler gibi önemli başarılar sağladı. Ancak, bu yaklaşımın iyi ölçeklenmediği kısa sürede anlaşıldı. Bir uzmandan bilgi çıkarmak, bunu bir bilgisayarda temsil etmek ve bilgi tabanını doğru tutmak çok karmaşık ve birçok durumda pratik olmaktan çok pahalı bir görev olduğu ortaya çıktı. Bu durum, 1970'lerde [AI Kışı](https://en.wikipedia.org/wiki/AI_winter) olarak adlandırılan döneme yol açtı.

<img alt="Yapay Zekanın Kısa Tarihi" src="images/history-of-ai.png" width="70%"/>

> Görsel: [Dmitry Soshnikov](http://soshnikov.com)

Zamanla, bilgisayar kaynakları ucuzladı ve daha fazla veri erişilebilir hale geldi, bu nedenle sinir ağı yaklaşımları, insanlarla rekabet edebilecek performans göstermeye başladı. Son on yılda, Yapay Zeka terimi çoğunlukla Sinir Ağları ile eş anlamlı olarak kullanıldı, çünkü duyduğumuz Yapay Zeka başarılarının çoğu bunlara dayanıyor.

Satranç oynayan bir bilgisayar programı oluşturma yaklaşımlarının nasıl değiştiğini gözlemleyebiliriz:

* İlk satranç programları arama tabanlıydı – bir program, belirli bir sayıdaki sonraki hamleler için bir rakibin olası hamlelerini açıkça tahmin etmeye çalıştı ve birkaç hamlede elde edilebilecek optimal pozisyona dayalı olarak optimal bir hamle seçti. Bu, [alpha-beta budama](https://en.wikipedia.org/wiki/Alpha%E2%80%93beta_pruning) arama algoritmasının geliştirilmesine yol açtı.
* Arama stratejileri, oyunun sonuna doğru, arama alanı sınırlı bir dizi olası hamle ile sınırlı olduğunda iyi çalışır. Ancak, oyunun başında arama alanı çok büyüktür ve algoritma, insan oyuncular arasındaki mevcut maçlardan öğrenerek geliştirilebilir. Sonraki deneyler, programın oyundaki mevcut pozisyona çok benzer durumları bilgi tabanında aradığı [örnek tabanlı akıl yürütme](https://en.wikipedia.org/wiki/Case-based_reasoning) olarak adlandırılan yöntemi kullandı.
* İnsan oyuncuları yenen modern programlar, sinir ağları ve [pekiştirmeli öğrenme](https://en.wikipedia.org/wiki/Reinforcement_learning) üzerine kuruludur. Bu programlar, yalnızca uzun süre kendilerine karşı oynayarak ve kendi hatalarından öğrenerek oynamayı öğrenir – tıpkı insanların satranç öğrenirken yaptığı gibi. Ancak, bir bilgisayar programı çok daha kısa sürede çok daha fazla oyun oynayabilir ve bu nedenle çok daha hızlı öğrenebilir.

✅ AI tarafından oynanan diğer oyunlar hakkında biraz araştırma yapın.

Benzer şekilde, “konuşan programlar” (Turing testini geçebilecek türden) oluşturma yaklaşımının nasıl değiştiğini görebiliriz:

* Bu türden erken programlar, örneğin [Eliza](https://en.wikipedia.org/wiki/ELIZA), çok basit dilbilgisi kurallarına ve giriş cümlesinin bir soruya yeniden formüle edilmesine dayanıyordu.
* Modern asistanlar, Cortana, Siri veya Google Asistan gibi, konuşmayı metne dönüştürmek ve niyetimizi tanımak için Sinir ağlarını kullanan ve ardından gerekli eylemleri gerçekleştirmek için bazı akıl yürütme veya açık algoritmalar kullanan hibrit sistemlerdir.
* Gelecekte, diyalogu tamamen kendi başına ele alacak tam bir sinir tabanlı model bekleyebiliriz. Son zamanlardaki GPT ve [Turing-NLG](https://turing.microsoft.com/) sinir ağı ailesi bu konuda büyük başarılar göstermektedir.

<img alt="Turing testinin evrimi" src="images/turing-test-evol.png" width="70%"/>
> Görsel Dmitry Soshnikov tarafından, [fotoğraf](https://unsplash.com/photos/r8LmVbUKgns) [Marina Abrosimova](https://unsplash.com/@abrosimova_marina_foto) tarafından, Unsplash

## Son Dönem AI Araştırmaları

Sinir ağı araştırmalarındaki büyük büyüme, 2010 civarında, büyük halka açık veri setlerinin erişilebilir hale gelmesiyle başladı. Yaklaşık 14 milyon açıklamalı görüntü içeren [ImageNet](https://en.wikipedia.org/wiki/ImageNet) adlı büyük bir görüntü koleksiyonu, [ImageNet Büyük Ölçekli Görsel Tanıma Yarışması](https://image-net.org/challenges/LSVRC/) doğurdu.

![ILSVRC Doğruluk](../../../../lessons/1-Intro/images/ilsvrc.gif)

> Görsel [Dmitry Soshnikov](http://soshnikov.com) tarafından

2012 yılında, [Convolutional Neural Networks](../4-ComputerVision/07-ConvNets/README.md) ilk kez görüntü sınıflandırmada kullanıldı ve sınıflandırma hatalarında önemli bir düşüşe yol açtı (neredeyse %30'dan %16.4'e). 2015 yılında, Microsoft Research'ten ResNet mimarisi [insan seviyesinde doğruluk](https://doi.org/10.1109/ICCV.2015.123) elde etti.

O zamandan beri, Sinir Ağları birçok görevde çok başarılı bir performans sergiledi:

---

Yıl | İnsan Seviyesi Eşitlik Sağlandı
-----|--------
2015 | [Görüntü Sınıflandırma](https://doi.org/10.1109/ICCV.2015.123)
2016 | [Konuşma Tanıma](https://arxiv.org/abs/1610.05256)
2018 | [Otomatik Makine Çevirisi](https://arxiv.org/abs/1803.05567) (Çince'den İngilizce'ye)
2020 | [Görüntü Açıklama](https://arxiv.org/abs/2009.13682)

Son birkaç yılda, BERT ve GPT-3 gibi büyük dil modelleriyle büyük başarılar gördük. Bu, büyük ölçüde genel metin verilerinin bol miktarda bulunması sayesinde gerçekleşti. Bu veriler, modellerin metinlerin yapısını ve anlamını öğrenmesine, genel metin koleksiyonlarında önceden eğitilmesine ve ardından bu modellerin daha spesifik görevler için uzmanlaşmasına olanak tanıyor. Bu kursun ilerleyen bölümlerinde [Doğal Dil İşleme](../5-NLP/README.md) hakkında daha fazla bilgi edineceğiz.

## 🚀 Zorluk

İnternette bir tur yaparak, AI'nın en etkili şekilde nerede kullanıldığını düşündüğünüzü belirleyin. Bir haritalama uygulamasında mı, bir konuşmadan metne hizmette mi yoksa bir video oyununda mı? Sistemin nasıl oluşturulduğunu araştırın.

## [Ders sonrası test](https://ff-quizzes.netlify.app/en/ai/quiz/2)

## Gözden Geçirme ve Kendi Kendine Çalışma

AI ve ML tarihini gözden geçirmek için [bu dersi](https://github.com/microsoft/ML-For-Beginners/tree/main/1-Introduction/2-history-of-ML) okuyun. Bu dersin veya yukarıdaki dersin başındaki sketchnote'dan bir öğe seçin ve onun evrimini şekillendiren kültürel bağlamı daha iyi anlamak için daha derinlemesine araştırın.

**Görev**: [Game Jam](assignment.md)

---

