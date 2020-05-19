# Flyweight design pattern
|[Quay lại](../README.md)|[Đọc tiếp]()|
|:-----------|-----------:|
## Định nghĩa

Fly weight là một mẫu thiết kế cấu trúc <u><b>(structural design pattern)</b></u> cho phép các chương trình hỗ trợ số lượng lớn đối tượng tương tự bằng cách giữ mức tiêu thụ bộ nhớ thấp. 

Hay nói cách khác cho phép chương trình phù hợp với Bộ nhớ RAM sẵn có bằng cách chia sẻ các phần trạng thái chung giữa nhiều đối tượng thay vì lưu trữ tất cả dữ liệu trong mỗi đối tượng.

## Vấn đề gặp phải (Problem)
    
### Mục đích sử dụng:
Mẫu thiết kế cấu trúc <u><b>Flyweight</b></u> có một mục đích duy nhất là giảm thiểu lượng bộ nhớ. Nếu chương trình của bạn không đấu tranh với sự thiếu hụt RAM, thì bạn có thể bỏ qua mẫu thiết kế này trong thời gian đầu.

### Nhận biết mẫu thiết kế này: 
<u><b>Flyweight</b></u>: có thể được nhận ra bằng một phương thức khởi tạo trả về các đối tượng được lưu trong bộ nhớ cache (nếu nó tồn tại) thay vì tạo mới.

## Khả năng ứng dụng (Applicability)

- Sử dụng Flyweight chỉ khi chương trình của bạn phải hỗ trợ 1 số lượng lớn đối tượng khi mà bộ nhớ RAM của bạn có hạn.

- Lợi ích của việc áp dụng mẫu thiết kế này phụ thuộc rất nhiều vào cách thức và nơi mà nó sử dụng. Nó có ích nhất khi:
    * Một ứng dụng cần sinh ra một số lượng lớn các đối tượng tương tự nhau.
    * Điều này làm cạn kiệt tất cả lượng RAM có sẵn trên thiết bị đích.
    * Các đối tượng chứa các trạng thái giống nhau có thể được export và shared giữa nhiều đối tượng.

## Ý tưởng triển khai (How to Implement)
 
Cách triển khai mẫu thiết kế này thường bao gồm 5 bước sau:

1. Chia các fields của 1 class thành 2 phần:
    * Trạng thái nội tại (The intrinsic state - Trạng thái có sẵn): các trường chứa dữ liệu không thay đổi được nhân đôi trên nhiều đối tượng
    * Trạng thái bên ngoài (The extrinsic state): các trường chứa dữ liệu theo ngữ cảnh duy nhất cho từng đối tượng.
2. Để lại các trường đại diện cho trạng thái nội tại trong class, nhưng hãy chắc chắn rằng chúng không thay đổi. Họ chỉ nên lấy giá trị ban đầu của họ bên trong hàm tạo (constructor).
3. Đi qua các phương thức sử dụng các trường của trạng thái bên ngoài. Đối với mỗi trường được sử dụng trong phương thức, hãy đưa vào một tham số mới và sử dụng nó thay vì trường.
4. Thêm nữa, tạo 1 factory class để quản lý nhóm các flyweights. Nó nên kiểm tra một flyweight đã tồn tại trước khi tạo ra 1 flyweight mới. Khi một factory đã hoạt động, Clients chỉ cần gửi request flyweights tới nó. Chúng ta nên định nghĩa 1 flyweight bằng cách chuyển trạng thái nội tại của nó tới factory.
5. Khách hàng phải lưu trữ và tính toán giá trị cho trạng trái mới (trạng thái bên ngoài) để có thể gọi các phương thức của các đối tượng flyweight. Để thuận tiện, trạng thái bên ngoài cùng với trường tham chiếu flyweight có thể được chuyển sang một lớp ngữ cảnh riêng. 

## Ưu và nhược điểm (Pros and Cons)
| Ưu điểm | Nhược điểm  |
|:---------|:-------------|
|- Bạn có thể tiết kiệm rất nhiều RAM, giả sử chương trình của bạn có hàng triệu triệu các đối tượng tương tự nhau.|- Bạn có thể giao dịch RAM theo chu kỳ CPU khi một số dữ liệu ngữ cảnh cần được tính toán lại mỗi khi ai đó gọi phương thức flyweight.|
||- Code của bạn sẽ trở nên phức tạp hơn nhiều. Các thành viên mới của nhóm sẽ luôn tự hỏi tại sao trạng thái của một thực thể được tách ra theo cách như vậy.|

## Mối quan hệ với các mẫu thiết kế khác (Relations with Other Patterns )

- Bạn có thể triển khai mẫu nè với mẫu `Composite pattern` để tiết kiệm RAM.
- <u><b>Flyweight</b></u> chỉ ra cách tạo ra nhiều đối tượng nhỏ, trong khi <u><b>Facade</b></u> chỉ ra cách tạo một đối tượng duy nhất đại diện cho toàn bộ hệ thống con.
- <u><b>Flyweight</b></u> sẽ giống với <u><b>Singleton</b></u> nếu như bạn quản lý bằng cách nào để giảm bớt tất cả các trạng thái được chia sẻ của các đối tượng thành chỉ một đối tượng <u><b>Flyweight</b></u>. Nhưng có hai sự khác biệt cơ bản giữa các mẫu này:
    1. Chỉ nên có một instance Singleton, trong khi một class Flyweight có thể có nhiều instances với các trạng thái nội tại khác nhau.
    2. Đối tượng Singleton object có thể thay đổi (mutable). Flyweight objects thì không thay đổi (immutable)

|[Quay lại](../README.md)|[Đọc tiếp]()|
|:-----------|-----------:|
