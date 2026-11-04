# SHAP Values

*Machine Learning Explainability — lesson 4* · [Tutorial on Kaggle](https://www.kaggle.com/code/dansbecker/shap-values) · [Exercise on Kaggle](https://www.kaggle.com/code/dansbecker/exercise-shap-values)

## Key ideas

- SHAP values split a single prediction into contributions from each feature relative to a baseline.
- `shap.TreeExplainer` for tree models; force plots visualise one prediction.

## Functions and tools used

`pd.read_csv`, `train_test_split`, `.fit`, `RandomForestClassifier`, `.reshape`, `.predict_proba`, `shap.TreeExplainer`, `.shap_values`, `shap.initjs`, `shap.force_plot`, `shap.KernelExplainer`

## Exercise

### `q_1` — Step 1

**Discussion:** # Use permutation importance as a succinct model summary
# A measure of model performance on validation data would be useful here too

import eli5
from eli5.sklearn import PermutationImportance

perm = PermutationImportance(my_model, random_state=1).fit(val_X, val_y)
eli5.show_weights(perm, feature_names = val_X.columns.tolist())

### `q_2` — Step 2

**Discussion:** # PDP for number_inpatient feature

from matplotlib import pyplot as plt
from sklearn.inspection import PartialDependenceDisplay

feature_name = 'number_inpatient'
PartialDependenceDisplay.from_estimator(my_model, val_X, [feature_name])
plt.show()

### `q_3` — Step 3

**Discussion:** The results are very different. Specifically time in hospital has a much smaller effect. Code below:

    from matplotlib import pyplot as plt
    from sklearn.inspection import PartialDependenceDisplay

    feature_name = 'time_in_hospital'
    PartialDependenceDisplay.from_estimator(my_model, val_X, [feature_name])
    plt.show()

### `q_4` — Step 4

**Discussion:** # A simple pandas groupby showing the average readmission rate for each time_in_hospital.

# Do concat to keep validation data separate, rather than using all original data
all_train = pd.concat([train_X, train_y], axis=1)

all_train.groupby(['time_in_hospital']).mean().readmitted.plot()
plt.show()

### `q_5` — Step 5

**Discussion:** # Use SHAP values to show the effect of each feature of a given patient

import shap  # package used to calculate Shap values

sample_data_for_prediction = val_X.iloc[0].astype(float)  # to test function

def patient_risk_factors(model, patient_data):
    # Create object that can calculate shap values
    explainer = shap.TreeExplainer(model)
    shap_values = explainer.shap_values(patient_data)
    shap.initjs()
    return shap.force_plot(explainer.expected_value[1], shap_values[1], patient_data)
