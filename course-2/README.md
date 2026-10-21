# Course 2 — Deep Learning for Computer Vision (University of Colorado Boulder, Coursera)

Module notes and practice notebooks for the second CU Boulder computer vision course on Coursera.
Each module has a `notes.md` summary and a self-contained notebook that implements the module's ideas from scratch in NumPy (forward and backward passes written by hand).

## Module 1 — Neural Networks

- [Notes](module-1/notes.md)
- [1. Neural networks from scratch](module-1/1_neural_networks_from_scratch.ipynb): linear layer and bias trick, batched matmul, ReLU/Leaky ReLU/sigmoid/tanh, a 2-layer network learning a non-linear boundary, softmax vs sigmoid, BatchNorm vs LayerNorm

## Module 2 — CNN Fundamentals

- [Notes](module-2/notes.md)
- [2. CNN from scratch](module-2/2_cnn_from_scratch.ipynb): im2col convolution and output-size formula, Sobel filters, max-pool forward/backward, softmax + cross-entropy gradient, conv/ReLU/pool backward with numerical gradient check, training a tiny CNN on synthetic bars

## Module 3 — Autoencoders, Gradient Descent and GANs

- [Notes](module-3/notes.md)
- [3. Autoencoders and GANs](module-3/3_autoencoders_and_gans.ipynb): gradient descent and learning rate, numerical gradient checks for L2 and BCE, an autoencoder with a 2D bottleneck, latent-space walk, a 1D GAN with alternating updates

## Module 4 — Residual Networks, Skip Connections and U-Net

- [Notes](module-4/notes.md)
- [4. ResNet, skip connections, U-Net](module-4/4_resnet_skip_connections_unet.ipynb): higher-order logic via AND, vanishing gradients in plain vs residual networks, residual block, addition vs concatenation, transpose convolution as `C^T`, a tiny U-Net forward pass with shape tracing

All notebooks are executed with outputs and use synthetic data only (no downloads). Requirements: `numpy`, `matplotlib`.
