# Reflection — Lab 19

**Tên:** Học viên AICB
**Cohort:** A20-K1
**Path đã chạy:** lite

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

- **Exact queries (n=15):** BM25 và Hybrid đều đạt 96.7% Precision@10 (Vector: 88.7%) nhờ từ khóa kỹ thuật khớp chính xác.
- **Paraphrase queries (n=15):** Cả 3 mode suy giảm do `bge-small-en` hạn chế với tiếng Việt; BM25 đạt 33.3%, Hybrid 32.0%, Vector giảm sâu xuống 24.0% (cần đổi sang `bge-m3` để tối ưu ngữ nghĩa).
- **Mixed queries (n=20):** Hybrid đạt 100.0% Precision@10 (vượt Vector 98.5%, BM25 97.0%) nhờ kết hợp exact-keyword và ngữ nghĩa qua RRF ($k=60$). Đạt tổng thể Hybrid (78.6%) > BM25 (77.8%) > Vector (73.2%).

**Khi nào KHÔNG dùng Hybrid?**
1. **Pure BM25:** Tra cứu mã định danh (SKU, Error Code, ID, Log) đòi hỏi exact-match 100%, hoặc hệ thống siêu nhẹ cần tối ưu latency/RAM (BM25 P50 ~2.3ms vs Hybrid ~125.4ms, không tốn tài nguyên embedding).
2. **Pure Vector:** Tìm kiếm đa phương thức (Ảnh-Text), cross-lingual, hoặc truy vấn gợi ý ý tưởng mà từ khóa biến đổi hoàn toàn không trùng lặp keyword.

---

## Điều ngạc nhiên nhất khi làm lab này

RRF ($k=60$) kết hợp 2 thang điểm khác nhau (BM25 float score & Cosine similarity) một cách vô cùng hiệu quả và ổn định mà không cần chuẩn hóa điểm số hay train reranker model.

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- [ ] Pair work với: _N/A_
