## The predictive power of Case Detection Rate (CDR) in country-specific mortality outcomes for patients with a dual burden of Human Immunodeficiency Viruses (HIV) and Tuberculosis (TB)

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

Through the scatterplot below, we observe that the rate of decrease in the case detection rate is much higher in countries with a dual burden of TB and HIV. This suggests that the presence of dual burden cases will have a significant impact on our model, given the strong correlation detected between the case detection rate and mortality outcomes.

<div style="margin-bottom: 5px;">
  <iframe src="assets/Scatter.html" width="800" height="600px" frameborder="0" scrolling="yes" style="transform: translateX(-50px);margin-bottom: 5px;"></iframe>
</div> 

#### Detection to Prevalence Ratio (DPR)

To provide some more insight, I calculated DPRs and grouped them by region to understand the relationships between MIRs and DPRs amongst different regions.

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
- Conversely, regions like South-East Asia (SEA) and Eastern Mediterranean (EMR) suffer from significantly low DPRs (0.0063 and 0.226), which align with their relatively high TB MIRs (0.122 and 0.134) and TB-HIV MIRs (0.246 and 0.301).
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
df['MIR_TB_quartile'] = pd.qcut(df['MIR_TB'], q=4, labels=[1, 2, 3, 4])
df['MIR_TB_HIV_quartile'] = pd.qcut(df['MIR_TB_HIV'], q=4, labels=[1, 2, 3, 4])
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

   |   Class |   Precision |   Recall |   F1-Score |   Sensitivity |   Specificity |   Macro-Average AUC |
   |--------:|------------:|---------:|-----------:|--------------:|--------------:|--------------------:|
   |       1 |        0.29 |     0.80 |       0.42 |          0.80 |          0.57 |                0.62 |
   |       2 |        0.50 |     0.29 |       0.36 |          0.29 |          0.90 |                0.62 |
   |       3 |        0.00 |     0.00 |       0.00 |          0.00 |          0.85 |                0.62 |
   |       4 |        0.57 |     0.5  |       0.53 |          0.50 |          0.85 |                0.62 |

- Model 2: MIR TB without CDR
   ```
   numeric_features = ['Estimated total population number', 'Estimated prevalence of TB (all forms)'] 
   categorical_features = ['Country or territory name'] 
   ```
   
   |   Class |   Precision |   Recall |   F1-Score |   Sensitivity |   Specificity |   Macro-Average AUC |
   |--------:|------------:|---------:|-----------:|--------------:|--------------:|--------------------:|
   |       1 |        0.19 |     0.80 |       0.31 |          0.80 |          0.26 |                0.60 |
   |       2 |        0.67 |     0.29 |       0.40 |          0.29 |          0.95 |                0.60 |
   |       3 |        0.00 |     0.00 |       0.00 |          0.00 |          0.90 |                0.60 |
   |       4 |        0.00 |     0.00 |       0.00 |          0.00 |          0.90 |                0.60 |

#### MIR TB-HIV
```
X = df[['Country or territory name', 'Estimated total population number', 'Estimated prevalence of TB (all forms)', 'Case detection rate (all forms), percent']]
y = df[['MIR_TB_HIV_quartile']]
```
- Model 1: MIR TB with CDR
   ```
   numeric_features = ['Estimated total population number', 'Estimated prevalence of TB (all forms)', 'Case detection rate (all forms), percent'] 
   categorical_features = ['Country or territory name'] 
   ```
   
   |   Class |   Precision |   Recall |   F1-Score |   Sensitivity |   Specificity |   Macro-Average AUC |
   |--------:|------------:|---------:|-----------:|--------------:|--------------:|--------------------:|
   |       1 |        0.54 |     0.88 |       0.67 |          0.88 |          0.70 |                0.84 |
   |       2 |        0.75 |     0.38 |       0.50 |          0.38 |          0.95 |                0.84 |
   |       3 |        0.60 |     0.60 |       0.60 |          0.60 |          0.91 |                0.84 |
   |       4 |        1.00 |     0.86 |       0.92 |          0.86 |          1.00 |                0.84 |
  
- Model 2: MIR TB without CDR
   ```
   numeric_features = ['Estimated total population number', 'Estimated prevalence of TB (all forms)'] 
   categorical_features = ['Country or territory name'] 
   ```
   
   |   Class |   Precision |   Recall |   F1-Score |   Sensitivity |   Specificity |   Macro-Average AUC |
   |--------:|------------:|---------:|-----------:|--------------:|--------------:|--------------------:|
   |       1 |        0.41 |     0.88 |       0.56 |          0.88 |          0.50 |                0.67 |
   |       2 |        0.00 |     0.00 |       0.00 |          0.00 |          0.90 |                0.67 |
   |       3 |        0.22 |     0.40 |       0.29 |          0.40 |          0.70 |                0.67 |
   |       4 |        0.00 |     0.00 |       0.00 |          0.00 |          1.00 |                0.67 |



  













