[Ελληνικά](./README.md) · **English**

# Predicting Customer Churn with Neural Networks

I completed this project for the *Neural Nets & Deep Learning* module (AI105) at the University of Essex. I wanted to see how well a neural network could identify customers likely to leave a telecom company, and how its predictions would compare with a simpler starting point, logistic regression.

[Open the notebook to explore the analysis, charts and results](./Neural_Nets_Analysis.ipynb)

## How I approached the problem

I started by exploring customer data such as time spent with the company, contract type and monthly charges. After preparing the data, I trained a logistic regression model to give me a baseline for the rest of the experiments.

I then trained a multilayer perceptron (MLP), tried dropout and L2 regularisation, and used Optuna to tune its hyperparameters. I also included Random Forest and XGBoost in the final comparison. To understand what influenced the neural network’s predictions, I examined its outputs using SHAP.

## What I found

I evaluated the four models on a test set of 1,057 customers, using the same classification threshold of 0.50. Precision, recall and F1 refer to customers who left the company. ROC-AUC was calculated from each model’s predicted probabilities.

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
---------------------------------------------------------
| Logistic Regression | 0.8108 | 0.6884 | 0.5267 | 0.5968 | 0.8447 |
| MLP with Optuna | 0.7947 | 0.6441 | 0.5089 | 0.5686 | 0.8414 |
| Random Forest | 0.7985 | 0.6753 | 0.4662 | 0.5516 | 0.8399 |
| XGBoost | 0.7985 | 0.6683 | 0.4804 | 0.5590 | 0.8423 |

Logistic regression achieved the highest F1 and ROC-AUC on this split. What stood out to me was the gap between overall accuracy and the ability to identify customers who actually left. The model classified about 81% of all customers correctly, yet it caught only 53% of those who left. The notebook also explores how adjusting the decision threshold changes the balance between precision and recall.

## Running the notebook

1. Download and extract the [Telco Customer Churn dataset from Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn).
2. Create a `Dataset` folder next to the notebook and place the CSV at `Dataset/WA_Fn-UseC_-Telco-Customer-Churn.csv`.
3. I used Python 3.12.1 for the original run. From the repository folder, run the following commands on macOS:

   ```bash
   python3.12 -m venv .venv
   source .venv/bin/activate
   python -m pip install -r requirements.txt
   ```

4. Open the folder in VS Code with the Python and Jupyter extensions installed. Open `Neural_Nets_Analysis.ipynb`, choose `.venv` under **Select Kernel**, and select **Run All**.

The notebook’s comments and discussion are written in Greek.
