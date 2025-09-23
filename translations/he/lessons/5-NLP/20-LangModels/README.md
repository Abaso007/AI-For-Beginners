<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "97836d30a6bec736f8e3b4411c572bc2",
  "translation_date": "2025-09-23T10:23:55+00:00",
  "source_file": "lessons/5-NLP/20-LangModels/README.md",
  "language_code": "he"
}
-->
# מודלים גדולים של שפה מאומנים מראש

בכל המשימות הקודמות שלנו, אימנו רשת עצבית לבצע משימה מסוימת באמצעות מערך נתונים מתויג. עם מודלים גדולים של טרנספורמרים, כמו BERT, אנו משתמשים במידול שפה בצורה עצמאית כדי לבנות מודל שפה, אשר לאחר מכן מתמחה למשימה ספציפית באמצעות אימון נוסף בתחום מסוים. עם זאת, הוכח כי מודלים גדולים של שפה יכולים גם לפתור משימות רבות ללא כל אימון ספציפי לתחום. משפחת מודלים המסוגלת לעשות זאת נקראת **GPT**: Generative Pre-Trained Transformer.

## [שאלון לפני ההרצאה](https://ff-quizzes.netlify.app/en/ai/quiz/39)

## יצירת טקסט ומדד Perplexity

הרעיון של רשת עצבית המסוגלת לבצע משימות כלליות ללא אימון נוסף מוצג במאמר [Language Models are Unsupervised Multitask Learners](https://cdn.openai.com/better-language-models/language_models_are_unsupervised_multitask_learners.pdf). הרעיון המרכזי הוא שמשימות רבות אחרות יכולות להיות ממודלות באמצעות **יצירת טקסט**, משום שהבנת טקסט למעשה משמעה היכולת לייצר אותו. מכיוון שהמודל מאומן על כמות עצומה של טקסט שמכילה ידע אנושי, הוא גם הופך למיומן במגוון רחב של נושאים.

> הבנה ויכולת לייצר טקסט כוללת גם ידע על העולם סביבנו. אנשים לומדים במידה רבה על ידי קריאה, ורשת GPT דומה בהיבט הזה.

רשתות ליצירת טקסט פועלות על ידי חיזוי ההסתברות של המילה הבאה $$P(w_N)$$. עם זאת, ההסתברות הבלתי מותנית של המילה הבאה שווה לתדירות שלה במאגר הטקסט. GPT מסוגל לספק לנו **הסתברות מותנית** של המילה הבאה, בהתחשב במילים הקודמות: $$P(w_N | w_{n-1}, ..., w_0)$$.

> ניתן לקרוא עוד על הסתברויות בתוכנית הלימודים שלנו [Data Science for Beginners](https://github.com/microsoft/Data-Science-For-Beginners/tree/main/1-Introduction/04-stats-and-probability).

איכות מודל ליצירת שפה יכולה להיות מוגדרת באמצעות **מדד Perplexity**. זהו מדד פנימי שמאפשר לנו למדוד את איכות המודל ללא מערך נתונים ספציפי למשימה. המדד מבוסס על הרעיון של *הסתברות של משפט* - המודל מקצה הסתברות גבוהה למשפט שסביר שיהיה אמיתי (כלומר, המודל אינו **מבולבל** ממנו), והסתברות נמוכה למשפטים שפחות הגיוניים (לדוגמה: *Can it does what?*). כאשר אנו מספקים למודל משפטים ממאגר טקסט אמיתי, אנו מצפים שהם יקבלו הסתברות גבוהה ו**מדד Perplexity** נמוך. מתמטית, הוא מוגדר כהסתברות הפוכה מנורמלת של מערך הבדיקה:
$$
\mathrm{Perplexity}(W) = \sqrt[N]{1\over P(W_1,...,W_N)}
$$ 

**ניתן להתנסות ביצירת טקסט באמצעות [עורך טקסט מבוסס GPT של Hugging Face](https://transformer.huggingface.co/doc/gpt2-large)**. בעורך זה, מתחילים לכתוב טקסט ולחיצה על **[TAB]** תציע מספר אפשרויות להשלמה. אם הן קצרות מדי או לא מספקות, ניתן ללחוץ שוב על [TAB] ולקבל אפשרויות נוספות, כולל קטעי טקסט ארוכים יותר.

## GPT היא משפחה

GPT אינו מודל יחיד, אלא אוסף של מודלים שפותחו ואומנו על ידי [OpenAI](https://openai.com).

במשפחת מודלי GPT, יש לנו:

| [GPT-2](https://huggingface.co/docs/transformers/model_doc/gpt2#openai-gpt2) | [GPT 3](https://openai.com/research/language-models-are-few-shot-learners) | [GPT-4](https://openai.com/gpt-4) |
| -- | -- | -- |
|מודל שפה עם עד 1.5 מיליארד פרמטרים. | מודל שפה עם עד 175 מיליארד פרמטרים | 100 טריליון פרמטרים ומקבל גם קלטי תמונה וגם טקסט ומפיק טקסט. |

המודלים GPT-3 ו-GPT-4 זמינים [כשירות קוגניטיבי מ-Microsoft Azure](https://azure.microsoft.com/en-us/services/cognitive-services/openai-service/#overview?WT.mc_id=academic-77998-cacaste), וגם כ-[API של OpenAI](https://openai.com/api/).

## הנדסת הנחיות (Prompt Engineering)

מכיוון ש-GPT אומן על כמויות עצומות של נתונים כדי להבין שפה וקוד, הוא מספק פלטים בתגובה לקלטים (הנחיות). הנחיות הן קלטים או שאילתות ל-GPT שבהם מספקים למודלים הוראות למשימות שהם מבצעים. כדי להשיג תוצאה רצויה, יש צורך בהנחיה האפקטיבית ביותר, הכוללת בחירת המילים, הפורמטים, הביטויים או אפילו הסמלים הנכונים. גישה זו נקראת [הנדסת הנחיות](https://learn.microsoft.com/en-us/shows/ai-show/the-basics-of-prompt-engineering-with-azure-openai-service?WT.mc_id=academic-77998-bethanycheum).

[תיעוד זה](https://learn.microsoft.com/en-us/semantic-kernel/prompt-engineering/?WT.mc_id=academic-77998-bethanycheum) מספק מידע נוסף על הנדסת הנחיות.

## ✍️ מחברת לדוגמה: [משחק עם OpenAI-GPT](GPT-PyTorch.ipynb)

המשיכו ללמוד במחברות הבאות:

* [יצירת טקסט עם OpenAI-GPT ו-Hugging Face Transformers](GPT-PyTorch.ipynb)

## סיכום

מודלים חדשים של שפה מאומנים מראש לא רק ממדלים את מבנה השפה, אלא גם מכילים כמות עצומה של שפה טבעית. לכן, ניתן להשתמש בהם ביעילות כדי לפתור משימות NLP מסוימות במצבים של אפס או מעט דוגמאות.

## [שאלון לאחר ההרצאה](https://ff-quizzes.netlify.app/en/ai/quiz/40)

---

