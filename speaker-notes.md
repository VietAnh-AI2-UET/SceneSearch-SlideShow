# SceneSearch — Speaker notes

Tổng thời lượng: **430 giây (khoảng 7 phút 10 giây)**. Thời lượng gồm lời nói, dừng để người xem đọc hình và chuyển ý. Screenshot là ảnh tĩnh, không phải video có thể phát trong slide.

## 1. SceneSearch — 20 giây (00:00–00:20)

**Lời dẫn:** SceneSearch là công cụ tìm kiếm ngữ nghĩa trong dữ liệu lái. Người dùng mô tả một cảnh cần tìm, nhận những clip ứng viên, rồi xem và duyệt clip phù hợp. Bài trình bày đi từ nhu cầu tìm dữ liệu đến thao tác sử dụng, kiến trúc và những phép đo cần có.

**Chuyển ý:** Vì sao việc tìm một cảnh ngắn lại tốn nhiều công sức?

**Nguồn:** `../dumb-scribings/presentation.md`, mục 1 và storyboard slide 1; `../ARCHITECTURE.md`, mục 1.

## 2. Nút thắt nằm ở khâu duyệt video — 75 giây (00:20–01:35)

**Lời dẫn:** Đây là tình huống giả định để minh họa, không phải benchmark. Giả sử nhóm cần một nghìn clip xe máy tạt đầu cho training AEB hoặc Trajectory Prediction. Nếu trung bình hai giờ lái mới gặp một cảnh, khối lượng cần tìm khoảng hai nghìn giờ video. Nhưng sự kiện đáng quan tâm có thể chỉ kéo dài một đến ba giây.

Đi theo năm bước trên hình: tiếp nhận yêu cầu khoảng hai giờ công, lọc metadata sáu giờ, duyệt thủ công chín trăm sáu mươi giờ, cắt và trích xuất năm mươi giờ, đóng gói tám giờ. Tổng cộng một nghìn không trăm hai mươi sáu giờ công. Khâu duyệt chiếm gần toàn bộ thanh màu cam, khoảng 93,6 phần trăm. Dữ liệu lớn, cảnh hiếm và diễn biến nhanh làm việc duyệt trở thành nút thắt.

**Nhịp trình bày:** Dừng ở số 2.000 giờ video, rồi chỉ vào 960 giờ công. Đây là hai đại lượng khác nhau. Không suy ra tốc độ duyệt đã đo từ hai số này.

**Phép tính:** 2 + 6 + 960 + 50 + 8 = 1.026 giờ công; 1.026 / 8 = 128,25 ngày công; 960 / 1.026 × 100 ≈ 93,567%; phần còn lại 66 giờ công. Thanh tỷ trọng dùng tỷ lệ này.

**Chuyển ý:** SceneSearch tìm ứng viên bằng mô tả để người dùng tập trung vào duyệt kết quả. Chưa có bằng chứng cho tuyên bố “1.000 giờ thành vài phút”.

**Nguồn:** `../dumb-scribings/presentation.md`, mục 3 và storyboard slide 2. Toàn bộ số liệu tình huống do brief cung cấp.

## 3. Từ video đến câu truy vấn — 40 giây (01:35–02:15)

**Lời dẫn:** Người dùng upload video và chờ hệ thống hoàn tất xử lý, tạo index. Chỉ khi bộ video sẵn sàng mới bắt đầu tìm kiếm. Tiếp theo, nhập mô tả cảnh và chọn video nguồn hoặc khoảng thời gian cần tìm. Thời gian này tính trên video gốc, giúp giới hạn đúng phần dữ liệu cần xét.

Ví dụ nhu cầu của chúng ta là “xe máy tạt đầu”. Ảnh thật bên phải minh họa thao tác bằng query English “pedestrian crossing the road”; đây là một cảnh khác, dùng để giới thiệu giao diện.

**Ngôn ngữ query:** UI nhận văn bản, truyền query xuống engine, không thấy bước dịch trong luồng đã kiểm tra. Screenshot và placeholder dùng English. Chưa xác minh chất lượng tiếng Việt; không khẳng định bắt buộc dùng English. Có thể thử “a motorcycle cutting in front of the ego vehicle” khi demo cảnh xe máy, nhưng đây là câu đề xuất chưa chạy thử.

**Chuyển ý:** Sau khi tìm kiếm, chúng ta xem clip và đối chiếu thông tin nguồn.

**Nguồn:** `../ARCHITECTURE.md`, mục 2, 5; `../demo/streamlit_app.py`, `upload_view`, `processing_status`, `search_view`; ảnh `assets/image-1.png`. Đã xem ảnh upload `assets/image.png` nhưng không đưa vào mặt slide để tránh chật.

