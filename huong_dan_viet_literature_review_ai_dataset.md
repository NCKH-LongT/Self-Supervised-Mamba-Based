# Hướng dẫn chi tiết viết Literature Review cho bài báo AI và Dataset

## 1. Mục tiêu của Literature Review

Literature Review không chỉ là phần liệt kê các bài báo liên quan. Đây là phần chứng minh rằng nghiên cứu của mình được xây dựng trên nền tảng học thuật vững chắc, hiểu rõ các công trình trước đó, nhận diện được hạn chế còn tồn tại, và từ đó xác định vị trí đóng góp của bài báo hiện tại.

Với các bài báo liên quan đến AI và dataset, Literature Review cần trả lời được các câu hỏi chính:

1. Các nghiên cứu trước đã giải quyết bài toán gì?
2. Họ sử dụng dataset nào?
3. Dataset đó có đặc điểm, ưu điểm và hạn chế gì?
4. Họ sử dụng mô hình AI nào?
5. Họ xử lý dữ liệu như thế nào trước khi đưa vào mô hình?
6. Họ thiết kế thí nghiệm và đánh giá kết quả ra sao?
7. Hạn chế còn lại là gì?
8. Bài nghiên cứu hiện tại sẽ giải quyết điểm nào trong các hạn chế đó?

Một Literature Review tốt cần dẫn dắt người đọc đi từ **bối cảnh nghiên cứu** đến **khoảng trống nghiên cứu**, thay vì chỉ tóm tắt từng bài báo một cách rời rạc.

---

## 2. Cấu trúc tổng thể của Literature Review

Một Literature Review cho bài báo AI và Dataset nên có cấu trúc như sau:

```markdown
## 2. Literature Review

### 2.1 Background of the Research Problem
### 2.2 Review of Existing Datasets
### 2.3 Data Preprocessing and Feature Representation
### 2.4 Review of AI Models
### 2.5 Experimental Protocols and Evaluation Metrics
### 2.6 Comparative Analysis of Existing Studies
### 2.7 Research Gaps
### 2.8 Positioning of the Current Study
```

Tùy theo độ dài bài báo, có thể gộp một số mục lại. Tuy nhiên, với các bài nghiên cứu AI có dùng dataset, không nên bỏ qua các phần: **dataset**, **preprocessing**, **model**, **evaluation**, và **gap**.

---

## 3. Phần 2.1 - Background of the Research Problem

### 3.1 Mục đích

Phần này dùng để giới thiệu bối cảnh bài toán. Người đọc cần hiểu vì sao bài toán này quan trọng, dữ liệu đầu vào là gì, mô hình AI cần làm gì, và kết quả đầu ra có ý nghĩa như thế nào.

### 3.2 Nội dung cần viết

Cần trình bày các ý sau:

- Bài toán nghiên cứu thuộc lĩnh vực nào?
- Bài toán thực tế cần giải quyết là gì?
- Dữ liệu đầu vào là gì?
- Đầu ra mong muốn là gì?
- Vì sao AI phù hợp để giải quyết bài toán này?
- Vì sao dataset đóng vai trò quan trọng?

### 3.3 Ví dụ nội dung

Ví dụ với bài toán fault diagnosis:

```text
In industrial fault diagnosis, sensor signals such as vibration, temperature, acoustic emission, and motor current are commonly used to monitor machine health conditions. The objective is to classify operating states, detect early-stage degradation, or predict remaining useful life before severe failures occur. Recent advances in artificial intelligence, especially deep learning, have enabled automatic feature learning from raw or transformed sensor data. However, the reliability of AI-based diagnosis systems strongly depends on dataset quality, labeling strategy, data distribution, and evaluation protocol.
```

Ví dụ với bài toán RAG:

```text
Retrieval-Augmented Generation has become an important approach for building domain-specific question-answering systems. Instead of relying only on the parametric knowledge of large language models, RAG systems retrieve relevant external documents and use them as context for answer generation. The performance of such systems depends heavily on document quality, parsing methods, chunking strategy, embedding models, retrieval accuracy, and evaluation metrics.
```

---

## 4. Phần 2.2 - Review of Existing Datasets

