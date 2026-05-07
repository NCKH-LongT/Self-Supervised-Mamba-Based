# Bước 1 - Ghi chú nội bộ về baseline three-stage (không coi là bài đã duyệt/xuất bản)

## 1. Thông tin bản thảo/baseline nội bộ đã đọc

**Tên bản thảo/baseline:** Three-Stage Bearing Health Classification Using Vibration Short-Time Fourier Transform and Temperature Trends in a Run-to-Failure Setting

**Nguồn file:** `LongTTask/papers-ref/Three_Stage_Bearing_Health_Classification_Using_Vibration_STFT_and_Temperature_Trends_in_a_Run_to_Failure_Setting__Final_ (1).pdf`

**Mục tiêu baseline:** Phân loại trạng thái sức khỏe ổ bi trong bối cảnh run-to-failure thành 3 lớp:

- Healthy
- Degrading
- Fault

**Dữ liệu sử dụng:**

- Vibration hai trục.
- Temperature hai kênh.
- Dữ liệu được chuẩn hóa theo trục time-to-failure, gọi là TTF%.

**Cách chia trạng thái theo TTF% trong bài báo:**

| Giai đoạn | Khoảng TTF% |
|---|---:|
| Healthy | 0-60% |
| Degrading | 60-90% |
| Fault | 90-100% |

## 2. Tóm tắt phương pháp của bài báo đầu tiên

Bài báo đầu tiên xây dựng một pipeline classification nhẹ, gồm các bước chính:

1. Chia tín hiệu vibration và temperature thành các cửa sổ 1 giây, overlap 50%.
2. Chuyển vibration hai trục thành STFT log-spectrogram.
3. Resize spectrogram về kích thước 160 x 160.
4. Chuẩn hóa spectrogram theo từng dải tần để ổn định độ sáng phổ.
5. Trích xuất temperature descriptor 6 chiều từ hai kênh temperature:
   - mean
   - standard deviation
   - slope
6. Dùng CNN/ResNet-style 2D encoder để học đặc trưng vibration.
7. Dùng linear layer để embed temperature descriptor.
8. Ghép vibration embedding và temperature embedding bằng late fusion.
9. Dùng classifier để dự đoán Healthy, Degrading hoặc Fault.
10. Gộp kết quả theo file bằng mean-logit hoặc majority vote.

## 3. Điểm mạnh của bài báo đầu tiên

### 3.1. Có giao thức đánh giá tránh rò rỉ dữ liệu thời gian

Bài báo không chỉ dùng random/window-level split mà dùng temporal split theo TTF:

```text
Train: 0-60% TTF
Validation: 60-70% TTF
Test: 70-100% TTF
```

Điểm này quan trọng vì dữ liệu time-series có nguy cơ rò rỉ nếu các cửa sổ overlap xuất hiện cả trong train và test.

### 3.2. Có kết hợp vibration và temperature

Vibration cung cấp bằng chứng dao động cơ học, trong khi temperature cung cấp xu hướng nhiệt liên quan đến ma sát và tải. Bài báo cho thấy temperature giúp cải thiện nhận diện ở late-life, đặc biệt trong vùng Fault.

### 3.3. Kết quả tốt ở giai đoạn cuối vòng đời

Một số kết quả nổi bật:

| Giao thức | Kết quả |
|---|---|
| Stratified development split | Macro-F1 khoảng 0.7762 |
| Temporal test 70-100% TTF | Accuracy 0.8974, Macro-F1 present 0.9044 |
| Early slice 70-90% TTF | Degrading F1 0.9388 |
| Late slice 90-100% TTF | Fault F1 0.9600 |
| Full range 0-100% với majority vote | Accuracy 0.8915, Macro-F1 0.8739 |

### 3.4. Có ablation chứng minh vai trò của temperature

Trong temporal protocol, mô hình vibration-only CNN kém ổn định hơn nhiều so với mô hình multi-modal vibration + temperature. Điều này tạo cơ sở để bài mới tiếp tục khai thác fusion giữa vibration và temperature.

## 4. Hạn chế của bài báo đầu tiên

### 4.1. Vẫn là bài toán classification

Bài báo hiện tại vẫn yêu cầu mô hình dự đoán trực tiếp một trong ba nhãn:

```text
Healthy / Degrading / Fault
```

Cách tiếp cận này phụ thuộc vào việc định nghĩa nhãn theo ngưỡng TTF cố định. Trong thực tế, quá trình suy thoái diễn ra dần dần nên ranh giới giữa Healthy và Degrading không thật sự rõ.

### 4.2. Vùng Healthy-Degrading vẫn là điểm khó

Bài báo chỉ ra rằng phần lớn lỗi còn lại tập trung quanh vùng chuyển tiếp Healthy-Degrading, đặc biệt quanh khoảng 60-70% TTF. Đây là vùng suy thoái sớm, tín hiệu thay đổi chậm và dễ chồng lấn với trạng thái bình thường.

### 4.3. Chưa học trực tiếp động học chuỗi dài

Phương pháp hiện tại dựa trên từng cửa sổ 1 giây và STFT spectrogram. CNN học pattern cục bộ tốt, nhưng chưa khai thác rõ quan hệ dài hạn giữa nhiều cửa sổ theo thời gian.

