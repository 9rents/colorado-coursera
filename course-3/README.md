# Course 3 — Computer Vision (University of Colorado Boulder, Coursera)

Module notes and practice notebooks for the third CU Boulder computer vision course on Coursera.
Each module has a `notes.md` summary and a self-contained notebook that implements the module's ideas from scratch in NumPy.

## Module 1 — SVM, RBF Kernel and the Discrete Fourier Transform

- [Notes](module-1/notes.md)
- [1. SVM, RBF kernel and DFT](module-1/1_svm_rbf_and_dft.ipynb): kernel SVM trained in the dual (support vectors = α > 0), linear vs RBF, effect of γ and C, DFT as a matrix multiplication, orthogonal basis, inverse DFT, 2D DFT with `1/(M·N)` and low-pass reconstruction

## Module 2 — Probabilistic Models and RNNs

- [Notes](module-2/notes.md)
- [2. Probabilistic models and RNNs](module-2/2_probabilistic_models_and_rnn.ipynb): joint vs conditional probability from counts, chain rule on a probability tree, bigram language model, autoregressive pixel-by-pixel image model, char-level RNN trained with BPTT, vanishing gradient through time, encoder to a fixed-size context

## Module 3 — Transformers & Attention

- [Notes](module-3/notes.md)
- [3. Attention, transformers, ViT](module-3/3_attention_transformers_vit.ipynb): scaled dot-product attention and why √d_k, positional encoding, multi-head attention as one matmul, self vs cross attention, causal decoding with sampling, LayerNorm + skip connections, ViT from patches to class probabilities

## Module 4 — CLIP and Diffusion Models

- [Notes](module-4/notes.md)
- [4. CLIP and diffusion](module-4/4_clip_and_diffusion.ipynb): toy CLIP trained with the symmetric contrastive loss and zero-shot classification, temperature, DDPM forward noising, time-conditioned noise predictor with L2 loss, generation by iterative denoising

All notebooks are executed with outputs and use synthetic data only (no downloads). Requirements: `numpy`, `matplotlib`.
