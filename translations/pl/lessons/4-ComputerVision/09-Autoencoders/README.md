<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "0b306c04f5337b6e7430e5c0b16bb5c0",
  "translation_date": "2025-08-24T10:25:32+00:00",
  "source_file": "lessons/4-ComputerVision/09-Autoencoders/README.md",
  "language_code": "pl"
}
-->
# Autoenkodery

Podczas trenowania CNN, jednym z problemów jest potrzeba dużej ilości danych oznaczonych. W przypadku klasyfikacji obrazów musimy ręcznie przyporządkować obrazy do różnych klas, co wymaga sporego wysiłku.

## [Pre-lecture quiz](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/109)

Możemy jednak chcieć wykorzystać surowe (nieoznaczone) dane do trenowania ekstraktorów cech CNN, co nazywa się **uczeniem samonadzorowanym**. Zamiast etykiet, użyjemy obrazów treningowych zarówno jako wejścia, jak i wyjścia sieci. Główna idea **autoenkodera** polega na tym, że mamy **sieć enkodera**, która przekształca obraz wejściowy w pewną **przestrzeń latentną** (zwykle jest to wektor o mniejszym rozmiarze), a następnie **sieć dekodera**, której celem jest odtworzenie oryginalnego obrazu.

> ✅ [Autoenkoder](https://wikipedia.org/wiki/Autoencoder) to "rodzaj sztucznej sieci neuronowej używanej do nauki efektywnego kodowania nieoznaczonych danych."

Ponieważ trenujemy autoenkoder, aby uchwycić jak najwięcej informacji z oryginalnego obrazu w celu dokładnej rekonstrukcji, sieć stara się znaleźć najlepsze **osadzenie** obrazów wejściowych, aby uchwycić ich znaczenie.

![Schemat Autoenkodera](../../../../../lessons/4-ComputerVision/09-Autoencoders/images/autoencoder_schema.jpg)

> Obraz z [blogu Keras](https://blog.keras.io/building-autoencoders-in-keras.html)

## Scenariusze użycia Autoenkoderów

Choć samo odtwarzanie oryginalnych obrazów może wydawać się mało użyteczne, istnieje kilka scenariuszy, w których autoenkodery są szczególnie przydatne:

* **Obniżanie wymiaru obrazów w celu wizualizacji** lub **trenowanie osadzeń obrazów**. Zazwyczaj autoenkodery dają lepsze wyniki niż PCA, ponieważ uwzględniają przestrzenną naturę obrazów i hierarchiczne cechy.
* **Usuwanie szumów**, czyli eliminowanie zakłóceń z obrazu. Ponieważ szum zawiera wiele niepotrzebnych informacji, autoenkoder nie jest w stanie zmieścić ich wszystkich w stosunkowo małej przestrzeni latentnej, dzięki czemu uchwyca tylko istotne części obrazu. Podczas trenowania usuwania szumów zaczynamy od oryginalnych obrazów, a jako wejście dla autoenkodera używamy obrazów z dodanym sztucznie szumem.
* **Super-rozdzielczość**, czyli zwiększanie rozdzielczości obrazu. Zaczynamy od obrazów o wysokiej rozdzielczości, a jako wejście dla autoenkodera używamy obrazów o niższej rozdzielczości.
* **Modele generatywne**. Po przeszkoleniu autoenkodera, część dekodera może być używana do tworzenia nowych obiektów, zaczynając od losowych wektorów latentnych.

## Wariacyjne Autoenkodery (VAE)

Tradycyjne autoenkodery w pewien sposób redukują wymiar danych wejściowych, identyfikując istotne cechy obrazów wejściowych. Jednak wektory latentne często nie mają większego sensu. Innymi słowy, biorąc za przykład zbiór danych MNIST, ustalenie, które cyfry odpowiadają różnym wektorom latentnym, nie jest łatwym zadaniem, ponieważ bliskie wektory latentne niekoniecznie odpowiadają tym samym cyfrom.

Z drugiej strony, aby trenować modele *generatywne*, lepiej jest mieć pewne zrozumienie przestrzeni latentnej. Ta idea prowadzi nas do **wariacyjnego autoenkodera** (VAE).

VAE to autoenkoder, który uczy się przewidywać *rozkład statystyczny* parametrów latentnych, tzw. **rozkład latentny**. Na przykład możemy chcieć, aby wektory latentne były rozłożone normalnie z pewną średnią z<sub>mean</sub> i odchyleniem standardowym z<sub>sigma</sub> (zarówno średnia, jak i odchylenie standardowe są wektorami o pewnej wymiarowości d). Enkoder w VAE uczy się przewidywać te parametry, a następnie dekoder bierze losowy wektor z tego rozkładu, aby odtworzyć obiekt.

Podsumowując:

 * Z wektora wejściowego przewidujemy `z_mean` i `z_log_sigma` (zamiast przewidywać samo odchylenie standardowe, przewidujemy jego logarytm)
 * Pobieramy próbkę wektora `sample` z rozkładu N(z<sub>mean</sub>,exp(z<sub>log\_sigma</sub>))
 * Dekoder próbuje odtworzyć oryginalny obraz, używając `sample` jako wektora wejściowego

 <img src="images/vae.png" width="50%">

> Obraz z [tego wpisu na blogu](https://ijdykeman.github.io/ml/2016/12/21/cvae.html) autorstwa Isaaka Dykemana

Wariacyjne autoenkodery używają złożonej funkcji straty, która składa się z dwóch części:

* **Strata rekonstrukcji** to funkcja straty, która pokazuje, jak blisko odtworzony obraz jest do celu (może to być średni błąd kwadratowy, czyli MSE). Jest to ta sama funkcja straty, co w zwykłych autoenkoderach.
* **Strata KL**, która zapewnia, że rozkład zmiennych latentnych pozostaje bliski rozkładowi normalnemu. Opiera się na pojęciu [dywergencji Kullbacka-Leiblera](https://www.countbayesie.com/blog/2017/5/9/kullback-leibler-divergence-explained) - metryki do oszacowania podobieństwa dwóch rozkładów statystycznych.

Jedną z ważnych zalet VAE jest to, że pozwalają na stosunkowo łatwe generowanie nowych obrazów, ponieważ wiemy, z jakiego rozkładu pobierać wektory latentne. Na przykład, jeśli przeszkolimy VAE z 2-wymiarowym wektorem latentnym na MNIST, możemy następnie zmieniać komponenty wektora latentnego, aby uzyskać różne cyfry:

<img alt="vaemnist" src="images/vaemnist.png" width="50%"/>

> Obraz autorstwa [Dmitrija Soshnikova](http://soshnikov.com)

Zauważ, jak obrazy płynnie przechodzą jeden w drugi, gdy zaczynamy pobierać wektory latentne z różnych części przestrzeni parametrów latentnych. Możemy również zwizualizować tę przestrzeń w 2D:

<img alt="vaemnist cluster" src="images/vaemnist-diag.png" width="50%"/> 

> Obraz autorstwa [Dmitrija Soshnikova](http://soshnikov.com)

## ✍️ Ćwiczenia: Autoenkodery

Dowiedz się więcej o autoenkoderach w tych odpowiednich notatnikach:

* [Autoenkodery w TensorFlow](../../../../../lessons/4-ComputerVision/09-Autoencoders/AutoencodersTF.ipynb)
* [Autoenkodery w PyTorch](../../../../../lessons/4-ComputerVision/09-Autoencoders/AutoEncodersPyTorch.ipynb)

## Właściwości Autoenkoderów

* **Specyficzne dla danych** - działają dobrze tylko na typie obrazów, na których zostały przeszkolone. Na przykład, jeśli przeszkolimy sieć super-rozdzielczości na kwiatach, nie będzie dobrze działać na portretach. Dzieje się tak, ponieważ sieć może tworzyć obrazy o wyższej rozdzielczości, wykorzystując szczegóły z cech wyuczonych na zbiorze danych treningowych.
* **Stratne** - odtworzony obraz nie jest identyczny z oryginalnym obrazem. Charakter strat jest definiowany przez *funkcję straty* używaną podczas treningu.
* Działa na **danych nieoznaczonych**

## [Post-lecture quiz](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/209)

## Podsumowanie

W tej lekcji dowiedziałeś się o różnych typach autoenkoderów dostępnych dla naukowca zajmującego się AI. Nauczyłeś się, jak je budować i jak używać ich do odtwarzania obrazów. Dowiedziałeś się również o VAE i jak używać ich do generowania nowych obrazów.

## 🚀 Wyzwanie

W tej lekcji dowiedziałeś się o używaniu autoenkoderów do obrazów. Ale można je również używać do muzyki! Sprawdź projekt Magenta [MusicVAE](https://magenta.tensorflow.org/music-vae), który wykorzystuje autoenkodery do nauki odtwarzania muzyki. Przeprowadź kilka [eksperymentów](https://colab.research.google.com/github/magenta/magenta-demos/blob/master/colab-notebooks/Multitrack_MusicVAE.ipynb) z tą biblioteką, aby zobaczyć, co możesz stworzyć.

## [Post-lecture quiz](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/208)

## Przegląd i Samodzielna Nauka

Dla odniesienia, przeczytaj więcej o autoenkoderach w tych zasobach:

* [Budowanie Autoenkoderów w Keras](https://blog.keras.io/building-autoencoders-in-keras.html)
* [Wpis na blogu NeuroHive](https://neurohive.io/ru/osnovy-data-science/variacionnyj-avtojenkoder-vae/)
* [Wariacyjne Autoenkodery Wyjaśnione](https://kvfrans.com/variational-autoencoders-explained/)
* [Wariacyjne Autoenkodery Warunkowe](https://ijdykeman.github.io/ml/2016/12/21/cvae.html)

## Zadanie

Na końcu [tego notatnika używającego TensorFlow](../../../../../lessons/4-ComputerVision/09-Autoencoders/AutoencodersTF.ipynb) znajdziesz 'zadanie' - użyj tego jako swojego zadania.

**Zastrzeżenie**:  
Ten dokument został przetłumaczony za pomocą usługi tłumaczenia AI [Co-op Translator](https://github.com/Azure/co-op-translator). Chociaż staramy się zapewnić dokładność, prosimy mieć na uwadze, że automatyczne tłumaczenia mogą zawierać błędy lub nieścisłości. Oryginalny dokument w jego rodzimym języku powinien być uznawany za wiarygodne źródło. W przypadku informacji krytycznych zaleca się skorzystanie z profesjonalnego tłumaczenia wykonanego przez człowieka. Nie ponosimy odpowiedzialności za jakiekolwiek nieporozumienia lub błędne interpretacje wynikające z użycia tego tłumaczenia.