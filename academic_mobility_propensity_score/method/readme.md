# Applying Propensity Score Matching in R

## Description

[Propensity score matching](https://en.wikipedia.org/wiki/Propensity_score_matching) allows to assess the causal impact of treatments, interventions, or exposures in observational studies.

Propensity score matching takes covariates between treatment and control groups in tabular format as input and provides matched treatment–control pairs in a balanced dataset as output. Alternatively, propensity score matching can also be configured to pair entities based on other similarity metrics. Propensity score matching works with observational study data. Propensity score matching can use any propensity‐score–compatible estimation API. The output of propensity score matching is compatible with downstream causal‐effect estimation methods.

<img width="2355" height="755" alt="image" src="https://github.com/user-attachments/assets/b6af3e04-3941-4b7e-a9ec-7aa1ace4d30a" />

Propensity score matching placed N/A in the methodological performance competition on causal inference. Propensity score matching is much faster than other matching methods. Propensity score matching runs quickly on standard hardware. Propensity score matching does not require a GPU.

## Social Science Use Cases

- **Education Policy Evaluation**  
  [Assessing the impact of educational interventions on student outcomes](https://telearn.hal.science/hal-00190019/document)  
  **Use case:** Match students who received a new teaching method with similar peers to isolate its effect on math scores.

- **Healthcare Interventions**  
  [Evaluating the effectiveness of medical treatments on patient outcomes](https://www.tandfonline.com/doi/pdf/10.1080/00273171.2011.568786)  
  **Use case:** Compare patients on a new medication to matched controls to measure improvement in chronic disease symptoms.

- **Labor Market Studies**  
  [Analyzing the effects of job training programs on employment outcomes](https://www.nber.org/system/files/working_papers/w6829/w6829.pdf)  
  **Use case:** Match participants in a government job‐training program with non‑participants to estimate its impact on employment rates.

- **At‑Risk Youth Mentoring**  
  [Examining mentoring program impact on academic achievement](https://books.google.de/books?hl=de&lr=&id=5Y_MAwAAQBAJ&oi=fnd&pg=PP1)  
  **Use case:** Pair at‑risk students who received mentoring with similar peers to assess changes in graduation and performance.

- **Academic Mobility of Researchers**  
  [Assessing the impact of academic mobility on scientific outcomes](https://doi.org/10.1016/j.joi.2022.101280)  
  **Use case:** Match researchers who participated in international exchanges with counterparts to evaluate effects on publication and citation rates.

## Structure
The method consists of two main functions located in  ["propensity_matching_functions.R"](https://github.com/momenifi/methodHub/blob/main/academic_mobility_propensity_score/method/propensity_matching_functions.R):
1. `perform_propensity_matching`: Conducts propensity score matching and calculates standardized mean differences (SMDs) for unmatched and matched data.
2. `calculate_mean_diff`: Calculates mean differences, t-values, and standard errors for variables of interest between treatment and control groups.

## Keywords
Propensity score matching, Causal inference, Observational studies, Social science research, Methodology.

## Setup
### Environment Setup
To run this method locally, ensure you have R (version  3.6.0 or higher) installed on your system.

### Installing Dependencies
Install the required R packages:
- Matching
- tableone

### How to Use
1. Download  ["mydata_sample.csv"](https://github.com/momenifi/methodHub/blob/main/academic_mobility_propensity_score/method/mydata_sample.csv), ["propensity_matching_functions.R"](https://github.com/momenifi/methodHub/blob/main/academic_mobility_propensity_score/method/propensity_matching_functions.R), and ["main_script.R"](https://github.com/momenifi/methodHub/blob/main/academic_mobility_propensity_score/method/main_script.R) in a folder.
2. Run the commands in "main_script.R"
    - Load the input dataset into R (data_sample) (lines 1 to 5)
    - Define the functions (line 8)
    - Define the treatment variable (treatment_var) and covariates (covariates)(lines 11 and 12)
    - Call the `perform_propensity_matching` function to conduct propensity score matching (line 15) with parameters data_sample, treatment_var, and covariates.  
      The output contains SMDs of unmatched/matched data (unmatched_smd in line 20)/matched_smd in line 21) and 
    - Define the variables of interest (vars_of_interest) (line 29) and Matched data (matched_data in line 24)
    - Call the `calculate_mean_diff` function to calculate mean differences for variables of interest (line 33) with parameteres matched_data, treatment_var, and vars_of_interest. The output gets the mean differences of vars_of_interest. 


## Usage
### Input Data (DBD datasets)
This method can work with any dataset containing variables of interest, a treatment indicator, and covariates.

### Sample Input Data
Sample input data can be provided in CSV format with columns representing variables of interest (PPY, COPP, CPP), a treatment indicator (MOBILE), and covariates (REGION, MAIN_FIELD, INTERNATIONAL_COAUTHOR, GENDER, GDP_PC_ORIGIN, AGE). (mydata_sample.csv).
Here is a screenshot of sample input data:
![Image Alt Text](https://github.com/momenifi/methodHub/blob/main/academic_mobility_propensity_score/method/sample_data.PNG)

### Sample Output

The output includes standardized mean differences (SMD) for both unmatched and matched data, along with mean differences, t-values, and standard errors for the variables of interest.

By examining the SMD for unmatched and matched data under different covariances, we assess the effectiveness of the matching process in achieving balance between the treatment and control groups. A lower SMD indicates a smaller difference between the two groups. For instance, in this example, the SMD for the variable "AGE" is 0.34 for unmatched data and 0.03 for matched data. This suggests that the treatment group in the matched data is more similar to the control group compared to the unmatched data.
**SMD:**

![Image Alt Text](https://github.com/momenifi/methodHub/blob/main/academic_mobility_propensity_score/method/output_SMD.PNG)


**Main difference:**

A mean difference of 3.04 for the variable CPP indicates that, on average, the treatment group's CPP value is 3.04 units higher than that of the control group.
![Image Alt Text](https://github.com/momenifi/methodHub/blob/main/academic_mobility_propensity_score/method/output_mainDiff.PNG)


## Specifics
### Contact Details
For questions or feedback, contact [fakhri.momeni@gesis.org](mailto:fakhri.momeni@gesis.org).

### Publication
This method was utilized in the following paper:
- [The many facets of academic mobility and its impact on scholars' career](https://doi.org/10.1016/j.joi.2022.101280)

Propensity score matching results can be found in Table 6 and Table 7.
