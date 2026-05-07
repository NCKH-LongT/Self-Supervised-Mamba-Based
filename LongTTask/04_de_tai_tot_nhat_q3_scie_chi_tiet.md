# Đề tài tốt nhất để nhắm Q3 SCIE (bản chi tiết, độc lập với bài three-stage chưa duyệt)

Nguồn: tổng hợp từ `LongTTask/papers-ref/related/02_literature_review_5_bai_bao_bearing_mamba_anomaly.md` và hướng nghiên cứu nội bộ của nhóm (một baseline STFT + vibration–temperature fusion đã thử nghiệm trước đây, hiện chưa được duyệt/xuất bản).

## 1. Kết luận chọn chủ đề (đủ độc lập để viết bài mới)

Chủ đề có khả năng ra bài Q3 SCIE cao nhất (với câu chuyện rõ + thực nghiệm khả thi khi dữ liệu hạn chế) là:

> Self-Supervised Forecasting-Based Anomaly Detection for Early Bearing Degradation using Vibration–Temperature Signals with Long-Sequence Modeling (CNN/Patching-Mamba).

Lý do chọn (không phụ thuộc bài three-stage như một công trình đã được duyệt):

- Bài toán early degradation trong run-to-failure vốn có ranh giới mơ hồ giữa normal và suy thoái sớm; đây là gap tự nhiên của hướng classification theo stage.
- “Early degradation detection” là câu chuyện đủ mạnh để thành bài mới, không chỉ “thay model”, và có thể biện minh trực tiếp từ literature.
- Forecasting-based anomaly detection giải bài toán ranh giới nhãn mơ hồ, giảm phụ thuộc vào stage label.
- Mamba đóng vai trò backbone chuỗi dài: có cơ sở từ literature (long-sequence, chi phí tốt hơn attention) mà vẫn không biến bài thành “thuần model”.
- Nếu cần “cầu nối thực nghiệm”, nhóm có thể đưa thêm một baseline STFT + vibration–temperature fusion như một mốc so sánh nội bộ (không trình bày như công trình đã công bố).

## 2. Định nghĩa bài toán (Problem Formulation)

### 2.1. Dữ liệu

Tại mỗi thời điểm (hoặc mỗi bước sampling), có vector quan sát đa biến:

```text
x_t = [vib_x(t), vib_y(t), temp_1(t), temp_2(t)]
```

Với dữ liệu run-to-failure, chuẩn hóa timeline theo TTF% để xác định các vùng (có thể dùng cho cả đánh giá lẫn phân tích delay):

- Healthy: 0–60% TTF (normal)
- Transition: 60–70% TTF (khó)
- Degrading/Fault: 70–100% TTF (abnormal)

### 2.2. Forecasting task (self-supervised)

Tạo cặp (X, Y) theo sliding window:

```text
X = [x_{t-N+1}, ..., x_t]         (lookback N)
Y = [x_{t+1}, ..., x_{t+K}]       (horizon K)
```

Mô hình học hàm dự báo:

```text
Y_hat = f_theta(X)
```

Không cần stage label cho training, chỉ cần chuỗi tín hiệu.

### 2.3. Anomaly score và detection

Định nghĩa prediction error làm anomaly score:

```text
e_t = error(Y, Y_hat)  (MSE/MAE/RMSE)
score_t = aggregate(e_t)  (mean theo bước và/hoặc theo kênh)
```

Tách score theo modality (khuyến nghị để phân tích):

```text
score_vib  = MSE(Y_vib,  Yhat_vib)
score_temp = MSE(Y_temp, Yhat_temp)
score_total = alpha * score_vib + beta * score_temp
```

Thresholding:

- 3-sigma trên score vùng train (Healthy): `thr = mean + 3*std`
- hoặc percentile (95/99) trên score vùng train

Phát hiện suy thoái:

```text
anomaly_t = (score_total > thr)
```

Đo “detection delay” theo TTF%: thời điểm đầu tiên anomaly kéo dài liên tục L bước sau mốc 60% TTF.

## 3. Phương pháp đề xuất (Proposed Method)

### 3.1. Kiến trúc tổng thể

Mục tiêu: vừa nắm pattern cục bộ (vibration), vừa nắm động học dài hạn (degradation dynamics).

Pipeline đề xuất:

1. Preprocess
2. Patching/CNN Tokenizer
3. Mamba Encoder
4. Forecast Head
5. Anomaly Scoring + Thresholding

### 3.2. Hai biến thể phương pháp (để giảm rủi ro)

Biến thể V1 (kế thừa bài gốc, dễ nối với paper cũ):

- Input: STFT log-spectrogram theo window (2 kênh vib) + temperature (raw/descriptor)
- CNN 2D encoder tạo embedding theo window
- Mamba học chuỗi embedding theo thời gian
- Forecast embedding hoặc forecast trực tiếp tín hiệu giảm chiều

Biến thể V2 (thuần time-series, đúng “forecasting” hơn):

