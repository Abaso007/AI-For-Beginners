<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "62b3e3ad5182edb905eec649a87eeeb4",
  "translation_date": "2025-08-26T11:17:47+00:00",
  "source_file": "etc/TRANSLATIONS.md",
  "language_code": "ar"
}
-->
# ساهم بترجمة الدروس

نرحب بترجمات الدروس في هذا المنهج!

## الإرشادات

هناك مجلدات داخل كل مجلد درس ومجلد مقدمة الدرس تحتوي على ملفات Markdown المترجمة.

> ملاحظة، يرجى عدم ترجمة أي كود في ملفات عينات الكود؛ الأشياء الوحيدة التي يجب ترجمتها هي README، المهام، والاختبارات. شكرًا!

يجب أن تتبع الملفات المترجمة هذا التنسيق في التسمية:

**README._[language]_.md**

حيث _[language]_ هو اختصار مكون من حرفين للغة وفقًا لمعيار ISO 639-1 (مثل `README.es.md` للإسبانية و`README.nl.md` للهولندية).

**assignment._[language]_.md**

على غرار ملفات README، يرجى ترجمة المهام أيضًا.

**الاختبارات**

1. أضف ترجمتك إلى تطبيق الاختبار عن طريق إضافة ملف هنا: https://github.com/microsoft/AI-For-Beginners/tree/main/etc/quiz-app/src/assets/translations، مع الالتزام بتنسيق التسمية الصحيح (en.json، fr.json). **يرجى عدم ترجمة الكلمات 'true' أو 'false'. شكرًا!**

2. أضف رمز لغتك إلى القائمة المنسدلة في ملف App.vue الخاص بتطبيق الاختبار.

3. قم بتحرير [ملف index.js الخاص بالترجمات](https://github.com/microsoft/AI-For-Beginners/blob/main/etc/quiz-app/src/assets/translations/index.js) لتضمين لغتك.

4. وأخيرًا، قم بتحرير جميع روابط الاختبارات في ملفات README.md المترجمة لتشير مباشرة إلى اختبارك المترجم: https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/1 يصبح https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/1?loc=id

**شكرًا لكم**

نقدر جهودكم حقًا!

**إخلاء المسؤولية**:  
تم ترجمة هذا المستند باستخدام خدمة الترجمة بالذكاء الاصطناعي [Co-op Translator](https://github.com/Azure/co-op-translator). بينما نسعى لتحقيق الدقة، يرجى العلم أن الترجمات الآلية قد تحتوي على أخطاء أو معلومات غير دقيقة. يجب اعتبار المستند الأصلي بلغته الأصلية هو المصدر الموثوق. للحصول على معلومات حاسمة، يُوصى بالاستعانة بترجمة بشرية احترافية. نحن غير مسؤولين عن أي سوء فهم أو تفسيرات خاطئة ناتجة عن استخدام هذه الترجمة.