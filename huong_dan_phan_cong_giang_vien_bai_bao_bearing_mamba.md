# Hướng dẫn phân công công việc cho nhóm giảng viên  
## Chủ đề: Phát triển bài báo mới từ hướng Bearing Health Classification sang Self-Supervised Forecasting/Anomaly Detection

---

## 1. Mục tiêu chung của nhóm

Nhóm đang phát triển hướng nghiên cứu kế tiếp từ bài báo đầu tiên về **Three-Stage Bearing Health Classification**. Bài báo đầu tiên tập trung vào việc phân loại trạng thái ổ bi thành:

- **Healthy**
- **Degrading**
- **Fault**

bằng cách sử dụng dữ liệu **vibration STFT** kết hợp với **temperature trend**.

Hướng bài báo mới nên chuyển từ tư duy **classification** sang hướng:

> **Self-Supervised Forecasting-Based Anomaly Detection for Bearing Degradation**

Nói đơn giản:

- Mô hình học quy luật vận hành bình thường của ổ bi.
- Mô hình dự báo dữ liệu tương lai từ dữ liệu quá khứ.
- Khi ổ bi bắt đầu suy thoái, dữ liệu thật sẽ lệch khỏi dữ liệu dự báo.
- Sai số dự báo tăng lên sẽ được dùng làm **anomaly score**.
- Dựa vào anomaly score để phát hiện giai đoạn **Degrading** hoặc **Fault**.

Ví dụ:

```text
Input: 1024 điểm dữ liệu quá khứ gồm vibration_x, vibration_y, temp_1, temp_2
Output: 128 điểm dữ liệu tương lai

Nếu mô hình dự báo đúng gần với thực tế → hệ thống có khả năng vẫn Healthy
Nếu mô hình dự báo lệch nhiều → có khả năng bắt đầu Degrading hoặc Fault
```

---

# 2. Giảng viên 1: Phụ trách nền tảng nghiên cứu, khoảng trống và câu hỏi nghiên cứu

## 2.1. Mục tiêu chính

Giảng viên 1 chịu trách nhiệm làm rõ:

> Bài báo này giải quyết vấn đề gì, vì sao vấn đề đó quan trọng, các nghiên cứu trước đã làm đến đâu, và nhóm mình còn khoảng trống nào để đóng góp?

Nói đơn giản, giảng viên 1 là người xây dựng **lý do tồn tại của bài báo**.

---

## 2.2. Công việc 1: Đọc bài báo đầu tiên và xác định hướng phát triển tiếp theo

Bài báo đầu tiên đang làm hướng:

```text
Phân loại trạng thái ổ bi thành Healthy, Degrading, Fault bằng vibration STFT và temperature trend.
```

Giảng viên 1 cần đọc bài đầu tiên và rút ra các điểm có thể phát triển thành bài báo mới.

| Nội dung trong bài đầu tiên | Có thể phát triển thành hướng mới |
|---|---|
| Đang phân loại 3 trạng thái | Chuyển sang phát hiện suy thoái bằng anomaly detection |
| Cần nhãn Healthy/Degrading/Fault | Thử hướng self-supervised, ít phụ thuộc nhãn |
| Dùng STFT + CNN | Thêm mô hình chuỗi dài như Mamba/Transformer |
| Dùng temperature trend | Nghiên cứu sâu hơn vai trò của temperature trong phát hiện sớm |
| Khó ở vùng Healthy–Degrading | Tập trung vào early degradation detection |

---

## 2.3. Công việc 2: Xác định research gap

Giảng viên 1 nên tìm và viết ra khoảng trống nghiên cứu theo hướng:

> Các nghiên cứu hiện tại chủ yếu tập trung vào classification, nhưng trong thực tế, sự suy thoái diễn ra dần dần, khó gán nhãn rạch ròi. Vì vậy cần một hướng tiếp cận dựa trên forecasting/anomaly score để phát hiện sự thay đổi bất thường theo thời gian.

Ví dụ research gap bằng tiếng Anh:

```text
Most existing bearing diagnosis studies formulate the problem as supervised classification, where each signal window is assigned to a predefined health stage. However, degradation in run-to-failure settings evolves gradually, making the boundary between Healthy and Degrading ambiguous. This motivates a forecasting-based anomaly detection framework that learns normal temporal dynamics and identifies degradation through prediction errors.
```

Diễn giải dễ hiểu:

```text
Thay vì bắt mô hình trả lời ngay “đây là Healthy hay Degrading”, ta cho mô hình học quy luật vận hành bình thường. Khi ổ bi bắt đầu suy thoái, dữ liệu thật sẽ lệch khỏi dự báo, làm sai số tăng lên. Sai số này có thể dùng để phát hiện bất thường.
```

---

## 2.4. Công việc 3: Chia nhóm tài liệu cần đọc

Giảng viên 1 không nên đọc tài liệu một cách dàn trải. Nên chia paper thành 5 nhóm.

### Nhóm 1: Bearing fault diagnosis

Mục đích: hiểu nền tảng bài toán ổ bi.

Câu hỏi cần trả lời:

- Người ta thường dùng tín hiệu gì để phát hiện lỗi ổ bi?
- Vibration có vai trò gì?
- Temperature có thường được dùng không?
- Các trạng thái Healthy, Degrading, Fault thường được định nghĩa thế nào?

### Nhóm 2: Run-to-failure prognostics

Mục đích: hiểu bài toán theo vòng đời suy thoái.

Câu hỏi cần trả lời:

- Run-to-failure khác gì với fault classification thông thường?
- Time-to-failure, remaining useful life, degradation stage được dùng thế nào?
- Có những cách chia giai đoạn suy thoái nào?

### Nhóm 3: Time-series forecasting

Mục đích: tạo nền tảng cho hướng mới.

Câu hỏi cần trả lời:

- Forecasting trong chuỗi thời gian hoạt động ra sao?
- One-step forecasting và multi-step forecasting khác gì nhau?
- Forecasting error có thể dùng để phát hiện bất thường không?

### Nhóm 4: Anomaly detection

Mục đích: giải thích vì sao sai số dự báo có thể trở thành anomaly score.

Câu hỏi cần trả lời:

- Prediction error được dùng làm anomaly score như thế nào?
- Ngưỡng cảnh báo thường được đặt bằng cách nào?
- Làm sao đánh giá false alarm và early detection?

### Nhóm 5: Mamba/Transformer for long sequence

Mục đích: tạo lý do chọn Mamba.

Câu hỏi cần trả lời:

- Transformer có hạn chế gì khi xử lý chuỗi dài?
- Mamba có ưu điểm gì với long time-series?
- Mamba đã được dùng trong forecasting/anomaly detection chưa?
- Có thể so sánh Mamba với LSTM, TCN, Transformer như thế nào?

---

## 2.5. Công việc 4: Đề xuất bộ câu hỏi nghiên cứu chính

Giảng viên 1 nên đề xuất 4–5 câu hỏi nghiên cứu làm khung cho bài.

### RQ1

**Forecasting-based anomaly detection có phát hiện suy thoái ổ bi hiệu quả hơn classification-based approach không?**

Hướng giải thích:

- Classification cần nhãn rõ.
- Degrading là vùng chuyển tiếp, khó gán nhãn.
- Forecasting dùng sai số dự báo nên có thể nhạy với thay đổi dần dần.

### RQ2

**Mamba có phù hợp hơn LSTM/TCN/Transformer trong xử lý chuỗi vibration–temperature dài không?**

Hướng giải thích:

- Vibration là tín hiệu nhanh.
- Temperature là tín hiệu chậm.
- Mamba có tiềm năng nắm bắt cả xu hướng ngắn và dài.

### RQ3

**Temperature có giúp phát hiện sớm giai đoạn Degrading/Fault khi kết hợp với vibration không?**

Hướng giải thích:

- Vibration phản ánh dao động cơ học.
- Temperature phản ánh ma sát, tải, nhiệt tích lũy.
- Khi ổ bi suy thoái, nhiệt độ có thể thay đổi chậm nhưng ổn định.

### RQ4

**CNN/Patching có giúp giảm chi phí tính toán mà vẫn giữ được đặc trưng cục bộ của tín hiệu không?**

Hướng giải thích:

- Chuỗi vibration rất dài.
- Patching giúp biến chuỗi dài thành các đoạn ngắn.
- CNN giúp bắt pattern cục bộ trước khi đưa vào Mamba.

---

## 2.6. Công việc 5: Viết phần đóng góp của bài báo

Giảng viên 1 nên viết 3–4 contribution rõ ràng.

Ví dụ:

