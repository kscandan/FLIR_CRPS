# Infrared Imaging in Complex Regional Pain Syndrome

An interactive Wolfram Mathematica notebook supporting research into the use of FLIR infrared imaging in the context of **Complex Regional Pain Syndrome (CRPS) treatment**.

The notebook extracts raw thermal data from paired FLIR JPEG files, maps raw values to user-supplied temperature ranges, applies manually prepared masks, separates left and right regions, clusters temperature values, visualizes distributions, and computes before-versus-after comparison scores.

## Authors and contributors

- **K. Selcuk Candan** — Arizona State University  
  ORCID: [0000-0003-4977-6646](https://orcid.org/0000-0003-4977-6646)  
  Website: [kscandan.site](https://kscandan.site)
- **Burcu Candan**
- **Semih Gungor**

Contact: [candan@asu.edu](mailto:candan@asu.edu)

## Repository contents

```text
FLIR_CRPS/
├── notebooks/
│   └── flir_crps.nb
├── docs/
│   ├── METHOD.md
│   └── USAGE.md
├── data/
│   └── README.md
├── .github/
│   ├── ISSUE_TEMPLATE/
│   └── pull_request_template.md
├── .gitignore
├── CITATION.cff
├── CONTRIBUTING.md
├── LICENSE
├── README.md
├── RELEASE_CHECKLIST.md
└── SECURITY.md
```

## Requirements

- Wolfram Mathematica 12.0 or later. The notebook was created with Mathematica 12.0.
- [ExifTool](https://exiftool.org/) available from the command line.
- Two FLIR radiometric JPEG images: one before and one after an intervention.
- Corresponding manually prepared PNG masks.

## Quick start

1. Install Mathematica and ExifTool.
2. Clone this repository.
3. Open `notebooks/flir_crps.nb` in Mathematica.
4. Evaluate the notebook from top to bottom.
5. Select the working directory when prompted.
6. Follow the prompts for the before and after JPEG files, image ratios, and temperature limits.
7. Run each ExifTool command printed by the notebook to generate the raw thermal PNG files.
8. Supply masks named `before_mask.png` and `after_mask.png` in the working directory.
9. Continue evaluation to generate regional statistics, charts, and comparison scores.

Detailed instructions are in [`docs/USAGE.md`](docs/USAGE.md). A high-level explanation of the calculations is in [`docs/METHOD.md`](docs/METHOD.md).

## Expected working files

```text
before.jpg              # Before-intervention FLIR JPEG
before_thermal.png      # Raw thermal image extracted with ExifTool
before_mask.png         # User-prepared mask
after.jpg               # After-intervention FLIR JPEG
after_thermal.png       # Raw thermal image extracted with ExifTool
after_mask.png          # User-prepared mask
```

The actual JPEG names are entered interactively. Mask dimensions must match the associated thermal images.

## Important notes

- The workflow is interactive and pauses at `InputString` prompts and manual ExifTool steps.
- Temperature calibration depends on the minimum and maximum values entered by the user.
- Masks are not generated automatically.
- The notebook contains the original executable code with additional descriptive documentation cells. Its executable expressions were not intentionally changed while preparing the commented version.
- No patient, participant, or proprietary thermal images are included. Review all data for privacy, consent, institutional requirements, and applicable law before use or publication.

## Reproducibility

Record the Mathematica and ExifTool versions, camera model and acquisition settings, entered temperature bounds, orientation choices, split ratios, mask-generation procedure, and exact Git commit used for each analysis.

## Citation

The repository contains machine-readable citation metadata in [`CITATION.cff`](CITATION.cff). GitHub can display this through its **Cite this repository** feature.

Suggested AMA-style software citation:

> Candan KS, Candan B, Gungor S. *Infrared Imaging in Complex Regional Pain Syndrome*. Version 1.0.0. Published 2026. https://github.com/kscandan/FLIR_CRPS

Add the access date required by your journal or institution. Replace the repository URL with a version-specific DOI when one becomes available.

## License

Copyright 2023 K. Selcuk Candan.

Licensed under the [Apache License, Version 2.0](LICENSE). You may use, reproduce, and distribute the software subject to the license terms. No separate `NOTICE` file is included.

## Disclaimer

This software is provided for research and analytical use. It has not been validated as a medical device and must not be used as the sole basis for diagnosis, treatment, or other clinical decisions.
