# Template bài báo Q4/Q3  
## Chủ đề: Self-Supervised Forecasting-Based Anomaly Detection for Bearing Degradation Using Vibration–Temperature Fusion and Mamba Networks

---

## 1. Định hướng bài báo

Hướng bài báo nên phát triển từ bài đầu tiên về **Three-Stage Bearing Health Classification** sang hướng mới:

> **Self-Supervised Forecasting-Based Anomaly Detection for Bearing Degradation**

Ý tưởng chính:

- Bài đầu tiên phân loại trạng thái ổ bi thành:
  - Healthy
  - Degrading
  - Fault
- Bài mới không trực tiếp bắt mô hình phân loại nhãn ngay từ đầu.
- Thay vào đó, mô hình học quy luật vận hành bình thường của ổ bi.
- Mô hình dự báo dữ liệu tương lai từ dữ liệu quá khứ.
- Khi ổ bi bắt đầu suy thoái, dữ liệu thật sẽ lệch khỏi dữ liệu dự báo.
- Sai số dự báo tăng lên và được dùng làm **anomaly score**.
- Anomaly score được dùng để phát hiện giai đoạn Degrading hoặc Fault.

Ví dụ:

```text
Input: 1024 điểm dữ liệu quá khứ gồm vibration_x, vibration_y, temp_1, temp_2
Output: 128 điểm dữ liệu tương lai

Nếu mô hình dự báo đúng gần với thực tế → hệ thống có khả năng vẫn Healthy
Nếu mô hình dự báo lệch nhiều → có khả năng bắt đầu Degrading hoặc Fault
```

---

## 2. Title gợi ý

### Title chính

```text
Self-Supervised Forecasting-Based Anomaly Detection for Bearing Degradation Using Vibration–Temperature Fusion and Mamba Networks
```

### Title ngắn hơn

```text
Mamba-Based Self-Supervised Forecasting for Bearing Degradation Detection
```

### Title mềm hơn cho Q4/Q3

```text
A Forecasting-Based Anomaly Detection Framework for Bearing Health Monitoring Using Vibration and Temperature Signals
```

### Title có tên mô hình

```text
VT-MambaAD: A Vibration–Temperature Mamba Framework for Forecasting-Based Bearing Anomaly Detection
```

---

## 3. Keywords

```text
Bearing health monitoring
Self-supervised learning
Forecasting
Anomaly detection
Mamba
Vibration-temperature fusion
Run-to-failure prognostics
Predictive maintenance
```

---

## 4. Abstract

### Mục tiêu của Abstract

Tóm tắt bài báo trong khoảng 180–250 từ.

Abstract nên có 5 ý:

1. Bối cảnh: bearing fault diagnosis/prognostics quan trọng.
2. Vấn đề: classification cần nhãn rõ, trong khi suy thoái diễn ra dần dần.
3. Giải pháp: self-supervised forecasting-based anomaly detection.
4. Phương pháp: CNN/Patching + Mamba + vibration–temperature fusion.
5. Kết quả: nêu metric chính sau khi có kết quả.

### Abstract template

```text
Bearing health monitoring is essential for preventing unexpected machine failures in industrial systems. Most existing approaches formulate bearing diagnosis as a supervised classification problem, where each signal window is assigned to a predefined health stage such as Healthy, Degrading, or Fault. However, in run-to-failure scenarios, degradation evolves gradually, making stage boundaries ambiguous and expensive to label.

This paper proposes a self-supervised forecasting-based anomaly detection framework for bearing degradation detection. Instead of directly predicting health labels, the proposed model learns normal temporal dynamics from early-life data and forecasts future vibration and temperature signals from historical observations. Prediction errors between the forecasted and observed signals are then used to compute anomaly scores for identifying degradation and fault regions.

The framework integrates a CNN/Patching module for local signal representation, a Mamba-based sequence encoder for long-range temporal modeling, and a vibration–temperature fusion strategy to exploit complementary mechanical and thermal degradation cues. Experiments are conducted under a temporal leakage-aware run-to-failure evaluation protocol. The proposed method is compared with conventional forecasting baselines including LSTM, TCN, and Transformer models, as well as classification-based baselines.

Experimental results show that the proposed method achieves [fill result] in terms of anomaly detection performance, detection delay, and computational efficiency, suggesting its potential for practical bearing health monitoring.
```

---

# 5. Cấu trúc bài báo hoàn chỉnh

