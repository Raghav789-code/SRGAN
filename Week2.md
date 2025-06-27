# Week 2: SRGAN Architecture, Loss Functions & ESRGAN

## 🎨 SRGAN Generator Architecture
- **Initial Convolutional Layer**  
  ➝ With **PReLU activation** to extract low-level features.

- **16 Residual Blocks (Residual Learning)**  
  ➝ Each block contains:
  - Conv ➝ BatchNorm ➝ PReLU ➝ Conv ➝ BatchNorm ➝ Skip Connection

- **Skip Connection**  
  ➝ Adds the initial feature maps back after the residual blocks to help gradient flow and learning.

- **Upsampling Layers**  
  ➝ Uses **PixelShuffle layers** to upscale the resolution (typically by 4×).

- **Final Convolutional Layer**  
  ➝ Outputs a **3-channel (RGB)** high-resolution image.

---

## 🧠 SRGAN Discriminator Architecture
- Functions as a **standard CNN classifier**.
- Architecture:
  - Several **Conv ➝ BatchNorm ➝ LeakyReLU** layers to extract features.
  - Followed by **Dense (Fully Connected)** layers.
  - Ends with a **Sigmoid activation** to output probability (**real vs fake**).

---

## 📦 SRGAN Loss Functions

### 1️⃣ **Content Loss (Perceptual Loss)**
- Calculated using **feature maps from a pre-trained VGG network**.
- Measures perceptual similarity rather than just pixel-wise difference.
- Ensures that generated images maintain **texture, structure, and semantics**.

### 2️⃣ **Adversarial Loss**
- Derived from the Discriminator's output.
- Encourages the Generator to produce images that are indistinguishable from real HR images.

### 3️⃣ **Total Generator Loss**
- A weighted combination of:
  - **Content Loss (Perceptual)**
  - **Adversarial Loss (GAN)**

---

## 🚀 Introduction to ESRGAN (Enhanced SRGAN)

**Paper:** [Enhanced Super-Resolution Generative Adversarial Networks (ESRGAN)](https://arxiv.org/abs/1809.00219)

### 🔥 Key Improvements Over SRGAN:
- **Residual-in-Residual Dense Blocks (RRDBs)**  
  ➝ Deeper, more powerful, and stable architecture for better learning without BatchNorm.

- **Relativistic Discriminator (RaGAN)**  
  ➝ Instead of judging "real vs fake", it predicts whether a real image is **more realistic** than a generated one.  
  ➝ Leads to better texture generation and more realistic images.

- **Improved Perceptual Loss**  
  ➝ Uses **VGG-54 layer** (deeper feature extraction) instead of VGG-34.  
  ➝ Results in sharper, more **photo-realistic textures**.

- **Removal of Batch Normalization**  
  ➝ Helps avoid artifacts and allows better detail preservation.

---

## ✅ Summary of Enhancements:
| Component           | SRGAN                              | ESRGAN                                             |
|---------------------|------------------------------------|----------------------------------------------------|
| Feature Blocks       | Residual Blocks                   | Residual-in-Residual Dense Blocks (RRDB)           |
| Discriminator        | Standard Binary Classifier        | Relativistic Discriminator (RaGAN)                |
| Perceptual Loss      | VGG-34 feature layer              | VGG-54 deeper feature layer                       |
| Normalization        | Uses BatchNorm                    | **No BatchNorm (Better details)**                 |
| Visual Quality       | Good                              | **Sharper, realistic, fine textures**             |

---

> This week focuses on understanding the architectural differences and loss function innovations that lead from SRGAN to ESRGAN, setting the foundation for high-fidelity image super-resolution tasks.