## 4. Xem cảnh, kiểm tra mốc thời gian — 45 giây (02:15–03:00)

**Lời dẫn:** Kết quả được sắp theo ranking để người dùng lần lượt kiểm tra. Bên trái là clip demo đã xử lý privacy. Chú ý vùng mặt người và biển số có pixelate. Đây là minh họa cho media playback sau xử lý, không có nghĩa mọi mặt hay biển số đều luôn được che hoàn hảo.

Bảng bên phải giữ tên video, thời điểm bắt đầu, kết thúc và bộ video. Sample trong ảnh là khoảng 02:05 đến 02:10 của video gốc, trong khi trình phát clip bắt đầu từ 00:00. Điểm tương đồng 0,6727 trong ảnh chỉ giúp xếp hạng, không có nghĩa xác suất đúng 67,27 phần trăm.

**Nhịp trình bày:** Chỉ lần lượt vào clip, vùng làm mờ và metadata. Khi chia sẻ clip thực tế vẫn cần kiểm tra nội dung.

**Chuyển ý:** Hệ thống gợi ý ứng viên, còn quyết định sử dụng nằm ở người dùng.

**Nguồn:** `../ARCHITECTURE.md`, mục 3, 6; `../demo/streamlit_app.py`, `player`; `assets/image-3.png`, `assets/image-4.png`. Ảnh metadata crop phần bảng, giữ nguyên giá trị.

## 5. Người dùng quyết định clip phù hợp — 40 giây (03:00–03:40)

**Lời dẫn:** Người dùng xem ứng viên, đánh dấu clip phù hợp rồi vào mục Đã lưu để xem lại. Đây là bước human in the loop: con người xác nhận clip có đáp ứng nhu cầu dữ liệu hay không. Thao tác này không tự retrain model.

Có ba loại đầu ra cần phân biệt. CSV là bảng kết quả tìm kiếm, gồm metadata, rank và score. MP4 là từng clip đã xử lý privacy. JSON xuất danh sách đã lưu. Danh sách đánh dấu và lịch sử tìm kiếm chỉ giữ trong session hiện tại, không nên coi là kho lưu lựa chọn vĩnh viễn.

**Chi tiết CSV:** `rank`, `clip_id`, `source_id`, `filename`, `start_sec`, `end_sec`, `global_score`, `final_score`, `mode`, `privacy`.

**Chuyển ý:** Những thao tác đó được nối với backend như thế nào?

**Nguồn:** `../ARCHITECTURE.md`, mục 6; `../demo/streamlit_app.py`, `csv_results`, `save_result`, `saved_view`, `player`; `assets/image-2.png`.

## 6. Kiến trúc tổng quan — 40 giây (03:40–04:20)

**Lời dẫn:** Giao diện Streamlit gửi video hoặc query qua API FastAPI. Với video mới, backend điều phối xử lý video và embedding, rồi tạo index. Với query, backend gọi retrieval và ranking trên index đã có. Kết quả trả về gồm clip và metadata để UI hiển thị.

Có hai nơi lưu dữ liệu cần phân biệt. SQLite giữ upload records và trạng thái. Filesystem giữ vectors, metadata và media. Kiến trúc hiện tại không cần vẽ thêm một vector database hay dịch vụ cloud. Sơ đồ này gom các thành phần triển khai thành những khối dễ theo dõi.

**Nhịp trình bày:** Theo hàng trên từ trái sang phải cho indexing. Theo mũi tên query và index xuống retrieval, rồi theo hàng dưới sang trái về UI.

**Chuyển ý:** Đi sâu vào quá trình chuẩn bị dữ liệu trước khi tìm kiếm.

**Nguồn:** `../ARCHITECTURE.md`, mục 1, 4–6. Thành phần gốc: `DemoClient`, `VideoLibrary`, `product_index`, `ProductSearchEngine`, `WindowRepository`.

## 7. Embedding và indexing — 55 giây (04:20–05:15)

**Lời dẫn:** Video được chia thành các clip tối đa năm giây. Clip cuối giữ thời lượng thật. Từ đây có hai nhánh khác nhau. Nhánh raw clip xử lý privacy để tạo media đã làm mờ cho playback. Nhánh inference phục vụ model, tạo frames, tracks và embedding. Vì vậy không nên hiểu rằng mọi embedding đều lấy từ video đã làm mờ.

EG2 tạo GLOBAL vector đại diện toàn clip. Ngoài ra có local evidence: FRAME cho khung hình, WINDOW cho đoạn thời gian, TUBE theo object track. Các vector cùng metadata và media được ghi ra staging, kiểm tra, rồi publish thành index dùng cho tìm kiếm.

