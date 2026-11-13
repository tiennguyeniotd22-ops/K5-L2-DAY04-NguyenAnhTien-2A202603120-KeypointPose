# Báo cáo cá nhân — Nguyễn Anh Tiến (2A202603120)

> **Bản nháp đang hoàn thiện.** Còn thiếu ảnh chụp label person và ảnh khuôn mặt phóng to; bảng tự review và một phần thời gian cần học viên bổ sung. Ảnh JSON hiện được dựng từ ZIP đang có, cần cập nhật sau lần export cuối.

Dữ liệu bài: 12 ảnh người từ COCO val2017 và 8 ảnh khuôn mặt từ Wikimedia Commons. Annotation được thực hiện trên CVAT.

## 0. Thông tin học viên

- Họ tên: Nguyễn Anh Tiến.
- MSSV: 2A202603120.
- Email: tiennguyeniotd22@gmail.com.
- Link repository: https://github.com/tiennguyeniotd22-ops/K5-L2-DAY04-NguyenAnhTien-2A202603120-KeypointPose
- Phiên bản CVAT: 2.74.1 (đã kiểm tra API cục bộ ngày 13/11/2026).
- Máy: Windows 11 Home Single Language · bộ nhớ khả dụng 7.7 GB · CVAT chạy chế độ lite.
- Bộ ảnh trong src/exports/assignment.json: Có.
- Giờ bắt đầu: 17:00.
- Giờ kết thúc: 22:00 (khung thời gian 5 giờ; chưa tách thời gian nghỉ và từng checkpoint).

## 1. Kiểm tra label (CP0)

| Label | Kiểu | Số điểm | Tên điểm đúng bảng của lab? | Đúng thứ tự? | Số cạnh |
|---|---|---:|---|---|---:|
| person | skeleton | 17 | Có | Có | 19 |
| face | skeleton | 13 | Có | Có | 13 |

Mẫu person dựng theo người quay mặt về camera (các điểm left nằm bên phải khung mẫu): Có.

Cách đổi cờ cho một điểm: Rê chuột vào đúng điểm rồi bấm Q để bật/tắt occluded (v=1), hoặc O để bật/tắt outside (v=0); lưu thay đổi bằng Ctrl+S.

## 2. Số lượng đã gán và thời gian (CP1, CP2)

Số skeleton hiện có trong ZIP:

| Nhóm ảnh | Số ảnh được giao | Số skeleton trong ZIP hiện tại | Người dưới 60 px không gán | Poster/gương/màn hình bỏ qua | Thời gian (phút) |
|---|---:|---:|---:|---:|---:|
| easy | 5 | 5 | Chờ học viên bổ sung | Chờ học viên bổ sung | Chờ học viên bổ sung |
| occluded | 3 | 7 | Chờ học viên bổ sung | Chờ học viên bổ sung | Chờ học viên bổ sung |
| back | 2 | 4 | Chờ học viên bổ sung | Chờ học viên bổ sung | Chờ học viên bổ sung |
| small | 1 | 4 | Chờ học viên bổ sung | Chờ học viên bổ sung | Chờ học viên bổ sung |
| crowd | 1 | 3 | Chờ học viên bổ sung | Chờ học viên bổ sung | Chờ học viên bổ sung |
| faces | 8 | 8 | — | Chờ học viên bổ sung | Chờ học viên bổ sung |

Các nhóm là cách repo chia bộ 12 ảnh người: `easy` 5 ảnh, `occluded` 3, `back` 2, `small` 1 và `crowd` 1; đây không phải loại nhãn. `000000572411.jpg` thuộc `small`, `000000157271.jpg` thuộc `occluded`, `000000210604.jpg` thuộc `back`.

