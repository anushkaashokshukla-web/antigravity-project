# Implementation Plan - Image Processing Post-Lab Web Portal (All 10 Practicals)

Build a complete, interactive, state-of-the-art **Image Processing Post-Lab Web Application** covering all 10 curriculum practicals with real-time browser-based computer vision simulations, mathematical theory, post-lab questions & viva answers, Python OpenCV code snippets, self-assessment quizzes, and a printable lab report generator.

## User Review Required

> [!IMPORTANT]
> The application will be created as a standalone Vite + React project inside `c:\Users\Anushka Shukla\OneDrive\Desktop\ip-postlab-portal` using Vanilla CSS (no Tailwind, per web guidelines) with custom glassmorphism design, dark/light mode, and full client-side HTML5 Canvas / TypedArray image processing algorithms for all 10 practicals.

Please review the proposed architecture and modules below.

## Practicals Covered

The web portal includes 10 dedicated modules for each practical:

1. **Practical 1: Image Formats, Arithmetic & Bitwise Operations**
   - RGB to Grayscale conversion, Bit-plane slicing (visualizing 8 bit planes).
   - Pixel arithmetic (clamped addition, subtraction, blending $\alpha A + (1-\alpha)B$).
   - Bitwise operations (AND, OR, XOR, NOT).`
   - Post-lab analysis: uint8 saturation vs overflow, channel weighting.

2. **Practical 2: 2-D Geometric Transformations**
   - Interactive canvas affine transformations: Translation ($T_x, T_y$), Rotation ($\theta$), Scaling ($S_x, S_y$), Shearing ($Sh_x, Sh_y$), Reflection (Horizontal, Vertical, Origin), and Interactive Cropping.
   - Transformation matrix breakdown and coordinate mapping visualization.

3. **Practical 3: Spatial Domain Enhancement & Thresholding**
   - Histogram Equalization: Dynamic before/after intensity histograms, CDF mapping curve.
   - Spatial Filtering: 3x3 Box Smoothing vs Laplacian Sharpening.
   - Segmentation Thresholding: Manual slider, Otsu's optimal automatic thresholding, Adaptive local thresholding.

4. **Practical 4: Spatial Domain Filter Showdown**
   - Averaging Filter (Box blur), Gaussian Filter with variable $\sigma$.
   - Median Filter (impulse/salt-and-pepper noise removal).
   - Bilateral Filter (range + spatial kernel edge-preserving smoothing).
   - Noise injection tool (Gaussian noise, Salt & Pepper) to test filter resilience.

5. **Practical 5: Image Inpainting (Telea vs Navier-Stokes)**
   - Interactive scratch/damage canvas brush to artificially degrade images.
   - Telea Method (Fast Marching gradient boundary propagation).
   - Navier-Stokes Method (PDE fluid dynamics isophote curvature diffusion).
   - Quantitative & visual comparison of restoration artifacts.

6. **Practical 6: Lossless Image Compression**
   - Run-Length Encoding (RLE) encoder/decoder.
   - Huffman Coding engine: Pixel frequency analysis, Huffman tree generation, variable-length code table.
   - Compression metrics: Original vs Compressed size (bytes), Compression Ratio ($CR$), Entropy ($H$), Bitrate (bpp).

7. **Practical 7: Morphological Operations on Binary Images**
   - Structuring elements: Square, Cross, Disk with adjustable sizes ($3\times 3, 5\times 5, 7\times 7$).
   - Operations: Erosion, Dilation, Opening (noise removal), Closing (hole filling), Morphological Gradient / Boundary extraction.

8. **Practical 8: Object Detection using Correlation**
   - Normalized Cross-Correlation (NCC) template matching algorithm.
   - Interactive template selector box + preset library.
   - Correlation peak coordinates, bounding box overlay, and 2D correlation score heatmap.

9. **Practical 9: Edge Detection (Canny vs Sobel vs Prewitt)**
   - Sobel gradient operators ($S_x, S_y$).
   - Prewitt gradient operators ($P_x, P_y$).
   - Full Canny Edge Pipeline: Gaussian smoothing $\rightarrow$ Sobel gradient & orientation $\rightarrow$ Non-maximum suppression $\rightarrow$ Double thresholding & Hysteresis edge tracking.
   - Side-by-side tri-view comparison with edge density stats.

10. **Practical 10: Color Space Studio (RGB, HSV, YCrCb, Lab)**
    - Channel decomposition:
      - RGB (Red, Green, Blue)
      - HSV (Hue, Saturation, Value)
      - YCrCb (Luma, Chroma Blue, Chroma Red - JPEG/MPEG basis)
      - CIE Lab (Perceptual Lightness, a* Green-Red, b* Blue-Yellow)
    - Isolating luminance from chrominance analysis.

## Core Features & Architecture

- **Interactive Lab Workbench**:
  - Sample image loader (Cameraman, Lena, Baboon, Coins, Damaged vintage photo, Low-contrast landscape) + Custom image upload.
  - Interactive controls (sliders, color pickers, toggles, brush tool) with instant real-time canvas updates.
- **Post-Lab Theoretical Deep-Dive & Viva Bank**:
  - Step-by-step mathematical formulations and algorithms.
  - Comprehensive post-lab questions and verified answers for university lab viva.
- **Python / OpenCV Reference Implementations**:
  - Ready-to-copy, clean Python code snippets for every practical with syntax highlighting.
- **Interactive Post-Lab Assessment / Quiz**:
  - 5-10 curated multiple-choice and conceptual questions per practical with instant scoring and explanations.
- **Submission-Ready Post-Lab Report Exporter**:
  - Custom student metadata input (Name, Roll No, Batch, Date).
  - Select individual practical or all practicals.
  - Clean printable / PDF format with aims, observations, results, and post-lab Q&A.
- **Design & UI**:
  - Responsive, dark/light modern UI with sleek glassmorphism, glowing accents, clean typography (Inter / JetBrains Mono), smooth micro-animations, and tabs.

## Proposed Changes

### Project Setup
- Create project directory `c:\Users\Anushka Shukla\OneDrive\Desktop\ip-postlab-portal`
- Initialize Vite + React project using `npm.cmd`
- Install necessary icons (`lucide-react`) and setup Vanilla CSS design system

### Directory Structure
```
ip-postlab-portal/
├── index.html
├── package.json
├── src/
│   ├── main.jsx
│   ├── index.css                   # Comprehensive design system, glassmorphism, animations
│   ├── App.jsx                     # Main shell, navigation, global state, header/footer
│   ├── components/
│   │   ├── Navbar.jsx              # Navigation between 10 practicals, Quiz, Report Exporter
│   │   ├── ImageViewer.jsx         # Canvas before/after split viewer, zoom/pan
│   │   ├── CodeViewer.jsx          # Syntax highlighted Python OpenCV code
│   │   ├── QuizModal.jsx           # Post-lab interactive quiz per practical
│   │   ├── ReportExporter.jsx      # Printable lab report generator
│   │   └── TabNavigation.jsx       # Practical sub-tabs: Interactive Demo, Theory, Code, Viva
│   ├── practicals/
│   │   ├── practicalData.js        # Aims, theory, formulas, viva Q&A, quiz questions, python codes
│   │   ├── Practical1_Formats.jsx
│   │   ├── Practical2_Geometric.jsx
│   │   ├── Practical3_Enhancement.jsx
│   │   ├── Practical4_Filters.jsx
│   │   ├── Practical5_Inpainting.jsx
│   │   ├── Practical6_Compression.jsx
│   │   ├── Practical7_Morphology.jsx
│   │   ├── Practical8_Correlation.jsx
│   │   ├── Practical9_Edges.jsx
│   │   └── Practical10_ColorSpaces.jsx
│   └── utils/
│       ├── imageProcessing.js      # Pure JS image algorithms (convolution, morphology, ncc, canny, etc.)
│       └── sampleImages.js         # Embedded test patterns and synthetic benchmark images
```

## Verification Plan

### Automated / Build Verification
- Run `npm run build` in `ip-postlab-portal` to ensure zero compilation or bundling errors.

### Interactive Browser Verification
- Launch Vite dev server on local port (e.g. `http://localhost:5173`).
- Use the `browser_subagent` to navigate through:
  - Practical 1 through 10 interactive demos and verify canvas outputs.
  - Test sliders, image uploads, and transformations.
  - Test the Quiz system scoring and review.
  - Test the Report Exporter generation view.
