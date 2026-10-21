# Residual Networks, Skip Connections and U-Net: Module Notes

Summary of the module: higher-order logic in deep networks, residual learning, skip connections and the U-Net encoder-decoder.

## 1. Logic in neural networks

- As layers are added, each layer can represent increasingly higher-order logic built on the outputs of the previous layers.
- A deep-layer neuron that performs an AND over the outputs of earlier neurons combines simpler concepts into more complex ones (higher-order logic).
- Mixing first- and second-order terms in one layer combines the original input features with learned features, giving richer representations.

## 2. The problem with deep networks

- **Exploding gradients**: repeated multiplication by large weights during backpropagation.
- **Vanishing gradients**: repeated multiplication by small values; the gradient fades out.
- Without an identity mapping, important input features can become unavailable to deep layers.

## 3. Residual Networks (ResNet)

**Idea:** a layer does not learn the full transformation, only what has to be *added* to its input.

```
y = F(x) + x
```

- `F(x)` is the **residual**: the extra information that must be added to the input to get the desired output (the difference between the desired output and the input).
- The addition happens **before** the activation function: `output = activation(F(x) + x)`.
- Analogy: instead of rebuilding a house from scratch, improve it step by step by adding to it.
- **Division of labour**: early layers extract features, later layers learn what to add to their input.

### Why it helps

- Makes it possible to train very deep networks effectively.
- Helps against vanishing gradients: part of the gradient path turns from a multiplication into an **addition**.
- Shortcut connections make gradient flow easier.
- Information from early layers is preserved (identity mapping).
- It does not replace activation functions or backpropagation, and it does not fully remove overfitting.

## 4. Skip connections

- Go directly between **non-consecutive** layers.
- Use an identity mapping to preserve information.
- Do not duplicate weights and do not need new activation functions.

## 5. Concatenation vs addition

| | Addition | Concatenation |
|---|---|---|
| Operation | element-wise sum | stacking feature maps |
| Requirement | identical shapes | shapes match on all other axes |
| Effect | dimensions are **preserved** | number of features (channels) for the next layer grows |

## 6. U-Net

- Named after the **U-shaped** encoder-decoder architecture.
- Output is an **image**, e.g. a segmentation mask.
- The **encoder** compresses the input, the **decoder** restores the resolution.
- The **bottleneck ("code" layer)** holds the most important features in compressed form.
- **Skip connections** pass feature maps from early layers to later ones so that fine details can be reused.

## 7. Upscaling in the decoder

- **Parametric upscaling** learns the parameters that best reconstruct high-resolution features. The output depends on both the input and the learned kernel.
- **Transpose convolution**:
  - increases the spatial size (spatial resolution);
  - is a matrix multiplication with learned filters (the transpose of the convolution matrix);
  - unlike ordinary convolution, it enlarges rather than shrinks the output.
- **Convolutional vs fully connected upscaling**: the first uses spatially applied filters, the second uses large weight matrices.
