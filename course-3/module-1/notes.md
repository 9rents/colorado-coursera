# SVM, RBF Kernel and Discrete Fourier Transform: Module Notes

Summary of the module: support vector machines, the RBF kernel, and the DFT / inverse DFT in 1D and 2D.

## 1. Support Vector Machine (SVM)

### Core idea
An SVM finds the hyperplane that separates the classes with the **maximum margin**. The decision function is:

```
f(x) = sign(w·x + b)
```

- **w** sets the orientation of the hyperplane (its normal).
- **b (bias)** shifts the decision boundary **without changing its orientation**.

### Support vectors
- The training points closest to the hyperplane.
- The hyperplane is defined (and adjusted) only by them; the other points have no influence on it.
- A point is a support vector if its **Lagrange multiplier is non-zero (α > 0)**.
- Support vectors do not have to lie exactly on the margin and are not "equidistant from all hyperplanes"; the defining property is α ≠ 0.

### Training: SVM vs neural networks

| | SVM | Neural network |
|---|---|---|
| Optimization | Convex, global optimum | Non-convex, gradient descent |
| Weight updates | Solving a QP problem (dual form, α) | Backpropagation + gradient descent |
| Architecture | No feed-forward layers | Layers, activations |

## 2. Kernel trick and the RBF kernel

A kernel computes a dot product in a high-dimensional feature space without explicitly mapping into it.

**RBF (Gaussian) kernel:**

```
K(x, x') = exp(-γ · ||x - x'||²)
```

### Visualization
- Linear kernel -> straight lines (hyperplanes) in the original space.
- RBF kernel -> **circular / elliptical contours centered on the support vectors**; a point's influence decays with distance.

### Hyperparameters

| Parameter | What it does |
|---|---|
| **γ (gamma)** | Sets the kernel "width" and the **smoothness / locality of the decision boundary** |
| **C** | Regularization strength: trade-off between margin width and classification errors |

**Effect of gamma:**
- **Small γ** -> wide kernel -> smooth, simpler boundary (risk of underfitting).
- **Large γ** -> narrow kernel -> complex, localized boundary (risk of overfitting).

## 3. Discrete Fourier Transform (DFT)

### Purpose
The DFT **decomposes a signal into its frequency components**.

```
X[k] = Σ_{n=0}^{N-1} x[n] · e^{-2πi·kn/N}
```

### Basis functions
- Built from **cosines and sines** (via Euler's formula `e^{iθ} = cos θ + i sin θ`).
- Form a set of **orthogonal functions** for decomposing the signal.
- The number of cycles of a basis function is set by the **frequency index k**.
- Interpretation: the DFT measures **how similar the signal is to each sin/cos basis function** (dot product = similarity measure).

### DFT as matrix multiplication
- The DFT can be written as `X = W · x`, where W is the Fourier matrix (rows = basis functions).
- Analogy with a **linear layer** of a neural network: multiplying the input vector by a weight matrix (the difference: W is fixed, not learned).
- **Why matmul instead of the FFT:** it parallelizes efficiently on GPUs, which makes it competitive with the FFT on modern hardware. (It is not more accurate, and not faster on every kind of hardware.)

## 4. Inverse DFT (IDFT)

- Goal: **reconstruct the signal from the frequency domain** (frequency domain -> time/spatial domain).
- Uses the same basis functions with the opposite (complex-conjugate) sign in the exponent:

```
x[n] = (1/N) · Σ_{k=0}^{N-1} X[k] · e^{+2πi·kn/N}
```

## 5. 2D DFT / 2D inverse DFT (images)

- For images we say **"spatial domain"**, not "time domain": 2D signals are defined over space, not time.
- **2D DFT basis functions** combine the spatial indices **(x, y)** with the frequency indices **(u, v)**:

```
e^{-2πi (ux/M + vy/N)}
```

- The **scaling factor** of the 2D IDFT is `1 / (M · N)`, i.e. the product of the number of rows and columns.
- In the IDFT the basis functions are used to **reconstruct the spatial signal from its frequency components**.
- **Why visualize the IDFT result:** it shows how individual frequency components contribute to the spatial structure of the image (low frequencies = overall shape, high frequencies = details and edges).

## Quick cheat sheet

- `b` -> shifts the boundary, orientation unchanged
- Support vector ⇔ `α ≠ 0`
- RBF -> radial contours around support vectors
- `γ ↑` -> narrower kernel, more complex boundary; `γ ↓` -> wider kernel, smoother boundary
- `C` -> regularization; `γ` -> boundary smoothness
- SVM -> convex optimization; NN -> backprop + GD
- DFT -> decomposition into frequencies; IDFT -> signal reconstruction
- DFT basis -> sin/cos, orthogonal set, number of cycles set by `k`
- 2D IDFT scaling -> `1 / (rows × cols)`
- Matmul vs FFT -> wins through GPU parallelism
