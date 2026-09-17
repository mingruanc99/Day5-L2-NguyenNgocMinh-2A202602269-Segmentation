# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên VLearn. Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Tên học viên: NGUYỄN NGỌC MINH
- Mã học viên theo lớp: 2A202602269
- Ngày / CVAT local: 17/09/2026 / CVAT local (http://localhost:8080)
- Công cụ đã dùng: Brush, Polygon

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh VLearn đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip | 3 / 3 | 20 |
| medium_instance | medium_instance.zip | 3 / 3 | 32 |
| hard_panoptic | hard_panoptic.zip | 2 / 2 | 30 |
| cp1_holes | cp1_holes.zip | 1 / 1 | 3 |
| cp2_slice | cp2_slice.zip | 1 / 1 | 3 |
| cp5_occlusion | cp5_occlusion.zip | 1 / 1 | 3 |
| cp3_thin | cp3_thin.zip | 1 / 1 | 3 |
| cp4_curb | cp4_curb.zip | 1 / 1 | 3 |
| cp6_coverage | cp6_coverage.zip | 1 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Ghi chú tình trạng các task:
- Cả 9 task đều đã hoàn thành đủ 100% số ảnh (14/14 ảnh) và được kiểm tra cấu trúc hợp lệ (0 lỗi).
- `cp5_occlusion`: Đã vẽ đầy đủ 24 annotations (ô tô, xe máy, xe tải, xe buýt, người) xử lý các trường hợp vật bị che khuất thành các phần rời nhau nhưng vẫn là 1 instance.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: Ảnh `000000181542.jpg`, chiếc xe ô tô (`car`) màu trắng ở phía trước, nằm gần mép phải nửa dưới khung hình.
- Class và quy tắc tôi dùng để chọn biên: Class `car`. Tôi dùng Polygon vẽ bám sát đường bao thực tế của thân xe (viền kính, bánh xe chạm đất, vỏ xe). Dừng đường biên tại điểm tiếp xúc với mặt đường và phần bị khuất bởi mép ảnh bên phải; không vẽ tràn ra vùng bóng đổ dưới gầm xe trên mặt đường.
- Nếu dùng gợi ý sau đó: vùng gợi ý sai/đúng, hành động sửa/giữ và lý do: Khi thử dùng gợi ý tự động cho các xe phía xa, công cụ thường bị lẹm ăn vào bóng râm mặt đường và gộp hai xe liền nhau thành một mask. Tôi đã dùng Eraser để gọt bỏ phần bóng đổ và tách thành từng instance độc lập.
- Nếu không dùng gợi ý: không dùng; em chủ động vẽ thủ công toàn bộ để kiểm soát chính xác ranh giới.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: Task `easy_semantic`, ảnh `81ae7cbb-6bc63a4a.jpg`, khu vực ranh giới giữa vỉa hè (`sidewalk`) và lòng đường (`road`).
- Lỗi thuộc loại: sai lớp / biên: Ban đầu dùng cọ vẽ nhanh đã tô nhầm một phần mặt đường nhựa màu xám sáng vào lớp `sidewalk`.
- Bằng chứng tôi nhìn thấy: Quan sát kỹ thấy gờ bó vỉa (curb) nổi cao ngăn cách rõ ràng làn xe chạy và lối đi bộ; mép đường có vạch kẻ sơn phân định chức năng giao thông.
- Quy tắc và hành động sửa: Áp dụng quy tắc phân loại ranh giới theo chức năng và gờ bó vỉa thay vì cảm quan màu sắc. Dùng Brush chuyển lại vùng nhầm sang `road` và căn chỉnh đường biên bám sát mép gờ bó vỉa.
- Sau sửa đã Save và export lại chưa? Đã bấm Save trên CVAT và export lại file `easy_semantic.zip`.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): Kết quả tự đánh giá với bộ ground truth ba tier (scorecard.py): Easy mIoU 0.662 (11.6/20), Medium metric 0.556 (11.1/32, mean matched IoU 0.774), Hard PQ 0.384 (12.3/30); tổng ba tier đạt 35.0/82 điểm. Lớp road đạt IoU rất cao (0.981). Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 1. `easy_semantic` (ảnh `7ee6d192-89e2408b.jpg`): Vùng cây bụi thấp mọc sát chân tường tòa nhà bên lề | Cân nhắc giữa `vegetation` (thực vật) hay gộp vào `building` (khuôn viên kiến trúc) | Nhìn rõ hình thái tán lá và sắc xanh tự nhiên của bụi cây, phân tách khỏi kết cấu tường bê tông | Quyết định gán riêng thành `vegetation` theo nguyên tắc phân loại pixel nhìn thấy. |
| 2. `cp1_holes` (ảnh `000000144300.jpg`): Phần kính cửa sổ trong suốt của xe ô tô nhìn xuyên thấu cảnh vật phía sau | Khoét lỗ phần kính xe (coi như background) hay giữ nguyên trọn vẹn trong mask `car` | Quy tắc đặc thù của trạm `cp1_holes`: cửa sổ, kính và khe hở xe nằm trọn trong mask, không được khoét bỏ | Quyết định bao phủ toàn bộ vùng kính xe trong mask `car` theo đúng quy định. |
| 3. `cp4_curb` (ảnh `7d83710e-4697c3b2.jpg`): Đoạn dốc hạ vỉa hè để xe lên xuống bằng phẳng với mặt đường | Cân nhắc gán là `road` (vì cùng cao độ mặt đường) hay `sidewalk` (thuộc hành lang đi bộ) | Dù không có gờ cao nhưng vị trí thuộc hành lang vỉa hè dành cho người đi bộ/dẫn vào nhà dân | Quyết định gán là `sidewalk` theo chức năng quy hoạch không gian; mong coach xác nhận thêm quy ước cho vị trí này. |
