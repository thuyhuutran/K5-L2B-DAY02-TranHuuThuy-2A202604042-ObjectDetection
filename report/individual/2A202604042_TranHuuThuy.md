# Báo cáo cá nhân — Ngày 2 Object Detection

## 1. Thông tin học viên

- Họ tên: Trần Hữu Thủy.
- MSSV: 2A202604042.
- Email: huuthuytrann3004@gmail.com.
- Lớp: L2B.
- Link repo bài làm: .
- Link Colab đã chạy: .

## 2. Schema và mini guideline

Schema trong [data.yaml](../../data.yaml): `car=0`, `truck=1`, `bus=2`, `van=3`. Mỗi xe hợp lệ có một box riêng ôm sát phần nhìn thấy, không vượt biên ảnh; không gán người, xe máy hoặc xe đạp.

[Mini guideline](../../GUIDELINE_MINI.md) hiện ghi ba ca sau. Nội dung này được tổng hợp từ file, chưa được kiểm tra lại trên ảnh trong lần lập báo cáo này.

| Ảnh | Tình huống đã ghi | Quyết định đã ghi |
|---|---|---|
| `drive_012` | Xe khách màu kem khó phân biệt bus/van | Chọn bus dựa trên thân dài và nhiều cửa sổ. |
| `drive_027` | Cụm xe nhỏ, xa, chồng lên nhau ở góc trên trái | Gán car khi nhận diện được, box ôm phần nhìn thấy. |
| `drive_036` | Xe bạc bị nhòe, khó phân biệt car/van | Chọn car theo hình dáng mui và đầu xe đã mô tả. |

Cần hỏi giảng viên về quy tắc “còn thấy khoảng 30%” và “phân vân car/van thì chọn car” đang ghi trong mini guideline. GUIDE yêu cầu ghi lại ca mơ hồ và hỏi giảng viên, không tự đoán lớp. Chưa có xác nhận các quy tắc này đã được giảng viên chấp thuận.

## 3. Annotation và self-QC

- Số file nhãn train: **50**, trong `dataset/labels/train/`.
- Kết quả chạy `python tools/check_yolo_labels.py` ngày 10/11/2026: **ĐẠT cấu trúc: 50/50 file nhãn hợp lệ**.
- Lỗi cấu trúc còn được checker báo: Không có trong lần chạy này. Chưa có nhật ký lỗi đã xử lý trước đó.
- Danh sách ít nhất 10 ảnh đã rà bằng mắt: **Chưa được học viên cung cấp; cần bổ sung**.
- Lỗi bỏ sót/box/class phát hiện khi rà và cách sửa: Chưa có nhật ký được xác nhận.
- Commit khóa nhãn ban đầu: Chưa cung cấp mã hoặc link commit.

Checker xác nhận định dạng; chưa chứng minh đủ vật thể, đúng lớp hoặc box sát.

## 4. Gold QC và rework

Kết quả tại [annotation_evaluation.json](../../outputs/annotation_evaluation.json). Lần kiểm tra lại ngày 10/11/2026 lưu riêng tại [annotation_evaluation_current.json](../../outputs/annotation_evaluation_current.json), cho kết quả giống file trên.

Chưa có cặp phiên bản nhãn và nhật ký đủ để xác định kết quả trước/sau một vòng sửa. Bảng ghi bộ nhãn hiện tại, không coi việc chạy lại là hoàn thành rework.

| Chỉ số | Bộ nhãn hiện tại | Sau sửa đã xác nhận |
|---|---:|---|
| TP | 449 | Chưa có |
| FP | 467 | Chưa có |
| FN | 204 | Chưa có |
| Precision | 0,4902 | Chưa có |
| Recall | 0,6876 | Chưa có |
| F1 | 0,5723 | Chưa có |
| mean_iou_of_matches | 0,8538 | Chưa có |
| passed | false | Chưa có |

Evaluator ghép box cùng lớp tại IoU ≥ 0,50. Điều kiện chuyển sang train là F1 ≥ 0,80 và mean IoU ≥ 0,70. Bộ nhãn hiện tại **chưa đạt do F1 dưới ngưỡng**; mean IoU của các box đã ghép đạt ngưỡng.

Một số ảnh cần ưu tiên rà từ thống kê evaluator:

| Ảnh | Box học viên | Box gold | Matches | FP | FN |
|---|---:|---:|---:|---:|---:|
| `drive_005` | 7 | 24 | 6 | 1 | 18 |
| `drive_012` | 39 | 23 | 18 | 21 | 5 |
| `drive_041` | 21 | 24 | 10 | 11 | 14 |
| `drive_050` | 36 | 18 | 16 | 20 | 2 |

Đây là danh sách cần rà, chưa phải ảnh đã sửa. FP/FN không tự xác định nguyên nhân: cần mở ảnh để phân biệt box thừa, bỏ sót, sai lớp hoặc box lệch. Chưa có quyết định sửa/giữ từng box được học viên xác nhận. Sau khi tự kiểm tra và sửa, cần ghi ảnh, thay đổi, lý do và chạy lại evaluator; giữ nguyên gold labels.

## 5. Kết quả YOLO

- Runtime, GPU/CPU, phiên bản Ultralytics và Torch: Chưa có thông tin phiên chạy.
- Các tham số thay đổi so với notebook và lý do: Chưa có thông tin được xác nhận.
- Đường dẫn best checkpoint: Chưa tìm thấy trong thư mục bài làm.
- Trạng thái: Chưa có bằng chứng hoàn thành train/eval; annotation hiện chưa đạt điều kiện chuyển sang train.

