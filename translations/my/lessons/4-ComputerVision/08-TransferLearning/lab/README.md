<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "7765935c35fcee69b9fe2d0cfd6963e2",
  "translation_date": "2025-08-25T23:17:32+00:00",
  "source_file": "lessons/4-ComputerVision/08-TransferLearning/lab/README.md",
  "language_code": "my"
}
-->
# Oxford အိမ်မွေးတိရစ္ဆာန်များကို Transfer Learning အသုံးပြု၍ ခွဲခြားခြင်း

[AI for Beginners Curriculum](https://github.com/microsoft/ai-for-beginners) မှ Lab Assignment။

## တာဝန်

သင်သည် အိမ်မွေးတိရစ္ဆာန်များကို စာရင်းသွင်းရန်အတွက် pet nursery အတွက် အက်ပ်တစ်ခု ဖန်တီးရန်လိုအပ်သည်ဟု စိတ်ကူးပါစေ။ ထိုအက်ပ်၏ အလွန်ကောင်းမွန်သော အင်္ဂါရပ်တစ်ခုမှာ ဓာတ်ပုံမှ တိရစ္ဆာန်၏ အမျိုးအစားကို အလိုအလျောက် ရှာဖွေနိုင်ခြင်းဖြစ်မည်။ ဤအလုပ်မှာ [Oxford-IIIT](https://www.robots.ox.ac.uk/~vgg/data/pets/) အိမ်မွေးတိရစ္ဆာန်များ dataset မှ တကယ့်ဘဝ အိမ်မွေးတိရစ္ဆာန်ဓာတ်ပုံများကို Transfer Learning အသုံးပြု၍ ခွဲခြားသတ်မှတ်သွားမည်ဖြစ်သည်။

## Dataset

ကျွန်ုပ်တို့သည် [Oxford-IIIT](https://www.robots.ox.ac.uk/~vgg/data/pets/) အိမ်မွေးတိရစ္ဆာန်များ dataset ကို အသုံးပြုမည်ဖြစ်ပြီး၊ ၎င်းတွင် ခွေးနှင့်ကြောင် ၃၅ မျိုးအထိ ပါဝင်သည်။

Dataset ကို ဒေါင်းလုဒ်လုပ်ရန် အောက်ပါ code snippet ကို အသုံးပြုပါ-

```python
!wget https://www.robots.ox.ac.uk/~vgg/data/pets/data/images.tar.gz
!tar xfz images.tar.gz
!rm images.tar.gz
```

## Notebook စတင်ခြင်း

Lab ကို [OxfordPets.ipynb](../../../../../../lessons/4-ComputerVision/08-TransferLearning/lab/OxfordPets.ipynb) ဖိုင်ကို ဖွင့်၍ စတင်ပါ။

## အဓိကအချက်

Transfer learning နှင့် pre-trained networks များသည် တကယ့်ဘဝ image classification ပြဿနာများကို အလွန်လွယ်ကူစွာ ဖြေရှင်းနိုင်စေသည်။ သို့သော် pre-trained networks များသည် အမျိုးအစားတူသော ဓာတ်ပုံများတွင်သာ ကောင်းစွာအလုပ်လုပ်နိုင်ပြီး၊ အလွန်ကွဲပြားသော ဓာတ်ပုံများ (ဥပမာ- ဆေးဘက်ဆိုင်ရာဓာတ်ပုံများ) ကို ခွဲခြားရန် စတင်လျှင်၊ ရလဒ်များမှာ အလွန်မကောင်းနိုင်ပါ။

**အကြောင်းကြားချက်**:  
ဤစာရွက်စာတမ်းကို AI ဘာသာပြန်ဝန်ဆောင်မှု [Co-op Translator](https://github.com/Azure/co-op-translator) ကို အသုံးပြု၍ ဘာသာပြန်ထားပါသည်။ ကျွန်ုပ်တို့သည် တိကျမှုအတွက် ကြိုးစားနေပါသော်လည်း၊ အလိုအလျောက် ဘာသာပြန်ခြင်းတွင် အမှားများ သို့မဟုတ် မတိကျမှုများ ပါရှိနိုင်သည်ကို သတိပြုပါ။ မူရင်းဘာသာစကားဖြင့် ရေးသားထားသော စာရွက်စာတမ်းကို အာဏာတရားရှိသော ရင်းမြစ်အဖြစ် သတ်မှတ်သင့်ပါသည်။ အရေးကြီးသော အချက်အလက်များအတွက် လူ့ဘာသာပြန်ပညာရှင်များမှ ပရော်ဖက်ရှင်နယ် ဘာသာပြန်ခြင်းကို အကြံပြုပါသည်။ ဤဘာသာပြန်ကို အသုံးပြုခြင်းမှ ဖြစ်ပေါ်လာသော အလွဲအလွတ်များ သို့မဟုတ် အနားယူမှားမှုများအတွက် ကျွန်ုပ်တို့သည် တာဝန်မယူပါ။