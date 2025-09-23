<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "4bedc8e702db17260cfe824d58b6cfd4",
  "translation_date": "2025-08-25T23:04:21+00:00",
  "source_file": "lessons/4-ComputerVision/06-IntroCV/README.md",
  "language_code": "my"
}
-->
# ကွန်ပျူတာဗီရှင်းအကြောင်းမိတ်ဆက်

[ကွန်ပျူတာဗီရှင်း](https://wikipedia.org/wiki/Computer_vision) ဆိုတာက ကွန်ပျူတာတွေကို ဒစ်ဂျစ်တယ်ပုံရိပ်တွေကို အဆင့်မြင့်နားလည်မှုရရှိစေဖို့ ရည်ရွယ်တဲ့ အပိုင်းတစ်ခုဖြစ်ပါတယ်။ ဒီအဓိပ္ပါယ်က အတော်လေးကျယ်ပြန့်ပြီး *နားလည်မှု* ဆိုတာ အမျိုးမျိုးသောအရာတွေကို ဆိုလိုနိုင်ပါတယ်။ ဥပမာအားဖြင့် ပုံထဲမှာ အရာဝတ္ထုတစ်ခုကို ရှာဖွေခြင်း (**object detection**), ဖြစ်ပျက်နေတဲ့အရာကို နားလည်ခြင်း (**event detection**), ပုံကို စာသားနဲ့ ဖော်ပြခြင်း, ဒါမှမဟုတ် 3D အနေအထားမှာ ရှုခင်းကို ပြန်လည်တည်ဆောက်ခြင်းစသည်ဖြင့်။ လူပုံရိပ်တွေနဲ့ဆိုင်တဲ့ အထူးလုပ်ငန်းတွေပါရှိပါတယ် - အသက်အရွယ်နဲ့ခံစားချက်ခန့်မှန်းခြင်း, မျက်နှာရှာဖွေခြင်းနဲ့ မှတ်မိခြင်း, 3D အနေအထားခန့်မှန်းခြင်းစသည်ဖြင့်။

## [မိန့်ခွန်းမတိုင်မီမေးခွန်း](https://ff-quizzes.netlify.app/en/ai/quiz/11)

ကွန်ပျူတာဗီရှင်းရဲ့ အလွယ်ဆုံးလုပ်ငန်းတစ်ခုက **ပုံရိပ်အမျိုးအစားခွဲခြင်း** ဖြစ်ပါတယ်။

ကွန်ပျူတာဗီရှင်းကို AI ရဲ့ အပိုင်းတစ်ခုအဖြစ် အများအားဖြင့် သတ်မှတ်ကြပါတယ်။ ယနေ့ခေတ်မှာ ကွန်ပျူတာဗီရှင်းလုပ်ငန်းအများစုကို နယူးရယ်နက်ဝက်များကို အသုံးပြုပြီး ဖြေရှင်းကြပါတယ်။ ကွန်ပျူတာဗီရှင်းအတွက် အသုံးပြုတဲ့ နယူးရယ်နက်ဝက်အမျိုးအစား [convolutional neural networks](../07-ConvNets/README.md) အကြောင်းကို ဒီအပိုင်းမှာ သင်ယူသွားပါမယ်။

သို့သော် ပုံရိပ်ကို နယူးရယ်နက်ဝက်ဆီ ပေးပို့မီမှာ အခါအားလျော်စွာ ပုံရိပ်ကို တိုးတက်စေဖို့ algorithmic နည်းလမ်းတွေကို အသုံးပြုဖို့ make sense ဖြစ်ပါတယ်။

Python မှာ ပုံရိပ်ကို ကိုင်တွယ်ဖို့ library အများအပြားရှိပါတယ် -

* **[imageio](https://imageio.readthedocs.io/en/stable/)** ကို ပုံရိပ် format အမျိုးမျိုးကို ဖတ်/ရေးဖို့ အသုံးပြုနိုင်ပါတယ်။ ဒါ့အပြင် ffmpeg ကိုလည်း ပံ့ပိုးပေးပြီး ဗီဒီယို frame တွေကို ပုံရိပ်အဖြစ် ပြောင်းဖို့ အသုံးပြုနိုင်ပါတယ်။
* **[Pillow](https://pillow.readthedocs.io/en/stable/index.html)** (PIL အဖြစ်လည်း သိထားကြပါတယ်) က ပိုမိုအစွမ်းထက်ပြီး ပုံရိပ်ကို ပြောင်းလဲခြင်း၊ palette ကို ချိန်ညှိခြင်းစသည်ဖြင့် လုပ်ဆောင်နိုင်ပါတယ်။
* **[OpenCV](https://opencv.org/)** က C++ နဲ့ရေးသားထားတဲ့ အစွမ်းထက်တဲ့ ပုံရိပ်ကိုင်တွယ်မှု library ဖြစ်ပြီး image processing အတွက် *de facto* standard ဖြစ်လာပါတယ်။ Python interface လည်း ရှိပါတယ်။
* **[dlib](http://dlib.net/)** က machine learning algorithm အများအပြားကို အကောင်အထည်ဖော်ထားတဲ့ C++ library ဖြစ်ပြီး Computer Vision algorithm အချို့ကိုလည်း ပါဝင်ပါတယ်။ Python interface ရှိပြီး မျက်နှာနဲ့ မျက်နှာ landmark detection စသည်ဖြင့် အခက်အခဲရှိတဲ့လုပ်ငန်းတွေကို လုပ်ဆောင်နိုင်ပါတယ်။

## OpenCV

[OpenCV](https://opencv.org/) ကို ပုံရိပ်ကိုင်တွယ်မှုအတွက် *de facto* standard အဖြစ် သတ်မှတ်ကြပါတယ်။ C++ နဲ့ရေးသားထားတဲ့ အသုံးဝင်တဲ့ algorithm အများအပြား ပါဝင်ပါတယ်။ Python ကနေ OpenCV ကို ခေါ်သုံးနိုင်ပါတယ်။

OpenCV ကို သင်ယူဖို့ အကောင်းဆုံးနေရာက [ဒီ Learn OpenCV course](https://learnopencv.com/getting-started-with-opencv/) ဖြစ်ပါတယ်။ ကျွန်တော်တို့ရဲ့ သင်ခန်းစာမှာ OpenCV ကို သင်ယူဖို့မဟုတ်ဘဲ OpenCV ကို ဘယ်အချိန်မှာ အသုံးပြုနိုင်မလဲ၊ ဘယ်လိုအသုံးပြုမလဲဆိုတာကို ဥပမာအချို့နဲ့ ပြသဖို့ ရည်ရွယ်ပါတယ်။

### ပုံရိပ်များကို Load လုပ်ခြင်း

Python မှာ ပုံရိပ်တွေကို NumPy array အဖြစ် အဆင်ပြေစွာ ကိုယ်စားပြုနိုင်ပါတယ်။ ဥပမာအားဖြင့် 320x200 pixel အရွယ်ရှိ grayscale ပုံရိပ်တွေကို 200x320 array အဖြစ် သိမ်းဆည်းနိုင်ပြီး အရောင်ပုံရိပ်တွေကတော့ 200x320x3 (အရောင် channel 3 ခုအတွက်) shape ရှိပါတယ်။ ပုံရိပ်ကို load လုပ်ဖို့ အောက်ပါ code ကို အသုံးပြုနိုင်ပါတယ် -

```python
import cv2
import matplotlib.pyplot as plt

im = cv2.imread('image.jpeg')
plt.imshow(im)
```

ရိုးရာအားဖြင့် OpenCV က အရောင်ပုံရိပ်တွေကို BGR (Blue-Green-Red) encoding ကို အသုံးပြုပြီး Python tools အများစုက RGB (Red-Green-Blue) encoding ကို အသုံးပြုပါတယ်။ ပုံရိပ်ကို မှန်ကန်စွာ ပြသဖို့ RGB color space ကို ပြောင်းဖို့လိုပါတယ်။ NumPy array မှာ dimension တွေကို ပြောင်းခြင်း၊ ဒါမှမဟုတ် OpenCV function ကို ခေါ်သုံးခြင်းဖြင့် ပြောင်းနိုင်ပါတယ် -

```python
im = cv2.cvtColor(im,cv2.COLOR_BGR2RGB)
```

တူညီတဲ့ `cvtColor` function ကို အခြား color space transformation တွေကို လုပ်ဆောင်ဖို့လည်း အသုံးပြုနိုင်ပါတယ်။ ဥပမာအားဖြင့် ပုံရိပ်ကို grayscale သို့မဟုတ် HSV (Hue-Saturation-Value) color space ကို ပြောင်းခြင်း။

OpenCV ကို အသုံးပြုပြီး ဗီဒီယို frame-by-frame ကို load လုပ်နိုင်ပါတယ် - ဥပမာကို [OpenCV Notebook](../../../../../lessons/4-ComputerVision/06-IntroCV/OpenCV.ipynb) မှာ ပေးထားပါတယ်။

### ပုံရိပ်ကို ကိုင်တွယ်ခြင်း

ပုံရိပ်ကို နယူးရယ်နက်ဝက်ဆီ ပေးပို့မီမှာ pre-processing လုပ်ငန်းအချို့ကို လုပ်ဆောင်ချင်နိုင်ပါတယ်။ OpenCV က အများကြီးလုပ်နိုင်ပါတယ်၊ အထူးသဖြင့် -

* **ပုံရိပ်ကို Resizing** `im = cv2.resize(im, (320,200),interpolation=cv2.INTER_LANCZOS)` ကို အသုံးပြုခြင်း
* **ပုံရိပ်ကို Blurring** `im = cv2.medianBlur(im,3)` သို့မဟုတ် `im = cv2.GaussianBlur(im, (3,3), 0)` ကို အသုံးပြုခြင်း
* **အလင်းနဲ့ contrast** ကို NumPy array ကို manipulate လုပ်ခြင်းဖြင့် ပြောင်းလဲနိုင်ပါတယ်၊ [ဒီ Stackoverflow note](https://stackoverflow.com/questions/39308030/how-do-i-increase-the-contrast-of-an-image-in-python-opencv) မှာ ဖော်ပြထားပါတယ်။
* [thresholding](https://docs.opencv.org/4.x/d7/d4d/tutorial_py_thresholding.html) ကို `cv2.threshold`/`cv2.adaptiveThreshold` function တွေကို ခေါ်သုံးခြင်းဖြင့် ပြုလုပ်နိုင်ပါတယ်၊ brightness သို့မဟုတ် contrast ကို ချိန်ညှိခြင်းထက် ပိုမိုကောင်းမွန်ပါတယ်။
* ပုံရိပ်ကို [transformations](https://docs.opencv.org/4.5.5/da/d6e/tutorial_py_geometric_transformations.html) အမျိုးမျိုးကို အသုံးပြုခြင်း:
    - **[Affine transformations](https://docs.opencv.org/4.5.5/d4/d61/tutorial_warp_affine.html)** က ပုံရိပ်ထဲမှာ rotation, resizing နဲ့ skewing ကို ပေါင်းစပ်ဖို့ အသုံးဝင်ပြီး ပုံရိပ်ထဲမှာ point 3 ခုရဲ့ source နဲ့ destination location ကို သိထားရပါမယ်။ Affine transformations က parallel line တွေကို parallel အတိုင်း ထားရှိပါတယ်။
    - **[Perspective transformations](https://medium.com/analytics-vidhya/opencv-perspective-transformation-9edffefb2143)** က ပုံရိပ်ထဲမှာ point 4 ခုရဲ့ source နဲ့ destination position ကို သိထားရပါမယ်။ ဥပမာအားဖြင့် smartphone ကင်မရာနဲ့ angle တစ်ခုကနေ rectangular document ကို ရိုက်ပြီး document ကို rectangular ပုံရိပ်အဖြစ် ပြောင်းလဲချင်တဲ့အခါ။
* **[optical flow](https://docs.opencv.org/4.5.5/d4/dee/tutorial_optical_flow.html)** ကို အသုံးပြုပြီး ပုံရိပ်ထဲမှာ လှုပ်ရှားမှုကို နားလည်ခြင်း။

## ကွန်ပျူတာဗီရှင်းကို အသုံးပြုတဲ့ ဥပမာများ

ကျွန်တော်တို့ရဲ့ [OpenCV Notebook](../../../../../lessons/4-ComputerVision/06-IntroCV/OpenCV.ipynb) မှာ ကွန်ပျူတာဗီရှင်းကို အသုံးပြုပြီး အထူးလုပ်ငန်းတွေကို လုပ်ဆောင်တဲ့ ဥပမာအချို့ကို ပေးထားပါတယ် -

* **Braille စာအုပ်ရဲ့ ဓာတ်ပုံကို Pre-processing လုပ်ခြင်း**။ thresholding, feature detection, perspective transformation နဲ့ NumPy manipulations ကို အသုံးပြုပြီး Braille symbol တစ်ခုချင်းစီကို neural network နဲ့ classification လုပ်ဖို့ ခွဲထုတ်ပေးနိုင်ပါတယ်။

![Braille Image](../../../../../translated_images/braille.341962ff76b1bd7044409371d3de09ced5028132aef97344ea4b7468c1208126.my.jpeg) | ![Braille Image Pre-processed](../../../../../translated_images/braille-result.46530fea020b03c76aac532d7d6eeef7f6fb35b55b1001cd21627907dabef3ed.my.png) | ![Braille Symbols](../../../../../translated_images/braille-symbols.0159185ab69d533909dc4d7d26a1971b51401c6a80eb3a5584f250ea880af88b.my.png)
----|-----|-----

> [OpenCV.ipynb](../../../../../lessons/4-ComputerVision/06-IntroCV/OpenCV.ipynb) မှ ပုံရိပ်

* **Frame difference ကို အသုံးပြုပြီး ဗီဒီယိုထဲမှာ motion ကို ရှာဖွေခြင်း**။ ကင်မရာက fix ဖြစ်နေတဲ့အခါမှာ frame တွေဟာ တစ်ခုနဲ့တစ်ခု အတော်လေးတူညီပါတယ်။ frame တွေကို array အဖြစ် ကိုယ်စားပြုထားတဲ့အတွက် frame 2 ခုကို subtract လုပ်ခြင်းဖြင့် pixel difference ကို ရရှိနိုင်ပြီး static frame တွေမှာ pixel difference ဟာ နည်းပါးပြီး motion ရှိတဲ့အခါမှာ pixel difference ဟာ မြင့်မားလာပါတယ်။

![Image of video frames and frame differences](../../../../../translated_images/frame-difference.706f805491a0883c938e16447bf5eb2f7d69e812c7f743cbe7d7c7645168f81f.my.png)

> [OpenCV.ipynb](../../../../../lessons/4-ComputerVision/06-IntroCV/OpenCV.ipynb) မှ ပုံရိပ်

* **Optical Flow ကို အသုံးပြုပြီး motion ရှာဖွေခြင်း**။ [Optical flow](https://docs.opencv.org/3.4/d4/dee/tutorial_optical_flow.html) က ဗီဒီယို frame တွေထဲမှာ pixel တစ်ခုချင်းစီ ဘယ်လိုရွေ့လျားနေတယ်ဆိုတာကို နားလည်စေပါတယ်။ Optical flow 2 မျိုးရှိပါတယ် -

   - **Dense Optical Flow** က pixel တစ်ခုချင်းစီ ဘယ်နေရာကိုရွေ့လျားနေတယ်ဆိုတာကို ပြသတဲ့ vector field ကို တွက်ချက်ပေးပါတယ်။
   - **Sparse Optical Flow** က ပုံရိပ်ထဲမှာ အထူးသတ်မှတ်ချက်ရှိတဲ့ feature (ဥပမာ edge) တွေကို ရွေးပြီး frame တစ်ခုနဲ့တစ်ခုကြားမှာ trajectory ကို တည်ဆောက်ပေးပါတယ်။

![Image of Optical Flow](../../../../../translated_images/optical.1f4a94464579a83a10784f3c07fe7228514714b96782edf50e70ccd59d2d8c4f.my.png)

> [OpenCV.ipynb](../../../../../lessons/4-ComputerVision/06-IntroCV/OpenCV.ipynb) မှ ပုံရိပ်

## ✍️ ဥပမာ Notebook: OpenCV [OpenCV in Action ကို စမ်းကြည့်ပါ](../../../../../lessons/4-ComputerVision/06-IntroCV/OpenCV.ipynb)

[OpenCV Notebook](../../../../../lessons/4-ComputerVision/06-IntroCV/OpenCV.ipynb) ကို စူးစမ်းပြီး OpenCV နဲ့ စမ်းသပ်မှုတွေ လုပ်ကြည့်ပါ။

## နိဂုံး

တစ်ခါတစ်ရံ motion detection သို့မဟုတ် fingertip detection ကဲ့သို့ အတော်လေးရှုပ်ထွေးတဲ့လုပ်ငန်းတွေကို pure computer vision နဲ့ ဖြေရှင်းနိုင်ပါတယ်။ ဒါကြောင့် ကွန်ပျူတာဗီရှင်းရဲ့ အခြေခံနည်းလမ်းတွေကို သိထားဖို့၊ OpenCV က ဘာတွေ လုပ်နိုင်တယ်ဆိုတာကို သိထားဖို့ အရေးကြီးပါတယ်။

## 🚀 စိန်ခေါ်မှု

AI show မှာ [ဒီဗီဒီယို](https://docs.microsoft.com/shows/ai-show/ai-show--2021-opencv-ai-competition--grand-prize-winners--cortic-tigers--episode-32?WT.mc_id=academic-77998-cacaste) ကို ကြည့်ပြီး Cortic Tigers project အကြောင်းနဲ့ သူတို့ဘယ်လို robot ကို အသုံးပြုပြီး computer vision လုပ်ငန်းတွေကို democratize လုပ်ဖို့ block-based solution တည်ဆောက်ခဲ့တယ်ဆိုတာကို သင်ယူပါ။ ဒီလို project အခြားတွေကို ရှာဖွေပြီး ကွန်ပျူတာဗီရှင်းနယ်ပယ်ကို သင်ယူသူအသစ်တွေ onboard လုပ်ဖို့ ဘယ်လိုကူညီနိုင်တယ်ဆိုတာကို သုတေသနလုပ်ပါ။

## [မိန့်ခွန်းပြီးနောက်မေးခွန်း](https://ff-quizzes.netlify.app/en/ai/quiz/12)

## ပြန်လည်သုံးသပ်ခြင်းနှင့် ကိုယ်တိုင်လေ့လာခြင်း

Optical flow အကြောင်းကို [ဒီအလွန်ကောင်းမွန်တဲ့ tutorial](https://learnopencv.com/optical-flow-in-opencv/) မှာ ဖတ်ရှုပါ။

## [Assignment](lab/README.md)

ဒီ lab မှာ သင် gesture ရိုးရှင်းတဲ့ ဗီဒီယိုတစ်ခုကို ရိုက်ကူးပြီး optical flow ကို အသုံးပြုပြီး up/down/left/right motion တွေကို ရှာဖွေဖို့ ရည်ရွယ်ပါတယ်။

<img src="images/palm-movement.png" width="30%" alt="Palm Movement Frame"/>

**အကြောင်းကြားချက်**:  
ဤစာရွက်စာတမ်းကို AI ဘာသာပြန်ဝန်ဆောင်မှု [Co-op Translator](https://github.com/Azure/co-op-translator) ကို အသုံးပြု၍ ဘာသာပြန်ထားပါသည်။ ကျွန်ုပ်တို့သည် တိကျမှုအတွက် ကြိုးစားနေသော်လည်း၊ အလိုအလျောက် ဘာသာပြန်မှုများတွင် အမှားများ သို့မဟုတ် မတိကျမှုများ ပါဝင်နိုင်သည်ကို သတိပြုပါ။ မူရင်းစာရွက်စာတမ်းကို ၎င်း၏ မူရင်းဘာသာစကားဖြင့် အာဏာတရားရှိသော အရင်းအမြစ်အဖြစ် သတ်မှတ်သင့်ပါသည်။ အရေးကြီးသော အချက်အလက်များအတွက် လူ့ဘာသာပြန်ပညာရှင်များမှ ပရော်ဖက်ရှင်နယ် ဘာသာပြန်မှုကို အကြံပြုပါသည်။ ဤဘာသာပြန်မှုကို အသုံးပြုခြင်းမှ ဖြစ်ပေါ်လာသော အလွဲအလွတ်များ သို့မဟုတ် အနားလွဲမှုများအတွက် ကျွန်ုပ်တို့သည် တာဝန်မယူပါ။