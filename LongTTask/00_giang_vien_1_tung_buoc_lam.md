# Giảng viên 1 - Quy trình đọc 5 bài báo liên quan để xây dựng research gap hoàn chỉnh

## 1. Vai trò của Giảng viên 1

Giảng viên 1 chịu trách nhiệm xây dựng nền tảng lý luận cho bài báo mới:

> Bài báo giải quyết vấn đề gì, vì sao vấn đề đó quan trọng, các nghiên cứu trước đã làm đến đâu, còn thiếu gì, và nhóm sẽ đóng góp ở khoảng trống nào?

Hướng nghiên cứu của bài mới chuyển từ:

```text
Three-Stage Bearing Health Classification
```

sang:

```text
Self-Supervised Forecasting-Based Anomaly Detection for Bearing Degradation
```

Nói ngắn gọn, thay vì bắt mô hình phân loại trực tiếp từng cửa sổ tín hiệu thành **Healthy**, **Degrading** hoặc **Fault**, bài mới hướng đến việc cho mô hình học quy luật vận hành bình thường của ổ bi. Khi dữ liệu thật lệch khỏi dữ liệu dự báo, sai số dự báo được dùng làm **anomaly score** để phát hiện suy thoái sớm.

Vai trò của Giảng viên 1 không chỉ là viết gap theo cảm tính, mà phải đọc có hệ thống **5 bài báo liên quan** để chứng minh rằng gap có cơ sở học thuật.

---

## 2. Đầu ra cần hoàn thành

| Đầu ra | Yêu cầu |
|---|---|
| Bảng đọc 5 bài báo | Tóm tắt bài toán, phương pháp, dataset, điểm mạnh, hạn chế, liên quan đến bài mới |
| Literature comparison matrix | So sánh 5 bài theo các tiêu chí: task, model, dataset, modality, evaluation, limitation |
| Research gap hoàn chỉnh | Viết 1-2 đoạn gap có dẫn chứng từ 5 bài đã đọc |
| Research questions | Đề xuất 4-5 câu hỏi nghiên cứu bám theo gap |
| Contributions | Viết 3-4 đóng góp chính, tránh nói quá rộng |
| Related Work outline | Lập dàn ý phần tổng quan tài liệu dựa trên 5 bài |
| Introduction draft | Viết bản nháp phần mở đầu có logic từ problem → limitation → gap → proposed direction |

---

## 3. Bối cảnh từ bài báo đầu tiên

Bài báo đầu tiên:

```text
Three-Stage Bearing Health Classification Using Vibration Short-Time Fourier Transform and Temperature Trends in a Run-to-Failure Setting
```

Bài báo này giải quyết bài toán phân loại trạng thái sức khỏe ổ bi thành 3 lớp:

- Healthy
- Degrading
- Fault

Dữ liệu sử dụng gồm:

- Vibration hai trục
- Temperature hai kênh
- TTF% để chia giai đoạn vòng đời ổ bi

Cách chia trạng thái theo TTF%:

| Giai đoạn | Khoảng TTF% |
|---|---:|
| Healthy | 0-60% |
| Degrading | 60-90% |
| Fault | 90-100% |

Điểm mạnh của bài đầu tiên:

- Có sử dụng vibration + temperature.
- Có temporal split để hạn chế leakage.
- Có kết quả tốt ở late-life.
- Có ablation chứng minh temperature hỗ trợ mô hình.

Hạn chế chính cần phát triển:

| Hạn chế của bài đầu tiên | Hướng phát triển cho bài mới |
|---|---|
| Vẫn là supervised classification | Chuyển sang self-supervised forecasting/anomaly detection |
| Cần nhãn Healthy/Degrading/Fault rõ ràng | Giảm phụ thuộc vào ngưỡng TTF cố định |
| Ranh giới Healthy-Degrading mơ hồ | Tập trung early degradation detection |
| CNN học từng window ngắn | Bổ sung long-sequence modeling bằng Mamba/Transformer |
| Temperature mới dùng như descriptor phụ | Khai thác temperature trong forecasting error/anomaly score |
| Dataset hiện còn giới hạn | Cần đọc thêm các paper/dataset run-to-failure để làm cơ sở |

---

## 4. Chọn 5 bài báo liên quan từ file CSV

