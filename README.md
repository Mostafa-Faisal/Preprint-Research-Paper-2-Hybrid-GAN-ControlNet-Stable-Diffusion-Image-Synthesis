# Preprint-Research-Paper-2-HYBRID GENERATIVE FRAMEWORK: Integrating Single-Image GANs with ControlNet-Guided Stable Diffusion for High-Fidelity Image Synthesis

> **Authors:**  
> 🔹 Rabeya Amin Jhuma — University of Information Technology and Sciences (UITS), Dhaka, Bangladesh  
> 🔹 Mostafa Mohaimen Akand Faisal — University of Information Technology and Sciences (UITS), Dhaka, Bangladesh  
> 📧 Contact: [mostafafaisal013@gmail.com](mailto:mostafafaisal013@gmail.com)  

---

## 📄 Abstract

Generative modeling has advanced rapidly with **Generative Adversarial Networks (GANs)** and **Diffusion Models**, each offering distinct advantages.  
GANs excel at capturing fine textures and structural details, while diffusion models achieve high-fidelity and semantically rich outputs.  
However, GANs often lack semantic control and diffusion models require structural conditioning.

This study presents a **hybrid generative framework** combining the strengths of both:
- A **conditional single-image GAN** captures local textures from minimal data.
- A **Stable Diffusion model guided by ControlNet (Canny edge maps)** introduces semantic richness and stylistic flexibility.

The framework enables **high-quality, controllable, and semantically rich image generation** even in data-constrained scenarios — offering a promising path toward efficient and high-fidelity image synthesis.

---

## 🚀 Key Contributions

- **Single-Image Conditional GAN:** Learns patch-level structure and texture from a single sample.  
- **ControlNet-Guided Diffusion:** Uses edge-based conditioning for structure-preserving stylization.  
- **Hybrid Two-Stage Pipeline:** Merges adversarial learning with diffusion-based refinement.  
- **Prompt-Based Artistic Control:** Text-driven generation for flexible visual outputs.  
- **Low-Data Capability:** Works effectively without large-scale datasets.

---

## 🧩 Methodology Overview

### 🥇 Phase 1: Conditional Single-Image GAN
- Input: 3-channel image + latent vector (128-dim) + feature vector (10-dim).  
- Output: Structure-preserving image with realistic textures.  
- Loss: Binary Cross Entropy (BCE).  
- Optimizer: Adam (lr = 2×10⁻⁴, β₁ = 0.5, β₂ = 0.999).  
- Trained for 10,000 epochs.

### 🥈 Phase 2: Stable Diffusion + ControlNet
- Input: GAN output + Canny edge map + text prompt.  
- Models:  
  - `lllyasviel/control_v11p_sd15_canny` (ControlNet model)  
  - `runwayml/stable-diffusion-v1-5` (Stable Diffusion backbone)  
- Steps: 80 inference steps, guidance scale = 12.  
- Output: High-fidelity, stylistically enhanced image.

---

## 🧠 Framework Diagram
    [ Latent Noise + Features ]
    ↓
    🎨 Conditional GAN
    ↓
    [ Generated Image + Canny Edges ]
    ↓
    🌀 ControlNet + Stable Diffusion
    ↓
    ✨ Final Stylized Output 



---

## 🧾 Dataset

- **Single scratch image** used for training (single-image generative modeling).  
- **No large dataset required.**  
- Useful for **artists, animators, and researchers** exploring low-data creative synthesis.

---

## 📊 Results

### 🔸 Qualitative Examples
| Input | Output (Prompt) |
|:------:|:----------------|
| ![Input](example_input.jpg) | *"A water lady with ocean blue eyes, soft lighting, photorealistic portrait."* |
| ![Input](example_input.jpg) | *"A mythical red fox spirit woman with burning eyes, ethereal glow, and flowing fur cloak."* |
| ![Input](example_input.jpg) | *"A surreal fantasy mermaid with glowing eyes."* |

The hybrid model consistently preserves **structural fidelity** while enhancing **stylistic diversity**.

---

## ⚙️ Requirements (for reproducibility)

| Dependency | Version / Source |
|-------------|------------------|
| Python | ≥ 3.10 |
| PyTorch | ≥ 2.0 |
| diffusers | ≥ 0.25 |
| transformers | ≥ 4.35 |
| ControlNet | lllyasviel/control_v11p_sd15_canny |
| Stable Diffusion | runwayml/stable-diffusion-v1-5 |
| OpenCV | For Canny edge detection |
| Pillow | For image preprocessing |

---

## 🧪 How to Use

```bash
# Clone repository
git clone https://github.com/yourusername/Hybrid-Generative-Framework.git
cd Hybrid-Generative-Framework

# Install dependencies
pip install -r requirements.txt

# Run GAN training
python train_gan.py --epochs 10000 --lr 0.0002

# Run diffusion refinement
python hybrid_pipeline.py --prompt "A cinematic water fairy with glowing eyes"


