# BÀI 13: XÂY DỰNG KHUNG QUẢN TRỊ AI DOANH NGHIỆP MARTX

## 1. Mục tiêu

Xây dựng Khung Quản trị AI cho MartX với quy mô 2.000 nhân viên tại 50 chi nhánh, nhằm:

- Bảo vệ dữ liệu cá nhân (PII) và bí mật kinh doanh.
- Kiểm soát chi phí sử dụng API và Token.
- Đảm bảo độ chính xác của AI và trách nhiệm kiểm duyệt của con người.

## 2. Thiết kế Khung Quản trị AI gồm 3 trụ cột

### 2.1. Trụ cột 1: Security & Data Privacy

Phân loại dữ liệu thành 3 mức:

| Mức dữ liệu | Quy định | Ví dụ |
|---|---|---|
| Đỏ - Vùng cấm | Tuyệt đối không đưa lên AI công cộng. | Mật khẩu, số CCCD, thông tin thẻ ngân hàng, dữ liệu khách hàng định danh, bí mật kinh doanh. |
| Vàng - Che mờ | Chỉ được sử dụng sau khi ẩn danh hoặc che thông tin nhạy cảm. | Họ tên khách hàng, số điện thoại, email, thông tin đơn hàng. |
| Xanh - Được phép | Được sử dụng trên nền tảng AI đã được doanh nghiệp phê duyệt. | Tài liệu công khai, kiến thức sản phẩm, nội dung quảng cáo đã công bố. |

Biện pháp kiểm soát:

- Sử dụng tài khoản AI doanh nghiệp, không dùng tài khoản cá nhân cho công việc.
- Thiết lập bộ lọc dữ liệu nhạy cảm trước khi gửi yêu cầu đến API.
- Ghi nhật ký sử dụng AI để phục vụ kiểm tra và xử lý sự cố.

### 2.2. Trụ cột 2: Token & Cost Governance

Mục tiêu: Kiểm soát chi phí API, tránh tình trạng nhân viên sử dụng AI không giới hạn.

**Hạn mức Token Quota đề xuất:**

| Nhóm nhân viên | Hạn mức/tháng |
|---|---:|
| Nhân viên thông thường | 500.000 Token |
| Trưởng nhóm | 1.500.000 Token |
| Nhân viên kỹ thuật AI | 5.000.000 Token |

Quy định:
- Mỗi nhân viên được cấp hạn mức Token riêng theo nhu cầu công việc.
- Cảnh báo khi sử dụng 80% hạn mức.
- Khi đạt 100%, hệ thống tạm dừng hoặc yêu cầu phê duyệt tăng Quota.
- Trưởng phòng phê duyệt nhu cầu sử dụng bổ sung.
- Bộ phận IT theo dõi Token và chi phí API hằng tháng.
- Định kỳ đánh giá mức sử dụng thực tế để điều chỉnh hạn mức.

**Quy trình Chat Summary bắt buộc:**

1. Nhân viên thực hiện công việc với AI.
2. Khi kết thúc phiên làm việc, yêu cầu AI tổng hợp nội dung quan trọng.
3. Lưu bản tóm tắt gồm mục tiêu, thông tin cần thiết, kết quả và công việc tiếp theo.
4. Sử dụng bản tóm tắt để tiếp tục phiên làm việc mới thay vì gửi lại toàn bộ lịch sử hội thoại.
5. Kiểm tra nội dung tóm tắt trước khi sử dụng.

### 2.3. Trụ cột 3: Accuracy & Accountability

Mục tiêu: Hạn chế thông tin sai lệch do AI tạo ra và đảm bảo con người chịu trách nhiệm cuối cùng.

**Quy chuẩn RAG Grounding bắt buộc:**

- AI phải ưu tiên tra cứu dữ liệu từ nguồn tài liệu nội bộ đã được phê duyệt.
- Câu trả lời phải có nguồn tham chiếu để nhân viên kiểm tra.
- Nếu không tìm thấy thông tin phù hợp, AI phải thông báo chưa đủ dữ liệu, không tự suy đoán.
- Nhân viên phải đối chiếu câu trả lời với tài liệu gốc trước khi sử dụng.

**Quy định Human-in-the-loop:**

| Công việc | Yêu cầu kiểm duyệt |
|---|---|
| Soạn nội dung quảng cáo | Nhân viên phụ trách kiểm tra trước khi đăng. |
| Tư vấn khách hàng | Nhân viên xác minh thông tin trước khi gửi. |
| Phân tích doanh thu | Trưởng phòng kiểm tra số liệu và kết luận. |
| Quyết định hoàn tiền, tuyển dụng hoặc xử lý khiếu nại | Bắt buộc có con người phê duyệt. |

**Chế tài và trách nhiệm:**

- Nhân viên chịu trách nhiệm kiểm tra nội dung AI trước khi sử dụng.
- Vi phạm quy định dữ liệu hoặc cố ý sử dụng AI sai mục đích sẽ bị xử lý theo nội quy doanh nghiệp.
- Bộ phận IT có trách nhiệm ghi nhận, điều tra và báo cáo sự cố AI.


## 3. AI Readiness Scorecard

Đánh giá mức độ sẵn sàng sử dụng AI của phòng ban trước khi cấp quyền API.

**Thang điểm:** 0 = Chưa đạt, 1 = Đạt một phần, 2 = Đạt đầy đủ.

| STT | Tiêu chí | Yêu cầu |
|---|---|---|
| 1 | Data Security | Biết phân loại và bảo vệ dữ liệu. |
| 2 | Cost Management | Có kế hoạch quản lý Token và chi phí. |
| 3 | AI Literacy | Nhân viên được đào tạo sử dụng AI an toàn. |
| 4 | Data Quality | Có tài liệu đáng tin cậy cho AI tra cứu. |
| 5 | Human Accountability | Có người kiểm tra và chịu trách nhiệm. |

**Điều kiện cấp quyền API:**

| Điểm | Kết quả |
|---|---|
| 9-10 | Được cấp API theo hạn mức. |
| 6-8 | Cấp thử nghiệm có giám sát. |
| 0-5 | Chưa được cấp API. |

