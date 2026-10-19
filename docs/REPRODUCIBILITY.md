# Reproducibility guide

## Recommended environment

**Google Colab** (Python 3.11/3.12 as available; GPU preferred, CPU possible). The notebook uses Colab-specific `/content/` absolute paths and `!pip` notebook syntax. It was authored and run for Colab and is **not guaranteed to run unchanged on Windows or local Jupyter**.

Use the provided `requirements.txt` as a **reference pinned environment**, not as a guarantee that all future Colab images will install an identical stack. The notebook itself installs `gdown`. In existing Colab GPU environments, avoid overriding working torch/torchvision builds unless needed and verified compatible with the runtime.

## Run steps

1. Download/open [`../notebooks/MUMDMC2025.ipynb`](../notebooks/MUMDMC2025.ipynb) in Colab.
2. Select GPU runtime if available.
3. Check that internet access is enabled (for `gdown` and pretrained ImageNet weights).
4. **Run all** cells in order and allow the public dataset to download and extract to `/content/MUMDMC2025_DataSet`.
5. Check the dataset audit prints **583** images and class counts **147 / 73 / 146 / 73 / 144**.
6. Review experiment outputs in the notebook. New CSV and PNG files are generated in `/content/outputs/`; trained CNN model state dictionaries in `/content/models/`.
7. For submission, record runtime type, available accelerator and installed library versions printed in the setup section. Do not treat previously saved cell outputs as evidence of a fresh successful run.

## Split and RNG settings

| Component | Configuration |
| --- | --- |
| Classical train/test split | Stratified 80/20, `random_state=42` |
| CV | Stratified 5 folds, shuffled, `random_state=42`, training partition only |
| KNN tuning | `n_neighbors=[1,3,5,7,9]`; choose by CV Macro-F1 |
| DT tuning | `max_depth=[5,10,15,None]`; choose by CV Macro-F1 |
| CNN train/validation/test | 396 / 70 / 117, stratified, `random_state=42` |
| CNN seeds | Python `random`, NumPy, PyTorch seed 42, cuDNN deterministic settings |

PyTorch operations and pretrained-weight downloads may vary by runtime and version; seeds reduce but cannot guarantee exact hardware-independent numerical identity.

## What is and is not included

Included: final notebook with saved output snapshots, pinned dependency reference file, selected charts, CSV summaries transcribed from saved Colab results, presentation and explanatory documentation.

Excluded: raw dataset, extracted images, model weights, generated full-size figures, and hidden/private API credentials. The notebook downloads its required dataset; pretrained model weights are downloaded by `torchvision` if not already cached.

## Continuous integration

The repository includes `.github/workflows/notebook-check.yml`, which validates `.ipynb` structure and checks the syntax of regular Python code cells. It intentionally **does not run dataset download, model training or GPU inference**. Therefore a green GitHub Actions status is **not** a full reproducibility certification.

## Troubleshooting

- **Google Drive rate/permission issue:** confirm the shared data ZIP is still accessible or download it separately from the dataset location. Do not change the class-folder structure.
- **No GPU:** CNN stages may take substantially longer; the notebook chooses the available device.
- **Pretrained weight download failure:** internet access is required for EfficientNet-B0 and ConvNeXt-Tiny on first run.
- **Local execution error mentioning `/content/`:** use Colab as documented; local use requires systematically adapting paths and possibly CNN DataLoader worker settings.
- **Different accuracy after rerun:** check image count, exact file ordering, split settings, library versions and execution order before interpreting differences as a methodological improvement.