```text
Title

Abstract

Keywords

1. Introduction
   1.1 Background and motivation
   1.2 Limitations of supervised bearing health classification
   1.3 Forecasting-based anomaly detection motivation
   1.4 Contributions

2. Related Work
   2.1 Bearing fault diagnosis
   2.2 Run-to-failure prognostics
   2.3 Forecasting-based anomaly detection
   2.4 Long-sequence models for time-series analysis

3. Materials and Methods
   3.1 Dataset description
   3.2 Problem formulation
   3.3 Forecasting data construction
   3.4 Temporal split protocol
   3.5 Normalization strategy

4. Proposed Method
   4.1 Overall architecture
   4.2 CNN/Patching block
   4.3 Mamba encoder
   4.4 Vibration-temperature fusion
   4.5 Forecasting head
   4.6 Training objective
   4.7 Anomaly score
   4.8 Thresholding strategy

5. Experiments
   5.1 Experimental setup
   5.2 Baselines
   5.3 Evaluation metrics
   5.4 Main results

6. Ablation Study
   6.1 Effect of vibration-temperature fusion
   6.2 Effect of Mamba encoder
   6.3 Effect of patching
   6.4 Effect of lookback and forecasting horizon
   6.5 Effect of thresholding method

7. Discussion
   7.1 Interpretation of anomaly score
   7.2 Role of temperature in degradation detection
   7.3 Computational efficiency
   7.4 Limitations

8. Conclusion

References
```

---

# 6. Section 1 — Introduction

## 6.1. Mục tiêu

Phần Introduction phải trả lời 4 câu:

1. Vì sao bearing health monitoring quan trọng?
2. Vì sao supervised classification chưa đủ?
3. Vì sao forecasting/anomaly detection phù hợp hơn?
4. Bài này đóng góp gì?

## 6.2. Cấu trúc đề xuất

### Đoạn 1: Bối cảnh

Viết về:

- Bearing là thành phần quan trọng trong máy quay, động cơ, hệ thống công nghiệp.
- Hỏng bearing có thể gây downtime, chi phí bảo trì cao.
- Vibration thường được dùng vì phản ánh dao động cơ học.
- Temperature bổ sung thông tin về ma sát, tải và nhiệt tích lũy.

### Đoạn 2: Vấn đề của classification

Nêu rõ:

- Nhiều nghiên cứu chia tín hiệu thành Healthy/Degrading/Fault.
- Cách này cần nhãn rõ.
- Trong run-to-failure, ranh giới Healthy–Degrading không rõ ràng.
- Random split dễ gây leakage nếu các window gần nhau xuất hiện ở cả train/test.

### Đoạn 3: Động lực của forecasting-based anomaly detection

Ý chính:

- Thay vì học nhãn, mô hình học hành vi bình thường.
- Khi bearing suy thoái, dữ liệu thật sẽ lệch khỏi dữ liệu dự báo.
- Sai số dự báo tăng lên có thể dùng làm anomaly score.
- Cách này phù hợp với self-supervised learning vì không cần nhãn trực tiếp cho từng window.

### Đoạn 4: Vì sao dùng Mamba

Nêu vừa phải, không overclaim:

- Vibration là chuỗi dài, tần số cao.
- Temperature là tín hiệu chậm, có xu hướng dài hạn.
- Mamba phù hợp để thử nghiệm vì có khả năng mô hình hóa long sequence hiệu quả hơn attention-based Transformer trong một số ngữ cảnh.
- Bài này không cần tuyên bố Mamba “luôn tốt hơn”, chỉ nên nói: **investigate the suitability of Mamba**.

## 6.3. Contributions

```text
The main contributions of this study are as follows:

1. We propose a self-supervised forecasting-based anomaly detection framework for bearing degradation detection under a run-to-failure setting.

2. We design a CNN/Patching-Mamba architecture to capture local vibration patterns and long-range degradation dynamics from multivariate time-series signals.

3. We investigate vibration–temperature fusion for anomaly-score-based early degradation detection.

4. We conduct a temporal leakage-aware evaluation with baseline comparison and ablation studies on input modality, sequence length, forecasting horizon, and thresholding strategy.
```

---

# 7. Section 2 — Related Work

## 7.1. Mục tiêu

Phần Related Work nên chia thành 4 nhóm:

1. Bearing fault diagnosis
2. Run-to-failure prognostics
3. Forecasting-based anomaly detection
4. Long-sequence models: LSTM, TCN, Transformer, Mamba

Với mức Q4/Q3, không cần review quá sâu, nhưng mỗi nhóm nên có 1–2 đoạn.

---

## 7.2. Bearing Fault Diagnosis

### Nội dung cần viết

- Các phương pháp truyền thống:
  - handcrafted features
  - statistical features
  - frequency-domain features
  - FFT
  - STFT
  - wavelet
- Các phương pháp deep learning:
  - CNN
  - LSTM
  - Transformer
  - STFT-CNN
- Tín hiệu vibration thường là nguồn chính.
- Temperature ít được khai thác hơn nhưng có thể bổ sung thông tin về ma sát/nhiệt.

### Câu chốt gợi ý

```text
Although supervised bearing fault diagnosis has achieved promising results, its dependence on predefined labels limits its applicability in gradual degradation scenarios.
```

---

## 7.3. Run-to-Failure Prognostics

### Nội dung cần viết

- Run-to-failure theo dõi toàn bộ vòng đời của bearing.
- Thường liên quan đến:
  - degradation trend
  - remaining useful life
  - time-to-failure percentage
- Khó khăn:
  - suy thoái không xảy ra đột ngột
  - trạng thái Healthy–Degrading chuyển tiếp dần
  - nhãn giai đoạn có thể mang tính heuristic