- Input: chuỗi 4 kênh raw (vib_x, vib_y, temp1, temp2)
- Patching 1D + CNN 1D
- Mamba encoder
- Forecast head dự báo trực tiếp chuỗi tương lai 4 kênh

Khuyến nghị: làm V2 làm chính, V1 dùng như ablation hoặc hướng “tận dụng STFT” để nối với bài cũ.

## 4. Baselines và so sánh công bằng

Forecasting baselines (bắt buộc):

- LSTM forecasting (seq2seq hoặc encoder-decoder)
- TCN forecasting
- Transformer forecasting (attention-based)
- Mamba forecasting

Anomaly detection baselines (bắt buộc):

- USAD hoặc Autoencoder reconstruction-based (multivariate)
- (Optional) Anomaly Transformer

Baseline tham chiếu theo hướng classification (không ràng buộc phải trích dẫn bài three-stage của nhóm):

- Một baseline classification tiêu chuẩn cho bearing health stage (ví dụ STFT+CNN cho vibration, thêm temperature fusion ở late stage) để so sánh với hướng forecasting/anomaly.

Mục tiêu: chứng minh “forecasting anomaly score” phù hợp hơn classification, đặc biệt ở vùng transition (60–70% TTF).

## 5. Giao thức đánh giá (Evaluation Protocol)

Leakage-aware temporal split (biện minh từ nguyên tắc time-series evaluation, không cần dựa vào bài nội bộ):

- Train: 0–60% TTF
- Val: 60–70% TTF
- Test: 70–100% TTF

Metrics:

- Forecasting: MSE/MAE/RMSE
- Detection: AUC, Precision/Recall/F1, False alarm rate, Detection delay (theo TTF%)

Trọng tâm: báo cáo riêng cho vùng 60–70% TTF (early degradation).

## 6. Ablation (để “SCIE-ready”)

- Vib-only vs Vib+Temp
- Score: vib-only score vs fused score
- Threshold: 3-sigma vs percentile
- Lookback/horizon: (N, K) nhỏ → lớn
- Backbone: Mamba vs Transformer vs LSTM/TCN
- Tokenizer: có/không patching, patch size khác nhau

## 7. Research Gap (đưa vào Introduction)

```text
Most existing bearing diagnosis studies formulate the problem as supervised classification, where each window is assigned to a discrete health stage. However, degradation in run-to-failure settings evolves gradually, making the Healthy-to-Degrading boundary ambiguous and limiting early detection.

This motivates a self-supervised forecasting-based anomaly detection framework that learns normal temporal dynamics from early-life vibration–temperature signals and detects degradation via prediction-error-based anomaly scores. Meanwhile, long-sequence modeling remains challenging for high-rate vibration data; selective state space models such as Mamba provide an efficient alternative to attention-based Transformers for capturing long-range degradation dynamics.
```

## 8. Contributions (dự kiến)

```text
1) We propose a self-supervised forecasting-based anomaly detection framework for early bearing degradation detection in run-to-failure settings using vibration–temperature signals.
2) We design a long-sequence forecasting architecture built on a CNN/Patching tokenizer and a Mamba encoder to capture local vibration patterns and long-range degradation dynamics efficiently.
3) We define prediction-error-based anomaly scores with leakage-aware temporal evaluation and report detection delay and false alarm rates focused on the Healthy-to-Degrading transition.
4) We conduct extensive comparisons with forecasting and anomaly-detection baselines and provide ablation studies on modality fusion, thresholding, and sequence length settings.
```

## 9. Paper outline (đề cương)

1. Introduction
2. Related Work
3. Problem Formulation
4. Proposed Method
5. Experimental Setup
6. Results and Discussion
7. Ablation and Analysis
8. Conclusion and Future Work

## 10. Kế hoạch thực thi tối thiểu

1. Chốt data construction: N/K, stride, normalization train-only.
2. Implement baseline forecasting: LSTM, TCN, Transformer.
3. Implement proposed: CNN/Patching-Mamba forecasting.
4. Implement anomaly scoring + thresholding + metrics (delay/false alarm).
5. Chạy thí nghiệm core + ablation vib-only vs vib+temp.
6. Viết sections: Method, Experiments, Results, Ablation, Discussion.

## 11. Cách viết để “tránh phụ thuộc” bài three-stage chưa duyệt

Nguyên tắc trình bày:

1. Không gọi bài three-stage là “paper trước/previous paper (published)”.
2. Nếu cần nhắc, chỉ gọi là “baseline nội bộ” hoặc “một pipeline nhẹ đã thử nghiệm” và trình bày như một baseline trong Experiments.
3. Động lực khoa học phải bám literature: ambiguity ở transition, nhu cầu self-supervised, forecasting error làm anomaly score, long-sequence modeling.
4. Tất cả claims trong Introduction/Related Work phải dựa vào các công trình công bố (survey + anomaly detection + long sequence + multimodal).