### 4.1 Mục đích

Dataset là nền tảng của mọi nghiên cứu AI. Phần này cần phân tích các dataset đã được các nghiên cứu trước sử dụng, không chỉ nêu tên dataset.

### 4.2 Nội dung cần phân tích

Với mỗi dataset, cần xem xét:

- Tên dataset
- Nguồn dataset
- Public hay private
- Lĩnh vực ứng dụng
- Loại dữ liệu
- Kích thước dữ liệu
- Số lượng class hoặc label
- Cách thu thập dữ liệu
- Điều kiện thu thập dữ liệu
- Có dữ liệu thời gian thực hay không
- Có dữ liệu từ môi trường thực tế hay chỉ trong phòng thí nghiệm
- Có mất cân bằng dữ liệu hay không
- Có thiếu dữ liệu, noise, hoặc domain shift hay không
- Có phù hợp với bài toán nghiên cứu hiện tại hay không

### 4.3 Bảng review dataset

Nên tạo bảng như sau:

| Dataset | Domain | Data Type | Size | Label Type | Public/Private | Strength | Limitation |
|---|---|---|---|---|---|---|---|
| CWRU | Bearing fault diagnosis | Vibration | Small | Fault class | Public | Widely used benchmark | Lab condition, limited realism |
| XJTU-SY | Bearing degradation | Vibration | Medium | Run-to-failure | Public | Supports degradation analysis | Limited operating conditions |
| PlantVillage | Crop disease detection | Image | Large | Disease class | Public | Large number of labeled images | Controlled background |
| MIMIC | Healthcare AI | Tabular/Text | Large | Clinical labels | Restricted | Real clinical data | Privacy and access constraints |

### 4.4 Cách viết phân tích dataset

Không nên viết:

```text
Several datasets have been used, such as CWRU, XJTU-SY, and Paderborn.
```

Nên viết:

```text
Several benchmark datasets have been widely adopted for bearing fault diagnosis. The CWRU dataset is commonly used due to its accessibility and well-defined fault categories. However, it was collected under controlled laboratory conditions, which limits its ability to represent real industrial variability. In contrast, run-to-failure datasets such as XJTU-SY provide temporal degradation information and are more suitable for prognostics-oriented studies. Nevertheless, these datasets still cover a limited range of operating conditions, which may restrict cross-domain generalization.
```

### 4.5 Các vấn đề dataset thường dùng để tìm gap

Một số hạn chế phổ biến:

- Dataset quá nhỏ
- Dataset chỉ thu trong phòng thí nghiệm
- Dataset không đại diện cho môi trường thực tế
- Dataset thiếu dữ liệu đa miền
- Dataset thiếu multimodal data
- Dataset mất cân bằng class
- Dataset không có temporal information
- Dataset không có metadata đầy đủ
- Dataset không công khai
- Dataset không cho phép tái lập nghiên cứu
- Label không rõ ràng
- Dữ liệu có nguy cơ leakage khi chia train/test

---

## 5. Phần 2.3 - Data Preprocessing and Feature Representation

### 5.1 Mục đích

Phần này review cách các nghiên cứu trước xử lý dữ liệu trước khi huấn luyện mô hình. Với AI, preprocessing có thể ảnh hưởng rất mạnh đến kết quả.

### 5.2 Với dữ liệu time-series hoặc vibration

Cần xem xét:

- Dữ liệu thô có được lọc nhiễu không?
- Có normalize không?
- Có chia window không?
- Window size và overlap là bao nhiêu?
- Có dùng FFT, STFT, Wavelet, hoặc Hilbert transform không?
- Có chuyển tín hiệu thành ảnh spectrogram không?
- Có dùng feature thống kê không?
- Có data augmentation không?

Ví dụ các kỹ thuật thường gặp:

| Technique | Purpose | Strength | Limitation |
|---|---|---|---|
| Normalization | Scale data | Stabilizes training | May remove absolute magnitude information |
| Window slicing | Generate samples | Increases data size | Risk of leakage if split incorrectly |
| FFT | Frequency analysis | Simple and efficient | Loses temporal information |
| STFT | Time-frequency analysis | Preserves temporal-frequency pattern | More computational cost |
| Wavelet transform | Multi-resolution analysis | Good for non-stationary signals | Requires parameter tuning |