### Câu chốt gợi ý

```text
Run-to-failure data provide a more realistic setting for studying degradation, but they also introduce ambiguity in defining health-stage boundaries.
```

---

## 7.4. Forecasting-Based Anomaly Detection

### Nội dung cần viết

- Forecasting học từ quá khứ để dự đoán tương lai.
- Khi dữ liệu thật lệch khỏi dự báo, prediction error tăng.
- Error có thể dùng làm anomaly score.
- Các threshold có thể dùng:
  - 3-sigma
  - percentile
  - GMM

### Câu chốt gợi ý

```text
Forecasting-based anomaly detection provides an alternative to direct classification by detecting deviations from learned normal temporal dynamics.
```

---

## 7.5. Long-Sequence Models: LSTM, TCN, Transformer, Mamba

### Nội dung cần viết

- LSTM/GRU xử lý chuỗi nhưng khó với chuỗi rất dài.
- TCN hiệu quả với pattern cục bộ và receptive field.
- Transformer mạnh nhưng attention có chi phí cao với chuỗi dài.
- Mamba là hướng mới đáng khảo sát cho long time-series.

### Câu chốt gợi ý

```text
Despite the increasing interest in long-sequence models, the role of Mamba-based forecasting for bearing degradation detection remains underexplored.
```

---

# 8. Section 3 — Materials and Methods

---

## 8.1. Dataset Description

### Mục tiêu

Mô tả:

- Dataset name
- Loại thí nghiệm
- Sensor
- Số kênh
- Sampling rate
- Run-to-failure timeline
- Cách định nghĩa Healthy/Degrading/Fault nếu dùng để đánh giá

### Template viết

```text
The dataset used in this study consists of synchronized vibration and temperature signals collected from a ball bearing run-to-failure experiment. Vibration signals are recorded along two axes, while temperature is measured from two channels. The full lifetime of the bearing is normalized into a time-to-failure percentage scale, where early-life, transition, and late-life regions are associated with Healthy, Degrading, and Fault stages, respectively.
```

### Hình nên có

```text
Figure 1. Bearing run-to-failure timeline

0% -------------------- 60% -------------------- 90% -------- 100%
Healthy                 Degrading                Fault
```

---

## 8.2. Problem Formulation

### Mục tiêu

Chuyển bài toán từ classification sang forecasting.

### Bài cũ

```text
Input: signal window
Output: Healthy / Degrading / Fault
```

### Bài mới

```text
Input: past sequence
Output: future sequence
```

### Template viết

```text
Given a multivariate time-series sequence X = {x_t, x_{t+1}, ..., x_{t+N-1}}, where each time step contains vibration and temperature measurements, the objective is to forecast the future sequence Y = {x_{t+N}, ..., x_{t+N+K-1}}. The model is trained in a self-supervised manner using historical observations as inputs and future observations as prediction targets.
```

### Ký hiệu

```text
X_t ∈ R^{N × C}
Y_t ∈ R^{K × C}
```

Trong đó:

- `N`: lookback length
- `K`: forecast horizon
- `C`: số kênh tín hiệu
- Ví dụ:
  - `vibration_x`
  - `vibration_y`
  - `temperature_1`
  - `temperature_2`

---

## 8.3. Forecasting Data Construction

### Mục tiêu

Mô tả cách tạo sample bằng sliding window.

### Template

```text
A sliding-window strategy is used to construct forecasting samples. For each timestamp t, the previous N observations are used as the input sequence, and the following K observations are used as the forecasting target. This construction allows the model to learn temporal dependencies without requiring explicit health-stage labels during training.
```

### Bảng cấu hình nên đưa vào

| Config | Lookback N | Horizon K | Purpose |
|---|---:|---:|---|
| A | 512 | 64 | Lightweight initial setting |
| B | 1024 | 128 | Balanced setting |
| C | 2048 | 256 | Longer temporal context |
| D | 4096 | 256 | Long-sequence evaluation |

### Khuyến nghị

- Chạy chính với `N=1024, K=128`.
- Chạy ablation thêm `N=512, K=64` và `N=2048, K=256`.
- Không cần quá nhiều config nếu thời gian hạn chế.

---

## 8.4. Temporal Split Protocol

### Mục tiêu

Chứng minh bài có đánh giá nghiêm túc, tránh data leakage.

### Không nên dùng

```text
Random split theo window
```

Vì các window gần nhau có thể xuất hiện ở cả train/test, làm kết quả bị lạc quan.

### Nên dùng

```text
Train: 0–60% TTF
Validation: 60–70% TTF
Test: 70–100% TTF
```

### Template viết

```text
To avoid temporal leakage, we adopt a contiguous temporal split along the normalized lifetime axis. The model is trained on early-life data, validated on the transition region, and tested on later-life degradation and fault regions. This protocol better approximates deployment conditions, where future degradation patterns should not be visible during training.
```

### Bảng

| Split | TTF range | Purpose |
|---|---:|---|
| Train | 0–60% | Learn normal/early-life dynamics |
| Validation | 60–70% | Tune threshold and hyperparameters |
| Test | 70–100% | Evaluate degradation/fault detection |

