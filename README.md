# HybridShield: A Two-Layer Defense Framework Against Dataset Poisoning Attacks Using SHA-256 Integrity Verification and SSIM Perceptual Filtering

## 📝 Background & Implementation Note
This project is an implementation and extension of the research presented in the paper **"DATASET INTEGRITY VERIFICATION THROUGH HYBRID HASHING AND PERCEPTUAL SIMILARITY"**. While the core concepts of dataset integrity are derived from this study, this framework introduces significant **modifications and novelties** to enhance robustness against sophisticated poisoning vectors.

## 🚀 Project Overview
HybridShield is a multi-layered defense mechanism designed to protect image datasets from adversarial poisoning. By combining cryptographic integrity checks with perceptual similarity metrics, the system distinguishes between benign data processing and malicious adversarial attacks.

### 🛡️ The Hybrid Defense Strategy (The Two-Layer Framework)

1.  **Layer 1: Strict Integrity (SHA-256):** Verifies bit-for-bit identity. This acts as the first line of defense to detect *any* unauthorized modification.
2.  **Layer 2: Perceptual Filtering (SSIM):** For images that fail the hash check (e.g., due to preprocessing or compression), the system uses the Structural Similarity Index to determine if the change is a **Benign Transformation** or an **Adversarial Poisoning** attempt.

## ✨ Novelties & Modifications
Beyond the base implementation found in the literature, this framework includes:
- **Advanced Attack Diversity:** Implementation of complex TrojanNN and subtle Clean-Label attacks that challenge standard SSIM filters.
- **Optimized Perceptual Thresholding:** Fine-tuned `THRESHOLD` logic to minimize the False Positive Rate (FPR) for legitimate data augmentations.
- **Automated Failure Analysis:** Integrated logic to evaluate where individual defenses (SHA-256 alone or SSIM alone) fail, proving the necessity of the hybrid approach.

## ⚠️ Attacks Simulated
| Attack Type | Novelty Level | Description |
| :--- | :--- | :--- |
| **Benign** | Standard | Resizing, Rotation, and Blur to simulate real-world data pipelines. |
| **BadNets** | Standard | Injection of a visible red pixel trigger patch. |
| **TrojanNN** | **Modified** | Combined heavy Gaussian noise with green triggers to mimic complex corruption. |
| **Clean-Label** | **Novel** | Subtle noise designed to bypass detection while affecting model weights. |

## 📊 Technical Stack
- **Dataset:** CIFAR-100 (5,000 images).
- **Stack:** Python, NumPy, TensorFlow, Scikit-Image, PIL, Seaborn.
- **Metrics:** SHA-256 Hash, SSIM Score, False Positive Rate.

## 🛠️ Usage
Ensure dependencies are installed:
```bash
pip install numpy matplotlib seaborn pillow tensorflow scikit-image
```
