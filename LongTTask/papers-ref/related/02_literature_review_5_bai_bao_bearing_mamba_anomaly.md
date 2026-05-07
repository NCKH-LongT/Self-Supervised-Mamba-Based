# Literature Review chi tiết cho 5 bài báo liên quan đến hướng nghiên cứu

**Chủ đề nghiên cứu định hướng:**  
**Self-Supervised Forecasting-Based Anomaly Detection for Bearing Degradation using Vibration–Temperature Signals and Long-Sequence Modeling**

**Mục tiêu của file này:**  
Tổng hợp, phân tích và đối chiếu 5 bài báo nền tảng để phục vụ viết **Related Work**, **Research Gap**, **Research Questions** và **Contributions** cho bài báo mới. Năm bài được đọc không chỉ để tóm tắt riêng lẻ, mà còn để trả lời câu hỏi chính:

> Các nghiên cứu hiện tại đã cung cấp nền tảng gì cho bài toán phát hiện suy thoái ổ bi, và còn thiếu khoảng trống nào để đề xuất một framework self-supervised forecasting/anomaly detection dùng vibration–temperature và Mamba?

---

## 1. Danh sách 5 bài báo được review

| STT | Bài báo | Vai trò trong nghiên cứu mới |
|---:|---|---|
| 1 | **Deep Learning and Its Applications to Machine Health Monitoring: A Survey** | Nền tảng về machine health monitoring, diagnosis/prognosis, AE/CNN/RNN, xu hướng deep learning cho dữ liệu máy móc |
| 2 | **Mamba: Linear-Time Sequence Modeling with Selective State Spaces** | Nền tảng kiến trúc long-sequence modeling, selective state space, lý do chọn Mamba thay Transformer/LSTM |
| 3 | **Multimodal Machine Learning: A Survey and Taxonomy** | Nền tảng lý thuyết cho multimodal representation/fusion, giúp biện minh việc kết hợp vibration và temperature |
| 4 | **USAD: UnSupervised Anomaly Detection on Multivariate Time Series** | Nền tảng anomaly detection không giám sát bằng autoencoder, reconstruction error/anomaly score, multivariate time series |
| 5 | **Anomaly Transformer: Time Series Anomaly Detection with Association Discrepancy** | Nền tảng anomaly detection bằng Transformer, association discrepancy, long-range temporal association |

---

# 2. Bài 1 — Deep Learning and Its Applications to Machine Health Monitoring: A Survey

## 2.1. Thông tin chung

**Tên bài:** Deep Learning and Its Applications to Machine Health Monitoring: A Survey  
**Tác giả:** Rui Zhao, Ruqiang Yan, Zhenghua Chen, Kezhi Mao, Peng Wang, Robert X. Gao  
**Loại bài:** Survey  
**Miền ứng dụng:** Machine Health Monitoring, Fault Diagnosis, Prognosis  
**Vai trò với bài mới:** Là bài nền để giải thích vì sao deep learning phù hợp với machine health monitoring và vì sao bài toán diagnosis/prognosis có thể chuyển từ handcrafted features sang representation learning.

## 2.2. Mục tiêu của bài báo

Bài survey này tổng hợp các hướng ứng dụng deep learning trong **Machine Health Monitoring Systems (MHMS)**. Bài báo nhấn mạnh rằng các hệ thống công nghiệp hiện đại tạo ra lượng lớn dữ liệu từ cảm biến, trong khi các phương pháp vật lý truyền thống khó cập nhật online và khó mô hình hóa trong môi trường nhiễu, phức tạp.

Bài báo đặt deep learning như một cầu nối giữa **big machinery data** và **intelligent machine health monitoring**, nhờ khả năng học biểu diễn tự động từ dữ liệu thô hoặc dữ liệu đã xử lý.

## 2.3. Nội dung chính

Bài báo phân loại các hướng deep learning trong MHMS thành 4 nhóm chính:

1. **Autoencoder và biến thể**
   - Học biểu diễn không giám sát.
   - Có thể dùng reconstruction error để đánh giá bất thường.
   - Phù hợp khi nhãn lỗi khan hiếm.

2. **Restricted Boltzmann Machine, Deep Belief Network, Deep Boltzmann Machine**
   - Học biểu diễn tầng sâu.
   - Được dùng nhiều trong các nghiên cứu fault diagnosis giai đoạn đầu.

3. **Convolutional Neural Network**
   - Trích xuất đặc trưng cục bộ từ tín hiệu 1D hoặc ảnh phổ 2D.
   - Phù hợp với vibration signal, spectrogram, STFT, wavelet.
   - Liên quan trực tiếp đến bài báo đầu tiên của nhóm, vốn dùng STFT + CNN.

4. **Recurrent Neural Network, LSTM, GRU**
   - Xử lý dữ liệu chuỗi.
   - Phù hợp với prognosis, RUL prediction, temporal degradation.
   - Bài survey cũng nhắc đến hướng encoder–decoder LSTM học normal behavior và dùng reconstruction error làm health index.

## 2.4. Phương pháp/khung phân tích của bài

Bài không đề xuất một mô hình mới, mà tổng hợp theo kiến trúc deep learning. Điểm quan trọng là bài so sánh:

| Hướng truyền thống | Hướng deep learning |
|---|---|
| Cần handcrafted features | Học representation tự động |
| Các module tách rời: feature design, feature selection, model training | Có thể train end-to-end |
| Phụ thuộc chuyên gia miền | Giảm phụ thuộc chuyên gia |
| Khó mở rộng với big data | Phù hợp dữ liệu cảm biến lớn |
| Thường tách diagnosis/prognosis | Có thể điều chỉnh output layer để chuyển giữa classification và regression |

