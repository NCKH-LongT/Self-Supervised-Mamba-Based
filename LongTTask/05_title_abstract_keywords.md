# Title, Abstract, Keywords (bản nháp cho bài mới)

Chủ đề: self-supervised forecasting-based anomaly detection cho **early bearing degradation** với **vibration–temperature** và **long-sequence modeling (CNN/Patching-Mamba)**. Bài viết độc lập, không dựa vào bài three-stage chưa duyệt.

## 1) Title (đề xuất 6 lựa chọn)

1. Self-Supervised Forecasting-Based Anomaly Detection for Early Bearing Degradation Using Vibration–Temperature Signals
2. Early Bearing Degradation Detection via Self-Supervised Multimodal Forecasting and Prediction-Error Anomaly Scoring
3. Long-Sequence Multimodal Forecasting with CNN/Patching-Mamba for Bearing Degradation Anomaly Detection
4. Prediction-Error Anomaly Scoring for Run-to-Failure Bearing Monitoring with Vibration–Temperature Fusion
5. Efficient Long-Sequence Forecasting for Bearing Degradation Detection: A CNN/Patching-Mamba Approach
6. Leakage-Aware Evaluation of Forecasting-Based Anomaly Detection for Early Bearing Degradation with Vibration–Temperature Signals

Khuyến nghị dùng Title #3 hoặc #2 (vừa có novelty “Mamba/long-sequence”, vừa có task “early degradation”).

## 2) Abstract (Structured)

### Background
Early bearing degradation in run-to-failure monitoring evolves gradually, making the boundary between normal and early-degrading behavior ambiguous and limiting the reliability of stage-based supervised classification, especially near transition regions.

### Objective
This study aims to detect early bearing degradation using a self-supervised forecasting-based anomaly detection framework built on multimodal vibration–temperature signals and efficient long-sequence modeling.

### Methods
We formulate bearing monitoring as a multivariate time-series forecasting task: a model is trained to predict future vibration–temperature observations from past sequences learned primarily from early-life (normal) data. Degradation is detected using prediction-error-based anomaly scores with practical thresholding strategies. To handle long, high-rate sensor sequences efficiently, we design a CNN/Patching tokenizer followed by a Mamba encoder to capture local vibration patterns and long-range degradation dynamics. Evaluation follows a leakage-aware temporal protocol aligned with the normalized time-to-failure axis and reports both anomaly detection performance and detection delay around the normal-to-degrading transition.

### Results
Experiments demonstrate that forecasting-based anomaly scoring improves sensitivity to early degradation compared with classification-style baselines, while the proposed CNN/Patching-Mamba architecture provides competitive detection performance with improved efficiency for long input sequences. Ablation studies further quantify the contribution of temperature fusion, sequence length, backbone choice, and thresholding method.

### Conclusions
Self-supervised multimodal forecasting provides a practical and label-efficient approach for early bearing degradation detection under run-to-failure settings, and selective state space models offer an effective backbone for long sensor sequences.

## 3) Abstract (Plain, 150–220 words)

Run-to-failure bearing degradation typically evolves gradually, making the boundary between normal and early-degrading behavior ambiguous and limiting the effectiveness of stage-based supervised classification, particularly near transition regions. This paper proposes a self-supervised forecasting-based anomaly detection framework for early bearing degradation detection using multimodal vibration–temperature signals. The model is trained to forecast future observations from past sequences learned primarily from early-life normal data. Degradation is then detected using prediction-error-based anomaly scores with practical thresholding, enabling label-efficient monitoring without requiring precise health-stage annotations. To efficiently capture both local vibration patterns and long-range degradation dynamics in long sensor sequences, we design a CNN/Patching tokenizer and a Mamba encoder for long-sequence multimodal forecasting. We evaluate the proposed approach under a leakage-aware, temporal protocol aligned with the normalized time-to-failure axis, and report detection performance, false alarm rate, and detection delay with a focus on the normal-to-degrading transition. Results and ablations show the benefits of forecasting-based anomaly scoring, temperature fusion, and selective state space modeling for early degradation detection in run-to-failure settings.

## 4) Keywords (8–12 từ khóa)

- bearing degradation
- run-to-failure
- early degradation detection
- anomaly detection
- self-supervised learning
- time-series forecasting
- prediction error
- multimodal fusion
- vibration–temperature
- long-sequence modeling
- Mamba
- leakage-aware evaluation

## 5) Dataset (chọn dataset và lý do)

### Dataset chính (khuyến nghị)

**Run-to-failure bearing vibration–temperature dataset (single-run)** có đồng bộ **vibration 2 trục** và **temperature 2 kênh** theo thời gian.

Lý do chọn:

- Phù hợp trực tiếp với bài toán: run-to-failure, degradation diễn ra dần.
- Có đủ 2 modality (vibration + temperature) để làm fusion và phân tích ablation.
- Cho phép dựng giao thức **TTF-aligned temporal split** để tránh leakage (split theo thời gian, không random window).