- Tổng số người bỏ qua: 6 — 4 người mờ/vỡ pixel nên không xác định rõ; 2 người chỉ lộ một phần đầu ở `000000572411.jpg` (ảnh thuộc nhóm `small`). Chưa xác định được trong số này có bao nhiêu người thực sự dưới 60 px và chưa phân bổ đủ theo từng nhóm.
- Số ảnh người hoàn thành ở mốc phút 105: Chưa ghi lại.
- Thời gian thực tế theo checkpoint/nhóm: Chưa ghi lại; hiện chỉ xác nhận khung 17:00–22:00.
- Ảnh khó nhất: `000000157271.jpg` (nhóm `occluded`) và `000000210604.jpg` (nhóm `back`) vì người xoay hướng, cần đổi trái/phải và khó xác định mắt, mũi, tai. `000000572411.jpg` (nhóm `small`) khó vì ảnh vỡ pixel, phải cân nhắc có đủ căn cứ gán hay không.

Ghi chú áp dụng ngưỡng: 6 người bỏ qua là tổng theo ghi nhớ của học viên, không đồng nghĩa cả 6 đều dưới 60 px. Với hai người chỉ lộ đầu ở ảnh `000000572411.jpg`, cần xác nhận kích thước người và phần bị cắt: nếu người đủ ngưỡng thì gán các điểm quan sát được, phần không thấy để `outside` (`v=0`); nếu người thực sự dưới 60 px thì không tạo skeleton.

## 3. Bảng ca khó (CP1, CP2)

Các tình huống dưới đây được đối chiếu lại theo thông tin học viên cung cấp. Cảnh báo chiều cao là độ trải của các điểm có thể nhìn thấy trong annotation; cần đối chiếu với người thật trong ảnh trước khi quyết định giữ hay bỏ.

| Ảnh | Người | Cảnh báo / điểm | Kết luận hiện tại | Ghi chú |
|---|---|---|---|---|
| 000000311300.jpg | #2 | cặp `left_ankle` / `right_ankle` bị báo ngược phía | Đã kiểm tra; trái/phải được xác nhận đúng, giữ nguyên | Không đổi cặp điểm chỉ để làm mất cảnh báo. |
| 000000572411.jpg | #1 | độ trải điểm 58 px | Nhận ra người; tạm giữ | Học viên cho rằng tư thế ngồi làm điểm trải thấp; cần đối chiếu chiều cao người nhìn thấy/cắt khung. |
| 000000572411.jpg | #2 | độ trải điểm 59 px | Nhận ra người; tạm giữ | Như trên; xác nhận lại theo kích thước người trong ảnh trước lần export cuối. |
| 000000572411.jpg | #2 | cặp wrist bị báo ngược phía | Đã kiểm tra; trái/phải được xác nhận đúng, giữ nguyên | Không đổi cặp điểm chỉ để làm mất cảnh báo. |
| 000000572411.jpg | #3 | độ trải điểm 17 px | Học viên nhận ra người; tạm giữ | Có thể do tư thế ngồi/che khuất; cần so với chiều cao người nhìn thấy trước lần export cuối. |
| 000000572411.jpg | #4 | độ trải điểm 23 px | Học viên nhận ra người; tạm giữ | Có thể do tư thế ngồi/che khuất; cần so với chiều cao người nhìn thấy trước lần export cuối. |

Hai cặp trái/phải bị cảnh báo đã được học viên kiểm tra trên ảnh và xác nhận đúng. Với cảnh báo dưới 60 px, không kết luận chỉ từ con số độ trải điểm: script đo hộp bao quanh các điểm có thể nhìn thấy; cần so với chiều cao người trong ảnh và phần bị cắt/che. Tư thế ngồi là bối cảnh cần ghi, nhưng không tự động miễn ngưỡng 60 px.

## 4. Bảng tự review (CP3)

Chọn 5 ảnh người khi review ngược từ ảnh cuối về ảnh đầu, trong đó có ít nhất 2 ảnh thuộc nhóm back hoặc crowd; chọn thêm 3 ảnh mặt. Các ảnh gợi ý bên dưới được lấy từ bộ đã giao. Học viên điền lỗi đã quan sát và tình trạng sửa, không đánh dấu ok trước khi kiểm tra trên ảnh.