## 2.5. Điểm mạnh

Bài survey có giá trị lớn ở phần định vị lĩnh vực. Nó cho thấy machine health monitoring có hai nhánh lớn:

- **Diagnosis:** phát hiện hoặc phân loại lỗi sau khi lỗi đã xuất hiện.
- **Prognosis:** dự đoán tình trạng tương lai hoặc Remaining Useful Life.

Đây là điểm rất quan trọng cho bài mới, vì bài đầu tiên của nhóm đang ở hướng **diagnosis/classification**, còn bài mới muốn chuyển sang hướng gần hơn với **prognosis/anomaly detection**.

## 2.6. Hạn chế của bài

Vì là survey cũ, bài chưa bao quát các kiến trúc hiện đại như Transformer, Mamba, foundation sequence model hoặc state space model mới. Ngoài ra, bài chủ yếu tổng hợp các phương pháp DL truyền thống, chưa đi sâu vào:

- self-supervised forecasting,
- anomaly score dựa trên prediction error,
- early degradation detection,
- multimodal vibration–temperature fusion,
- leakage-aware temporal evaluation trong run-to-failure setting.

## 2.7. Liên hệ với hướng nghiên cứu mới

Bài này hỗ trợ phần **background** và **motivation**:

- Chứng minh deep learning là hướng phù hợp cho MHMS.
- Cho thấy AE/RNN/CNN đã được dùng cho diagnosis và prognosis.
- Tạo nền để nói rằng bài mới kế thừa CNN/local feature extraction nhưng mở rộng sang long-sequence modeling.
- Gợi ý rằng reconstruction/forecasting error có thể dùng như health indicator hoặc anomaly score.

## 2.8. Cách dùng trong Related Work

Có thể đưa bài này vào mục:

```text
2.1. Deep Learning for Machine Health Monitoring
```

Đoạn viết gợi ý:

> Deep learning has been widely adopted in machine health monitoring because it can learn hierarchical representations from raw machinery data and reduce the dependence on handcrafted features. Prior surveys have organized DL-based MHMS into autoencoder-, CNN-, RNN-, and RBM-based models, covering both fault diagnosis and prognosis. However, early DL-based MHMS studies mainly focused on classification, regression, or reconstruction with conventional architectures, leaving room for more recent long-sequence and self-supervised approaches.

---

# 3. Bài 2 — Mamba: Linear-Time Sequence Modeling with Selective State Spaces

## 3.1. Thông tin chung

**Tên bài:** Mamba: Linear-Time Sequence Modeling with Selective State Spaces  
**Tác giả:** Albert Gu, Tri Dao  
**Loại bài:** Method/Architecture paper  
**Miền ứng dụng:** General sequence modeling, language, audio, genomics  
**Vai trò với bài mới:** Cơ sở lý thuyết để chọn **Mamba** làm backbone học chuỗi dài vibration–temperature.

## 3.2. Mục tiêu của bài báo

Bài Mamba giải quyết hạn chế của Transformer khi xử lý chuỗi dài. Transformer mạnh nhờ attention, nhưng attention có chi phí tính toán và bộ nhớ tăng theo bình phương độ dài chuỗi. Điều này tạo khó khăn khi áp dụng cho tín hiệu dài như vibration, audio hoặc dữ liệu cảm biến liên tục.

Bài báo đề xuất **Selective State Space Model**, trong đó các tham số state space phụ thuộc vào input, giúp mô hình quyết định thông tin nào nên giữ lại, thông tin nào nên quên.

## 3.3. Ý tưởng cốt lõi

Mamba dựa trên ba ý tưởng chính:

### 3.3.1. Selective State Space

Các state space model trước đó thường là **linear time-invariant**, nghĩa là động học của mô hình không thay đổi theo input tại từng thời điểm. Điều này giúp tính toán hiệu quả, nhưng làm giảm khả năng chọn lọc thông tin.

Mamba thay đổi bằng cách cho một số tham số của SSM phụ thuộc vào input. Nhờ đó, mô hình có thể:

- lọc thông tin nhiễu,
- giữ lại thông tin quan trọng,
- reset hoặc cập nhật trạng thái tùy theo nội dung chuỗi,
- xử lý dependency dài mà không cần attention toàn cục.

### 3.3.2. Hardware-aware selective scan

Việc làm SSM input-dependent khiến mô hình không còn dùng convolution hiệu quả như các SSM trước. Bài báo giải quyết bằng thuật toán **selective scan** tối ưu cho GPU, giúp giữ tính tuyến tính theo chiều dài chuỗi.

### 3.3.3. Kiến trúc Mamba block

Mamba kết hợp selective SSM với gating và projection trong một block đơn giản, không cần attention và không cần MLP block tách rời như Transformer truyền thống.

## 3.4. Điểm mạnh

| Điểm mạnh | Ý nghĩa với bài mới |
|---|---|
| Linear scaling theo sequence length | Phù hợp vibration signal dài |
| Không cần self-attention toàn cục | Giảm chi phí so với Transformer |
| Có selection mechanism | Có khả năng lọc nhiễu và giữ tín hiệu suy thoái quan trọng |
| Thành công trên audio/genomics | Gợi ý phù hợp với continuous signal |
| Có thể xử lý context rất dài | Phù hợp với degradation dynamics kéo dài |

## 3.5. Hạn chế

Bài Mamba là paper nền tảng kiến trúc, không tập trung vào bearing degradation hoặc anomaly detection. Vì vậy, khi dùng cho bài mới cần cẩn thận:

- Không thể nói Mamba đã trực tiếp giải quyết bearing fault detection trong paper gốc.
- Cần thiết kế task-specific framework cho vibration–temperature.
- Cần so sánh với LSTM, TCN, Transformer trong bối cảnh bearing degradation.
- Cần đánh giá detection delay, false alarm và early degradation thay vì chỉ accuracy/perplexity.

## 3.6. Liên hệ với hướng nghiên cứu mới

Bài mới có thể dùng Mamba theo hướng:

```text
Vibration/temperature windows → patching/CNN local encoder → Mamba temporal backbone → forecasting head → prediction error → anomaly score
```

Mamba phù hợp vì:

- vibration có tần số cao, tạo chuỗi dài;
- temperature biến thiên chậm, thể hiện xu hướng dài hạn;
- degradation không xảy ra tức thời mà tích lũy theo thời gian;
- early degradation cần mô hình nhận ra thay đổi nhỏ trong động học chuỗi.

## 3.7. Cách dùng trong Related Work

Có thể đưa vào mục:

```text
2.4. Long-Sequence Modeling with Transformer and Mamba
```

Đoạn viết gợi ý:

> Mamba introduces selective state space models that retain linear-time sequence modeling while allowing input-dependent state updates. This is particularly relevant to vibration-based degradation monitoring, where long sensor sequences must be modeled efficiently and irrelevant fluctuations should be filtered. However, the original Mamba study is not designed for bearing degradation or forecasting-based anomaly detection, motivating task-specific adaptation for vibration–temperature run-to-failure data.

---

# 4. Bài 3 — Multimodal Machine Learning: A Survey and Taxonomy

## 4.1. Thông tin chung

**Tên bài:** Multimodal Machine Learning: A Survey and Taxonomy  
**Tác giả:** Tadas Baltrušaitis, Chaitanya Ahuja, Louis-Philippe Morency  
**Loại bài:** Survey/Taxonomy  
**Miền ứng dụng:** Multimodal learning  
**Vai trò với bài mới:** Cơ sở lý thuyết để biện minh việc kết hợp **vibration** và **temperature**.

## 4.2. Mục tiêu của bài báo

Bài survey này hệ thống hóa lĩnh vực multimodal machine learning. Thay vì chỉ chia đơn giản thành early fusion và late fusion, bài đề xuất 5 nhóm thách thức chính:

1. Representation
2. Translation
3. Alignment
4. Fusion
5. Co-learning

Đối với bài nghiên cứu mới, hai nhóm quan trọng nhất là:

- **Representation:** biểu diễn dữ liệu nhiều modality.
- **Fusion:** kết hợp thông tin từ nhiều modality để dự đoán.

## 4.3. Nội dung chính liên quan đến bài mới

### 4.3.1. Multimodal representation

Bài phân biệt hai kiểu representation:

| Kiểu representation | Ý nghĩa |
|---|---|
| Joint representation | Ghép nhiều modality vào cùng một không gian biểu diễn |
| Coordinated representation | Mỗi modality có không gian riêng nhưng được ràng buộc tương quan |

Trong bài mới, vibration và temperature có bản chất khác nhau:

- vibration: tín hiệu nhanh, dao động mạnh, nhiều nhiễu, giàu thông tin tần số;
- temperature: tín hiệu chậm, thể hiện nhiệt tích lũy, ma sát, tải, xu hướng.

Vì vậy, không nên chỉ concat thô hai loại dữ liệu. Cần có chiến lược fusion phù hợp.

### 4.3.2. Fusion

Fusion là quá trình kết hợp nhiều modality để phục vụ prediction. Với bài mới, fusion có thể xảy ra ở nhiều cấp:

| Cấp fusion | Cách áp dụng |
|---|---|
| Early fusion | Ghép vibration và temperature ở input |
| Feature-level fusion | Mỗi modality có encoder riêng, sau đó ghép embedding |
| Late fusion | Tính score riêng cho vibration và temperature rồi kết hợp |
| Score-level fusion | `score_total = α * score_vibration + β * score_temperature` |
| Cross-modal fusion | Dùng attention/gating để modality này điều chỉnh modality kia |

## 4.4. Điểm mạnh

Bài này giúp tạo nền tảng lý thuyết cho câu hỏi:

> Vì sao cần dùng cả vibration và temperature thay vì vibration-only?

Nó cũng giúp tránh lập luận đơn giản rằng “có thêm sensor thì tốt hơn”. Thay vào đó, có thể lập luận rằng vibration và temperature là hai modality có **complementarity**:

- vibration phản ánh trạng thái cơ học tức thời;
- temperature phản ánh xu hướng nhiệt, ma sát và suy thoái tích lũy;
- kết hợp hai modality có thể tăng robustness, nhất là ở giai đoạn suy thoái sớm.

## 4.5. Hạn chế

Bài survey này không thuộc miền bearing health monitoring. Nó không nói trực tiếp về vibration–temperature hoặc run-to-failure. Vì vậy, nó nên được dùng như **theoretical support** cho multimodal fusion, không nên dùng làm bằng chứng thực nghiệm trực tiếp.

## 4.6. Liên hệ với hướng nghiên cứu mới

Bài mới có thể xây dựng phần fusion như sau:

```text
Vibration encoder: CNN/STFT hoặc 1D patch encoder
Temperature encoder: statistical/trend encoder hoặc temporal encoder
Fusion: concatenate/gated fusion/score-level fusion
Output: forecasting future signal hoặc anomaly score
```

Trong đó cần làm ablation:

