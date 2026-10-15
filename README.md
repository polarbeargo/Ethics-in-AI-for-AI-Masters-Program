# Ethics in AI for AI Masters Program

This project explores data representation, model performance, and fairness for a hypothetical activity recommender called **IDOOU**. Its notebook develops a classifier to predict whether a user's activity budget is at least $300, then evaluates and mitigates differences in predictions across education groups.

The analysis uses a synthetic user-experience dataset and is intended for educational purposes. It is not a production recommendation system or a model for financial or other high-stakes decisions.

## Repository contents

- [`AI Ethics Project -- STARTER.ipynb`](./AI%20Ethics%20Project%20--%20STARTER.ipynb) — data exploration, preprocessing, model evaluation, fairness metrics, and mitigation analysis.
- [`udacity_ai_ethics_project_data.csv`](./udacity_ai_ethics_project_data.csv) — dataset loaded by the notebook.
- [`requirements.txt`](./requirements.txt) — pinned Python package dependencies.
- [`model_card.html`](./model_card.html) — model details, intended use, evaluation summary, ethical considerations, and recommendations.
- [`mitigated_confusion_matrix.png`](./mitigated_confusion_matrix.png) — confusion matrix after bias mitigation.
- [`mitigated_feature_importance.png`](./mitigated_feature_importance.png) — feature-importance visualization.
- [`cohort_accuracy_by_education.png`](./cohort_accuracy_by_education.png) — cohort accuracy comparison by education.

## Getting started

### Prerequisites

- Python and Jupyter Notebook or JupyterLab.
- The project dataset is included as `udacity_ai_ethics_project_data.csv` in the repository root.

1. Clone the repository and move into its directory:

   ```bash
   git clone https://github.com/polarbeargo/Ethics-in-AI-for-AI-Masters-Program.git
   cd Ethics-in-AI-for-AI-Masters-Program
   ```

2. Install the dependencies from `requirements.txt`.

Install the dependencies listed in [`requirements.txt`](./requirements.txt) into your Python environment before starting Jupyter:

```bash
python -m pip install -r requirements.txt
```

If Jupyter is not already installed in your environment, install it separately. The notebook also contains package-install cells; installing from `requirements.txt` first provides the project's pinned dependency versions.

### Run the analysis

1. Open `AI Ethics Project -- STARTER.ipynb` in Jupyter from the repository directory so it can find the CSV.
2. Run the notebook cells in order.

The notebook cleans missing data, groups age and budget into categories, explores demographic representation, one-hot encodes categorical features, and limits its education comparison to high-school graduates and bachelor's/master's degree holders. It trains and evaluates classifiers, reports performance and fairness metrics, and applies AIF360's Reject Option Classification post-processing to the logistic regression model.

## Reported findings

The model card reports the following held-out test-set results for the logistic regression analysis:

| Measure | Before mitigation | After mitigation |
|---|---:|---:|
| Statistical parity difference | -0.9936 | 0.0064 |
| Equal opportunity difference | -1.0000 | 0.0000 |
| Disparate impact | 0.0000 | 1.0065 |
| Balanced accuracy | 0.9978 | 0.5092 |

The mitigation moves the reported parity metrics closer to their ideal values (0 for differences and 1 for disparate impact), while balanced accuracy drops substantially. These results illustrate a fairness/performance trade-off; they should not be read as evidence that the model is reliable or fair for real-world use.

## Important limitations

- The dataset has substantial missingness. Dropping incomplete rows can skew the analyzed population toward younger and more highly educated participants.
- The fairness comparison covers only selected education groups; findings do not automatically generalize to other education levels or demographic intersections.
- Near-perfect baseline performance on synthetic data may reflect patterns in how the dataset was generated, not real-world predictive ability.
- Education, age, gender, and predicted budget can encode sensitive or socioeconomic patterns. Predictions should remain optional, explainable, and subject to user correction.
- Do not use this model for credit, lending, eligibility, or other consequential decisions.

See [`model_card.html`](./model_card.html) for further details, intended-use guidance, and recommendations for additional evaluation.