| Ảnh | Người / mặt | Điểm | Mã lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|---|
| 000000413160.jpg (crowd) | Chờ kiểm | Chờ kiểm | Chờ học viên | Chờ học viên | Chờ học viên |
| 000000572411.jpg (small) | Chờ kiểm | Chờ kiểm | Chờ học viên | Chờ học viên | Chờ học viên |
| 000000311300.jpg (back) | Chờ kiểm | Chờ kiểm | Chờ học viên | Chờ học viên | Chờ học viên |
| 000000210604.jpg (back) | Chờ kiểm | Chờ kiểm | Chờ học viên | Chờ học viên | Chờ học viên |
| 000000461389.jpg (occluded) | Chờ kiểm | Chờ kiểm | Chờ học viên | Chờ học viên | Chờ học viên |
| face_483667.jpg | Chờ kiểm | Chờ kiểm | Chờ học viên | Chờ học viên | Chờ học viên |
| face_294580.jpg | Chờ kiểm | Chờ kiểm | Chờ học viên | Chờ học viên | Chờ học viên |
| face_288853.jpg | Chờ kiểm | Chờ kiểm | Chờ học viên | Chờ học viên | Chờ học viên |

Mã lỗi dùng đúng một trong: lr_swap, vis_flag, position, missing, extra, ok.

Tổng hợp số lỗi theo mã: Chờ học viên hoàn tất review 8 dòng rồi tổng hợp.

Điểm còn phân vân giữa v=1 và v=0, hai lựa chọn và lý do chọn: Chờ học viên bổ sung từ tình huống thực tế đã review.

## 5. Kiểm file xuất và kết quả tự kiểm (CP4)
Cấu trúc ZIP, số phần tử keypoints, mã v và num_keypoints đã được đối chiếu bằng script tự kiểm. Học viên cần mở từng mẫu JSON để xác nhận hoàn tất bước tự kiểm tay trước khi nộp.


| File | Người / mặt kiểm (ảnh, thứ tự) | Số phần tử keypoints | Điểm outside ra v=0, occluded ra v=1? | num_keypoints khớp? |
|---|---|---:|---|---|
| NguyenAnhTien_persons.zip | 000000043968.jpg, #1 | 51 | Có; CVAT 2.x giữ tọa độ cũ tại một số điểm v=0 | Có |
| NguyenAnhTien_persons.zip | 000000311300.jpg, #1 | 51 | Có; CVAT 2.x giữ tọa độ cũ tại một số điểm v=0 | Có |
| NguyenAnhTien_faces.zip | face_185015.jpg, #1 | 39 | Có | Có |

Sau khi xuất, CVAT ghi occluded thành v=1 và outside thành v=0. Điểm outside trong ZIP hiện tại có thể giữ tọa độ cũ; đây là cách xuất của CVAT 2.x và không phải lỗi.

Trạng thái CVAT lần xác minh trước: persons, Job #11 (12 ảnh), completed; faces, Job #12 (8 ảnh), annotation in progress. Trong lượt cập nhật này, tab Edge đang mở Job #11 ở ảnh `000000431893.jpg`; trạng thái Job #12 chưa được kiểm tra lại. Cần kiểm tra/lưu đủ 8 ảnh và hoàn tất Job #12 trên CVAT trước lần export cuối.

Kết quả tự kiểm của ZIP đang lưu (được xuất lúc 09:15 ngày 13/11/2026):