---

## 8.5. Normalization Strategy

### Mục tiêu

Mô tả chuẩn hóa dữ liệu đúng nguyên tắc.

### Cấu hình chính nên dùng

```text
Global train-only z-score normalization
```

### Công thức

```text
x_norm = (x - mean_train) / std_train
```

### Template viết

```text
All input channels are normalized using statistics computed only from the training split. This prevents information from validation or test regions from leaking into the training process. We primarily use global z-score normalization and compare it with alternative strategies in the ablation study.
```

### Ablation normalization

| Strategy | Purpose | Risk |
|---|---|---|
| Train-only global z-score | Main setting | Stable, deployment-like |
| Per-window z-score | Reduce amplitude variation | May remove anomaly amplitude |
| Robust scaling | Handle outliers | May need tuning |

### Lưu ý quan trọng

Với anomaly detection, không nên dùng per-window z-score làm cấu hình chính, vì nó có thể làm mất tín hiệu tăng biên độ khi lỗi xuất hiện.

---

# 9. Section 4 — Proposed Method

---

## 9.1. Overall Architecture

### Mục tiêu

Mô tả pipeline tổng thể.

### Sơ đồ

```text
Raw vibration + temperature
        ↓
Train-only normalization
        ↓
CNN/Patching Block
        ↓
Mamba Encoder
        ↓
Vibration–Temperature Fusion
        ↓
Forecast Head
        ↓
Predicted future sequence
        ↓
Prediction Error
        ↓
Anomaly Score
        ↓
Healthy / Degrading / Fault decision
```

### Template viết

```text
The proposed framework consists of four main components: a CNN/Patching block, a Mamba-based temporal encoder, a vibration–temperature fusion module, and a forecasting head. The CNN/Patching block extracts local temporal patterns and reduces the length of the input sequence. The Mamba encoder then models long-range temporal dependencies among compact patch tokens. The fusion module combines mechanical and thermal degradation representations, and the forecasting head predicts future multivariate signals. Finally, prediction errors are converted into anomaly scores for degradation detection.
```

---

## 9.2. CNN/Patching Block

### Mục tiêu

Giải thích vì sao cần patching.

Ý chính:

- Vibration dài và dày.
- Đưa raw sequence trực tiếp vào model sẽ tốn bộ nhớ.
- Patching giảm chiều dài chuỗi.
- CNN giữ pattern cục bộ.

### Ví dụ

```text
Input length = 4096
Patch size = 16
Number of patches = 256
```

### Template viết

```text
To reduce the computational cost of long vibration sequences, the input sequence is divided into non-overlapping or partially overlapping temporal patches. Each patch is processed using local convolutional filters to extract short-term vibration patterns. The resulting patch embeddings form a compact token sequence that is passed to the Mamba encoder.
```

---

## 9.3. Mamba Encoder

### Mục tiêu

Giải thích vai trò của Mamba.

### Không nên viết

```text
Mamba is better than Transformer.
```

### Nên viết

```text
Mamba is investigated as an efficient long-sequence modeling component.
```

### Template

```text
The Mamba encoder is used to model temporal dependencies among patch-level representations. Compared with conventional recurrent models, Mamba provides a sequence modeling mechanism that is suitable for long-range temporal dynamics. In this study, we investigate whether Mamba can improve forecasting-based degradation detection when applied to multivariate vibration–temperature sequences.
```

### Hyperparameter đề xuất

| Parameter | Values |
|---|---|
| Number of Mamba layers | 2, 4 |
| Hidden dimension | 64, 128, 256 |
| Dropout | 0.1 |
| Batch size | tùy GPU |
| Optimizer | AdamW |
| Loss | MSE |

---

## 9.4. Vibration–Temperature Fusion

### Mục tiêu

Làm rõ cách kết hợp vibration và temperature.

### Kiến trúc khuyến nghị

```text
Vibration branch:
[vib_x, vib_y] → CNN/Patching → Mamba → h_v

Temperature branch:
[temp_1, temp_2] → MLP/TCN → h_t

Fusion:
concat(h_v, h_t) → Forecast Head
```

### Template

```text
Because vibration and temperature signals represent different physical characteristics of bearing degradation, we process them using separate branches before fusion. The vibration branch captures high-frequency mechanical patterns, while the temperature branch captures slower thermal trends. Their latent representations are concatenated and passed to the forecasting head.
```

### Ablation cần có

| Variant | Purpose |
|---|---|
| Vibration-only | Kiểm tra chỉ dùng tín hiệu cơ học |
| Temperature-only | Kiểm tra vai trò nhiệt độ |
| Vibration + Temperature | Kiểm tra fusion |
| Early fusion | Gộp 4 kênh từ đầu |
| Late fusion | Tách nhánh rồi fusion |

---

## 9.5. Forecasting Head

### Mục tiêu

Dự báo K bước tương lai.

### Template

