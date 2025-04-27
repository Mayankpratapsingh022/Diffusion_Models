# Diffusion-Based Symbol Generation Across Scripts and Glyph Systems

This project explores the application of **diffusion models** for **symbol and character generation** across various writing systems — starting from natural imagery (butterflies, faces) and scaling to **English letters, Devanagari script**, and **ancient glyphs (Aztec and Mayan)**.
![diffusion model](https://github.com/user-attachments/assets/679412c8-afcf-43e7-8a36-c4c4d866622e)

The primary goal was to train **diffusion models from scratch** under different data regimes, solve real-world bottlenecks by creating custom datasets, and analyze how diffusion models behave with limited, diverse symbol data.

---

## Project Structure

---

## 1. Initial Experiments: Natural Imagery

- **Butterfly Generation**: Training diffusion models to generate butterfly images using standard DDPM training pipelines.
- **Face Generation**: Scaling complexity to human face datasets for deeper understanding of model capacity and training stability.

Purpose: Familiarization with model architectures, sampling schedulers (DDPM, DDIM), and denoising behavior.

---

Also trained a model for chinese characters


![diffusion_process4](https://github.com/user-attachments/assets/fb3d981c-b01b-4ea7-9cbc-268b12995fe4)

![second image style](https://github.com/user-attachments/assets/d2eb4fc9-130d-426e-83aa-eb8f75dd8161)
## 2. English Character Generation


![8cbdf990-622b-47e9-ad80-918c77a2f633](https://github.com/user-attachments/assets/aa473f5b-6f0b-4b4a-803d-d36aaf74eab2)

### Challenge
No publicly available high-resolution datasets covering A-Z, a-z, 0-9 characters across diverse fonts.

### Solution
Created a **custom English Characters Dataset**.

- **85,000+ fonts rendered programmatically**.
- **128x128 grayscale images** for each character.
- **80,000–100,000 samples per character**.
- Used for training unconditional diffusion models.

Dataset available: [English Characters Image Dataset](https://huggingface.co/datasets/Mayank022/English_Characters_Images)

### Key Observations
- Models successfully captured **serif and sans-serif** variations.
- Style blending observed during sampling.
- Single-character training stable with ~300-500 samples.
- Training across multiple letters without conditioning led to **ambiguous outputs** (e.g., circular shapes resembling 'O', '0', '8').

---

## 3. Devanagari Character Generation

![trainin-on-single-ka-100epochs-300 imagges](https://github.com/user-attachments/assets/9c2793ce-d172-48e0-bf8e-e348b590bd1f)
![100 epochs sing char_ka](https://github.com/user-attachments/assets/a23b5e63-b700-4118-a436-85045995a4e8)


### Challenge
Existing Devanagari datasets were low-resolution (32x32) with limited font diversity.

### Solution
Created a **Devanagari Characters Image Dataset**.

- **305 Unicode-compliant Devanagari fonts**.
- **128x128 grayscale images**.
- Covers vowels, consonants, matra combinations, and Hindi numerals.
- **~24,000 images** across 80+ characters.

Dataset available: [Devanagari Characters Image Dataset](https://huggingface.co/datasets/Mayank022/Devanagari-Characters-Image)

### Key Observations
- Models could **reconstruct characters accurately** with >300 examples.
- Reducing data to ~50 samples severely affected quality.
- Overfitting was **desirable** — helped models "memorize with variation."
- DDIM scheduler provided **faster sampling** without major quality loss compared to DDPM.

---

## 4. Ancient Glyph Generation (Aztec and Mayan)

### Collaborative Work
This section was led by **Kiran**, focusing on Aztec and Mayan glyphs.

- Dataset contained **~50–70 glyphs** with high diversity.
- Grayscale preprocessing and augmentation techniques applied.
- Focused training on selected glyphs attempted.

### Results
- Despite limited data, **promising preliminary outputs were achieved** — showing early signs of structural learning by the diffusion models.
- The experiments demonstrated the potential for symbol generation even under severe data scarcity with thoughtful augmentation and training.

Full credit to **Kiran** for leading and navigating the glyph experiments.

---

## 5. Parameter Tuning and Insights

Special thanks to **Pranav**, who contributed extensively to:

- Optimizing learning rates and batch sizes.
- Scheduler comparisons (DDPM vs DDIM).
- Suggesting strategic training improvements for better convergence and stability.

Their contributions significantly enriched the project outcomes.

---

## 6. Conditional Diffusion for Controlled Character Generation

Moving beyond unconditional models, a **Conditional Diffusion Model** was trained successfully:

- Given an input label (e.g., 'A', 'क'), the model generates the corresponding character image.
- Opens pathways for controlled, multilingual text image generation in the future.

Details and sample generations will be shared soon.

---


## How to Run

1. Clone the repository.
3. Download the datasets (English Characters, Devanagari Characters, Aztec/Mayan Glyphs).
4. Run notebooks inside `/notebooks/` to reproduce experiments:
   - For unconditional training: `English_Characters_Diffusion.ipynb`, `Devanagari_Characters_Diffusion.ipynb`
   - For glyphs: `Aztec_Mayan_Glyphs_Diffusion.ipynb`
   - For conditional training: `Conditional_Character_Diffusion.ipynb`

---

## Future Work

- Improve glyph generation through conditional architectures.
- Train multilingual text generators using larger datasets.
- Explore specialized diffusion variants for low-data regimes.
- Apply transfer learning or data-efficient training pipelines for ancient scripts.

---

# Conclusion

This project highlights both the **power and limitations of diffusion models** in small-data symbol generation settings.  
While unconditional models work well with sufficient structured examples, **future work must focus on conditioning, augmentation, and model scaling** to handle multilingual, multi-symbol generation tasks more robustly.