### 5.3 Với dữ liệu image

Cần xem xét:

- Resize ảnh
- Crop ảnh
- Normalize màu
- Augmentation
- Denoising
- Segmentation
- Balance class

### 5.4 Với dữ liệu text hoặc RAG

Cần xem xét:

- Document parsing
- Text cleaning
- Chunking
- Chunk size
- Chunk overlap
- Metadata extraction
- Embedding model
- Vector database
- Retriever
- Reranker
- Prompting strategy

### 5.5 Cách viết phần preprocessing

Ví dụ:

```text
Existing studies differ significantly in how raw data are transformed before model training. Traditional approaches often rely on handcrafted statistical or frequency-domain features, while recent deep learning methods increasingly use raw signals, spectrograms, or multimodal representations. For vibration-based diagnosis, STFT-based spectrograms have been widely adopted because they preserve both temporal and frequency information. However, the choice of window size, overlap ratio, and normalization strategy is often underreported, reducing reproducibility across studies.
```

---

## 6. Phần 2.4 - Review of AI Models

### 6.1 Mục đích

Phần này phân tích các nhóm mô hình AI đã được dùng trong các nghiên cứu trước. Không nên chỉ liệt kê tên mô hình. Cần so sánh xu hướng, ưu điểm, hạn chế và mức độ phù hợp với bài toán.

### 6.2 Nhóm Traditional Machine Learning

Các mô hình thường gặp:

- SVM
- Random Forest
- KNN
- Decision Tree
- XGBoost
- Logistic Regression

Ưu điểm:

- Dễ triển khai
- Dễ giải thích hơn deep learning
- Phù hợp với dataset nhỏ
- Chi phí tính toán thấp

Hạn chế:

- Phụ thuộc nhiều vào feature engineering
- Khó học đặc trưng phức tạp
- Hiệu quả kém hơn khi dữ liệu lớn và phi tuyến

### 6.3 Nhóm Deep Learning

Các mô hình thường gặp:

- CNN
- RNN
- LSTM
- GRU
- Autoencoder
- Transformer
- Vision Transformer
- Graph Neural Network
- Mamba hoặc State Space Models

Ưu điểm:

- Có thể tự học đặc trưng
- Hiệu quả với dữ liệu lớn
- Phù hợp với dữ liệu ảnh, chuỗi thời gian, văn bản và multimodal

Hạn chế:

- Cần nhiều dữ liệu
- Dễ overfit
- Khó giải thích
- Tốn tài nguyên tính toán
- Cần thiết kế thí nghiệm cẩn thận để tránh kết quả ảo

### 6.4 Nhóm Foundation Models, LLM và AI Agent

Dùng cho các bài toán:

- RAG
- Scientific paper assistant
- Chatbot chuyên ngành
- AI Agent
- Code generation
- Multimodal reasoning
- Decision support system

Cần phân tích:

- Mô hình ngôn ngữ sử dụng là gì?
- Embedding model là gì?
- Dữ liệu ngoài được đưa vào bằng cách nào?
- Có tool calling không?
- Có agent planner không?
- Có đánh giá hallucination không?
- Có đo chi phí token, latency, và độ tin cậy không?

### 6.5 Cách viết phần model review

Không nên viết:

```text
Author A used CNN. Author B used LSTM. Author C used Transformer.
```

Nên viết:

```text
The development of AI-based methods shows a clear transition from traditional machine learning to deep learning architectures. Early studies relied on handcrafted features combined with classifiers such as SVM and Random Forest. More recent studies use CNN-based models to automatically extract spatial or time-frequency representations from transformed signals. Sequence models such as LSTM and Transformer have also been explored to capture temporal dependencies. However, despite their promising performance, many deep learning models are evaluated under random split settings, which may overestimate their ability to generalize to unseen operating conditions.
```

---

## 7. Phần 2.5 - Experimental Protocols and Evaluation Metrics

### 7.1 Mục đích

Phần này đánh giá cách các bài báo thiết kế thí nghiệm và đo hiệu quả mô hình. Đây là phần rất quan trọng để phát hiện research gap.

### 7.2 Các câu hỏi cần kiểm tra

Với mỗi bài báo, cần hỏi:

- Dữ liệu được chia train/validation/test như thế nào?
- Có dùng random split không?
- Có dùng temporal split không?
- Có chia theo file, subject, machine, hoặc operating condition không?
- Có nguy cơ data leakage không?
- Có so sánh với baseline không?
- Có so sánh với state-of-the-art không?
- Có kiểm tra robustness không?
- Có ablation study không?
- Có báo cáo cấu hình thí nghiệm đầy đủ không?
- Có public code không?

### 7.3 Các chiến lược chia dữ liệu phổ biến

| Split Strategy | Description | Strength | Risk |
|---|---|---|---|
| Random split | Randomly divide samples | Simple and common | High leakage risk in windowed data |
| Cross-validation | Multiple train/test folds | More stable estimate | May still leak if samples are correlated |
| Temporal split | Train on early period, test on later period | More realistic for time-series | Harder task |
| Subject-wise split | Separate subjects between train and test | Tests generalization | Needs enough subjects |
| Domain split | Train and test on different domains | Tests robustness | May reduce accuracy significantly |
| File-wise split | Split by original files | Reduces leakage | Requires enough files |

### 7.4 Evaluation metrics theo từng bài toán

#### Classification

- Accuracy
- Precision
- Recall
- F1-score
- Macro-F1
- Weighted-F1
- Confusion matrix
- AUC

#### Fault diagnosis hoặc imbalanced data

- Macro-F1
- Per-class F1
- Recall for fault class
- False alarm rate
- Miss detection rate
- Confusion matrix

#### Regression hoặc forecasting

- MAE
- RMSE
- MAPE
- R²

#### RAG hoặc LLM

- Answer correctness
- Faithfulness
- Context precision
- Context recall
- Hallucination rate
- Latency
- Token cost
- Human evaluation score

#### AI Agent

- Task success rate
- Tool-use accuracy
- Planning correctness
- Number of reasoning steps
- Cost per task
- Failure recovery rate
- Safety violation rate

### 7.5 Cách viết phần evaluation

```text
Although many studies report high classification accuracy, their experimental protocols are not always comparable. A common issue is the use of random window-level splitting, where overlapping or highly similar segments from the same original signal may appear in both training and testing sets. This setting can inflate performance and may not reflect real-world deployment scenarios. More rigorous protocols, such as temporal split, file-wise split, or cross-domain evaluation, are needed to assess the true generalization capability of AI models.
```

---

## 8. Phần 2.6 - Comparative Analysis of Existing Studies

### 8.1 Mục đích

Phần này tổng hợp và so sánh các nghiên cứu trước theo nhóm. Đây là phần chứng minh người viết không chỉ đọc từng bài riêng lẻ mà còn hiểu được xu hướng chung của lĩnh vực.

### 8.2 Literature Matrix

Nên tạo bảng Literature Matrix như sau:

| ID | Paper | Year | Dataset | Data Type | Model | Preprocessing | Split Strategy | Metrics | Key Result | Limitation | Relevance |
|---|---|---|---|---|---|---|---|---|---|---|---|
| P01 | Author A | 2022 | CWRU | Vibration | CNN | STFT | Random | Accuracy | High accuracy | Leakage risk | Baseline |
| P02 | Author B | 2023 | XJTU-SY | Vibration | LSTM | Windowing | Temporal | F1 | Good degradation tracking | Limited domain | Temporal comparison |
| P03 | Author C | 2024 | Custom | Multimodal | Transformer | Normalization | Cross-domain | Macro-F1 | Better robustness | High cost | Related method |

### 8.3 Cách phân nhóm bài báo

Có thể phân nhóm theo:

#### Theo dataset

- Benchmark dataset
- Real-world dataset
- Private dataset
- Synthetic dataset
- Multimodal dataset

#### Theo model

- Traditional ML
- CNN-based models
- Sequence models
- Transformer-based models
- Hybrid models
- Foundation models

#### Theo vấn đề nghiên cứu

