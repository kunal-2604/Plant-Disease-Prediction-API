# Plant Disease Prediction API

A FastAPI application for predicting plant diseases from images using pre-trained TensorFlow/Keras models.

## Project Structure

- `plant_api.py` - Main FastAPI application.
- `requirements.txt` - Python dependencies.
- `model/` - Saved model files used for prediction:
  - `cotton_plant_disease_classifier.h5`
  - `maize_disease_detection_new_model.h5`
  - `model_inception.h5`
  - `riceplantdetectionmodel.h5`
  - `wheatDiseaseModel.h5`

## Supported Crops

The API supports predictions for the following crops:
- `cotton`
- `maize`
- `rice`
- `tomato`
- `wheat`

## Installation

1. Create and activate a Python environment (recommended):

```bash
python -m venv venv
venv\Scripts\activate
```

2. Install dependencies:

```bash
pip install -r requirements.txt
```

## Run the API

Start the server with Uvicorn:

```bash
uvicorn plant_api:app --reload
```

The API will be available at `http://127.0.0.1:8000`.

## Endpoints

### GET `/predict`

Predict using query parameters.

**Request:**

```http
GET /predict?crop_name=maize&image_path=cor.jpg
```

**Response:**

```json
{
  "result": "Common rust",
  "confidence": 92.34
}
```

### POST `/predict`

Predict using a JSON payload.

**Request:**

```bash
curl -X POST "http://127.0.0.1:8000/predict" \
  -H "Content-Type: application/json" \
  -d '{"crop_name": "maize", "image_path": "cor.jpg"}'
```

### POST `/predict-file`

Predict using a multipart file upload.

**Request:**

```bash
curl -X POST "http://127.0.0.1:8000/predict-file" \
  -F crop_name=maize \
  -F image=@cor.jpg
```

## Notes

- The API expects local image file paths for the `image_path` parameter in `/predict` endpoints.
- Uploaded images are temporarily saved and removed after prediction.
- Model files are loaded dynamically per request.
- If the crop name is invalid or the image path does not exist, the API returns an error.

## Development

Use the automatic FastAPI docs at:

- `http://127.0.0.1:8000/docs`
- `http://127.0.0.1:8000/redoc`

## Requirements

Dependencies are listed in `requirements.txt` and include:

- `fastapi`
- `uvicorn`
- `tensorflow`
- `numpy`
- `pillow`
- `python-multipart`