```text
The main contributions of this study are as follows:

1. We propose a self-supervised forecasting-based framework for bearing degradation detection under a run-to-failure setting.

2. We design a CNN/Patching-Mamba architecture to capture both local vibration patterns and long-range degradation dynamics.

3. We investigate vibration–temperature fusion for anomaly-score-based early degradation detection.

4. We conduct temporal leakage-aware evaluation with baseline comparison and ablation studies.
```

---

## 2.7. Đầu ra cần hoàn thành

| Đầu ra | Mô tả |
|---|---|
| Research gap | 1–2 đoạn nêu rõ khoảng trống nghiên cứu |
| Research questions | 4–5 câu hỏi nghiên cứu chính |
| Contribution | 3–4 đóng góp chính |
| Related Work outline | Dàn ý phần tổng quan tài liệu |
| Introduction draft | Bản nháp phần mở đầu |

---

# 3. Giảng viên 2: Phụ trách dataset, tiền xử lý và xây dựng dữ liệu forecasting

## 3.1. Mục tiêu chính

Giảng viên 2 chịu trách nhiệm làm rõ:

> Dữ liệu được lấy từ đâu, xử lý thế nào, chia train/test thế nào, và chuyển từ bài toán classification sang forecasting ra sao?

Nói đơn giản, giảng viên 2 là người xây dựng **nền móng dữ liệu cho bài báo**.

---

## 3.2. Công việc 1: Mô tả lại dataset hiện tại

Giảng viên 2 cần mô tả dataset theo hướng dễ đưa vào bài báo.

Ví dụ:

```text
The dataset contains synchronized vibration and temperature signals collected from a ball bearing run-to-failure experiment. Vibration is recorded along two axes, while temperature is measured from two channels. The entire run is normalized into a time-to-failure percentage scale, where early-life, mid-life, and late-life regions correspond to Healthy, Degrading, and Fault stages.
```

Có thể hình dung timeline:

```text
0% -------------------- 60% --------------- 90% ------- 100%
Healthy                 Degrading           Fault
```

---

## 3.3. Công việc 2: Chuyển dữ liệu từ classification sang forecasting

Bài báo đầu tiên dùng dạng:

```text
Input: một cửa sổ tín hiệu
Output: Healthy / Degrading / Fault
```

Bài mới nên chuyển thành:

```text
Input: N điểm dữ liệu quá khứ
Output: K điểm dữ liệu tương lai
```

Ví dụ cụ thể:

```text
Input X = dữ liệu từ t đến t+1024
Output Y = dữ liệu từ t+1025 đến t+1152
```

Nếu có 4 kênh:

```text
vibration_x
vibration_y
temperature_1
temperature_2
```

Thì một mẫu dữ liệu có dạng:

```text
X shape = [1024, 4]
Y shape = [128, 4]
```

---

## 3.4. Công việc 3: Đề xuất các cấu hình lookback và forecast horizon

Giảng viên 2 cần đề xuất nhiều cấu hình để nhóm chạy thử.

| Cấu hình | Lookback N | Horizon K | Ý nghĩa |
|---|---:|---:|---|
| Config A | 512 | 64 | Nhanh, nhẹ, phù hợp thử nghiệm ban đầu |
| Config B | 1024 | 128 | Cân bằng giữa tốc độ và ngữ cảnh |
| Config C | 2048 | 256 | Nhìn được xu hướng dài hơn |
| Config D | 4096 | 256 | Chuỗi dài, phù hợp kiểm tra sức mạnh Mamba |

Hướng đi khuyến nghị:

```text
Bắt đầu với N=1024, K=128 để code beta chạy ổn trước. Sau đó mới mở rộng sang N=2048 hoặc 4096 để so sánh Mamba với Transformer.
```

---

## 3.5. Công việc 4: Thiết kế cách chia train/validation/test

Không nên random window vì dễ làm rò rỉ dữ liệu thời gian.

Hướng chia đề xuất:

```text
Train: 0–60% TTF
Validation: 60–70% TTF
Test: 70–100% TTF
```

Ý nghĩa:

- Train trên giai đoạn ổn định/healthy.
- Validation trên vùng chuyển tiếp.
- Test trên vùng degradation và fault.

Ví dụ diễn giải trong bài:

```text
To approximate deployment conditions, we adopt a contiguous temporal split along the normalized lifetime axis. The model is trained on early-life data, validated on the transition region, and tested on later-life degradation and fault regions.
```

---

## 3.6. Công việc 5: Thiết kế normalization

Giảng viên 2 cần đề xuất các cách chuẩn hóa để thử.

### Cách 1: Global z-score

