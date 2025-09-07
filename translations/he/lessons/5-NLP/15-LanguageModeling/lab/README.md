<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "5130f01fdc5ebb83032b23d489027aac",
  "translation_date": "2025-08-28T20:00:49+00:00",
  "source_file": "lessons/5-NLP/15-LanguageModeling/lab/README.md",
  "language_code": "he"
}
-->
# אימון מודל Skip-Gram

משימת מעבדה מתוך [AI for Beginners Curriculum](https://github.com/microsoft/ai-for-beginners).

## משימה

במעבדה זו, אנו מאתגרים אותך לאמן מודל Word2Vec באמצעות טכניקת Skip-Gram. אמן רשת עם הטמעה (embedding) כדי לחזות מילים שכנות בחלון Skip-Gram ברוחב $N$ טוקנים. ניתן להשתמש ב-[קוד מהשיעור הזה](../CBoW-TF.ipynb) ולבצע בו שינויים קלים.

## מאגר הנתונים

אתה מוזמן להשתמש בכל ספר שתרצה. ניתן למצוא הרבה טקסטים חינמיים ב-[Project Gutenberg](https://www.gutenberg.org/), לדוגמה, הנה קישור ישיר ל-[Alice's Adventures in Wonderland](https://www.gutenberg.org/files/11/11-0.txt) מאת לואיס קרול. לחלופין, ניתן להשתמש במחזות של שייקספיר, אותם ניתן להשיג באמצעות הקוד הבא:

```python
path_to_file = tf.keras.utils.get_file(
   'shakespeare.txt', 
   'https://storage.googleapis.com/download.tensorflow.org/data/shakespeare.txt')
text = open(path_to_file, 'rb').read().decode(encoding='utf-8')
```

## חקור!

אם יש לך זמן ואתה רוצה להעמיק בנושא, נסה לחקור כמה דברים:

* כיצד גודל ההטמעה משפיע על התוצאות?
* כיצד סגנונות טקסט שונים משפיעים על התוצאה?
* קח כמה סוגים שונים מאוד של מילים והסינונימים שלהן, השג את הייצוגים הווקטוריים שלהן, יישם PCA כדי לצמצם את הממדים ל-2, ושרטט אותן במרחב דו-ממדי. האם אתה רואה דפוסים כלשהם?

---

**כתב ויתור**:  
מסמך זה תורגם באמצעות שירות תרגום מבוסס AI [Co-op Translator](https://github.com/Azure/co-op-translator). למרות שאנו שואפים לדיוק, יש לקחת בחשבון שתרגומים אוטומטיים עשויים להכיל שגיאות או אי דיוקים. המסמך המקורי בשפתו המקורית צריך להיחשב כמקור סמכותי. עבור מידע קריטי, מומלץ להשתמש בתרגום מקצועי על ידי אדם. איננו נושאים באחריות לאי הבנות או לפרשנויות שגויות הנובעות משימוש בתרגום זה.