```text
The forecasting head maps the fused temporal representation into a future multivariate sequence. Given the encoded representation, a lightweight MLP is used to predict the next K time steps for all selected channels.
```

### Output

```text
Y_pred ∈ R^{K × C}
```

Nếu dự báo 4 kênh:

```text
C = 4
Output = [K, 4]
```

### Khuyến nghị

- Bản chính: dự báo cả vibration + temperature.
- Ablation: dự báo vibration-only.

---

## 9.6. Training Objective

### Mục tiêu

Mô tả loss.

### Công thức

```text
L = MSE(Y_true, Y_pred)
```

### Template

```text
The model is trained using mean squared error between the predicted future sequence and the observed future sequence. Since the target sequence is generated directly from the raw time series, no manual health-stage label is required during training.
```

---

## 9.7. Anomaly Score

### Mục tiêu

Định nghĩa anomaly score.

### Công thức đơn giản

```text
Score_t = MSE(Y_true, Y_pred)
```

### Công thức multimodal

```text
score_total = α × score_vib + β × score_temp
```

Ví dụ:

```text
score_total = 0.8 × score_vib + 0.2 × score_temp
```

### Template

```text
After forecasting, the prediction error is computed between the predicted and observed future sequences. This error is used as the anomaly score. A higher anomaly score indicates that the observed signal deviates from the learned normal temporal dynamics, suggesting potential degradation or fault.
```

---

## 9.8. Thresholding Strategy

### Mục tiêu

Chuyển anomaly score thành cảnh báo.

### Main threshold

```text
threshold = mean_healthy + 3 × std_healthy
```

### Ablation threshold

| Threshold | Vai trò |
|---|---|
| 3-sigma | Dễ giải thích, phù hợp Q3/Q4 |
| 95th percentile | Nhạy hơn |
| 99th percentile | Bảo thủ hơn |
| GMM | Nếu muốn chia score thành Normal/Degrading/Fault |

### Template

```text
The decision threshold is estimated from the anomaly scores of the training split. In the main experiment, we use a 3-sigma threshold, defined as the mean training anomaly score plus three standard deviations. Percentile-based and GMM-based thresholds are further evaluated in the ablation study.
```

---

# 10. Section 5 — Experiments

---

## 10.1. Experimental Setup

### Cần mô tả

- Dataset
- Split
- Lookback/horizon
- Model configs
- Optimizer
- Batch size
- Epoch
- Hardware
- Repeated runs nếu có

### Template

```text
All models are trained using the same temporal split and forecasting configuration. Unless otherwise specified, the lookback length is set to N = 1024 and the forecasting horizon is set to K = 128. AdamW is used as the optimizer, and MSE is used as the forecasting loss. Hyperparameters are selected based on validation performance.
```

---

## 10.2. Baselines

### Forecasting baselines

| Model | Lý do chọn |
|---|---|
| LSTM | Baseline chuỗi thời gian cổ điển |
| TCN | Mạnh với pattern cục bộ |
| Transformer | Attention-based long sequence baseline |
| Mamba | Long-sequence model chính |
| Proposed Fusion Mamba | Mô hình đề xuất |

### Classification baselines nếu còn thời gian

| Model | Lý do |
|---|---|
| STFT-CNN vibration-only | Kế thừa bài đầu tiên |
| STFT-CNN + temperature | So với hướng classification cũ |
| SVM handcrafted features | Baseline truyền thống |

### Tối thiểu cho Q4/Q3

```text
LSTM, TCN, Transformer, Mamba, Proposed Fusion Mamba
```

---

## 10.3. Evaluation Metrics

### Forecasting metrics

| Metric | Ý nghĩa |
|---|---|
| MSE | Sai số chính, dùng tạo anomaly score |
| MAE | Ít nhạy với outlier |
| RMSE | Dễ diễn giải hơn MSE |

### Detection metrics

| Metric | Ý nghĩa |
|---|---|
| Precision | Cảnh báo đúng bao nhiêu |
| Recall | Phát hiện được bao nhiêu suy thoái |
| F1-score | Cân bằng precision/recall |
| AUC | Khả năng phân biệt normal/anomaly |
| False alarm rate | Báo động giả |
| Detection delay | Phát hiện sớm hay muộn |

### Template viết

```text
The evaluation is conducted at two levels. First, forecasting performance is measured using MSE, MAE, and RMSE. Second, anomaly detection performance is evaluated using Precision, Recall, F1-score, AUC, false alarm rate, and detection delay.
```

---

## 10.4. Main Results

### Bảng chính

| Method | Forecast MSE | MAE | AUC | F1 Degrading | F1 Fault | Detection Delay | Runtime |
|---|---:|---:|---:|---:|---:|---:|---:|
| LSTM |  |  |  |  |  |  |  |
| TCN |  |  |  |  |  |  |  |
| Transformer |  |  |  |  |  |  |  |
| Mamba |  |  |  |  |  |  |  |
| Proposed Fusion Mamba |  |  |  |  |  |  |  |

### Cách phân tích nếu kết quả tốt