Tính mean/std trên tập train rồi áp dụng cho val/test.

```text
x_norm = (x - mean_train) / std_train
```

Ưu điểm:

- Đúng nguyên tắc deployment.
- Tránh nhìn trước test.

### Cách 2: Per-window z-score

Chuẩn hóa riêng từng cửa sổ.

Ưu điểm:

- Giảm khác biệt biên độ.
- Tốt cho vibration.

Nhược điểm:

- Có thể làm mất thông tin mức tăng biên độ khi lỗi xuất hiện.

### Cách 3: Robust scaling

Dùng median và IQR.

Ưu điểm:

- Ít bị ảnh hưởng bởi outlier.

Khuyến nghị:

```text
Với anomaly detection, nên cẩn thận với per-window z-score vì nó có thể làm mất tín hiệu bất thường. Nên ưu tiên global train-only normalization, sau đó làm ablation thêm per-window normalization.
```

---

## 3.7. Công việc 6: Định nghĩa anomaly label để đánh giá

Dù mô hình học forecasting không cần label trực tiếp, nhưng khi đánh giá vẫn cần biết vùng nào là Healthy, Degrading, Fault.

Có thể dùng quy ước:

```text
0–60% TTF: Healthy
60–90% TTF: Degrading
90–100% TTF: Fault
```

Sau đó dùng anomaly score để xem model cảnh báo vào vùng nào.

Ví dụ:

```text
Nếu anomaly score vượt threshold từ 68% TTF, thì model bắt đầu phát hiện suy thoái gần vùng Degrading.
```

---

## 3.8. Công việc 7: Tìm thêm dataset phụ để mở rộng

Giảng viên 2 có thể gợi ý cho sinh viên tìm thêm:

| Dataset | Hướng dùng |
|---|---|
| NASA IMS Bearing Dataset | Kiểm tra bearing run-to-failure |
| XJTU-SY Bearing Dataset | Multi-run bearing degradation |
| Paderborn Bearing Dataset | Classification baseline |
| Battery degradation dataset | Mở rộng sang time-series prognostics |
| C-MAPSS turbofan dataset | RUL prediction baseline nếu muốn mở rộng |

Hướng đi:

```text
Nếu thời gian ngắn, dùng dataset hiện tại để hoàn thành bài Q3. Nếu cần tăng độ mạnh, thêm XJTU-SY hoặc NASA IMS làm external validation.
```

---

## 3.9. Đầu ra cần hoàn thành

| Đầu ra | Mô tả |
|---|---|
| Dataset description | Mô tả dataset chính |
| Forecasting data construction | Cách tạo X quá khứ và Y tương lai |
| Temporal split protocol | Cách chia train/val/test theo TTF |
| Normalization strategy | Các cách chuẩn hóa cần thử |
| N/K configuration table | Bảng cấu hình lookback và horizon |
| Dataset section draft | Bản nháp phần dataset/preprocessing |

---

# 4. Giảng viên 3: Phụ trách kiến trúc mô hình đề xuất

## 4.1. Mục tiêu chính

Giảng viên 3 chịu trách nhiệm làm rõ:

> Mô hình đề xuất gồm những khối nào, vì sao chọn các khối đó, dữ liệu đi qua mô hình ra sao, và anomaly score được tạo ra như thế nào?

Nói đơn giản, giảng viên 3 là người xây dựng **trái tim kỹ thuật của bài báo**.

---

## 4.2. Công việc 1: Thiết kế kiến trúc tổng thể

Kiến trúc đề xuất có thể đi theo hướng:

```text
Raw vibration + temperature
        ↓
Normalization
        ↓
CNN/Patching Block
        ↓
Mamba Encoder
        ↓
Fusion Module
        ↓
Forecast Head
        ↓
Predicted future sequence
        ↓
Prediction error
        ↓
Anomaly score
```

Ý tưởng dễ hiểu:

```text
CNN/Patching giúp nén tín hiệu dài thành các token ngắn hơn. Mamba học quan hệ dài hạn giữa các token. Forecast Head dự báo tương lai. Sai số giữa tương lai thật và tương lai dự báo được dùng làm anomaly score.
```

---

## 4.3. Công việc 2: Thiết kế CNN/Patching Block

Mục đích:

- Vibration có rất nhiều điểm dữ liệu.
- Nếu đưa trực tiếp chuỗi dài vào model thì tốn bộ nhớ.
- Patching chia chuỗi thành nhiều đoạn nhỏ.
- CNN học pattern cục bộ trong từng đoạn.