Từ file CSV, ưu tiên chọn 5 bài liên quan nhất đến hướng bài mới. Không chọn dàn trải quá nhiều paper diagnosis thuần classification.

### 4.1. Danh sách 5 bài nên đọc trước

| Mã | Tên bài báo | Lý do chọn |
|---|---|---|
| P1 | **Bearing Degradation Prediction based on Multi-Scale Mamba-Transformer Model (2025)** | Gần nhất với hướng bearing degradation + Mamba + long-sequence. Có thể làm paper nền chính cho phần Mamba/Transformer. |
| P2 | **FEMamba: A Feature-Enhanced Mamba Framework with Degradation-Stage Global Regularization for Bearing RUL Prediction (2025)** | Liên quan đến degradation stage, Mamba và RUL. Hữu ích để so sánh với hướng anomaly score của bài mới. |
| P3 | **Remaining useful life prediction method for rolling bearings based on Mamba-SDP (2025)** | Liên quan trực tiếp rolling bearing RUL + Mamba. Dùng để phân tích cách các nghiên cứu hiện tại mô hình hóa suy thoái. |
| P4 | **Rolling Bearing Life Prediction Based on Improved Transformer Encoding Layer and Multi-Scale Convolution (2025)** | Không phải Mamba nhưng quan trọng để so sánh Transformer + multi-scale CNN với Mamba. |
| P5 | **A Frequency-Adaptive Feature Extraction Framework for Bearing Remaining Useful Life Prediction (2026)** | Liên quan feature extraction, frequency-adaptive, RUL, FEMTO-ST. Hữu ích cho phần vibration/time-frequency feature. |

### 4.2. Các bài đọc bổ sung nếu còn thời gian

| Tên bài | Khi nào dùng |
|---|---|
| Mamba TFVisionChaos: A Mamba-based Multimodal Bearing Fault Diagnosis Model with Time-Frequency Dual-Axis and Chaos Enhancement | Dùng khi cần chứng minh Mamba đã được áp dụng cho bearing diagnosis, nhưng còn thiên về classification. |
| Rolling Bearing Fault Diagnosis Based on Fractional Constant Q Non-Stationary Gabor Transform and VMamba-Conv | Dùng cho related work về time-frequency + Mamba + lightweight diagnosis. |
| An improved RSMamba network based on multi-domain image fusion for wheelset bearing fault diagnosis under composite conditions | Dùng khi bàn về multi-domain image fusion và diagnosis dưới điều kiện phức tạp. |
| A physical knowledge-informed bearing fault feature extraction network based on Mamba | Dùng nếu muốn mở rộng discussion sang physics-informed feature extraction. |
| Remaining Useful Life Prediction of Airplane Engine Based on Bidirectional Mamba and Causal Discovery | Dùng làm paper ngoài miền bearing để chứng minh Mamba có tiềm năng cho prognostics dài hạn. |

---

## 5. Quy trình đọc từng bài báo

Mỗi bài cần đọc theo cùng một template để dễ so sánh. Không đọc kiểu ghi chú tự do.

### 5.1. Template đọc một bài báo

```markdown
## Paper ID: P1/P2/P3/P4/P5

### 1. Thông tin chung
- Title:
- Year:
- Venue/Journal:
- Task chính:
- Dataset:
- Input modality:
- Output:

### 2. Bài toán nghiên cứu
- Bài báo giải quyết vấn đề gì?
- Vấn đề đó thuộc classification, RUL prediction, forecasting hay anomaly detection?
- Bài toán có liên quan run-to-failure không?

### 3. Phương pháp
- Mô hình chính là gì?
- Có dùng Mamba/Transformer/CNN/LSTM/TCN không?
- Có xử lý long sequence không?
- Có dùng vibration, temperature hay multi-sensor không?
- Có dùng STFT/time-frequency/patching/frequency feature không?

### 4. Dataset và giao thức đánh giá
- Dataset nào được dùng?
- Dataset có run-to-failure không?
- Có vibration không?
- Có temperature không?
- Chia train/val/test như thế nào?
- Có tránh leakage thời gian không?
- Metric sử dụng là gì?

### 5. Kết quả chính
- Mô hình tốt hơn baseline nào?
- Metric nổi bật là gì?
- Kết quả có chứng minh được khả năng early degradation detection không?

### 6. Điểm mạnh
- Điểm mới của bài là gì?
- Bài có đóng góp gì cho hướng Mamba/RUL/degradation?

### 7. Hạn chế
- Có phụ thuộc nhãn RUL hoặc health stage không?
- Có phát hiện sớm Healthy-Degrading không?
- Có dùng prediction error làm anomaly score không?
- Có khai thác temperature không?
- Có đánh giá false alarm/detection delay không?

### 8. Liên hệ với bài mới
- Bài này hỗ trợ phần nào trong Related Work?
- Bài này để lại gap gì cho bài mới?
- Bài mới khác bài này ở điểm nào?
```

