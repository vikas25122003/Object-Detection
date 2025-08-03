# YOLOv8 for Household Object & Cleanliness Detection

This project uses a YOLOv8 model to detect 77 different classes of household items, appliances, and cleanliness states. The model is trained on a custom-merged dataset to identify objects like kitchenware and furniture, as well as assess the cleanliness of surfaces such as floors, toilets, and pipes.

-----

## 🚀 Key Features

  * **Comprehensive Detection**: Identifies **77 distinct classes** of household and sanitary objects.
  * **Cleanliness Assessment**: Capable of detecting states like `uncleaned floor/tiles`, `cleaned floor/tiles`, `stains`, and `rusty pipes`.
  * **High Performance**: The model achieves a **mAP50-95 of 0.635** on the test set.
  * **Pre-trained Model**: The final trained weights are available for direct download and use.

-----

## 🔧 Environment & Dependencies

The model was trained and tested in the following environment:

  * **GPU**: NVIDIA Tesla T4
  * **Python**: `3.10.12`
  * **Core Libraries**:
      * `ultralytics==8.3.173`
      * `torch==2.5.1+cu121`
      * `opencv-python`
      * `matplotlib`

### Setup

1.  **Clone the Repository**:

    ```bash
    git clone <your-repository-url>
    cd <your-project-directory>
    ```

2.  **Create a Virtual Environment** (Recommended):

    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate
    ```

3.  **Install Dependencies**:

    ```bash
    pip install ultralytics torch torchvision
    ```

-----

## ⚡️ How to Run

You can either use the pre-trained model for immediate inference or train the model from scratch.

### 1\. Download Pre-trained Model

The best-performing model weights from 150 epochs of training are available on Google Drive.

  * **[Download best.pt from Google Drive](https://drive.google.com/file/d/1FCVPKhi3OC8lJzDBBgXNdTd6MV2kysEL/view)**

Save the downloaded `best.pt` file in your project's root directory.

### 2\. Prepare Data for Prediction

Place the images you want to test in a folder (e.g., `./demo_images`).

### 3\. Run Prediction

Use the following command to run inference on your images. The results, with bounding boxes drawn, will be saved in the `./runs/detect/predict` directory.

```bash
yolo task=detect mode=predict model=best.pt conf=0.25 source=./demo_images save=True
```

### 4\. (Optional) Train the Model from Scratch

If you wish to retrain the model, follow these steps:

1.  **Prepare the Dataset**: Ensure your dataset is structured as expected by YOLOv8 and is available at the paths specified in the YAML file. The training script used this Kaggle input path: `/kaggle/input/final-ds-reduced-classes/`.

2.  **Create `data.yaml`**: Create a file named `data.yaml` with the correct paths to your `train`, `val`, and `test` sets and the class names.

    ```yaml
    train: /path/to/your/dataset/train/images
    val: /path/to/your/dataset/valid/images
    test: /path/to/your/dataset/test/images

    names:
      0: Air conditioner
      1: Air purifier
      # ... (add all 77 class names here) ...
      75: uncleaned floor/tiles
      76: uncleaned toilet
    ```

3.  **Start Training**: Run the training command. This will train a `yolov8s` model for 150 epochs with an early stopping patience of 35 rounds.

    ```bash
    yolo task=detect mode=train model=yolov8s.pt data=data.yaml epochs=150 imgsz=640 plots=true patience=35
    ```

-----

## 📊 Model Performance

The model was trained for **150 epochs**, and the performance metrics for the best model are as follows:

| Dataset     | mAP50-95 (IoU=0.5:0.95) | mAP50 (IoU=0.5) | Precision | Recall |
| :---------- | :---------------------- | :-------------- | :-------- | :----- |
| **Validation** | 0.603                   | 0.806           | 0.832     | 0.769  |
| **Test** | **0.635** | **0.804** | 0.803     | 0.780  |

### Visual Results

Key visualizations from the training process are saved in the `runs/detect/train/` directory.

**Confusion Matrix (Normalized):**
<img width="946" height="744" alt="image" src="https://github.com/user-attachments/assets/c6e6d1c7-4171-41e3-8c86-75557297e780" />


**Metrics (Precision-Recall Curve, etc.):**
<img width="1188" height="586" alt="image" src="https://github.com/user-attachments/assets/af3ec513-8688-4ea3-a3b2-57b54cd5ad7b" />
<img width="1160" height="794" alt="image" src="https://github.com/user-attachments/assets/84fab9ef-9c39-42c9-a17e-b1bbc4cd096b" />
<img width="1206" height="771" alt="image" src="https://github.com/user-attachments/assets/2ec662ab-a8c2-4c8f-ab61-dc091d36cc72" />
<img width="1002" height="775" alt="image" src="https://github.com/user-attachments/assets/c9a670e4-7a5c-4373-b80a-f907850a8032" />

Note : The Readme is for New Reduced DS Notebook . 
Full notebook at : https://www.kaggle.com/code/jaivigneshavikasrm/new-ds-reduced-classes-obj-detection