| Chỉ số trên 10 ảnh eval | Giá trị |
|---|---|
| Precision | Chưa có kết quả |
| Recall | Chưa có kết quả |
| mAP50 | Chưa có kết quả |
| mAP50–95 | Chưa có kết quả |

Chưa tìm thấy `assets/eval_predictions/` và `assets/yolo26_runs/` cạnh báo cáo. Cần bổ sung sau phiên chạy Colab, kèm nhận xét của học viên về ít nhất một ảnh và vật thể cụ thể.

Bốn câu hỏi cuối notebook:

1. **Lớp nào recall thấp nhất? Ảnh nào minh họa?** Chưa có metrics theo lớp hoặc ảnh prediction để xác định. Cần bổ sung sau khi chạy eval.
2. **Nếu mAP50 cao nhưng mAP50–95 thấp, cần kiểm điều gì trên box?** Cần kiểm vị trí và kích thước box ở các ngưỡng IoU cao hơn: cạnh box có lệch, lấy thừa nền hoặc cắt mất phần xe nhìn thấy hay không. Đây là giải thích khái niệm, chưa phải kết luận về model của bài làm.
3. **Lỗi class nào có thể liên quan guideline? Dữ kiện nào hỗ trợ?** Chưa có confusion matrix và kiểm tra ảnh để kết luận lỗi class thực tế. Mini guideline có các ca car/van và bus/van cần đối chiếu; học viên cần tự kiểm prediction và bổ sung bằng chứng trước khi nhận xét.
4. **Vì sao không dùng 10 ảnh eval để train? Vai trò validation là gì?** Theo GUIDE và `data.yaml`, 10 ảnh eval được giữ làm validation để đánh giá trong quá trình train và chọn best checkpoint. Đưa chúng vào train sẽ làm mất sự tách biệt với dữ liệu huấn luyện. Vì tập này cũng tham gia chọn checkpoint, đây không phải test set độc lập.

## 6. Khó khăn và cách xử lý

| Bước/thời điểm | Lỗi quan sát | Cách đã thử | Kết quả/còn thiếu |
|---|---|---|---|
| Self-QC, 10/11/2026 | Cần xác nhận cấu trúc nhãn | Chạy checker | 50/50 file hợp lệ; còn thiếu danh sách rà bằng mắt. |
| Gold QC, 10/11/2026 | Evaluator báo CHƯA ĐẠT | Chạy lại với nhãn hiện tại | F1 = 0,5723; mean IoU = 0,8538; chưa đạt gate. |
| Rework | Chưa biết thao tác sửa theo FN/FP | Hỏi Codex cách mở CVAT, kiểm tra lớp, thêm/xóa và chỉnh box | Đã có hướng dẫn; chưa xác nhận hoàn thành sửa trên ảnh. |
| Pipeline YOLO | Chưa có kết quả trong thư mục bài làm | Chưa có phiên chạy được xác nhận | Cần hoàn thành QC rồi bổ sung Colab, metrics, checkpoint và ảnh eval. |

## 7. Tự đánh giá theo rubric

Đối chiếu [RUBRIC.md](../../RUBRIC.md):

- **Định dạng YOLO:** Có 50 file nhãn train, checker đạt.
- **Đầy đủ vật thể, hình học box và phân lớp:** Chưa xác nhận hoàn thành; evaluator còn FP/FN và chưa có nhật ký rà ảnh. Mean IoU cao chỉ mô tả các box đã ghép.
- **Mini guideline:** Có bốn lớp và ba ca mơ hồ; cần xác nhận quy tắc xử lý ca khó với giảng viên.
- **Gold-set QC:** Có đánh giá nhưng F1 chưa đạt; còn thiếu vòng rework được ghi chép rõ.
- **Pipeline YOLO và phân tích:** Chưa có bằng chứng kết quả train/eval trong thư mục hiện tại.
- **Thông tin nộp bài:** Còn thiếu email, lớp, link repo, link Colab và commit khóa nhãn.

Chưa tự chấm điểm hoặc nhận hoàn thành phần chưa có bằng chứng.

## 8. Công cụ AI và tài liệu tham khảo

Đã sử dụng ChatGPT/Codex để giải thích FN/FP, IoU, hướng dẫn thao tác sửa nhãn trong CVAT, chạy checker/evaluator và hỗ trợ điền báo cáo từ các file có sẵn. AI hỗ trợ tổng hợp số liệu và giải thích khái niệm; chưa thực hiện sửa nhãn thay học viên trong lần lập báo cáo này.

Phần học viên đã tự kiểm tra: Chưa được xác nhận trong cuộc trao đổi; cần bổ sung các ảnh đã rà, thao tác sửa và nhận xét thực tế trước khi nộp. Đây là bản dự thảo có AI hỗ trợ, cần học viên đọc lại và chịu trách nhiệm về nội dung theo [RULES.md](../../RULES.md).

Tài liệu sử dụng: [GUIDE.md](../../GUIDE.md), [CHECKPOINTS.md](../../CHECKPOINTS.md), [RUBRIC.md](../../RUBRIC.md), [SUBMISSION.md](../../SUBMISSION.md), [GUIDELINE_MINI.md](../../GUIDELINE_MINI.md), [checker](../../tools/check_yolo_labels.py) và [evaluator](../../tools/evaluate_annotations.py). Chưa có nguồn ngoài repo được cung cấp.