---

## 6. Bảng so sánh 5 bài báo

Sau khi đọc xong 5 bài, điền bảng sau.

| Tiêu chí | P1: MSMT | P2: FEMamba | P3: Mamba-SDP | P4: TransCN | P5: Frequency-Adaptive |
|---|---|---|---|---|---|
| Task | Bearing degradation/RUL | Bearing RUL | Bearing RUL | Bearing life/RUL | Bearing RUL |
| Có run-to-failure không? | Cần kiểm tra | Cần kiểm tra | Cần kiểm tra | Cần kiểm tra | Cần kiểm tra |
| Dataset | Cần ghi rõ | Cần ghi rõ | Cần ghi rõ | Cần ghi rõ | FEMTO-ST/khác |
| Input | Vibration? Temp? | Vibration? | Vibration? | Vibration? | Multi-sensor/frequency |
| Model | Mamba + Transformer | Mamba | Mamba-SDP | Transformer + multi-scale CNN | Frequency-adaptive + Transformer/CNN |
| Có forecasting không? | Cần kiểm tra | Cần kiểm tra | Cần kiểm tra | Cần kiểm tra | Cần kiểm tra |
| Có anomaly detection không? | Thường là không | Thường là không | Thường là không | Không rõ | Không rõ |
| Có prediction error/anomaly score không? | Cần kiểm tra | Cần kiểm tra | Cần kiểm tra | Cần kiểm tra | Cần kiểm tra |
| Có early degradation detection không? | Cần kiểm tra | Có thể liên quan | Cần kiểm tra | Cần kiểm tra | Cần kiểm tra |
| Có temperature fusion không? | Cần kiểm tra | Cần kiểm tra | Cần kiểm tra | Cần kiểm tra | Cần kiểm tra |
| Hạn chế chính | Ghi sau khi đọc | Ghi sau khi đọc | Ghi sau khi đọc | Ghi sau khi đọc | Ghi sau khi đọc |
| Gap để lại cho bài mới | Ghi sau khi đọc | Ghi sau khi đọc | Ghi sau khi đọc | Ghi sau khi đọc | Ghi sau khi đọc |

Lưu ý: Không được tự kết luận khi chưa đọc đủ nội dung paper. Các ô “Cần kiểm tra” phải được thay bằng thông tin cụ thể sau khi đọc paper.

---

## 7. Cách rút research gap từ 5 bài báo

Sau khi đọc 5 bài, không viết gap ngay. Cần tổng hợp theo 4 lớp phân tích.

### 7.1. Lớp 1 - Các nghiên cứu đã làm gì?

Trả lời các câu hỏi:

- Các paper hiện tại tập trung vào **fault diagnosis**, **RUL prediction**, hay **degradation prediction**?
- Mamba/Transformer đang được dùng để giải quyết vấn đề gì?
- Các paper có ưu tiên long-sequence modeling không?
- Các paper có dùng vibration + temperature không?
- Các paper có dùng run-to-failure dataset không?

Ví dụ cách viết:

```text
Recent studies have increasingly explored Mamba, Transformer, and multi-scale convolution architectures for bearing degradation and RUL prediction. These methods demonstrate strong capability in modeling long-range temporal dependencies and extracting degradation-related vibration features from run-to-failure datasets.
```

### 7.2. Lớp 2 - Các nghiên cứu còn thiếu gì?

Tìm các thiếu sót lặp lại trong 5 bài:

- Có bài nào dùng **self-supervised forecasting** không?
- Có bài nào dùng **prediction error** làm anomaly score không?
- Có bài nào tập trung riêng vào **early degradation detection** không?
- Có bài nào đánh giá **false alarm** và **detection delay** không?
- Có bài nào khai thác **temperature** như tín hiệu bổ sung cho anomaly score không?
- Có bài nào tránh leakage bằng temporal split rõ ràng không?

Ví dụ cách viết:

```text
However, most existing Mamba-based bearing prognostics studies still formulate the problem as supervised RUL regression or degradation-stage prediction. Such formulations often require target labels or predefined degradation stages and may not directly address early anomaly detection when the Healthy-Degrading boundary is ambiguous.
```

### 7.3. Lớp 3 - Vì sao thiếu sót đó quan trọng?

Liên hệ với bài báo đầu tiên và bài mới:

- Suy thoái ổ bi diễn ra dần dần.
- Ranh giới Healthy-Degrading không rõ.
- Classification/RUL label có thể khó xác định chính xác ở early degradation.
- Trong thực tế, cần cảnh báo sớm hơn là chỉ dự đoán lớp hoặc RUL.
- Vibration biến thiên nhanh, temperature biến thiên chậm; kết hợp hai tín hiệu có thể giúp anomaly score ổn định hơn.

Ví dụ cách viết:

```text
This limitation is important in run-to-failure bearing monitoring because degradation evolves gradually, and the early transition from normal operation to degradation may not produce clear class boundaries. A model that only predicts health stages or RUL may overlook subtle deviations that appear before severe fault symptoms emerge.
```

### 7.4. Lớp 4 - Bài mới sẽ lấp gap như thế nào?

Bài mới nên được định vị như sau:

```text
This study addresses the above gap by proposing a self-supervised forecasting-based anomaly detection framework for bearing degradation. The model learns normal vibration-temperature dynamics and uses forecasting error as an anomaly score to detect early degradation under a leakage-aware temporal evaluation protocol.
```

---

## 8. Research gap hoàn chỉnh - bản nháp sau khi đọc 5 bài

### 8.1. Bản tiếng Việt

```text
Các nghiên cứu gần đây trong lĩnh vực dự đoán suy thoái và tuổi thọ còn lại của ổ bi đã bắt đầu khai thác các kiến trúc chuỗi dài như Transformer, Mamba và các biến thể kết hợp CNN/multi-scale feature extraction. Những hướng tiếp cận này cho thấy hiệu quả trong việc học đặc trưng suy thoái từ tín hiệu vibration và cải thiện độ chính xác trong bài toán RUL prediction hoặc degradation-stage prediction.

Tuy nhiên, phần lớn các nghiên cứu này vẫn mô hình hóa bài toán theo hướng có giám sát, chẳng hạn dự đoán RUL, phân loại trạng thái lỗi hoặc dự đoán giai đoạn suy thoái đã được định nghĩa trước. Cách tiếp cận này phụ thuộc vào nhãn, ngưỡng giai đoạn hoặc target RUL, trong khi trong dữ liệu run-to-failure, quá trình suy thoái ổ bi thường diễn ra dần dần và ranh giới giữa Healthy và Degrading không rõ ràng. Đặc biệt, các nghiên cứu hiện tại chưa tập trung đầy đủ vào hướng self-supervised forecasting-based anomaly detection, nơi mô hình học quy luật vận hành bình thường và dùng forecasting error làm anomaly score để phát hiện suy thoái sớm.

Do đó, bài báo này đề xuất một framework phát hiện suy thoái ổ bi dựa trên self-supervised forecasting, kết hợp vibration và temperature trong bối cảnh run-to-failure. Thay vì dự đoán trực tiếp class label hoặc RUL, mô hình học động học bình thường của tín hiệu quá khứ và phát hiện bất thường thông qua sự gia tăng sai số dự báo. Hướng tiếp cận này nhằm giải quyết vùng chuyển tiếp Healthy-Degrading, giảm phụ thuộc vào nhãn giai đoạn cố định và cung cấp cơ sở cho cảnh báo suy thoái sớm.
```

### 8.2. Bản tiếng Anh

