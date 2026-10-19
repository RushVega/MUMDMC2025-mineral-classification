# Methods and experimental design

## Reproduction target

Reproduce the paper's Decision Tree and KNN method using five mineral classes (Biotite, Hornblende, Plagioclase, Potassium-Feldspar, Quartz) on the available **583-image** cropped subset.

## Baseline

1. Read images recursively below each mineral class; classes are folder labels.
2. Normalize RGB image pixels and reshape each image into a flattened feature vector.
3. Compare two common input sizes: cropped-image branch standardized to **224×224** for this subset and a resized branch at **150×150**.
4. Create a stratified **80/20 split** with `random_state=42` → **466 train / 117 test**.
5. Fit a `DecisionTreeClassifier(random_state=42)` and default `KNeighborsClassifier()` (`k=5`).
6. Report accuracy, weighted precision/recall/F1, confusion matrices and additional baseline diagnostics.

**Note:** the phrase “original” in the code names an *input branch*, not the article's camera-native original resolution.

## Experiment 2: cross-validation

Perform `StratifiedKFold(n_splits=5, shuffle=True, random_state=42)` **only on the 466 training images**, using 150×150 inputs. Record Accuracy and Macro-F1 for each fold and report mean and standard deviation. The 117-image holdout is not a CV fold. Stratification maintains approximate class proportions but does not remove within-group correlation.

## Experiment 3: tuning

Use `GridSearchCV` with the same five stratified folds on the **training images only**:

- KNN: `n_neighbors ∈ {1, 3, 5, 7, 9}`.
- Decision Tree: `max_depth ∈ {5, 10, 15, None}`.

Choose the highest average **Macro-F1**; `refit='Macro_F1'` retrains the selected estimator on all 466 training images. Evaluate on the existing 117-image holdout. The holdout was already inspected during the baseline, so these are *not* claims of an entirely untouched independent benchmark after exploratory analysis.

## Experiment 4: error analysis

Display confusion matrices, sample KNN misclassifications, and the one-nearest training neighbor for each test image. Determine whether test and neighbor files have the same parent acquisition folder. **Same-folder correctness is expected for 1-NN given folder-level class labels**; it quantifies within-group proximity rather than proving generalization.

## Experiment 5: CNN transfer learning

- Architectures: ImageNet-pretrained **EfficientNet-B0** and **ConvNeXt-Tiny**.
- Data: same stratified **117-image test set**; remaining 466 images split into **396 training / 70 validation** (`random_state=42`).
- Inputs: **224×224** RGB, ImageNet normalization; data augmentation only for training.
- Head-only stage: **10 epochs**, Adam learning rate `1e-3`; backbone frozen.
- Fine-tuning: up to **15 epochs**, Adam learning rate `1e-5`; last feature stage and head trainable; early stopping patience 5 on validation loss.
- Batch size 32; report Accuracy, weighted Precision/Recall/F1, Macro-F1 and multiclass ROC-AUC.
- Model selection uses validation data; weights are evaluated on the image-level test set. Pretrained ImageNet representations provide a major starting advantage over DT/KNN trained on flattened pixels.

Runtime and final CNN values can differ depending on hardware, library versions and stochastic GPU operations.
