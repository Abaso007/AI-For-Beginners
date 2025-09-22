<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "2f7b97b375358cb51a1e098df306bf73",
  "translation_date": "2025-08-29T12:19:43+00:00",
  "source_file": "lessons/4-ComputerVision/07-ConvNets/CNN_Architectures.md",
  "language_code": "vi"
}
-->
# Các Kiến Trúc CNN Nổi Tiếng

### VGG-16

VGG-16 là một mạng đạt độ chính xác 92.7% trong phân loại top-5 của ImageNet vào năm 2014. Nó có cấu trúc các lớp như sau:

![ImageNet Layers](../../../../../translated_images/vgg-16-arch1.d901a5583b3a51baeaab3e768567d921e5d54befa46e1e642616c5458c934028.vi.jpg)

Như bạn có thể thấy, VGG tuân theo kiến trúc hình kim tự tháp truyền thống, là một chuỗi các lớp tích chập và pooling.

![ImageNet Pyramid](../../../../../translated_images/vgg-16-arch.64ff2137f50dd49fdaa786e3f3a975b3f22615efd13efb19c5d22f12e01451a1.vi.jpg)

> Hình ảnh từ [Researchgate](https://www.researchgate.net/figure/Vgg16-model-structure-To-get-the-VGG-NIN-model-we-replace-the-2-nd-4-th-6-th-7-th_fig2_335194493)

### ResNet

ResNet là một họ các mô hình được đề xuất bởi Microsoft Research vào năm 2015. Ý tưởng chính của ResNet là sử dụng **khối dư**:

<img src="images/resnet-block.png" width="300"/>

> Hình ảnh từ [bài báo này](https://arxiv.org/pdf/1512.03385.pdf)

Lý do sử dụng đường dẫn nhận dạng là để lớp của chúng ta dự đoán **sự khác biệt** giữa kết quả của lớp trước đó và đầu ra của khối dư - do đó có tên gọi *residual*. Những khối này dễ huấn luyện hơn nhiều, và người ta có thể xây dựng các mạng với hàng trăm khối dư (các biến thể phổ biến nhất là ResNet-52, ResNet-101 và ResNet-152).

Bạn cũng có thể nghĩ về mạng này như khả năng điều chỉnh độ phức tạp của nó theo dữ liệu. Ban đầu, khi bạn bắt đầu huấn luyện mạng, giá trị trọng số nhỏ, và phần lớn tín hiệu đi qua các lớp nhận dạng. Khi quá trình huấn luyện tiến triển và trọng số trở nên lớn hơn, tầm quan trọng của các tham số mạng tăng lên, và mạng điều chỉnh để phù hợp với khả năng biểu đạt cần thiết để phân loại chính xác các hình ảnh huấn luyện.

### Google Inception

Kiến trúc Google Inception đưa ý tưởng này tiến xa hơn, và xây dựng mỗi lớp mạng như một sự kết hợp của nhiều đường dẫn khác nhau:

<img src="images/inception.png" width="400"/>

> Hình ảnh từ [Researchgate](https://www.researchgate.net/figure/Inception-module-with-dimension-reductions-left-and-schema-for-Inception-ResNet-v1_fig2_355547454)

Ở đây, chúng ta cần nhấn mạnh vai trò của các tích chập 1x1, bởi vì ban đầu chúng có vẻ không hợp lý. Tại sao chúng ta cần chạy qua hình ảnh với bộ lọc 1x1? Tuy nhiên, bạn cần nhớ rằng các bộ lọc tích chập cũng hoạt động với nhiều kênh độ sâu (ban đầu là màu RGB, trong các lớp tiếp theo là các kênh cho các bộ lọc khác nhau), và tích chập 1x1 được sử dụng để trộn các kênh đầu vào này với nhau bằng các trọng số có thể huấn luyện. Nó cũng có thể được xem như là giảm mẫu (pooling) trên chiều kênh.

Đây là [một bài viết blog hay](https://medium.com/analytics-vidhya/talented-mr-1x1-comprehensive-look-at-1x1-convolution-in-deep-learning-f6b355825578) về chủ đề này, và [bài báo gốc](https://arxiv.org/pdf/1312.4400.pdf).

### MobileNet

MobileNet là một họ các mô hình có kích thước giảm, phù hợp cho các thiết bị di động. Sử dụng chúng nếu bạn thiếu tài nguyên và có thể chấp nhận hy sinh một chút độ chính xác. Ý tưởng chính đằng sau chúng là **tích chập phân tách theo chiều sâu**, cho phép biểu diễn các bộ lọc tích chập bằng sự kết hợp của các tích chập không gian và tích chập 1x1 trên các kênh độ sâu. Điều này làm giảm đáng kể số lượng tham số, khiến mạng nhỏ hơn về kích thước, và cũng dễ huấn luyện hơn với ít dữ liệu.

Đây là [một bài viết blog hay về MobileNet](https://medium.com/analytics-vidhya/image-classification-with-mobilenet-cc6fbb2cd470).

## Kết luận

Trong bài học này, bạn đã học được khái niệm chính đằng sau các mạng nơ-ron thị giác máy tính - mạng tích chập. Các kiến trúc thực tế hỗ trợ phân loại hình ảnh, phát hiện đối tượng, và thậm chí các mạng tạo hình ảnh đều dựa trên CNN, chỉ với nhiều lớp hơn và một số mẹo huấn luyện bổ sung.

## 🚀 Thử thách

Trong các notebook đi kèm, có các ghi chú ở cuối về cách đạt được độ chính xác cao hơn. Hãy thử nghiệm để xem liệu bạn có thể đạt được độ chính xác cao hơn không.

## [Câu hỏi sau bài giảng](https://ff-quizzes.netlify.app/en/ai/quiz/14)

## Ôn tập & Tự học

Mặc dù CNN thường được sử dụng cho các nhiệm vụ Thị giác Máy tính, chúng cũng rất tốt trong việc trích xuất các mẫu có kích thước cố định. Ví dụ, nếu chúng ta đang xử lý âm thanh, chúng ta cũng có thể muốn sử dụng CNN để tìm kiếm một số mẫu cụ thể trong tín hiệu âm thanh - trong trường hợp này, các bộ lọc sẽ là 1 chiều (và CNN này sẽ được gọi là 1D-CNN). Ngoài ra, đôi khi 3D-CNN được sử dụng để trích xuất các đặc điểm trong không gian đa chiều, chẳng hạn như các sự kiện nhất định xảy ra trong video - CNN có thể nắm bắt các mẫu thay đổi đặc điểm theo thời gian. Hãy ôn tập và tự học về các nhiệm vụ khác có thể được thực hiện với CNN.

## [Bài tập](lab/README.md)

Trong bài thực hành này, bạn được giao nhiệm vụ phân loại các giống mèo và chó khác nhau. Những hình ảnh này phức tạp hơn so với tập dữ liệu MNIST, có kích thước lớn hơn, và có hơn 10 lớp.

---

**Tuyên bố miễn trừ trách nhiệm**:  
Tài liệu này đã được dịch bằng dịch vụ dịch thuật AI [Co-op Translator](https://github.com/Azure/co-op-translator). Mặc dù chúng tôi cố gắng đảm bảo độ chính xác, xin lưu ý rằng các bản dịch tự động có thể chứa lỗi hoặc không chính xác. Tài liệu gốc bằng ngôn ngữ bản địa nên được coi là nguồn thông tin chính thức. Đối với các thông tin quan trọng, khuyến nghị sử dụng dịch vụ dịch thuật chuyên nghiệp bởi con người. Chúng tôi không chịu trách nhiệm cho bất kỳ sự hiểu lầm hoặc diễn giải sai nào phát sinh từ việc sử dụng bản dịch này.