```text
Recent studies on bearing degradation and remaining useful life prediction have increasingly adopted long-sequence architectures such as Transformer, Mamba, and multi-scale convolutional models. These approaches have shown promising performance in extracting degradation-related features from vibration signals and improving RUL or degradation-stage prediction accuracy.

However, most existing studies still formulate the problem as supervised RUL regression, fault diagnosis, or predefined degradation-stage prediction. Such formulations depend on target labels, stage thresholds, or RUL annotations, whereas bearing degradation in run-to-failure settings evolves gradually and the boundary between Healthy and Degrading is often ambiguous. In particular, limited attention has been paid to self-supervised forecasting-based anomaly detection, where a model learns normal temporal dynamics and uses forecasting error as an anomaly score for early degradation detection.

To address this gap, this study proposes a self-supervised forecasting-based anomaly detection framework for bearing degradation under a run-to-failure setting. Instead of directly predicting class labels or RUL values, the proposed model learns normal vibration-temperature dynamics from historical signals and identifies degradation through increased prediction errors. This formulation aims to improve early Healthy-Degrading transition detection, reduce dependence on fixed stage labels, and support leakage-aware temporal evaluation for practical bearing health monitoring.
```

---

## 9. Research questions sau khi có gap

Sau khi hoàn tất bảng đọc 5 bài, điều chỉnh các RQ sau theo bằng chứng thực tế.

### RQ1

**Can self-supervised forecasting-based anomaly detection identify early bearing degradation more effectively than classification- or RUL-based formulations?**

Ý cần kiểm chứng:

- Classification/RUL cần nhãn rõ.
- Early degradation thường mơ hồ.
- Forecasting error có thể nhạy với thay đổi nhỏ trong tín hiệu.

### RQ2

**Does a CNN/Patching-Mamba architecture improve long-sequence vibration-temperature modeling for bearing degradation detection?**

Ý cần kiểm chứng:

- CNN/patching giữ đặc trưng cục bộ.
- Mamba học phụ thuộc dài hạn với chi phí thấp hơn attention thông thường.
- So sánh với LSTM, TCN, Transformer hoặc CNN baseline.

### RQ3

**Does temperature information improve anomaly-score stability and early degradation detection when fused with vibration signals?**

Ý cần kiểm chứng:

- Vibration phản ánh dao động cơ học nhanh.
- Temperature phản ánh ma sát/nhiệt tích lũy chậm.
- Fusion có thể giảm false alarm hoặc cải thiện detection delay.

### RQ4

**Which anomaly score design is most effective for detecting the Healthy-Degrading transition?**

Các score có thể so sánh:

- Vibration-only forecasting error.
- Temperature-only forecasting error.
- Weighted vibration-temperature error.
- Normalized reconstruction/forecasting error.

### RQ5

**How robust is the proposed framework under leakage-aware temporal evaluation?**

Ý cần kiểm chứng:

- Train trên early/normal segment.
- Validation trên transition segment.
- Test trên late-life segment.
- Báo cáo detection delay, false alarm, AUC/F1 theo threshold.

---

## 10. Contributions sau khi đọc 5 bài

### 10.1. Bản tiếng Anh

```text
The main contributions of this study are as follows:

1. We propose a self-supervised forecasting-based anomaly detection framework for bearing degradation monitoring under a run-to-failure setting, reducing dependence on predefined health-stage labels or RUL targets.

2. We design a CNN/Patching-Mamba architecture to capture both local vibration patterns and long-range temporal degradation dynamics from historical sensor sequences.

3. We investigate vibration-temperature fusion for anomaly-score-based early degradation detection and analyze whether thermal trends improve detection stability.

4. We conduct leakage-aware temporal evaluation with baseline comparison and ablation studies, focusing on the Healthy-Degrading transition, false alarms, and detection delay.
```

### 10.2. Bản tiếng Việt

```text
Các đóng góp chính của nghiên cứu này gồm:

1. Đề xuất một framework phát hiện suy thoái ổ bi dựa trên self-supervised forecasting trong bối cảnh run-to-failure, nhằm giảm phụ thuộc vào nhãn health-stage hoặc RUL target được định nghĩa trước.

2. Thiết kế kiến trúc CNN/Patching-Mamba để khai thác đồng thời đặc trưng dao động cục bộ và động học suy thoái dài hạn từ chuỗi cảm biến quá khứ.

3. Khảo sát vai trò của việc kết hợp vibration-temperature trong phát hiện suy thoái sớm dựa trên anomaly score, đặc biệt phân tích khả năng temperature giúp ổn định cảnh báo.

4. Thực hiện đánh giá theo giao thức tránh rò rỉ thời gian, kết hợp so sánh baseline và ablation study, tập trung vào vùng chuyển tiếp Healthy-Degrading, false alarm và detection delay.
```