~~~text
=== srcexportsNguyenAnhTien_persons.zip (label person) ===
  [CẢNH BÁO] 000000311300.jpg #1: cặp ankle nằm ngược phía so với các cặp còn lại. Có thể đổi trái/phải một cặp (lr_swap), hoặc tay / chân bắt chéo thật: kiểm lại.
  [CẢNH BÁO] 000000572411.jpg #1: các điểm chỉ trải cao 17 px (< 60 px). Người dưới 60 px không gán; nếu người cao hơn nhưng bị cắt khung thì bỏ qua cảnh báo này.
  [CẢNH BÁO] 000000572411.jpg #2: các điểm chỉ trải cao 58 px (< 60 px). Người dưới 60 px không gán; nếu người cao hơn nhưng bị cắt khung thì bỏ qua cảnh báo này.
  [CẢNH BÁO] 000000572411.jpg #3: các điểm chỉ trải cao 17 px (< 60 px). Người dưới 60 px không gán; nếu người cao hơn nhưng bị cắt khung thì bỏ qua cảnh báo này.
  [CẢNH BÁO] 000000572411.jpg #4: các điểm chỉ trải cao 59 px (< 60 px). Người dưới 60 px không gán; nếu người cao hơn nhưng bị cắt khung thì bỏ qua cảnh báo này.
  [CẢNH BÁO] 000000572411.jpg #4: cặp wrist nằm ngược phía so với các cặp còn lại. Có thể đổi trái/phải một cặp (lr_swap), hoặc tay / chân bắt chéo thật: kiểm lại.

----- TÓM TẮT (dán vào báo cáo mục 5) -----
- File person: NguyenAnhTien_persons.zip
  Số ảnh: 12 · số skeleton person: 23 · mỗi annotation 51 số
  Skeleton theo ảnh: 000000043968=1, 000000157271=2, 000000189365=2, 000000194027=1, 000000210604=2, 000000294329=1, 000000295358=1, 000000311300=2, 000000413160=3, 000000431893=1, 000000461389=3, 000000572411=4
  Cờ v: v=2 236 (60%) · v=1 48 (12%) · v=0 107 (27%)
  num_keypoints trung bình: 12.3
- File face: NguyenAnhTien_faces.zip
  Số ảnh: 8 · số skeleton face: 8 · mỗi annotation 39 số
  Skeleton theo ảnh: face_185015=1, face_264124=1, face_288853=1, face_294580=1, face_421231=1, face_469647=1, face_483667=1, face_85624=1
  Cờ v: v=2 93 (89%) · v=1 11 (11%) · v=0 0 (0%)
  num_keypoints trung bình: 13.0
- Ghi chú: 107 điểm v = 0 vẫn mang tọa độ cũ (CVAT 2.x xuất như vậy; chuẩn COCO ghi 0, 0). Không phải lỗi: điểm v = 0 bị bỏ qua khi huấn luyện và khi chấm.
- Số [LỖI]: 0 · số [CẢNH BÁO]: 6
Kết quả: ĐẠT (đọc lại từng cảnh báo ở trên)
~~~

ZIP đang lưu trong repo được tạo lúc 09:15 ngày 13/11/2026. Sau đó học viên gửi danh sách cảnh báo mới: cặp ankle của `000000311300.jpg #2` và cặp wrist của `000000572411.jpg #2` đã được kiểm tra, xác nhận đúng; các độ trải điểm lần lượt là 58, 59, 17 và 23 px. Vì ZIP trong repo chưa được export lại trong lượt cập nhật này, cần chạy export và checker cuối để đồng bộ phần cảnh báo, số liệu tổng kết và JSON mẫu.

## 6. Ảnh chụp màn hình

Các ảnh minh chứng theo yêu cầu trong `report/individual/images/`:

1. `1_label_person.png` — Label constructor, thấy đủ 17 điểm có tên. **Còn thiếu.**
2. `2_nguoi_quay_lung.png` — Đã thêm ảnh CVAT học viên gửi, có người quay lưng/nghiêng được gán skeleton.
3. `3_mat_phong_to.png` — Khuôn mặt có đủ 13 điểm, phóng to vùng mắt. **Còn thiếu.**
4. `4_json_export.png` — Đã tạo từ annotation thật trong ZIP đang lưu, có `keypoints` và `num_keypoints`; thay/cập nhật sau lần export cuối.

Ảnh hỗ trợ khác do học viên gửi: `images/cvat_train_scene.png` (cảnh đoàn tàu) và `images/cvat_keypoint_legs.png` (cận cảnh các điểm ở chân). Ảnh khuôn mặt và label constructor vẫn cần chụp bổ sung trực tiếp trên CVAT.

