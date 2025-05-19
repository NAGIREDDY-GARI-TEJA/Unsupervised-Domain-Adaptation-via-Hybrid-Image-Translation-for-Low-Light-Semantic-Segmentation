# Unsupervised Domain Adaptation via Hybrid Image Translation for Low-Light Semantic Segmentation

This project addresses the challenge of semantic segmentation in low-light conditions for autonomous driving using unsupervised domain adaptation. We combine state-of-the-art segmentation networks (UNet, MA-UNet, and DeepLab V3 models) with CycleGAN-based image translation and image enhancement techniques to effectively translate and adapt nighttime driving scenes to daytime conditions before feeding them to semantic segmentation models.

---

## 🧠 Overview

- **Domain Gap:** Segmenting objects in low-light images is challenging due to poor visibility and noise.
- **Solution:** Translate nighttime (low-light) images into daytime domain using CycleGAN + image enhancement.
- **Goal:** Improve segmentation accuracy on nighttime data using models trained on daytime data.

---

## 📁 Project Structure

```

Unsupervised-Domain-Adaptation-via-Hybrid-Image-Translation-for-Low-Light-Semantic-Segmentation/
├── data/
│   ├── night/               # Raw nighttime images
│   ├── day/                 # Raw daytime images
│   └── enhanced/            # Enhanced night-to-day images
├── models/
│   ├── unet.py
│   ├── maunet.py
│   ├── resnet_segmenter.py
│   └── cycle_gan/           # CycleGAN implementation
├── notebooks/
│   ├── preprocessing.ipynb
│   ├── training_segmentation.ipynb
│   └── eval.ipynb
├── utils/
│   ├── enhancement.py       # Enhancement functions
│   └── dataloader.py
├── checkpoints/             # Trained model weights and logs
├── results/
│   └── qualitative/         # Visual outputs of segmentation
├── requirements.txt
└── README.md
```


## 🔧 Pipeline

1. **Data Collection**  
   - Unpaired day and night driving datasets (e.g., BDD100K, Data Zurich)

2. **Image Enhancement**  
   - Pixel-wise Amplifier Module  
   - Illumination Adaptive Norm

3. **Image Translation**  
   - Night → Day using CycleGAN  
   - Trained on unpaired data  
   - Improves feature distribution alignment

4. **Semantic Segmentation**  
   - Models used:  
     - UNet  
     - MA-UNet  
     - DeepLab V3 
   - Trained on daytime images  
   - Inference on translated/enhanced night images

5. **Evaluation**  
   - Metrics: mIoU, Pixel Accuracy, Class-wise IoU  
   - Compare original, enhanced, and translated images




🏁 Usage

1. Install dependencies

    ```bash
    pip install -r requirements.txt

2. Enhance night images

    ```bash
    python utils/enhancement.py --input_dir data/night --output_dir data/enhanced

3. Train CycleGAN

    ```bash
    python train_segmentation.py --model unet --dataset data/day

4. Train segmentation model (e.g., UNet)

    ```bash
    python train_segmentation.py --model unet --dataset data/day

5. Inference on translated images

    ```bash
    python inference.py --model unet --input data/enhanced_translated

Results

![image](https://github.com/user-attachments/assets/e02577bc-17ac-4a74-a981-e241d39394f2)

