# Experimental Phases

This document details all test phases conducted during the project, ordered chronologically by modification date.

---

## Phase 1: Dragon Dataset + ResNet50 (Initial Prototype)
**Notebook:** `notebooks/AI_gen_Image_ART_test_1.ipynb` (Oct 31, 2025)
**Folder:** `test 1 (Dragon) (resNet50)/`
**Saved Model:** `best_model.pth`

- Initial proof-of-concept using ResNet50 architecture
- Dataset: Custom Dragon dataset
- Focus on establishing baseline pipeline for AI-generated image detection

---

## Phase 2: SuSy Dataset + ResNet50
**Notebooks:**
- `notebooks/AI_gen_Image_ART_test_2.ipynb` (Nov 1, 2025)
- `test 2 (Susy) ResNet50/AI_Gen_test_2_(on_SuSy_dataset)_ResNet50.ipynb` (Sep 5, 2025)
**Saved Model:** `best_susy_model.pth`

- Migrated to SuSy dataset (tabular + image data)
- Used KaggleHub / HuggingFace datasets for SuSy data loading
- ~15GB dataset with train/val/test splits
- Trained on Google Colab with T4 GPU

---

## Phase 3: Kaggle CIFAKE + ResNet50/CNN
**Notebooks:**
- `notebooks/AI_gen_Image_ART_test_3.ipynb` (Nov 5, 2025)
- `test 3 (Kaggle - CNN)/AI_Gen_test_3_(Kaggle_dataset) (ResNet50).ipynb` (Sep 5, 2025)
**Saved Model:** `best_cifake_model.pth`

- Transitioned to CIFAKE dataset (100K real + 100K AI-generated images)
- Explored both custom CNN and ResNet50 architectures
- Generated confusion matrix, F1 score, PR curve, and ROC visualizations

---

## Phase 4: CIFAKE + EfficientNet-B4
**Notebooks:**
- `notebooks/AI_gen_Image_ART_test_5.ipynb` (Nov 14, 2025)
- `test 4 (CIFAKE) EfficientNet b4/AI_Gen_test_4(EfficientNet_b4)_(on_CIFAKE_dataset).ipynb` (Sep 5, 2025)
**Saved Model:** `best_cifake_model.pth`

Upgraded from ResNet50 to **EfficientNet-B4** for better accuracy.
Key training results (first 10 epochs, interrupted at epoch 10):

| Epoch | Train Loss | Val Loss | Accuracy | Precision | Recall | F1-Score |
|-------|-----------|---------|----------|-----------|--------|----------|
| 1 | 0.4973 | 0.3969 | 0.8287 | 0.8731 | 0.7692 | **0.8179** |
| 2 | 0.4655 | 0.3722 | 0.8418 | 0.8648 | 0.8103 | **0.8367** |
| 3 | 0.4576 | 0.3678 | 0.8438 | 0.8837 | 0.7918 | 0.8352 |
| 4 | 0.4599 | 0.3619 | 0.8446 | 0.8824 | 0.7953 | 0.8366 |
| 5 | 0.4573 | 0.3607 | 0.8454 | 0.8700 | 0.8123 | **0.8402** |
| 6 | 0.4589 | 0.3611 | 0.8475 | 0.8952 | 0.7871 | 0.8377 |
| 7 | 0.4552 | 0.3599 | 0.8464 | 0.8860 | 0.7951 | 0.8381 |
| 8 | 0.4558 | 0.3580 | 0.8460 | 0.8837 | 0.7969 | 0.8380 |
| 9 | 0.4564 | 0.3596 | 0.8467 | 0.8936 | 0.7871 | 0.8370 |
| 10 | 0.4583 | - | - | - | - | - (interrupted) |

Final evaluation on full test set (20,000 images):
- **AUC: 0.9259**
- Classification Report:
  - REAL (Class 0): Precision 0.82, Recall 0.88, F1-Score 0.85
  - FAKE (Class 1): Precision 0.87, Recall 0.81, F1-Score 0.84

---

## Phase 5: SuSy + EfficientNet-B4
**Notebook:** `test-5 (SuSy) EfficientNet b4/AI_Gen_test_5(EfficientNet_b4)_(on_SuSy_dataset).ipynb` (Sep 5, 2025)

- Applied EfficientNet-B4 on SuSy dataset
- Preprocessed images at 380x380 (optimal for EfficientNet-B4)
- Batch size: 32, 5 epochs planned
- Model saved to Google Drive

---

## Phase 6: CIFAKE + EfficientNet-B4 (Improved)
**Notebooks:**
- `notebooks/AI_gen_Image_ART_test_6.ipynb` (Dec 16, 2025) -- **Latest notebook**
- `test_6_(CIFAKE)_(EfficientNet_b4)/test_6_(CIFAKE)_(EfficientNet_b4).ipynb` (Sep 7, 2025)
**Saved Model:** `best_cifake_model.pth`

- Refined EfficientNet-B4 training pipeline on CIFAKE
- Improved data preprocessing and augmentation
- Generated comprehensive evaluation metrics with confusion matrix

---

## Final Phase: HybridForensicsNetV3
**Document:** `docs/Blinded_Manuscript.docx`

The final research output integrates all learnings into **HybridForensicsNetV3**, a multi-modal framework that:
1. Analyzes images across 5 domains: RGB, FFT, Wavelet, ELA, Noise Residuals
2. Uses MoE gating and cross-attention fusion for adaptive feature weighting
3. Employs Clean-then-Hard curriculum learning strategy

**Final Performance: F1-Score: 99.5%, Recall: 100%**
