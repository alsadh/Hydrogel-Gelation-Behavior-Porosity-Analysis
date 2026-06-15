# Hydrogel-Gelation-Behavior-Porosity-Analysis

This repository contains the Google Colab file that was used to perform pore analysis for Clarkson University's Almeida Lab. 

## Requirements

Running the file requires saving it to your google drive. 

## Visualization

To simply run the visualization of the pore segmentation on a single image, run the last two code blocks and modify the path in 

```python
visualize_segmentation("/content/drive/MyDrive/path/to/your/image.tif")
```

to an SEM file in your google drive.

## Full Analysis

To run the full analysis, a specific workspace is required. The workspace must have the following folder structure in your google drive:

```
root/
├── sample_1/
│   ├── Core/
│   │   ├── subfolder_1/
│   │   │   ├── image1.tif
│   │   │   └── image2.tif
│   │   └── subfolder_2/
│   │       └── image3.tif
│   ├── Mold/
│   └── Top/
├── sample_2/
├── sample_3/
└── ...
```

## Outputs

The analysis generates summary statistics for each sample in an excel file that averages the pore count, area in micrometers, circularity, eccentricity, and porosity ratio. It also generates box plots for each of these statistics.

## Scale

To calculate the area, a scale of **267 pixels = 100 µm** is used via the scalebar present in our SEM images. If your scale is different, modify this in the second code block by changing the "100/267" in the line

```python
"avg_area_micrometer": (np.mean(areas)*((100/267) ** 2)) if areas else 0
```

## Modifiable Parameters

| Parameter | Default | Description |
|---|---|---|
| `blockSize` | 501 | Adaptive threshold neighborhood size (must be odd and larger than largest pore diameter) |
| `C` | 7 | How much darker than local mean a pixel must be to count as a pore |
| `h` | 6 | Minimum prominence of a peak in the distance transform to count as a separate pore |
| `sigma` | 3 | Gaussian smoothing of distance transform before watershed |

