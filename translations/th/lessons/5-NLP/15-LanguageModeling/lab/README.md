<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "5130f01fdc5ebb83032b23d489027aac",
  "translation_date": "2025-08-29T09:19:22+00:00",
  "source_file": "lessons/5-NLP/15-LanguageModeling/lab/README.md",
  "language_code": "th"
}
-->
# การฝึกโมเดล Skip-Gram

งานในห้องปฏิบัติการจาก [AI for Beginners Curriculum](https://github.com/microsoft/ai-for-beginners).

## งานที่ต้องทำ

ในห้องปฏิบัติการนี้ เราท้าทายให้คุณฝึกโมเดล Word2Vec โดยใช้เทคนิค Skip-Gram ฝึกเครือข่ายที่มี embedding เพื่อทำนายคำที่อยู่ใกล้เคียงในหน้าต่าง Skip-Gram ที่กว้าง $N$ โทเค็น คุณสามารถใช้ [โค้ดจากบทเรียนนี้](../CBoW-TF.ipynb) และปรับเปลี่ยนเล็กน้อย

## ชุดข้อมูล

คุณสามารถใช้หนังสือใดก็ได้ คุณสามารถค้นหาข้อความฟรีจำนวนมากได้ที่ [Project Gutenberg](https://www.gutenberg.org/) ตัวอย่างเช่น นี่คือลิงก์ตรงไปยัง [Alice's Adventures in Wonderland](https://www.gutenberg.org/files/11/11-0.txt) โดย Lewis Carroll หรือคุณสามารถใช้บทละครของ Shakespeare ซึ่งคุณสามารถดึงข้อมูลได้โดยใช้โค้ดต่อไปนี้:

```python
path_to_file = tf.keras.utils.get_file(
   'shakespeare.txt', 
   'https://storage.googleapis.com/download.tensorflow.org/data/shakespeare.txt')
text = open(path_to_file, 'rb').read().decode(encoding='utf-8')
```

## สำรวจ!

หากคุณมีเวลาและต้องการเจาะลึกในหัวข้อนี้ ลองสำรวจสิ่งต่าง ๆ ต่อไปนี้:

* ขนาดของ embedding มีผลต่อผลลัพธ์อย่างไร?
* สไตล์ข้อความที่แตกต่างกันมีผลต่อผลลัพธ์อย่างไร?
* เลือกคำที่มีความแตกต่างกันมากและคำพ้องความหมายของมันหลายคำ นำเสนอเวกเตอร์ของคำเหล่านั้น ใช้ PCA เพื่อลดมิติลงเหลือ 2 และวาดกราฟในพื้นที่ 2 มิติ คุณเห็นรูปแบบอะไรบ้าง?

---

**ข้อจำกัดความรับผิดชอบ**:  
เอกสารนี้ได้รับการแปลโดยใช้บริการแปลภาษา AI [Co-op Translator](https://github.com/Azure/co-op-translator) แม้ว่าเราจะพยายามให้การแปลมีความถูกต้อง แต่โปรดทราบว่าการแปลอัตโนมัติอาจมีข้อผิดพลาดหรือความไม่แม่นยำ เอกสารต้นฉบับในภาษาต้นทางควรถือเป็นแหล่งข้อมูลที่เชื่อถือได้ สำหรับข้อมูลที่สำคัญ ขอแนะนำให้ใช้บริการแปลภาษามนุษย์มืออาชีพ เราจะไม่รับผิดชอบต่อความเข้าใจผิดหรือการตีความที่ผิดพลาดซึ่งเกิดจากการใช้การแปลนี้