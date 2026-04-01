# Plant Disease Detection System

A deep learning web application that detects diseases in plant leaves from uploaded images and provides causes, remedies, and treatment recommendations.

## Overview

This system classifies leaf images into 38 categories covering 14 plant species — identifying both healthy plants and common diseases. For each detected disease, it provides the cause, suggested remedies, and both organic and inorganic treatment options.

## Supported Plants & Diseases

| Plant | Conditions Detected |
|-------|-------------------|
| Apple | Apple Scab, Black Rot, Cedar Apple Rust, Healthy |
| Blueberry | Healthy |
| Cherry | Powdery Mildew, Healthy |
| Corn (Maize) | Cercospora Leaf Spot, Common Rust, Northern Leaf Blight, Healthy |
| Grape | Black Rot, Esca (Black Measles), Leaf Blight, Healthy |
| Orange | Huanglongbing (Citrus Greening) |
| Peach | Bacterial Spot, Healthy |
| Bell Pepper | Bacterial Spot, Healthy |
| Potato | Early Blight, Late Blight, Healthy |
| Raspberry | Healthy |
| Soybean | Healthy |
| Squash | Powdery Mildew |
| Strawberry | Leaf Scorch, Healthy |
| Tomato | Bacterial Spot, Early Blight, Late Blight, Leaf Mold, Septoria Leaf Spot, Spider Mites, Target Spot, Mosaic Virus, Yellow Leaf Curl Virus, Healthy |

## Project Structure

```
├── BACKEND/
│   ├── CODE.ipynb          # Model training notebook (CNN & MobileNet)
│   ├── app.py              # Flask web application
│   ├── db.sql              # MySQL database schema
│   ├── dataset link.txt    # Link to the PlantVillage dataset
│   ├── images/             # Uploaded images (runtime)
│   ├── static/             # CSS, JS, fonts, images
│   └── templates/          # HTML templates
├── FRONTEND/               # Frontend assets and app
├── ABSTARCT/
│   └── Abstract.docx
├── DOCUMNET/
│   └── FINAL DOC.docx
├── PPT/                    # Presentation slides
└── VIDEO FILE/             # Demo video
```

## Models

Two deep learning models were trained and compared:

- **CNN** — Custom convolutional network (67M parameters), saved as `CNN.h5`
- **MobileNet** — Transfer learning on MobileNet pretrained on ImageNet (4.9M parameters), saved as `mobilenet.h5` *(used in production)*

Both models were trained on 54,305 images across 38 classes using the [PlantVillage dataset](https://www.kaggle.com/datasets/abdallahalidev/plantvillage-dataset).

**Training configuration:**
- Input size: 256×256 RGB
- Optimizer: Adam
- Loss: Categorical Cross-Entropy
- Epochs: 50
- Batch size: 20

## Tech Stack

- **Backend:** Python, Flask
- **ML/DL:** TensorFlow / Keras
- **Database:** MySQL (MariaDB)
- **Frontend:** HTML, CSS, JavaScript

## Setup & Installation

### Prerequisites

- Python 3.8+
- MySQL / MariaDB
- GPU recommended for model training (not required for inference)

### 1. Install Python dependencies

```bash
pip install flask mysql-connector-python tensorflow pillow numpy pandas matplotlib
```

### 2. Set up the database

Import the schema into MySQL:

```bash
mysql -u root -p < BACKEND/db.sql
```

This creates the `leaf_data` database with a `users` table.

### 3. Add the trained model

Place the trained `mobilenet.h5` model file at:

```
BACKEND/models/mobilenet.h5
```

To train the model from scratch, run all cells in `BACKEND/CODE.ipynb`.

### 4. Run the application

```bash
cd BACKEND
python app.py
```

The app will be available at `http://localhost:5000`.

## Usage

1. **Register** — Create an account at `/contact`
2. **Sign in** — Log in at `/signin`
3. **Upload** — Go to the upload page and submit a leaf image (JPG, PNG, JPEG, JFIF)
4. **Results** — View the predicted disease along with its causes, organic remedies, and inorganic treatment options

## Dataset

The PlantVillage dataset was used for training:
- 54,305 images across 38 plant/disease classes
- Source: https://www.kaggle.com/datasets/abdallahalidev/plantvillage-dataset
