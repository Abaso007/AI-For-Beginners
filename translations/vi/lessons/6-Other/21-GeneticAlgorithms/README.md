<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "893aa368cb485da704b466a0f3775587",
  "translation_date": "2025-08-29T12:12:14+00:00",
  "source_file": "lessons/6-Other/21-GeneticAlgorithms/README.md",
  "language_code": "vi"
}
-->
# Thuật toán Di truyền

## [Câu hỏi trước bài giảng](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/121)

**Thuật toán Di truyền** (GA) dựa trên cách tiếp cận **tiến hóa** trong AI, trong đó các phương pháp tiến hóa của một quần thể được sử dụng để tìm ra giải pháp tối ưu cho một vấn đề cụ thể. Thuật toán này được đề xuất vào năm 1975 bởi [John Henry Holland](https://wikipedia.org/wiki/John_Henry_Holland).

Thuật toán Di truyền dựa trên các ý tưởng sau:

* Các giải pháp hợp lệ cho vấn đề có thể được biểu diễn dưới dạng **gen**
* **Lai ghép** cho phép chúng ta kết hợp hai giải pháp lại với nhau để tạo ra một giải pháp mới hợp lệ
* **Chọn lọc** được sử dụng để chọn các giải pháp tối ưu hơn bằng cách sử dụng một **hàm đánh giá**
* **Đột biến** được giới thiệu để làm mất ổn định tối ưu hóa và giúp thoát khỏi cực tiểu cục bộ

Nếu bạn muốn triển khai một Thuật toán Di truyền, bạn cần:

 * Tìm một phương pháp mã hóa các giải pháp của vấn đề bằng **gen** g∈Γ
 * Trên tập hợp các gen Γ, cần định nghĩa **hàm đánh giá** fit: Γ→**R**. Giá trị hàm càng nhỏ thì giải pháp càng tốt.
 * Định nghĩa cơ chế **lai ghép** để kết hợp hai gen lại với nhau nhằm tạo ra một giải pháp mới hợp lệ crossover: Γ<sup>2</sub>→Γ.
 * Định nghĩa cơ chế **đột biến** mutate: Γ→Γ.

Trong nhiều trường hợp, lai ghép và đột biến là các thuật toán khá đơn giản để thao tác gen dưới dạng chuỗi số hoặc vector bit.

Việc triển khai cụ thể của một thuật toán di truyền có thể thay đổi tùy trường hợp, nhưng cấu trúc tổng quát như sau:

1. Chọn một quần thể ban đầu G⊂Γ
2. Ngẫu nhiên chọn một trong các thao tác sẽ được thực hiện ở bước này: lai ghép hoặc đột biến
3. **Lai ghép**:
  * Ngẫu nhiên chọn hai gen g<sub>1</sub>, g<sub>2</sub> ∈ G
  * Tính toán lai ghép g=crossover(g<sub>1</sub>,g<sub>2</sub>)
  * Nếu fit(g)<fit(g<sub>1</sub>) hoặc fit(g)<fit(g<sub>2</sub>) - thay thế gen tương ứng trong quần thể bằng g.
4. **Đột biến** - chọn ngẫu nhiên một gen g∈G và thay thế nó bằng mutate(g)
5. Lặp lại từ bước 2, cho đến khi đạt được giá trị fit đủ nhỏ, hoặc cho đến khi đạt giới hạn số bước.

## Nhiệm vụ điển hình

Các nhiệm vụ thường được giải quyết bằng Thuật toán Di truyền bao gồm:

1. Tối ưu hóa lịch trình
1. Tối ưu hóa đóng gói
1. Tối ưu hóa cắt
1. Tăng tốc tìm kiếm toàn diện

## ✍️ Bài tập: Thuật toán Di truyền

Tiếp tục học trong các notebook sau:

Truy cập [notebook này](Genetic.ipynb) để xem hai ví dụ về việc sử dụng Thuật toán Di truyền:

1. Phân chia kho báu công bằng
1. Bài toán 8 quân hậu

## Kết luận

Thuật toán Di truyền được sử dụng để giải quyết nhiều vấn đề, bao gồm các vấn đề về logistics và tìm kiếm. Lĩnh vực này được lấy cảm hứng từ nghiên cứu kết hợp các chủ đề trong Tâm lý học và Khoa học Máy tính.

## 🚀 Thử thách

"Thuật toán di truyền dễ triển khai, nhưng hành vi của chúng rất khó hiểu." [nguồn](https://wikipedia.org/wiki/Genetic_algorithm) Hãy nghiên cứu để tìm một triển khai của thuật toán di truyền, chẳng hạn như giải bài toán Sudoku, và giải thích cách nó hoạt động dưới dạng phác thảo hoặc sơ đồ luồng.

## [Câu hỏi sau bài giảng](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/221)

## Ôn tập & Tự học

Xem [video tuyệt vời này](https://www.youtube.com/watch?v=qv6UVOQ0F44) nói về cách máy tính học chơi Super Mario bằng mạng nơ-ron được huấn luyện bởi thuật toán di truyền. Chúng ta sẽ học thêm về cách máy tính học chơi các trò chơi như vậy [trong phần tiếp theo](../22-DeepRL/README.md).

## [Bài tập: Phương trình Diophantine](Diophantine.ipynb)

Mục tiêu của bạn là giải cái gọi là **phương trình Diophantine** - một phương trình với nghiệm nguyên. Ví dụ, hãy xem xét phương trình a+2b+3c+4d=30. Bạn cần tìm các nghiệm nguyên thỏa mãn phương trình này.

*Bài tập này được lấy cảm hứng từ [bài viết này](https://habr.com/post/128704/).*

Gợi ý:

1. Bạn có thể xem xét nghiệm trong khoảng [0;30]
1. Là một gen, hãy xem xét sử dụng danh sách các giá trị nghiệm

Sử dụng [Diophantine.ipynb](Diophantine.ipynb) làm điểm bắt đầu.

---

**Tuyên bố miễn trừ trách nhiệm**:  
Tài liệu này đã được dịch bằng dịch vụ dịch thuật AI [Co-op Translator](https://github.com/Azure/co-op-translator). Mặc dù chúng tôi cố gắng đảm bảo độ chính xác, xin lưu ý rằng các bản dịch tự động có thể chứa lỗi hoặc không chính xác. Tài liệu gốc bằng ngôn ngữ bản địa nên được coi là nguồn tham khảo chính thức. Đối với các thông tin quan trọng, chúng tôi khuyến nghị sử dụng dịch vụ dịch thuật chuyên nghiệp từ con người. Chúng tôi không chịu trách nhiệm cho bất kỳ sự hiểu lầm hoặc diễn giải sai nào phát sinh từ việc sử dụng bản dịch này.