# Usage Guide

## 1. Install dependencies

Install Wolfram Mathematica and ExifTool. Confirm that ExifTool is available in a terminal:

```bash
exiftool -ver
```

## 2. Prepare a working directory

Create a directory outside the repository for the image data and generated files. Keeping data outside the repository reduces the risk of accidentally committing sensitive images.

Example:

```text
thermal-analysis-run/
├── before.jpg
├── before_mask.png
├── after.jpg
└── after_mask.png
```

## 3. Open and evaluate the notebook

Open:

```text
notebooks/compare_flirr_v6_well_commented.nb
```

Evaluate cells from top to bottom. The notebook first clears symbols in the `Global`` context and defines helper functions used later in the analysis.

## 4. Respond to interactive prompts

The main workflow asks for:

- Working directory.
- Before-image JPEG filename.
- Before-image split ratio.
- Before-image minimum and maximum temperature.
- Thermal PNG filename or confirmation prompts.
- Orientation and processing choices.
- Equivalent values for the after image.

Use numeric input where a number is expected. Keep a record of every response for reproducibility.

## 5. Extract raw thermal images

For each FLIR JPEG, the notebook prints an ExifTool command based on this pattern:

```bash
exiftool -b -rawthermalimage INPUT.jpg > OUTPUT_thermal.png
```

Run the printed command in a terminal. Confirm that the generated PNG is in the working directory before continuing notebook evaluation.

Typical output names are:

```text
before_thermal.png
after_thermal.png
```

## 6. Prepare masks

The notebook expects:

```text
before_mask.png
after_mask.png
```

Each mask must have dimensions compatible with its corresponding thermal image. The mask determines which pixels are retained for analysis. Document the software, thresholding rules, manual edits, and quality-control procedure used to create the masks.

## 7. Review outputs

The notebook performs the following broad sequence for each image:

1. Imports the visible and raw thermal images.
2. Converts raw thermal pixel values into the selected temperature interval.
3. Applies orientation handling selected by the user.
4. Applies the mask.
5. Divides the retained area into left and right regions.
6. Removes background pixels.
7. Clusters temperature values and computes counts and summaries.
8. Produces heat-map, pie-chart, and histogram outputs.
9. Compares before and after distributions with the notebook's scoring functions.

## 8. Save results

The notebook is primarily interactive. Save the evaluated notebook under a new filename or export outputs explicitly from Mathematica. Do not overwrite the repository copy with data-specific paths, outputs, or identifying information.

## Troubleshooting

### ExifTool is not found

Add ExifTool to the system `PATH`, restart the terminal, and verify with `exiftool -ver`.

### Thermal PNG cannot be imported

Check that the ExifTool command completed successfully, the filename matches the notebook input, and the file is in the selected working directory.

### Mask dimensions do not match

Resize or regenerate the mask using the same pixel dimensions and orientation as the thermal image. Avoid interpolation that changes binary mask boundaries unless it is part of a documented procedure.

### Results appear reversed

Revisit the orientation prompts and verify whether the image should be reversed before defining left and right regions.

### Unexpected results after rerunning cells

Restart the Mathematica kernel and evaluate the notebook from the beginning. The first cell clears the `Global`` context, but a clean kernel provides the strongest reset.
