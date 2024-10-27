
# Retail Store Profit Forecasting Django Application

This Django application forecasts profits for a retail store based on date, gender, product category, and age. It provides visual insights through historical data trends, forecasted values with confidence intervals, and a comparison of actual vs. forecasted profits.

## Table of Contents

- **Getting Started**
- **Setup Instructions**
- **Dataset and Forecasting Model**
- **Challenges Faced**

---

## Getting Started

Follow these steps to set up the project, run the application, and view the retail store profit forecasting dashboard.

---

## Setup Instructions

1. **Clone the Repository**

   Clone this repository to your local machine using:
   ```bash
   git clone git@github.com:TEBIAN/Retail-Store.git
   ```

2. **Navigate to the Project Directory**
   ```bash
   cd retail-store-profit-forecasting
   ```

3. **Create and Activate a Virtual Environment**

   It’s recommended to use a virtual environment for dependency management:
   ```bash
   python3 -m venv env
   source env/bin/activate  # For Windows: env\Scripts\activate
   ```

4. **Install Dependencies**

   Install the necessary packages using `pip`:
   ```bash
   pip install -r requirements.txt
   ```

5. **Set Up Django Application**

   Run the following to apply migrations and create the initial database
   ```bash
   python forecasting_app/forecasting/manage.py migrate
   ```


6. **Load Sample Data**

   Place your dataset file (e.g., `sales_data.csv`) in the project root directory. This dataset should include the following columns:

   - `date` (date of sale)
   - `gender` (customer gender)
   - `product_category` (type of product)
   - `age` (customer age)
   - `profit` (profit generated from the sale)

7. **Train the Model**

   Run the `train_model` function in `ml_model.py` to train and save the forecasting model. This function loads the dataset, preprocesses data, trains a Random Forest model, and saves the model to `model.pkl` for reuse.
   ```python
   python forecasting_app/forecasting/manage.py shell
   >>> from app_name.ml_model import train_model
   >>> train_model()
   ```

8. **Run the Django Server**

   Start the server using:
   ```bash
   python manage.py runserver
   ```

9. **Access the Application**

   Go to `http://127.0.0.1:8000/visualizations/` to view visualizations for historical trends, forecasted values, and actual vs. forecasted comparisons.

---

## Dataset and Forecasting Model

### Dataset

The dataset used in this application contains records of retail sales, with each row representing a sale. Key columns include:
- **Date**: Date of sale, which we use to derive `year`, `month`, and `day`.
- **Gender**: Customer gender, an important categorical feature.
- **Product Category**: Type of product purchased.
- **Age**: Customer age, allowing for customer segmentation.
- **Profit**: Profit generated from each sale, the target variable for forecasting.

### Forecasting Model

The forecasting model is built using **Random Forest Regressor**, which is robust for regression tasks involving numerical and categorical data. The model takes date-derived features, gender, age, and product category to predict the profit from future sales. Key visualizations provided by the app include:
- **Historical Profit Trends**: Shows past profit trends to help identify patterns.
- **Forecasted Profit with Confidence Intervals**: Provides 30-day profit forecasts, displaying upper and lower confidence limits.
- **Actual vs. Forecasted Profit Comparison**: Highlights the accuracy of the model by comparing actual profits with predicted values.

---

## Challenges Faced

During the implementation, several challenges arose:

1. **Data Preprocessing**:
   - Handling date features required extracting `year`, `month`, and `day`, which was essential for the model to understand time-related patterns.
   - Encoding categorical features such as `gender` and `product category` was necessary for using them in the machine learning pipeline.

2. **Pipeline and Transformer Compatibility**:
   - Initial errors were encountered due to differences between using `DataFrame` vs. `NumPy arrays` in the `ColumnTransformer`. Ensuring that input data remained as a DataFrame resolved these issues.

3. **Model Interpretation and Confidence Intervals**:
   - Confidence intervals were approximated at ±10% of the forecasted values to provide an initial sense of forecast reliability. In production, more robust methods like quantile regression could enhance accuracy.

---

This application demonstrates an end-to-end solution for profit forecasting in a retail setting, combining machine learning, data visualization, and web deployment with Django. Future improvements could include additional model optimization, improved forecasting methods, and further refinement of confidence intervals.
