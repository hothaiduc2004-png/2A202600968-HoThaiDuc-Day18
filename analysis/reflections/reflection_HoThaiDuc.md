# Reflection: HoThaiDuc

## Phần 1: Mapping bài giảng vào code

| Lecture Concept | Module | Hàm cụ thể | Observation |
|----------------|--------|------------|-------------|
| Semantic chunking | M1 | `chunk_semantic()` | Dùng cosine similarity để gom các câu liên quan và tránh cắt ý giữa chừng. Fallback về grouping thô khi embedding không sẵn sàng. |
| BM25 + Dense fusion | M2 | `reciprocal_rank_fusion()` | Kết hợp BM25 và Qdrant dense search, rồi merge kết quả bằng RRF để tận dụng cả keyword và semantic. |
| Cross-encoder reranking | M3 | `CrossEncoderReranker.rerank()` | Reranker xếp lại các document top-k bằng CrossEncoder; nếu model không tải được thì fallback theo score gốc. |
| RAGAS 4 metrics | M4 | `evaluate_ragas()` | Bao bọc gọi RAGAS bằng try/except, trả về các metric chính và `per_question` để phân tích failure. |
| Contextual enrichment | M5 | `contextual_prepend()` | Prepend metadata văn bản vào chunk để tăng chất lượng retrieval; `enrich_chunks()` hỗ trợ chế độ combined và fallback không API. |

## Phần 2: Khó khăn & giải quyết

- Khó khăn: `src/m5_enrichment.py` có lỗi fallback và phần code thừa sau `contextual_prepend()` khiến module không đọc đúng.
- Debug: Dùng `pytest tests/ -q` để tìm lỗi cụ thể; đọc traceback khi `check_lab.py` thông báo test parsing fail và sửa phần mã không hợp lệ.
- Kiến thức thiếu: Tương tác với Qdrant/Docker trong môi trường Windows và cách xử lý API fallback khi OpenAI key không có.
- Cách bổ sung: Nâng cao hiểu về tương thích client/server Qdrant và chuẩn prompt LLM cho enrichment.

## Phần 3: Action Plan cho project

## Project: RAG Knowledge Assistant

### Hiện tại
- RAG pipeline hiện tại: M1 chunking, M5 enrichment, M2 hybrid search, M3 reranking, M4 evaluation. Các module đã được implement và test ổn định tại code level.
- Known issues: Chưa sinh được `reports/ragas_report.json` vì Qdrant/Docker chưa chạy trong môi trường hiện tại; cần chạy Docker Compose và khởi tạo Qdrant.

### Plan áp dụng
1. [ ] Chunking strategy: giữ hierarchical parent-child + semantic grouping để cân bằng context và precision.
2. [ ] Search: dùng hybrid BM25 + dense, vì corpus tiếng Việt cần cả keyword và semantic match.
3. [ ] Reranking: có, dùng cross-encoder nếu có model, nếu không fallback thành score gốc.
4. [ ] Evaluation: dùng RAGAS 4 metrics để so sánh faithfulness, relevancy, precision, recall.
5. [ ] Enrichment: dùng chế độ combined nếu có API key, fallback bằng summary/hyqa/contextual khi offline.

### Timeline
- Tuần 1: Hoàn thiện chunking và hybrid retrieval, đảm bảo end-to-end pipeline chạy với Qdrant.
- Tuần 2: Tối ưu reranking và enrichment, kiểm tra RAGAS, và hoàn thiện failure analysis.
- Tuần 3: Triển khai cải tiến metadata filtering, prompt design, và báo cáo project.
