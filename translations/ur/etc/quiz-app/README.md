<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "d699cf8509f74baa5b0b838de5cf0662",
  "translation_date": "2025-08-26T11:24:50+00:00",
  "source_file": "etc/quiz-app/README.md",
  "language_code": "ur"
}
-->
# کوئزز

یہ کوئزز AI نصاب کے لیے لیکچر سے پہلے اور بعد کے کوئزز ہیں، جو یہاں دستیاب ہیں: https://aka.ms/ai-beginners

## ترجمہ شدہ کوئز سیٹ شامل کرنا

کوئز کا ترجمہ شامل کرنے کے لیے، `assets/translations` فولڈرز میں مماثل کوئز اسٹرکچرز بنائیں۔ اصل کوئزز `assets/translations/en` میں موجود ہیں۔ کوئزز کو سبق کے لحاظ سے مختلف گروپوں میں تقسیم کیا گیا ہے۔ یقینی بنائیں کہ نمبرنگ کو صحیح کوئز سیکشن کے ساتھ ہم آہنگ کریں۔ اس نصاب میں کل 40 کوئزز ہیں، اور گنتی 0 سے شروع ہوتی ہے۔

ترجمے میں ترمیم کرنے کے بعد، ترجمہ فولڈر میں `index.js` فائل کو ایڈٹ کریں تاکہ تمام فائلوں کو `en` میں موجود کنونشنز کے مطابق امپورٹ کریں۔

`assets/translations` میں `index.js` فائل کو ایڈٹ کریں تاکہ نئی ترجمہ شدہ فائلوں کو امپورٹ کریں۔

اس کے بعد، اس ایپ میں `App.vue` کی ڈراپ ڈاؤن فہرست کو ایڈٹ کریں تاکہ اپنی زبان شامل کریں۔ لوکلائزڈ مخفف کو اپنی زبان کے فولڈر کے نام سے ہم آہنگ کریں۔

آخر میں، ترجمہ شدہ اسباق میں موجود تمام کوئز لنکس کو ایڈٹ کریں، اگر وہ موجود ہوں، تاکہ اس لوکلائزیشن کو کوئری پیرامیٹر کے طور پر شامل کریں: مثال کے طور پر `?loc=fr`۔

## پروجیکٹ سیٹ اپ

```
npm install
```

### ڈویلپمنٹ کے لیے کمپائل اور ہاٹ ری لوڈز

```
npm run serve
```

### پروڈکشن کے لیے کمپائل اور منیفائی

```
npm run build
```

### فائلز کو لنٹ اور فکس کریں

```
npm run lint
```

### کنفیگریشن کو حسب ضرورت بنائیں

