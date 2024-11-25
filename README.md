## The predictive power of Case Detection Rate (CDR) in country-specific mortality outcomes for patients with a dual burden of Human Immunodeficiency Viruses (HIV) and Tuberculosis (TB)

### Introduction

The dataset, [Tuberculosis Burden by Country](https://public.tableau.com/app/sample-data/TB_Burden_Country.csv?_gl=1*jep8cy*_ga*MTk5ODg2MTIzMi4xNzMxOTM4NzQx*_ga_8YLN0SNXVS*MTczMjU0MjY2OS42LjEuMTczMjU0MjgyNC4wLjAuMA..), focuses on the global burden of TB across various countries, with an emphasis on its intersection with HIV. The data provides a detailed overview of country-specific TB burden indicators, which are critical for understanding the public health challenges related to TB and its co-morbidities, including HIV. 
<p>
Before any cleaning, the dataset contains 5120 rows. 
The following columns are relevant to our analysis:
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
- Missing values (NaN) for certain years in the dataset were addressed using forward filling `ffill` for each country. This approach assumes that the latest available data is the closest estimate for subsequent missing years and avoids potential biases from averaging.
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

|   index | Country or territory name   |   Year |   Estimated total population number |   Estimated prevalence of TB (all forms) |   Estimated number of deaths from TB (all forms, excluding HIV) |   Estimated number of deaths from TB in people who are HIV-positive |   Estimated number of incident cases (all forms) |   Estimated HIV in incident TB (percent) |   Estimated incidence of TB cases who are HIV-positive |   Case detection rate (all forms), percent |   mir_TB |   mir_TB_HIV |
|--------:|:----------------------------|-------:|------------------------------------:|-----------------------------------------:|----------------------------------------------------------------:|--------------------------------------------------------------------:|-------------------------------------------------:|-----------------------------------------:|-------------------------------------------------------:|-------------------------------------------:|---------:|-------------:|
|      23 | Afghanistan                 |   2013 |                            30551674 |                                   100000 |                                                           13000 |                                                                  82 |                                            58000 |                                     0.34 |                                                    200 |                                         53 | 0.224138 |     0.41     |
|      71 | Algeria                     |   2013 |                            39208194 |                                    49000 |                                                            5100 |                                                                  35 |                                            32000 |                                     0.37 |                                                    120 |                                         66 | 0.159375 |     0.291667 |
|     143 | Angola                      |   2013 |                            21471618 |                                    91000 |                                                            6900 |                                                                1600 |                                            69000 |                                    11    |                                                   7500 |                                         85 | 0.1      |     0.213333 |
|     191 | Argentina                   |   2013 |                            41446246 |                                    13000 |                                                             570 |                                                                  44 |                                            10000 |                                     2.7  |                                                    270 |                                         89 | 0.057    |     0.162963 |
|     215 | Armenia                     |   2013 |                             2976566 |                                     2000 |                                                             170 |                                                                  12 |                                             1500 |                                     4.5  |                                                     66 |                                         95 | 0.113333 |     0.181818 |









