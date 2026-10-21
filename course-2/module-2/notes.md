# CNN Fundamentals: Module Notes

Summary of the module on convolutional neural networks (CNNs): architecture, forward pass, loss function and backpropagation.

## 1. Why CNNs

- CNNs automatically extract hierarchical features from images: from low-level (edges, textures) to high-level (shapes, objects).
- Similar to an MLP: layers of weights + activation functions, trained with gradient descent. The difference: convolutional layers use filters with shared weights and respect spatial structure.
- They map well onto GPUs: convolution can be written as one large matrix multiplication (im2col + matmul).

## 2. Convolutional layer

- Filters (kernels) detect patterns: edges, textures, etc.
- **Handcrafted vs learned**: handcrafted filters are designed by hand (Sobel etc.), learned filters are optimized during training.
- Number of output feature maps = number of filters.
- Filter depth = number of input channels, so all channels are processed at once.
- Larger filter -> captures larger patterns.
- Stride (together with filter size and padding) determines the output size: `out = (in + 2p - k) / s + 1`.
- **Padding**: adding pixels around the border; preserves the spatial size of the feature map after convolution.

## 3. Pooling

- Max-pooling reduces the size of the feature maps while keeping the strongest activations.
- Pooling layers have no parameters (nothing is learned) and do not normalize the data.
- Convolution learns a feature hierarchy; pooling reduces dimensionality.

## 4. Activations and regularization

- ReLU passes the gradient only for positive inputs.
- Dropout and Batch Norm are for regularization and stabilization, not for reducing dimensionality.

## 5. Classifier and loss

- A fully connected (linear) layer maps the extracted features to class scores (logits).
- Softmax turns logits into a probability distribution; the probabilities always sum to 1.
- **Categorical cross-entropy**:
  1. softmax of the model outputs,
  2. true labels as one-hot vectors,
  3. negative log-likelihood of the predicted probabilities.
- `prediction - target` = gradient of the loss with respect to the logits.

## 6. Backpropagation

- The gradient says how much and in which direction to change the weights (the direction that minimizes the loss).
- **MaxPool backward**: the gradient goes only to the position of the maximum, so the argmax indices are stored during the forward pass.
- If several gradients land in the same position, they are summed.
- **Conv backward**: gradients from different windows are summed, because the same weight is shared across many spatial positions (weight sharing).
- **ReLU backward**: the gradient flows only where the input was > 0.