```text
The proposed Fusion Mamba achieves the best overall detection performance, with higher AUC and F1-score than recurrent, convolutional, and attention-based baselines. This suggests that combining local patch-level representations with long-range temporal modeling is beneficial for forecasting-based degradation detection.
```

### Cách phân tích nếu Mamba không thắng rõ

```text
Although Mamba and Transformer achieve comparable detection performance, Mamba requires lower runtime and memory usage, indicating its potential advantage for efficient long-sequence bearing monitoring.
```

---

# 11. Section 6 — Ablation Study

Phần này rất quan trọng để bài nhìn “đủ nghiên cứu” ở Q3/Q4.

---

## 11.1. Effect of Temperature Fusion

| Model | AUC | F1 Degrading | F1 Fault | Detection Delay |
|---|---:|---:|---:|---:|
| Vibration-only |  |  |  |  |
| Temperature-only |  |  |  |  |
| Vibration + Temperature |  |  |  |  |

### Câu phân tích

```text
The improvement from vibration-only to vibration–temperature fusion indicates that thermal trends provide complementary degradation information, especially when mechanical vibration patterns become unstable near the degradation stage.
```

---

## 11.2. Effect of Mamba Encoder

| Encoder | MSE | AUC | F1 | Runtime |
|---|---:|---:|---:|---:|
| LSTM |  |  |  |  |
| TCN |  |  |  |  |
| Transformer |  |  |  |  |
| Mamba |  |  |  |  |

### Câu phân tích

```text
The Mamba encoder achieves competitive or better performance than conventional sequence models, suggesting that long-range temporal modeling is useful for capturing gradual degradation dynamics.
```

---

## 11.3. Effect of Patching

| Variant | Sequence Length | GPU Memory | AUC | F1 |
|---|---:|---:|---:|---:|
| Without patching | 4096 |  |  |  |
| With patching | 256 tokens |  |  |  |

### Câu phân tích

```text
Patching reduces the effective sequence length and computational cost while preserving local temporal patterns, leading to more efficient training and inference.
```

---

## 11.4. Effect of Lookback and Horizon

| Lookback N | Horizon K | MSE | AUC | Detection Delay |
|---:|---:|---:|---:|---:|
| 512 | 64 |  |  |  |
| 1024 | 128 |  |  |  |
| 2048 | 256 |  |  |  |
| 4096 | 256 |  |  |  |

### Câu phân tích

```text
Longer lookback windows provide richer temporal context for degradation modeling, but excessively long sequences may increase computational cost without proportional performance gains.
```

---

## 11.5. Effect of Thresholding Method

| Threshold | Precision | Recall | F1 | False Alarm Rate |
|---|---:|---:|---:|---:|
| 3-sigma |  |  |  |  |
| 95th percentile |  |  |  |  |
| 99th percentile |  |  |  |  |
| GMM |  |  |  |  |

### Câu phân tích

```text
The 3-sigma threshold provides a simple and interpretable decision rule, while percentile-based thresholds offer a trade-off between sensitivity and false alarm rate.
```

---

# 12. Section 7 — Discussion

---

## 12.1. Why Forecasting-Based Detection Works

### Ý chính

- Model học normal pattern.
- Khi bearing degradation xuất hiện, prediction error tăng.
- Cách này phù hợp khi nhãn Degrading không rõ.

### Template

```text
The forecasting-based framework is effective because it does not require the model to learn hard health-stage boundaries. Instead, it learns normal temporal dynamics and identifies degradation through deviations from predicted behavior.
```

---

## 12.2. Role of Temperature

### Ý chính

- Vibration phản ánh cơ học.
- Temperature phản ánh ma sát/nhiệt tích lũy.
- Temperature có thể giúp score ổn định hơn.

### Template

```text
Temperature signals provide complementary information to vibration. While vibration captures high-frequency mechanical changes, temperature reflects slower thermal trends related to friction and load accumulation.
```

---

## 12.3. Why Mamba Is Useful

### Ý chính

- Mamba có thể học chuỗi dài.
- Patching giúp giảm chi phí.
- Kết hợp CNN/Patching + Mamba hợp lý cho vibration time-series.

### Template

```text
The combination of CNN/Patching and Mamba allows the model to capture both local vibration patterns and long-range degradation dynamics. This is particularly useful in run-to-failure scenarios where degradation evolves gradually over time.
```

---

## 12.4. Limitations

### Nên nêu 4 hạn chế

1. Chỉ dùng một dataset chính.
2. Threshold còn đơn giản.
3. Nhãn Healthy/Degrading/Fault theo TTF% có thể chưa hoàn toàn chính xác.
4. Chưa kiểm tra real-time deployment thật.

### Template

```text
This study has several limitations. First, the experiments are conducted mainly on a single run-to-failure dataset, which may limit generalizability. Second, the health-stage boundaries are defined based on normalized lifetime percentages, which may not fully reflect physical degradation transitions. Third, the thresholding strategy remains relatively simple. Future work should validate the framework on additional bearing datasets and investigate adaptive thresholding strategies.
```

---

# 13. Section 8 — Conclusion

## Template