Ghi chú trình bày để bài độc lập:

- Chỉ mô tả dataset theo bài báo/dataset paper công bố (tên nguồn + năm + DOI nếu có).
- Không cần nhắc đến bất kỳ “paper nội bộ” hay bản thảo chưa duyệt nào.

### Dataset phụ (tuỳ chọn, nếu cần tăng độ mạnh bài Q3)

Nếu đủ thời gian, thêm external validation:

- **NASA IMS Bearing Dataset** (run-to-failure)
- **XJTU-SY Bearing Dataset** (multi-run bearing degradation)

Mục tiêu: chứng minh framework hoạt động ổn trên dataset khác (không overfit một run).

## 6) Method (mô tả phương pháp đề xuất)

### 6.1. Problem setup

Ta coi tín hiệu là chuỗi đa biến:

```text
x_t = [vib_x(t), vib_y(t), temp_1(t), temp_2(t)]
```

Tạo mẫu forecasting theo lookback/horizon:

```text
X_t = [x_{t-N+1}, ..., x_t]      (lookback N)
Y_t = [x_{t+1}, ..., x_{t+K}]    (horizon K)
```

Mục tiêu học self-supervised:

```text
Y_hat = f_theta(X)
```

### 6.2. Data construction (khuyến nghị thông số tối thiểu)

1. Đồng bộ kênh vibration và temperature (nếu khác sampling rate thì resample).
2. Chuẩn hoá theo thống kê **train-only** để tránh leakage:
   - Global z-score theo từng kênh dựa trên tập train.
3. Tạo sliding windows theo stride s (khuyến nghị s nhỏ hơn N để đủ mẫu).

Khuyến nghị cấu hình để chạy ổn trước:

- Config A: `N=1024`, `K=128`
- Config B: `N=2048`, `K=256`
- Config C: `N=4096`, `K=256` (để chứng minh long-sequence)

### 6.3. Architecture (CNN/Patching-Mamba forecaster)

Pipeline đề xuất:

1. **Patching/CNN Tokenizer**
   - Chia chuỗi input dài thành patch (kích thước P).
   - Dùng Conv1D (hoặc MLP nhẹ) để biến mỗi patch thành embedding token.

2. **Mamba Encoder**
   - Nhận chuỗi token và học phụ thuộc dài hạn với chi phí tuyến tính theo độ dài chuỗi.

3. **Forecast Head**
   - Dự báo K bước tương lai cho 4 kênh (multivariate forecasting).

Mục tiêu thiết kế:

- CNN/Patching bắt pattern cục bộ của vibration.
- Mamba bắt degradation dynamics dài hạn và lọc nhiễu theo ngữ cảnh.
- Forecast head đủ đơn giản để không “ăn” hết novelty.

### 6.4. Training objective

Loss forecasting (mặc định):

```text
L = MSE(Y_true, Y_pred)
```

Tuỳ chọn:

- Weighted MSE theo modality để ổn định (ví dụ ưu tiên vibration nhưng vẫn giữ temperature).
- Huber loss để giảm ảnh hưởng outlier.

### 6.5. Anomaly scoring và thresholding

Anomaly score dựa trên prediction error:

```text
score_t = mean_{k=1..K} MSE(y_{t+k}, yhat_{t+k})
```

Tách modality để phân tích:

```text
score_vib, score_temp, score_total = alpha*score_vib + beta*score_temp
```

Thresholding (dựa trên vùng train/healthy):

- 3-sigma: `thr = mean(score_train) + 3*std(score_train)`
- Percentile: `thr = p95(score_train)` hoặc `p99(score_train)`

Giảm false alarm bằng “persistence rule”:

- Chỉ báo động nếu `score > thr` liên tục L bước (ví dụ L=3 hoặc L=5).

### 6.6. Leakage-aware evaluation protocol

Temporal split theo TTF% (contiguous split):

- Train: 0–60% TTF (normal)
- Val: 60–70% TTF (transition)
- Test: 70–100% TTF (degrading+fault)

Lý do: hạn chế window overlap leakage và phản ánh deployment (train trên early-life, test trên later-life).

### 6.7. Metrics và báo cáo (để hợp bài Q3)

Forecasting metrics:

- MSE/MAE/RMSE trên train/val/test

Detection metrics:

- AUC (Healthy vs {Degrading+Fault})
- Precision/Recall/F1 (early detection)
- False alarm rate (trên vùng Healthy)
- Detection delay theo TTF% (tập trung vùng 60–70%)

### 6.8. Baselines tối thiểu

Forecasting baselines:

- LSTM
- TCN
- Transformer

Anomaly detection baselines:

- USAD (reconstruction-based)
- (Optional) Anomaly Transformer

Multimodal ablation:

- Vib-only vs Vib+Temp (để chứng minh giá trị temperature).
