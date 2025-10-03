<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "06ca1b0138e65b964481ae83275b270e",
  "translation_date": "2025-10-03T08:13:01+00:00",
  "source_file": "lessons/1-Intro/README.md",
  "language_code": "tr"
}
-->
# Yapay Zekaya Giriş

![Yapay Zekaya Giriş içeriğinin bir çizim özeti](../../../../translated_images/ai-intro.bf28d1ac4235881c096f0ffdb320ba4102940eafcca4e9d7a55a03914361f8f3.tr.png)

> Çizim notları: [Tomomi Imura](https://twitter.com/girlie_mac)

## [Ders öncesi test](https://ff-quizzes.netlify.app/en/ai/quiz/1)

**Yapay Zeka**, bilgisayarların insanlara özgü zeki davranışlar sergilemesini nasıl sağlayabileceğimizi inceleyen heyecan verici bir bilim dalıdır; örneğin, insanların iyi yaptığı şeyleri yapabilmek.

Başlangıçta, bilgisayarlar [Charles Babbage](https://en.wikipedia.org/wiki/Charles_Babbage) tarafından belirli bir prosedürü - bir algoritmayı - takip ederek sayılar üzerinde işlem yapmak için icat edildi. Modern bilgisayarlar, 19. yüzyılda önerilen orijinal modelden çok daha gelişmiş olsalar da, hala kontrollü hesaplama fikrini takip ediyor. Bu nedenle, bir hedefe ulaşmak için gereken adımların tam sırasını biliyorsak, bir bilgisayarı bir şey yapması için programlamak mümkündür.

![Bir kişinin fotoğrafı](../../../../translated_images/dsh_age.d212a30d4e54fb5f68b94a624aad64bc086124bcbbec9561ae5bd5da661e22d8.tr.png)

> Fotoğraf: [Vickie Soshnikova](http://twitter.com/vickievalerie)

> ✅ Bir kişinin fotoğrafından yaşını belirlemek, açıkça programlanamayacak bir görevdir, çünkü bunu yaparken kafamızda bir sayı belirlediğimizde nasıl yaptığımızı bilmiyoruz.

---

Ancak, açıkça nasıl çözüleceğini bilmediğimiz bazı görevler vardır. Örneğin, bir kişinin fotoğrafından yaşını belirlemeyi düşünün. Bunu yapmayı bir şekilde öğreniyoruz, çünkü farklı yaşlardaki birçok insan örneği gördük, ancak bunu nasıl yaptığımızı açıkça açıklayamıyoruz ve bilgisayarı bunu yapması için programlayamıyoruz. İşte tam da bu tür görevler **Yapay Zeka** (kısaca AI) için ilgi çekicidir.

✅ Bilgisayara devredebileceğiniz ve AI'dan faydalanabilecek bazı görevler düşünün. Finans, tıp ve sanat alanlarını göz önünde bulundurun - bu alanlar bugün AI'dan nasıl faydalanıyor?

## Zayıf AI ve Güçlü AI

Zayıf AI | Güçlü AI
---------------------------------------|-------------------------------------
Zayıf AI, belirli bir görev veya dar bir görev seti için tasarlanmış ve eğitilmiş AI sistemlerini ifade eder.|Güçlü AI veya Yapay Genel Zeka (AGI), insan seviyesinde zeka ve anlayışa sahip AI sistemlerini ifade eder.
Bu AI sistemleri genel olarak zeki değildir; önceden tanımlanmış bir görevde mükemmel performans gösterirler ancak gerçek bir anlayış veya bilinçten yoksundurlar.|Bu AI sistemleri, bir insanın yapabileceği herhangi bir entelektüel görevi yerine getirme, farklı alanlara uyum sağlama ve bir tür bilinç veya öz farkındalık sahibi olma yeteneğine sahiptir.
Zayıf AI örnekleri arasında Siri veya Alexa gibi sanal asistanlar, akış hizmetleri tarafından kullanılan öneri algoritmaları ve belirli müşteri hizmetleri görevleri için tasarlanmış sohbet botları bulunur.|Güçlü AI'ya ulaşmak, AI araştırmalarının uzun vadeli bir hedefidir ve AI sistemlerinin geniş bir görev ve bağlam yelpazesinde akıl yürütme, öğrenme, anlama ve uyum sağlama yeteneğini geliştirmeyi gerektirir.
Zayıf AI son derece özelleşmiştir ve dar alanının ötesinde insan benzeri bilişsel yeteneklere veya genel problem çözme yeteneklerine sahip değildir.|Güçlü AI şu anda teorik bir kavramdır ve hiçbir AI sistemi bu genel zeka seviyesine ulaşmamıştır.

Daha fazla bilgi için **[Yapay Genel Zeka](https://en.wikipedia.org/wiki/Artificial_general_intelligence)** (AGI) sayfasına bakabilirsiniz.

## Zekanın Tanımı ve Turing Testi

**[Zeka](https://en.wikipedia.org/wiki/Intelligence)** terimiyle uğraşırken karşılaşılan sorunlardan biri, bu terimin net bir tanımının olmamasıdır. Zekanın **soyut düşünme** veya **öz farkındalık** ile bağlantılı olduğunu iddia edebilirsiniz, ancak bunu doğru bir şekilde tanımlayamayız.

![Bir kedinin fotoğrafı](../../../../translated_images/photo-cat.8c8e8fb760ffe45725c5b9f6b0d954e9bf114475c01c55adf0303982851b7eae.tr.jpg)

> [Fotoğraf](https://unsplash.com/photos/75715CVEJhI): [Amber Kipp](https://unsplash.com/@sadmax) tarafından Unsplash'tan alınmıştır.

*Zeka* teriminin belirsizliğini görmek için şu soruyu yanıtlamayı deneyin: "Bir kedi zeki midir?" Farklı insanlar bu soruya farklı yanıtlar verme eğilimindedir, çünkü bu iddianın doğru olup olmadığını kanıtlayacak evrensel olarak kabul edilmiş bir test yoktur. Ve eğer olduğunu düşünüyorsanız - kedinizi bir IQ testine sokmayı deneyin...

✅ Zekayı nasıl tanımladığınızı bir dakika düşünün. Bir labirenti çözerek yiyeceğe ulaşabilen bir karga zeki midir? Bir çocuk zeki midir?

---

AGI'den bahsederken, gerçekten zeki bir sistem oluşturup oluşturmadığımızı anlamanın bir yoluna ihtiyacımız var. [Alan Turing](https://en.wikipedia.org/wiki/Alan_Turing), aynı zamanda bir zeka tanımı olarak da işlev gören bir yöntem önerdi: **[Turing Testi](https://en.wikipedia.org/wiki/Turing_test)**. Test, verilen bir sistemi doğal olarak zeki bir şeyle - gerçek bir insanla - karşılaştırır ve herhangi bir otomatik karşılaştırma bir bilgisayar programı tarafından atlatılabileceği için, bir insan sorgulayıcı kullanırız. Yani, bir insan, bir gerçek kişi ile bir bilgisayar sistemi arasındaki farkı metin tabanlı bir diyalogda ayırt edemezse - sistem zeki kabul edilir.

> St. Petersburg'da geliştirilen [Eugene Goostman](https://en.wikipedia.org/wiki/Eugene_Goostman) adlı bir sohbet botu, 2014 yılında Turing testini geçmeye yaklaşarak zekice bir kişilik hilesi kullandı. Bot, baştan 13 yaşında bir Ukraynalı çocuk olduğunu belirtti, bu da bilgi eksikliğini ve metindeki bazı tutarsızlıkları açıklıyordu. Bot, 5 dakikalık bir diyalogdan sonra yargıçların %30'unu insan olduğuna ikna etti, bu Turing'in 2000 yılına kadar bir makinenin geçebileceğine inandığı bir ölçüttü. Ancak, bunun zeki bir sistem oluşturduğumuz anlamına gelmediğini veya bir bilgisayar sisteminin insan sorgulayıcıyı kandırdığını anlamak önemlidir - sistem insanları kandırmadı, aksine botun yaratıcıları kandırdı!

✅ Hiç bir sohbet botunun insan olduğuna inanmanız için sizi kandırdığı oldu mu? Sizi nasıl ikna etti?

## Yapay Zekaya Yaklaşımlar

Bir bilgisayarın insan gibi davranmasını istiyorsak, bir şekilde bilgisayarın içinde düşünme biçimimizi modellememiz gerekir. Dolayısıyla, bir insanı zeki yapan şeyin ne olduğunu anlamaya çalışmamız gerekir.

> Bir makineye zeka programlayabilmek için, kendi karar verme süreçlerimizin nasıl çalıştığını anlamamız gerekir. Biraz kendinizi gözlemlediğinizde, bazı süreçlerin bilinçaltında gerçekleştiğini fark edeceksiniz – örneğin, bir kediyi bir köpekten ayırt edebiliriz, ancak bunu düşünmeden yaparız - diğer bazı süreçler ise akıl yürütmeyi içerir.

Bu soruna iki olası yaklaşım vardır:

Üstten Aşağı Yaklaşım (Sembolik Akıl Yürütme) | Alttan Yukarı Yaklaşım (Sinir Ağları)
---------------------------------------|-------------------------------------
Üstten aşağı yaklaşım, bir kişinin bir problemi çözmek için akıl yürütme biçimini modellemeye çalışır. Bu, bir insandan **bilgi** çıkarmayı ve bunu bilgisayar tarafından okunabilir bir biçimde temsil etmeyi içerir. Ayrıca, bilgisayar içinde **akıl yürütmeyi** modellemenin bir yolunu geliştirmemiz gerekir. | Alttan yukarı yaklaşım, insan beyninin yapısını, **nöronlar** adı verilen çok sayıda basit birimden oluşan bir yapıyı modellemeye çalışır. Her nöron, girdilerinin ağırlıklı bir ortalaması gibi davranır ve nöron ağını **eğitim verileri** sağlayarak faydalı problemleri çözmek için eğitebiliriz.

Zekaya yönelik başka olası yaklaşımlar da vardır:

* **Ortaya çıkan**, **Sinerjetik** veya **çoklu ajan yaklaşımı**, karmaşık zeki davranışların çok sayıda basit ajanların etkileşimiyle elde edilebileceği gerçeğine dayanır. [Evrimsel sibernetik](https://en.wikipedia.org/wiki/Global_brain#Evolutionary_cybernetics)'e göre, zeka daha basit, tepkisel davranışlardan *metasistem geçişi* sürecinde *ortaya çıkabilir*.

* **Evrimsel yaklaşım** veya **genetik algoritma**, evrim ilkelerine dayanan bir optimizasyon sürecidir.

Bu yaklaşımları kursun ilerleyen bölümlerinde ele alacağız, ancak şu anda iki ana yön üzerinde duracağız: üstten aşağı ve alttan yukarı.

### Üstten Aşağı Yaklaşım

**Üstten aşağı yaklaşımda**, akıl yürütmemizi modellemeye çalışırız. Çünkü akıl yürütürken düşüncelerimizi takip edebiliriz, bu süreci biçimlendirmeye ve bilgisayarın içine programlamaya çalışabiliriz. Buna **sembolik akıl yürütme** denir.

İnsanlar, karar verme süreçlerini yönlendiren bazı kurallara sahip olma eğilimindedir. Örneğin, bir doktor bir hastayı teşhis ederken, kişinin ateşi olduğunu ve dolayısıyla vücutta bir iltihaplanma olabileceğini fark edebilir. Doktor, belirli bir probleme büyük bir kural seti uygulayarak nihai teşhise ulaşabilir.

Bu yaklaşım büyük ölçüde **bilgi temsili** ve **akıl yürütme**ye dayanır. Bir insan uzmandan bilgi çıkarmak en zor kısım olabilir, çünkü bir doktor birçok durumda belirli bir teşhise neden ulaştığını tam olarak bilmeyebilir. Bazen çözüm açık düşünme olmadan kafasında belirir. Bir kişinin fotoğrafından yaşını belirlemek gibi bazı görevler, bilgiyi manipüle etmeye indirgenemez.

### Alttan Yukarı Yaklaşım

Alternatif olarak, beynimizdeki en basit öğeleri – bir nöronu – modellemeye çalışabiliriz. Bilgisayarın içinde **yapay bir sinir ağı** oluşturabilir ve ardından ona örnekler vererek problemleri çözmeyi öğretmeye çalışabiliriz. Bu süreç, yeni doğmuş bir çocuğun çevresini gözlem yaparak öğrenmesine benzer.

✅ Bebeklerin nasıl öğrendiği hakkında biraz araştırma yapın. Bir bebeğin beyninin temel öğeleri nelerdir?

> | Peki ya ML?         |      |
> |--------------|-----------|
> | Bir bilgisayarın bazı verilere dayanarak bir problemi çözmeyi öğrenmesine dayanan Yapay Zeka'nın bir kısmına **Makine Öğrenimi** denir. Bu kursta klasik makine öğrenimini ele almayacağız - sizi ayrı bir [Makine Öğrenimi için Başlangıç](http://aka.ms/ml-beginners) müfredatına yönlendiriyoruz. |   ![ML için Başlangıç](../../../../translated_images/ml-for-beginners.9e4fed176fd5817d7d1f7d358302515186579cbf09b2a6c5bd8092b345da7f22.tr.png)    |

## Yapay Zekanın Kısa Tarihi

Yapay Zeka, yirminci yüzyılın ortalarında bir alan olarak başladı. Başlangıçta, sembolik akıl yürütme yaygın bir yaklaşımdı ve sınırlı problem alanlarında bir uzman gibi davranabilen bilgisayar programları olan uzman sistemler gibi önemli başarılara yol açtı. Ancak, bu yaklaşımın iyi ölçeklenmediği kısa sürede anlaşıldı. Bir uzmandan bilgi çıkarmak, bunu bir bilgisayarda temsil etmek ve bilgi tabanını doğru tutmak çok karmaşık ve birçok durumda pratik olmayan bir görev olduğu ortaya çıktı. Bu, 1970'lerde [AI Kışı](https://en.wikipedia.org/wiki/AI_winter) olarak adlandırılan döneme yol açtı.

<img alt="Yapay Zekanın Kısa Tarihi" src="../../../../translated_images/history-of-ai.7e83efa70b537f5a0264357672b0884cf3a220fbafe35c65d70b2c3805f7bf5e.tr.png" width="70%"/>

> Görsel: [Dmitry Soshnikov](http://soshnikov.com)

Zamanla, bilgisayar kaynakları ucuzladı ve daha fazla veri erişilebilir hale geldi, bu nedenle sinir ağı yaklaşımları, insanlarla rekabet edebilecek performans göstermeye başladı. Son on yılda, Yapay Zeka terimi çoğunlukla Sinir Ağları ile eş anlamlı olarak kullanıldı, çünkü duyduğumuz Yapay Zeka başarılarının çoğu bunlara dayanıyor.

Satranç oynayan bir bilgisayar programı oluşturma yaklaşımlarının nasıl değiştiğini gözlemleyebiliriz:

* İlk satranç programları arama tabanlıydı – bir program, belirli bir sayıda sonraki hamle için bir rakibin olası hamlelerini açıkça tahmin etmeye çalıştı ve birkaç hamlede elde edilebilecek optimal pozisyona dayalı olarak optimal hamleyi seçti. Bu, [alpha-beta budama](https://en.wikipedia.org/wiki/Alpha%E2%80%93beta_pruning) arama algoritmasının geliştirilmesine yol açtı.
* Arama stratejileri, oyunun sonuna doğru, arama alanı sınırlı bir olası hamle sayısıyla sınırlı olduğunda iyi çalışır. Ancak, oyunun başında arama alanı çok büyüktür ve algoritma, insan oyuncular arasındaki mevcut maçlardan öğrenerek geliştirilebilir. Sonraki deneyler, programın oyundaki mevcut pozisyona çok benzer durumları bilgi tabanında aradığı [durum tabanlı akıl yürütme](https://en.wikipedia.org/wiki/Case-based_reasoning) olarak adlandırılan yöntemi kullandı.
* İnsan oyuncuları yenen modern programlar, sinir ağları ve [pekiştirmeli öğrenme](https://en.wikipedia.org/wiki/Reinforcement_learning) üzerine kuruludur; burada programlar yalnızca uzun süre kendilerine karşı oynayarak ve kendi hatalarından öğrenerek oynamayı öğrenir – tıpkı insanların satranç oynamayı öğrenirken yaptığı gibi. Ancak, bir bilgisayar programı çok daha kısa sürede çok daha fazla oyun oynayabilir ve böylece çok daha hızlı öğrenebilir.

✅ AI tarafından oynanan diğer oyunlar hakkında biraz araştırma yapın.

Benzer şekilde, "konuşan programlar" (Turing testini geçebilecek olanlar) oluşturma yaklaşımının nasıl değiştiğini görebiliriz:

* Bu tür erken programlar, örneğin [Eliza](https://en.wikipedia.org/wiki/ELIZA), çok basit dilbilgisi kurallarına ve giriş cümlesinin bir soruya yeniden biçimlendirilmesine dayanıyordu.
* Cortana, Siri veya Google Assistant gibi modern asistanlar, konuşmayı metne dönüştürmek ve niyetimizi tanımak için Sinir ağlarını kullanan ve ardından gerekli eylemleri gerçekleştirmek için bazı akıl yürütme veya açık algoritmalar kullanan hibrit sistemlerdir.
* Gelecekte, diyaloğu tamamen kendi başına yönetebilecek tam bir sinir tabanlı model bekleyebiliriz. Son zamanlardaki GPT ve [Turing-NLG](https://www.microsoft.com/research/blog/turing-nlg-a-17-billion-parameter-language-model-by-microsoft) sinir ağı ailesi bu konuda büyük başarılar göstermektedir.

<img alt="Turing testinin evrimi" src="../../../../translated_images/turing-test-evol.4184696701293ead6de6e6441a659c62f0b119b342456987f531005f43be0b6d.tr.png" width="70%"/>
> Görsel Dmitry Soshnikov tarafından, [fotoğraf](https://unsplash.com/photos/r8LmVbUKgns) [Marina Abrosimova](https://unsplash.com/@abrosimova_marina_foto) tarafından, Unsplash

## Son Dönem AI Araştırmaları

Sinir ağı araştırmalarındaki büyük büyüme, yaklaşık 2010 yılında, büyük halka açık veri setlerinin erişilebilir hale gelmesiyle başladı. Yaklaşık 14 milyon açıklamalı görüntü içeren [ImageNet](https://en.wikipedia.org/wiki/ImageNet) adlı büyük bir görüntü koleksiyonu, [ImageNet Büyük Ölçekli Görsel Tanıma Yarışması](https://image-net.org/challenges/LSVRC/) doğurdu.

![ILSVRC Doğruluk](../../../../lessons/1-Intro/images/ilsvrc.gif)

> Görsel [Dmitry Soshnikov](http://soshnikov.com) tarafından

2012 yılında, [Convolutional Neural Networks](../4-ComputerVision/07-ConvNets/README.md) ilk kez görüntü sınıflandırmada kullanıldı ve bu, sınıflandırma hatalarında önemli bir düşüşe yol açtı (neredeyse %30'dan %16.4'e). 2015 yılında, Microsoft Research'ten ResNet mimarisi [insan seviyesinde doğruluk](https://doi.org/10.1109/ICCV.2015.123) elde etti.

O zamandan beri, Sinir Ağları birçok görevde çok başarılı bir performans sergiledi:

---

Yıl | İnsan Seviyesi Eşitlik Sağlandı
-----|--------
2015 | [Görüntü Sınıflandırma](https://doi.org/10.1109/ICCV.2015.123)
2016 | [Konuşma Tanıma](https://arxiv.org/abs/1610.05256)
2018 | [Otomatik Makine Çevirisi](https://arxiv.org/abs/1803.05567) (Çince-İngilizce)
2020 | [Görüntü Açıklama](https://arxiv.org/abs/2009.13682)

Son birkaç yılda, BERT ve GPT-3 gibi büyük dil modelleriyle büyük başarılar gördük. Bu, büyük ölçüde genel metin verilerinin bol miktarda bulunması sayesinde gerçekleşti. Bu veriler, modellerin metinlerin yapısını ve anlamını öğrenmesine, genel metin koleksiyonlarında önceden eğitilmesine ve ardından bu modellerin daha spesifik görevler için özelleştirilmesine olanak tanıyor. Bu kursun ilerleyen bölümlerinde [Doğal Dil İşleme](../5-NLP/README.md) hakkında daha fazla bilgi edineceğiz.

## 🚀 Zorluk

İnternette bir tur yaparak, AI'nin en etkili şekilde nerede kullanıldığını düşündüğünüzü belirleyin. Bir haritalama uygulamasında mı, bir konuşmadan metne hizmette mi yoksa bir video oyununda mı? Sistemin nasıl inşa edildiğini araştırın.

## [Ders sonrası test](https://ff-quizzes.netlify.app/en/ai/quiz/2)

## Gözden Geçirme ve Kendi Kendine Çalışma

AI ve ML tarihini gözden geçirmek için [bu dersi](https://github.com/microsoft/ML-For-Beginners/tree/main/1-Introduction/2-history-of-ML) okuyun. Bu dersin veya yukarıdaki dersin başındaki sketchnote'dan bir öğe seçin ve onun evrimini şekillendiren kültürel bağlamı daha iyi anlamak için daha derinlemesine araştırın.

**Ödev**: [Game Jam](assignment.md)

---

**Feragatname**:  
Bu belge, AI çeviri hizmeti [Co-op Translator](https://github.com/Azure/co-op-translator) kullanılarak çevrilmiştir. Doğruluğu sağlamak için çaba göstersek de, otomatik çevirilerin hata veya yanlışlık içerebileceğini lütfen unutmayın. Belgenin orijinal dili, yetkili kaynak olarak kabul edilmelidir. Kritik bilgiler için profesyonel insan çevirisi önerilir. Bu çevirinin kullanımından kaynaklanan yanlış anlamalar veya yanlış yorumlamalar için sorumluluk kabul edilmez.