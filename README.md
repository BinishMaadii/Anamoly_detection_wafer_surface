# Label-Free Defect Detection in Semiconductor Microscopy

A **PatchCore-style anomaly detection pipeline** for identifying defects in semiconductor microscopy images without requiring defect labels during model training. It uses microscopy-pretrained ResNet-50 features, a normal-image feature memory bank, and nearest-neighbor distances to generate image-level anomaly scores and spatial anomaly maps.

## Method

1. **Feature extraction:** Extracts and combines intermediate ResNet-50 feature maps from a model pretrained on ImageNet and fine-tuned on MicroNet microscopy images.
2. **Memory bank:** Builds a reference bank of 9,216 representative normal-image patches using a 1% coreset.
3. **Anomaly scoring:** Measures each patch's distance to its nearest reference patch and generates smoothed anomaly maps.
4. **Thresholding:** Sets the detection threshold at the 99th percentile of scores from 100 normal calibration images.
5. **Evaluation and grouping:** Evaluates image-level detection, pixel-level localization, and defect-size performance; clusters flagged images for visual inspection.

## Results

Evaluated on 388 images: 272 normal and 116 defective.

| Metric | Result |
|---|---:|
| Image AUROC | 0.9669 |
| Image average precision | 0.9386 |
| Defect recall | 84.5% (98/116) |
| Precision | 92.5% |
| False alarms | 8/272 normal images |
| Pixel AUROC | 0.9907 |
| Pixel average precision | 0.3049 |
| Small-defect recall | 69.0% |
| Large-defect recall | 100% |

Pixel metrics are approximate, calculated on every fourth pixel. Small and large defects are defined by the median ground-truth mask area.

## Requirements

Python, PyTorch, torchvision, NumPy, pandas, Pillow, scikit-learn, SciPy, and Matplotlib. A CUDA-enabled GPU is recommended. Internet access is required to download the pretrained weights unless they are cached.

## Run

Run the script in a Kaggle notebook with GPU enabled and the MIIC dataset and MicroNet weights accessible. Configure the dataset paths and settings at the beginning of the script. Results, evaluation tables, anomaly visualizations, and cluster galleries are saved to:

`/kaggle/working/results`

## Limitations

The reported run uses 900 normal images for training and 100 for calibration, sampled from the normal test-image directory; it does not use the separate `Anomaly_train` folder. Pixel AUROC alone does not establish segmentation quality, and the results should be validated on an independent dataset before deployment.# Label-Free Defect Detection in Semiconductor Microscopy

A **PatchCore-style anomaly detection pipeline** for identifying defects in semiconductor microscopy images without requiring defect labels during model training. It uses microscopy-pretrained ResNet-50 features, a normal-image feature memory bank, and nearest-neighbor distances to generate image-level anomaly scores and spatial anomaly maps.

## Method

1. **Feature extraction:** Extracts and combines intermediate ResNet-50 feature maps from a model pretrained on ImageNet and fine-tuned on MicroNet microscopy images.
2. **Memory bank:** Builds a reference bank of 9,216 representative normal-image patches using a 1% coreset.
3. **Anomaly scoring:** Measures each patch's distance to its nearest reference patch and generates smoothed anomaly maps.
4. **Thresholding:** Sets the detection threshold at the 99th percentile of scores from 100 normal calibration images.
5. **Evaluation and grouping:** Evaluates image-level detection, pixel-level localization, and defect-size performance; clusters flagged images for visual inspection.

## Results

Evaluated on 388 images: 272 normal and 116 defective.

| Metric | Result |
|---|---:|
| Image AUROC | 0.9669 |
| Image average precision | 0.9386 |
| Defect recall | 84.5% (98/116) |
| Precision | 92.5% |
| False alarms | 8/272 normal images |
| Pixel AUROC | 0.9907 |
| Pixel average precision | 0.3049 |
| Small-defect recall | 69.0% |
| Large-defect recall | 100% |

Pixel metrics are approximate, calculated on every fourth pixel. Small and large defects are defined by the median ground-truth mask area.

## Requirements

Python, PyTorch, torchvision, NumPy, pandas, Pillow, scikit-learn, SciPy, and Matplotlib. A CUDA-enabled GPU is recommended. Internet access is required to download the pretrained weights unless they are cached.

## Run

Run the script in a Kaggle notebook with GPU enabled and the MIIC dataset and MicroNet weights accessible. Configure the dataset paths and settings at the beginning of the script. Results, evaluation tables, anomaly visualizations, and cluster galleries are saved to:

`/kaggle/working/results`

## Limitations

The reported run uses 900 normal images for training and 100 for calibration, sampled from the normal test-image directory; it does not use the separate `Anomaly_train` folder. Pixel AUROC alone does not establish segmentation quality, and the results should be validated on an independent dataset before deployment.
