# Chủ đề bài mới độc lập (lấy cảm hứng từ baseline nội bộ three-stage, nhưng không phụ thuộc bài chưa duyệt)

Nguồn tổng hợp chính: `LongTTask/papers-ref/related/02_literature_review_5_bai_bao_bearing_mamba_anomaly.md`. File `LongTTask/01_buoc_1_doc_bai_bao_dau_tien.md` chỉ dùng như ghi chú nội bộ về một baseline đã thử nghiệm (không trình bày như công trình đã duyệt/xuất bản).


## 1. Tóm tắt “khoảng trống” để phát triển từ bài gốc

Baseline nội bộ (three-stage classification) mạnh ở:

- Pipeline nhẹ: STFT + CNN (vibration) + descriptor nhiệt 6-D (temperature) + late fusion.
- Đánh giá leakage-aware theo trục TTF%, kết quả tốt ở late-life.

Nhưng còn hạn chế (và cũng là hạn chế phổ biến của hướng classification theo stage):

- Vẫn là **supervised classification**, phụ thuộc vào nhãn/threshold TTF.
- **Healthy–Degrading transition (60–70% TTF)** là vùng khó và quan trọng nhất cho phát hiện sớm.
- Chưa mô hình hóa động học chuỗi dài rõ ràng; xử lý chủ yếu theo cửa sổ ngắn.

Sau khi đọc 5 bài (DL-MHMS survey, Multimodal ML survey, USAD, Anomaly Transformer, Mamba), có thể chốt gap:

```text
Chưa có hướng nào giải quyết đồng thời:
Bearing run-to-failure
+ vibration–temperature fusion
+ self-supervised forecasting
+ prediction-error anomaly score
+ early degradation detection (Healthy→Degrading)
+ long-sequence efficient modeling (Mamba)
+ leakage-aware temporal evaluation
```

## 2. 3 hướng chủ đề có thể đi sâu

### Hướng A (Khuyến nghị): Forecasting-based anomaly detection tập trung “early degradation”

**Tên chủ đề gợi ý:**

- Self-Supervised Forecasting-Based Anomaly Detection for Early Bearing Degradation using Vibration–Temperature Signals

**Ý tưởng chính:**

- Chuyển bài toán từ `classification(Healthy/Degrading/Fault)` sang `forecasting`.
- Train mô hình chủ yếu trên vùng Healthy/early-life (0–60% TTF) để học normal dynamics.
- Dùng **prediction error** (MSE/MAE) làm **anomaly score**; phát hiện suy thoái sớm khi score vượt ngưỡng.

**Vì sao ăn khớp với bài gốc:**

- Bài gốc đã dùng TTF split và nêu rõ “Healthy–Degrading boundary” là điểm yếu.
- Forecasting/anomaly score giải quyết đúng “ranh giới mơ hồ” của Degrading.
- Vẫn tận dụng vibration+temperature; temperature có thể làm score ổn định hơn.

**Đóng góp dự kiến (3–4 ý):**

1. Đề xuất framework self-supervised forecasting cho bearing degradation detection trong run-to-failure.
2. Định nghĩa anomaly score từ prediction error và giao thức thresholding/detection delay theo TTF%.
3. Phân tích vai trò vibration–temperature (vib-only vs vib+temp) cho early detection và false alarm.
4. Đánh giá leakage-aware theo temporal split (TTF-aligned), tập trung vùng 60–70% TTF.

**Rủi ro/khoá chặt:**

- Cần xác định rõ task: multi-step forecasting (K bước) hay one-step.
- Cần đảm bảo không “leak” thông tin tương lai qua normalization.

---

### Hướng B: CNN/Patching + Mamba cho long-sequence forecasting/anomaly

**Tên chủ đề gợi ý:**

- CNN/Patching-Mamba for Long-Sequence Vibration–Temperature Forecasting in Bearing Degradation Detection

**Ý tưởng chính:**

- Dữ liệu vibration dài và nhiễu, cần mô hình chuỗi dài hiệu quả.
- Dùng CNN/Patching để nén tín hiệu, rồi dùng **Mamba** để học quan hệ dài hạn.
- Forecast tương lai và dùng prediction error/association-based score làm anomaly score.

**Vì sao dựa được trên literature review 5 bài:**