```text
This paper presented a self-supervised forecasting-based anomaly detection framework for bearing degradation detection. By forecasting future vibration and temperature signals and using prediction errors as anomaly scores, the proposed method avoids direct dependence on manually assigned health-stage labels. The framework combines CNN/Patching, Mamba-based temporal modeling, and vibration–temperature fusion to capture both local signal patterns and long-range degradation dynamics.

Experimental results under a temporal leakage-aware run-to-failure protocol show that the proposed method achieves competitive anomaly detection performance compared with conventional forecasting baselines. The ablation studies further demonstrate the contribution of temperature fusion, patching, and long-sequence modeling. Future work will extend the framework to additional run-to-failure datasets and explore adaptive thresholding for real-time industrial deployment.
```

---

# 14. Research Questions

Có thể dùng 4 RQ sau:

```text
RQ1: Can forecasting-based anomaly detection effectively identify bearing degradation under a run-to-failure setting?

RQ2: Does Mamba-based temporal modeling improve degradation detection compared with conventional sequence models such as LSTM, TCN, and Transformer?

RQ3: Does vibration–temperature fusion improve early degradation detection compared with vibration-only modeling?

RQ4: How do lookback length, forecasting horizon, and thresholding strategy affect anomaly detection performance?
```

---

# 15. Tên mô hình đề xuất

Nên đặt tên mô hình để bài nhìn chuyên nghiệp hơn.

## Một số tên

```text
VT-MambaForecast
```

Viết đầy đủ:

```text
Vibration–Temperature Mamba Forecasting Network
```

Hoặc:

```text
SSM-BAD
Self-Supervised Mamba for Bearing Anomaly Detection
```

Hoặc dễ hiểu:

```text
Fusion-MambaAD
```

## Khuyến nghị

```text
VT-MambaAD: Vibration–Temperature Mamba Anomaly Detection
```

---

# 16. Method Overview có thể dùng ngay

```text
The proposed VT-MambaAD framework detects bearing degradation through self-supervised future prediction. Given a multivariate sequence containing two vibration channels and two temperature channels, the model forecasts the next K time steps from the previous N observations. The vibration signals are first transformed into compact patch-level representations using a CNN/Patching block, while the temperature signals are encoded using a lightweight temporal branch. The extracted representations are fused and passed into a Mamba encoder to model long-range temporal dependencies. A forecasting head then predicts the future multivariate sequence. During inference, the discrepancy between the predicted and observed future sequence is computed as an anomaly score. When the anomaly score exceeds a threshold estimated from early-life training data, the corresponding window is identified as abnormal.
```

---

# 17. Bộ hình nên có trong bài

| Figure | Tên hình | Vai trò |
|---|---|---|
| Figure 1 | Overall research workflow | Cho thấy classification → forecasting/anomaly detection |
| Figure 2 | Run-to-failure timeline | Mô tả Healthy/Degrading/Fault theo TTF% |
| Figure 3 | Proposed architecture | CNN/Patching + Mamba + Fusion + Forecast Head |
| Figure 4 | Anomaly score over TTF% | Hình quan trọng nhất |
| Figure 5 | Confusion matrix | Đánh giá phân loại theo threshold |
| Figure 6 | F1-score per class | Xem lớp nào khó |
| Figure 7 | Ablation results | Chứng minh từng module có ích |
| Figure 8 | Runtime/memory comparison | Nếu muốn đẩy lên Q3 |

---

# 18. Bộ bảng nên có trong bài

| Table | Nội dung |
|---|---|
| Table 1 | Dataset summary |
| Table 2 | Forecasting configuration N/K |
| Table 3 | Baseline model configuration |
| Table 4 | Main result comparison |
| Table 5 | Vibration-temperature ablation |
| Table 6 | Encoder ablation: LSTM/TCN/Transformer/Mamba |
| Table 7 | Thresholding comparison |
| Table 8 | Runtime/memory comparison |

---

# 19. Mức Q4/Q3 nên làm đến đâu?

## 19.1. Mức Q4: đủ để nộp

| Thành phần | Mức cần có |
|---|---|
| Dataset | 1 dataset chính |
| Model | CNN/Patching + Mamba |
| Baseline | LSTM, TCN, Transformer |
| Metric | MSE, MAE, F1, AUC |
| Threshold | 3-sigma hoặc percentile |
| Ablation | vibration-only vs vibration+temperature |
| Figure | anomaly score over TTF%, confusion matrix |
| Novelty | self-supervised forecasting + anomaly score |

## 19.2. Mức Q3: nên bổ sung

| Thành phần | Bổ sung để mạnh hơn |
|---|---|
| Dataset | thêm NASA IMS hoặc XJTU-SY nếu được |
| Baseline | thêm classification baseline từ bài đầu |
| Ablation | thêm patching, N/K, threshold |
| Metric | thêm detection delay, false alarm rate |
| Figure | runtime/memory comparison |
| Discussion | phân tích kỹ Healthy–Degrading boundary |
| Robustness | chạy nhiều seed hoặc nhiều bearing run |

---

