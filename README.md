# Logo Detection

Logo and brand detection with Ultralytics YOLO11. The folder contains a trained checkpoint (`last (1).pt`), a dataset configuration file (`logodek.yaml`), a notebook for running inference, sample images and test videos. The configuration file lists about 3000 brand names as classes.

## Features

- Inference on single images or videos using Ultralytics YOLO
- Saves annotated output images (`save=True` in the notebook)
- Training evaluation plots (confusion matrices) included

## Project structure

- `last (1).pt`: trained checkpoint (last epoch) for logo detection.
- `yolo11n.pt`: pretrained YOLO11 nano base weights. The notebook loads this file, not `last (1).pt`.
- `logodek.yaml`: dataset configuration. The `train` and `val` paths are placeholders and the `nc` value is marked in the file as needing replacement, so it is a template.
- `Testing Model.ipynb`: notebook that loads a model and runs inference on one image.
- `confusion_matrix (2).png`, `confusion_matrix_normalized (2).png`: evaluation plots from training.
- `photo.jpg`, `london_*.jpg`, `miami_*.jpg`, `train_batch0 (1).jpg`: sample images.
- `test1.mp4`, `test2.mp4`: sample videos.

## Requirements

Imports used: `ultralytics`, `cv2`.

```
pip install ultralytics opencv-python
```

## Installation

```
git clone https://github.com/Yaldram69/Logo-Detection.git
cd Logo-Detection
pip install ultralytics opencv-python
```

## Usage

Notebook: open `Testing Model.ipynb`, point the model path to `last (1).pt` and the image path to a file such as `photo.jpg`, then run the cells. Annotated results are written by Ultralytics to a `runs/` folder.

Equivalent command line with the Ultralytics CLI:

```
yolo predict model="last (1).pt" source="photo.jpg"
yolo predict model="last (1).pt" source="test1.mp4"
```

Input is an image or video path. The notebook's model and image paths are hardcoded to the author's machine and must be edited.

## Notes

- Weights and images are included in the repository; the training dataset is not.
- The class names come from the checkpoint. To list them, run `YOLO("last (1).pt").names`. This was not verified against the YAML file.
- In the notebook's last cell, `cv2.imshow(results, "results")` has its arguments reversed and will fail. Use `results[0].show()` or save and open the output file instead.
- `cv2` is imported after it is first needed in the notebook; run the import cell first.
- Accuracy on the 3000-class set is not reported in the repository beyond the two confusion matrix images.
