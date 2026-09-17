# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên VLearn. Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202602243
- Ngày / CVAT local: 17-09-2026
- Công cụ đã dùng: CVAT

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh VLearn đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task            | File ZIP đúng tên   | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --------------- | ------------------- | -----------------: | ---------------------------: |
| easy_semantic   | easy_semantic.zip   |              3 / 3 |                           20 |
| medium_instance | medium_instance.zip |              3 / 3 |                           32 |
| hard_panoptic   | hard_panoptic.zip   |              2 / 2 |                           30 |
| cp1_holes       | cp1_holes.zip       |              1 / 1 |                            3 |
| cp2_slice       | cp2_slice           |              1 / 1 |                            3 |
| cp5_occlusion   | cp5_occlusion.zip   |              1 / 1 |                            3 |
| cp3_thin        | cp3_thin.zip        |              1 / 1 |                            3 |
| cp4_curb        | cp4_curb.zip        |              1 / 1 |                            3 |
| cp6_coverage    | cp6_coverage.zip    |              1 / 1 |                            3 |
| **Tổng tối đa** |                     |                    |                      **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

## 2. Một quyết định trước khi dùng gợi ý

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: Ảnh 000000181542.jpg, người điều khiển xe máy (đội mũ bảo hiểm) ở nửa bên trái bức ảnh, vị trí ngay phía sau người phụ nữ mặc áo dài đang đi bộ sang đường.
- Class và quy tắc tôi dùng để chọn biên: Class `person`. Áp dụng quy tắc che khuất: chỉ vẽ các pixel phần cơ thể thực sự nhìn thấy được (đầu, lưng, cánh tay và chân lộ ra ngoài), dừng nét vẽ ngay sát mép tà áo dài của người đi bộ che phía trước; không vẽ nối xuyên qua phần bị che khuất và tách riêng biệt hoàn toàn với đối tượng xe máy (`motorcycle`).
- Không dùng công cụ gợi ý.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: hard_panoptic, ảnh 000000460147.jpg
- Lỗi thuộc loại: chồng lấn / phủ vùng
- Bằng chứng tôi nhìn thấy: Khi kiểm tra lại trên CVAT và chạy kiểm thử tự động, vùng mask nền lòng đường (`road`) được vẽ thành một đa giác lớn bao trùm toàn bộ mặt đường, đè xuyên qua các mask đối tượng xe cộ (`car`, `truck`) đang chạy bên trên. Đồng thời, toàn bộ khu vực nhà mặt phố cao tầng bên phải và trạm xăng bên trái bị bỏ trống, chưa được gán nhãn `building`.
- Quy tắc và hành động sửa: Áp dụng quy tắc Panoptic Segmentation (mỗi pixel chỉ thuộc về đúng một mask duy nhất, không có hiện tượng pixel vừa là road vừa là car). Tôi dùng Brush và Polygon khoét rỗng (trừ vùng) của lớp `road` tại vị trí các phương tiện giao thông đè lên; đồng thời bổ sung phủ kín nhãn `building` cho các khối nhà hai bên đường để giải quyết cảnh báo thiếu độ phủ vùng (coverage).
- Sau sửa đã Save và export lại chưa? Đã Save, đã export lại

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): … / chưa có điểm. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí                                                                      | Hai cách hiểu có thể                                                                                                                                                  | Quy tắc/chứng cứ                                                                                                                           | Quyết định hoặc câu hỏi cho coach                                                                                                                         |
| :------------------------------------------------------------------------------ | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1. Ảnh 000000460147.jpg**<br>_(Xe chở xe chuyên dụng ở làn giữa)_             | **Cách 1:** Vẽ gộp toàn bộ thành 1 instance `truck`.<br>**Cách 2:** Tách riêng xe tải chuyên dụng (`truck`) và từng chiếc ô tô con (`car`) đang được chở trên sàn xe. | Quy tắc Instance/Thing yêu cầu đếm từng cá thể độc lập. Các xe con trên giá tuy không tự lăn bánh nhưng vẫn có ranh giới thị giác rõ ràng. | **Quyết định:** Gán sàn và đầu kéo xe là 1 instance `truck`; vẽ riêng từng mask `car` cho 4 xe con trên thùng chở để tránh lỗi gộp vật thể.               |
| **2. Ảnh 000000350023.jpg**<br>_(Cần cẩu/cột tháp công trình in trên nền trời)_ | **Cách 1:** Tô `sky` phủ trùm qua vì các thanh kim loại quá mảnh.<br>**Cách 2:** Phải chừa/khoét lỗ các thanh giàn giáo, gán nhãn công trình/vật cản.                 | Ranh giới giữa vùng nền (`sky`) và nét mảnh kiến trúc. Nếu tô tràn sky qua thân cần cẩu sẽ vi phạm ranh giới biên vật thể nhìn thấy.       | **Quyết định:** Chừa/khoét lỗ các thanh giàn giáo, gán nhãn công trình/vật cản.                                                                           |
| **3. Ảnh 000000350023.jpg**<br>_(Đoạn dải phân cách và bồn cây ở giữa đường)_   | **Cách 1:** Gộp chung vào lớp nền lòng đường `road`.<br>**Cách 2:** Phải tách riêng thành `vegetation` (cho cây) và `sidewalk` / curb cho phần bê tông dải phân cách. | Quan sát kết cấu chức năng: khu vực này có bó vỉa gờ cao và trồng cây xanh, xe cộ không lưu thông được.                                    | **Quyết định:** Tách dải đất trồng cây ở giữa thành nhãn riêng (`vegetation`), khoét khỏi diện tích mặt đường `road` để đảm bảo tính phân tách chức năng. |
