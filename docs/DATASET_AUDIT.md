# Dataset audit and limitations

## Accessible data vs. article description

The paper documents a broad **14,400-image** photomicrographic collection and reports a **2,500-image XPL sample** used for classification (500 images for each of five classes). The working cropped-image archive used in this repository contains only **583 files**, so the work is a **partial reproduction** and cannot reproduce the reported experiment under identical data conditions.

The difference concerns the **particular archive used for this project**, not a verified claim that other files were never published elsewhere.

## Acquisition groups

| Class | Folder counts | Total |
| --- | --- | ---: |
| Biotite | CN/1: 72, CN/2: 75 | 147 |
| Hornblende | CN: 73 | 73 |
| Plagioclase | CN/1: 73, CN/2: 73 | 146 |
| Potassium-Feldspar | CN: 73 | 73 |
| Quartz | CN/1: 72, CN/2: 72 | 144 |
| **Total** | **8 folder groups** | **583** |

Files within each group are associated with rotation angles, typically 5° increments. Preliminary visual inspection suggests that each group *may* represent a physical crystal imaged at different angles, but crystal identity has **not** been verified.

## Filename and metadata ambiguity

The paper documents a filename naming scheme involving thin-section identifier, mineral, lighting condition, crystal number, photo number and rotation angle. In the working ZIP, identical filenames occur across different folders even when image contents differ. Separate metadata workbooks describe **2,500** records and identifiers that cannot always be aligned with the image archive (including disagreements in image dimensions).

Therefore, neither folder names nor filename-derived crystal numbers are reliable, externally validated **independent specimen identifiers** for this subset. We do **not** conclude that mineral class labels are incorrect simply from this naming ambiguity.

## Leakage risk and interpretation

For the baseline stratified 80/20 image-level split, **all 117 test images** have a same-folder acquisition group also represented in the training partition. With KNN `k=1`, **101/117** nearest training neighbors belong to the same folder and **101/101** such matches are correctly labeled. These numbers indicate strong within-folder similarity and should not be confused with evaluation on unseen crystals.

A physical-crystal-disjoint evaluation would require a reliable specimen/group identifier and adequate independent groups per class. This was not available in the working subset; hence we do not quantify how much accuracy is inflated by any group effect. No claim of leakage into model fitting via an explicit test-set label feature is made.

**Scientific conclusion:** image-level generalization on correlated rotation views and generalization to previously unseen physical crystals are different evaluation targets. The reported scores measure the former.
