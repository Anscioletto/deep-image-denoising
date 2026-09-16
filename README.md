# deep-image-denoising
Image Denoising & Restoration: Autoencoders, Skip Connections & Grad-CAM Analysis
An ablation study comparing Autoencoder architectures and Transfer Learning strategies for image restoration under Gaussian and Salt & Pepper noise.

Overview
This project explores how network depth, skip connections, and pre-trained backbones impact image denoising performance. We corrupt images using synthetic noise patterns and train various autoencoder models to reconstruct the original ground-truth images.

Alongside standard quantitative benchmarks (MSE, PSNR, SSIM), we apply Grad-CAM across all trained models to visualize how structural choices affect feature attention during reconstruction.

Model Architectures
We evaluated four distinct setups under identical training conditions:

Simple Autoencoder: A shallow baseline with 2 convolutional layers.
Deep Autoencoder (No Skip Connections): A deeper sequential architecture to test information bottlenecking and vanishing gradients.
Deep Autoencoder (With Skip Connections): A U-Net style residual model designed to preserve high-frequency spatial features.
Transfer Learning Model: A pre-trained backbone loaded via timm and fine-tuned for dense pixel-level reconstruction.
Datasets & Noise Setup
Datasets: Fashion-MNIST (1 channel) and CIFAR-10 / CIFAR-100 (3 channels, 
32
×
32
).
Corruptions:
Gaussian Noise: Additive continuous zero-mean noise.
Salt & Pepper Noise: Impulse noise affecting random pixels.
Key Takeaways
Skip Connections are Essential: The deep model with skip connections outperformed the non-skip variant, achieving significantly higher SSIM values by allowing fine edge details to bypass the compression bottleneck.
Transfer Learning Bottlenecks: Classification backbones (like ResNet) require careful adapter design for denoising, as standard pooling layers tend to discard spatial details critical for pixel-wise reconstruction.
Feature Attention (Grad-CAM): Attention maps show that high-performing models focus on high-contrast object boundaries while filtering out high-frequency background noise.
🛠️ Tech Stack
Core: PyTorch, Torchvision
Model Zoo: timm (PyTorch Image Models)
XAI / Interpretability: pytorch-grad-cam
Analysis: NumPy, Matplotlib
Environment: Google Colab (NVIDIA T4 GPU)
📁 Repository Structure
.
├── denoising_study.ipynb   # Main notebook with training pipelines and Grad-CAM generation
├── presentation.pdf        # Project presentation slides
└── README.md

 How to Run
Open file in Google Colab (ensure GPU hardware acceleration is enabled).

Install the required dependencies in the first cell:

Bash
pip install timm grad-cam
Run all cells sequentially to train the models, generate evaluation metrics, and render Grad-CAM visuali
