
# 🛡️ Intrusion Detection in Network Security using Machine Learning

This project presents a comparative study of two machine learning algorithms—**K-Nearest Neighbors (KNN)** and **Kernel Density Estimation (KDE) Naïve-Bayes**—for the purpose of network intrusion detection. The goal is to classify network traffic and identify potential security threats.

-----

## 🎯 Project Overview

In an era dominated by technology, cybersecurity is paramount. This study leverages machine learning classification techniques to distinguish between normal and malicious network activity, aiming to prevent cyber attacks.

The project compares two distinct classification algorithms:

  * **K-Nearest Neighbors (KNN)**: A non-parametric algorithm that classifies data points based on the majority class of their 'k' nearest neighbors, using Euclidean distance. [cite\_start]It performs well with complex decision boundaries but can be computationally expensive with large datasets[cite: 70, 71, 72].
  * **KDE Naïve-Bayes**: An enhancement of the traditional Naïve-Bayes algorithm. [cite\_start]Instead of assuming a simple Gaussian distribution, it uses Kernel Density Estimation (in this case, with a Gaussian kernel) to model more complex, non-Gaussian data distributions often found in network traffic data[cite: 74, 75].

[cite\_start]The performance of these models is evaluated using metrics such as **accuracy, precision, recall, and F1-score**, supplemented by confusion matrices for a detailed analysis[cite: 78].

-----

## 💿 Dataset: NSL-KDD

[cite\_start]This study uses the **NSL-KDD dataset**, a standard benchmark for intrusion detection systems[cite: 79].

  * [cite\_start]**Structure**: The dataset contains 19,000 instances, each with 41 features[cite: 81, 82].
  * [cite\_start]**Classes**: The data is categorized into five labels: **Normal, DoS (Denial of Service), Probe, R2L (Remote to Local), and U2R (User to Root)**[cite: 80].
  * [cite\_start]**Imbalance**: The dataset is highly imbalanced, with the **U2R** class having a very small number of samples, making its detection a significant challenge[cite: 83, 84].

### Dataset Distribution

-----

## ⚙️ Methodology

### Preprocessing

Before training the models, several preprocessing steps were applied:

1.  [cite\_start]**Data Cleaning & Label Mapping**: Invalid and missing labels were refined to help the models focus on general attack patterns[cite: 99, 100, 101].
2.  [cite\_start]**Feature Encoding**: Categorical features like `"protocol_type"` and `"service"` were converted into numerical values[cite: 102].
3.  [cite\_start]**Normalization**: All features were scaled to ensure they contribute equally to the model's distance calculations, which is particularly important for KNN[cite: 102].

### Model Implementation

  * [cite\_start]**KNN**: The classifier was trained using **5 nearest neighbors (k=5)**[cite: 109].
  * **KDE Naïve-Bayes**: A custom classifier was built. [cite\_start]It uses **Principal Component Analysis (PCA)** to reduce dimensionality, and then fits a separate Gaussian KDE model for each feature within each class[cite: 105, 106]. [cite\_start]The final prediction is based on the class with the highest computed probability[cite: 107, 108].

[cite\_start]The data was split into **60% for training, 20% for validation, and 20% for testing**[cite: 82].

-----

## 📊 Results & Analysis

### KNN Performance Analysis

[cite\_start]The KNN model demonstrated exceptional performance across the board, achieving an overall **accuracy of 98%** on the train, validation, and test sets[cite: 210, 273, 285, 325].

  * [cite\_start]**Strengths**: The model showed nearly perfect precision and recall for detecting **DoS, Normal, Probe, and R2L** traffic[cite: 211]. [cite\_start]The confusion matrices show a strong diagonal, indicating that most samples were classified correctly[cite: 337].
  * [cite\_start]**Weaknesses**: As predicted, the model struggled to identify **U2R** attacks due to the insufficient number of samples, resulting in a recall of 0% on the validation and test sets[cite: 214].

#### KNN Metrics

| **TRAIN Metrics** | **precision** | **recall** | **f1-score** |
| :--- | :---: | :---: | :---: |
| DoS | 0.98 | 0.99 | 0.99 |
| Normal | 0.99 | 0.99 | 0.99 |
| Probe | 0.95 | 0.94 | 0.94 |
| R2L | 0.98 | 0.98 | 0.98 |
| U2R | 0.88 | 0.33 | 0.48 |
| **accuracy** | | | **0.98** |

| **TEST Metrics** | **precision** | **recall** | **f1-score** |
| :--- | :---: | :---: | :---: |
| DoS | 0.98 | 0.99 | 0.98 |
| Normal | 0.98 | 0.98 | 0.98 |
| Probe | 0.94 | 0.90 | 0.92 |
| R2L | 0.97 | 0.98 | 0.98 |
| U2R | 0.00 | 0.00 | 0.00 |
| **accuracy** | | | **0.98** |

#### KNN Confusion Matrices (Train / Test)

### KDE Naïve-Bayes Performance Analysis

[cite\_start]The KDE Naïve-Bayes model showed significantly weaker performance, with a consistent **accuracy of around 58-59%** across all datasets, indicating poor generalization[cite: 463, 467].

  * [cite\_start]**Strengths**: The model was effective at identifying **Probe** attacks (100% recall) and reasonably good at detecting **R2L** traffic[cite: 465, 468].
  * **Weaknesses**: It suffered from major inconsistencies. [cite\_start]The high recall for 'Probe' came with very low precision (0.19), meaning many other attack types were misclassified as 'Probe'[cite: 465]. [cite\_start]The model was particularly poor at identifying **DoS** and **U2R** attacks[cite: 724]. [cite\_start]The confusion matrices reveal significant misclassifications between multiple classes[cite: 589].

#### KDE Naïve-Bayes Metrics

| **TRAIN Metrics** | **precision** | **recall** | **f1-score** |
| :--- | :---: | :---: | :---: |
| DoS | 0.41 | 0.18 | 0.25 |
| Normal | 0.95 | 0.71 | 0.82 |
| Probe | 0.19 | 1.00 | 0.32 |
| R2L | 0.62 | 0.85 | 0.72 |
| U2R | 0.40 | 0.48 | 0.43 |
| **accuracy** | | | **0.59** |

| **TEST Metrics** | **precision** | **recall** | **f1-score** |
| :--- | :---: | :---: | :---: |
| DoS | 0.40 | 0.18 | 0.25 |
| Normal | 0.95 | 0.72 | 0.82 |
| Probe | 0.19 | 1.00 | 0.32 |
| R2L | 0.64 | 0.84 | 0.73 |
| U2R | 0.00 | 0.00 | 0.00 |
| **accuracy** | | | **0.58** |

#### KDE Naïve-Bayes Confusion Matrices (Train / Test)

-----

## 🏁 Conclusion

[cite\_start]The experimental results demonstrate that for the NSL-KDD dataset, **KNN significantly outperforms the custom KDE Naïve-Bayes model**[cite: 721]. KNN provided high accuracy and consistent precision/recall scores, proving to be a much more reliable classifier for this task.

[cite\_start]While KDE Naïve-Bayes offers a more flexible approach for non-Gaussian data, its performance was hampered by the specific data distributions in this study, leading to weak accuracy and significant misclassifications[cite: 724].

These findings suggest that for this intrusion detection problem, the simpler distance-based approach of KNN is more effective. [cite\_start]The study also underscores a critical challenge in machine learning: class imbalance can severely impact a model's performance, as seen with the U2R attack category[cite: 722, 725].
