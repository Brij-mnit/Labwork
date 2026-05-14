# HybridShield: A Two-Layer Defense Framework Against Dataset Poisoning Attacks Using SHA-256 Integrity Verification and SSIM Perceptual Filtering

This project implements and evaluates a multi-layered defense mechanism designed to protect image datasets from adversarial poisoning and tampering. By combining cryptographic integrity checks with perceptual similarity metrics, the system distinguishes between benign data processing and malicious adversarial attacks.

## 🚀 Project Overview

In machine learning, data integrity is paramount. Adversarial attacks often involve 'poisoning' datasets with triggers or subtle noise to corrupt model training. This notebook simulates a real-world scenario where a receiver must verify the integrity of a dataset that has been intercepted and modified by an attacker.

### 🛡️ The Hybrid Defense Strategy

The defense relies on a two-stage verification process:
1.  **Strict Integrity (SHA-256):** Verifies that the image is bit-for-bit identical to the source. This detects *all* modifications but cannot distinguish between a simple resize and a malicious payload.
2.  **Perceptual Similarity (SSIM):** For images that fail the hash check, the system calculates the Structural Similarity Index. If the SSIM remains high, the modification is treated as a **Benign Transformation**. If it drops below a threshold, it is flagged as an **Adversarial Attack**.

## ⚠️ Attacks Simulated

| Attack Type | Description | Intended Effect |
| :--- | :--- | :--- |
| **Benign** | Resize, Rotation (5°), and slight Gaussian Blur. | Test for False Positives. |
| **BadNets** | Injection of a visible red pixel trigger patch. | Classic backdoor trigger. |
| **TrojanNN** | Heavy Gaussian noise combined with a green trigger patch. | Evades simple similarity filters. |
| **Clean-Label** | Subtle additive Gaussian noise. | Targets model weights without visible artifacts. |

## 📊 Technical Implementation

- **Dataset:** CIFAR-100 (Sub-sampled to 5,000 images).
- **Stack:** Python, NumPy, TensorFlow/Keras, Scikit-Image, PIL, Seaborn.
- **Metrics:**
  - `SHA-256` for bitwise integrity.
  - `SSIM` (Structural Similarity Index) for visual consistency.
  - `FPR` (False Positive Rate) to measure the cost of defense on clean data.

## 📈 Performance Analysis

The notebook generates several visualizations to evaluate the defense:
- **Detection Bar Charts:** Comparing detection rates across different attack vectors.
- **SSIM Distribution Histograms:** Visualizing how different attacks affect structural similarity.
- **Confusion Matrix/Heatmaps:** Showing the trade-off between accepted benign images and rejected poisons.
- **Visual Side-by-Side:** Direct comparison of Original vs. Attacked images with their corresponding SSIM scores.

## 🛠️ Installation & Usage

To reproduce these results, ensure you have the required dependencies:

```bash
pip install numpy matplotlib seaborn pillow tensorflow scikit-image
```

Run the notebook cells sequentially to simulate the Sender -> Attacker -> Receiver pipeline.