Ví dụ:

```text
Input sequence length = 4096
Patch size = 16
Number of patches = 256
```

Mỗi patch có thể xem như một “từ” trong chuỗi.

```text
4096 raw points → 256 patch tokens
```

Hướng viết trong bài:

```text
A patching layer is first applied to reduce the temporal resolution of long input sequences. Local convolutional filters are then used to extract short-term vibration patterns within each patch before passing the compact token sequence to the Mamba encoder.
```

---

## 4.4. Công việc 3: Thiết kế Mamba Encoder

Mục đích:

- Học tương quan dài hạn.
- Theo dõi quá trình suy thoái diễn ra từ từ.
- Tránh chi phí cao của attention trong Transformer.

Ví dụ:

```text
Input to Mamba:
[batch, number_of_patches, hidden_dim]

Example:
[32, 256, 128]
```

Output:

```text
Context representation:
[32, 256, 128]
```

Hướng đi thực tế:

- Dùng 2–4 lớp Mamba cho bản beta.
- Hidden dim thử 64, 128, 256.
- Dropout thử 0.1.
- So sánh với Transformer cùng số layer/hidden dim để công bằng.

---

## 4.5. Công việc 4: Thiết kế nhánh vibration và temperature

Có 2 hướng.

### Hướng A: Gộp 4 kênh ngay từ đầu

```text
[vib_x, vib_y, temp_1, temp_2] → CNN/Patching → Mamba
```

Ưu điểm:

- Dễ code.
- Đơn giản.

Nhược điểm:

- Vibration và temperature có bản chất rất khác nhau.
- Temperature thay đổi chậm, vibration thay đổi nhanh.

### Hướng B: Tách nhánh rồi fusion

```text
Vibration branch:
[vib_x, vib_y] → CNN/Patching → Mamba → hv

Temperature branch:
[temp_1, temp_2] → small MLP/TCN → ht

Fusion:
[hv; ht] → Forecast Head
```

Ưu điểm:

- Rõ ràng hơn về mặt khoa học.
- Kế thừa logic từ bài báo đầu tiên: vibration branch + temperature descriptor.
- Dễ làm ablation vibration-only vs vibration+temperature.

Khuyến nghị:

```text
Nên dùng hướng B cho bài báo vì dễ giải thích đóng góp của temperature fusion.
```

---

## 4.6. Công việc 5: Thiết kế Fusion Module

Có thể thử 3 mức độ.

### Mức 1: Concatenation Fusion

```text
h = concat(h_vibration, h_temperature)
```

Ưu điểm:

- Dễ làm.
- Dễ giải thích.
- Phù hợp bài đầu tiên.

### Mức 2: Weighted Fusion

```text
h = α * h_vibration + β * h_temperature
```

Ví dụ:

```text
h = 0.7 * h_vibration + 0.3 * h_temperature
```

Có thể để α, β là tham số học được.

### Mức 3: Attention Fusion

Cho mô hình tự học kênh nào quan trọng hơn.

Ưu điểm:

- Mạnh hơn.
- Có thể giải thích attention weight.

Nhược điểm:

- Phức tạp hơn.
- Cần nhiều dữ liệu hơn.

Khuyến nghị:

```text
Bản đầu dùng concatenation fusion. Nếu kết quả ổn, thêm weighted fusion hoặc attention fusion như ablation.
```

---

## 4.7. Công việc 6: Thiết kế Forecast Head

Forecast Head dự báo K bước tương lai.

Ví dụ:

```text
Input representation → MLP → K future steps
```

Nếu dự báo cả 4 kênh:

```text
Output shape = [batch, K, 4]
```

Nếu chỉ dự báo vibration:

```text
Output shape = [batch, K, 2]
```

| Cách dự báo | Ưu điểm | Nhược điểm |
|---|---|---|
| Dự báo vibration only | Tập trung tín hiệu chính | Không kiểm tra được temp future |
| Dự báo vibration + temperature | Đầy đủ multimodal | Khó hơn |
| Dự báo embedding tương lai | Gọn hơn | Khó giải thích |

Khuyến nghị:

```text
Bản beta nên dự báo 4 kênh để giữ đúng tinh thần multimodal forecasting. Sau đó ablation dự báo vibration-only.
```

---

## 4.8. Công việc 7: Thiết kế anomaly score

Cách đơn giản nhất:

```text
Anomaly Score = MSE(Y_true, Y_pred)
```

Có thể tách theo modality:

```text
score_vib = MSE(vib_true, vib_pred)
score_temp = MSE(temp_true, temp_pred)
score_total = α * score_vib + β * score_temp
```

Ví dụ:

```text
score_total = 0.8 * score_vib + 0.2 * score_temp
```

Hướng đi:

- Nếu vibration nhiều nhiễu, temperature có thể giúp score ổn định hơn.
- Nếu temperature thay đổi chậm, score_temp có thể tăng muộn nhưng ít nhiễu.
- Có thể vẽ riêng score_vib và score_temp theo TTF%.

---

## 4.9. Đầu ra cần hoàn thành

| Đầu ra | Mô tả |
|---|---|
| Overall architecture diagram | Sơ đồ mô hình tổng thể |
| CNN/Patching design | Mô tả cách nén chuỗi dài |
| Mamba Encoder design | Mô tả vai trò của Mamba |
| Fusion design | Cách kết hợp vibration và temperature |
| Forecast Head design | Cách dự báo K bước tương lai |
| Anomaly score formula | Công thức tính điểm bất thường |
| Proposed Method draft | Bản nháp phần phương pháp |

---

# 5. Giảng viên 4: Phụ trách thực nghiệm, baseline, ablation và phân tích kết quả

## 5.1. Mục tiêu chính

Giảng viên 4 chịu trách nhiệm làm rõ:

> Làm sao chứng minh mô hình đề xuất tốt hơn, đáng tin hơn, và từng thành phần trong mô hình thật sự có đóng góp?

Nói đơn giản, giảng viên 4 là người xây dựng **bằng chứng thực nghiệm của bài báo**.

---

## 5.2. Công việc 1: Xác định baseline cần so sánh

Nên chia baseline thành 2 nhóm.

### Nhóm A: Baseline classification từ bài đầu tiên

Mục đích:

```text
So sánh hướng forecasting/anomaly detection với hướng classification cũ.
```

Ví dụ baseline:

```text
Classical SVM with handcrafted vibration features
STFT-CNN vibration-only classifier
STFT-CNN + temperature fusion classifier
```

Câu hỏi cần trả lời:

- Forecasting anomaly detection có phát hiện Degrading/Fault tốt hơn classification không?
- Classification có bị yếu ở vùng Healthy–Degrading không?
- Forecasting có phát hiện sớm hơn không?

### Nhóm B: Baseline forecasting

Mục đích:

```text
Chứng minh Mamba đáng dùng hơn các mô hình chuỗi thời gian khác.
```

Ví dụ baseline:

```text
LSTM Forecasting
GRU Forecasting
TCN Forecasting
Transformer Forecasting
Informer/iTransformer nếu đủ thời gian
Mamba Forecasting
```

Hướng đi thực tế:

- Bắt buộc nên có: LSTM, TCN, Transformer, Mamba.
- Nếu thời gian hạn chế, bỏ GRU hoặc Informer.
- Cần giữ cùng input/output N/K để so sánh công bằng.

---

## 5.3. Công việc 2: Chọn metric đánh giá

Vì bài mới có 2 tầng: forecasting và detection, nên cần 2 nhóm metric.

### Metric forecasting

| Metric | Dùng để làm gì |
|---|---|
| MSE | Đo sai số dự báo, dùng làm anomaly score |
| MAE | Ít nhạy hơn với outlier |
| RMSE | Dễ diễn giải vì cùng đơn vị với tín hiệu |

Ví dụ:

```text
Mamba đạt MSE thấp hơn LSTM trong vùng Healthy, nghĩa là học quy luật bình thường tốt hơn.
```

### Metric detection

| Metric | Dùng để làm gì |
|---|---|
| Precision | Cảnh báo suy thoái có đúng không |
| Recall | Có bỏ sót suy thoái không |
| F1-score | Cân bằng precision và recall |
| AUC | Khả năng phân biệt bình thường/bất thường |
| False alarm rate | Có báo động giả nhiều không |
| Detection delay | Phát hiện sớm hay muộn |

Ví dụ:

```text
Nếu threshold được vượt tại 66% TTF, trong khi Degrading bắt đầu từ 60% TTF, detection delay là 6% TTF.
```

---

## 5.4. Công việc 3: Thiết kế thresholding

Anomaly score cần ngưỡng để quyết định khi nào cảnh báo.

### Cách 1: 3-sigma threshold

