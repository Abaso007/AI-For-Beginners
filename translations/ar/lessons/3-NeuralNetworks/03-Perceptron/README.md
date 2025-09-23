<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "0c37770bba4fff3c71dc00eb261ee61b",
  "translation_date": "2025-08-26T10:35:55+00:00",
  "source_file": "lessons/3-NeuralNetworks/03-Perceptron/README.md",
  "language_code": "ar"
}
-->
# مقدمة إلى الشبكات العصبية: بيرسيبترون

## [اختبار ما قبل المحاضرة](https://ff-quizzes.netlify.app/en/ai/quiz/5)

أحد أولى المحاولات لتطبيق شيء مشابه للشبكات العصبية الحديثة قام بها فرانك روزنبلات من مختبر كورنيل للطيران في عام 1957. كان ذلك عبارة عن تطبيق مادي يُسمى "Mark-1"، صُمم للتعرف على الأشكال الهندسية البدائية، مثل المثلثات والمربعات والدوائر.

|      |      |
|--------------|-----------|
|<img src='images/Rosenblatt-wikipedia.jpg' alt='فرانك روزنبلات'/> | <img src='images/Mark_I_perceptron_wikipedia.jpg' alt='بيرسيبترون Mark 1' />|

> الصور [من ويكيبيديا](https://en.wikipedia.org/wiki/Perceptron)

تم تمثيل الصورة المدخلة بمصفوفة من 20x20 خلية ضوئية، وبالتالي كان للشبكة العصبية 400 مدخل ومخرج ثنائي واحد. احتوت الشبكة البسيطة على خلية عصبية واحدة، تُعرف أيضًا باسم **وحدة منطق العتبة**. عملت أوزان الشبكة العصبية مثل المقاومات المتغيرة التي كانت تتطلب تعديلًا يدويًا أثناء مرحلة التدريب.

> ✅ المقاومة المتغيرة هي جهاز يسمح للمستخدم بضبط مقاومة الدائرة.

> كتبت صحيفة نيويورك تايمز عن البيرسيبترون في ذلك الوقت: *جنين حاسوب إلكتروني تتوقع [البحرية] أنه سيكون قادرًا على المشي، والتحدث، والرؤية، والكتابة، والتكاثر، وأن يكون واعيًا بوجوده.*

## نموذج البيرسيبترون

لنفترض أن لدينا N من الميزات في نموذجنا، وفي هذه الحالة سيكون متجه المدخلات عبارة عن متجه بحجم N. البيرسيبترون هو نموذج **تصنيف ثنائي**، أي يمكنه التمييز بين فئتين من بيانات المدخلات. سنفترض أنه لكل متجه مدخلات x سيكون مخرج البيرسيبترون إما +1 أو -1، اعتمادًا على الفئة. سيتم حساب المخرج باستخدام الصيغة:

y(x) = f(w<sup>T</sup>x)

حيث f هي دالة تفعيل من نوع الخطوة.

<!-- img src="http://www.sciweavers.org/tex2img.php?eq=f%28x%29%20%3D%20%5Cbegin%7Bcases%7D%0A%20%20%20%20%20%20%20%20%20%2B1%20%26%20x%20%5Cgeq%200%20%5C%5C%0A%20%20%20%20%20%20%20%20%20-1%20%26%20x%20%3C%200%0A%20%20%20%20%20%20%20%5Cend%7Bcases%7D%20%5C%5C%0A&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0" align="center" border="0" alt="f(x) = \begin{cases} +1 & x \geq 0 \\ -1 & x < 0 \end{cases} \\" width="154" height="50" / -->
<img src="images/activation-func.png"/>

## تدريب البيرسيبترون

لتدريب البيرسيبترون، نحتاج إلى إيجاد متجه أوزان w يصنف معظم القيم بشكل صحيح، أي يؤدي إلى أقل **خطأ**. يتم تعريف هذا الخطأ E بواسطة **معيار البيرسيبترون** بالطريقة التالية:

E(w) = -∑w<sup>T</sup>x<sub>i</sub>t<sub>i</sub>

حيث:

* يتم أخذ المجموع على نقاط بيانات التدريب i التي تؤدي إلى تصنيف خاطئ.
* x<sub>i</sub> هي بيانات المدخلات، وt<sub>i</sub> تكون إما -1 أو +1 للأمثلة السلبية والإيجابية على التوالي.

يُعتبر هذا المعيار دالة لأوزان w، ونحتاج إلى تقليلها. غالبًا ما يتم استخدام طريقة تُسمى **الانحدار التدريجي**، حيث نبدأ ببعض الأوزان الأولية w<sup>(0)</sup>، ثم نقوم في كل خطوة بتحديث الأوزان وفقًا للصيغة:

w<sup>(t+1)</sup> = w<sup>(t)</sup> - η∇E(w)

هنا η هو ما يُسمى **معدل التعلم**، و∇E(w) يُشير إلى **تدرج** E. بعد حساب التدرج، نحصل على:

w<sup>(t+1)</sup> = w<sup>(t)</sup> + ∑ηx<sub>i</sub>t<sub>i</sub>

يبدو الخوارزم في Python كما يلي:

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

## الخاتمة

في هذه الدرس، تعلمت عن البيرسيبترون، وهو نموذج تصنيف ثنائي، وكيفية تدريبه باستخدام متجه الأوزان.

## 🚀 تحدي

إذا كنت ترغب في محاولة بناء بيرسيبترون خاص بك، جرب [هذا المختبر على Microsoft Learn](https://docs.microsoft.com/en-us/azure/machine-learning/component-reference/two-class-averaged-perceptron?WT.mc_id=academic-77998-cacaste) الذي يستخدم [مصمم Azure ML](https://docs.microsoft.com/en-us/azure/machine-learning/concept-designer?WT.mc_id=academic-77998-cacaste).

## [اختبار ما بعد المحاضرة](https://ff-quizzes.netlify.app/en/ai/quiz/6)

## المراجعة والدراسة الذاتية

لرؤية كيفية استخدام البيرسيبترون لحل مشكلة بسيطة وكذلك مشاكل الحياة الواقعية، وللاستمرار في التعلم - انتقل إلى [دفتر البيرسيبترون](../../../../../lessons/3-NeuralNetworks/03-Perceptron/Perceptron.ipynb).

إليك مقالًا مثيرًا للاهتمام عن [البيرسيبترونات](https://towardsdatascience.com/what-is-a-perceptron-basics-of-neural-networks-c4cfea20c590
).

## [التكليف](lab/README.md)

في هذا الدرس، قمنا بتطبيق بيرسيبترون لمهمة تصنيف ثنائي، واستخدمناه لتصنيف بين رقمين مكتوبين بخط اليد. في هذا المختبر، يُطلب منك حل مشكلة تصنيف الأرقام بالكامل، أي تحديد الرقم الأكثر احتمالًا الذي يتوافق مع صورة معينة.

* [التعليمات](lab/README.md)
* [دفتر الملاحظات](../../../../../lessons/3-NeuralNetworks/03-Perceptron/lab/PerceptronMultiClass.ipynb)

**إخلاء المسؤولية**:  
تم ترجمة هذا المستند باستخدام خدمة الترجمة بالذكاء الاصطناعي [Co-op Translator](https://github.com/Azure/co-op-translator). بينما نسعى لتحقيق الدقة، يرجى العلم أن الترجمات الآلية قد تحتوي على أخطاء أو معلومات غير دقيقة. يجب اعتبار المستند الأصلي بلغته الأصلية المصدر الرسمي. للحصول على معلومات حاسمة، يُوصى بالاستعانة بترجمة بشرية احترافية. نحن غير مسؤولين عن أي سوء فهم أو تفسيرات خاطئة تنشأ عن استخدام هذه الترجمة.