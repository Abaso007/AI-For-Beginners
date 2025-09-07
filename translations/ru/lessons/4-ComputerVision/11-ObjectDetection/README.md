<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "d85c8b08f6d1b48fd7f35b99f93c1138",
  "translation_date": "2025-08-26T06:40:49+00:00",
  "source_file": "lessons/4-ComputerVision/11-ObjectDetection/README.md",
  "language_code": "ru"
}
-->
# Обнаружение объектов

Модели классификации изображений, с которыми мы работали до сих пор, принимали изображение и выдавали категориальный результат, например, класс "цифра" в задаче MNIST. Однако во многих случаях нам недостаточно просто знать, что на изображении есть объекты — мы хотим определить их точное местоположение. Именно этим занимается **обнаружение объектов**.

## [Тест перед лекцией](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/111)

![Обнаружение объектов](../../../../../translated_images/Screen_Shot_2016-11-17_at_11.14.54_AM.b4bb3769353287be1b905373ed9c858102c054b16e4595c76ec3f7bba0feb549.ru.png)

> Изображение с [веб-сайта YOLO v2](https://pjreddie.com/darknet/yolov2/)

## Простой подход к обнаружению объектов

Предположим, мы хотим найти кошку на изображении. Очень простой подход к обнаружению объектов может быть следующим:

1. Разбить изображение на множество плиток.
2. Запустить классификацию изображений для каждой плитки.
3. Те плитки, которые дают достаточно высокую активацию, можно считать содержащими искомый объект.

![Простое обнаружение объектов](../../../../../translated_images/naive-detection.e7f1ba220ccd08c68a2ea8e06a7ed75c3fcc738c2372f9e00b7f4299a8659c01.ru.png)

> *Изображение из [учебной тетради](../../../../../lessons/4-ComputerVision/11-ObjectDetection/ObjectDetection-TF.ipynb)*

Однако этот подход далек от идеала, так как он позволяет алгоритму лишь приблизительно определить границы объекта. Для более точного определения местоположения необходимо использовать **регрессию**, чтобы предсказать координаты ограничивающих рамок — а для этого нужны специализированные наборы данных.

## Регрессия для обнаружения объектов

[Этот блог](https://towardsdatascience.com/object-detection-with-neural-networks-a4e2c46b4491) предлагает отличное введение в обнаружение форм.

## Наборы данных для обнаружения объектов

Для этой задачи вы можете встретить следующие наборы данных:

* [PASCAL VOC](http://host.robots.ox.ac.uk/pascal/VOC/) — 20 классов.
* [COCO](http://cocodataset.org/#home) — Common Objects in Context. 80 классов, ограничивающие рамки и маски сегментации.

![COCO](../../../../../translated_images/coco-examples.71bc60380fa6cceb7caad48bd09e35b6028caabd363aa04fee89c414e0870e86.ru.jpg)

## Метрики для обнаружения объектов

### Пересечение над объединением (IoU)

Если для классификации изображений легко измерить, насколько хорошо работает алгоритм, то для обнаружения объектов нужно оценивать как правильность класса, так и точность предсказания местоположения ограничивающей рамки. Для последнего используется метрика **Пересечение над объединением** (IoU), которая измеряет, насколько хорошо две рамки (или две произвольные области) перекрываются.

![IoU](../../../../../translated_images/iou_equation.9a4751d40fff4e119ecd0a7bcca4e71ab1dc83e0d4f2a0d66ff0859736f593cf.ru.png)

> *Рисунок 2 из [этого отличного блога о IoU](https://pyimagesearch.com/2016/11/07/intersection-over-union-iou-for-object-detection/)*

Идея проста — мы делим площадь пересечения двух фигур на площадь их объединения. Для двух идентичных областей IoU будет равен 1, а для полностью разобщенных областей — 0. В остальных случаях значение будет варьироваться от 0 до 1. Обычно учитываются только те ограничивающие рамки, для которых IoU превышает определенное значение.

### Средняя точность (Average Precision)

Предположим, мы хотим измерить, насколько хорошо распознается определенный класс объектов $C$. Для этого используется метрика **Средняя точность**, которая рассчитывается следующим образом:

1. Рассматривается кривая точности-отзыва, показывающая точность в зависимости от порогового значения обнаружения (от 0 до 1).
2. В зависимости от порога мы получаем больше или меньше объектов, обнаруженных на изображении, и разные значения точности и отзыва.
3. Кривая выглядит следующим образом:

<img src="https://github.com/shwars/NeuroWorkshop/raw/master/images/ObjDetectionPrecisionRecall.png"/>

> *Изображение из [NeuroWorkshop](http://github.com/shwars/NeuroWorkshop)*

Средняя точность для данного класса $C$ — это площадь под этой кривой. Более точно, ось отзыва обычно делится на 10 частей, и точность усредняется по всем этим точкам:

$$
AP = {1\over11}\sum_{i=0}^{10}\mbox{Precision}(\mbox{Recall}={i\over10})
$$

### AP и IoU

Мы рассматриваем только те обнаружения, для которых IoU превышает определенное значение. Например, в наборе данных PASCAL VOC обычно предполагается $\mbox{IoU Threshold} = 0.5$, а в COCO AP измеряется для разных значений $\mbox{IoU Threshold}$.

<img src="https://github.com/shwars/NeuroWorkshop/raw/master/images/ObjDetectionPrecisionRecallIoU.png"/>

> *Изображение из [NeuroWorkshop](http://github.com/shwars/NeuroWorkshop)*

### Средняя средняя точность (mAP)

Основная метрика для обнаружения объектов называется **Средняя средняя точность** или **mAP**. Это значение средней точности, усредненное по всем классам объектов, а иногда также по $\mbox{IoU Threshold}$. Более подробно процесс расчета **mAP** описан
[в этом блоге](https://medium.com/@timothycarlen/understanding-the-map-evaluation-metric-for-object-detection-a07fe6962cf3), а также [здесь с примерами кода](https://gist.github.com/tarlen5/008809c3decf19313de216b9208f3734).

## Различные подходы к обнаружению объектов

Существует два основных класса алгоритмов обнаружения объектов:

* **Сети предложений регионов** (R-CNN, Fast R-CNN, Faster R-CNN). Основная идея заключается в генерации **регионов интереса** (ROI) и запуске CNN по ним, чтобы найти максимальную активацию. Это немного похоже на простой подход, за исключением того, что ROI генерируются более умным способом. Одним из основных недостатков таких методов является их медлительность, так как требуется множество проходов классификатора CNN по изображению.
* **Однопроходные** методы (YOLO, SSD, RetinaNet). В этих архитектурах сеть спроектирована так, чтобы предсказывать как классы, так и ROI за один проход.

### R-CNN: CNN на основе регионов

[R-CNN](http://islab.ulsan.ac.kr/files/announcement/513/rcnn_pami.pdf) использует [Selective Search](http://www.huppelen.nl/publications/selectiveSearchDraft.pdf) для генерации иерархической структуры регионов ROI, которые затем проходят через CNN для извлечения признаков, SVM-классификаторы для определения класса объекта и линейную регрессию для определения координат *ограничивающей рамки*. [Официальная статья](https://arxiv.org/pdf/1506.01497v1.pdf)

![RCNN](../../../../../translated_images/rcnn1.cae407020dfb1d1fb572656e44f75cd6c512cc220591c116c506652c10e47f26.ru.png)

> *Изображение из van de Sande et al. ICCV’11*

![RCNN-1](../../../../../translated_images/rcnn2.2d9530bb83516484ec65b250c22dbf37d3d23244f32864ebcb91d98fe7c3112c.ru.png)

> *Изображения из [этого блога](https://towardsdatascience.com/r-cnn-fast-r-cnn-faster-r-cnn-yolo-object-detection-algorithms-36d53571365e)*

### F-RCNN - Fast R-CNN

Этот подход похож на R-CNN, но регионы определяются после применения сверточных слоев.

![FRCNN](../../../../../translated_images/f-rcnn.3cda6d9bb41888754037d2d9763e2298a96de5d9bc2a21db3147357aa5da9b1a.ru.png)

> Изображение из [официальной статьи](https://www.cv-foundation.org/openaccess/content_iccv_2015/papers/Girshick_Fast_R-CNN_ICCV_2015_paper.pdf), [arXiv](https://arxiv.org/pdf/1504.08083.pdf), 2015

### Faster R-CNN

Основная идея этого подхода заключается в использовании нейронной сети для предсказания ROI — так называемой *сети предложений регионов* (Region Proposal Network). [Статья](https://arxiv.org/pdf/1506.01497.pdf), 2016

![FasterRCNN](../../../../../translated_images/faster-rcnn.8d46c099b87ef30ab2ea26dbc4bdd85b974a57ba8eb526f65dc4cd0a4711de30.ru.png)

> Изображение из [официальной статьи](https://arxiv.org/pdf/1506.01497.pdf)

### R-FCN: Полностью сверточная сеть на основе регионов

Этот алгоритм еще быстрее, чем Faster R-CNN. Основная идея следующая:

1. Извлекаем признаки с помощью ResNet-101.
2. Признаки обрабатываются **Position-Sensitive Score Map**. Каждый объект из $C$ классов делится на $k\times k$ регионов, и сеть обучается предсказывать части объектов.
3. Для каждой части из $k\times k$ регионов все сети голосуют за классы объектов, и выбирается класс объекта с максимальным количеством голосов.

![r-fcn image](../../../../../translated_images/r-fcn.13eb88158b99a3da50fa2787a6be5cb310d47f0e9655cc93a1090dc7aab338d1.ru.png)

> Изображение из [официальной статьи](https://arxiv.org/abs/1605.06409)

### YOLO - You Only Look Once

YOLO — это алгоритм реального времени с одним проходом. Основная идея следующая:

 * Изображение делится на $S\times S$ регионы.
 * Для каждого региона **CNN** предсказывает $n$ возможных объектов, координаты *ограничивающей рамки* и *уверенность*=*вероятность* * IoU.

 ![YOLO](../../../../../translated_images/yolo.a2648ec82ee8bb4ea27537677adb482fd4b733ca1705c561b6a24a85102dced5.ru.png)

> Изображение из [официальной статьи](https://arxiv.org/abs/1506.02640)

### Другие алгоритмы

* RetinaNet: [официальная статья](https://arxiv.org/abs/1708.02002)
   - [Реализация на PyTorch в Torchvision](https://pytorch.org/vision/stable/_modules/torchvision/models/detection/retinanet.html)
   - [Реализация на Keras](https://github.com/fizyr/keras-retinanet)
   - [Обнаружение объектов с RetinaNet](https://keras.io/examples/vision/retinanet/) в примерах Keras
* SSD (Single Shot Detector): [официальная статья](https://arxiv.org/abs/1512.02325)

## ✍️ Упражнения: Обнаружение объектов

Продолжите обучение в следующей тетради:

[ObjectDetection.ipynb](../../../../../lessons/4-ComputerVision/11-ObjectDetection/ObjectDetection.ipynb)

## Заключение

В этом уроке вы познакомились с различными способами обнаружения объектов!

## 🚀 Задание

Прочитайте эти статьи и тетради о YOLO и попробуйте их самостоятельно:

* [Хороший блог](https://www.analyticsvidhya.com/blog/2018/12/practical-guide-object-detection-yolo-framewor-python/) о YOLO
 * [Официальный сайт](https://pjreddie.com/darknet/yolo/)
 * YOLO: [Реализация на Keras](https://github.com/experiencor/keras-yolo2), [пошаговая тетрадь](https://github.com/experiencor/basic-yolo-keras/blob/master/Yolo%20Step-by-Step.ipynb)
 * YOLO v2: [Реализация на Keras](https://github.com/experiencor/keras-yolo2), [пошаговая тетрадь](https://github.com/experiencor/keras-yolo2/blob/master/Yolo%20Step-by-Step.ipynb)

## [Тест после лекции](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/211)

## Обзор и самостоятельное изучение

* [Обнаружение объектов](https://tjmachinelearning.com/lectures/1718/obj/) от Нихила Сарданы
* [Хорошее сравнение алгоритмов обнаружения объектов](https://lilianweng.github.io/lil-log/2018/12/27/object-detection-part-4.html)
* [Обзор алгоритмов глубокого обучения для обнаружения объектов](https://medium.com/comet-app/review-of-deep-learning-algorithms-for-object-detection-c1f3d437b852)
* [Пошаговое введение в основные алгоритмы обнаружения объектов](https://www.analyticsvidhya.com/blog/2018/10/a-step-by-step-introduction-to-the-basic-object-detection-algorithms-part-1/)
* [Реализация Faster R-CNN на Python для обнаружения объектов](https://www.analyticsvidhya.com/blog/2018/11/implementation-faster-r-cnn-python-object-detection/)

## [Задание: Обнаружение объектов](lab/README.md)

**Отказ от ответственности**:  
Этот документ был переведен с использованием сервиса автоматического перевода [Co-op Translator](https://github.com/Azure/co-op-translator). Несмотря на наши усилия обеспечить точность, автоматические переводы могут содержать ошибки или неточности. Оригинальный документ на его родном языке следует считать авторитетным источником. Для получения критически важной информации рекомендуется профессиональный перевод человеком. Мы не несем ответственности за любые недоразумения или неправильные интерпретации, возникшие в результате использования данного перевода.