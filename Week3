# Week 3: DIV2K Dataset Preparation, LR-HR Pair Generation, and Custom PyTorch Dataset

---

## 📚 About the DIV2K Dataset
- **Full Form:** DIVerse 2K Resolution Dataset
- Provides **high-quality HR images** for Super-Resolution tasks.

### 📦 Dataset Split:
- **Training Set:** 800 images
- **Validation Set:** 100 images
- **Testing Set:** 100 images (without ground truth; used for benchmarking)

---

## 🔽 Steps for Dataset Preparation

### 1️⃣ Downloading the DIV2K Dataset:
- ✅ Used TensorFlow Dataset Catalog:  
  ➝ [DIV2K on TensorFlow Datasets](https://www.tensorflow.org/datasets/catalog/div2k)  
- ✅ Alternatively, downloaded images **manually** from official sources.

---

### 2️⃣ Generating LR-HR Image Pairs:
- **Downsampling Method:** Bicubic interpolation
- **Scale Factor:** ×4

### 🔧 Example:
- **Original HR image size:** 2040×2040  
- **Generated LR image size:** 510×510

---

## 🐍 Custom PyTorch Dataset Implementation

### ✅ Steps:
- Created a **Python class** inheriting from `torch.utils.data.Dataset`.
- Loaded both **HR (High-Resolution)** and **LR (Low-Resolution)** images.
- Applied essential transformations:
  - **Convert images to tensors**
  - **Normalize values** (usually to [-1, 1] or [0, 1] range)

### 🚀 Features:
- Supports efficient data loading with PyTorch’s **DataLoader**.
- Handles batching, shuffling, and parallel data loading for training.

### 🔗 Reference:  
Followed the official PyTorch tutorial for dataset creation:  
➝ [PyTorch Custom Dataset Tutorial](https://pytorch.org/tutorials/beginner/data_loading_tutorial.html)

---

## 🔗 PyTorch DataLoader Usage
- Split dataset into **training** and **validation** sets.
- Utilized `DataLoader` for:
  - Efficient **batch loading**
  - **Multi-threaded loading** (via `num_workers`)
  - **Shuffling** the dataset

---

## 🗂️ Directory Example Structure:
