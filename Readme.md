 # Predicting Bioactivity, Solubility, and Molecular Weight of Compounds

## Problem Statement

The goal of this project is to predict the **bioactivity**, **solubility**, and **molecular weight** of compounds with respect to a biological target of any disease. The project compares the performance of **deep learning techniques** (LSTM) with **traditional machine learning techniques** (Random Forest Regressor).

---

## Data Collection

- Data was collected from the **ChEMBL** website.
- A CSV file was downloaded containing information about compounds, including:
  - **SMILE strings** (representing molecular structures)
  - **Solubility**
  - **Bioactivity**
  - **Molecular weight**

---

## Data Cleaning

1. **Initial Cleaning**:
   - Removed all rows with `NaN` values in the following columns:
     - `Smiles`
     - `Bioactivity (or Standard Value)`
     - `Molecular Weight`
     - `AlogP` (measure of solubility)
     - `Standard Units` (measurement unit for bioactivity)

2. **Unit Standardization**:
   - Bioactivity data had units such as:
     - `nM`, `%`, `hr`, `uM`, `ug.mL-1`, `10'-4No_unit`, `degrees C`, `10'-3/s`, `10'5/M/s`, `% ID/g`, `μM`, `equiv`.
   - Retained rows with units `nM`, `uM`, or `μM` only.
   - Converted `uM` and `μM` values to `nM` for consistency.

---

## Data Visualization

- Plotted data distributions for:
  - **Bioactivity**
  - **Solubility**
  - **Molecular Weight**

---

## Data Preprocessing

1. **Input Features**:
   - Used **SMILE strings** as input features.
   - Converted SMILE strings into **one-hot encoded vectors** for model input.

2. **Output Values**:
   - Used **solubility**, **bioactivity**, and **molecular weight** as output variables.
   - Normalized the output variables using **MinMax Scaler**.

3. **Dataset Splitting**:
   - Created PyTorch `DataLoader` objects for **train**, **test**, and **validation** datasets.

---

## Model Architecture (Deep Learning)

- Built an **LSTM-based model** using PyTorch with the following components:
  1. **LSTM Layer**: Processes the SMILE string sequences.
  2. **Fully Connected Layers**: Processes the last hidden state of the LSTM.
- The model was trained using the training set, validated after each epoch, and tested using the test set.

---

## Traditional Machine Learning Approach

- Used a **Random Forest Regressor** to predict solubility, bioactivity, and molecular weight.
- Steps followed:
  1. **Data Cleaning**: Same as the deep learning approach.
  2. **Data Preprocessing**:
     - Flattened the one-hot encoded SMILE strings into 2D input, with dimensions:
       - **Feature Dimension**: One dimension for the SMILE encoding.
       - **Batch Dimension**: The batch size.
- Trained and evaluated the Random Forest Regressor on the processed data.
