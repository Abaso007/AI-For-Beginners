<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "365f0decfe0f47b460bbde8227c5009d",
  "translation_date": "2025-08-26T09:12:01+00:00",
  "source_file": "lessons/4-ComputerVision/12-Segmentation/lab/README.md",
  "language_code": "ur"
}
-->
# انسانی جسم کی تقسیم

[AI for Beginners Curriculum](https://github.com/microsoft/ai-for-beginners) سے لیب اسائنمنٹ۔

## کام

ویڈیو پروڈکشن میں، جیسے کہ موسم کی پیش گوئی، ہمیں اکثر کیمرے سے انسانی تصویر کو کاٹ کر کسی اور فوٹیج کے اوپر رکھنا ہوتا ہے۔ یہ عام طور پر **کرومہ کی** تکنیک کے ذریعے کیا جاتا ہے، جہاں انسان کو ایک یکساں رنگ کے پس منظر کے سامنے فلمایا جاتا ہے، جسے بعد میں ہٹا دیا جاتا ہے۔ اس لیب میں، ہم ایک نیورل نیٹ ورک ماڈل کو تربیت دیں گے تاکہ انسانی خاکہ کو کاٹ سکیں۔

## ڈیٹا سیٹ

ہم [Segmentation Full Body MADS Dataset](https://www.kaggle.com/datasets/tapakah68/segmentation-full-body-mads-dataset) کا استعمال کریں گے جو Kaggle سے دستیاب ہے۔ Kaggle سے ڈیٹا سیٹ کو دستی طور پر ڈاؤنلوڈ کریں۔

## ابتدائی نوٹ بک

لیب کو شروع کرنے کے لیے [BodySegmentation.ipynb](../../../../../../lessons/4-ComputerVision/12-Segmentation/lab/BodySegmentation.ipynb) کھولیں۔

## نتیجہ

جسم کی تقسیم تصاویر کے ساتھ کیے جانے والے عام کاموں میں سے ایک ہے۔ دیگر اہم کاموں میں **اسکلیٹن ڈیٹیکشن** اور **پوز ڈیٹیکشن** شامل ہیں۔ [OpenPose](https://github.com/CMU-Perceptual-Computing-Lab/openpose) لائبریری کو دیکھیں تاکہ یہ جان سکیں کہ ان کاموں کو کیسے نافذ کیا جا سکتا ہے۔

**ڈسکلیمر**:  
یہ دستاویز AI ترجمہ سروس [Co-op Translator](https://github.com/Azure/co-op-translator) کا استعمال کرتے ہوئے ترجمہ کی گئی ہے۔ ہم درستگی کے لیے کوشش کرتے ہیں، لیکن براہ کرم آگاہ رہیں کہ خودکار ترجمے میں غلطیاں یا عدم درستگی ہو سکتی ہیں۔ اصل دستاویز، جو اس کی مقامی زبان میں ہے، کو مستند ذریعہ سمجھا جانا چاہیے۔ اہم معلومات کے لیے، پیشہ ور انسانی ترجمہ کی سفارش کی جاتی ہے۔ اس ترجمے کے استعمال سے پیدا ہونے والی کسی بھی غلط فہمی یا غلط تشریح کے لیے ہم ذمہ دار نہیں ہیں۔