---

## 11. Related Work outline dựa trên 5 bài

```text
2. Related Work

2.1. Bearing Health Monitoring and Run-to-Failure Prognostics
- Trình bày bài toán bearing health monitoring.
- Phân biệt fault diagnosis, degradation prediction và RUL prediction.
- Nêu vai trò của run-to-failure dataset.
- Liên hệ bài báo đầu tiên về three-stage classification.

2.2. Deep Learning for Bearing RUL and Degradation Prediction
- Tổng hợp các hướng CNN, LSTM, TCN, Transformer.
- Phân tích các bài TransCN và frequency-adaptive framework.
- Chỉ ra điểm mạnh: học đặc trưng suy thoái, dự đoán RUL tốt.
- Chỉ ra hạn chế: vẫn phụ thuộc RUL target hoặc supervised labels.

2.3. Mamba-Based Models for Bearing Prognostics
- Tổng hợp MSMT, FEMamba, Mamba-SDP.
- Giải thích vì sao Mamba phù hợp với long sequence.
- So sánh với Transformer về chi phí tính toán và khả năng học phụ thuộc dài hạn.
- Chỉ ra khoảng trống: đa số vẫn là RUL/degradation prediction, chưa tập trung forecasting-error anomaly detection.

2.4. Forecasting-Based Anomaly Detection for Time-Series Monitoring
- Giải thích ý tưởng học normal dynamics.
- Trình bày prediction error/anomaly score.
- Nêu các cách đặt threshold, đánh giá false alarm và detection delay.
- Chỉ ra vì sao hướng này phù hợp với early degradation detection.

2.5. Vibration-Temperature Fusion for Early Degradation Detection
- Vibration phản ánh dao động cơ học nhanh.
- Temperature phản ánh xu hướng nhiệt, ma sát và tải tích lũy.
- Phân tích vì sao fusion có thể hỗ trợ vùng Healthy-Degrading.
- Nêu khoảng trống: ít nghiên cứu dùng temperature trong anomaly-score forecasting framework.
```

---

## 12. Draft Introduction sau khi hoàn tất đọc 5 bài

```text
Bearing health monitoring is a critical task in predictive maintenance because bearing degradation can lead to unexpected downtime, safety risks, and costly mechanical failures. Recent studies have increasingly applied deep learning models to bearing fault diagnosis, degradation prediction, and remaining useful life estimation using vibration signals collected from run-to-failure experiments.

Among recent methods, Transformer, Mamba, and multi-scale convolutional architectures have shown promising performance for modeling long temporal dependencies and extracting degradation-related features from bearing sensor data. Mamba-based models are particularly attractive because they can process long sequences efficiently while maintaining the ability to capture temporal dynamics relevant to degradation evolution.

Despite these advances, most existing bearing prognostics studies still formulate the task as supervised RUL regression, fault classification, or predefined degradation-stage prediction. These formulations require target labels, health-stage thresholds, or RUL annotations. However, bearing degradation in run-to-failure settings often evolves gradually, making the transition from Healthy to Degrading ambiguous and difficult to label precisely.

To address this limitation, this study investigates a self-supervised forecasting-based anomaly detection framework for bearing degradation monitoring. Instead of directly predicting health classes or RUL values, the model learns normal vibration-temperature dynamics from historical observations and predicts future sensor behavior. The prediction error is then used as an anomaly score to detect deviations from normal operation.

Motivated by the long-sequence nature of vibration signals and the complementary thermal information provided by temperature, we further design a CNN/Patching-Mamba architecture for multimodal forecasting. The proposed framework aims to capture local vibration patterns, long-range degradation dynamics, and thermal trends for early Healthy-Degrading transition detection under a leakage-aware temporal evaluation protocol.
```

---

## 13. Checklist làm việc của Giảng viên 1

### 13.1. Checklist đọc 5 bài báo

