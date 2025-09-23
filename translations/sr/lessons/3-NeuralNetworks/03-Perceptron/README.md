<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "c34cbba802058b6fa267e1a294d4e510",
  "translation_date": "2025-09-23T14:44:55+00:00",
  "source_file": "lessons/3-NeuralNetworks/03-Perceptron/README.md",
  "language_code": "sr"
}
-->
# Увод у неуронске мреже: Перцептрон

## [Квиз пре предавања](https://ff-quizzes.netlify.app/en/ai/quiz/5)

Један од првих покушаја да се имплементира нешто слично модерној неуронској мрежи направио је Френк Розенблат из Корнел лабораторије за ваздухопловство 1957. године. То је била хардверска имплементација названа "Mark-1", дизајнирана да препозна примитивне геометријске фигуре, као што су троуглови, квадрати и кругови.

|      |      |
|--------------|-----------|
|<img src='images/Rosenblatt-wikipedia.jpg' alt='Frank Rosenblatt'/> | <img src='images/Mark_I_perceptron_wikipedia.jpg' alt='The Mark 1 Perceptron' />|

> Слике [са Википедије](https://en.wikipedia.org/wiki/Perceptron)

Улазна слика је била представљена низом од 20x20 фотоћелија, тако да је неуронска мрежа имала 400 улаза и један бинарни излаз. Једноставна мрежа је садржала један неурон, који се називао и **јединица логичког прага**. Тежине неуронске мреже су функционисале као потенциометри који су захтевали ручно подешавање током фазе тренинга.

> ✅ Потенциометар је уређај који омогућава кориснику да подеси отпор у колу.

> Њујорк Тајмс је у то време писао о перцептрону: *ембрион електронског рачунара за који [морнарица] очекује да ће моћи да хода, говори, види, пише, репродукује се и буде свестан свог постојања.*

## Модел перцептрона

Претпоставимо да имамо N карактеристика у нашем моделу, у ком случају би улазни вектор био вектор величине N. Перцептрон је модел за **бинарну класификацију**, односно може да разликује две класе улазних података. Претпоставићемо да за сваки улазни вектор x излаз нашег перцептрона буде или +1 или -1, у зависности од класе. Излаз ће се рачунати помоћу формуле:

y(x) = f(w<sup>T</sup>x)

где је f функција активације у облику степенасте функције.

<!-- img src="http://www.sciweavers.org/tex2img.php?eq=f%28x%29%20%3D%20%5Cbegin%7Bcases%7D%0A%20%20%20%20%20%20%20%20%20%2B1%20%26%20x%20%5Cgeq%200%20%5C%5C%0A%20%20%20%20%20%20%20%20%20-1%20%26%20x%20%3C%200%0A%20%20%20%20%20%20%20%5Cend%7Bcases%7D%20%5C%5C%0A&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0" align="center" border="0" alt="f(x) = \begin{cases} +1 & x \geq 0 \\ -1 & x < 0 \end{cases} \\" width="154" height="50" / -->
<img src="images/activation-func.png"/>

## Тренинг перцептрона

Да бисмо обучили перцептрон, потребно је да пронађемо вектор тежина w који класификује већину вредности исправно, односно резултира најмањом **грешком**. Ова грешка E је дефинисана **критеријумом перцептрона** на следећи начин:

E(w) = -&sum;w<sup>T</sup>x<sub>i</sub>t<sub>i</sub>

где:

* збир се узима за оне тачке података за тренинг i које резултирају погрешном класификацијом
* x<sub>i</sub> су улазни подаци, а t<sub>i</sub> је или -1 или +1 за негативне и позитивне примере, респективно.

Овај критеријум се сматра функцијом тежина w, и потребно је да га минимизирамо. Често се користи метода названа **градијентни спуст**, у којој почињемо са неким почетним тежинама w<sup>(0)</sup>, а затим на сваком кораку ажурирамо тежине према формули:

w<sup>(t+1)</sup> = w<sup>(t)</sup> - &eta;&nabla;E(w)

Овде је &eta; такозвана **стопа учења**, а &nabla;E(w) означава **градијент** E. Након што израчунамо градијент, добијамо:

w<sup>(t+1)</sup> = w<sup>(t)</sup> + &sum;&eta;x<sub>i</sub>t<sub>i</sub>

Алгоритам у Python-у изгледа овако:

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

## Закључак

У овом предавању сте научили о перцептрону, који је модел за бинарну класификацију, и како да га обучите користећи вектор тежина.

## 🚀 Изазов

Ако желите да покушате да направите свој перцептрон, пробајте [ову лабораторију на Microsoft Learn](https://docs.microsoft.com/en-us/azure/machine-learning/component-reference/two-class-averaged-perceptron?WT.mc_id=academic-77998-cacaste) која користи [Azure ML designer](https://docs.microsoft.com/en-us/azure/machine-learning/concept-designer?WT.mc_id=academic-77998-cacaste).

## [Квиз после предавања](https://ff-quizzes.netlify.app/en/ai/quiz/6)

## Преглед и самостално учење

Да бисте видели како можемо користити перцептрон за решавање једноставних проблема као и проблема из стварног живота, и да наставите са учењем - идите на [Perceptron](Perceptron.ipynb) бележницу.

Ево занимљивог [чланка о перцептронима](https://towardsdatascience.com/what-is-a-perceptron-basics-of-neural-networks-c4cfea20c590).

## [Задатак](lab/README.md)

У овом предавању смо имплементирали перцептрон за задатак бинарне класификације и користили га за класификацију између две руком писане цифре. У овој лабораторији, од вас се тражи да решите проблем класификације цифара у потпуности, односно да одредите која цифра највероватније одговара датој слици.

* [Упутства](lab/README.md)
* [Бележница](lab/PerceptronMultiClass.ipynb)

---

