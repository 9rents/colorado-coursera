# Computer Vision: Image Arrays, Linear Combinations and 2D Transformations

Summary of the module (image representation, simple image math, matrix transformations).

## 1. Image arrays and pixel representation

- An image is stored as an array (matrix) of pixel values. This gives a structured format for storing data, makes pixel-level manipulation and analysis possible, and allows efficient processing.
- **RGB model**: three channels (Red, Green, Blue). Each channel stores intensity, typically as one byte (0-255). The alpha channel is *not* part of RGB (it is transparency).
- **Normalization**: arrays of type `double` are converted to image metrics by scaling values to a specific range (e.g. [0, 1] or [0, 255]).
- **LED matrix simulation**: an RGB image can be arranged as an LED screen. The essentials are uniform pixel spacing and precise pixel alignment.
- **Excel for simulation**: Conditional Formatting (color scales) is used to display pixel values and visualize functions as heat maps. The benefit is easy manipulation of pixel data.

## 2. Modifying images

- Dimension changes: resizing, scaling, cropping.
- Image scaling simplifies high-resolution images while preserving essential details.
- Multiplying every pixel by a factor > 1 makes the image brighter.

## 3. Linear combination of images

- Result = weighted sum of pixel values: `R(x, y) = a * I1(x, y) + b * I2(x, y)`.
- Key components: constant multipliers, coefficient parameters, weighted sum of pixel values.
- Math concepts involved: scalar multiplication, matrix addition, weighted averaging.
- Example: a = 0.5, b = 0.3, I1 = 200, I2 = 150, so R = 0.5*200 + 0.3*150 = 100 + 45 = **145**.

## 4. 2D Gaussian

- The spread of a 2D Gaussian is controlled by sigma (σ). The mean (μ) sets the center.
- Can be visualized in Excel as a heat map with Conditional Formatting.

## 5. 2D transformations with matrices

| Transformation | What it does | Notes |
|---|---|---|
| **Scaling** | Changes size along x and y (`sx`, `sy`) | `sx = sy = 2` doubles the object. Different `sx`/`sy` change proportions. Does not rotate or translate. |
| **Translation** | Shifts all points by a constant vector (`tx`, `ty`) | Changes position only, not size, shape or orientation. Uses displacement parameters. |
| **Rotation** | Rotates around a point (origin by default) | Not done by scaling or translation matrices. |

- Scaling and translation matrices can be combined for comprehensive transformations.
- Transforming a group of points = **matrix multiplication** (a linear transformation applied to point coordinates).
- Transformation matrices use real-number coefficients, not only integers; formulas define the relation between points and matrices.
- **Order matters**: matrix multiplication is not commutative, so the order in which transformations are applied changes the result.
- Core idea: **coordinate transformation using matrices** is how images are transformed in computer vision.
- GPUs (3D gaming, deep learning) use matrix multiplication to accelerate the computation of transformations.

## 6. Responsible AI use (course policy)

- Violations can lead to: a warning, a 0-50% grade on the assignment, failing the course, loss of access to course materials, or referral to student conduct.
- Never enter another person's private data into an AI tool without consent.
- Main ethical risk: unintentional plagiarism or data fabrication.
- Where AI is not permitted, only non-AI tools (e.g. built-in spell check) are allowed.
- Where full AI use is allowed: document your use and maintain privacy and security.