- Accuracy improvement
- Domain adaptation
- Data scarcity
- Explainability
- Robustness
- Deployment efficiency
- Evaluation reliability

#### Theo kỹ thuật xử lý dữ liệu

- Raw signal learning
- Handcrafted feature engineering
- Time-frequency representation
- Data augmentation
- Multimodal fusion

### 8.4 Cách viết Comparative Analysis

Không nên viết theo kiểu từng bài:

```text
Paper A did this. Paper B did that. Paper C did another thing.
```

Nên viết theo nhóm:

```text
Existing studies can be grouped into three main categories. The first group relies on traditional machine learning models with handcrafted features, which are computationally efficient but limited in representation learning. The second group uses deep learning architectures such as CNN and LSTM to automatically learn discriminative features from raw or transformed data. The third group explores Transformer-based and hybrid models to improve long-range dependency modeling and generalization. Despite these advances, most studies still depend on limited benchmark datasets and do not sufficiently evaluate robustness under domain shift or realistic deployment conditions.
```

---

## 9. Phần 2.7 - Research Gaps

### 9.1 Mục đích

Phần này rút ra các khoảng trống nghiên cứu từ toàn bộ phần review. Research gap phải được suy ra từ bằng chứng trong các nghiên cứu trước, không nên viết cảm tính.

### 9.2 Công thức viết gap

Một research gap tốt có cấu trúc:

```text
Although previous studies have achieved [result] using [method/model], most of them rely on [limitation]. This creates a problem because [reason]. Therefore, there is a need for [new direction].
```

### 9.3 Ví dụ gap về dataset

```text
Although existing AI-based studies have achieved promising results on benchmark datasets, many of them rely on controlled laboratory data. This limits the generalizability of trained models because real-world environments often contain noise, varying operating conditions, and distribution shifts. Therefore, there is a need for evaluation on more realistic datasets or cross-domain validation protocols.
```

### 9.4 Ví dụ gap về evaluation

```text
Although many studies report high accuracy in fault classification, a large proportion of them use random sample-level splitting. This may introduce data leakage when adjacent windows from the same original signal appear in both training and testing sets. Therefore, more leakage-aware protocols such as file-wise, temporal, or domain-based splitting are required.
```

### 9.5 Ví dụ gap về model

```text
Although deep learning models can automatically learn discriminative representations, many existing architectures are computationally expensive and difficult to deploy in resource-constrained environments. Therefore, lightweight and efficient models should be further explored for practical deployment.
```

### 9.6 Ví dụ gap về RAG

```text
Although RAG systems have improved the factual grounding of LLM-based applications, many studies focus mainly on answer generation quality while underreporting retrieval quality, chunking strategy, latency, and cost. Therefore, a more comprehensive evaluation framework is needed to assess both answer correctness and system-level efficiency.
```

### 9.7 Các loại research gap phổ biến

| Gap Type | Meaning | Example |
|---|---|---|
| Dataset gap | Dataset chưa đủ tốt hoặc chưa thực tế | Lab dataset, small dataset, missing modality |
| Method gap | Phương pháp còn hạn chế | Model chưa xử lý tốt domain shift |
| Evaluation gap | Cách đánh giá chưa chặt | Random split gây leakage |
| Reproducibility gap | Khó tái lập kết quả | Không public code hoặc thiếu config |
| Interpretability gap | Mô hình khó giải thích | Black-box decision |
| Deployment gap | Khó triển khai thực tế | Model quá nặng, latency cao |
| Multimodal gap | Chưa tận dụng nhiều nguồn dữ liệu | Chỉ dùng vibration, bỏ qua temperature |
| Robustness gap | Chưa kiểm tra độ bền mô hình | Không test noise hoặc domain shift |

---

## 10. Phần 2.8 - Positioning of the Current Study

### 10.1 Mục đích

Phần này nối Literature Review với bài nghiên cứu hiện tại. Sau khi đã chỉ ra gap, cần giải thích bài của mình giải quyết gap nào và đóng góp ra sao.

### 10.2 Nội dung cần có

Cần trả lời:

- Bài nghiên cứu hiện tại tập trung vào gap nào?
- Vì sao gap đó quan trọng?
- Bài này dùng dataset nào?
- Bài này cải tiến ở preprocessing, model, evaluation, hoặc deployment?
- Đóng góp chính là gì?
- Khác gì so với các nghiên cứu trước?

