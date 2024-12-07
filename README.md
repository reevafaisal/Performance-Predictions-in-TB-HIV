## The predictive power of Case Detection Rate (CDR) in country-specific mortality outcomes for patients with a dual burden of Tuberculosis (TB) and Human Immunodeficiency Viruses (HIV)

### Introduction

The dataset, [Tuberculosis Burden by Country](https://public.tableau.com/app/sample-data/TB_Burden_Country.csv?_gl=1*jep8cy*_ga*MTk5ODg2MTIzMi4xNzMxOTM4NzQx*_ga_8YLN0SNXVS*MTczMjU0MjY2OS42LjEuMTczMjU0MjgyNC4wLjAuMA..), focuses on the global burden of TB across various countries, with an emphasis on its intersection with HIV. The data provides a detailed overview of country-specific TB burden indicators, which are critical for understanding the public health challenges related to TB and its co-morbidities, including HIV. 
<p>
Before any cleaning, the dataset contains 5120 rows. 
The following columns are relevant to the analysis:
</p> 

1. **Country or territory name**  
   - The name of the country. 

2. **Year**  
   - The reporting year.

3. **Population**  
   - The total population of the country.
     
4. **Case Detection Rate (CDR)**  
   - The proportion of new and relapsed TB cases detected and notified per year, expressed as a percentage.  
   - Independent variable of interest, representing the effectiveness of a country’s TB diagnostic and reporting systems.

5. **Estimated number of deaths from TB (all forms, excluding HIV)**  
   - Mortality per 100,000 population.
   - Used to calculate Mortality-Incidence Ratio for only TB (MIR_TB).

6. **Estimated number of deaths from TB in people who are HIV-positive**  
   - Mortality per 100,000 population.
   - Used to calculate Mortality-Incidence Ratio for only TB (MIR_TB).

7. **Estimated number of incident cases (all forms)**
   - Estimated number of TB cases per 100,000 population.
   - Used to calculate Mortality-Incidence Ratio for dual burden of HIV and TB (MIR_TB_HIV).

8. **Estimated incidence of TB cases who are HIV-positive**
   - Estimated number of TB cases among HIV-positive individuals per 100,000 population.
   - Used to calculate Mortality-Incidence Ratio for dual burden of HIV and TB (MIR_TB_HIV).

9. **Estimated prevalence of TB (all forms)e**  
   - Estimated number of TB cases (new and existing) per 100,000 population.
  
### Data Cleaning and Exploratory Data Analysis
- Missing values (NaN) for certain years in the dataset were addressed using forward filling (`ffill`) for each country. This approach assumes that the latest available data is the closest estimate for subsequent missing years and avoids potential biases from averaging.
- Small island sovereignties, such as Antigua and Barbuda, Barbados, Bermuda, and others (total: 11), were deemed as outliers by identifying countries where the estimated number of incident cases was lower than the estimated number of deaths from TB. Including these entries could skew the analysis, as their data does not align with trends observed in larger, more populous countries. To maintain analytical cleanliness, these entries were removed from the dataset. 
- The dataset was further filtered to retain only rows from the year 2013 for each country. This decision was made to focus on a single year, ensuring consistency and comparability across countries.
- Our final step was to drop all countries that contained no relevant data from the dataset.
  
#### Calculation of target variables
- Variable 1: MIR_TB == mortality of TB / incidence of TB
```
MIR_TB = df['Estimated number of deaths from TB (all forms, excluding HIV)'] / df['Estimated number of incident cases (all forms)']
```
- Variable 2: MIR_TB_HIV == mortality of (TB & HIV) / incidence of (TB & HIV)
```
MIR_TB_HIV = df['Estimated number of deaths from TB in people who are HIV-positive'] / df['Estimated incidence of TB cases who are HIV-positive']
```

These variables will be employed as predictor variables to help analyze the predictive power of Case Detection Rate (CDR) in country-specific mortality outcomes for patients with a dual burden of Human Immunodeficiency Viruses (HIV) and Tuberculosis (TB). 

| Country or territory name   |   Year |   Estimated total population number |   Estimated prevalence of TB (all forms) |   Estimated number of deaths from TB (all forms, excluding HIV) |   Estimated number of deaths from TB in people who are HIV-positive |   Estimated number of incident cases (all forms) |   Estimated HIV in incident TB (percent) |   Estimated incidence of TB cases who are HIV-positive |   Case detection rate (all forms), percent |   MIR_TB |   MIR_TB_HIV |
|:----------------------------|-------:|------------------------------------:|-----------------------------------------:|----------------------------------------------------------------:|--------------------------------------------------------------------:|-------------------------------------------------:|-----------------------------------------:|-------------------------------------------------------:|-------------------------------------------:|---------:|-------------:|
| Afghanistan                 |   2013 |                            30551674 |                                   100000 |                                                           13000 |                                                                  82 |                                            58000 |                                     0.34 |                                                    200 |                                         53 | 0.224138 |     0.41     |
| Algeria                     |   2013 |                            39208194 |                                    49000 |                                                            5100 |                                                                  35 |                                            32000 |                                     0.37 |                                                    120 |                                         66 | 0.159375 |     0.291667 |
| Angola                      |   2013 |                            21471618 |                                    91000 |                                                            6900 |                                                                1600 |                                            69000 |                                    11    |                                                   7500 |                                         85 | 0.1      |     0.213333 |
| Argentina                   |   2013 |                            41446246 |                                    13000 |                                                             570 |                                                                  44 |                                            10000 |                                     2.7  |                                                    270 |                                         89 | 0.057    |     0.162963 |
| Armenia                     |   2013 |                             2976566 |                                     2000 |                                                             170 |                                                                  12 |                                             1500 |                                     4.5  |                                                     66 |                                         95 | 0.113333 |     0.181818 |


#### MIR_TB vs MIR_TB_HIV

The closer the MIR is to 1, the higher the mortality rate. From the plots below, we can observe that in cases of a dual burden of TB and HIV, MIRs are significantly higher and exhibit more variation compared to MIRs for TB alone. This suggests that, regardless of whether a country has a higher incidence of TB, its healthcare system is less effective at treating patients who are burdened by both TB and HIV.

<div style="margin-bottom: 5px;">
  <iframe src="assets/MIR_TB.html" width="700" height="400px" frameborder="0" scrolling="yes" style="transform: translateX(-50px);margin-bottom: 5px;"></iframe>
</div>

<div style="margin-bottom: 5px;">
  <iframe src="assets/MIR_TB_HIV.html" width="700" height="400px" frameborder="0" scrolling="yes" style="transform: translateX(-50px);margin-bottom: 5px;"></iframe>
</div>

#### CDR vs MIRs

Through the scatterplot below, we observe that the rate of decrease in the case detection rate is much higher in countries with a dual burden of TB and HIV. This suggests that the presence of dual burden cases will have a large impact on our model, given the strong correlation detected between the case detection rate and mortality outcomes.

<div style="margin-bottom: 5px;">
  <iframe src="assets/Scatter.html" width="800" height="600px" frameborder="0" scrolling="yes" style="transform: translateX(-50px);margin-bottom: 5px;"></iframe>
</div> 

#### Detection to Prevalence Ratio

To provide some more insight, I calculated detection-to-prevalence ratios (DPRs) and grouped them by region to understand the relationships between MIRs and DPRs amongst different regions.

```
df['DPR'] = df['Case detection rate (all forms), percent'] / df['Estimated prevalence of TB (all forms)']
grouped_table = df.groupby(['Region']).agg(
    Total_Incidence=('Estimated number of incident cases (all forms)', 'sum'),
    Mean_DPR = ('DPR', 'sum'),
    Mean_TB_MIR=('MIR_TB', 'mean'),
    Mean_TB_HIV_MIR=('MIR_TB_HIV', 'mean')
).reset_index()
```

| Region   |   Total_Incidence |   Mean_DPR |   Mean_TB_MIR |   Mean_TB_HIV_MIR |
|:---------|------------------:|-----------:|--------------:|------------------:|
| AFR      |       2.57845e+06 | 0.76766    |     0.129574  |          0.306569 |
| AMR      |  285057           | 4.47835    |     0.0670003 |          0.196754 |
| EMR      |  713290           | 0.226031   |     0.133612  |          0.300686 |
| EUR      |  350150           | 2.1533     |     0.0684857 |          0.148143 |
| SEA      |       3.357e+06   | 0.00630488 |     0.121748  |          0.246023 |
| WPR      |       1.60893e+06 | 0.345882   |     0.0853927 |          0.170309 |

- Using the data above, we can see a clear inverse relationship between DPRs and MIRs, demonstrating early detection's critical role in reducing mortality outcomes. Regions like the Americas (AMR) and Europe (EUR), with the highest DPRs (4.478 and 2.153, respectively), report the lowest mean TB MIRs (0.067 and 0.068) and mean TB-HIV MIRs (0.197 and 0.148). This demonstrates how early detection of TB cases, enables timely treatment and lowers mortality rates. 
- Conversely, regions like South-East Asia (SEA) and Eastern Mediterranean (EMR) suffer from low DPRs (0.0063 and 0.226), which align with their relatively high TB MIRs (0.122 and 0.134) and TB-HIV MIRs (0.246 and 0.301).
- These figures highlight a diagnostic gap, where undetected cases progress to severe or fatal outcomes. Africa (AFR), with a moderate DPR (0.768), still records a high TB-HIV MIR (0.307), reflecting additional challenges in managing the dual burden cases. 

### Framing a Prediction Problem

The goal of this analysis is to evaluate **the predictive power of CDR in determining country-specific mortality outcomes for patients experiencing a dual burden of Human HIV and TB**.

#### Problem Type
- This is a multiclass classification problem. The response variables represent MIRs for TB only and TB-HIV patients, binned into quartiles to capture varying mortality levels. These quartiles represent the levels of mortality risk in countries, making this a logistic regression problem with four categories.
- The response variables are the quartiles of TB MIR (`MIR_TB_quartile`) and TB-HIV MIR (`MIR_TB_HIV_quartile`), derived from the distribution of mortality-to-incidence ratios for TB only and TB-HIV patients. These variables were chosen because they capture the gradient of mortality risk across countries, enabling nuanced predictions rather than a binary outcome.

#### Features for Prediction
- **Country or territory name**: To control for geographical disparities.
- **Estimated Total Population Number**: Accounts for variations in country size.
- **Case detection rate (all forms), percent**: The primary feature of interest, as it reflects the capacity to diagnose cases early, which is hypothesized to lower mortality rates.

#### Evaluation Metrics
- The evaluation metrics used to evaluate the performance of our model are:
   - **Sensitivity (Recall)** measures the ability to correctly identify countries in each mortality quartile, and evades false negatives. Prioritized as false negatives can have severe public health implications.
   - **Specificity** ensures that resources are not wasted on false alarms as it prevents over-prediction, and evaluates the ability to correctly exclude countries not in a specific quartile.
   - **Precision** indicates the proportion of correctly identified instances for each quartile, reducing false positives, and is prioritized over **accuracy** which is less informative in imbalanced data settings (such as in our population level data).
   - **F1-Score** accounts for both false positives and false negatives, making it ideal for imbalanced datasets.
   - **AUC** evaluates the model's ability to distinguish between categories by considering its performance across all possible decision thresholds which is useful to address the performance of our model.

### Baseline Model

To prepare the data for performing the logistic regression, I binned the MIRs by percentiles so as not to under-assign or over-assign values to specific bins.
```
quartile_discretizer = KBinsDiscretizer(n_bins=4, encode='ordinal', strategy='quantile')
df['MIR_TB_quartile'] = quartile_discretizer.fit_transform(df[['MIR_TB']]).astype(int) + 1
df['MIR_TB_HIV_quartile'] = quartile_discretizer.fit_transform(df[['MIR_TB_HIV']]).astype(int) + 1
```

**Defining the Logistic Regression model**
```
preprocessor = ColumnTransformer(
    transformers=[
        ("num", numeric_transformer, numeric_features),
        ("cat", categorical_transformer, categorical_features)
    ]
)

logistic_model = LogisticRegression(
    multi_class="multinomial",  
    solver="lbfgs",  
    max_iter=500
)
```

#### MIR TB
```
X = df[['Country or territory name', 'Estimated total population number', 'Estimated prevalence of TB (all forms)', 'Case detection rate (all forms), percent']]
y = df[['MIR_TB_quartile']]
```

- Model 1: MIR TB with CDR
   ```
   numeric_features = ['Estimated total population number', 'Estimated prevalence of TB (all forms)', 'Case detection rate (all forms), percent'] 
   categorical_features = ['Country or territory name'] 
   ```

   |   Class |   Precision |   Recall |   F1-Score |   Sensitivity |   Specificity |   AUC |
   |--------:|------------:|---------:|-----------:|--------------:|--------------:|------:|
   |       1 |       0.333 |    0.8   |      0.471 |         0.8   |         0.652 | 0.608 |
   |       2 |       0.429 |    0.429 |      0.429 |         0.429 |         0.81  | 0.608 |
   |       3 |       0     |    0     |      0     |         0     |         0.95  | 0.608 |
   |       4 |       0.625 |    0.625 |      0.625 |         0.625 |         0.85  | 0.608 |

- Model 2: MIR TB without CDR
   ```
   numeric_features = ['Estimated total population number', 'Estimated prevalence of TB (all forms)'] 
   categorical_features = ['Country or territory name'] 
   ```
   
   |   Class |   Precision |   Recall |   F1-Score |   Sensitivity |   Specificity |   AUC |
   |--------:|------------:|---------:|-----------:|--------------:|--------------:|------:|
   |       1 |       0.19  |    0.8   |      0.308 |         0.8   |         0.261 | 0.566 |
   |       2 |       0.667 |    0.286 |      0.4   |         0.286 |         0.952 | 0.566 |
   |       3 |       0     |    0     |      0     |         0     |         0.95  | 0.566 |
   |       4 |       0     |    0     |      0     |         0     |         0.85  | 0.566 |

#### MIR TB-HIV
```
X = df[['Country or territory name', 'Estimated total population number', 'Estimated prevalence of TB (all forms)', 'Case detection rate (all forms), percent']]
y = df[['MIR_TB_HIV_quartile']]
```
- Model 1: MIR TB-HIV with CDR
   ```
   numeric_features = ['Estimated total population number', 'Estimated prevalence of TB (all forms)', 'Case detection rate (all forms), percent'] 
   categorical_features = ['Country or territory name'] 
   ```
   
   |   Class |   Precision |   Recall |   F1-Score |   Sensitivity |   Specificity |   AUC |
   |--------:|------------:|---------:|-----------:|--------------:|--------------:|------:|
   |       1 |       0.538 |    0.875 |      0.667 |         0.875 |         0.7   | 0.856 |
   |       2 |       1     |    0.375 |      0.545 |         0.375 |         1     | 0.856 |
   |       3 |       0.6   |    0.6   |      0.6   |         0.6   |         0.913 | 0.856 |
   |       4 |       0.857 |    0.857 |      0.857 |         0.857 |         0.952 | 0.856 |
  
- Model 2: MIR TB-HIV without CDR
   ```
   numeric_features = ['Estimated total population number', 'Estimated prevalence of TB (all forms)'] 
   categorical_features = ['Country or territory name'] 
   ```
   
   |   Class |   Precision |   Recall |   F1-Score |   Sensitivity |   Specificity |   AUC |
   |--------:|------------:|---------:|-----------:|--------------:|--------------:|------:|
   |       1 |       0.389 |    0.875 |      0.538 |         0.875 |         0.45  | 0.693 |
   |       2 |       0.333 |    0.125 |      0.182 |         0.125 |         0.9   | 0.693 |
   |       3 |       0     |    0     |      0     |         0     |         1     | 0.693 |
   |       4 |       0.571 |    0.571 |      0.571 |         0.571 |         0.857 | 0.693 |

### Final Model

<div style="margin-bottom: 5px;">
  <iframe src="assets/three_graphs.html" width="800" height="350px" frameborder="0" scrolling="yes" style="transform: translateX(-50px);margin-bottom: 5px;"></iframe>
</div> 

Through the above visualization, we can see that the total population and TB prevalence are extremely right-skewed. Since log transformations efficiently normalize right-skewed data, I have used them to transform those columns. Since the CDR is skewed in the other direction, I have used a quantile transformer to transform it into a uniform distribution. These transformations will ensure our data is less skewed and more robust to outliers.

```
log_transformer = FunctionTransformer(np.log1p, validate=True)
quantile_transformer = QuantileTransformer(output_distribution='uniform', random_state=42)

numeric_transformer = ColumnTransformer(
    transformers=[
        ("log", log_transformer, ['Estimated total population number', 'Estimated prevalence of TB (all forms)']),
        ("quantile", quantile_transformer, ['Case detection rate (all forms), percent']),
        ("scaler", StandardScaler(), numeric_features)  
    ]
)
```

#### Modeling Algorithm
- For this task, I used Logistic Regression as the modeling algorithm, leveraging its suitability for multiclass classification through softmax regression.
I used GridSearchCV to select the hyperparameters. This method performs cross-validation (2-fold in our case) for each combination of hyperparameters and evaluates performance using an AUC scorer.

```
param_grid = {
    "logistic__C": [0.01, 0.1, 1, 10, 100],  
    "logistic__solver": ["lbfgs", "liblinear"],  
    "logistic__penalty": ["l1", "l2"],  
    "logistic__multi_class": ["ovr", "multinomial"], 
    "logistic__max_iter": [100, 200, 500]  
}

auc_scorer = make_scorer(roc_auc_score, needs_proba=True, multi_class="ovr", average="macro")

grid_search = GridSearchCV(
    estimator=pipeline,
    param_grid=param_grid,
    cv=2,  
    scoring=auc_scorer, 
    verbose=1,  
    n_jobs=-1 
)
```

#### New MIR TB
```
X = df[['Country or territory name', 'Estimated total population number', 'Estimated prevalence of TB (all forms)', 'Case detection rate (all forms), percent']]
y = df[['MIR_TB_quartile']]
```

- Model 1: MIR TB with CDR
   ```
   numeric_features = ['Estimated total population number', 'Estimated prevalence of TB (all forms)', 'Case detection rate (all forms), percent'] 
   categorical_features = ['Country or territory name'] 
   ```

   |   Class |   Precision |   Recall |   F1-Score |   Sensitivity |   Specificity |   AUC |
   |--------:|------------:|---------:|-----------:|--------------:|--------------:|------:|
   |       1 |       0.286 |    0.8   |      0.421 |         0.8   |         0.565 | 0.686 |
   |       2 |       0.75  |    0.429 |      0.545 |         0.429 |         0.952 | 0.686 |
   |       3 |       0     |    0     |      0     |         0     |         1     | 0.686 |
   |       4 |       0.6   |    0.75  |      0.667 |         0.75  |         0.8   | 0.686 |

   Best performing hyperparameters:
   ```
   {'logistic__C': 0.1, 'logistic__max_iter': 200, 'logistic__multi_class': 'ovr', 'logistic__penalty': 'l1', 'logistic__solver': 'liblinear'}
   ```


- Model 2: MIR TB without CDR
   ```
   numeric_features = ['Estimated total population number', 'Estimated prevalence of TB (all forms)'] 
   categorical_features = ['Country or territory name'] 
   ```
   
   |   Class |   Precision |   Recall |   F1-Score |   Sensitivity |   Specificity |   AUC |
   |--------:|------------:|---------:|-----------:|--------------:|--------------:|------:|
   |       1 |       0.286 |     0.8  |      0.421 |          0.8  |         0.565 | 0.593 |
   |       2 |       0     |     0    |      0     |          0    |         1     | 0.593 |
   |       3 |       0     |     0    |      0     |          0    |         1     | 0.593 |
   |       4 |       0.429 |     0.75 |      0.545 |          0.75 |         0.6   | 0.593 |

   Best performing hyperparameters:
   ```
   {'logistic__C': 0.1, 'logistic__max_iter': 100, 'logistic__multi_class': 'ovr', 'logistic__penalty': 'l1', 'logistic__solver': 'liblinear'}
   ```

#### New MIR TB-HIV
```
X = df[['Country or territory name', 'Estimated total population number', 'Estimated prevalence of TB (all forms)', 'Case detection rate (all forms), percent']]
y = df[['MIR_TB_HIV_quartile']]
```
- Model 1: MIR TB-HIV with CDR
   ```
   numeric_features = ['Estimated total population number', 'Estimated prevalence of TB (all forms)', 'Case detection rate (all forms), percent'] 
   categorical_features = ['Country or territory name'] 
   ```
   
   |   Class |   Precision |   Recall |   F1-Score |   Sensitivity |   Specificity |   AUC |
   |--------:|------------:|---------:|-----------:|--------------:|--------------:|------:|
   |       1 |        0.75 |    0.75  |      0.75  |         0.75  |         0.9   | 0.874 |
   |       2 |        0.6  |    0.75  |      0.667 |         0.75  |         0.8   | 0.874 |
   |       3 |        0.5  |    0.4   |      0.444 |         0.4   |         0.913 | 0.874 |
   |       4 |        1    |    0.857 |      0.923 |         0.857 |         1     | 0.874 |

   Best performing hyperparameters:
   ```
   {'logistic__C': 100, 'logistic__max_iter': 500, 'logistic__multi_class': 'multinomial', 'logistic__penalty': 'l2', 'logistic__solver': 'lbfgs'}
   ```
  
- Model 2: MIR TB-HIV without CDR
   ```
   numeric_features = ['Estimated total population number', 'Estimated prevalence of TB (all forms)'] 
   categorical_features = ['Country or territory name'] 
   ```
   
   |   Class |   Precision |   Recall |   F1-Score |   Sensitivity |   Specificity |   AUC |
   |--------:|------------:|---------:|-----------:|--------------:|--------------:|------:|
   |       1 |         0.5 |    0.875 |      0.636 |         0.875 |         0.65  | 0.749 |
   |       2 |         0   |    0     |      0     |         0     |         0.9   | 0.749 |
   |       3 |         0   |    0     |      0     |         0     |         1     | 0.749 |
   |       4 |         0.5 |    0.857 |      0.632 |         0.857 |         0.714 | 0.749 |

   Best performing hyperparameters:
   ```
   {'logistic__C': 100, 'logistic__max_iter': 100, 'logistic__multi_class': 'multinomial', 'logistic__penalty': 'l2', 'logistic__solver': 'lbfgs'}
   ```

### Key Findings
- Impact of CDR on Mortality Prediction:
   - Including CDR as a feature improved model performance across both MIR TB and MIR TB-HIV, highlighting its predictive power in reducing mortality outcomes.
   - In countries with dual TB-HIV burdens, the presence of CDR yielded notable improvements in sensitivity and AUC, indicating the importance of early case detection in mitigating mortality.
- Differences Between MIR TB and MIR TB-HIV:
   - Models predicting MIR TB-HIV consistently outperformed those predicting MIR TB, likely due to the higher variability and complexity in dual-burden mortality outcomes.
   - MIR TB-HIV models achieved higher precision, recall, and AUC values, suggesting that the dual-burden dataset contains more actionable patterns for logistic regression.
- Role of Regularization and Solvers:
   - liblinear solver with L1 regularization performed better for MIR TB predictions, where sparsity was beneficial for the simpler relationships in the dataset.
   - lbfgs solver with L2 regularization excelled in MIR TB-HIV predictions, as it preserved subtle relationships among features in a more complex dataset.

### Conclusion
This study demonstrates that incorporating Case Detection Rate (CDR) and applying feature engineering techniques like log and quantile transformations substantially improve the predictive power of logistic regression models for mortality outcomes in TB and TB-HIV patients. The findings underscore the critical role of early detection systems in reducing mortality and provide actionable insights for public health policies aimed at addressing TB and HIV's dual burden globally.








  