[کنفیگریشن ریفرنس](https://cli.vuejs.org/config/) دیکھیں۔

کریڈٹس: اس کوئز ایپ کے اصل ورژن کا شکریہ: https://github.com/arpan45/simple-quiz-vue

## Azure پر ڈیپلائمنٹ

یہاں ایک مرحلہ وار گائیڈ ہے جو آپ کو شروع کرنے میں مدد دے گی:

1. GitHub ریپوزٹری کو فورک کریں  
یقینی بنائیں کہ آپ کا اسٹیٹک ویب ایپ کوڈ آپ کی GitHub ریپوزٹری میں موجود ہے۔ اس ریپوزٹری کو فورک کریں۔

2. Azure اسٹیٹک ویب ایپ بنائیں  
- ایک [Azure اکاؤنٹ](http://azure.microsoft.com) بنائیں  
- [Azure پورٹل](https://portal.azure.com) پر جائیں  
- "Create a resource" پر کلک کریں اور "Static Web App" تلاش کریں۔  
- "Create" پر کلک کریں۔  

3. اسٹیٹک ویب ایپ کو کنفیگر کریں  
- بنیادی معلومات:  
  - سبسکرپشن: اپنی Azure سبسکرپشن منتخب کریں۔  
  - ریسورس گروپ: نیا ریسورس گروپ بنائیں یا موجودہ استعمال کریں۔  
  - نام: اپنی اسٹیٹک ویب ایپ کے لیے ایک نام فراہم کریں۔  
  - ریجن: اپنے صارفین کے قریب ترین ریجن منتخب کریں۔  

- #### ڈیپلائمنٹ کی تفصیلات:  
  - سورس: "GitHub" منتخب کریں۔  
  - GitHub اکاؤنٹ: Azure کو اپنے GitHub اکاؤنٹ تک رسائی کی اجازت دیں۔  
  - آرگنائزیشن: اپنی GitHub آرگنائزیشن منتخب کریں۔  
  - ریپوزٹری: وہ ریپوزٹری منتخب کریں جس میں آپ کی اسٹیٹک ویب ایپ موجود ہے۔  
  - برانچ: وہ برانچ منتخب کریں جس سے آپ ڈیپلائے کرنا چاہتے ہیں۔  

- #### بلڈ کی تفصیلات:  
  - بلڈ پری سیٹس: وہ فریم ورک منتخب کریں جس پر آپ کی ایپ بنی ہے (مثلاً React، Angular، Vue وغیرہ)۔  
  - ایپ لوکیشن: وہ فولڈر بتائیں جہاں آپ کا ایپ کوڈ موجود ہے (مثلاً / اگر یہ روٹ میں ہے)۔  
  - API لوکیشن: اگر آپ کے پاس API ہے تو اس کا مقام بتائیں (اختیاری)۔  
  - آؤٹ پٹ لوکیشن: وہ فولڈر بتائیں جہاں بلڈ آؤٹ پٹ جنریٹ ہوتا ہے (مثلاً build یا dist)۔  

4. جائزہ لیں اور بنائیں  
اپنی سیٹنگز کا جائزہ لیں اور "Create" پر کلک کریں۔ Azure ضروری وسائل کو سیٹ اپ کرے گا اور آپ کی ریپوزٹری میں ایک GitHub Actions ورک فلو بنائے گا۔

5. GitHub Actions ورک فلو  
Azure خودکار طور پر آپ کی ریپوزٹری میں ایک GitHub Actions ورک فلو فائل بنائے گا (.github/workflows/azure-static-web-apps-<name>.yml)۔ یہ ورک فلو بلڈ اور ڈیپلائمنٹ کے عمل کو ہینڈل کرے گا۔

6. ڈیپلائمنٹ کی نگرانی کریں  
اپنی GitHub ریپوزٹری میں "Actions" ٹیب پر جائیں۔  
آپ کو ایک ورک فلو چلتا ہوا نظر آئے گا۔ یہ ورک فلو آپ کی اسٹیٹک ویب ایپ کو Azure پر بلڈ اور ڈیپلائے کرے گا۔  
جب ورک فلو مکمل ہو جائے، تو آپ کی ایپ فراہم کردہ Azure URL پر لائیو ہو جائے گی۔

### ورک فلو فائل کی مثال

یہاں GitHub Actions ورک فلو فائل کی ایک مثال دی گئی ہے:  
name: Azure Static Web Apps CI/CD  
```
on:
  push:
    branches:
      - main
  pull_request:
    types: [opened, synchronize, reopened, closed]
    branches:
      - main

jobs:
  build_and_deploy_job:
    runs-on: ubuntu-latest
    name: Build and Deploy Job
    steps:
      - uses: actions/checkout@v2
      - name: Build And Deploy
        id: builddeploy
        uses: Azure/static-web-apps-deploy@v1
        with:
          azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN }}
          repo_token: ${{ secrets.GITHUB_TOKEN }}
          action: "upload"
          app_location: "etc/quiz-app # App source code path"
          api_location: ""API source code path optional
          output_location: "dist" #Built app content directory - optional
```

### اضافی وسائل  
- [Azure Static Web Apps دستاویزات](https://learn.microsoft.com/azure/static-web-apps/getting-started)  
- [GitHub Actions دستاویزات](https://docs.github.com/actions/use-cases-and-examples/deploying/deploying-to-azure-static-web-app)  

**ڈسکلیمر**:  
یہ دستاویز AI ترجمہ سروس [Co-op Translator](https://github.com/Azure/co-op-translator) کا استعمال کرتے ہوئے ترجمہ کی گئی ہے۔ ہم درستگی کے لیے کوشش کرتے ہیں، لیکن براہ کرم آگاہ رہیں کہ خودکار ترجمے میں غلطیاں یا غیر درستیاں ہو سکتی ہیں۔ اصل دستاویز کو اس کی اصل زبان میں مستند ذریعہ سمجھا جانا چاہیے۔ اہم معلومات کے لیے، پیشہ ور انسانی ترجمہ کی سفارش کی جاتی ہے۔ ہم اس ترجمے کے استعمال سے پیدا ہونے والی کسی بھی غلط فہمی یا غلط تشریح کے ذمہ دار نہیں ہیں۔