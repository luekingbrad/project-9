# LSTM SMS Spam Detection

A deep learning natural language processing project that uses an **LSTM neural network** to classify SMS messages as either **spam** or **ham (not spam)**.

The project demonstrates an end-to-end text classification workflow, including text cleaning, tokenization, sequence padding, supervised learning, and model evaluation.

## Project Overview

The objective of this project is to build a deep learning model capable of distinguishing spam messages from legitimate messages.

The overall workflow is:

```text
SMS Dataset
    │
    ▼
Text Cleaning
    │
    ▼
Label Encoding
    │
    ▼
Train / Validation / Test Split
    │
    ▼
Tokenization
    │
    ▼
Sequence Padding
    │
    ▼
LSTM Neural Network
    │
    ▼
Model Training
    │
    ▼
Test Evaluation
    │
    ▼
Confusion Matrix / Classification Report
```

## Dataset

The project uses the `spam.csv` dataset.

The original data contains two relevant fields:

* `v1` — message classification label
* `v2` — SMS message text

The labels are converted into binary values:

```text
ham  → 0
spam → 1
```

The dataset is loaded locally and is **not included in this repository**.

## Text Preprocessing

Before the messages are passed to the neural network, the text is cleaned and normalized.

The preprocessing function:

* Converts messages to lowercase
* Removes URLs
* Removes non-alphabetic characters
* Normalizes whitespace

This produces a cleaned text field used as the model input.

## Dataset Splitting

The dataset is intended to be divided into three groups:

* Training data
* Validation data
* Testing data

The original notebook produced the following dataset sizes:

```text
Training:   3,900
Validation:   836
Testing:     836
```

The split uses `train_test_split` with stratification so the class distribution is maintained across the datasets.

### Implementation Correction

The original notebook contained a variable-assignment error during the second split:

```python
X_val, X_test, y_train, y_test = train_test_split(...)
```

The validation labels should instead be assigned to `y_val`.

The cleaned portfolio notebook corrects this to:

```python
X_val, X_test, y_val, y_test = train_test_split(...)
```

This correction is necessary because the model-training stage expects `y_val` for validation.

## Tokenization

The cleaned text is converted into numerical sequences using the TensorFlow/Keras `Tokenizer`.

The project uses:

```text
Vocabulary size: 10,000
Maximum sequence length: 100
```

The tokenizer is fitted using the training data and then applied to the training, validation, and test datasets.

## Sequence Padding

Because SMS messages have different lengths, the resulting sequences are padded to a consistent length of 100 tokens.

Padding is performed after the existing sequence values:

```python
pad_sequences(
    sequences,
    maxlen=100,
    padding="post"
)
```

This creates a consistent numerical representation that can be passed into the LSTM model.

## LSTM Model

The project uses a sequential deep learning architecture containing:

* Embedding layer
* LSTM layer with 64 units
* Dropout layer
* Dense layer with 32 neurons
* Second Dropout layer
* Single-neuron sigmoid output layer

The intended model architecture is:

```text
Input Text
    │
    ▼
Embedding
    │
    ▼
LSTM (64)
    │
    ▼
Dropout (0.5)
    │
    ▼
Dense (32, ReLU)
    │
    ▼
Dropout (0.5)
    │
    ▼
Dense (1, Sigmoid)
    │
    ▼
Spam / Ham Classification
```

The model uses:

* **Binary cross-entropy** loss
* **Adam** optimizer
* **Accuracy** as the evaluation metric

## Model Training

The intended training configuration is:

```text
Epochs:     10
Batch size: 32
Optimizer:  Adam
Loss:       Binary Cross-Entropy
```

Validation data is supplied during training so the model can be evaluated against data that is separate from the training set.

The original execution, however, did **not successfully reach model training** because the LSTM model construction generated a TensorFlow/NumPy compatibility error.

The subsequent training, evaluation, and prediction cells therefore produced `NameError` messages because the `model` object was never successfully created.

The cleaned notebook retains the intended working implementation while removing the lengthy error traces from the portfolio presentation.

## Evaluation

The completed workflow is designed to evaluate the model using:

### Test Accuracy

The model is evaluated against the held-out test dataset.

### Confusion Matrix

A confusion matrix is used to examine:

* True negatives
* False positives
* False negatives
* True positives

### Classification Report

The classification report is intended to provide:

* Precision
* Recall
* F1-score
* Support

The original project execution did not generate valid evaluation metrics because the model failed to initialize in the recorded environment. Therefore, no fabricated accuracy or classification results are presented here.

## Technologies Used

* Python
* Jupyter Notebook
* TensorFlow
* Keras
* LSTM Neural Networks
* NumPy
* Pandas
* scikit-learn
* Natural Language Processing
* Text Tokenization
* Sequence Padding
* Supervised Learning

## Project Structure

```text
LSTM-SMS-Spam-Detection/
│
├── .gitignore
├── README.md
├── requirements.txt
├── spam_detection_lstm.ipynb
│
└── screenshots/
```

### File Descriptions

**`spam_detection_lstm.ipynb`**

The primary Jupyter Notebook containing the complete SMS preprocessing, tokenization, sequence preparation, LSTM architecture, training workflow, and evaluation process.

**`requirements.txt`**

Contains the Python packages required to reproduce the project.

**`.gitignore`**

Prevents the local dataset, Python cache files, virtual environments, Jupyter checkpoints, and other development files from being committed.

**`screenshots/`**

Contains selected screenshots documenting the major stages of the project.

## Dataset Considerations

The original `spam.csv` dataset is intentionally **not included in this repository**.

The notebook expects the dataset to be available locally:

```text
spam.csv
```

This keeps the GitHub repository focused on the machine learning workflow while preventing unnecessary redistribution of the dataset.

## Installation

### 1. Clone the repository

```bash
git clone <repository-url>
cd LSTM-SMS-Spam-Detection
```

### 2. Create a virtual environment

```bash
python3 -m venv .venv
```

Activate it on macOS/Linux:

```bash
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Add the dataset

Place the required dataset in the project directory:

```text
spam.csv
```

### 5. Launch the notebook

```bash
jupyter notebook
```

Then open:

```text
spam_detection_lstm.ipynb
```

## Skills Demonstrated

This project demonstrates experience with:

* Natural language processing
* Deep learning
* LSTM neural networks
* TensorFlow/Keras
* Text preprocessing
* Tokenization
* Sequence padding
* Supervised classification
* Train/validation/test dataset design
* Binary classification
* Confusion matrix analysis
* Classification metrics
* Cybersecurity-related spam detection

## Future Development

Potential improvements include:

* Resolve the TensorFlow/NumPy compatibility issue in the original environment
* Successfully train and evaluate the model
* Record test accuracy and classification metrics
* Plot training and validation accuracy
* Plot training and validation loss
* Compare LSTM performance with traditional machine-learning classifiers
* Experiment with different sequence lengths and vocabulary sizes
* Address class imbalance using additional evaluation techniques
* Test the model against previously unseen spam campaigns
* Extend the system toward phishing and malicious-message detection

## Author

**Bradley Lueking**

Cybersecurity | AI | Machine Learning | Deep Learning | Security Operations | GRC
