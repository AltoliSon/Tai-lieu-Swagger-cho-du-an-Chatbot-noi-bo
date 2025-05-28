....# Tai-lieu-Swagger-cho-du-an-Chatbot-noi-bo
Để xây dựng tài liệu API đầy đủ cho chatbot nội bộ, chúng ta cần tuần tự thực hiện các bước như sau:

1. Phân tích API
2. Tổ chức nội dung theo module
3. Viết file cấu hình Swagger/OpenAPI (YAML/JSON) với schema chi tiết
4. Kiểm tra tính hợp lệ và cuối cùng là hiển thị tài liệu qua giao diện Swagger UI.
=> Mục tiêu là tài liệu phải mô tả toàn bộ các API hiện có cho 3 phần chính của hệ thống: **Upload tài liệu**, **Giao tiếp Chatbot**, và **Quản lý thẻ FAQ (Cards)**. Tài liệu sẽ phục vụ cả team backend lẫn team design, nên cần rõ ràng, có mô tả dễ hiểu từng endpoint kèm ví dụ minh họa

# Swagger - Công cụ viết tài liệu cho restfull API
Viết tài liệu API với mục đích là để hướng dẫn bên thứ ba sử dụng. Tài liệu hướng dẫn sử dụng API là một nội dung kỹ thuật, chứa tất cả các thông tin được yêu cầu để có thể làm việc với API. Bao gồm thông tin chi tiết về các tài nguyên, phương thức, các request và response, thông tin xác thực...
### Tại sao tài liệu hướng dẫn API lại quan trọng?
Sản phẩm của chúng ta có thể là tốt và chất lượng nhất, nhưng sẽ không có ai biết sử dụng nếu không biết nó vận hành như thế nào và công dụng của nó là gì. => Vậy nên, Swagger được sinh ra để trở thành một công cụ tối ưu hóa thông tin tài liệu để các Dev có thể dễ dàng trong việc xây dựng sản phẩm. Dưới đây sẽ liệt kê một số tầm quan trọng của tài liệu hướng dẫn API:

- Cải thiện trải nghiệm người dùng: khi có một tài liệu hướng dẫn tốt, người dùng sẽ dễ dàng hơn trong việc tiếp cận hiểu về dịch vụ hay sản phẩm đó
- Tiết kiệm thời gian và chi phí: tài liệu hướng dẫn tốt, giúp giảm lượng thời gian phải bỏ ra để hỗ trợ người dùng mới, các thành viên hoặc team đối tác...Ví dụ: khi ta cung cấp cho người dùng tài liệu hướng dẫn test API trước khi triển khai, bạn sẽ tiết kiệm cho team mình thời gian một cách đáng kể như trả lời email, các cuộc gọi hỗ trợ

### OpenAPI là gì?
Là một định dạng mô tả API dành cho REST APIs. Một file OpenAPI cho phép bạn mô tả toàn bộ API bao gồm: 

- Cho phép những endpoints(/users) và cách thức hoạt động của mỗi andpoint(GET, POST, PUT, DELETE)
- Các tham số đầu vào và đầu ra của mỗi API
- Phương thức xác thực
- Thông tin liên hệ, chứng chỉ(HTTP/HTTPS) và những thông tin khác.
- OpenAPI có thể được viết dưới dạng YAML hoặc JSON.

### Swagger là gì?
Là một công cụ mã nguồn mở để xây dựng OpenAPI specifications giúp thiết kế, xây dựng tài liệu và sử dụng REST APIs.

<div style="text-align: center; border: 1px solid #ccc;">
  <img src="https://github.com/user-attachments/assets/41a992b0-7850-4175-8aed-1700a07eaac7" alt="Ảnh mẫu" style="max-width: 300px; max-height: 200px;">
</div>

🧰 Swagger cung cấp 3 tools chính cho các develops:
- **Swagger-editor**: dùng để design lên các APIs hoàn toàn mới hoặc edit lại các APIs có sẵn thông qua một 1 file config.
- **Swagger-Codegen**: dùng để generate ra code từ các file config có sẵn.
- **Swagger-UI**: dùng để generate ra file html, css từ một file config. (Được người dùng ưa chuộng nhất)

 Có 2 cách tiếp cận chính khi viết document cho Swagger như sau:
 - **Top-down approach**: Thiết kế API trước khi code
 - **Bottom-up approach**: từ các API có sẵn thiết kế file config để mô tả chúng.

Thông thường người dùng sẽ chọn Swagger-UI để giao diện từ tài liệu fiel config dưới dạng chuẩn OpenAPI. Giao diện được hiện ra rõ ràng và tường minh cho cả lập trình viên và người dùng. Các bạn có thể truy cập link demo với Swagger-UI theo: [link Swagger-ui](http://petstore.swagger.io/)
Như vậy tại giao diện sẽ cung cấp rõ các thông tin như: thông tin dự án, các API được cung cấp, method, và url tương ứng của nó. 

<div style="text-align: center; border: 1px solid #ccc;">
  <img src="https://github.com/user-attachments/assets/f072da31-4ca5-4caa-b411-3807115cc9ff" alt="Ảnh mẫu" style="max-width: 300px; max-height: 200px;">
</div>

Với mỗi API chúng ta có thể biết được chi tiết input và output cũng như trường nào bắt buộc gủi lên, kết quả trả về có thể nhận được những Status nào. Đặc biệt ta có thể input data để thử kiểm tra kết quả. 

<div style="text-align: center; border: 1px solid #ccc;">
  <img src="https://github.com/user-attachments/assets/e0df50a4-01bf-43d9-9bbd-f8eeb0c053d5" alt="Ảnh mẫu" style="max-width: 300px; max-height: 200px;">
</div>

### Cấu trúc cơ bản của Swagger 
Một cấu trúc hoàn thiện được thể hiện như sau: [editor](https://editor.swagger.io)
**Phần Infor**: Mỗi OpenAPIs sẽ bắt đầu với từ khóa openAPI để khai báo phiên bản(ví dụ: openApi: 3.0.0). Phiên bản này sẽ định nghĩa toàn bộ cấu trúc của API. Phần infor sẽ gồm:
- title: tên API
- description: thông tin mô tả về API, có thể viết thành nhiều dòng & hỗ trợ cú pháp Markdown.
- infor: thông tin liên hệ, chứng chỉ, điều khoản sử dụng và thông tin khai thác.
- version: phiên bản API.

<div style="text-align: center; border: 1px solid #ccc;">
  <img src="https://github.com/user-attachments/assets/1305247a-ead8-4cc1-a571-d8e673876f07" alt="Ảnh mẫu" style="max-width: 300px; max-height: 200px;">
</div>

**Phần basePath**: Đường dẫn gốc đến thư mục API của dự án

**Phần tags**: Tags là cách để bạn nhóm các endpoint API lại thành từng nhóm logic rõ ràng trong tài liệu Swagger/OpenAPI. 
Ví dụ bạn có nhiều API về upload file, chat, FAQ card — bạn tạo 3 tag tương ứng tên “Upload”, “Chat”, “FAQ Cards” để phân loại chúng.

<div style="text-align: center; border: 1px solid #ccc;">
  <img src="https://github.com/user-attachments/assets/6d095b9b-7f68-408d-bac1-2db2e0db3e5a" alt="Ảnh mẫu" style="max-width: 300px; max-height: 200px;">
</div>

**Phần Paths**: 

<div style="text-align: center; border: 1px solid #ccc;">
  <img src="https://github.com/user-attachments/assets/631ef514-9c8a-4bac-94e9-2d72deb684e3" alt="Ảnh mẫu" style="max-width: 300px; max-height: 200px;">
</div>