# 20. Checklist triển khai bài báo

## 20.1. Phần nghiên cứu nền tảng

- [ ] Xác định research gap.
- [ ] Viết research questions.
- [ ] Viết contribution.
- [ ] Tìm paper về bearing fault diagnosis.
- [ ] Tìm paper về run-to-failure prognostics.
- [ ] Tìm paper về forecasting-based anomaly detection.
- [ ] Tìm paper về Mamba/Transformer for time-series.
- [ ] Viết Introduction.
- [ ] Viết Related Work.

## 20.2. Phần dữ liệu

- [ ] Mô tả dataset.
- [ ] Chuyển dữ liệu sang forecasting format.
- [ ] Tạo sample X quá khứ và Y tương lai.
- [ ] Thiết kế lookback N và horizon K.
- [ ] Thiết kế temporal split.
- [ ] Thiết kế normalization.
- [ ] Chuẩn bị Dataset/Preprocessing section.

## 20.3. Phần mô hình

- [ ] Vẽ overall architecture.
- [ ] Thiết kế CNN/Patching block.
- [ ] Thiết kế Mamba Encoder.
- [ ] Thiết kế temperature branch.
- [ ] Thiết kế fusion module.
- [ ] Thiết kế Forecast Head.
- [ ] Viết công thức anomaly score.
- [ ] Viết Proposed Method.

## 20.4. Phần thực nghiệm

- [ ] Chọn baseline.
- [ ] Chọn metric.
- [ ] Thiết kế threshold.
- [ ] Chạy main experiment.
- [ ] Chạy ablation vibration vs vibration-temperature.
- [ ] Chạy ablation Mamba vs LSTM/TCN/Transformer.
- [ ] Chạy ablation N/K.
- [ ] Vẽ anomaly score over TTF%.
- [ ] Vẽ confusion matrix.
- [ ] Viết Results.
- [ ] Viết Discussion.
- [ ] Viết Conclusion.

---

# 21. Đánh giá tổng thể

Hướng này phù hợp để viết bài Q4/Q3 vì:

1. Có sự kế thừa rõ từ bài đầu: Healthy/Degrading/Fault classification.
2. Có hướng mới vừa đủ: self-supervised forecasting-based anomaly detection.
3. Có mô hình hiện đại: Mamba.
4. Có multimodal signal: vibration + temperature.
5. Có đánh giá nghiêm túc: temporal split, anomaly score, threshold, ablation.
6. Không cần claim quá lớn, chỉ cần chứng minh mô hình khả thi và tốt hơn baseline ở một số metric.

Điểm cần cẩn thận nhất là **đừng overclaim**.

## Nên viết

```text
We investigate...
We propose a framework...
Experimental results suggest...
```

## Không nên viết

```text
This method solves bearing fault prediction completely.
Mamba is always better than Transformer.
The proposed method is universally applicable.
```

---

# 22. Gợi ý mức độ novelty

## Novelty mức Q4

```text
Áp dụng self-supervised forecasting để phát hiện degradation bằng anomaly score trên bearing run-to-failure dataset.
```

## Novelty mức Q3

```text
Kết hợp CNN/Patching + Mamba + vibration-temperature fusion, đánh giá bằng temporal leakage-aware protocol, so sánh forecasting baseline, classification baseline và thực hiện ablation đầy đủ.
```

---

# 23. Dàn ý viết nhanh theo từng ngày

## Ngày 1–2: Nền tảng

- Viết Introduction.
- Viết Research Gap.
- Viết RQ.
- Viết Contribution.
- Tìm 20–30 paper liên quan.

## Ngày 3–4: Dataset và Method

- Viết Dataset.
- Viết Problem Formulation.
- Viết Forecasting Data Construction.
- Viết Proposed Method.
- Vẽ architecture.

## Ngày 5–7: Experiment

- Chạy baseline LSTM, TCN, Transformer.
- Chạy Mamba.
- Chạy Fusion Mamba.
- Tạo anomaly score.
- Tạo threshold.

## Ngày 8–9: Result và Ablation

- Vẽ bảng kết quả.
- Vẽ anomaly score over TTF%.
- Vẽ confusion matrix.
- Chạy ablation cơ bản.

## Ngày 10: Hoàn thiện

- Viết Discussion.
- Viết Limitation.
- Viết Conclusion.
- Chuẩn hóa citation.
- Soát lại claim cho phù hợp Q4/Q3.

---

# 24. Kết luận định hướng

Bài báo nên được định vị như sau:

```text
Không phải là một bài classification truyền thống.
Không phải là một bài Mamba thuần túy.
Không phải là một bài RUL prediction quá lớn.

Đây là một bài self-supervised forecasting-based anomaly detection cho bearing degradation, dùng Mamba để học long sequence và dùng vibration-temperature fusion để tăng khả năng phát hiện sớm.
```

Đây là hướng vừa đủ mới, vừa đủ khả thi, phù hợp để phát triển thành bài Q4/Q3 nếu thực nghiệm được trình bày rõ ràng, có baseline, có ablation và tránh data leakage.
