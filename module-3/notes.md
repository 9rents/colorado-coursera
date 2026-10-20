# Computer Vision & Image Recognition: Module Notes

Summary of the module: from 1D signal filtering to 2D image processing and 3D camera geometry.

## 1. Signals and 1D filters

**Sliding window**
- Moves a small window over the signal, so every output value depends on a local neighborhood.
- Basis for filtering, smoothing and feature detection.

**Cross-correlation vs convolution**
- Cross-correlation measures similarity between a filter and each segment of the signal; peaks mark where the pattern occurs.
- Convolution is the same operation, but the filter is flipped before computation. Cross-correlation does not flip it.
- Neither requires normalization, and neither guarantees perfect pattern detection.
- Both are linear operations and the core of 1D filtering (denoising, enhancing frequency components, edge detection).

**Common filters**

| Filter | What it does |
|---|---|
| Mean | Averages neighboring values; reduces random noise, smooths transitions |
| Gaussian | Weighted average (Gaussian weights); designed by choosing standard deviation and kernel size |
| Laplacian | Second derivative; highlights regions of rapid change, used for edge detection |

**Non-linear operations**
- ReLU: `max(0, x)`. Output is zero for negative inputs. Non-linear, widely used in neural networks.
- MaxPool: non-parametric and non-linear.
- Non-linear transformations allow complex mappings of the input signal.

## 2. 2D image processing

**Sliding windows in 2D**
- Convolution/correlation applies a filter over pixel neighborhoods.
- Image-to-column (im2col): each window is turned into a matrix column, so filtering becomes matrix multiplication.
- Output size: `floor((N + 2P - K) / S) + 1`
  (N input size, K filter size, P padding, S stride). A larger stride gives a smaller output. Larger filters capture more spatial context.

**Padding**
- Padding with 1 (for a 3x3 filter) preserves the spatial dimensions of the image and handles boundary conditions.

**Smoothing**
- Mean filter: averages the neighborhood; filter size controls how strong the smoothing is.
- Gaussian filter: weighted average, smoother result than the mean filter.
- Laplacian: detects edges and boundaries.

**Morphological operations**

| Operation | Definition | Effect |
|---|---|---|
| Dilation | Max over the neighborhood | Expands bright/foreground regions |
| Erosion | Min over the neighborhood | Thins foreground objects |
| Open | Erosion, then dilation | Removes small objects, smooths boundaries |
| Close | Dilation, then erosion | Fills small holes, smooths boundaries |
| Gradient | Dilation minus erosion | Highlights object outlines |

Steps of dilation: define the neighborhood of each pixel, take the maximum. Erosion: apply a minimum filter, with padding for borders.

**Functional style for image processing**
- `map` for per-pixel manipulation, `filter` for selecting pixel values, working by column.

## 3. 3D geometry and the camera model

**Rotation matrices**
- Define rotations by an angle around the x, y and z axes.
- Rotate an object about any of the three axes. They do not translate or scale.

**Translation**
- Shifts coordinates of objects relative to the camera / the camera position in 3D space.

**Extrinsic matrix** `[R | t]`
- World coordinates to camera coordinates (rotation + translation).

**Intrinsic matrix** `K`
- Camera coordinates to pixel coordinates.
- Contains camera-specific parameters: focal length and principal point offset.

**Perspective projection**

```
u = f * X / Z + c_x
v = f * Y / Z + c_y
```

Pipeline: world point -> extrinsics -> camera coordinates -> intrinsics (focal length, offset) -> pixel coordinates.
