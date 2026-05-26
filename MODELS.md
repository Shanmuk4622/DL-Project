# Model Architectures

## Overview

Three primary architectures were evaluated across the experimental phases, progressing from simple to complex.

---

## 1. ResNet50
**Used in:** Tests 1, 2, 3

- Pre-trained on ImageNet
- 50-layer deep residual network
- Standard transfer learning: frozen feature extractor + custom binary classifier head
- Input size: 224x224
- Pros: Fast training, good baseline
- Cons: Limited capacity for fine-grained forensic artifacts

## 2. Custom CNN
**Used in:** Test 3 (Kaggle)

- Simple convolutional stack designed for binary classification
- Fewer parameters, faster inference
- Used as a baseline comparison point

## 3. EfficientNet-B4
**Used in:** Tests 4, 5, 6

- State-of-the-art efficient architecture using compound scaling
- Pre-trained on ImageNet with `EfficientNet_B4_Weights.DEFAULT`
- Input size: 380x380 (optimal for B4 variant)
- Classifier: Sequential(Dropout(0.4), Linear(1792, 1))
- Optimizer: Adam (lr=0.001) on classifier layer only (backbone frozen)
- Loss: BCEWithLogitsLoss
- Metrics: BinaryAccuracy, BinaryPrecision, BinaryRecall, BinaryF1Score

**Key hyperparameters:**
- Batch size: 32
- Epochs: 15 (Test 4), 5 (Test 5)
- Image transforms: RandomResizedCrop, RandomHorizontalFlip, Normalize (ImageNet stats)
- Validation: Resize(400) -> CenterCrop(380)

## 4. HybridForensicsNetV3 (Final Model)
**Document:** `docs/Blinded_Manuscript.docx`

The final architecture integrates **five complementary forensic modalities**:

| Modality | Domain | Purpose |
|----------|--------|---------|
| RGB | Spatial/Visual | Standard pixel-level features |
| FFT Spectrum | Frequency | Periodic GAN artifacts (checkerboard patterns) |
| Wavelet Decomposition | Multi-scale Texture | Detail coefficients for texture anomalies |
| Error Level Analysis (ELA) | Compression | JPEG compression inconsistencies |
| Noise Residuals | Sensor Noise | Absence of camera sensor fingerprint |

**Key innovations:**
- **Mixture-of-Experts (MoE) Gating**: Dynamically routes each image to the most relevant modality expert
- **Cross-Attention Fusion**: Adaptively combines features across modalities instead of naive concatenation
- **Clean-then-Hard Curriculum Learning**: Two-phase training -- first on high-confidence data, then fine-tuned on hard samples

**Performance: F1-Score: 99.5%, Recall: 100%**
