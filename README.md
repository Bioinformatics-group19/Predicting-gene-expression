# Predicting Gene Expression

> **Enformer-Based Genomic Modeling** > *A deep learning repository dedicated to predicting gene expression levels directly from DNA sequences using a lightweight, custom Enformer architecture.*

---

## 📄 Reference Paper & Project Scope

This project is a simplified, from-scratch implementation inspired by the groundbreaking research paper from DeepMind:
* **Paper:** *Effective gene expression prediction from sequence by integrating long-range interactions* (Avsec et al., 2021)
* **Core Concept:** The original Enformer uses a combination of Convolutional layers and Transformer blocks to capture long-range genomic interactions to predict gene expression and chromatin states directly from DNA sequences.

---

## 🛠️ Simplifications Made (Our Architecture)

To make training, debugging, and experimentation feasible on consumer-grade hardware or standard cloud instances, we introduced several strategic simplifications to the original DeepMind setup:

1. **Targeted Organism & Assay Focus (Human CAGE Only)**
   * **Human Only:** We stripped away all mouse genomic tracks, focusing exclusively on human data.
   * **CAGE Data Focus:** Instead of trying to predict thousands of mixed epigenetic tracks (like DNase or ChIP-seq), this implementation maps sequence data directly to continuous **CAGE (Cap Analysis Gene Expression)** signals to track transcription start sites cleanly.

2. **Reduced Model Scale ("Enformer Mini")**
   * Instead of the massive depth used in the paper, we scaled down the number of Transformer layers and channels. This drastically reduced the VRAM footprint and training execution time.

3. **Optimized Input Context & Binning**
   * We adjusted the input sequence lengths and optimized the resolution of the downsampling blocks (genomic bins) to ensure the model could be trained smoothly without losing the vital structural context of the DNA tracks.

4. **Targeted One-Hot Encoding**
   * The model processes DNA sequences structured into clean, predictable one-hot encoded matrices ($A, C, G, T$), streamlining data loading pipelines and saving memory during forward and backward passes.

5. **Mini Scalar Checkpointing**
   * The training output is compiled into a lightweight scalar checkpoint (`best_enformer_mini_scalar.pt`), making it incredibly easy to load the model for immediate inference, analysis, or evaluation.

---

## 📁 Repository Structure

* **enformer.ipynb**: Core notebook focusing on the architectural design, custom layer mechanics, and configuration of our lightweight Enformer blocks.
* **gene_expression_prediction.ipynb**: End-to-end pipeline handling genomic data preprocessing, human CAGE sequence binning adjustments, training loops, and validation metrics.
* **best_enformer_mini_scalar.pt**: Saved PyTorch model weights representing the highest-performing checkpoint from our training runs.

---

## 🧬 Technical Highlights

* **Long-Range Attention:** Utilizing self-attention mechanisms to learn interactions across distant genomic regions, overcoming the rigid local receptive fields of standard CNNs.
* **CAGE Signal Mapping:** Training the network to map structural sequence inputs directly to continuous human biological tracks.
