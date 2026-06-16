# Part 3: Churn Prediction Model

## Overview
This section of the project focuses on building and evaluating a churn prediction model. The goal is to identify customers who are likely to churn, enabling the business to take proactive measures to retain them by leverageing historical data and machine learning techniques to predict churn probability.

## Files and Structure
- **churn_model.ipynb**: Jupyter Notebook containing the step-by-step process for data preprocessing, model training and evaluation.
- **metrics.json**: JSON file storing the evaluation metrics of the trained model.
- **model.pkl**: Serialized model file for deployment or further use.
- **requirements.txt**: List of dependencies required to run the code.
- **output/**: Directory containing the below files:
  - **error_analysis.md**: Detailed analysis of model errors.
  - **metrics.json**: Duplicate of the metrics file for reference.
  - **model_card.md**: Documentation of the model, including its purpose, limitations, and usage.
  - **charts/**: Visualizations generated during the modeling process such as ROC curves, feature importance, and confusion matrices.

## Steps to Run

### Prerequisites
1. Install Python on your system if not installed.
2. Install the required dependencies using the following command:
   ```bash
   pip install -r requirements.txt
   ```

### Running the Notebook
1. Open `churn_model.ipynb` in Jupyter Notebook or Google Colab.
2. Follow the cells sequentially to preprocess data, train the model, and evaluate its performance.
3. Review the generated charts and metrics for insights.

## Outputs
- **Evaluation Metrics**: Stored in `metrics.json`, including accuracy, precision, recall, and F1-score.
- **Visualizations**: ROC curve, feature importance, and confusion matrix in the `output/charts/` directory.
- **Model File**: Saved as `model.pkl` for deployment.

## Validation
Ensure the outputs match the expected results as outlined in the assignment requirements.

## Remark
- If using Google Colab, ensure the dataset is uploaded to the workspace before running the notebook.
- Modify paths in the script or notebook if the dataset is located in a different directory.