- [ ] Đọc P1: Bearing Degradation Prediction based on Multi-Scale Mamba-Transformer Model.
- [ ] Đọc P2: FEMamba.
- [ ] Đọc P3: Mamba-SDP.
- [ ] Đọc P4: Improved Transformer Encoding Layer and Multi-Scale Convolution.
- [ ] Đọc P5: Frequency-Adaptive Feature Extraction Framework.
- [ ] Điền template đọc paper cho từng bài.
- [ ] Điền bảng comparison matrix 5 bài.
- [ ] Ghi rõ paper nào liên quan trực tiếp, paper nào chỉ dùng làm related work phụ.

### 13.2. Checklist viết gap

- [ ] Tổng hợp các nghiên cứu đã làm được gì.
- [ ] Chỉ ra thiếu sót lặp lại trong 5 bài.
- [ ] Liên hệ thiếu sót đó với bài báo đầu tiên.
- [ ] Viết gap tiếng Việt.
- [ ] Viết gap tiếng Anh.
- [ ] Kiểm tra gap có đủ 3 phần: previous studies, limitation, proposed direction.

### 13.3. Checklist viết RQ và contributions

- [ ] RQ1 bám vào forecasting-based anomaly detection.
- [ ] RQ2 bám vào CNN/Patching-Mamba.
- [ ] RQ3 bám vào vibration-temperature fusion.
- [ ] RQ4 bám vào anomaly score design.
- [ ] RQ5 bám vào leakage-aware temporal evaluation.
- [ ] Contributions không được trùng với RQ, mà phải nói rõ bài này đóng góp gì.

### 13.4. Checklist đồng bộ với nhóm

- [ ] Gửi danh sách 5 bài đã đọc cho Giảng viên 2 để đối chiếu dataset.
- [ ] Gửi RQ2/RQ4 cho Giảng viên 3 để thiết kế model và anomaly score.
- [ ] Gửi RQ5 cho Giảng viên 4 để thiết kế thực nghiệm và metric.
- [ ] Thống nhất lại tên bài, scope và contribution trước khi viết Introduction chính thức.

---

## 14. Thứ tự ưu tiên thực hiện

Nếu thời gian nhiều:

1. Đọc đủ 5 bài.
2. Điền template từng bài.
3. Lập comparison matrix.
4. Rút research gap.
5. Viết RQ.
6. Viết contributions.
7. Viết Related Work outline.
8. Viết Introduction draft.

Nếu thời gian ngắn:

1. Đọc abstract, introduction, method, experiment, conclusion của 5 bài.
2. Điền nhanh comparison matrix.
3. Viết gap tiếng Anh và tiếng Việt.
4. Viết 4 RQ chính.
5. Viết 3 contributions chính.

Ưu tiên bắt buộc:

```text
5-paper comparison matrix → research gap → research questions → contributions
```

---

## 15. Tiêu chí đánh giá gap đã đủ tốt hay chưa

Một research gap được xem là đạt khi trả lời rõ 5 câu hỏi sau:

1. **Các nghiên cứu trước đã làm gì?**
   - Ví dụ: dùng Mamba/Transformer/CNN cho bearing RUL hoặc degradation prediction.

2. **Các nghiên cứu trước còn thiếu gì?**
   - Ví dụ: chưa tập trung self-supervised forecasting-based anomaly detection.

3. **Vì sao thiếu sót đó quan trọng?**
   - Ví dụ: Healthy-Degrading là vùng chuyển tiếp mơ hồ, khó gán nhãn, nhưng rất quan trọng cho cảnh báo sớm.

4. **Bài mới sẽ giải quyết thiếu sót đó như thế nào?**
   - Ví dụ: dùng CNN/Patching-Mamba để forecast vibration-temperature và dùng prediction error làm anomaly score.

5. **Có thể kiểm chứng bằng thực nghiệm không?**
   - Ví dụ: so sánh với classification/RUL/forecasting baselines, đánh giá false alarm, detection delay, AUC/F1 theo temporal split.

Nếu gap chỉ nói chung chung rằng “các nghiên cứu trước chưa tốt” mà không chỉ ra rõ **task nào**, **model nào**, **dataset nào**, **metric nào**, **thiếu ở đâu**, thì gap chưa đạt.
