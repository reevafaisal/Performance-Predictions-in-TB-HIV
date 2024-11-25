## The predictive power of Case Detection Rate (CDR) in country-specific mortality outcomes for patients with a dual burden of Human Immunodeficiency Viruses (HIV) and Tuberculosis (TB)

### Introduction

The dataset, [Tuberculosis Burden by Country](https://public.tableau.com/app/sample-data/TB_Burden_Country.csv?_gl=1*jep8cy*_ga*MTk5ODg2MTIzMi4xNzMxOTM4NzQx*_ga_8YLN0SNXVS*MTczMjU0MjY2OS42LjEuMTczMjU0MjgyNC4wLjAuMA..), focuses on the global burden of tuberculosis (TB) across various countries, with an emphasis on its intersection with Human Immunodeficiency Virus (HIV). The data provides a detailed overview of country-specific TB burden indicators, which are critical for understanding the public health challenges related to TB and its co-morbidities, including HIV. 
<p>
Before any cleaning, the dataset contains 5120 rows. 
The following columns are relevant to our analysis:
</p>

1. **Country or territory name**  
   - The name of the country. 

2. **Year**  
   - The reporting year. 

3. **Case Detection Rate (CDR)**  
   - The proportion of new and relapse TB cases detected and notified per year, expressed as a percentage.  
   - Independent variable of interest, representing the effectiveness of a country’s TB diagnostic and reporting systems.

4. **Estimated number of deaths from TB (all forms, excluding HIV)**  
   - Mortality per 100,000 population.
   - Used to calculate mortality-to-incidence ratio (MIR_TB) for only TB.

4. **Estimated number of deaths from TB in people who are HIV-positive**  
   - Mortality per 100,000 population.
   - Used to calculate mortality-to-incidence ratio (MIR_TB) for only TB.

5. **Incidence Rate (TB)**
   - Estimated number of TB cases per 100,000 population.
   - Used to calculate mortality-to-incidence ratio (MIR_TB_HIV) for dual burden of HIV and TB.

6. **Incidence Rate (TB/TB & HIV)**
   - Estimated number of TB cases among HIV-positive individuals per 100,000 population.
   - Used to calculate mortality-to-incidence ratio (MIR_TB_HIV) for dual burden of HIV and TB.

7. **TB Prevalence Rate**  
   - Estimated number of TB cases (new and existing) per 100,000 population.  
   - Gives an overview of the TB burden in the population.

8. **HIV Prevalence Rate**  
   - The estimated number of people living with HIV per 100,000 population.  
   - Contextualizes the extent of HIV within the population, which is crucial for understanding the dual burden.

9. **TB Mortality Rate (All Causes)**  
   - Mortality attributable to TB (irrespective of HIV status) per 100,000 population.  
   - Broader metric for TB’s impact on overall population mortality.

