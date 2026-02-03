# Deepfake Audio Detection

## 📌 Project Overview
The rise of Generative Adversarial Networks (GANs) has enabled the creation of highly realistic synthetic voices, posing significant risks to digital security and voice-based authentication. This project introduces a robust deep learning framework designed to distinguish between authentic human speech and manipulated audio by analyzing spectral and temporal patterns.

## 📂 Repository Structure
* **`Codes/`**: 10 Python scripts covering the end-to-end pipeline (Preprocessing, Training, and Evaluation).
* **`Computed Image Representation/`**: Features extracted and saved as images:
    * `STFT/`: Short-Time Fourier Transform visual representations.
    * `Mel-spectrograms/`: Log-mel scaled frequency images.
    * `MFCCs/`: Mel-Frequency Cepstral Coefficients.
* **`sample_data.zip`**: Contains raw `.wav` audio files organized into `real` and `fake` folders.

## 📊 Audio-to-Image Representations
To leverage high-performance classification models, raw audio signals are transformed into three distinct 2D visual formats:

1.  **Short-Time Fourier Transform (STFT)**
    * **Function:** Analyzes frequency content changes over time by segmenting audio into small overlapping windows.
    * **Importance:** Effectively identifies fast transient events or localized artifacts caused by synthetic manipulation.
2.  **Mel-spectrograms**
    * **Function:** Maps frequencies onto the Mel scale to mirror how human hearing perceives sound.
    * **Importance:** Highlights inconsistencies in lower-to-mid range frequency bands that are critical for speech audibility but difficult for AI to replicate perfectly.
3.  **Mel-Frequency Cepstral Coefficients (MFCCs)**
    * **Function:** Extracts the spectral envelope of audio to represent the physical characteristics of the vocal tract.
    * **Importance:** Captures fine-grained phonetic details and cepstral patterns unique to natural human speech, exposing distortions in synthetic audio.

### Importance of Image Conversion
Converting 1D audio waveforms into 2D images allows for the use of **Convolutional Neural Networks (CNNs)**, which excel at recognizing complex spatial hierarchies, textures, and visual patterns. This transformation makes subtle synthetic artifacts—such as minor frequency shifts or unnatural transitions—visible to the model in ways that raw audio analysis might miss.

## 🔬 Experimental Testing & Model Selection
The framework's development involved testing three image formats across three specialized deep learning architectures:

* **Temporal Convolutional Networks (TCN):** Utilizes causal convolutions and dilation to analyze audio as a continuous sequence while maintaining temporal order.
* **Gated Recurrent Units (GRU):** Efficiently handles sequential data and long-term dependencies within audio signals without heavy computational resources.
* **EfficientNet:** Employs a systematic compound scaling method to balance network depth, width, and resolution for optimal feature extraction.

### Final Rationale
The final choice for the detection framework is a **Dual-Input EfficientNet-B0** model using **Mel-spectrograms** and **MFCCs** as concurrent inputs. This decision was made because:
* **Superior Accuracy:** EfficientNet achieved the best results when tested independently for each feature type compared to TCN and GRU.
* **Complementary Features:** While Mel-spectrograms capture frequency-based characteristics, MFCCs focus on vocal tract signatures, providing the model with richer, multi-dimensional information.

## ⚡ Computational Performance & Time Complexity

| Phase | Time |
| :--- | :--- |
| Preprocessing | 40m 24s |
| Training | 13m 45s |
|Evaluation | 40s |
| **Total Pipeline** | 54m 49s |

## 🏆 Final Performance
The proposed dual-input model demonstrated exceptional reliability in separating authentic and synthetic audio:
* **Overall Accuracy:** 99.62%
* **Precision:** 1.00
* **Recall:** 1.00
* **F1-Score:** 1.00
