# Status Codes

Mỗi thông báo phản hồi HTTP phải chứa mã trạng thái trong dòng đầu tiên, cho biết kết quả của yêu cầu. Các mã trạng thái được chia thành năm nhóm, theo chữ số đầu tiên của mã:
- 1xx (Informational – Thông tin): Các status code loại này dùng để đơn giản thông báo với client rằng server đã nhận được request. Các status code này ít được sử dụng.
- 2xx (Sucess – Thành công): Các status code loại này có ý nghĩa rằng request được server và xử lý thành công.
- 3xx (Redirect – Chuyển hướng): Các status code loại này có ý nghĩa rằng server sẽ chuyển tiếp request hiện tại sang một request khác và client cần thực hiện việc gửi request tiếp theo đó để có thể hoàn tất. Thông thường khi trình duyệt nhận được status code loại này nó sẽ tự động thực hiện việc gửi request tiếp theo để lấy về kết quả.
- 4xx (Client error – Lỗi Client): Các status code loại này có ý nghĩa rằng đã có lỗi từ phía client trong khi gửi request. Ví dụ như sai URL, sai HTTP method, không có quyền truy cập vào trang…
- 5xx (Server error – Lỗi Server): Các status code loại này có ý nghĩa rằng đã có lỗi từ phía server trong khi xử lý request. Ví dụ như server quá tải, hết bộ nhớ, lỗi kết nối database…

Có rất nhiều mã trạng thái cụ thể, nhiều mã chỉ được sử dụng trong các trường hợp đặc biệt. Dưới đây là các mã trạng thái mà bạn có nhiều khả năng gặp phải nhất khi tấn công một ứng dụng web, cùng với cụm từ lý do thông thường liên quan đến chúng:
#### 1xx (Informational – Thông tin)

- `100 Continue`: Chỉ một phần của Request được nhận bởi Server (có thể là header và Client cần gửi tiếp body), nhưng miễn là nó không bị loại bỏ, Client nên tiếp tục với Request.
- `101 Switching Protocols`: Server thay đổi protocol.

#### 2xx (Sucess – Thành công)

- `200 OK`: Request đã được tiếp nhận và xử lý thành công.
- `201 Created`: Request đã được tiếp nhận và xử lý thành công và 1 tài nguyên mới được tạo trên server.
- `202 Accepted`: Request được chấp nhận xử lý nhưng việc Xử lý không hoàn thành.
- `204 No content`: Request được xử lý thành công nhưng server không trả về dữ liệu nào.
- `206 Partial Content`: Server chỉ trả về một phần dữ liệu.

#### 3xx (Redirect – Chuyển hướng)

- `300 Multiple Choices`: Một danh sách các link. Người sử dụng có thể chọn một link và tới vị trí đó. Có tối đa 5 địa chỉ. Ví dụ: List các file video với format khác nhau.
- `301 Moved Permanently`: Request hiện tại và các request sau được yêu cầu di chuyển tới một URI mới.
- `302 Found`: Trang được yêu cầu đã được di chuyển tới vị trí mới.
- `303 See Other`: Trang được yêu cầu cũng có thể được trả về ở một URL khác bằng cách sử dụng phương thức GET.
- `304 Not Modified`: hướng dẫn trình duyệt sử dụng bản sao được lưu trong bộ nhớ cache của tài nguyên được yêu cầu. Máy chủ sử dụng các tiêu đề yêu cầu `If-Modified-Since` và `If-None-Match` để xác định xem máy khách có phiên bản mới nhất của tài nguyên hay không.

#### 4xx: (Client Error – Lỗi Client)

- `400 Bad Request`: Server không thể xử lý hoặc sẽ không xử lý các Request lỗi của phía client (ví dụ Request có cú pháp sai).
- `401 Unauthorized`: Cần username, password để truy cập.
- `403 Forbidden`: Truy cập bị từ chối (ví dụ ip bị chặn)
- `404 Not Found`: Trang được yêu cầu không tồn tại tại thời điểm hiện tại, tuy nhiên có thể tồn tại trong tương lai.
- `405 Method Not Allowed`: Trang được yêu cầu không hỗ trợ method của request (ví dụ chỉ xử lý method POST, không xử lý method GET).
- `406 Not Acceptable`: Server chỉ có thể tạo một Response mà không được chấp nhận bởi Client.
- `407 Proxy Authentication Required`: Bạn phải xác nhận với một proxy server trước khi request này được phục vụ.
- `408 Request Timeout`: Request tốn thời gian dài hơn thời gian Server được chuẩn bị để đợi.
- `409 Conflict`: Request không thể được hoàn thành bởi vì sự xung đột.
- `410 Gone`: Giống 404 nhưng tài nguyên/trang cũng không tồn tại trong tương lai.
- `411 Length Required`: Chưa định nghĩa trường `Content-Length` trong header của request gửi đi.
- `412 Precondition Failed`: Server sẽ không đáp ứng một trong những điều kiện tiên quyết của Client trong Request.
- `413 Payload Too Large`: Server sẽ không chấp nhận yêu cầu, bởi vì đối tượng yêu cầu là quá rộng.
- `414 URI Too Long`: URI được cung cấp là quá dài để Server xử lý.
- `415 Unsupported Media Type`: Server sẽ không chấp nhận Request, bởi vì kiểu phương tiện không được hỗ trợ.
- `416 Range Not Satisfiable`: Client yêu cầu một phần dữ liệu nhưng không có sẵn trên server.

#### 5xx (Server error – Lỗi server)

- `500 Internal Server Error`: Một thông báo chung chung, được đưa ra khi Server bị lỗi bất ngờ (chủ yếu do lỗi lập trình, kết nối database).
- `501 Not Implemented`: Server không hỗ trợ xử lý request này.
- `502 Bad Gateway`: Server đã hoạt động như một gateway hoặc proxy và nhận được một Response không hợp lệ từ máy chủ nguồn.
- `503 Service Unavailable`: Server hiện tại không có sẵn (Quá tải hoặc được down để bảo trì). Nói chung đây chỉ là trạng thái tạm thời.
- `504 Gateway Timeout`: Server đã hoạt động như một gateway hoặc proxy và không nhận được một Response từ máy chủ nguồn.
- `505 HTTP Version Not Supported`: Server không hỗ trợ phiên bản “giao thức HTTP”.