- vibration-only,
- temperature-only,
- early fusion,
- late fusion,
- score-level fusion.

## 4.7. Cách dùng trong Related Work

Có thể đưa vào mục:

```text
2.5. Vibration–Temperature Fusion for Bearing Degradation Detection
```

Đoạn viết gợi ý:

> Multimodal learning research emphasizes that heterogeneous modalities can provide complementary and redundant information through representation and fusion. In bearing monitoring, vibration and temperature differ in temporal scale and physical meaning. Vibration captures fast mechanical oscillations, while temperature may reflect slower frictional and thermal trends. This motivates a multimodal forecasting framework rather than a vibration-only anomaly detector.

---

# 5. Bài 4 — USAD: UnSupervised Anomaly Detection on Multivariate Time Series

## 5.1. Thông tin chung

**Tên bài:** USAD: UnSupervised Anomaly Detection on Multivariate Time Series  
**Tác giả:** Julien Audibert, Pietro Michiardi, Frédéric Guyard, Sébastien Marti, Maria A. Zuluaga  
**Hội nghị:** KDD 2020  
**Loại bài:** Method paper  
**Miền ứng dụng:** Multivariate time-series anomaly detection  
**Vai trò với bài mới:** Cơ sở trực tiếp cho anomaly score dựa trên reconstruction error trong multivariate time series.

## 5.2. Mục tiêu của bài báo

USAD giải quyết bài toán phát hiện bất thường không giám sát trên chuỗi thời gian đa biến. Bối cảnh ban đầu là giám sát hệ thống IT quy mô lớn, nơi dữ liệu cảm biến/metrics nhiều chiều, phức tạp và nhãn anomaly khó thu thập.

Mục tiêu của USAD là xây dựng một phương pháp:

- không cần nhãn anomaly khi train,
- học normal behavior,
- phát hiện anomaly bằng reconstruction error,
- train nhanh hơn các mô hình RNN nặng,
- ổn định hơn GAN truyền thống.

## 5.3. Phương pháp

USAD dùng kiến trúc gồm:

```text
Encoder E
Decoder D1
Decoder D2
```

Hai autoencoder chia sẻ encoder:

```text
AE1(W) = D1(E(W))
AE2(W) = D2(E(W))
```

Trong đó `W` là cửa sổ thời gian đa biến.

### 5.3.1. Phase 1 — Autoencoder training

Cả AE1 và AE2 học reconstruct input window bình thường:

```text
L_AE1 = ||W - AE1(W)||²
L_AE2 = ||W - AE2(W)||²
```

### 5.3.2. Phase 2 — Adversarial training

AE1 và AE2 được train theo cơ chế lấy cảm hứng từ GAN:

- AE1 cố gắng đánh lừa AE2;
- AE2 cố phân biệt input thật và input đã reconstruct;
- mục tiêu là làm reconstruction error của anomaly trở nên rõ hơn.

### 5.3.3. Anomaly score

USAD dùng anomaly score kết hợp hai reconstruction error:

```text
A(W) = α ||W - AE1(W)||² + β ||W - AE2(AE1(W))||²
```

Thông số `α` và `β` cho phép điều chỉnh độ nhạy giữa false positives và true positives.

## 5.4. Điểm mạnh

| Điểm mạnh | Ý nghĩa với bài mới |
|---|---|
| Không cần nhãn anomaly | Phù hợp degradation detection khi nhãn Healthy/Degrading mơ hồ |
| Dùng window multivariate time series | Phù hợp vibration–temperature |
| Anomaly score rõ ràng | Có thể kế thừa công thức score |
| Có cơ chế sensitivity α/β | Có thể dùng để phân tích false alarm |
| Train nhanh hơn RNN nặng | Phù hợp khi cần lightweight baseline |

## 5.5. Hạn chế

USAD dùng reconstruction error, không phải forecasting error. Điều này có một hạn chế quan trọng:

- Reconstruction model có thể học tái tạo cả anomaly nếu anomaly gần với normal pattern.
- Với bearing degradation, giai đoạn early degradation có thể rất gần healthy, nên reconstruction error chưa chắc tăng rõ.
- USAD không được thiết kế riêng cho run-to-failure hoặc early degradation detection.
- USAD chưa khai thác long-range temporal dependency mạnh như Transformer/Mamba.
- USAD không xử lý riêng sự khác biệt giữa vibration nhanh và temperature chậm.

## 5.6. Liên hệ với hướng nghiên cứu mới

USAD là baseline rất phù hợp cho bài mới:

```text
Baseline 1: USAD reconstruction-based anomaly detection
Proposed: forecasting-based CNN/Patching-Mamba anomaly detection
```

Bài mới có thể lập luận:

- Reconstruction-based anomaly detection đã chứng minh hiệu quả cho multivariate time series.
- Nhưng trong bearing degradation, phát hiện sớm cần mô hình dự báo normal dynamics và phát hiện lệch khỏi tương lai kỳ vọng.
- Vì vậy, forecasting error có thể nhạy hơn reconstruction error ở vùng Healthy–Degrading.

## 5.7. Cách dùng trong Related Work

Có thể đưa vào mục:

```text
2.3. Forecasting/Reconstruction-Based Anomaly Detection
```

Đoạn viết gợi ý:

> USAD demonstrates that unsupervised autoencoder-based learning can detect anomalies in multivariate time series by amplifying reconstruction errors through adversarial training. This supports the use of normal-behavior modeling and anomaly scores. However, reconstruction-based approaches may still reproduce subtle early degradation patterns, whereas a forecasting-based formulation can explicitly model expected future dynamics and use prediction errors as degradation evidence.

