<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "365f0decfe0f47b460bbde8227c5009d",
  "translation_date": "2025-08-28T19:36:41+00:00",
  "source_file": "lessons/4-ComputerVision/12-Segmentation/lab/README.md",
  "language_code": "he"
}
-->
# חיתוך גוף האדם

משימת מעבדה מתוך [AI for Beginners Curriculum](https://github.com/microsoft/ai-for-beginners).

## משימה

בהפקת וידאו, לדוגמה בתחזיות מזג אוויר, לעיתים קרובות יש צורך לחתוך תמונה של אדם מהמצלמה ולהניח אותה מעל קטע וידאו אחר. בדרך כלל עושים זאת באמצעות טכניקות **chroma key**, שבהן מצלמים אדם מול רקע בצבע אחיד, שמוסר לאחר מכן. במעבדה זו, נלמד מודל רשת עצבית לחתוך את צללית האדם.

## מערך הנתונים

נשתמש ב-[Segmentation Full Body MADS Dataset](https://www.kaggle.com/datasets/tapakah68/segmentation-full-body-mads-dataset) מ-Kaggle. הורידו את מערך הנתונים באופן ידני מ-Kaggle.

## פתיחת המחברת

התחילו את המעבדה על ידי פתיחת [BodySegmentation.ipynb](BodySegmentation.ipynb)

## תובנות

חיתוך גוף הוא רק אחת מהמשימות הנפוצות שניתן לבצע עם תמונות של אנשים. משימות חשובות נוספות כוללות **זיהוי שלד** ו-**זיהוי תנוחות**. עיינו בספריית [OpenPose](https://github.com/CMU-Perceptual-Computing-Lab/openpose) כדי לראות כיצד ניתן ליישם משימות אלו.

---

**כתב ויתור**:  
מסמך זה תורגם באמצעות שירות תרגום מבוסס בינה מלאכותית [Co-op Translator](https://github.com/Azure/co-op-translator). למרות שאנו שואפים לדיוק, יש להיות מודעים לכך שתרגומים אוטומטיים עשויים להכיל שגיאות או אי-דיוקים. המסמך המקורי בשפתו המקורית צריך להיחשב כמקור הסמכותי. למידע קריטי, מומלץ להשתמש בתרגום מקצועי על ידי מתרגם אנושי. איננו נושאים באחריות לאי-הבנות או לפרשנויות שגויות הנובעות משימוש בתרגום זה.