Tính trên vùng Healthy:

```text
threshold = mean_healthy + 3 * std_healthy
```

Ví dụ:

```text
Healthy score mean = 0.02
Healthy score std = 0.005
Threshold = 0.02 + 3*0.005 = 0.035
```

Nếu score > 0.035 thì cảnh báo.

Ưu điểm:

- Dễ giải thích.
- Phù hợp bài Q3.

### Cách 2: Percentile threshold

Ví dụ:

```text
Threshold = 95th percentile của Healthy score
```

Ưu điểm:

- Dễ làm.
- Ít giả định phân phối chuẩn.

### Cách 3: GMM threshold

Dùng Gaussian Mixture Model để phân cụm anomaly score.

Ý tưởng:

```text
Score thấp → Normal
Score trung bình → Degrading
Score cao → Fault
```

Ưu điểm:

- Có tính xác suất.
- Phù hợp nếu muốn chia 3 trạng thái.

Khuyến nghị:

```text
Bắt đầu với 3-sigma và percentile. Nếu kết quả ổn, thêm GMM để tăng độ sâu cho bài báo.
```

---

## 5.5. Công việc 4: Thiết kế ablation study

Ablation cần trả lời:

```text
Nếu bỏ từng thành phần, mô hình có yếu đi không?
```

### Ablation 1: Vibration-only vs Vibration + Temperature

Mục tiêu:

```text
Kiểm tra temperature có giúp không.
```

Ví dụ bảng kỳ vọng:

| Model | F1 Degrading | F1 Fault | Nhận xét |
|---|---:|---:|---|
| Vibration-only | 0.78 | 0.85 | Dễ nhiễu hơn |
| Vibration + Temperature | 0.85 | 0.92 | Ổn định hơn |

### Ablation 2: Without Mamba

Thay Mamba bằng LSTM/TCN/Transformer.

Mục tiêu:

```text
Kiểm tra Mamba có thật sự tốt hơn không.
```

Ví dụ:

| Model | AUC | Runtime |
|---|---:|---:|
| LSTM | 0.82 | 1.0x |
| Transformer | 0.88 | 2.5x |
| Mamba | 0.91 | 1.4x |

### Ablation 3: Without Patching

Mục tiêu:

```text
Kiểm tra patching có giúp giảm chi phí không.
```

Ví dụ:

| Variant | Sequence length | GPU memory | F1 |
|---|---:|---:|---:|
| Raw sequence | 4096 | Cao | 0.86 |
| Patch sequence | 256 tokens | Thấp hơn | 0.88 |

### Ablation 4: Different N/K

Mục tiêu:

```text
Tìm cấu hình lookback và forecast horizon tốt nhất.
```

Ví dụ:

| Lookback N | Horizon K | F1 | Detection delay |
|---:|---:|---:|---:|
| 512 | 64 | 0.80 | 12% TTF |
| 1024 | 128 | 0.86 | 8% TTF |
| 2048 | 256 | 0.88 | 6% TTF |
| 4096 | 256 | 0.87 | 6% TTF |

### Ablation 5: Threshold method

Mục tiêu:

```text
Tìm cách đặt ngưỡng tốt nhất.
```

Ví dụ:

| Threshold | Recall | False alarm | Nhận xét |
|---|---:|---:|---|
| 3-sigma | 0.84 | Thấp | Dễ giải thích |
| Percentile 95 | 0.90 | Cao | Nhạy nhưng báo giả nhiều |
| Percentile 99 | 0.78 | Thấp | Bảo thủ |
| GMM | 0.87 | Trung bình | Cân bằng |

---

## 5.6. Công việc 5: Thiết kế bảng kết quả chính

Giảng viên 4 nên chuẩn bị sẵn template bảng để khi sinh viên chạy xong chỉ cần điền.

Ví dụ bảng chính:

| Method | Forecast MSE | AUC | F1 Degrading | F1 Fault | Detection Delay | Runtime |
|---|---:|---:|---:|---:|---:|---:|
| LSTM |  |  |  |  |  |  |
| TCN |  |  |  |  |  |  |
| Transformer |  |  |  |  |  |  |
| Mamba |  |  |  |  |  |  |
| Proposed Fusion Mamba |  |  |  |  |  |  |

---

## 5.7. Công việc 6: Hướng phân tích kết quả

Khi có kết quả, giảng viên 4 nên phân tích theo logic sau.

### Nếu Proposed tốt hơn baseline

Có thể viết:

