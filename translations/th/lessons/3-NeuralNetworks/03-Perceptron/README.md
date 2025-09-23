<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "0c37770bba4fff3c71dc00eb261ee61b",
  "translation_date": "2025-08-29T09:09:36+00:00",
  "source_file": "lessons/3-NeuralNetworks/03-Perceptron/README.md",
  "language_code": "th"
}
-->
# บทนำสู่โครงข่ายประสาทเทียม: เพอร์เซปตรอน

## [แบบทดสอบก่อนเรียน](https://ff-quizzes.netlify.app/en/ai/quiz/5)

หนึ่งในความพยายามแรก ๆ ในการสร้างสิ่งที่คล้ายกับโครงข่ายประสาทเทียมสมัยใหม่เกิดขึ้นโดย Frank Rosenblatt จาก Cornell Aeronautical Laboratory ในปี 1957 ซึ่งเป็นการสร้างฮาร์ดแวร์ที่เรียกว่า "Mark-1" ออกแบบมาเพื่อจดจำรูปทรงเรขาคณิตพื้นฐาน เช่น สามเหลี่ยม สี่เหลี่ยม และวงกลม

|      |      |
|--------------|-----------|
|<img src='images/Rosenblatt-wikipedia.jpg' alt='Frank Rosenblatt'/> | <img src='images/Mark_I_perceptron_wikipedia.jpg' alt='The Mark 1 Perceptron' />|

