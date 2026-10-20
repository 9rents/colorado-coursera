# University of Colorado Boulder — Computer Vision (Coursera)

Module notes and practice notebooks for the CU Boulder computer vision course on Coursera.
Each module has a `notes.md` summary and a self-contained notebook that implements the module's ideas from scratch in NumPy.

## Module 1 — Image Arrays, Linear Combinations and 2D Transformations

- [Notes](module-1/notes.md)
- [1. Image arrays and 2D transforms](module-1/1_image_arrays_and_2d_transforms.ipynb): RGB arrays, normalization, image blending, 2D Gaussian, scaling/translation/rotation matrices, why order matters

## Module 2 — Image Features and Similarity

- [Notes](module-2/notes.md)
- [2. Image features and similarity](module-2/2_image_features_and_similarity.ipynb): image moments, histograms, gradients and HoG, L1/L2/cosine/cross-entropy

## Module 3 — Filtering, Morphology and the Camera Model

- [Notes](module-3/notes.md)
- [3. Filtering, morphology, camera model](module-3/3_filtering_morphology_camera_model.ipynb): 1D correlation vs convolution, mean/Gaussian/Laplacian, ReLU and MaxPool, im2col, morphological operations, 3D rotation and perspective projection

## Module 4 — Camera Geometry and Epipolar Geometry

- [Notes](module-4/notes.md)
- [4. Epipolar geometry](module-4/4_epipolar_geometry.ipynb): `P = K[R | t]`, surface normals, Essential and Fundamental matrices, epipoles and epipolar lines, normalized 8-point algorithm

All notebooks are executed with outputs and use synthetic data only (no downloads). Requirements: `numpy`, `matplotlib`.
