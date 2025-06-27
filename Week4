# 🏁 Week 4: Performance Metrics (PSNR, SSIM), Training Tricks and Improvements

---

## 📏 Implemented Evaluation Metrics

### 1️⃣ PSNR (Peak Signal-to-Noise Ratio)
- Measures **pixel-wise similarity** between the generated HR image and the ground truth HR image.
- **Higher PSNR = Better image quality.**
- ✅ A standard metric for assessing image fidelity.

### 🔢 Formula:

PSNR = 10 * log10(MAX^2 / MSE)PSNR = 10 * log10(MAX^2 / MSE)

- Where:
  - **MAX = 1** (if images are normalized to [0,1])
  - **MSE = Mean Squared Error** between the generated and ground truth HR images.

---

### 2️⃣ SSIM (Structural Similarity Index Measure)
- Measures **perceptual similarity** considering:
  - **Luminance**
  - **Contrast**
  - **Structure**
- 🔢 **Range:** -1 to 1 (Closer to **1** indicates better perceptual similarity).
- ✅ More aligned with human visual perception compared to PSNR.

---

## 🚀 Training Improvements Implemented

### 🔖 Label Smoothing
- **Purpose:** Prevents the Discriminator from becoming too confident too quickly.
- **Method:**  
  - Instead of labels being hard **1 (real)** and **0 (fake)**, use soft labels like:
    - **0.9 for real**
    - **0.1 for fake**

---

### 🔽 Learning Rate Scheduler
- Helps reduce the learning rate as training progresses to stabilize learning.
- ✅ Used PyTorch's:
  - **StepLR**
  - **MultiStepLR**
- **Effect:** Prevents overshooting minima and improves convergence.

---

### 🎯 Generator Pretraining
- **Phase 1:**  
  - Pretrained the **Generator** with **L1 Loss** or **MSE Loss** for image reconstruction.
  - This step stabilizes the generator before introducing adversarial noise.
- **Phase 2:**  
  - Switched to **Adversarial Training** using:
    - **GAN Loss (Adversarial)**
    - **Perceptual Loss (VGG-based)**

---

### 🎨 Normalization for VGG Perceptual Loss
- To correctly compute perceptual loss using a pretrained VGG network:
- Input images are normalized using **ImageNet statistics**:
```python
mean = [0.485, 0.456, 0.406]
std  = [0.229, 0.224, 0.225]