> รูปภาพ [จาก Wikipedia](https://en.wikipedia.org/wiki/Perceptron)

ภาพอินพุตถูกแทนด้วยอาร์เรย์โฟโตเซลล์ขนาด 20x20 ดังนั้นโครงข่ายประสาทเทียมจึงมีอินพุต 400 ตัวและเอาต์พุตแบบไบนารีหนึ่งตัว เครือข่ายง่าย ๆ นี้มีเพียงนิวรอนเดียว ซึ่งเรียกอีกอย่างว่า **threshold logic unit** น้ำหนักของโครงข่ายประสาทเทียมทำหน้าที่เหมือนตัวต้านทานปรับค่าได้ที่ต้องปรับด้วยมือในระหว่างขั้นตอนการฝึก

> ✅ ตัวต้านทานปรับค่าได้ (potentiometer) คืออุปกรณ์ที่ช่วยให้ผู้ใช้ปรับค่าความต้านทานในวงจรได้

> หนังสือพิมพ์ The New York Times เขียนเกี่ยวกับเพอร์เซปตรอนในเวลานั้นว่า: *ตัวอ่อนของคอมพิวเตอร์อิเล็กทรอนิกส์ที่ [กองทัพเรือ] คาดว่าจะสามารถเดิน พูด มองเห็น เขียน สืบพันธุ์ตัวเอง และตระหนักถึงการมีอยู่ของตัวเองได้*

## โมเดลเพอร์เซปตรอน

สมมติว่าเรามีคุณลักษณะ (features) N ตัวในโมเดลของเรา ซึ่งในกรณีนี้เวกเตอร์อินพุตจะเป็นเวกเตอร์ขนาด N เพอร์เซปตรอนเป็นโมเดลสำหรับ **การจำแนกประเภทแบบไบนารี** นั่นคือสามารถแยกแยะระหว่างสองคลาสของข้อมูลอินพุตได้ เราจะสมมติว่าสำหรับเวกเตอร์อินพุต x แต่ละตัว เอาต์พุตของเพอร์เซปตรอนจะเป็น +1 หรือ -1 ขึ้นอยู่กับคลาส โดยเอาต์พุตจะคำนวณด้วยสูตร:

y(x) = f(w<sup>T</sup>x)

โดยที่ f คือฟังก์ชันการกระตุ้นแบบขั้นบันได (step activation function)

<!-- img src="http://www.sciweavers.org/tex2img.php?eq=f%28x%29%20%3D%20%5Cbegin%7Bcases%7D%0A%20%20%20%20%20%20%20%20%20%2B1%20%26%20x%20%5Cgeq%200%20%5C%5C%0A%20%20%20%20%20%20%20%20%20-1%20%26%20x%20%3C%200%0A%20%20%20%20%20%20%20%5Cend%7Bcases%7D%20%5C%5C%0A&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0" align="center" border="0" alt="f(x) = \begin{cases} +1 & x \geq 0 \\ -1 & x < 0 \end{cases} \\" width="154" height="50" / -->
<img src="images/activation-func.png"/>

## การฝึกเพอร์เซปตรอน

เพื่อฝึกเพอร์เซปตรอน เราจำเป็นต้องหาน้ำหนักเวกเตอร์ w ที่สามารถจำแนกค่าต่าง ๆ ได้ถูกต้องมากที่สุด หรือกล่าวอีกนัยหนึ่งคือทำให้ **ข้อผิดพลาด** (error) มีค่าน้อยที่สุด ข้อผิดพลาด E นี้ถูกกำหนดโดย **เกณฑ์ของเพอร์เซปตรอน** (perceptron criterion) ดังนี้:

E(w) = -∑w<sup>T</sup>x<sub>i</sub>t<sub>i</sub>

โดยที่:

* ผลรวมจะคำนวณจากจุดข้อมูลการฝึก i ที่จำแนกผิด
* x<sub>i</sub> คือข้อมูลอินพุต และ t<sub>i</sub> คือ -1 หรือ +1 สำหรับตัวอย่างที่เป็นลบและบวกตามลำดับ

เกณฑ์นี้ถือว่าเป็นฟังก์ชันของน้ำหนัก w และเราจำเป็นต้องทำให้มันมีค่าน้อยที่สุด โดยทั่วไปจะใช้วิธีที่เรียกว่า **gradient descent** ซึ่งเริ่มต้นด้วยน้ำหนักเริ่มต้น w<sup>(0)</sup> และในแต่ละขั้นตอนจะอัปเดตน้ำหนักตามสูตร:

w<sup>(t+1)</sup> = w<sup>(t)</sup> - η∇E(w)

ที่นี่ η คือ **อัตราการเรียนรู้** (learning rate) และ ∇E(w) หมายถึง **กราดิเอนต์** ของ E หลังจากคำนวณกราดิเอนต์แล้ว เราจะได้:

w<sup>(t+1)</sup> = w<sup>(t)</sup> + ∑ηx<sub>i</sub>t<sub>i</sub>

อัลกอริทึมใน Python มีลักษณะดังนี้:

```python
def train(positive_examples, negative_examples, num_iterations = 100, eta = 1):

    weights = [0,0,0] # Initialize weights (almost randomly :)
        
    for i in range(num_iterations):
        pos = random.choice(positive_examples)
        neg = random.choice(negative_examples)

        z = np.dot(pos, weights) # compute perceptron output
        if z < 0: # positive example classified as negative
            weights = weights + eta*weights.shape

        z  = np.dot(neg, weights)
        if z >= 0: # negative example classified as positive
            weights = weights - eta*weights.shape

    return weights
```

## สรุป

ในบทเรียนนี้ คุณได้เรียนรู้เกี่ยวกับเพอร์เซปตรอน ซึ่งเป็นโมเดลสำหรับการจำแนกประเภทแบบไบนารี และวิธีการฝึกโดยใช้น้ำหนักเวกเตอร์

## 🚀 ความท้าทาย

หากคุณต้องการลองสร้างเพอร์เซปตรอนของคุณเอง ลองดู [แลปนี้บน Microsoft Learn](https://docs.microsoft.com/en-us/azure/machine-learning/component-reference/two-class-averaged-perceptron?WT.mc_id=academic-77998-cacaste) ซึ่งใช้ [Azure ML designer](https://docs.microsoft.com/en-us/azure/machine-learning/concept-designer?WT.mc_id=academic-77998-cacaste)

## [แบบทดสอบหลังเรียน](https://ff-quizzes.netlify.app/en/ai/quiz/6)

## การทบทวนและการศึกษาด้วยตนเอง

เพื่อดูว่าเราสามารถใช้เพอร์เซปตรอนในการแก้ปัญหาแบบง่าย ๆ และปัญหาในชีวิตจริงได้อย่างไร และเพื่อเรียนรู้เพิ่มเติม - ไปที่ [Perceptron](Perceptron.ipynb) โน้ตบุ๊ก

นี่คือ [บทความที่น่าสนใจเกี่ยวกับเพอร์เซปตรอน](https://towardsdatascience.com/what-is-a-perceptron-basics-of-neural-networks-c4cfea20c590) เช่นกัน

## [การบ้าน](lab/README.md)

ในบทเรียนนี้ เราได้สร้างเพอร์เซปตรอนสำหรับงานการจำแนกประเภทแบบไบนารี และเราได้ใช้มันเพื่อจำแนกระหว่างตัวเลขเขียนด้วยมือสองตัว ในแลปนี้ คุณถูกขอให้แก้ปัญหาการจำแนกตัวเลขทั้งหมด กล่าวคือกำหนดว่าตัวเลขใดมีแนวโน้มที่จะตรงกับภาพที่กำหนดมากที่สุด

* [คำแนะนำ](lab/README.md)
* [โน้ตบุ๊ก](lab/PerceptronMultiClass.ipynb)

---

**ข้อจำกัดความรับผิดชอบ**:  
เอกสารนี้ได้รับการแปลโดยใช้บริการแปลภาษา AI [Co-op Translator](https://github.com/Azure/co-op-translator) แม้ว่าเราจะพยายามให้การแปลมีความถูกต้องมากที่สุด แต่โปรดทราบว่าการแปลอัตโนมัติอาจมีข้อผิดพลาดหรือความไม่ถูกต้อง เอกสารต้นฉบับในภาษาดั้งเดิมควรถือเป็นแหล่งข้อมูลที่เชื่อถือได้ สำหรับข้อมูลที่สำคัญ ขอแนะนำให้ใช้บริการแปลภาษามืออาชีพ เราไม่รับผิดชอบต่อความเข้าใจผิดหรือการตีความผิดที่เกิดจากการใช้การแปลนี้