---

# 6. Bài 5 — Anomaly Transformer: Time Series Anomaly Detection with Association Discrepancy

## 6.1. Thông tin chung

**Tên bài:** Anomaly Transformer: Time Series Anomaly Detection with Association Discrepancy  
**Tác giả:** Jiehui Xu, Haixu Wu, Jianmin Wang, Mingsheng Long  
**Hội nghị:** ICLR 2022  
**Loại bài:** Method paper  
**Miền ứng dụng:** Unsupervised time-series anomaly detection  
**Vai trò với bài mới:** Cơ sở cho Transformer-based anomaly detection và lập luận về temporal association.

## 6.2. Mục tiêu của bài báo

Bài báo cho rằng anomaly detection không chỉ cần học representation từng điểm, mà còn cần học **quan hệ temporal** giữa một time point và toàn bộ chuỗi. Các phương pháp reconstruction hoặc prediction error tính theo điểm có thể không đủ vì không mô tả đầy đủ temporal context.

Bài đề xuất **Association Discrepancy** như một tiêu chí anomaly mới.

## 6.3. Ý tưởng cốt lõi

Bài dựa trên quan sát:

- Normal points có thể xây dựng association rộng với toàn bộ chuỗi.
- Anomaly points hiếm và khó liên kết với pattern toàn cục.
- Do đó, association của anomaly thường tập trung vào điểm lân cận.

Từ đó, bài xây dựng hai loại association:

| Thành phần | Ý nghĩa |
|---|---|
| Prior-association | Giả định local/adjacent association bằng Gaussian kernel |
| Series-association | Association học từ self-attention |
| Association discrepancy | Khoảng cách giữa prior-association và series-association |

Anomaly Transformer dùng cơ chế **Anomaly-Attention** để học đồng thời hai association này.

## 6.4. Phương pháp

Bài sử dụng Transformer nhưng thay self-attention bằng Anomaly-Attention.

### 6.4.1. Prior-association

Được mô hình hóa bằng Gaussian kernel theo khoảng cách thời gian. Ý tưởng là anomaly thường chỉ có association gần lân cận.

### 6.4.2. Series-association

Được học từ self-attention map, thể hiện quan hệ thực tế giữa mỗi time point và toàn chuỗi.

### 6.4.3. Association discrepancy

Được tính bằng KL divergence đối xứng giữa prior-association và series-association.

### 6.4.4. Minimax training

Bài dùng chiến lược minimax:

- minimize phase: prior-association học gần series-association;
- maximize phase: series-association được đẩy ra để tăng khả năng phân biệt normal/anomaly.

### 6.4.5. Final anomaly score

Anomaly score kết hợp:

```text
reconstruction error × normalized association discrepancy
```

## 6.5. Điểm mạnh

| Điểm mạnh | Ý nghĩa với bài mới |
|---|---|
| Không chỉ dùng reconstruction error | Gợi ý cần thêm tiêu chí temporal/contextual |
| Dùng Transformer học long-range association | Là baseline mạnh cho anomaly detection |
| Có association-based criterion | Có thể so sánh với prediction-error score |
| Đánh giá trên nhiều dataset anomaly | Là paper mạnh cho Related Work |
| Có minimax để tăng phân biệt normal/anomaly | Gợi ý thiết kế loss function cho anomaly score |

## 6.6. Hạn chế

Bài này có một số điểm cần lưu ý khi áp dụng cho bearing degradation:

- Transformer attention có chi phí cao với chuỗi dài.
- Dữ liệu benchmark không tập trung vào bearing run-to-failure.
- Mục tiêu chính là anomaly point detection, không phải early degradation detection.
- Chưa xử lý multimodal physical signals như vibration–temperature.
- Chưa đánh giá theo trục TTF hoặc detection delay so với mốc Degrading.

## 6.7. Liên hệ với hướng nghiên cứu mới

Anomaly Transformer là baseline/đối trọng quan trọng với Mamba:

```text
Transformer-based anomaly detection → mạnh về association nhưng tốn chi phí
Mamba-based anomaly detection → hướng tới long-sequence efficient modeling
```

Bài mới có thể dùng lập luận:

- Anomaly Transformer cho thấy temporal association quan trọng trong anomaly detection.
- Nhưng với vibration sequence dài, attention có thể tốn chi phí.
- Mamba là lựa chọn hợp lý để giữ khả năng học dài hạn nhưng giảm chi phí.
- Thay vì association discrepancy, bài mới dùng forecasting error làm anomaly score.

## 6.8. Cách dùng trong Related Work

Có thể đưa vào mục:

```text
2.3. Unsupervised Time-Series Anomaly Detection
2.4. Transformer and Mamba for Long-Sequence Modeling
```

Đoạn viết gợi ý:

> Anomaly Transformer extends Transformer-based time-series anomaly detection by introducing association discrepancy, arguing that anomalies exhibit different temporal association patterns from normal points. This highlights the importance of modeling temporal context beyond pointwise reconstruction or prediction errors. Nevertheless, attention-based architectures may be computationally expensive for long vibration sequences, motivating the use of selective state-space models such as Mamba for efficient long-range degradation modeling.

---

# 7. Bảng so sánh 5 bài báo

