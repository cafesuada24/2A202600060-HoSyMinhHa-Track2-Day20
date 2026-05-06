# Reflection — Lab 20 (Personal Report)

> **Đây là báo cáo cá nhân.** Mỗi học viên chạy lab trên laptop của mình, với spec của mình. Số liệu của bạn không so sánh được với bạn cùng lớp — chỉ so sánh **before vs after trên chính máy bạn**. Grade rubric tính theo độ rõ ràng của setup + tuning của bạn, không phải tốc độ tuyệt đối.

---

**Họ Tên:** _Ho Sy Minh Ha_
**Cohort:** _A20-K2_
**Ngày submit:** _2026-06-05_

---

## 1. Hardware spec (từ `00-setup/detect-hardware.py`)

> Paste output của `python 00-setup/detect-hardware.py` vào đây, hoặc điền thủ công:

- **OS:** _Linux 6.17.0-23-generic (x86_64)_
- **CPU:** _11th Gen Intel(R) Core(TM) i5-11300H @ 3.10GHz_
- **Cores:** _8 physical · 8 logical cores_
- **CPU extensions:** _AVX-512_
- **RAM:** _15.3 GB_
- **Accelerator:** _CPU only (no discrete accelerator)_
- **llama.cpp backend đã chọn:** _CPU_
- **Recommended model tier:** _Qwen2.5-1.5B-Instruct (Q4_K_M)_

**Setup story**
_Không thay đổi quá nhiều, chỉ dùng uv để setup nhanh hơn_

---

## 2. Track 01 — Quickstart numbers (từ `benchmarks/01-quickstart-results.md`)

> Paste bảng từ `benchmarks/01-quickstart-results.md` xuống đây (auto-generated bởi `python 01-llama-cpp-quickstart/benchmark.py`).

| Model | Load (ms) | TTFT P50/P95 (ms) | TPOT P50/P95 (ms) | E2E P50/P95/P99 (ms) | Decode rate (tok/s) |
|---|---:|---:|---:|---:|---:|
| qwen2.5-1.5b-instruct-q4_k_m.gguf | 690 | 93 / 110 | 29.9 / 30.6 | 1969 / 2011 / 2012 | 33.5 |
| qwen2.5-1.5b-instruct-q2_k.gguf | 707 | 134 / 161 | 23.2 / 24.6 | 1589 / 1676 / 1697 | 43.0 |


---

## 3. Track 02 — llama-server load test

> Chạy 2 lần locust ở concurrency 10 và 50, paste tóm tắt bên dưới.

| Concurrency | Total RPS | TTFB P50 (ms) | E2E P95 (ms) | E2E P99 (ms) | Failures |
|--:|--:|--:|--:|--:|--:|
| 10 | 56 | 8100 | 12000 | 14000 | 0 |
| 50 | 63  | 15000 | 26000 | 28000 | 0 |


---

## 4. Track 03 — Milestone integration

- **N16 (Cloud/IaC):** _stub: localhost only_
- **N17 (Data pipeline):** _"stub: in-memory dict"_
- **N18 (Lakehouse):** _stub: SQLite_
- **N19 (Vector + Feature Store):** _stub: TOY_DOCS_

**Nơi tốn nhiều ms nhất** trong pipeline (đo bằng `time.perf_counter` trong `pipeline.py`):

- embed: _0_
- retrieve: _0_
- llama-server: _6506_


---

## 5. Bonus — The single change that mattered most

> **Most important section.** Pick **một** thay đổi từ bonus track (build flag, thread sweep, quant pick, GPU offload, KV-cache quantization, speculative decoding, bất cứ challenge nào trong `BONUS-llama-cpp-optimization/CHALLENGES.md`) đã tạo ra speedup lớn nhất trên máy bạn.

**Change:** _<vd: rebuild llama.cpp với `-DGGML_NATIVE=ON -DGGML_BLAS=ON`; vd: hạ `-t` từ 12 xuống 6; vd: bật Metal trên M2>_

**Before vs after** (paste 2-3 dòng từ sweep output):

```
before: <số liệu>
after:  <số liệu>
speedup: ~<X.Y>×
```

**Tại sao nó work** (1–2 đoạn ngắn — đây là phần grader đọc kỹ nhất):

_Giải thích như đang nói với một bạn cùng lớp đang ngồi cạnh. Tránh "vibes-based" reasoning — bám vào mô hình mental của hardware (memory bandwidth? compute? cache?). Nếu kết quả khác kỳ vọng từ deck, nói rõ — đó là phần grader thưởng điểm._


---

## 7. Self-graded checklist

- [ x ] `hardware.json` đã commit
- [ x ] `models/active.json` đã commit (hoặc paste path snapshot vào section 1)
- [ x ] `benchmarks/01-quickstart-results.md` đã commit
- [ x ] `benchmarks/02-server-results.md` (hoặc CSV từ `record-metrics.py`) đã commit
- [ x ] `benchmarks/bonus-*.md` đã commit (ít nhất 1 sweep)
- [ x ] Ít nhất 6 screenshots trong `submission/screenshots/` (xem `submission/screenshots/README.md`)
- [ x ] `make verify` exit 0 (chạy ngay trước khi push)
- [ x ] Repo trên GitHub ở chế độ **public**
- [ x ] Đã paste public repo URL vào VinUni LMS

---
