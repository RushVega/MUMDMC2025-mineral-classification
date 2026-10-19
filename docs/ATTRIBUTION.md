# Academic attribution and licensing

## Research paper

B. G. Amer et al. (2025), *A Photomicrographic Dataset of Rocks for the Accurate Classification of Minerals*, **Scientific Data**. DOI: https://doi.org/10.1038/s41597-025-05879-9

## Reference implementation

The original authors make related preprocessing and evaluation code available at:
https://github.com/MscModelTrain/MUMDMC2025-preprocessing-evaluation

That repository publishes its code under the **MIT License**, including this notice:

> Copyright (c) 2025 MscModelTrain

This project implements and adapts the research methodology and reference preprocessing/evaluation pipeline to the working 583-image dataset, then adds its own cross-validation, parameter search, error analysis, and CNN comparison. The repository preserves the upstream copyright notice in [`../LICENSE`](../LICENSE).

## Dataset and pretrained models

- Dataset source and access details: https://doi.org/10.6084/m9.figshare.29483204.v1
- The shared 583-image subset is downloaded at runtime; image files are not included in this repository.
- EfficientNet-B0 and ConvNeXt-Tiny use weights provided through `torchvision` and may have their own model/data distribution conditions.

The MIT **software** license in this repository does not claim ownership or grant new rights over external dataset images, research paper content, or pretrained weights. Refer to their original publishers for applicable terms.