| Tiêu chí | DL-MHMS Survey | Mamba | Multimodal ML Survey | USAD | Anomaly Transformer |
|---|---|---|---|---|---|
| Loại bài | Survey | Method | Survey | Method | Method |
| Miền chính | Machine health monitoring | Sequence modeling | Multimodal ML | Time-series anomaly | Time-series anomaly |
| Có liên quan bearing? | Có, gián tiếp/nền tảng | Không trực tiếp | Không trực tiếp | Không trực tiếp | Không trực tiếp |
| Có xử lý time series? | Có | Có | Có, nhưng rộng | Có | Có |
| Có unsupervised/self-supervised? | Có nhắc AE | Có pretraining sequence | Có representation learning | Có | Có |
| Có anomaly score? | Có nhắc reconstruction/HI | Không | Không | Có | Có |
| Có forecasting? | Có nhắc prognosis/RUL | Có autoregressive modeling | Không chính | Không, chủ yếu reconstruction | Có nhắc autoregression nhưng method chính là reconstruction + association |
| Có multimodal fusion? | Có nhắc multi-sensor | Có thể áp dụng nhưng không chính | Có | Multivariate nhưng không fusion taxonomy | Multivariate nhưng không fusion vật lý |
| Có long-sequence modeling? | RNN/LSTM | Rất mạnh | Có alignment/sequence | Hạn chế | Transformer attention |
| Hạn chế chính với bài mới | Chưa có Mamba/modern anomaly | Không domain-specific | Không domain-specific | Reconstruction chưa đủ early degradation | Attention cost, không bearing-specific |

---

# 8. Tổng hợp theo nhóm Related Work cho bài báo mới

## 8.1. Deep Learning for Machine Health Monitoring

Bài DL-MHMS Survey cho thấy deep learning đã thay thế dần các pipeline truyền thống dựa trên handcrafted features. Trong machine health monitoring, DL được dùng cho diagnosis và prognosis với AE, CNN, RNN, DBN. Bài này giúp đặt bài mới vào dòng nghiên cứu machine health monitoring dựa trên dữ liệu cảm biến.

**Khoảng trống còn lại:** Các nghiên cứu cũ chưa khai thác tốt self-supervised forecasting, Mamba và multimodal vibration–temperature trong run-to-failure degradation.

## 8.2. Multimodal Vibration–Temperature Fusion

Bài Multimodal ML Survey cung cấp nền tảng taxonomy cho representation và fusion. Với bearing monitoring, vibration và temperature có đặc tính khác nhau về tốc độ biến thiên và ý nghĩa vật lý. Điều này tạo cơ sở cho một framework fusion thay vì vibration-only.

**Khoảng trống còn lại:** Các phương pháp anomaly detection phổ biến thường xử lý multivariate input như một tensor chung, chưa phân tích rõ vai trò vật lý khác biệt của từng modality.

## 8.3. Unsupervised Time-Series Anomaly Detection

USAD và Anomaly Transformer là hai bài quan trọng. USAD đại diện cho reconstruction-based anomaly detection bằng autoencoder. Anomaly Transformer đại diện cho attention/association-based anomaly detection.

**Khoảng trống còn lại:** Các phương pháp này chưa tập trung vào bearing run-to-failure, chưa đánh giá early degradation theo TTF và chưa khai thác forecasting error như tín hiệu phát hiện suy thoái sớm.

## 8.4. Long-Sequence Modeling with Transformer and Mamba

Anomaly Transformer cho thấy Transformer có thể học temporal association, nhưng attention có chi phí cao. Mamba cho thấy selective state space có thể xử lý chuỗi dài với linear scaling và input-dependent selection.

**Khoảng trống còn lại:** Mamba chưa được thiết kế trực tiếp cho self-supervised forecasting-based bearing degradation anomaly detection với vibration–temperature fusion.

---

# 9. Research Gap hoàn chỉnh đề xuất

## 9.1. Research gap tiếng Việt

Phần lớn các nghiên cứu về machine health monitoring và bearing fault diagnosis trước đây mô hình hóa bài toán dưới dạng phân loại có giám sát hoặc dự đoán RUL, trong đó mô hình được yêu cầu gán mỗi cửa sổ tín hiệu vào một trạng thái sức khỏe hoặc dự đoán trực tiếp tuổi thọ còn lại. Cách tiếp cận này hiệu quả khi nhãn rõ ràng và dữ liệu đủ đại diện, nhưng trong bối cảnh run-to-failure, quá trình suy thoái của ổ bi thường diễn ra dần dần, khiến ranh giới giữa Healthy và Degrading trở nên mơ hồ. Vì vậy, các mô hình classification có thể gặp khó khăn trong phát hiện suy thoái sớm, đặc biệt khi biến đổi tín hiệu ban đầu còn nhỏ và dễ bị nhiễu che khuất.

Các nghiên cứu anomaly detection không giám sát như USAD và Anomaly Transformer đã chứng minh rằng việc học normal behavior và sử dụng anomaly score là hướng tiềm năng cho chuỗi thời gian đa biến. Tuy nhiên, các phương pháp này chưa được thiết kế riêng cho dữ liệu bearing run-to-failure, chưa khai thác rõ sự bổ sung giữa vibration và temperature, và chưa đánh giá sâu khả năng phát hiện sớm theo trục time-to-failure. Đồng thời, Transformer-based anomaly detection có thể tốn kém khi xử lý chuỗi vibration dài. Điều này tạo ra khoảng trống cho một framework self-supervised forecasting-based anomaly detection sử dụng CNN/Patching-Mamba để học động học dài hạn của vibration–temperature và phát hiện suy thoái thông qua sự gia tăng của prediction error.

## 9.2. Research gap tiếng Anh

