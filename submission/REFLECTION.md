# Reflection — Lab 19

**Tên:** Học viên AICB
**Cohort:** A20-K1
**Path đã chạy:** lite

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

- **Exact queries:** BM25 và Hybrid đều đạt 100% Precision@10 nhờ từ khóa kỹ thuật khớp chính xác.
- **Paraphrase queries:** Với `bge-small-en` (384d, English-trained), Vector bị suy giảm (25.3%) khi diễn đạt lại bằng tiếng Việt; BM25 & Hybrid giữ 100% nhờ giữ được thuật ngữ gốc. Đổi sang `bge-m3` (Docker path) sẽ giúp Vector phát huy tối đa semantic search tiếng Việt.
- **Mixed queries:** Hybrid duy trì độ chính xác cao nhất (100%) nhờ kết hợp tín hiệu khớp exact-keyword và ngữ nghĩa qua RRF ($k=60$).

**Khi nào KHÔNG dùng Hybrid?**
1. **Pure BM25:** Tra cứu mã định danh (SKU, Error Code, ID, Log) đòi hỏi exact-match 100%, hoặc hệ thống siêu nhẹ cần tiết kiệm RAM/latency (không dùng embedding model).
2. **Pure Vector:** Tìm kiếm đa phương thức (Ảnh-Text), cross-lingual, hoặc truy vấn gợi ý ý tưởng mà từ khóa biến đổi hoàn toàn.

---

## Điều ngạc nhiên nhất khi làm lab này

RRF ($k=60$) kết hợp 2 thang điểm khác nhau (BM25 float score & Cosine similarity) một cách vô cùng hiệu quả và ổn định mà không cần chuẩn hóa điểm số hay train reranker model.

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- [ ] Pair work với: _N/A_
