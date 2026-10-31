# Image Matching with LoG Edges, SIFT and FLANN

Computer vision course project (USTO-MB, M1 AI & Applications, 2025/2026).

The goal is to match images of the same object seen from different viewpoints, using only **edges** as detection primitives, and to compare this with running SIFT on the full image.

## Pipeline

```
Images → LoG (edges) → Morphological dilation → SIFT on mask → FLANN matching
                                                                ↕ comparison
                                                SIFT on full image → FLANN matching
```

1. **Edge extraction**: Laplacian of Gaussian (LoG) filter + thresholding, then morphological dilation (5×5 elliptical kernel)
2. **SIFT detection** restricted to the dilated edge mask
3. **FLANN matching** (KD-tree) with Lowe's ratio test (0.75) on the 3 image pairs, with and without the mask

## Findings

On these three views of a single object on a dark background, restricting SIFT to the LoG edge mask gave essentially the same result as SIFT on the full image (88 valid matches in total for both). The notebook discusses why, and when a mask would matter more (cluttered backgrounds).

## Repository content

| Path | Description |
|------|-------------|
| `image_matching_sift_flann.ipynb` | The full notebook, with outputs |
| `images/` | The 3 input views (`im1.png`, `im2.png`, `im3.png`) |
| `requirements.txt` | Python dependencies |

## Run it

**On Kaggle:** <!-- add your Kaggle notebook link here -->

**Locally:**

```bash
pip install -r requirements.txt
jupyter notebook image_matching_sift_flann.ipynb
```

The notebook reads the images from the Kaggle input folder when it exists, and from the local `images/` folder otherwise.

## Data

The images come from the [Middlebury multi-view datasets](https://vision.middlebury.edu/mview/data/). Please refer to that page for the terms of use of the original data.
