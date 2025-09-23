<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "c34cbba802058b6fa267e1a294d4e510",
  "translation_date": "2025-09-23T07:10:15+00:00",
  "source_file": "lessons/3-NeuralNetworks/03-Perceptron/README.md",
  "language_code": "mr"
}
-->
# न्यूरल नेटवर्क्सची ओळख: परसेप्ट्रॉन

## [पूर्व-व्याख्यान प्रश्नमंजुषा](https://ff-quizzes.netlify.app/en/ai/quiz/5)

आधुनिक न्यूरल नेटवर्कसारखे काहीतरी अंमलात आणण्याचा पहिला प्रयत्न 1957 मध्ये कॉर्नेल एरोनॉटिकल लॅबोरेटरीचे फ्रँक रोझनब्लाट यांनी केला. हे "मार्क-1" नावाचे हार्डवेअर होते, ज्याचे उद्दिष्ट त्रिकोण, चौकोन आणि वर्तुळ यांसारख्या प्राथमिक भूमितीय आकृत्या ओळखणे होते.

|      |      |
|--------------|-----------|
|<img src='images/Rosenblatt-wikipedia.jpg' alt='Frank Rosenblatt'/> | <img src='images/Mark_I_perceptron_wikipedia.jpg' alt='The Mark 1 Perceptron' />|