Most prior studies in machine health monitoring and bearing fault diagnosis formulate the problem as supervised classification or remaining useful life prediction, where each signal window is mapped to a predefined health stage or a continuous degradation target. While effective under reliable labels, such formulations are less suitable for run-to-failure settings where bearing degradation evolves gradually and the boundary between normal operation and early degradation is ambiguous. As a result, classification-based methods may struggle to detect early degradation when signal changes are subtle and partially masked by noise.

Unsupervised time-series anomaly detection methods such as USAD and Anomaly Transformer demonstrate the potential of learning normal behavior and deriving anomaly scores from reconstruction errors or temporal association discrepancies. However, these methods are not specifically designed for bearing run-to-failure degradation, do not explicitly exploit the complementary physical roles of vibration and temperature, and rarely evaluate early detection behavior along the time-to-failure axis. Moreover, attention-based anomaly detection can be computationally expensive for long vibration sequences. This motivates a self-supervised forecasting-based anomaly detection framework using CNN/Patching-Mamba to model long-range vibration–temperature dynamics and identify bearing degradation through prediction-error-based anomaly scores.

---

# 10. Research Questions đề xuất

## RQ1

**Can self-supervised forecasting-based anomaly detection detect early bearing degradation more effectively than supervised health-stage classification?**

Ý nghĩa: Câu hỏi này kiểm tra xem việc học normal dynamics và dùng prediction error có nhạy hơn classification trong vùng Healthy–Degrading hay không.

## RQ2

**Does Mamba provide a better trade-off between long-sequence modeling performance and computational efficiency than LSTM, TCN, and Transformer baselines for vibration–temperature time series?**

Ý nghĩa: Câu hỏi này đánh giá lý do chọn Mamba.

## RQ3

**How does vibration–temperature fusion affect early degradation detection compared with vibration-only and temperature-only models?**

Ý nghĩa: Câu hỏi này kiểm tra đóng góp của multimodal fusion.

## RQ4

**Which anomaly score formulation is most effective for bearing degradation detection: vibration prediction error, temperature prediction error, or fused multimodal prediction error?**

Ý nghĩa: Câu hỏi này giúp thiết kế anomaly score.

## RQ5

**How early can the proposed framework detect the transition from Healthy to Degrading under a leakage-aware temporal evaluation protocol?**

Ý nghĩa: Câu hỏi này liên kết trực tiếp với mục tiêu early detection và đánh giá theo TTF.

---

# 11. Contributions đề xuất

## 11.1. Contributions tiếng Việt

1. Đề xuất một framework self-supervised forecasting-based anomaly detection cho phát hiện suy thoái ổ bi trong bối cảnh run-to-failure, giảm phụ thuộc vào nhãn giai đoạn Healthy/Degrading/Fault.

2. Thiết kế kiến trúc CNN/Patching-Mamba để kết hợp trích xuất đặc trưng cục bộ từ tín hiệu vibration với mô hình hóa động học dài hạn của chuỗi vibration–temperature.

3. Xây dựng và phân tích anomaly score dựa trên prediction error đa modality, cho phép so sánh vibration-only, temperature-only và vibration–temperature fusion.

4. Đánh giá mô hình bằng giao thức temporal leakage-aware theo trục time-to-failure, tập trung vào early degradation detection, false alarm và detection delay.

## 11.2. Contributions tiếng Anh

1. We propose a self-supervised forecasting-based anomaly detection framework for bearing degradation detection in a run-to-failure setting, reducing the reliance on predefined Healthy/Degrading/Fault labels.

2. We design a CNN/Patching-Mamba architecture that combines local vibration feature extraction with long-range vibration–temperature temporal modeling.

3. We develop and analyze multimodal prediction-error-based anomaly scores, enabling systematic comparison among vibration-only, temperature-only, and vibration–temperature fusion settings.

4. We conduct leakage-aware temporal evaluation along the time-to-failure axis, emphasizing early degradation detection, false alarms, and detection delay.

---

# 12. Outline Related Work đề xuất

```text
2. Related Work

2.1. Deep Learning for Machine Health Monitoring
- Diagnosis vs prognosis
- Handcrafted features vs deep representation learning
- AE, CNN, RNN in machine health monitoring
- Limitation: supervised labels and conventional sequence models

2.2. Bearing Degradation and Run-to-Failure Monitoring
- Health stages: Healthy, Degrading, Fault
- RUL and degradation modeling
- Limitation: ambiguous early degradation boundary

2.3. Unsupervised Time-Series Anomaly Detection
- Reconstruction-based anomaly detection: AE, USAD
- Prediction-error-based anomaly detection
- Association-based anomaly detection: Anomaly Transformer
- Limitation: not tailored for bearing run-to-failure early degradation

2.4. Long-Sequence Modeling with Transformer and Mamba
- Transformer for temporal association
- Attention cost in long sequences
- Mamba/selective SSM for linear-time sequence modeling
- Motivation for CNN/Patching-Mamba

2.5. Multimodal Vibration–Temperature Fusion
- Multimodal representation and fusion taxonomy
- Vibration as fast mechanical signal
- Temperature as slow thermal/degradation trend
- Need for modality-aware anomaly score
```

---

# 13. Literature Review draft có thể đưa vào bài báo

## 13.1. Draft tiếng Việt

Các phương pháp học sâu đã được ứng dụng rộng rãi trong machine health monitoring nhờ khả năng học biểu diễn tự động từ dữ liệu cảm biến và giảm phụ thuộc vào handcrafted features. Các kiến trúc như Autoencoder, CNN và RNN đã được dùng cho cả fault diagnosis và prognosis, trong đó CNN thường khai thác đặc trưng cục bộ hoặc time–frequency từ vibration, còn RNN/LSTM được dùng để mô hình hóa sự phụ thuộc theo thời gian. Tuy nhiên, nhiều nghiên cứu truyền thống vẫn dựa trên supervised classification hoặc regression, yêu cầu nhãn rõ ràng cho từng trạng thái sức khỏe hoặc RUL.