### 10.3 Mẫu viết

```text
Based on the above review, three major limitations can be identified. First, many existing studies rely on controlled benchmark datasets that may not fully represent real-world data variability. Second, several studies use random sample-level splitting, which may lead to optimistic performance estimation due to data leakage. Third, limited attention has been given to multimodal fusion and temporal evaluation. To address these limitations, this study proposes a leakage-aware AI framework using [dataset/method], where [main contribution] is designed to improve [target outcome].
```

---

## 11. Checklist đọc từng bài báo

Khi đọc mỗi bài báo, nên điền theo mẫu sau:

```markdown
# Paper Review Form

## 1. Basic Information

- Paper ID:
- Title:
- Authors:
- Year:
- Venue:
- DOI/Link:

## 2. Research Problem

- Bài báo giải quyết vấn đề gì?
- Bài toán thuộc loại nào?
  - Classification
  - Regression
  - Detection
  - Forecasting
  - Retrieval
  - Generation
  - Agentic task
- Vì sao vấn đề này quan trọng?

## 3. Dataset

- Dataset được sử dụng:
- Public hay private:
- Loại dữ liệu:
- Kích thước:
- Số class/label:
- Cách thu thập:
- Điều kiện thu thập:
- Có noise/domain shift/missing data không?
- Hạn chế của dataset:

## 4. Preprocessing

- Dữ liệu được làm sạch như thế nào?
- Có normalization không?
- Có chia window/chunk không?
- Có feature engineering không?
- Có augmentation không?
- Có mô tả đủ để tái lập không?

## 5. Method / Model

- Mô hình chính:
- Kiến trúc tổng quan:
- Input của model:
- Output của model:
- Có baseline không?
- Có ablation study không?

## 6. Experiment Design

- Train/test split:
- Validation strategy:
- Metrics:
- Baseline comparison:
- Có nguy cơ data leakage không?
- Có kiểm tra robustness không?

## 7. Results

- Kết quả chính:
- Model tốt hơn baseline ở điểm nào?
- Kết quả có thuyết phục không?
- Có báo cáo per-class performance không?

## 8. Limitations

- Hạn chế về dataset:
- Hạn chế về model:
- Hạn chế về evaluation:
- Hạn chế về reproducibility:
- Hạn chế về deployment:

## 9. Relevance to My Study

- Bài này liên quan đến nghiên cứu của mình ở điểm nào?
- Có thể kế thừa gì?
- Có thể phản biện gì?
- Có thể dùng làm baseline không?
- Có giúp hình thành research gap không?
```

---

## 12. Quy trình viết Literature Review từng bước

## Bước 1: Xác định phạm vi review

Cần xác định rõ:

- Chủ đề chính là gì?
- Domain là gì?
- Bài toán AI là gì?
- Dataset nào liên quan?
- Thời gian ưu tiên bài báo là bao lâu?
- Chỉ review bài Q1/Q2 hay cả conference?
- Có bao gồm survey paper không?

Ví dụ:

```text
Scope: AI-based vibration signal fault diagnosis using public bearing datasets, with focus on dataset quality, preprocessing, model architecture, and leakage-aware evaluation.
```

## Bước 2: Tìm bài báo nền tảng

Nên tìm các loại bài:

- Survey paper
- Systematic literature review
- Benchmark paper
- Dataset paper
- State-of-the-art method paper
- Recent application paper

Keyword gợi ý:

```text
AI fault diagnosis dataset
bearing fault diagnosis deep learning dataset
vibration signal classification benchmark
domain shift fault diagnosis
cross-domain bearing fault diagnosis
RAG evaluation dataset
LLM retrieval augmented generation benchmark
AI agent evaluation dataset
```

## Bước 3: Lọc bài báo

Tiêu chí chọn bài:

- Có liên quan trực tiếp đến bài toán
- Có dataset rõ ràng
- Có phương pháp AI rõ ràng
- Có experimental protocol rõ ràng
- Có kết quả và metric cụ thể
- Có giá trị để so sánh hoặc tìm gap

