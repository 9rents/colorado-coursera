# Transformers & Attention: Module Notes

Summary of the key concepts from the module on attention, transformers and Vision Transformers (ViT).

## 1. Self-Attention

- **Formula:** `Attention(Q, K, V) = softmax(QKᵀ / √d_k) · V`
- **Steps:** compute dot products between queries and keys -> scale by `√d_k` -> apply softmax -> multiply by values.
- **Softmax** normalizes attention scores so they sum to 1 for each query across all keys.
- **Scaling by √d_k** prevents large dot-product values from dominating the softmax (saturation, tiny gradients).
- **Attention-weighted input** = a linear combination of value vectors weighted by attention scores.
- **Why it helps MLPs:** each input can incorporate context from other positions.
- **Matrix form:** attention is computed efficiently by multiplying the attention matrix (softmax scores) with the value matrix `V`.

## 2. Positional Encoding

- Attention is order-agnostic, so positional encoding gives the model information about the **position of tokens** in the sequence.

## 3. Multi-Head Attention

- Implemented by running **several attention mechanisms in parallel**.
- Implemented efficiently with a **single large matrix multiplication** that combines projections.
- Head outputs are concatenated, then a **final linear projection** returns the output to the original model size (needed for consistency and layer stacking).

## 4. Self-Attention vs Cross-Attention

| | Self-attention | Cross-attention |
|---|---|---|
| Sequences | Operates on the **same** sequence | Interaction between **two** sequences |
| Attention matrix | **Square** | **Rectangular** |
| Role | Context within a sequence | Decoder attends to encoder output representations |

## 5. Transformer Decoder

- **Autoregressive decoding:** generates **one token at a time**, using previously generated tokens as input.
- **Final linear layer** maps decoder output to **vocabulary logits** for word prediction.
- **Softmax** turns logits into a probability distribution.
- **Sampling** after softmax introduces variability and produces diverse outputs.

## 6. Skip Connections & Normalization

- **Skip connections + layer normalization** stabilize training and preserve information across layers.
- **LayerNorm** normalizes across neurons within a layer; **BatchNorm** normalizes across batch samples.
- ViTs use **LayerNorm** because BatchNorm becomes impractical with large batch sizes / depends on batch statistics.

## 7. Vision Transformer (ViT)

Image -> tokens pipeline:
1. **Divide the image into fixed-size patches**
2. **Flatten each patch** into a vector
3. **Linearly embed** the vectors and add **positional information**

- **Positional encoding** preserves spatial information lost when patches are flattened.
- **Class token** aggregates information for classification.
- **Attention** lets the model focus on important parts of the image.
- **Consistent model size across layers** ensures compatibility between layers for stacking.

## 8. Training for Classification

- **Softmax** after the final linear projection converts raw scores into a probability distribution over classes.
- **Loss gradient** for categorical classification (softmax + cross-entropy): `Prediction − Target`.
