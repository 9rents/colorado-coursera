# CLIP and Diffusion Models: Module Notes

Summary of the key concepts from the module on multimodal models (CLIP) and diffusion models.

## 1. CLIP (Contrastive Language-Image Pre-training)

### Core idea
CLIP learns to **align images and text in a shared (joint) embedding space**. Matching image-text pairs end up close together, non-matching pairs end up far apart. This makes it a key multimodal foundation model: it integrates two modalities for many downstream tasks.

### Architecture
- **Image encoder**: turns an image into a feature vector. A final **projection layer** reduces the dimensionality of image features to the embedding size.
- **Text encoder** (transformer): turns a sentence into a vector. The **end-of-text (EOT) token** aggregates information from all previous tokens and its output is used as the final sentence representation.
- Both encoders map inputs into lower-dimensional embeddings, which are **normalized** before comparison.
- The final text-encoder output represents the sentence in the shared embedding space with images (not for captioning or classification into fixed classes).

### Training with image-text pairs
- Training elements: **contrastive loss, image encoder, text encoder**.
- Pairs are processed in **batches**, mainly for efficient parallel computation on GPUs. Batches also provide many in-batch negative pairs.
- Compute the **similarity matrix** between all images and texts in the batch.
  - Dot product of normalized embeddings = **cosine similarity**.
  - The **diagonal** holds the similarity between each image and its own caption (the correct pairs).
- The target is an **identity matrix**: correct pairs lie on the diagonal.
- **Temperature** parameter: sharpens or softens the similarity distribution in the softmax.
- Loss is computed in **both directions** (image-to-text and text-to-image) for symmetric learning and better alignment.
- Purpose of contrastive pre-training: **differentiate similar and dissimilar pairs** of embeddings.

### Zero-shot classification
- Write a text description for each class (e.g. "a photo of a dog").
- Encode the image and all class descriptions, then pick the class whose text embedding is **most similar** to the image embedding.
- Needs **no labeled examples** for the target classes and no extra classifier training.

### Why a joint embedding space?
It **facilitates multimodal learning**: one shared space lets us compare, search and combine images and text directly.

## 2. Diffusion Models

### Core idea
Diffusion models generate images by **transforming random noise into coherent images** through **iterative denoising**. This differs from GANs: no adversarial training and no single-step generation.

### Training
- Noise is gradually added to images (forward process); the model learns to reverse it.
- The neural network is trained to **estimate (predict) the noise** in an image accurately.
- Common loss: **L2 loss** (MSE between predicted and true noise).
- **U-Net** is the commonly used architecture for noise prediction.
- Noise is managed effectively with **time-dependent noise scheduling**.

### Time conditioning
- The model receives the timestep as input.
- It **informs the model how much noise to remove at each step** and guides the diffusion process at every step.

### Generation (multi-step process)
- Start from pure noise and **incrementally remove noise** step by step, revealing image details gradually.
- The multi-step approach is what makes high-quality generation possible.

## Quick comparison

| | CLIP | Diffusion model |
|---|---|---|
| Goal | Align image and text embeddings | Generate images from noise |
| Key mechanism | Contrastive loss on similarity matrix | Iterative denoising |
| Loss | Symmetric cross-entropy over similarities | L2 on predicted noise |
| Architecture | Image encoder + text encoder | U-Net with time conditioning |
| Typical use | Zero-shot classification, retrieval | Image generation |
