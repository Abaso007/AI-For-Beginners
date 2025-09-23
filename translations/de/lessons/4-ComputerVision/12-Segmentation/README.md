<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "d7f8a25ff13cfe9f4cd671cc23351fad",
  "translation_date": "2025-08-24T09:34:07+00:00",
  "source_file": "lessons/4-ComputerVision/12-Segmentation/README.md",
  "language_code": "de"
}
-->
# Segmentierung

Wir haben zuvor über Objekterkennung gelernt, die es uns ermöglicht, Objekte in einem Bild durch Vorhersage ihrer *Bounding Boxes* zu lokalisieren. Für einige Aufgaben benötigen wir jedoch nicht nur Bounding Boxes, sondern auch eine präzisere Objektlokalisierung. Diese Aufgabe nennt man **Segmentierung**.

## [Pre-lecture quiz](https://ff-quizzes.netlify.app/en/ai/quiz/23)

Segmentierung kann als **Pixelklassifikation** betrachtet werden, bei der für **jeden** Pixel des Bildes seine Klasse vorhergesagt werden muss (*Hintergrund* ist dabei eine der Klassen). Es gibt zwei Hauptalgorithmen für die Segmentierung:

* **Semantische Segmentierung** gibt nur die Klasse des Pixels an und unterscheidet nicht zwischen verschiedenen Objekten derselben Klasse.
* **Instanzsegmentierung** teilt Klassen in verschiedene Instanzen auf.

Bei der Instanzsegmentierung sind diese Schafe unterschiedliche Objekte, während bei der semantischen Segmentierung alle Schafe durch eine Klasse repräsentiert werden.

<img src="images/instance_vs_semantic.jpeg" width="50%">

> Bild aus [diesem Blogbeitrag](https://nirmalamurali.medium.com/image-classification-vs-semantic-segmentation-vs-instance-segmentation-625c33a08d50)

Es gibt verschiedene neuronale Architekturen für die Segmentierung, aber sie haben alle dieselbe Struktur. In gewisser Weise ähnelt sie dem Autoencoder, den Sie zuvor kennengelernt haben, aber anstatt das ursprüngliche Bild zu rekonstruieren, ist unser Ziel, eine **Maske** zu rekonstruieren. Eine Segmentierungsnetzwerk hat daher folgende Bestandteile:

* **Encoder** extrahiert Merkmale aus dem Eingabebild.
* **Decoder** transformiert diese Merkmale in das **Maskenbild**, mit derselben Größe und einer Anzahl von Kanälen, die der Anzahl der Klassen entspricht.

<img src="images/segm.png" width="80%">

> Bild aus [dieser Publikation](https://arxiv.org/pdf/2001.05566.pdf)

Besonders erwähnenswert ist die Verlustfunktion, die für die Segmentierung verwendet wird. Bei klassischen Autoencodern müssen wir die Ähnlichkeit zwischen zwei Bildern messen, wofür wir den mittleren quadratischen Fehler (MSE) verwenden können. Bei der Segmentierung repräsentiert jeder Pixel im Zielmaskenbild die Klassennummer (one-hot-encoded entlang der dritten Dimension), daher müssen wir Verlustfunktionen verwenden, die speziell für Klassifikationen geeignet sind - Kreuzentropieverlust, gemittelt über alle Pixel. Wenn die Maske binär ist, wird der **binäre Kreuzentropieverlust** (BCE) verwendet.

> ✅ One-Hot-Encoding ist eine Methode, um eine Klassenbezeichnung in einen Vektor mit einer Länge zu kodieren, die der Anzahl der Klassen entspricht. Schauen Sie sich [diesen Artikel](https://datagy.io/sklearn-one-hot-encode/) zu dieser Technik an.

## Segmentierung in der medizinischen Bildgebung

In dieser Lektion werden wir die Segmentierung in Aktion sehen, indem wir ein Netzwerk trainieren, um menschliche Nävi (auch bekannt als Muttermale) auf medizinischen Bildern zu erkennen. Wir verwenden die <a href="https://www.fc.up.pt/addi/ph2%20database.html">PH<sup>2</sup>-Datenbank</a> mit Dermatoskopiebildern als Bildquelle. Dieses Datenset enthält 200 Bilder von drei Klassen: typischer Nävus, atypischer Nävus und Melanom. Alle Bilder enthalten auch eine entsprechende **Maske**, die den Nävus umreißt.

> ✅ Diese Technik ist besonders geeignet für diese Art der medizinischen Bildgebung, aber welche anderen Anwendungen in der realen Welt könnten Sie sich vorstellen?

<img alt="navi" src="images/navi.png"/>

> Bild aus der PH<sup>2</sup>-Datenbank

Wir werden ein Modell trainieren, um jeden Nävus vom Hintergrund zu segmentieren.

## ✍️ Übungen: Semantische Segmentierung

Öffnen Sie die untenstehenden Notebooks, um mehr über verschiedene Architekturen der semantischen Segmentierung zu erfahren, mit ihnen zu arbeiten und sie in Aktion zu sehen.

* [Semantische Segmentierung Pytorch](../../../../../lessons/4-ComputerVision/12-Segmentation/SemanticSegmentationPytorch.ipynb)
* [Semantische Segmentierung TensorFlow](../../../../../lessons/4-ComputerVision/12-Segmentation/SemanticSegmentationTF.ipynb)

## [Post-lecture quiz](https://ff-quizzes.netlify.app/en/ai/quiz/24)

## Fazit

Segmentierung ist eine sehr leistungsstarke Technik für die Bildklassifikation, die über Bounding Boxes hinausgeht und eine Klassifikation auf Pixelebene ermöglicht. Sie wird unter anderem in der medizinischen Bildgebung eingesetzt.

## 🚀 Herausforderung

Die Segmentierung des Körpers ist nur eine der häufigen Aufgaben, die wir mit Bildern von Menschen durchführen können. Andere wichtige Aufgaben umfassen **Skelett-Erkennung** und **Posenerkennung**. Probieren Sie die [OpenPose](https://github.com/CMU-Perceptual-Computing-Lab/openpose)-Bibliothek aus, um zu sehen, wie Posenerkennung verwendet werden kann.

## Rückblick & Selbststudium

Dieser [Wikipedia-Artikel](https://wikipedia.org/wiki/Image_segmentation) bietet einen guten Überblick über die verschiedenen Anwendungen dieser Technik. Informieren Sie sich selbst über die Teilbereiche der Instanzsegmentierung und der Panoptischen Segmentierung in diesem Forschungsfeld.

## [Aufgabe](lab/README.md)

In diesem Labor versuchen Sie die **Segmentierung des menschlichen Körpers** mit dem [Segmentation Full Body MADS Dataset](https://www.kaggle.com/datasets/tapakah68/segmentation-full-body-mads-dataset) von Kaggle.

**Haftungsausschluss**:  
Dieses Dokument wurde mit dem KI-Übersetzungsdienst [Co-op Translator](https://github.com/Azure/co-op-translator) übersetzt. Obwohl wir uns um Genauigkeit bemühen, beachten Sie bitte, dass automatisierte Übersetzungen Fehler oder Ungenauigkeiten enthalten können. Das Originaldokument in seiner ursprünglichen Sprache sollte als maßgebliche Quelle betrachtet werden. Für kritische Informationen wird eine professionelle menschliche Übersetzung empfohlen. Wir übernehmen keine Haftung für Missverständnisse oder Fehlinterpretationen, die sich aus der Nutzung dieser Übersetzung ergeben.