# Neural Networks: Module Notes

Summary of the module: network structure, linear layers, matrix computation, activation functions, softmax and normalization.

## 1. Network structure

- Layers: input -> hidden -> output.
- A "2-layer neural network" = one hidden layer + the output layer. The input layer is not counted.
- Hidden nodes receive signals from the input nodes. The output layer aggregates the outputs of several hidden nodes, weighted by the connection weights.

## 2. Linear layer

- Computes a weighted sum of the inputs and adds a bias:

```
Y = WX + b      (or Y = XW + b, depending on the row/column convention)
```

- **Weights** set how strongly each input value influences the next layer.
- **Bias** lets the model learn an offset. It is added to the weighted sum *before* the activation function and is used in every layer, not only the input one.
- **Bias trick**: append a constant `1` to the input vector, so the bias becomes an extra column of the weight matrix and the whole layer is one matrix operation.
- A linear layer on its own adds no non-linearity; that comes from the activation function.

Order of operations in a layer:

```
matrix multiplication -> bias addition -> activation function
```

## 3. Matrix computation and batches

- Matrix multiplication transforms the input data as it passes through the layers.
- A batch = several inputs processed at once by the same network (same weights) with one batched matrix multiplication.
- The graphical view of a network gives intuition about linear transformations.
- Key elements when visualizing a network: input layer, weight matrices, bias terms, activation functions.

## 4. Activation functions

| Function | Formula | Notes |
|---|---|---|
| ReLU | `f(x) = max(0, x)` | 0 for negative inputs, x for positive ones |
| Leaky ReLU | `f(x) = x if x > 0, αx if x <= 0` | small non-zero gradient for negative inputs |
| Sigmoid | `f(x) = 1 / (1 + e^(-x))` | output in (0, 1) |
| Tanh | `f(x) = (e^x - e^(-x)) / (e^x + e^(-x))` | output in (-1, 1) |

- Combining the outputs of several hidden nodes (weighted sum) with a non-linear activation lets the network learn more complex decision boundaries.

## 5. Softmax

```
softmax(z)_i = e^(z_i) / Σ_j e^(z_j)
```

- Order: exponentiate every output, then divide by the sum of all exponentials.
- Turns raw outputs (logits) into probabilities: values in (0, 1) that sum to 1.
- For multi-class classification it is preferred over sigmoid because it gives a proper probability distribution over the classes.
- Softmax is preceded by a final linear transformation, so that the number of output units equals the number of classes.

## 6. Normalization

### Batch Normalization

- Goal: stabilize training and improve convergence; also allows larger learning rates.
- Helps when the input distribution shifts (e.g. image brightness changes): the network behaves consistently.
- Applied **after the linear transformation and before the activation function**.
- Formulas:

```
x_hat = (x - μ_B) / sqrt(σ_B² + ε)
y     = γ · x_hat + β
```

- `ε` is a small constant that prevents division by zero.
- `γ` (gamma) and `β` (beta) are learnable scale and shift parameters for the normalized output.

### Layer Normalization

- Does not depend on the batch size and does not need large batches.
- Normalizes across the features of a single example (not across the batch).
- Note: the quiz phrased this as "normalization occurs across each neuron in the layer", which is slightly imprecise: the statistics are computed over all neurons of the layer, separately for each example.
