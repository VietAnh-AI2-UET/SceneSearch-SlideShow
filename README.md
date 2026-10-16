# SceneSearch slide deck

## Mở và trình chiếu

- Mở `index.html` bằng Chrome, Edge hoặc trình duyệt hiện đại. Không cần build, server hay Internet.
- Giữ `index.html` và thư mục `assets/` cạnh nhau khi sao chép.
- 10 slide, canvas 1920×1080, tổng thời lượng gợi ý 430 giây. Lời dẫn, chuyển ý và nguồn nằm trong `speaker-notes.md`.
- ← / →, Space, Page Up / Page Down: chuyển slide. Home / End: đầu / cuối. F hoặc nút Toàn màn hình: fullscreen. Có nút điều hướng, vuốt và cuộn chuột.
- `#1` đến `#10` ở cuối đường dẫn mở slide tương ứng. Screenshot trong slide là ảnh tĩnh.

## Chỉnh nội dung và benchmark

- Slide 9 có các ô `td.benchmark-value`, với `data-field` mô tả trường cần điền. Giá trị ban đầu hoàn toàn trống.
- Nhấn **Sửa** hoặc E để sửa chữ và điền ô benchmark. Nhấn Esc để thoát. Chọn **Lưu HTML**, hoặc Ctrl+S khi đang sửa, để tải bản HTML đã sửa; thay bản `index.html` bằng bản tải về và giữ nguyên `assets/`.
- Chỉnh sửa không tự ghi xuống file hoặc lưu qua lần đóng trang; phải dùng Lưu HTML. Trình duyệt tự chọn vị trí tải về.
- Có thể sửa HTML trực tiếp. Màu nằm trong `:root`, bố cục ở CSS có chú thích từng phần. Dùng font hệ thống để giữ khả năng chạy offline.

## Thông tin còn thiếu

- CPU model, cores/threads, RAM; metric, k, tập đánh giá và giá trị retrieval; thời lượng video, số clip, thời gian indexing; kích thước index, top-k và thời gian query.
- Cần ghi điều kiện đo: encoder hay toàn pipeline, device thực chạy, cache warm/cold, mode, số lần chạy, thống kê và phạm vi đo thời gian.
- Chưa xác minh chất lượng query tiếng Việt. UI nhận văn bản trực tiếp; ảnh thật dùng English. Câu “xe máy tạt đầu” diễn tả nhu cầu, không phải kết quả demo đã đo.
- Không có mâu thuẫn chính giữa kiến trúc và phần code đã kiểm tra. Bổ sung JSON cho danh sách đã lưu theo code hiện tại. Lựa chọn và lịch sử chỉ giữ trong session, không tự retrain model.

## Nguồn và hình ảnh

- Nội dung dựa vào `../dumb-scribings/presentation.md`, `../ARCHITECTURE.md` và các đoạn code liên quan được ghi theo từng slide trong notes.
- Đã xem cả 5 ảnh nguồn. Bản sao nguyên vẹn nằm trong `assets/`; ảnh upload được giữ để tham khảo. Deck dùng các ảnh query, results, privacy và metadata.
- Crop bằng CSS để tập trung vào vùng cần nhìn; không sửa giá trị hay dựng UI giả. Số trong ảnh là sample, không phải benchmark.
- Sơ đồ HTML/SVG là bản rút gọn để trình bày. Media privacy tách với nhánh inference. SQLite giữ records/trạng thái; vectors và media trên filesystem.

## Kiểm tra

- Đã mở HTML bằng Chrome headless, render từng slide tại 1280×720 và xem ảnh để chỉnh bố cục.
- Kiểm tra 10 slide, tất cả ảnh tải thành công, không có tài nguyên HTTP/CDN, không có lỗi JavaScript trong lần kiểm tra.
- Home, ArrowRight, End lần lượt cho bộ đếm 1/9, 2/9, 9/9.
- Viewport điện thoại 390×844: stage 390×219,375, đúng 16:9, không cuộn ngang. Nội dung giữ nguyên bố cục, có khoảng trống theo chiều dọc.
- Reduced motion vẫn hiện nội dung. Sau chỉnh bố cục, cả 10 slide có scrollWidth 1920 và scrollHeight 1080.
- Xác nhận toàn bộ ô benchmark rỗng. Tổng thời lượng notes 20+75+40+45+40+40+55+55+50 = 430 giây.
- Phép tính giả định: 1.026 giờ công, 128,25 ngày công với 8h/ngày, khâu duyệt 93,567%.
- Chưa chạy sản phẩm, chưa đo benchmark thực tế. Chưa kiểm tra trên thiết bị điện thoại vật lý hoặc mọi trình duyệt. Fullscreen cần thao tác người dùng và quyền hỗ trợ của trình duyệt; có thể dùng F11 nếu cần.

## Cập nhật thiết kế theo ảnh tham khảo

- Thư mục hiện tại: `slide-show/` ở repo root. Các đường dẫn nguồn trong notes đã cập nhật theo vị trí mới.
- Nền giấy sáng, chữ đen đậm, viền/bóng cứng, màu hồng nhạt và xanh nhạt; trang mở đầu nhấn xanh blue.
- Thanh mục phía trên có thể bấm để chuyển chương, mục hiện tại có nền hồng.

- Thêm slide 10 cảm ơn khán giả, khoảng 10 giây. Tổng thời lượng gợi ý hiện tại khoảng 7 phút 10 giây.

## Cập nhật slide 6–8 (17/10/2026)

- Slide 6: tách UI, HTTP/API, VideoLibrary, hai lane indexing/search, SQLite và filesystem; bổ sung đường trả kết quả và preview.
- Slide 7: bổ sung FFmpeg, privacy, inference, YOLO11n/ByteTrack, EG2, bốn loại evidence và staging → kiểm tra → publish → ready.
- Slide 8: thể hiện năm bước query, nguồn index, ba nhánh mode và bước cắt top-k sau ranking theo mode.
- Đã kiểm tra bản cập nhật trong Chrome headless ở 1280×720 và stage 16:9 tại viewport 390×844; không phát hiện tràn khung hoặc lỗi JavaScript ở slide 6–8. Đã xem ảnh render để chỉnh khoảng cách với footer. Nội dung kiến trúc đối chiếu ARCHITECTURE.md; không chạy inference hoặc benchmark.