```text
The proposed model achieves higher F1 and lower detection delay, suggesting that the Mamba-based forecasting framework captures long-range degradation dynamics more effectively than conventional recurrent or attention-based baselines.
```

### Nếu temperature giúp cải thiện

Có thể viết:

```text
The improvement from vibration-only to vibration–temperature fusion indicates that thermal trends provide complementary degradation cues, especially in late-life regions where friction-induced heating becomes more pronounced.
```

### Nếu Healthy–Degrading vẫn khó

Có thể viết:

```text
Most errors occur near the Healthy–Degrading boundary, where degradation evolves gradually and the statistical distribution of signals overlaps between normal and early-degradation states.
```

### Nếu Mamba không vượt Transformer rõ ràng

Vẫn có thể viết:

```text
Although Mamba and Transformer achieve comparable detection performance, Mamba requires lower memory and shorter training time, making it more suitable for real-time deployment.
```

---

## 5.8. Công việc 7: Định hướng hình minh họa cần có

Giảng viên 4 nên yêu cầu sinh viên tạo các hình sau:

| Hình | Ý nghĩa |
|---|---|
| Anomaly score over TTF% | Quan trọng nhất, cho thấy score tăng khi suy thoái |
| Threshold line | Minh họa điểm cảnh báo |
| Confusion matrix | So sánh dự đoán trạng thái |
| F1 per class | Xem lớp nào khó |
| Runtime/memory comparison | Chứng minh hiệu quả tính toán |
| Ablation bar chart | Chứng minh từng thành phần có ích |

Ví dụ hình quan trọng nhất:

```text
X-axis: TTF%
Y-axis: Anomaly Score

Healthy region: score thấp
Degrading region: score bắt đầu tăng
Fault region: score tăng mạnh
Threshold: đường ngang cảnh báo
```

---

## 5.9. Đầu ra cần hoàn thành

| Đầu ra | Mô tả |
|---|---|
| Baseline plan | Danh sách model cần so sánh |
| Metric definition | Định nghĩa metric forecasting và detection |
| Thresholding strategy | 3-sigma, percentile, GMM |
| Ablation plan | Các biến thể cần chạy |
| Result table template | Mẫu bảng kết quả |
| Figure requirements | Danh sách hình cần vẽ |
| Experiment/Results draft | Bản nháp phần thực nghiệm và kết quả |

---

# 6. Tóm tắt rất ngắn vai trò của từng giảng viên

| Giảng viên | Vai trò chính | Câu hỏi cần trả lời |
|---|---|---|
| Giảng viên 1 | Nền tảng lý thuyết, gap, RQ | Vì sao bài báo này cần làm? |
| Giảng viên 2 | Dataset, preprocessing, forecasting data | Dữ liệu được chuẩn bị thế nào? |
| Giảng viên 3 | Kiến trúc mô hình | Mô hình hoạt động ra sao? |
| Giảng viên 4 | Thực nghiệm, baseline, ablation | Làm sao chứng minh mô hình tốt? |

---

# 7. Checklist cuối cùng cho nhóm giảng viên

## Giảng viên 1

- [ ] Đọc bài báo đầu tiên.
- [ ] Xác định research gap.
- [ ] Chia nhóm related work.
- [ ] Viết 4–5 research questions.
- [ ] Viết contribution.
- [ ] Viết draft Introduction/Related Work.

## Giảng viên 2

- [ ] Mô tả dataset.
- [ ] Chuyển bài toán classification sang forecasting.
- [ ] Đề xuất lookback N và horizon K.
- [ ] Thiết kế temporal split.
- [ ] Đề xuất normalization.
- [ ] Chuẩn bị phần Dataset/Preprocessing.

## Giảng viên 3

- [ ] Vẽ kiến trúc tổng thể.
- [ ] Thiết kế CNN/Patching.
- [ ] Thiết kế Mamba Encoder.
- [ ] Thiết kế fusion vibration–temperature.
- [ ] Thiết kế Forecast Head.
- [ ] Định nghĩa anomaly score.
- [ ] Viết phần Proposed Method.

## Giảng viên 4

- [ ] Chọn baseline classification và forecasting.
- [ ] Chọn metric forecasting và detection.
- [ ] Thiết kế thresholding.
- [ ] Thiết kế ablation study.
- [ ] Chuẩn bị bảng kết quả.
- [ ] Định hướng hình minh họa.
- [ ] Viết phần Experiments/Results/Discussion.