Trong bối cảnh run-to-failure, quá trình suy thoái ổ bi thường diễn ra dần dần, khiến ranh giới giữa Healthy và Degrading không rõ. Do đó, các mô hình classification có thể khó phát hiện giai đoạn suy thoái sớm. Các phương pháp anomaly detection không giám sát như USAD đã cho thấy tiềm năng của việc học normal behavior và dùng reconstruction error làm anomaly score. Tuy nhiên, reconstruction-based methods có thể tái tạo tốt cả những bất thường nhẹ, làm giảm độ nhạy trong vùng early degradation. Anomaly Transformer mở rộng hướng này bằng cách mô hình hóa temporal association và association discrepancy, cho thấy tầm quan trọng của temporal context trong anomaly detection. Dù vậy, attention-based models có thể tốn chi phí khi xử lý chuỗi vibration dài.

Mamba, với selective state space mechanism và linear-time sequence modeling, mở ra hướng phù hợp cho long-sequence sensor data. Cơ chế selection cho phép mô hình lọc thông tin không liên quan và giữ lại thông tin quan trọng theo ngữ cảnh, điều này đặc biệt hữu ích cho dữ liệu vibration nhiều nhiễu và quá trình degradation kéo dài. Đồng thời, lý thuyết multimodal learning cho thấy các modality khác nhau có thể bổ sung thông tin cho nhau. Trong bearing monitoring, vibration phản ánh dao động cơ học nhanh, còn temperature phản ánh xu hướng nhiệt và ma sát tích lũy. Vì vậy, việc thiết kế một framework forecasting-based anomaly detection kết hợp vibration–temperature bằng CNN/Patching-Mamba là một hướng nghiên cứu có cơ sở và có khoảng trống rõ ràng.

## 13.2. Draft tiếng Anh

Deep learning has been widely applied to machine health monitoring due to its ability to learn hierarchical representations from machinery sensor data and reduce the dependence on handcrafted features. Architectures such as autoencoders, CNNs, and RNNs have been used for both fault diagnosis and prognosis, where CNNs are commonly adopted to extract local or time–frequency vibration features and RNNs are used to capture temporal dependencies. However, many existing approaches still rely on supervised classification or regression, requiring reliable labels for health stages or remaining useful life targets.

In run-to-failure settings, bearing degradation typically evolves gradually, making the boundary between Healthy and Degrading ambiguous. Consequently, classification-based models may struggle to detect early degradation. Unsupervised anomaly detection methods such as USAD demonstrate the potential of learning normal behavior and using reconstruction errors as anomaly scores. Nevertheless, reconstruction-based methods may still reconstruct subtle abnormal patterns, reducing sensitivity to early degradation. Anomaly Transformer further highlights the importance of temporal context by modeling association discrepancy, but attention-based models can be computationally expensive for long vibration sequences.

Mamba, with selective state spaces and linear-time sequence modeling, provides a promising backbone for long sensor sequences. Its selection mechanism allows the model to filter irrelevant fluctuations and retain contextually important information, which is particularly relevant to noisy vibration signals and gradual degradation dynamics. Meanwhile, multimodal learning theory suggests that heterogeneous modalities can provide complementary information. In bearing monitoring, vibration captures fast mechanical oscillations, whereas temperature reflects slower thermal and frictional trends. These observations motivate a self-supervised forecasting-based anomaly detection framework that combines vibration–temperature fusion with CNN/Patching-Mamba and detects degradation through prediction-error-based anomaly scores.

---

# 14. Kết luận sau khi đọc 5 bài

Năm bài báo này tạo thành nền tảng khá đầy đủ cho bài nghiên cứu mới:

- **DL-MHMS Survey** cung cấp nền tảng machine health monitoring.
- **Multimodal ML Survey** cung cấp lý thuyết fusion.
- **USAD** cung cấp nền tảng unsupervised anomaly score bằng reconstruction error.
- **Anomaly Transformer** cung cấp nền tảng temporal association và Transformer-based anomaly detection.
- **Mamba** cung cấp kiến trúc long-sequence efficient backbone.

Tuy nhiên, chưa có bài nào trong 5 bài giải quyết đầy đủ tổ hợp sau:

```text
Bearing run-to-failure
+ vibration–temperature fusion
+ self-supervised forecasting
+ prediction-error anomaly score
+ early degradation detection
+ efficient long-sequence modeling with Mamba
+ leakage-aware temporal evaluation
```

Đây chính là khoảng trống nghiên cứu có thể dùng để phát triển bài báo mới.

---

# 15. Checklist việc tiếp theo

- [ ] Tìm thêm 3–5 bài trực tiếp về **Mamba for bearing RUL/degradation prediction**.
- [ ] Tìm thêm 3–5 bài về **forecasting-based anomaly detection**.
- [ ] Tìm thêm bài dùng **vibration + temperature** trong bearing prognostics.
- [ ] Lập bảng literature matrix gồm: dataset, signal, task, model, supervision, anomaly score, metric, limitation.
- [ ] Chốt baseline: USAD, LSTM-AE/LSTM forecasting, TCN, Transformer/Anomaly Transformer, Mamba.
- [ ] Viết phần Related Work chính thức dựa trên outline ở mục 12.
- [ ] Viết research gap trong Introduction dựa trên mục 9.
