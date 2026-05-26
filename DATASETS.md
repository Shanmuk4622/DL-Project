# Datasets

## 1. Dragon Dataset
**Used in:** Test 1
- Custom dataset of real and AI-generated dragon images
- Small-scale, used for pipeline prototyping

## 2. SuSy Dataset
**Used in:** Tests 2, 5
- Source: HuggingFace `HPAI-BSC/SuSy-Dataset`
- Size: ~15.2GB train, ~4.73GB val, ~6.02GB test
- Image classification dataset with binary labels (0: Background, 1: Signal)
- Train: 14,451 samples, Val: ~5,000, Test: ~5,500
- Multi-class labels (0-5) eventually mapped to binary real/fake

## 3. CIFAKE Dataset
**Used in:** Tests 3, 4, 6
- Source: Kaggle `birdy654/cifake-real-and-ai-generated-synthetic-images`
- 100,000 real images + 100,000 AI-generated synthetic images
- Train: 100,000 images (50K real + 50K fake)
- Test: 20,000 images (10K real + 10K fake)
- Balanced binary classification dataset
- Images are 32x32 (CIFAR-style) or resized for EfficientNet

## 4. Multi-Generator Evaluation Dataset (Final)
**Used in:** HybridForensicsNetV3
- Source: Real and Fake AI-Generated Standardized 512px Image Forensics Dataset [45]
- 512x512 uniformly preprocessed images
- Spans both GAN-based and Diffusion-based synthetic imagery
- Ensures controlled, reproducible evaluation across diverse generation mechanisms
