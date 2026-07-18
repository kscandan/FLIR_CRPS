# Method Overview

This document summarizes the notebook's computational workflow. The notebook itself remains the authoritative implementation.

## Input and calibration

The workflow begins with paired FLIR JPEG images representing conditions before and after an intervention. Raw thermal images are extracted from the JPEG metadata with ExifTool. The raw pixel range is then mapped to minimum and maximum temperatures entered by the user.

Because the calibration bounds are user supplied, they must be recorded and justified for every analysis.

## Masking and regional separation

A manually prepared mask removes pixels outside the region of interest. The remaining image is divided into left and right regions using an interactively supplied ratio. Orientation choices affect which pixels are assigned to each side and should be verified visually.

## Distribution summaries

The notebook flattens retained regional pixel values, filters background values, clusters temperature observations, and summarizes cluster frequencies and representative values. It then produces graphical summaries including pie charts and histograms.

## Directional probability

`prob[hx, hy, dir]` computes a weighted cumulative comparison between two equal-length histogram vectors:

- `dir == 1` uses an upper-tail cumulative mass.
- Other values use a lower-tail cumulative mass.

## Symmetric score

`score[hx, hy]` averages two complementary directional comparisons:

```text
0.5 * (prob[hx, hy, 0] + prob[hy, hx, 1])
```

This combines both input orderings and both cumulative directions used by the notebook.

## Relative improvement

`impr[ho, hn]` normalizes the score of a new distribution against the baseline's self-score:

```text
score[ho, hn] / score[ho, ho] - 1.0
```

Positive values indicate an increase relative to the selected baseline under this scoring definition. Interpretation depends on the construction and ordering of the histogram vectors.

## Validation considerations

Before relying on results, assess:

- Repeatability across acquisitions and operators.
- Sensitivity to temperature bounds.
- Sensitivity to mask boundaries and split ratios.
- Camera calibration and environmental conditions.
- Stability of clustering choices.
- Agreement with an independently validated reference method.

The notebook has not been represented here as a clinically validated diagnostic method.
