<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "4bedc8e702db17260cfe824d58b6cfd4",
  "translation_date": "2025-08-25T23:02:46+00:00",
  "source_file": "lessons/4-ComputerVision/06-IntroCV/README.md",
  "language_code": "hr"
}
-->
# Uvod u računalni vid

[Računalni vid](https://wikipedia.org/wiki/Computer_vision) je disciplina čiji je cilj omogućiti računalima da steknu visok nivo razumijevanja digitalnih slika. Ovo je prilično široka definicija jer *razumijevanje* može značiti mnogo različitih stvari, uključujući pronalaženje objekta na slici (**detekcija objekata**), razumijevanje što se događa (**detekcija događaja**), opisivanje slike tekstom ili rekonstrukciju scene u 3D. Postoje i posebni zadaci vezani za slike ljudi: procjena dobi i emocija, detekcija i identifikacija lica te procjena 3D poze, da spomenemo samo neke.

## [Kviz prije predavanja](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/106)

Jedan od najjednostavnijih zadataka računalnog vida je **klasifikacija slika**.

Računalni vid se često smatra granom umjetne inteligencije (AI). Danas se većina zadataka računalnog vida rješava pomoću neuronskih mreža. U ovom dijelu ćemo naučiti više o posebnoj vrsti neuronskih mreža koje se koriste za računalni vid, [konvolucijskim neuronskim mrežama](../07-ConvNets/README.md).

Međutim, prije nego što sliku proslijedite neuronskoj mreži, u mnogim slučajevima ima smisla koristiti neke algoritamske tehnike za poboljšanje slike.

Postoji nekoliko Python biblioteka dostupnih za obradu slika:

* **[imageio](https://imageio.readthedocs.io/en/stable/)** može se koristiti za čitanje/pisanje različitih formata slika. Također podržava ffmpeg, koristan alat za pretvaranje video okvira u slike.
* **[Pillow](https://pillow.readthedocs.io/en/stable/index.html)** (poznat i kao PIL) je nešto moćniji i podržava manipulaciju slikama poput morfinga, podešavanja paleta i još mnogo toga.
* **[OpenCV](https://opencv.org/)** je moćna biblioteka za obradu slika napisana u C++, koja je postala *de facto* standard za obradu slika. Ima praktično Python sučelje.
* **[dlib](http://dlib.net/)** je C++ biblioteka koja implementira mnoge algoritme strojnog učenja, uključujući neke algoritme računalnog vida. Također ima Python sučelje i može se koristiti za izazovne zadatke poput detekcije lica i obilježja lica.

## OpenCV

[OpenCV](https://opencv.org/) se smatra *de facto* standardom za obradu slika. Sadrži mnogo korisnih algoritama implementiranih u C++. OpenCV možete koristiti i iz Pythona.

Dobar izvor za učenje OpenCV-a je [ovaj Learn OpenCV tečaj](https://learnopencv.com/getting-started-with-opencv/). U našem kurikulumu cilj nije naučiti OpenCV, već vam pokazati neke primjere kada se može koristiti i kako.

### Učitavanje slika

Slike u Pythonu mogu se praktično predstaviti pomoću NumPy nizova. Na primjer, crno-bijele slike veličine 320x200 piksela bile bi pohranjene u nizu dimenzija 200x320, dok bi slike u boji iste dimenzije imale oblik 200x320x3 (za 3 kanala boja). Za učitavanje slike možete koristiti sljedeći kod:

```python
import cv2
import matplotlib.pyplot as plt

im = cv2.imread('image.jpeg')
plt.imshow(im)
```

Tradicionalno, OpenCV koristi BGR (plavo-zelena-crvena) kodiranje za slike u boji, dok ostatak Python alata koristi tradicionalniji RGB (crveno-zelena-plava). Da bi slika izgledala ispravno, trebate je pretvoriti u RGB prostor boja, bilo zamjenom dimenzija u NumPy nizu ili pozivanjem OpenCV funkcije:

```python
im = cv2.cvtColor(im,cv2.COLOR_BGR2RGB)
```

Ista funkcija `cvtColor` može se koristiti za izvođenje drugih transformacija prostora boja, poput pretvaranja slike u crno-bijelu ili u HSV (nijansa-zasićenost-vrijednost) prostor boja.

OpenCV također možete koristiti za učitavanje videozapisa okvir po okvir - primjer je dan u vježbi [OpenCV Notebook](../../../../../lessons/4-ComputerVision/06-IntroCV/OpenCV.ipynb).

### Obrada slika

Prije nego što sliku proslijedite neuronskoj mreži, možda ćete htjeti primijeniti nekoliko koraka predobrade. OpenCV može učiniti mnogo toga, uključujući:

* **Promjenu veličine** slike pomoću `im = cv2.resize(im, (320,200),interpolation=cv2.INTER_LANCZOS)`
* **Zamućivanje** slike pomoću `im = cv2.medianBlur(im,3)` ili `im = cv2.GaussianBlur(im, (3,3), 0)`
* Promjenu **svjetline i kontrasta** slike manipulacijom NumPy nizovima, kako je opisano [u ovoj bilješci na Stackoverflowu](https://stackoverflow.com/questions/39308030/how-do-i-increase-the-contrast-of-an-image-in-python-opencv).
* Korištenje [praga](https://docs.opencv.org/4.x/d7/d4d/tutorial_py_thresholding.html) pozivanjem funkcija `cv2.threshold`/`cv2.adaptiveThreshold`, što je često bolje od podešavanja svjetline ili kontrasta.
* Primjenu različitih [transformacija](https://docs.opencv.org/4.5.5/da/d6e/tutorial_py_geometric_transformations.html) na sliku:
    - **[Afine transformacije](https://docs.opencv.org/4.5.5/d4/d61/tutorial_warp_affine.html)** mogu biti korisne ako trebate kombinirati rotaciju, promjenu veličine i iskrivljenje slike te znate izvorne i odredišne lokacije tri točke na slici. Afine transformacije zadržavaju paralelne linije paralelnima.
    - **[Perspektivne transformacije](https://medium.com/analytics-vidhya/opencv-perspective-transformation-9edffefb2143)** mogu biti korisne kada znate izvorne i odredišne pozicije 4 točke na slici. Na primjer, ako slikate pravokutni dokument pametnim telefonom pod nekim kutom i želite dobiti pravokutnu sliku samog dokumenta.
* Razumijevanje kretanja unutar slike pomoću **[optčkog toka](https://docs.opencv.org/4.5.5/d4/dee/tutorial_optical_flow.html)**.

## Primjeri korištenja računalnog vida

U našem [OpenCV Notebook](../../../../../lessons/4-ComputerVision/06-IntroCV/OpenCV.ipynb) dajemo neke primjere kada se računalni vid može koristiti za obavljanje specifičnih zadataka:

* **Predobrada fotografije Brailleove knjige**. Fokusiramo se na to kako možemo koristiti pragove, detekciju obilježja, perspektivne transformacije i manipulacije NumPy nizovima kako bismo odvojili pojedinačne Brailleove simbole za daljnju klasifikaciju neuronskom mrežom.

![Braille slika](../../../../../translated_images/braille.341962ff76b1bd7044409371d3de09ced5028132aef97344ea4b7468c1208126.hr.jpeg) | ![Predobrađena Braille slika](../../../../../translated_images/braille-result.46530fea020b03c76aac532d7d6eeef7f6fb35b55b1001cd21627907dabef3ed.hr.png) | ![Braille simboli](../../../../../translated_images/braille-symbols.0159185ab69d533909dc4d7d26a1971b51401c6a80eb3a5584f250ea880af88b.hr.png)
----|-----|-----

> Slika iz [OpenCV.ipynb](../../../../../lessons/4-ComputerVision/06-IntroCV/OpenCV.ipynb)

* **Detekcija kretanja u videu pomoću razlike okvira**. Ako je kamera fiksna, tada bi okviri iz videozapisa trebali biti prilično slični. Budući da su okviri predstavljeni kao nizovi, jednostavnim oduzimanjem tih nizova za dva uzastopna okvira dobit ćemo razliku piksela, koja bi trebala biti mala za statične okvire, a postati veća kada postoji značajno kretanje na slici.

![Slika video okvira i razlike okvira](../../../../../translated_images/frame-difference.706f805491a0883c938e16447bf5eb2f7d69e812c7f743cbe7d7c7645168f81f.hr.png)

> Slika iz [OpenCV.ipynb](../../../../../lessons/4-ComputerVision/06-IntroCV/OpenCV.ipynb)

* **Detekcija kretanja pomoću optičkog toka**. [Optički tok](https://docs.opencv.org/3.4/d4/dee/tutorial_optical_flow.html) omogućuje nam razumijevanje kako se pojedini pikseli na video okvirima kreću. Postoje dvije vrste optičkog toka:

   - **Gusti optički tok** računa vektorsko polje koje pokazuje za svaki piksel kamo se kreće
   - **Rijetki optički tok** temelji se na uzimanju nekih karakterističnih obilježja na slici (npr. rubova) i praćenju njihove putanje od okvira do okvira.

![Slika optičkog toka](../../../../../translated_images/optical.1f4a94464579a83a10784f3c07fe7228514714b96782edf50e70ccd59d2d8c4f.hr.png)

> Slika iz [OpenCV.ipynb](../../../../../lessons/4-ComputerVision/06-IntroCV/OpenCV.ipynb)

## ✍️ Primjeri bilježnica: OpenCV [isprobajte OpenCV u praksi](../../../../../lessons/4-ComputerVision/06-IntroCV/OpenCV.ipynb)

Napravimo nekoliko eksperimenata s OpenCV-om istražujući [OpenCV Notebook](../../../../../lessons/4-ComputerVision/06-IntroCV/OpenCV.ipynb)

## Zaključak

Ponekad se relativno složeni zadaci poput detekcije kretanja ili detekcije vrhova prstiju mogu riješiti isključivo računalnim vidom. Stoga je vrlo korisno poznavati osnovne tehnike računalnog vida i što biblioteke poput OpenCV-a mogu učiniti.

## 🚀 Izazov

Pogledajte [ovaj video](https://docs.microsoft.com/shows/ai-show/ai-show--2021-opencv-ai-competition--grand-prize-winners--cortic-tigers--episode-32?WT.mc_id=academic-77998-cacaste) iz AI showa kako biste saznali više o projektu Cortic Tigers i kako su izgradili rješenje temeljeno na blokovima za demokratizaciju zadataka računalnog vida putem robota. Istražite druge slične projekte koji pomažu novim učenicima da se uključe u ovo područje.

## [Kviz nakon predavanja](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/206)

## Pregled i samostalno učenje

Pročitajte više o optičkom toku [u ovom odličnom vodiču](https://learnopencv.com/optical-flow-in-opencv/).

## [Zadatak](lab/README.md)

U ovom laboratoriju snimit ćete video s jednostavnim gestama, a vaš cilj je izdvojiti pokrete gore/dolje/lijevo/desno koristeći optički tok.

<img src="images/palm-movement.png" width="30%" alt="Pokret dlana okvir"/>

**Odricanje od odgovornosti**:  
Ovaj dokument je preveden pomoću AI usluge za prevođenje [Co-op Translator](https://github.com/Azure/co-op-translator). Iako nastojimo osigurati točnost, imajte na umu da automatski prijevodi mogu sadržavati pogreške ili netočnosti. Izvorni dokument na izvornom jeziku treba smatrati autoritativnim izvorom. Za kritične informacije preporučuje se profesionalni prijevod od strane čovjeka. Ne preuzimamo odgovornost za nesporazume ili pogrešna tumačenja koja mogu proizaći iz korištenja ovog prijevoda.