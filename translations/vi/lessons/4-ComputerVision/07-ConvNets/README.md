<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "088837b42b7d99198bf62db8a42411e0",
  "translation_date": "2025-08-29T12:19:05+00:00",
  "source_file": "lessons/4-ComputerVision/07-ConvNets/README.md",
  "language_code": "vi"
}
-->
# Mạng Nơ-ron Tích chập

Chúng ta đã thấy trước đây rằng mạng nơ-ron rất tốt trong việc xử lý hình ảnh, và thậm chí một perceptron một lớp cũng có thể nhận diện chữ số viết tay từ tập dữ liệu MNIST với độ chính xác khá cao. Tuy nhiên, tập dữ liệu MNIST rất đặc biệt, tất cả các chữ số đều được căn giữa trong hình ảnh, điều này làm cho nhiệm vụ trở nên đơn giản hơn.

## [Câu hỏi trước bài giảng](https://ff-quizzes.netlify.app/en/ai/quiz/13)

Trong thực tế, chúng ta muốn có khả năng nhận diện các đối tượng trong một bức ảnh bất kể vị trí chính xác của chúng trong hình ảnh. Thị giác máy tính khác với phân loại thông thường, bởi vì khi chúng ta cố gắng tìm một đối tượng cụ thể trong hình ảnh, chúng ta sẽ quét hình ảnh để tìm kiếm các **mẫu** cụ thể và sự kết hợp của chúng. Ví dụ, khi tìm kiếm một con mèo, đầu tiên chúng ta có thể tìm các đường ngang, có thể tạo thành râu, và sau đó sự kết hợp nhất định của các râu có thể cho chúng ta biết rằng đó thực sự là hình ảnh của một con mèo. Vị trí tương đối và sự hiện diện của các mẫu nhất định là quan trọng, chứ không phải vị trí chính xác của chúng trong hình ảnh.

Để trích xuất các mẫu, chúng ta sẽ sử dụng khái niệm **bộ lọc tích chập**. Như bạn đã biết, một hình ảnh được biểu diễn bằng một ma trận 2D, hoặc một tensor 3D với độ sâu màu. Áp dụng một bộ lọc có nghĩa là chúng ta lấy một ma trận **kernel bộ lọc** tương đối nhỏ, và đối với mỗi pixel trong hình ảnh gốc, chúng ta tính trung bình có trọng số với các điểm lân cận. Chúng ta có thể hình dung điều này như một cửa sổ nhỏ trượt qua toàn bộ hình ảnh, và tính trung bình tất cả các pixel theo trọng số trong ma trận kernel bộ lọc.

![Bộ lọc cạnh dọc](../../../../../translated_images/filter-vert.b7148390ca0bc356ddc7e55555d2481819c1e86ddde9dce4db5e71a69d6f887f.vi.png) | ![Bộ lọc cạnh ngang](../../../../../translated_images/filter-horiz.59b80ed4feb946efbe201a7fe3ca95abb3364e266e6fd90820cb893b4d3a6dda.vi.png)
----|----

> Hình ảnh bởi Dmitry Soshnikov

Ví dụ, nếu chúng ta áp dụng các bộ lọc cạnh dọc và cạnh ngang 3x3 lên các chữ số MNIST, chúng ta có thể làm nổi bật (ví dụ: giá trị cao) nơi có các cạnh dọc và ngang trong hình ảnh gốc. Do đó, hai bộ lọc này có thể được sử dụng để "tìm kiếm" các cạnh. Tương tự, chúng ta có thể thiết kế các bộ lọc khác để tìm kiếm các mẫu cấp thấp khác:

> Hình ảnh của [Leung-Malik Filter Bank](https://www.robots.ox.ac.uk/~vgg/research/texclass/filters.html)

Tuy nhiên, trong khi chúng ta có thể thiết kế các bộ lọc để trích xuất một số mẫu một cách thủ công, chúng ta cũng có thể thiết kế mạng sao cho nó tự động học các mẫu. Đây là một trong những ý tưởng chính đằng sau CNN.

## Ý tưởng chính đằng sau CNN

Cách CNN hoạt động dựa trên các ý tưởng quan trọng sau:

* Bộ lọc tích chập có thể trích xuất các mẫu
* Chúng ta có thể thiết kế mạng sao cho các bộ lọc được huấn luyện tự động
* Chúng ta có thể sử dụng cùng một phương pháp để tìm kiếm các mẫu trong các đặc trưng cấp cao, không chỉ trong hình ảnh gốc. Do đó, việc trích xuất đặc trưng của CNN hoạt động trên một hệ thống phân cấp các đặc trưng, bắt đầu từ các tổ hợp pixel cấp thấp, đến các tổ hợp cấp cao hơn của các phần hình ảnh.

![Trích xuất đặc trưng phân cấp](../../../../../translated_images/FeatureExtractionCNN.d9b456cbdae7cb643fde3032b81b2940e3cf8be842e29afac3f482725ba7f95c.vi.png)

> Hình ảnh từ [một bài báo của Hislop-Lynch](https://www.semanticscholar.org/paper/Computer-vision-based-pedestrian-trajectory-Hislop-Lynch/26e6f74853fc9bbb7487b06dc2cf095d36c9021d), dựa trên [nghiên cứu của họ](https://dl.acm.org/doi/abs/10.1145/1553374.1553453)

## ✍️ Bài tập: Mạng Nơ-ron Tích chập

Hãy tiếp tục khám phá cách mạng nơ-ron tích chập hoạt động, và cách chúng ta có thể đạt được các bộ lọc có thể huấn luyện, bằng cách làm việc qua các notebook tương ứng:

* [Mạng Nơ-ron Tích chập - PyTorch](ConvNetsPyTorch.ipynb)
* [Mạng Nơ-ron Tích chập - TensorFlow](ConvNetsTF.ipynb)

## Kiến trúc Kim tự tháp

Hầu hết các CNN được sử dụng để xử lý hình ảnh đều tuân theo cái gọi là kiến trúc kim tự tháp. Lớp tích chập đầu tiên được áp dụng lên hình ảnh gốc thường có số lượng bộ lọc tương đối thấp (8-16), tương ứng với các tổ hợp pixel khác nhau, chẳng hạn như các đường ngang/dọc hoặc nét. Ở cấp độ tiếp theo, chúng ta giảm kích thước không gian của mạng, và tăng số lượng bộ lọc, tương ứng với nhiều tổ hợp hơn của các đặc trưng đơn giản. Với mỗi lớp, khi chúng ta tiến tới bộ phân loại cuối cùng, kích thước không gian của hình ảnh giảm, và số lượng bộ lọc tăng lên.

Ví dụ, hãy xem kiến trúc của VGG-16, một mạng đạt được độ chính xác 92.7% trong phân loại top-5 của ImageNet vào năm 2014:

![Các lớp của ImageNet](../../../../../translated_images/vgg-16-arch1.d901a5583b3a51baeaab3e768567d921e5d54befa46e1e642616c5458c934028.vi.jpg)

![Kim tự tháp của ImageNet](../../../../../translated_images/vgg-16-arch.64ff2137f50dd49fdaa786e3f3a975b3f22615efd13efb19c5d22f12e01451a1.vi.jpg)

> Hình ảnh từ [Researchgate](https://www.researchgate.net/figure/Vgg16-model-structure-To-get-the-VGG-NIN-model-we-replace-the-2-nd-4-th-6-th-7-th_fig2_335194493)

## Các Kiến trúc CNN Nổi tiếng

[Tiếp tục nghiên cứu về các kiến trúc CNN nổi tiếng](CNN_Architectures.md)

---

**Tuyên bố miễn trừ trách nhiệm**:  
Tài liệu này đã được dịch bằng dịch vụ dịch thuật AI [Co-op Translator](https://github.com/Azure/co-op-translator). Mặc dù chúng tôi cố gắng đảm bảo độ chính xác, xin lưu ý rằng các bản dịch tự động có thể chứa lỗi hoặc không chính xác. Tài liệu gốc bằng ngôn ngữ bản địa nên được coi là nguồn tham khảo chính thức. Đối với các thông tin quan trọng, chúng tôi khuyến nghị sử dụng dịch vụ dịch thuật chuyên nghiệp từ con người. Chúng tôi không chịu trách nhiệm cho bất kỳ sự hiểu lầm hoặc diễn giải sai nào phát sinh từ việc sử dụng bản dịch này.