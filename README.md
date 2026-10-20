![HMPV Virus](images.jpg)

# 🦠 Human Metapneumovirus (HMPV): AI-Powered Diagnosis & Immune Evasion

## What this repository contains

- **`HMPV_Virus.ipynb`**: image-classification experiments on a **22-class virus electron-microscopy (TEM) image dataset**. The classes are Adenovirus, Astrovirus, CCHF, Cowpox, Dengue, Ebola, Guanarito, Influenza, LCM, Lassa, Machupo, Marburg, Nipah virus, Norovirus, Orf, Papilloma, Pseudocowpox, Rift Valley, Rotavirus, Sapovirus, TBE and West Nile. **HMPV is not one of the classes**, and the notebook does not classify HMPV or chest images.
- **`Adenovirus/`, `Cowpox/`, `Dengue/`**: a small sample (31 micrographs) of 3 of the 22 classes.
- The sections further down are background reading on HMPV biology and AI in respiratory diagnostics, adapted from the linked Medium article. They are not results from this repository.

### Dataset and why the file counts differ

Each micrograph in the dataset is stored as **three files**: the image (`.tif`), a particle-position file (`<name>_particlepositions.txt`) and a tag file (`<name>.tif_tags.csv`). The sample here shows the pattern: 31 images, 31 position files and 31 tag files. A file listing of the dataset therefore counts about **three times** the number of images (for example, 852 images would appear as 2,556 files). The notebook uses **only the `.tif` images**; the position and tag files are never read.

The notebook trains from a pre-split copy on Google Drive (`/content/drive/MyDrive/Virus/{train,validation,test}`), which it reports as **745 train, 248 validation and 252 test images (1,245 in total) across 22 classes**.

### Experiments and what they show

All models are ImageNet-pretrained backbones with a small classification head, input 224 x 224, batch size 32, early stopping on validation loss. Figures below are validation accuracy from the notebook's saved training logs (the saved output is truncated, so these are the logged epochs, not necessarily the best epoch).

| Model | Logged validation accuracy |
|---|---|
| MobileNetV2 (fine-tuning last 30 layers) | about 42-45% |
| MobileNetV2 (frozen) | about 42% |
| ResNet-50 (frozen) | about 18-22% |
| EfficientNetB0 + LSTM (frozen) | about 10% (not learning) |

- **No test-set result exists.** The `evaluate_model` calls are commented out, so no test accuracy, confusion matrix or AUC was produced.
- **Earlier claims removed.** A previous version of this README stated ">95% accuracy". The notebook does not support that figure and it has been removed.
- **The UNet cell is a shape demo only.** It is trained for 5 epochs on random noise tensors (`tf.random.normal`) with random masks; it is not trained on this dataset and produces no segmentation result.
- **Known issues.** Validation and test generators use `shuffle=True`, and the test generator applies training augmentation, so a future test evaluation should set `shuffle=False` and remove augmentation. The data split is made outside the notebook, so leakage between splits cannot be checked from this repo.

- 🚨 **Overview:**  
Human metapneumovirus (HMPV) is a leading cause of upper and lower respiratory tract infections. It poses a serious threat to children, the elderly, and immunocompromised individuals.

- 🧑‍⚕️ **Clinical Importance:**
The clinical severity escalates with comorbidities such as advanced age, chronic lung disease, cardiovascular issues, and weakened immunity. Early detection and risk stratification are essential for effective management.

- 🌍 **Epidemiology:**  
  HMPV is prevalent worldwide, with fluctuations in incidence and seasonal outbreaks. Regional studies show it can account for up to 10% of hospital admissions for acute respiratory illness.

- 🔬 **Immune Evasion:**  
  HMPV uses viral proteins (G, SH, M2.2, F) to evade host immune responses by inhibiting interferon pathways and sabotaging innate immunity. This enables viral persistence and increases disease burden.

- 🤖 **AI-Enabled Diagnostics (literature background):**  
  Published deep learning pipelines use architectures such as MobileNetV2, ResNet-50, UNet and LSTM for lung image segmentation, temporal progression modeling and virus classification. This repository's own experiments with these architectures are summarised above; they do not reach the accuracy reported in the literature.

- 🗂️ **Data Methodology:**  
  The imaging dataset is split into train, test, and validation sets. Preprocessing includes resizing, normalization, and augmentation, ensuring robust and unbiased model evaluation.

- 🏥 **Clinical Implementation:**  
  Published studies describe AI-powered diagnostics supporting real-time clinical decision-making and early identification of HMPV and related comorbidities such as pneumonia and ARDS. Nothing in this repository has been clinically validated.

- 🧠 **Multimodal Integration:**  
  Future pipelines aim to integrate clinical notes, lab results, and imaging data using attention mechanisms. This will enable holistic patient assessment and personalized management strategies.

- 🚀 **Deployment & Future Directions:**  
  Efficient deployment at the point of care is becoming possible with edge devices and federated learning. Continued validation and global multi-center studies are critical for improving outcomes.

## 🦠 Human Metapneumovirus (HMPV) Structure and Immune Evasion
- **Central Structure:**  
  The illustration shows the human metapneumovirus (hMPV) particle. The green spiral represents its RNA genome, which is surrounded by various viral and internal proteins embedded in the viral envelope.

- **Viral Proteins (Surface):**  
  - *G protein (purple):* Inhibits interferon (IFN) pathway and blocks innate immune responses, helping the virus evade detection.
  - *SH protein (blue):* Suppresses IFN signaling and inhibits the host's Type I IFN production.

- **Internal Proteins:**  
  - *F protein:* Facilitates fusion of the virus with host cell membranes and downregulates Type I IFN, aiding in viral entry and immune escape. Also contains RGD motif for interaction with host integrins.
  - *P, M, M2.2, L proteins:* Essential for replication and RNA synthesis during the viral cycle.  
  - Proteins M2.1 and palP7 are only expressed during active replication.

- **Genome Layout:**  
  - The RNA genome is organized: `3′ N—P—M—F—M2—SH—G—L 5′`, encoding all the above proteins for replication and immune evasion.

- **Roles in Immune Evasion:**  
  - *G protein:* Inhibits IFN and innate immunity pathways.
  - *M2.2 protein:* Disrupts MAVS signaling, recruits neutrophils.
  - *SH protein:* Halts antiviral responses.
  - *F protein:* Interacts with host cell integrins, facilitating immune modulation and infection.


## 📚 References

- [Human metapneumovirus infection and comorbid conditions]
- [Epidemiology and molecular detection surveys]
- [Deep learning chest imaging models for virus classification]
- [Hybrid model innovation (UNet, LSTM) for temporal modeling]
- [Clinical validation: Diagnostic accuracy]
- [Multimodal attention and data integration]
- [Generalizability and cohort study limitations]
- [Edge deployment and point-of-care studies]
- [Future directions in clinical informatics and predictive diagnostics]
- [NCBI – Human Metapneumovirus]

- Read the full article: [HMPV Virus on Medium](https://medium.com/@saivimenthanvl/hmpv-virus-177aad08d84a)
