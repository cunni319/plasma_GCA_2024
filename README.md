# plasma_GCA_2023
Analysis of plasma proteins in Giant Cell Arteritis (GCA) patients compared with healthy controls.
===================================================

This repository includes Jupyter lab notebooks to run for the analysis of this project. 
The input data is included in the repository; no editing is required to run the scripts. 
Each script has local data that is read in, and all output for the figures is automatically 
put into the corresponding output directory.

The scripts included are the following:

## Data Preprocessing

>quantile_normalization.ipynb

This script takes the raw RFU data from SomaLogic, and quantile normalizes the samples.
A box plot of all samples is provided at the end of the script to illustrate that all samples
have the same distribution and median after quantile normalization. The quantile normalized 
data is saved in the data directory for all downstream analysis.


## Exploratory analysis
>PCA.ipynb

This script takes the quantile normalized data and makes a PCA plot in R. Additionally, this
script makes box plots of the distribution of PC1 and PC2 values for all three study groups
(Active GCA, Inactive GCA, and Healthy controls). A Mann–Whitney *U* test was used to compare 
the PC1 and PC2 distributions between all three study groups, the *P*-values are provided and
denoted between each group.

## Differential abundance analysis
>linear_modeling_between_PC1_and_demographic_variables.ipynb

This script uses the quantile normalized data to do PCA analysis. The PC1 values for all
three study groups are saved for linear modeling. Linear regression models were constructed between
clinical and demographic variables for all three study groups. This includes the Study group, age,
prednisone use, BMI, aspirin use, sex, PGA, Smoking status, and CRP. Each clinical and demographic
variable had an individual linear regression model constructed. The *P*-value and the R<sup>2</sup> for the 
variable of interest are saved to make a lollipop plot with the length of the line representing the linear
regression model *P*-value and the size of the point representing the R<sup>2</sup> value.


>linear_modeling_active_and_controls.ipynb

This script uses the quantile normalized data as well as the clinical and demographic data to build linear
regression models between Active GCA patients and Healthy controls. Marginal linear regression models were
run on six clinical and demographic variables (age, smoking status, sex, prednisone use, aspirin use, and 
methotrexate use) between Active GCA and Healthy controls. Variables with linear regression model *P*-values < 
0.05 were identified as significant confounders and included in the full multiple linear regression models. In the
full multiple linear regression models, the *P*-value from the study group variable was used to identify 
differentially abundant proteins between Active GCA and Healthy controls. A threshold of *P* < 0.01 was applied to 
all plasma proteins for significance.


>linear_modeling_inactive_and_controls.ipynb

This script uses the quantile normalized data as well as the clinical and demographic data to build linear
regression models between Inactive GCA patients and Healthy controls. Marginal linear regression models were
run on six clinical and demographic variables (age, smoking status, sex, prednisone use, aspirin use, and 
methotrexate use) between Inactive GCA and Healthy controls. Variables with linear regression model 
*P*-values < 0.05 were identified as significant confounders and included in the full multiple linear regression 
models. In the full multiple linear regression models, the *P*-value from the study group variable was used to 
identify differentially abundant proteins between Inactive GCA and Healthy controls. A threshold of *P* < 0.01 was
applied to all plasma proteins for significance.

>linear_modeling_active_and_inactive_GCA.ipynb

This script uses the quantile normalized data as well as the clinical and demographic data to build linear
regression models between Inactive GCA patients and Healthy controls. Marginal random effect linear regression 
models were run on six clinical and demographic variables (age, smoking status, sex, prednisone use, aspirin use, 
and methotrexate use)between Active GCA and Inactive GCA. Variables with random effect linear regression model 
*P*-values < 0.05 were identified as significant confounders and included in the full random effect linear 
regression models. In the full random effect linear regression models, the *P*-value from the study group variable 
was used to identify differentially abundant proteins between Active GCA and Inactive GCA. A threshold of 
*P* < 0.01 was applied to all plasma proteins for significance.

>linear_modeling_summary.ipynb

This script reads the results from the multiple linear regression models between Active GCA and Healthy controls 
as well as for Inactive GCA and Healthy controls. It presents the number of significant proteins (*P* < 0.01) for
both group comparisons. Additionally, it provides how many proteins are higher or lower in both group comparisons 
(*i.e.,*, Active GCA vs. Healthy controls and Inactive GCA vs. Healthy controls) as well as how many overlapp
between the two groups. These results are denoted in Figures 2A and B.

>active_GCA_vs_healthy_controls_heatmap.ipynb

This script reads in the multiple linear regression model results between Active GCA and Healthy controls. It
gathers the proteins from Active GCA and Healthy control and makes a heatmap after doing a z-score transformation
on the data. Age, sex, smoking status, and BMI are denoted at the top of each heatmap for each study participant.

>inactive_GCA_vs_healthy_controls_heatmap.ipynb

This script reads in the multiple linear regression model results between Inactive GCA and Healthy controls. It
gathers the proteins from Inactive GCA and Healthy control and makes a heatmap after doing a z-score transformation
on the data. Age, sex, smoking status, and BMI are denoted at the top of each heatmap for each study participant.

>active_GCA_vs_inactive_GCA_heatmap.ipynb

This script reads in the random effect linear regression model results between Active GCA and Inactive GCA. It
gathers the proteins from Active GCA and Inactive GCA and makes a heatmap after doing a z-score transformation
on the data. Age, sex, smoking status, and BMI are denoted at the top of each heatmap for each study participant.


## Significant enriched GO Biological Processes
>top_20_GO_terms_from_DAVID.ipynb

This script reads the results from using the online bioinformatics tool DAVID to identify significantly
enriched Biological Processes for differentially abundant proteins. There are four groups of proteins that were
submitted to DAVID:
  1. Differentially abundant proteins higher in Active GCA compared to Healthy controls
  2. Differentially abundant proteins lower in Active GCA compared to Healthy controls
  3. Differentially abundant proteins higher in Inactive GCA compared to Healthy controls
  4. Differentially abundant protein lower in Inactive GCA compared to Healthy controls
     
A *P*-value < 0.01 from a modified Fisher's exact test provided by DAVID was used as a threshold for significance.
This script orders all Biological Processes based on their *P*-values and plots the top 20 most significant GO
Biological Processes for each group of differentially abundant proteins. The script makes four bar graphs with the
length of the bars as the *P*-value significance and shade representing the fold-enrichment.

>volcano_plot_with_PGA.ipynb

The Physician's Global Assessment (PGA) is a commonly used GCA measurement for disease severity in patients. This
script uses the Active GCA plasma proteins and the Active GCA patients' clinical and demographic data to identify
proteins associated with PGA in Active GCA patients. Marginal linear regression models were constructed between 
all proteins and six clinical and demographic variables (age, smoking status, sex, prednisone use, aspirin use,
and methotrexate use). Variables with a *P*-value < 0.05 were included in the full multiple linear regression
model between protein abundance and PGA. After constructing the linear regression models, Spearman rho values,
along with their corresponding *P*-values, were calculated between proteins and PGA. All proteins with a *P*-value 
< 0.05 and an |Spearman rho| > 0.4 were identified as significant associations. A volcano plot is made at the very
end, with the proteins of interest highlighted in colors (blue and red).



# Installation

There are a few R libraries that need to be installed to run these scripts.
They are:

```
library(dplyr)
library(reshape2)
library(ggpubr)
library(Hmisc)
library(preprocessCore)
library(effsize)
library(pheatmap)
library(FactoMineR)
library(stats)
library(factoextra)
library(ggfortify)
```

There are also a few Python libraries that need to be installed to run these scripts.
They are:

```
pandas
scikit-learn
numpy
```