> प्रतिमा [विकिपीडियावरून](https://en.wikipedia.org/wiki/Perceptron)

इनपुट प्रतिमा 20x20 फोटोसेल अ‍ॅरेद्वारे दर्शवली जात होती, त्यामुळे न्यूरल नेटवर्कमध्ये 400 इनपुट्स आणि एक बायनरी आउटपुट होते. साध्या नेटवर्कमध्ये एक न्यूरॉन होता, ज्याला **थ्रेशोल्ड लॉजिक युनिट** असेही म्हणतात. न्यूरल नेटवर्कचे वजन पोटेंशिओमीटरसारखे कार्य करत होते, ज्याला प्रशिक्षणाच्या टप्प्यात मॅन्युअली समायोजित करावे लागले.

> ✅ पोटेंशिओमीटर म्हणजे सर्किटचा प्रतिकार समायोजित करण्यासाठी वापरले जाणारे उपकरण.

> त्या काळात न्यूयॉर्क टाइम्सने परसेप्ट्रॉनबद्दल लिहिले: *एक इलेक्ट्रॉनिक संगणकाचे गर्भ, ज्याची [नौदलाला] अपेक्षा आहे की तो चालेल, बोलेल, पाहील, लिहील, स्वतःची पुनरुत्पत्ती करेल आणि त्याच्या अस्तित्वाची जाणीव ठेवेल.*

## परसेप्ट्रॉन मॉडेल

समजा आपल्या मॉडेलमध्ये N वैशिष्ट्ये आहेत, अशा परिस्थितीत इनपुट व्हेक्टर N आकाराचा व्हेक्टर असेल. परसेप्ट्रॉन हा **बायनरी वर्गीकरण** मॉडेल आहे, म्हणजेच तो इनपुट डेटाच्या दोन वर्गांमध्ये फरक करू शकतो. आपण गृहीत धरू की प्रत्येक इनपुट व्हेक्टर x साठी आमच्या परसेप्ट्रॉनचा आउटपुट +1 किंवा -1 असेल, वर्गावर अवलंबून. आउटपुट खालील सूत्राद्वारे गणना केली जाईल:

y(x) = f(w<sup>T</sup>x)

जिथे f हा एक स्टेप अ‍ॅक्टिवेशन फंक्शन आहे

<!-- img src="http://www.sciweavers.org/tex2img.php?eq=f%28x%29%20%3D%20%5Cbegin%7Bcases%7D%0A%20%20%20%20%20%20%20%20%20%2B1%20%26%20x%20%5Cgeq%200%20%5C%5C%0A%20%20%20%20%20%20%20%20%20-1%20%26%20x%20%3C%200%0A%20%20%20%20%20%20%20%5Cend%7Bcases%7D%20%5C%5C%0A&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0" align="center" border="0" alt="f(x) = \begin{cases} +1 & x \geq 0 \\ -1 & x < 0 \end{cases} \\" width="154" height="50" / -->
<img src="images/activation-func.png"/>

## परसेप्ट्रॉनचे प्रशिक्षण

परसेप्ट्रॉनचे प्रशिक्षण घेण्यासाठी आपल्याला असे वजन व्हेक्टर w शोधावे लागेल जे बहुतेक मूल्ये योग्यरित्या वर्गीकृत करते, म्हणजेच सर्वात कमी **त्रुटी** निर्माण करते. ही त्रुटी E खालीलप्रमाणे **परसेप्ट्रॉन निकष**द्वारे परिभाषित केली जाते:

E(w) = -&sum;w<sup>T</sup>x<sub>i</sub>t<sub>i</sub>

जिथे:

* योग त्या प्रशिक्षण डेटा पॉइंट्स i वर घेतला जातो ज्यामुळे चुकीचे वर्गीकरण होते
* x<sub>i</sub> म्हणजे इनपुट डेटा, आणि t<sub>i</sub> हे नकारात्मक आणि सकारात्मक उदाहरणांसाठी अनुक्रमे -1 किंवा +1 आहे.

हा निकष वजन w च्या फंक्शन म्हणून विचार केला जातो, आणि आपल्याला त्याचे **कमीकरण** करायचे आहे. अनेकदा, **ग्रेडियंट डिसेंट** नावाची पद्धत वापरली जाते, ज्यामध्ये आपण काही प्रारंभिक वजन w<sup>(0)</sup> सह सुरुवात करतो आणि नंतर प्रत्येक टप्प्यावर खालील सूत्रानुसार वजन अद्यतनित करतो:

w<sup>(t+1)</sup> = w<sup>(t)</sup> - &eta;&nabla;E(w)

इथे &eta; म्हणजे **लर्निंग रेट**, आणि &nabla;E(w) म्हणजे E चा **ग्रेडियंट**. ग्रेडियंटची गणना केल्यानंतर, आपल्याला मिळते:

w<sup>(t+1)</sup> = w<sup>(t)</sup> + &sum;&eta;x<sub>i</sub>t<sub>i</sub>

Python मधील अल्गोरिदम असे दिसते:

```python
def train(positive_examples, negative_examples, num_iterations = 100, eta = 1):

    weights = [0,0,0] # Initialize weights (almost randomly :)
        
    for i in range(num_iterations):
        pos = random.choice(positive_examples)
        neg = random.choice(negative_examples)

        z = np.dot(pos, weights) # compute perceptron output
        if z < 0: # positive example classified as negative
            weights = weights + eta*weights.shape

        z  = np.dot(neg, weights)
        if z >= 0: # negative example classified as positive
            weights = weights - eta*weights.shape

    return weights
```

## निष्कर्ष

या धड्यात, तुम्ही परसेप्ट्रॉनबद्दल शिकले, जो एक बायनरी वर्गीकरण मॉडेल आहे, आणि वजन व्हेक्टर वापरून त्याचे प्रशिक्षण कसे द्यायचे ते शिकले.

## 🚀 आव्हान

जर तुम्हाला स्वतःचा परसेप्ट्रॉन तयार करण्याचा प्रयत्न करायचा असेल, तर [Microsoft Learn](https://docs.microsoft.com/en-us/azure/machine-learning/component-reference/two-class-averaged-perceptron?WT.mc_id=academic-77998-cacaste) वरील [हा प्रयोग](https://docs.microsoft.com/en-us/azure/machine-learning/concept-designer?WT.mc_id=academic-77998-cacaste) वापरून पहा, जो [Azure ML designer](https://docs.microsoft.com/en-us/azure/machine-learning/concept-designer?WT.mc_id=academic-77998-cacaste) वापरतो.

## [व्याख्यानानंतरची प्रश्नमंजुषा](https://ff-quizzes.netlify.app/en/ai/quiz/6)

## पुनरावलोकन आणि स्व-अभ्यास

परसेप्ट्रॉनचा वापर करून खेळण्याच्या समस्यांचे तसेच वास्तविक जीवनातील समस्यांचे निराकरण कसे करता येईल हे पाहण्यासाठी आणि शिकणे सुरू ठेवण्यासाठी [Perceptron](Perceptron.ipynb) नोटबुककडे जा.

परसेप्ट्रॉनबद्दल एक मनोरंजक [लेख](https://towardsdatascience.com/what-is-a-perceptron-basics-of-neural-networks-c4cfea20c590) देखील आहे.

## [असाइनमेंट](lab/README.md)

या धड्यात, आपण बायनरी वर्गीकरण कार्यासाठी परसेप्ट्रॉन अंमलात आणला आहे, आणि आपण दोन हस्तलिखित अंकांमध्ये वर्गीकरण करण्यासाठी त्याचा वापर केला आहे. या प्रयोगात, तुम्हाला अंक वर्गीकरणाची समस्या पूर्णपणे सोडवायची आहे, म्हणजे दिलेल्या प्रतिमेसाठी कोणता अंक सर्वात जास्त शक्यता आहे ते ठरवायचे आहे.

* [सूचना](lab/README.md)
* [नोटबुक](lab/PerceptronMultiClass.ipynb)

---

