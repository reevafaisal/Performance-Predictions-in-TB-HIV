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

