# Dataset access

The original authors' dataset is published at [Figshare](https://doi.org/10.6084/m9.figshare.29483204.v1). The subset used for this reproduction is also accessible as a [shared ZIP on Google Drive](https://drive.google.com/file/d/1cq-YGOLOZfIrq3T1Nxv_VXJC0aQBR6fh/view).

The notebook **automatically downloads** that ZIP using `gdown` and extracts it in Google Colab:

```text
/content/MUMDMC2025_DataSet/Cropped_Images/
    Biotite/CN/1/ and CN/2/
    Hornblende/CN/
    Plagioclase/CN/1/ and CN/2/
    Potassium_Feldspar/CN/
    Quartz/CN/1/ and CN/2/
```

There are **583 cropped images** in this archive. The article and separate metadata workbooks describe a larger set of **2,500** image records. Do not assume that the metadata workbooks map one-to-one to this ZIP: some filenames repeat across folders and image dimensions differ. Folder series are useful acquisition groups but **not verified unique physical-crystal IDs**.

No raw image dataset is committed in this repository. This avoids duplicating large datasets or making unsupported redistribution claims; consult the original dataset's distribution terms for reuse.