### 4.4. Chưa dùng forecasting error làm tín hiệu phát hiện bất thường

Bài báo hiện tại dự đoán class label. Bài mới có thể chuyển sang cách tiếp cận:

```text
Input: dữ liệu quá khứ
Output: dữ liệu tương lai
Anomaly score: sai số giữa dữ liệu thật và dữ liệu dự báo
```

Cách này phù hợp hơn với bài toán phát hiện suy thoái sớm vì không cần bắt mô hình quyết định ranh giới class ngay từ đầu.

### 4.5. Dataset hiện mới có một run

Bài báo kết luận rằng nghiên cứu hiện bị giới hạn bởi single-run evaluation và các ngưỡng giai đoạn được chọn theo kinh nghiệm. Đây là điểm cần lưu ý khi viết bài mới.

## 5. Các điểm có thể phát triển thành bài báo mới

| Nội dung trong bài đầu tiên | Hướng phát triển cho bài mới |
|---|---|
| Phân loại Healthy/Degrading/Fault | Chuyển sang forecasting-based anomaly detection |
| Cần nhãn theo TTF threshold | Dùng self-supervised learning, giảm phụ thuộc nhãn |
| CNN học STFT từng window | Thêm mô hình chuỗi dài như Mamba để học temporal dynamics |
| Temperature descriptor chỉ dùng cho classification | Khai thác temperature trong anomaly score hoặc multimodal forecasting |
| Vùng Healthy-Degrading còn khó | Tập trung vào early degradation detection |
| Evaluation theo temporal split đã có | Kế thừa leakage-aware temporal evaluation cho bài mới |
| Có ablation vibration-only vs vibration+temperature | Mở rộng ablation sang forecasting model và anomaly score |

## 6. Hướng phát triển đề xuất cho bài báo mới

### 6.1. Chuyển từ classification sang self-supervised forecasting

Bài mới nên đặt bài toán như sau:

```text
Input X: N điểm/cửa sổ dữ liệu quá khứ gồm vibration_x, vibration_y, temp_1, temp_2
Output Y: K điểm/cửa sổ dữ liệu tương lai
```

Mô hình học dữ liệu bình thường ở giai đoạn Healthy. Khi ổ bi bắt đầu suy thoái, dữ liệu thật sẽ lệch khỏi dự báo, làm prediction error tăng.

### 6.2. Dùng prediction error làm anomaly score

Công thức đơn giản:

```text
Anomaly Score = MSE(Y_true, Y_pred)
```

Có thể tách riêng:

```text
score_vibration = MSE(vibration_true, vibration_pred)
score_temperature = MSE(temperature_true, temperature_pred)
score_total = alpha * score_vibration + beta * score_temperature
```

### 6.3. Dùng Mamba để học chuỗi dài

Lý do:

- Vibration là tín hiệu nhanh, có nhiều điểm dữ liệu.
- Temperature là tín hiệu chậm, thể hiện xu hướng tích lũy.
- Quá trình suy thoái diễn ra theo thời gian dài.
- Mamba phù hợp để xử lý long sequence với chi phí thấp hơn attention-based Transformer.

### 6.4. Giữ ưu điểm leakage-aware temporal split

Bài mới nên kế thừa cách chia theo TTF để tránh rò rỉ:

```text
Train: 0-60% TTF
Validation: 60-70% TTF
Test: 70-100% TTF
```

Nhưng thay vì train classifier, mô hình forecasting sẽ học trên vùng Healthy/early-life và phát hiện bất thường ở vùng Degrading/Fault.

## 7. Kết luận của Bước 1

Bài báo đầu tiên đã xây dựng nền tảng tốt cho hướng bearing health monitoring bằng STFT vibration và temperature fusion. Điểm mạnh là pipeline nhẹ, có temporal split tránh rò rỉ và kết quả tốt ở vùng late-life. Tuy nhiên, bài vẫn là supervised classification nên phụ thuộc vào nhãn và gặp khó ở vùng chuyển tiếp Healthy-Degrading.

Vì vậy, hướng bài báo mới nên phát triển theo trục:

```text
Three-stage classification
→ Self-supervised forecasting
→ Prediction-error-based anomaly detection
→ Early degradation detection
→ Long-sequence modeling with CNN/Patching-Mamba
```

Đây là cơ sở để bước tiếp theo viết **research gap**: các nghiên cứu classification hiện tại khó mô hình hóa ranh giới suy thoái dần dần, trong khi forecasting-based anomaly detection có thể học normal dynamics và phát hiện suy thoái thông qua sai số dự báo.

## 8. Checklist hoàn thành Bước 1

- [x] Đọc bài báo đầu tiên trong thư mục `papers-ref`.
- [x] Tóm tắt bài toán, dữ liệu và phương pháp.
- [x] Ghi lại kết quả chính.
- [x] Xác định điểm mạnh của bài báo đầu tiên.
- [x] Xác định hạn chế của bài báo đầu tiên.
- [x] Rút ra các hướng phát triển cho bài báo mới.
- [x] Xác định cơ sở để viết research gap ở Bước 2.