Nguồn ảnh: COCO val2017 cho ảnh người; Wikimedia Commons cho ảnh khuôn mặt.

## 7. Tự đánh giá

1. Khó khăn lớn nhất là phân biệt trái/phải khi người xoay hướng, đồng thời xác định mắt, mũi, tai khi mặt khuất; áo bông và mũ cũng làm khó việc định vị khớp. Để tránh lỗi, cần xác định hướng người trước, lần theo vai–khuỷu–cổ tay và hông–gối–cổ chân; chỉ đặt điểm mặt khi vị trí có căn cứ, điểm không thể xác định thì để `outside` (`v=0`).
2. Đề xuất thêm vào guideline: với ảnh mờ/vỡ pixel hoặc người bị cắt, trước hết xác định có nhận ra được người thật và hướng cơ thể hay không; nếu không chắc đó là người thật thì không tạo skeleton. Gán các điểm nhìn thấy rõ; điểm bị che nhưng ước lượng chắc thì `v=1`; điểm không thể suy ra thì `v=0`. Với người có tư thế ngồi hoặc bị cắt, kiểm tra kích thước người nhìn thấy thay vì kết luận chỉ từ độ trải của các keypoint.
3. Trong lần tự kiểm đầu, `right_hip` của `000000189365.jpg #1` bị đặt là điểm nhìn thấy dù nằm ngoài khung. Tôi đã sửa thành `outside` (`v=0`); lần tự kiểm sau không còn lỗi tọa độ này. Nếu giữ `v=2`, mô hình sẽ bị tính loss theo tọa độ sai/ngoài ảnh; `v=0` loại điểm đó khỏi supervision.

## 8. Khó khăn và lỗi kỹ thuật

Máy dùng Windows 11 Home Single Language với khoảng 7.7 GB bộ nhớ khả dụng. Docker Desktop không nằm ở đường dẫn cài đặt mặc định; vị trí cài đặt được tìm thấy trong thư mục Programs của tài khoản người dùng. Lần khởi động lại, Docker Desktop dừng vì socket cũ của Secrets Engine không truy cập được. Socket rỗng 0 byte được đổi tên để giữ bản dự phòng; sau đó Docker Engine 29.9.2 hoạt động.

CVAT ban đầu chưa phản hồi vì container cvat_clickhouse đã bị tắt trong chế độ lite, trong khi cvat_server đang chờ dịch vụ này. Đã bật riêng cvat_clickhouse để giảm tải các dịch vụ tùy chọn khác. Lệnh python lab.py start hoàn tất thành công: CVAT 2.74.1, OPA nạp 445 quy tắc; ổ đĩa repo còn 53.5 GB. Sau khi đăng nhập CVAT, đã xác minh Job #11 của task persons ở trạng thái completed và Job #12 của task faces còn annotation in progress (8 ảnh). Lệnh python lab.py check xác nhận API CVAT sẵn sàng; giao diện annotation có lúc vẫn hiện Connecting khi mở lại job, nên cần kiểm tra giao diện trước khi kết thúc Job #12.
## 9. Tài liệu tham khảo và công cụ AI đã dùng

- Tài liệu bài lab trong repository: README.md, docs/GUIDELINE.md, CHECKPOINTS.md, docs/COCO_KEYPOINTS.md và SUBMISSION.md.
- COCO val2017 (Lin et al., 2014) cho bộ ảnh người; Wikimedia Commons cho bộ ảnh khuôn mặt.
- CVAT 2.74.1 và công cụ kiểm tra src/check_submission.py.
- ChatGPT/Codex được dùng để giải thích cảnh báo của script và biên tập báo cáo. Tọa độ annotation được học viên gán và chỉnh trực tiếp trên CVAT; trợ lý không sửa tay các file JSON xuất.

## Bonus

Chưa làm bonus (học viên xác nhận).