**Chi tiết kỹ thuật nếu được hỏi:** Bản inference có thể được pad theo đầu vào model. GLOBAL dùng 5 RGB frames; local specs gồm 8 FRAME, 3 WINDOW dài 2 giây và tối đa 3 TUBE. Geometry dùng YOLO11n và ByteTrack. Encoder tạo vector 768 chiều, normalized, FP32. Slide giữ tên EG2 theo tài liệu, không bổ sung tên biến thể chưa cần thiết. GLOBAL lấy frames từ inference; local evidence lấy frames và tracks của nhánh geometry.

**Chuyển ý:** Khi index đã sẵn sàng, mỗi query đi qua một luồng riêng.

**Nguồn:** `../ARCHITECTURE.md`, mục 2–4; `../demo/product_runtime.py`, `ProductEncoder`. Diagram là bản rút gọn của luồng chuẩn bị, không thể hiện privacy như đầu vào encoder.

## 8. Query và xếp hạng — 55 giây (05:15–06:10)

**Lời dẫn:** Query đi cùng bộ lọc. Engine chọn dữ liệu theo source và thời gian trước khi chấm điểm. EG2 encode query, rồi so với GLOBAL vectors đã normalized để tạo cosine ranking. Từ ranking này hệ thống trả top-k clip và metadata.

Mặc định eg2_only giữ ranking gốc. Nếu chọn shadow hoặc active, engine đánh giá local evidence trong EG2 Top-5. Shadow tính đánh giá nhưng vẫn giữ thứ tự EG2. Active có thể đưa một candidate trong Top-5 lên đầu theo quyết định của engine, giữ thứ tự tương đối của các candidate còn lại. Vì vậy reranking là nhánh tùy mode, không phải bước luôn chạy mặc định.

**Nhịp trình bày:** Đi hàng trên sang phải, xuống cosine ranking, rồi theo hàng dưới sang trái tới kết quả. Sau đó giải thích nhánh tùy mode. Top-5 là phạm vi đánh giá local evidence; top-k là số kết quả được trả theo yêu cầu. Local evidence, khi bật, tham gia trước đầu ra cuối cùng.

**Chi tiết:** Query dùng prompt `SearchQuery`. Engine có cache query vector, nên benchmark cần phân biệt warm và cold cache. Cosine score không phải accuracy.

**Chuyển ý:** Để đánh giá giá trị thực tế, cần đo chất lượng và thời gian trong điều kiện rõ ràng.

**Nguồn:** `../ARCHITECTURE.md`, mục 5; `../demo/product_search.py`; `../hybrid_v2/driveevidence_v6_service.py`, `../hybrid_v2/driveevidence_v6_rerank.py` (truy vết được tài liệu kiến trúc chỉ ra).

## 9. Hiệu suất cần đo — 50 giây (06:10–07:00)

**Lời dẫn:** Hiện chưa có số liệu benchmark trong bộ slide. Bốn nhóm này là khung để bổ sung số đo thật. Đầu tiên ghi CPU, cores, threads và RAM. Tiếp theo chọn metric retrieval, k và tập đánh giá. Có thể chọn Precision@k hoặc Recall@k sau khi thống nhất ground truth và cách tính.

Với indexing, ghi thời lượng video, số clip và thời gian xử lý. Với query, ghi kích thước index, top-k và thời gian phản hồi. Hai giai đoạn phải đo riêng, vì query trên index có sẵn không bao gồm toàn bộ chi phí chuẩn bị video.

**Điều kiện cần bổ sung:** Đo riêng encoder hay toàn pipeline; có tính upload, privacy, geometry, publish không; device thực chạy; số lần lặp và cách tổng hợp; warm/cold cache; mode eg2_only/shadow/active; thời gian backend hay end-to-end gồm UI. Giữ các ô giá trị rỗng cho tới khi có dữ liệu. Không lấy thời gian 1,03 giây trong screenshot làm benchmark đại diện.

**Câu kết:** SceneSearch hướng đến rút ngắn khâu tìm cảnh thủ công để con người tập trung vào lựa chọn dữ liệu phù hợp.

**Nguồn:** `../dumb-scribings/presentation.md`, storyboard slide 9; `../ARCHITECTURE.md`, mục 4–5; `../demo/product_runtime.py`, lựa chọn device. Chưa chạy benchmark hoặc inference cho nhiệm vụ tạo slide này.


## 10. Cảm ơn — 10 giây (07:00–07:10)

**Lời dẫn:** Cảm ơn mọi người đã theo dõi. Tôi rất mong nhận được câu hỏi và góp ý về SceneSearch.

**Nhịp trình bày:** Dừng ở slide này để kết thúc hoặc trao đổi với khán giả.