- Mamba: backbone xử lý chuỗi dài tuyến tính.
- Anomaly Transformer: nhấn mạnh temporal association (có thể làm baseline).

**Đóng góp dự kiến:**

- Chứng minh Mamba phù hợp hơn Transformer/LSTM/TCN về runtime/memory trong chuỗi dài.
- Phân tích chất lượng phát hiện suy thoái sớm và detection delay.

**Rủi ro/khoá chặt:**

- Nếu dataset chỉ 1 run, lợi thế long-sequence có thể khó “chứng minh mạnh” nếu thiếu external validation.

---

### Hướng C: Multimodal anomaly score có “giải thích được” (decomposed score)

**Tên chủ đề gợi ý:**

- Decomposed Anomaly Scoring for Bearing Degradation: Separating Vibration and Temperature Prediction Errors

**Ý tưởng chính:**

- Tách anomaly score thành 2 phần: `score_vib` và `score_temp`.
- Học fusion (concat/weighted/attention) để tạo `score_total`.
- Phân tích tình huống temperature giúp ở late-life và khả năng giảm false alarm ở early-life.

**Đóng góp dự kiến:**

- Score decomposition giúp interpretability: “bất thường do cơ hay do nhiệt”.
- Ablation sâu về fusion và thresholding.

**Rủi ro/khoá chặt:**

- Cần thiết kế thí nghiệm khéo để chứng minh “giải thích được” có lợi thực sự (không chỉ là visualization).

## 3. Chủ đề khuyến nghị để chốt (đề xuất chọn)

Chốt theo Hướng A làm trục bài, và dùng Hướng B như “kiến trúc đề xuất” (Mamba) + baseline so sánh.

**Chủ đề chốt (1 câu):**

> Self-Supervised Forecasting-Based Anomaly Detection for Early Bearing Degradation using Vibration–Temperature Signals with Long-Sequence Modeling (CNN/Patching-Mamba).

## 4. Đề xuất Research Questions (để bám theo bài gốc)

1. Forecasting-based anomaly detection có phát hiện sớm vùng Healthy→Degrading tốt hơn classification-based approach không (đặc biệt 60–70% TTF)?
2. Mamba có cải thiện hiệu quả (detection/F1/delay) hoặc chi phí (runtime/memory) so với LSTM/TCN/Transformer trong chuỗi dài vibration–temperature không?
3. Temperature đóng vai trò gì trong early detection: tăng recall hay giảm false alarm (so với vib-only)?
4. Anomaly score/thresholding nào ổn định nhất trong leakage-aware temporal evaluation (3-sigma vs percentile vs learned threshold)?

## 5. Experimental skeleton (khung thực nghiệm tối thiểu)

- **Data split (leakage-aware):**
  - Train: 0–60% TTF (healthy/normal)
  - Val: 60–70% TTF (transition)
  - Test: 70–100% TTF (degrading+fault)

- **Task setup:**
  - Input: N bước quá khứ, 4 kênh (vib_x, vib_y, temp1, temp2)
  - Output: K bước tương lai (multi-step)

- **Baselines tối thiểu:**
  - LSTM/GRU forecasting
  - TCN forecasting
  - Transformer forecasting (hoặc iTransformer nếu có sẵn)
  - USAD / AE-based anomaly detection (reconstruction error)
  - (Optional) Anomaly Transformer

- **Metrics:**
  - Forecasting: MSE/MAE/RMSE trên vùng train/val/test
  - Detection: AUC/F1/Recall/False alarm rate/Detection delay theo TTF%

## 6. “Điểm nhấn” để bài mới khác bài gốc rõ ràng

- Bài gốc: **classification** theo nhãn stage.
- Bài mới: **self-supervised forecasting** + **prediction-error anomaly score** tập trung early degradation.
- Bài gốc: CNN/STFT per-window.
- Bài mới: long-sequence modeling (Mamba) để học degradation dynamics theo thời gian dài.

## 7. Việc tiếp theo cần làm (để triển khai chủ đề)

1. Chốt chính xác định nghĩa dữ liệu forecasting: N/K, stride, windowing, normalization (train-only).
2. Chốt anomaly score + thresholding và cách tính detection delay theo TTF%.
3. Chốt kiến trúc baseline và kiến trúc đề xuất (CNN/Patching-Mamba).
4. Viết lại research gap + contribution theo đúng “điểm nhấn” ở mục 6.
