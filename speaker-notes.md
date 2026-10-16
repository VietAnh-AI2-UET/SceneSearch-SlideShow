# SceneSearch — Speaker notes

Tổng thời lượng: **465 giây (khoảng 7 phút 45 giây)**. Thời lượng gồm lời nói, dừng để người xem đọc hình và chuyển ý. Screenshot là ảnh tĩnh, không phải video có thể phát trong slide.

## 1. SceneSearch — 20 giây (00:00–00:20)

**Lời dẫn:** SceneSearch là công cụ tìm kiếm ngữ nghĩa trong dữ liệu lái. Người dùng mô tả một cảnh cần tìm, nhận những clip ứng viên, rồi xem và duyệt clip phù hợp. Bài trình bày đi từ nhu cầu tìm dữ liệu đến thao tác sử dụng, kiến trúc và những phép đo cần có.

**Chuyển ý:** Vì sao việc tìm một cảnh ngắn lại tốn nhiều công sức?

**Nguồn:** `../dumb-scribings/presentation.md`, mục 1 và storyboard slide 1; `../ARCHITECTURE.md`, mục 1.

## 2. Nút thắt nằm ở khâu duyệt video — 75 giây (00:20–01:35)

**Lời dẫn:** Đây là tình huống giả định để minh họa, không phải benchmark. Giả sử nhóm cần một nghìn clip pedestrian crossing cho training AEB hoặc Trajectory Prediction. Hai nghìn giờ là tổng thời lượng dataset gốc trước khi lọc, gồm cảnh giao thông thông thường và cảnh đích, không phải video đã chỉ giữ lại cảnh pedestrian crossing. Tần suất giả định là trung bình hai giờ video lái xe mới có một lần pedestrian crossing; vì vậy cần khoảng một nghìn nhân hai bằng hai nghìn giờ video nguồn để kỳ vọng tìm được một nghìn cảnh. Đây là ước lượng theo tần suất, không bảo đảm đủ một nghìn cảnh. Mỗi sự kiện pedestrian crossing chỉ diễn ra trong một đến ba giây; đây là thời lượng hành vi cần tìm, không nhất thiết bằng độ dài clip trích xuất.

Đi theo năm bước trên hình: tiếp nhận yêu cầu khoảng hai giờ công, lọc metadata sáu giờ, duyệt thủ công chín trăm sáu mươi giờ, cắt và trích xuất năm mươi giờ, đóng gói tám giờ. Tổng cộng một nghìn không trăm hai mươi sáu giờ công. Khâu duyệt chiếm gần toàn bộ thanh màu cam, khoảng 93,6 phần trăm. Dữ liệu lớn, cảnh hiếm và diễn biến nhanh làm việc duyệt trở thành nút thắt.

**Nhịp trình bày:** Dừng ở số 2.000 giờ video, rồi chỉ vào 960 giờ công. Đây là hai đại lượng khác nhau. Không suy ra tốc độ duyệt đã đo từ hai số này.

**Phép tính:** 2 + 6 + 960 + 50 + 8 = 1.026 giờ công; 1.026 / 8 = 128,25 ngày công; 960 / 1.026 × 100 ≈ 93,567%; phần còn lại 66 giờ công. Thanh tỷ trọng dùng tỷ lệ này.

**Chuyển ý:** Khâu duyệt thủ công cần được tự động hóa. SceneSearch hỗ trợ tìm ứng viên để người dùng duyệt kết quả phù hợp. Chưa có bằng chứng cho tuyên bố “1.000 giờ thành vài phút”.

**Nguồn:** `../dumb-scribings/presentation.md`, mục 3 và storyboard slide 2. Toàn bộ số liệu tình huống do brief cung cấp.

## 3. Từ video đến câu truy vấn — 40 giây (01:35–02:15)

**Lời dẫn:** Người dùng upload video và chờ hệ thống hoàn tất xử lý, tạo index. Chỉ khi bộ video sẵn sàng mới bắt đầu tìm kiếm. Tiếp theo, nhập mô tả cảnh và chọn video nguồn hoặc khoảng thời gian cần tìm. Thời gian này tính trên video gốc, giúp giới hạn đúng phần dữ liệu cần xét.

Ví dụ nhu cầu của chúng ta là “pedestrian crossing”. Ảnh thật bên phải minh họa cùng loại cảnh bằng query English “pedestrian crossing the road”.

**Ngôn ngữ query:** UI nhận văn bản, truyền query xuống engine, không thấy bước dịch trong luồng đã kiểm tra. Screenshot và placeholder dùng English. Chưa xác minh chất lượng tiếng Việt; không khẳng định bắt buộc dùng English. Ví dụ trên slide dùng “pedestrian crossing”, phù hợp với loại cảnh trong screenshot.

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

**Nhịp trình bày:** Đi từ trái qua phải: Streamlit và DemoClient qua HTTP đến FastAPI, rồi VideoLibrary điều phối. Chỉ hai lane A/B: indexing ghi bản published, search đọc bản này. Bên phải, SQLite chỉ chứa records/trạng thái; filesystem chứa vectors, JSON và media. Kết bằng thanh trả kết quả: JSON cùng thời gian nguồn, còn preview URL có token dùng để phát safe.mp4. Các mũi tên hai chiều biểu diễn cả đọc/ghi hoặc request/response; không phải mọi service đều ghi mọi kho dữ liệu.

**Chuyển ý:** Đi sâu vào quá trình chuẩn bị dữ liệu trước khi tìm kiếm.

**Nguồn:** `../ARCHITECTURE.md`, mục 1, 4–6. Thành phần gốc: `DemoClient`, `VideoLibrary`, `product_index`, `ProductSearchEngine`, `WindowRepository`.

## 7. Embedding và indexing — 55 giây (04:20–05:15)

**Lời dẫn:** Video được chia thành các clip tối đa năm giây. Clip cuối giữ thời lượng thật. Từ đây có hai nhánh khác nhau. Nhánh raw clip xử lý privacy để tạo media đã làm mờ cho playback. Nhánh inference phục vụ model, tạo frames, tracks và embedding. Vì vậy không nên hiểu rằng mọi embedding đều lấy từ video đã làm mờ.

EG2 tạo GLOBAL vector đại diện toàn clip. Ngoài ra có local evidence: FRAME cho khung hình, WINDOW cho đoạn thời gian, TUBE theo object track. Các vector cùng metadata và media được ghi ra staging, kiểm tra, rồi publish thành index dùng cho tìm kiếm.

**Chi tiết kỹ thuật nếu được hỏi:** Bản inference có thể được pad theo đầu vào model. GLOBAL dùng 5 RGB frames; local specs gồm 8 FRAME, 3 WINDOW dài 2 giây và tối đa 3 TUBE. Geometry dùng YOLO11n và ByteTrack. Encoder tạo vector 768 chiều, normalized, FP32. Slide giữ tên EG2 theo tài liệu, không bổ sung tên biến thể chưa cần thiết. GLOBAL lấy frames từ inference; local evidence lấy frames và tracks của nhánh geometry.

**Nhịp trình bày:** Đi từ FFmpeg sang hai nhánh. Nhánh raw chạy phát hiện/theo dõi và pixelate, tạo safe.mp4 cùng poster để playback. Nhánh inference trích 5 RGB frames cho GLOBAL; geometry dùng YOLO11n + ByteTrack để chuẩn bị local specs. EG2 encode các đầu vào này thành vector 768 chiều, FP32, normalized. Chỉ bốn ô evidence, rồi kết ở staging → load_index → publish → SQLite ready. GLOBAL lấy trực tiếp từ frames inference; object tracks chỉ phục vụ local evidence.

**Chuyển ý:** Khi index đã sẵn sàng, mỗi query đi qua một luồng riêng.

**Nguồn:** `../ARCHITECTURE.md`, mục 2–4; `../demo/product_runtime.py`, `ProductEncoder`. Diagram là bản rút gọn của luồng chuẩn bị, không thể hiện privacy như đầu vào encoder.

## 8. Query và xếp hạng — 55 giây (05:15–06:10)

**Lời dẫn:** Query đi cùng bộ lọc. Engine chọn dữ liệu theo source và thời gian trước khi chấm điểm. EG2 encode query, rồi so với GLOBAL vectors đã normalized để tạo cosine ranking. Từ ranking này hệ thống trả top-k clip và metadata.

Mặc định eg2_only giữ ranking gốc. Nếu chọn shadow hoặc active, engine đánh giá local evidence trong EG2 Top-5. Shadow tính đánh giá nhưng vẫn giữ thứ tự EG2. Active có thể đưa một candidate trong Top-5 lên đầu theo quyết định của engine, giữ thứ tự tương đối của các candidate còn lại. Vì vậy reranking là nhánh tùy mode, không phải bước luôn chạy mặc định.

**Nhịp trình bày:** Theo năm bước từ trái sang phải: request, lọc corpus, encode query, cosine scores, ranking gốc. Thanh index phía trên mô tả hai nhóm dữ liệu có sẵn. Chọn một mode ở hàng dưới trước khi cắt top-k và trả metadata. Chỉ rõ shadow/active cùng chấm local_score và dùng decide trong EG2 Top-5; shadow chỉ ghi nhận đề xuất, active có thể đưa một candidate lên đầu. Top-5 và top-k có vai trò khác nhau. Query cache chỉ tiết kiệm bước encode khi đã có vector tương ứng.

**Chi tiết:** Query dùng prompt `SearchQuery`. Engine có cache query vector, nên benchmark cần phân biệt warm và cold cache. Cosine score không phải accuracy.

**Chuyển ý:** Để đánh giá giá trị thực tế, cần đo chất lượng và thời gian trong điều kiện rõ ràng.

**Nguồn:** `../ARCHITECTURE.md`, mục 5; `../demo/product_search.py`; `../hybrid_v2/driveevidence_v6_service.py`, `../hybrid_v2/driveevidence_v6_rerank.py` (truy vết được tài liệu kiến trúc chỉ ra).

## 9. Hiệu suất cần đo — 50 giây (06:10–07:00)

**Lời dẫn:** Số liệu do người dùng cung cấp: video đầu vào 10 phút, thời gian xử lý 30 phút, top-k bằng 5, thời gian phản hồi 1.000 ms. Kích thước index trên slide tính theo giả định query dùng cùng bộ video 10 phút: 120 clip. Số clip là số đoạn sau khi cắt video nguồn để indexing; 10 phút chia thành clip 5 giây tương ứng khoảng 120 clip, đã điền 120 theo phép tính này, không phải số đếm từ index thực tế. Bốn nhóm này là khung để bổ sung số đo thật. Đầu tiên ghi CPU, cores, threads và RAM. Tiếp theo chọn metric retrieval, k và tập đánh giá. Có thể chọn Precision@k hoặc Recall@k sau khi thống nhất ground truth và cách tính.

Với indexing, ghi thời lượng video, số clip và thời gian xử lý. Với query, ghi kích thước index, top-k và thời gian phản hồi. Hai giai đoạn phải đo riêng, vì query trên index có sẵn không bao gồm toàn bộ chi phí chuẩn bị video.

**Điều kiện cần bổ sung:** Đo riêng encoder hay toàn pipeline; có tính upload, privacy, geometry, publish không; device thực chạy; số lần lặp và cách tổng hợp; warm/cold cache; mode eg2_only/shadow/active; thời gian backend hay end-to-end gồm UI. Các ô chưa có dữ liệu tiếp tục để trống; kích thước index ghi 120 clip, theo giả định dùng cùng bộ video đầu vào. Không lấy thời gian 1,03 giây trong screenshot làm benchmark đại diện.

**Câu kết:** SceneSearch hướng đến rút ngắn khâu tìm cảnh thủ công để con người tập trung vào lựa chọn dữ liệu phù hợp.

**Nguồn:** `../dumb-scribings/presentation.md`, storyboard slide 9; `../ARCHITECTURE.md`, mục 4–5; `../demo/product_runtime.py`, lựa chọn device. Chưa chạy benchmark hoặc inference cho nhiệm vụ tạo slide này.


## 10. Workflow với SceneSearch — 35 giây (07:00–07:35)

**Lời dẫn:** Bắt đầu với chi phí chuẩn bị. Người dùng cung cấp embedding 3 phút video mất 9 phút, query 1 giây. Ngoại suy tuyến tính trên cùng cấu hình, xử lý tuần tự, 2.000 giờ video cần 6.000 giờ máy, tương đương 250 ngày chạy liên tục. Đây chỉ là embedding, chưa gồm upload, privacy, geometry và publish. Không coi giờ máy là giờ công; không suy ra tốc độ xử lý song song chưa đo.

Sau khi index sẵn sàng, giữ giả định tiếp nhận và lọc metadata 8 giờ công. Theo cập nhật của người dùng, soạn một query và filters mất 5 giây, hệ thống phản hồi trong 1 giây theo số được cung cấp. Giả định trả và duyệt 2.000 ứng viên, mỗi ứng viên 10 giây gồm xem và quyết định, với 1.000 clip được xác nhận đúng: 20.000 giây = 5,56 giờ công. Đây là giả định về chất lượng ứng viên và thao tác, không phải Precision@k đã đo; một query có thể không tìm đủ 1.000 clip thực tế. Clip đã được hệ thống cắt sẵn trong giai đoạn chuẩn bị nên không cộng lại 50 giờ cắt/trích xuất thủ công. Giữ giả định 8 giờ đóng gói từ ví dụ cũ; thời gian tải clip phụ thuộc dung lượng và đường truyền, chưa được đo.

**Phép tính:** 8 + 5/3600 + 2000×10/3600 + 8 = 21,557 giờ công ≈ 21,6 giờ công. 1 giây query là thời gian hệ thống riêng. So sánh khâu dò 960 giờ công với 5,6 giờ công duyệt ứng viên chỉ có giá trị theo giả định này. Ước lượng indexing áp dụng cho toàn dataset gốc, chưa tính giảm khối lượng nhờ lọc metadata vì chưa biết tỷ lệ giữ lại. Index có thể dùng lại cho truy vấn tiếp theo nếu dữ liệu không đổi.

**Nguồn:** Tốc độ embedding/query do người dùng cung cấp; khối lượng và workflow cũ từ slide 2. Thời gian soạn query do người dùng cung cấp; thời gian duyệt là giả định để lập kế hoạch, chưa benchmark.

## 11. Cảm ơn — 10 giây (07:35–07:45)

**Lời dẫn:** Cảm ơn mọi người đã theo dõi. Tôi rất mong nhận được câu hỏi và góp ý về SceneSearch.

**Nhịp trình bày:** Dừng ở slide này để kết thúc hoặc trao đổi với khán giả.


**Cập nhật phần cứng slide 9:** Đọc trực tiếp bằng Windows CIM: Intel Core i5-12500H (12th Gen), 12 cores / 16 threads, RAM 16 GB. Đây là cấu hình máy hiện tại; chưa xác minh các số thời gian được cung cấp đã được đo trên chính cấu hình này.


**Nguồn chất lượng retrieval slide 9:** `docs/embeddinggemma2.md`, mục Frozen evaluation and use, ghi EG2-B trên full200 (200 vectors, 63 positive queries): Top5=0.841270, MRR=0.630467. Điền Top5 (Hit@5), k=5, 84,13%. Đây là tỷ lệ query có ít nhất một clip liên quan trong 5 kết quả đầu, không phải Precision@5 hoặc tỷ lệ clip đúng trong Top-5. Tập full200 khác bộ video 10 phút / 120 clip đang minh họa indexing và query. Đây là số đánh giá lịch sử được ghi trong tài liệu repo, không phải benchmark vừa chạy; artifacts gốc không được phân phối cùng source theo tài liệu. Trong 45 positive queries không tham gia chọn cấu hình pilot, Top5=82,22%; không gọi 84,13% là kết quả heldout độc lập hoặc kết quả V6 active.
