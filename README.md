# DSN Bootcamp Qualification Hackathon 2026 — ML Track

## Product-Store Sales Prediction

This repository contains my solution for the **DSN Bootcamp Qualification Hackathon 2026 — Machine Learning Track**.

The objective of the project is to build a regression model that predicts **`total_sales`** for products across different stores using product-related and store-related characteristics.

The competition is evaluated using **Root Mean Squared Error (RMSE)**, where a lower score indicates better predictive performance.

---

## Project Workflow

The project follows an end-to-end machine learning workflow:

1. Data loading and inspection
2. Data cleaning
3. Missing-value treatment
4. Exploratory Data Analysis (EDA)
5. Feature engineering
6. Train-validation split
7. Categorical feature encoding
8. Model development
9. Model evaluation and comparison
10. Final model training
11. Prediction on the competition test data
12. Kaggle submission

---

## Data Preprocessing

The dataset was inspected for missing values, categorical variables and other data-quality issues before modelling.

### Product Weight

Missing values in `product_weight_kg` were imputed using the mean product weight calculated from the training data.

### Store Size

Rather than filling missing `store_size` values with a single global mode, store characteristics were investigated.

Store size was imputed using the most frequent size within combinations of:

- `store_format`
- `store_location_tier`

The remaining missing observations associated with a Corner Shop were assigned the `Small` category based on the observed pattern in the training data.

---

## Exploratory Data Analysis

Exploratory analysis was performed to better understand the relationships between product/store characteristics and total sales.

The analysis included:

- Distribution of store formats
- Average sales by store format
- Product price versus total sales
- Product weight versus total sales
- Average sales by store size
- Correlation analysis of numerical variables
- Store age group analysis

---

## Feature Engineering

Additional variables were created to provide potentially useful information to the models.

### Price per Unit Weight

A new feature was created as:

`price_per_weight = product_price / product_weight_kg`

This represents the price of a product relative to its weight.

### Store Age Group

Stores were grouped according to their age to capture possible nonlinear differences between newer and more established stores.

The original numerical `store_age_years` variable was retained.

### Store Profile

A store interaction feature was created by combining:

`store_format + store_location_tier`

This allows the model to represent differences between similar store formats operating in different location tiers.

---

## Categorical Encoding

Two approaches were used to transform categorical variables into numerical representations.

### Fixed / Binary Mapping

Fixed mappings were used for variables such as:

- `store_size`
- `store_location_tier`
- `store_age_group`
- `fat_content`

### Frequency Encoding

Frequency encoding was used for nominal variables including:

- `product_code`
- `product_category`
- `store_code`
- `store_format`
- `store_profile`

To reduce data leakage during model evaluation, frequency mappings were calculated using the training subset and subsequently applied to the validation subset.

---

## Models Evaluated

Three regression algorithms were evaluated:

- **Linear Regression**
- **Random Forest Regressor**
- **Gradient Boosting Regressor**

Linear Regression was used as a baseline, while Random Forest and Gradient Boosting were included to capture potentially nonlinear relationships and interactions in the dataset.

---

## Model Evaluation

The models were evaluated using:

- Root Mean Squared Error (RMSE)
- Mean Absolute Error (MAE)
- R² Score

RMSE was used as the primary model-selection metric because it is the official evaluation metric for the competition.

The model with the lowest validation RMSE was selected for final prediction.

---

## Kaggle Submission

After model evaluation, the selected model was retrained using the full training dataset.

The same preprocessing and feature-engineering procedures were applied to the competition test data before generating predictions.

The predictions were saved in the required `submission.csv` format and submitted to Kaggle.

### Public Kaggle Score

**RMSE: 1072.63695**

> Lower RMSE values indicate better predictive performance.

---

## Repository Structure

```text
dsn-bootcamp-2026-ml-hackathon/
│
├── DSN.ipynb
├── README.md
└── submission.csv
```

The competition datasets are not included in this repository.

---

## Tools and Technologies

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Jupyter Notebook
- Kaggle

---

## How to Run

Clone the repository:

```bash
git clone <your-repository-url>
```

Place the competition files in the project directory:

```text
train.csv
test.csv
sample_submission.csv
```

Open the Jupyter Notebook:

```bash
jupyter notebook
```

Run the notebook cells sequentially from top to bottom.

---

## Conclusion

This project demonstrates an end-to-end machine learning workflow for a regression problem, covering data cleaning, exploratory analysis, feature engineering, categorical encoding, model development, validation and generation of competition predictions.

The modelling process focused on maintaining consistency between training and test preprocessing while using RMSE to guide model selection.

---

## Author

**Gideon Adedayo**

DSN Bootcamp Qualification Hackathon 2026 — ML Track