Tiêu chí loại bài:

- Không có dataset rõ ràng
- Không mô tả thí nghiệm
- Không có metric đáng tin cậy
- Chỉ nói chung chung
- Không liên quan đến hướng nghiên cứu

## Bước 4: Điền Literature Matrix

Mỗi bài báo được đọc nên được đưa vào bảng matrix.

```markdown
| ID | Paper | Year | Dataset | Data Type | Model | Preprocessing | Split | Metrics | Result | Limitation | Use in My Paper |
|---|---|---|---|---|---|---|---|---|---|---|---|
| P01 | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... |
```

## Bước 5: Nhóm các bài báo

Không viết literature review theo thứ tự đọc bài. Nên nhóm theo chủ đề:

- Nhóm theo dataset
- Nhóm theo model
- Nhóm theo preprocessing
- Nhóm theo evaluation
- Nhóm theo research problem

## Bước 6: Viết phân tích từng nhóm

Mỗi nhóm nên có cấu trúc:

```text
[1] Nhóm nghiên cứu này làm gì.
[2] Họ thường dùng dataset/model nào.
[3] Kết quả hoặc đóng góp chính là gì.
[4] Hạn chế chung của nhóm này là gì.
[5] Liên quan thế nào đến bài nghiên cứu hiện tại.
```

## Bước 7: Rút ra gap

Sau khi phân tích, rút ra 2-4 gap chính. Không nên đưa quá nhiều gap.

Một gap tốt phải:

- Cụ thể
- Có bằng chứng từ literature
- Liên quan trực tiếp đến bài của mình
- Có thể giải quyết trong phạm vi nghiên cứu
- Không quá rộng

## Bước 8: Kết nối gap với contribution

Mỗi gap nên dẫn đến một contribution.

Ví dụ:

| Research Gap | Contribution |
|---|---|
| Random split gây leakage | Đề xuất temporal/file-wise split |
| Dataset thiếu multimodal fusion | Kết hợp vibration + temperature |
| Model nặng khó triển khai | Đề xuất lightweight model |
| RAG chỉ đánh giá answer quality | Đánh giá cả retrieval, cost, latency |

---

## 13. Mẫu đoạn văn Literature Review hoàn chỉnh

### 13.1 Mẫu đoạn về dataset

```text
Public benchmark datasets have played an important role in the development of AI-based fault diagnosis methods. Datasets such as CWRU and Paderborn are widely used because they provide labeled vibration signals under controlled fault conditions. These datasets enable fair comparison among different models and are useful for early-stage algorithm development. However, their controlled laboratory settings may not fully capture real-world industrial variations, such as changing loads, sensor noise, and environmental disturbances. As a result, models trained and evaluated only on these datasets may show limited generalization in practical deployment scenarios.
```

### 13.2 Mẫu đoạn về model

```text
Existing AI-based methods have gradually shifted from traditional machine learning to deep learning architectures. Earlier studies relied on handcrafted time-domain and frequency-domain features combined with classifiers such as SVM, Random Forest, and KNN. More recent studies employ CNN, LSTM, Transformer, and hybrid architectures to automatically learn discriminative representations from raw or transformed data. While these models have achieved promising results, their performance is often highly dependent on dataset quality, preprocessing choices, and evaluation protocols.
```

### 13.3 Mẫu đoạn về evaluation

```text
Despite the high accuracy reported in many studies, evaluation protocols remain a critical concern. In particular, random sample-level splitting is commonly used in window-based signal classification tasks. When overlapping windows from the same original signal are randomly assigned to both training and testing sets, the resulting performance may be overly optimistic. Therefore, more rigorous evaluation strategies, such as file-wise split, temporal split, or cross-domain validation, are necessary to better estimate real-world generalization.
```

### 13.4 Mẫu đoạn kết thúc Literature Review

```text
In summary, existing studies have demonstrated the potential of AI models for automated diagnosis and prediction tasks. However, several limitations remain unresolved, including limited dataset realism, insufficient evaluation under domain shift, possible data leakage in random split protocols, and limited analysis of model efficiency. These limitations motivate the present study, which aims to develop and evaluate a more robust framework under a leakage-aware and dataset-conscious experimental setting.
```

