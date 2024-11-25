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
<p>
Missing values (NaN) for certain years in the dataset were addressed using forward filling (ffill) for each country. This approach assumes that the latest available data is the closest estimate for subsequent missing years. This step preserves temporal continuity and ensures a complete dataset without introducing potential biases from averaging.
</p>
<p>
Small island sovereignties, such as Antigua and Barbuda, Barbados, Bermuda, and others (total: 11), were identified as outliers by identifying countries where the estimated number of incident cases was lesser than the estimated number of deaths from TB. Including these entries could skew the analysis, as their data does not align with trends observed in larger, more populous countries. To maintain analytical cleanliness, these entries were removed from the dataset. 
</p>
<p>
The dataset was further filtered to retain only rows from the year 2013 for each country. This decision was made to focus on a single year, ensuring consistency and comparability across countries. Our final step was to further drop all countries which contained no data from the dataset.
</p>






