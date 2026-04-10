# Analysis and Discussion of Findings: CNN Models for Image Classification

This report provides a detailed discussion of the insights derived from comparing four Convolutional Neural Network (CNN) models—one custom architecture and three pretrained models (DenseNet121, ResNet50, and InceptionV3)—evaluated on an image classification dataset.

## (a) Model Behaviour Interpretation

### i. Implications of Model Performance

The performance of each model during training and validation reveals significant differences in their ability to generalize.

*   **DenseNet121** emerged as the top performer, suggesting that its dense connectivity pattern, which promotes feature reuse and alleviates the vanishing-gradient problem, is highly effective for this specific dataset.
*   **InceptionV3** followed closely, benefiting from its multi-scale feature extraction capabilities.
*   **ResNet50** and the **Custom CNN** showed lower performance metrics, indicating that while ResNet50 is a powerful architecture, it may require more extensive fine-tuning or data augmentation. The Custom CNN, despite being much smaller, performed comparably to ResNet50, showing efficient but limited feature extraction.

### ii. Observations on Convergence and Fitting

*   **DenseNet121 and InceptionV3**: These models showed stable convergence during training. Their high validation accuracy relative to training suggests a healthy fit with minimal overfitting, likely due to the robust features learned during pretraining on ImageNet.
*   **ResNet50**: The model exhibited signs of underfitting or suboptimal convergence on this specific task, as evidenced by its lower accuracy (0.6352) compared to other pretrained models. This suggests the default pretrained weights might not align well with the target domain without further adaptation.
*   **Custom CNN**: This model showed the most significant struggle with convergence. With an accuracy of 0.6415, it likely suffered from limited capacity to capture complex patterns, leading to a plateau in performance early in the training process.

### iii. Strengths and Limitations

| Model        | Strengths                                                                                             | Limitations                                                                                                                                                               |
| :----------- | :---------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Custom CNN   | Extremely lightweight; fast training and inference; minimal resource requirements.                    | Low accuracy and F1-score; limited ability to learn complex hierarchical features.                                                                                          |
| DenseNet121  | Highest overall accuracy and F1-score; efficient parameter usage through feature reuse.               | Higher computational cost than custom models; moderate memory footprint.                                                                                                  |
| ResNet50     | Strong theoretical foundation with skip connections; robust for very deep architectures.              | Largest model size (224.79 MB); underperformed in this specific implementation.                                                                                           |
| InceptionV3  | Excellent multi-scale feature extraction; high ROC-AUC (0.8704).                                      | Large parameter count and significant model size (152.12 MB).                                                                                                             |

## (b) Comparative Performance Table

The following table summarizes the performance metrics for the four models evaluated on the dataset:

| Model       | Accuracy | Precision | Recall | F1-Score | Parameters  | Size (MB) |
| :---------- | :------- | :-------- | :----- | :------- | :---------- | :-------- |
| Custom CNN  | 0.6415   | 0.4911    | 0.6415 | 0.5381   | 1,442,341   | 16.65     |
| DenseNet121 | 0.7481   | 0.7427    | 0.7481 | 0.7376   | 7,699,013   | 44.82     |
| ResNet50    | 0.6352   | 0.4838    | 0.6352 | 0.5333   | 24,777,605  | 224.79    |
| InceptionV3 | 0.7086   | 0.7010    | 0.7086 | 0.6908   | 22,992,677  | 152.12    |

## (c) Deployment Suitability Assessment

| Model       | Web Applications                               | Mobile Devices                                   | Edge / Embedded Systems                               |
| :---------- | :--------------------------------------------- | :----------------------------------------------- | :---------------------------------------------------- |
| Custom CNN  | Highly Suitable: Fast load times and low latency. | Highly Suitable: Minimal battery and storage impact. | Ideal: Fits easily on low-power hardware.             |
| DenseNet121 | Suitable: Efficient enough for modern smartphones. | Moderate: May require optimization (e.g., quantization). | Suitable: Balanced performance and size.              |
| ResNet50    | Less Suitable: Large file size increases web load times. | Moderate: High memory and storage requirements.  | Poor: Too large for most restricted edge devices.     |
| InceptionV3 | Moderate: Significant size but high reliability. | Moderate: Heavy on resources; better for high-end devices. | Less Suitable: High computational complexity.         |

## (d) Overall Reliability Assessment

The **DenseNet121** model is the most reliable choice for this classification task. With the highest Accuracy (0.7481) and F1-Score (0.7376), it demonstrates a superior balance between precision and recall, ensuring fewer false positives and negatives compared to its counterparts.

From a real-world deployment perspective, its size (44.82 MB) is manageable for most platforms, including web and mobile. While the Custom CNN is smaller, its reliability is compromised by significantly lower performance metrics. DenseNet121’s high ROC-AUC (0.8995) further confirms its robustness in distinguishing between classes, making it the most dependable model for practical application.
