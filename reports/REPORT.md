# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

- Mã học viên theo lớp: 2A202602074
- Ngày: 17/09/2026/ CVAT local
- Công cụ đã dùng: Brush, Polygon, kiểm cấu trúc bằng notebook Colab

## 1. Bài đã nộp

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

Notebook Colab kiểm trước khi nộp báo tất cả 9 task đều OK; lỗi hợp đồng: 0; task chưa có ZIP: 0; ZIP tên lạ: [].

## 2. Một quyết định trước khi dùng gợi ý

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: `000000181542.jpg`, vùng nửa dưới ảnh, một người/xe ở khu vực giao thông đông.
- Class và quy tắc tôi dùng để chọn biên: tôi chọn đúng class theo vật nhìn thấy được; phần nào bị che thì chỉ vẽ phần còn lộ ra, không đoán phần bị khuất phía sau vật khác.
- Nếu dùng gợi ý sau đó: không dùng; tôi tự kiểm lại từng instance để tránh gộp các vật cùng lớp đứng sát nhau.
- Nếu không dùng gợi ý: không dùng; quyết định gán nhãn chính là tách từng vật đếm được thành mask riêng, còn nền/stuff không đưa vào task instance.

## 3. Một lỗi tôi tìm thấy và sửa

- Task/ảnh/vùng: `cp2_slice`, ảnh `000000017627.jpg`, hai xe cùng lớp nằm sát nhau.
- Lỗi thuộc loại: gộp-tách.
- Bằng chứng tôi nhìn thấy: có khe/ranh giữa hai xe, nên đây là hai vật riêng chứ không phải một object liền mạch.
- Quy tắc và hành động sửa: theo quy tắc Slice, hai xe cùng class nhưng là hai vật vật lý khác nhau phải tách thành hai instance; tôi tách mask, kiểm lại biên, Save rồi export lại.
- Sau sửa đã Save và export lại chưa? Đã Save và export lại `cp2_slice.zip`.

Kết quả tự kiểm liên quan: notebook Colab báo `cp2_slice · OK`, số annotation: 11, kiểu mask: `{'RLE': 11}`. Tổng kiểm trước khi nộp: 0 lỗi hợp đồng, 0 task thiếu ZIP.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| `cp1_holes` / `000000144300.jpg`, các lỗ/khoảng kính trong vật | Khoét lỗ khỏi mask hoặc giữ trong mask | Quy tắc task ghi holes/windows/gaps vẫn nằm trong mask | Tôi giữ các lỗ/khoảng kính trong mask, không tự khoét rỗng. |
| `cp5_occlusion` / `000000336232.jpg`, vật bị che tách thành hai phần nhìn thấy | Tách thành hai instance hoặc giữ một instance | Một object bị che bởi vật khác vẫn là một object nếu cùng vật lý | Tôi giữ là một instance cho cùng vật, chỉ vẽ phần nhìn thấy. |
| `cp4_curb` / `7d83710e-4697c3b2.jpg`, ranh road-sidewalk ở mép bó vỉa | Gán theo màu mặt đường hoặc theo chức năng vùng | Quy tắc task yêu cầu road vs sidewalk theo ranh chức năng, dù màu asphalt giống nhau | Tôi chọn sidewalk cho phần vỉa/hè và road cho phần lòng đường; xin coach xác nhận nếu đoạn ranh quá mờ. |