---

## 14. Các lỗi thường gặp khi viết Literature Review

### Lỗi 1: Chỉ tóm tắt từng bài riêng lẻ

Không nên viết:

```text
Author A used CNN. Author B used LSTM. Author C used Transformer.
```

Cách sửa:

```text
Existing studies show a transition from CNN-based local feature learning to sequence-based architectures such as LSTM and Transformer, which are designed to better capture temporal dependencies.
```

### Lỗi 2: Không phân tích dataset

Với bài AI, nếu không phân tích dataset thì Literature Review sẽ yếu. Cần luôn xem dataset có phù hợp, thực tế và tái lập được không.

### Lỗi 3: Chỉ nói kết quả accuracy

Accuracy cao không đủ. Cần xem:

- Dữ liệu có cân bằng không?
- Có per-class F1 không?
- Có confusion matrix không?
- Có leakage không?
- Có test trên domain khác không?

### Lỗi 4: Gap quá chung chung

Không nên viết:

```text
More research is needed to improve AI models.
```

Nên viết:

```text
There is a need for leakage-aware evaluation protocols because random window-level splitting may overestimate model performance in vibration signal classification.
```

### Lỗi 5: Không kết nối gap với bài của mình

Gap phải dẫn đến contribution. Nếu gap không liên quan đến bài mình thì không nên đưa vào.

---

## 15. Checklist hoàn thiện Literature Review

Trước khi hoàn thành, kiểm tra các câu hỏi sau:

- [ ] Literature Review có giới thiệu bối cảnh bài toán không?
- [ ] Có review dataset không?
- [ ] Có phân tích ưu điểm và hạn chế của dataset không?
- [ ] Có review preprocessing không?
- [ ] Có review các nhóm model không?
- [ ] Có so sánh experimental protocol không?
- [ ] Có phân tích evaluation metrics không?
- [ ] Có Literature Matrix không?
- [ ] Có chỉ ra research gap rõ ràng không?
- [ ] Gap có được suy ra từ literature không?
- [ ] Gap có liên quan trực tiếp đến bài hiện tại không?
- [ ] Có positioning của nghiên cứu hiện tại không?
- [ ] Có tránh viết kiểu liệt kê từng bài không?
- [ ] Có dẫn dắt logic từ previous studies đến current study không?

---

## 16. Template ngắn có thể dùng ngay

```markdown
## 2. Literature Review

### 2.1 Background of the Research Problem
Introduce the research domain, AI task, input data, output objective, and the importance of dataset quality.

### 2.2 Existing Datasets
Review public and private datasets used in previous studies. Compare their data types, size, labels, collection conditions, strengths, and limitations.

### 2.3 Data Preprocessing and Feature Representation
Discuss how previous studies transform raw data into model-ready inputs, including cleaning, normalization, windowing, feature extraction, augmentation, chunking, or embedding.

### 2.4 AI Models and Learning Approaches
Review traditional machine learning, deep learning, Transformer/Mamba/foundation models, hybrid models, and multimodal approaches.

### 2.5 Experimental Protocols and Evaluation Metrics
Compare data splitting strategies, baselines, metrics, validation methods, robustness tests, and reproducibility.

### 2.6 Comparative Analysis
Synthesize prior works by grouping them according to dataset, model type, preprocessing strategy, or evaluation protocol. Highlight common trends and limitations.

### 2.7 Research Gaps
Identify specific gaps related to dataset realism, domain shift, data leakage, model efficiency, explainability, reproducibility, or deployment.

### 2.8 Positioning of the Current Study
Explain how the current study addresses the identified gaps and what contributions it provides compared with previous studies.
```

---

## 17. Kết luận

Một Literature Review mạnh cho bài báo AI và Dataset cần đi theo logic:

```text
Bài toán → Dataset → Preprocessing → Model → Experiment → Evaluation → Limitation → Gap → Contribution
```

Không nên xem Literature Review là phần tổng hợp bài báo đơn thuần. Đây là phần giúp người đọc thấy rõ vì sao nghiên cứu hiện tại cần thiết, khác biệt và có giá trị học thuật.
