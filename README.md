# Transcriptomic-Profiling-of-Old-Age-Sarcoma-Patients-using-TCGA-RNA-seq-data

This project aims to identify significant differentially expressed genes, transcription factors, prognostic biomarkers and hub genes by transcriptomic profiling of older age (>=65 years) Sarcoma patients. 

## **Table of Contents**

- [Description](#description)
- [Installation](#installation)
- [Usage](#usage)
- [Acknowledgments](#acknowledgments)


## Description
Sarcoma is a rare type of cancer that is more frequently found among children (<18 years) and older adults ( OA- age at diagnosis ≥ 65years). However, these populations are less frequently involved in clinical studies and their survival rates are poorer compared to the younger adults (YA - age at diagnosis - 18-65 years). It is further seen that the tumor microenvironment in OA cancer patients is different compared to the YA. Hence, in this study we utilize the TCGA-SARC RNA-seq database to identify differentially regulated genes, transcription factors, prognostic biomarkers and hub genes. We further perform functional enrichment analysis along with literature survey on the identified genes to understand the dysregulated pathways in OA.

We use R programming language along with several tools like Cytoscape, STRING, ShinyGO and databases TCGA, DoRothEA, TRRUST for the analysis.

## Installation

Steps to set up the project locally:

1. Cloning of repository :<br> git clone <https://github.com/vidhya2205/Transcriptomic-Profiling-of-Old-Age-Sarcoma-Patients-using-TCGA-RNA-seq-data.git>
2. Navigate to the Code directory :<br>cd Transcriptomic-Profiling-of-Old-Age-Sarcoma-Patients-using-TCGA-RNA-seq-data/Code<br>**Code Directory**: This is the folder within the project where the code resides. Ensure you execute all subsequent commands from within this directory to avoid issues with file paths or configurations.
3. Install the R and R package dependencies:<br>
   R version 4.4.0 (2024-04-24 ucrt) is used<br>
   1. CRAN packages- <br> install.packages(c("dplyr", "tidyr", "ggplot2", "gplots", "tidyverse", "reshape2", "svglite", "survminer", "survival", "forestplot")) <br>
   3. Bioconductor packages - <br>if (!requireNamespace("BiocManager", quietly = TRUE)) { install.packages("BiocManager") }<br> BiocManager::install(c("TCGAbiolinks", "SummarizedExperiment", "EnhancedVolcano", "org.Hs.eg.db", "dorothea", "enrichR", "DESeq2"))
3. Additional tools used: <br>
   1. Cytoscape - [Download Cytoscape](https://cytoscape.org/download.html) (Version 3.10.2 was used)<br>
   2. ShinyGO - [ShinyGO 0.81](https://bioinformatics.sdstate.edu/go/) web tool.

## Usage
This project is built around an R Notebook (\`code.Rmd\`) that contains multiple sections to perform different tasks. Follow the steps below to use it effectively: 

1. **Open the Code.Rmd file-** <br>Use RStudio or any R-compatible IDE to open \`code.Rmd\`.
2. **Notebook Structure -** <br> The notebook is organized into the following sections: <br>
   1. **Load the libraries needed** <br>
   2. **Section 1**: Preliminary Survival analysis, Data extraction and preprocessing - <br>
      ***Description:*** <br>
      This section obtains the Clinical and RNA-seq data from the TCGA database for SARC (sarcoma patients). The samples are stratified based on age at diagnosis into OA (≥ 65 years) and YA (18-65 years) Further, the survival analysis is done using cox regression analysis and log rank association test. A bubble plot to represent the subtypes included in the study is plotted. The RNA-seq data is preprocessed and lowly expressed genes with a quantile normalization cutoff of 0.25 are filtered out.<br>
      ***Outputs:*** <br>
      This section produces 2 images <br>
        1. [Patient Demographics](/Images/Preliminary_Analysis/Patient%20Demographics.pdf)
        2. [KM\_Plot for OAvsYA](Images/Preliminary_Analysis/Survival_Analysis_OAvsYA.pdf)      
   3. **Section 2**: Differential Gene Expression analysis (DGEA) and Functional Enrichment analysis (FEA) - <br>
      **_Description:_** <br>
      DGEA  comparing the OA with YA samples is done using the edgeR methodology. Significant differentially regulated genes (Sig-DEG’s) are selected based on logFC > ± 1.5 and p value < 0.005. A Volcano plot and heatmap representing the up and down regulated genes is made. Further, FEA of the sig-DGE’s is done to obtain the top 5 significant GO Terms associated with them.<br>
      **_Outputs:_** <br>
      This section produces 4 images and 2 csv
        1. [Enhanced Volcano](Images/DGEA%20and%20FEA/Enhanced_Volcano_Plot.pdf)
        2. [Heatmap](Images/DGEA%20and%20FEA/Heatmap.pdf)
        3. [Up-regulated genes FEA](Images/DGEA%20and%20FEA/Up_regulated_FEA.pdf)
        4. [Down regulated genes\_FEA](Images/DGEA%20and%20FEA/Down_regulated_FEA.pdf)
        5. [DGEA results(all genes).csv](Documents/DGEA/All_DGEA_results.csv)
        6. [DGEA results(significant gens).csv](Documents/DGEA/DGEA_sig_results.csv)
    4. **Section 3**:  Transcription Factor Enrichment Analysis - <br>
     **_Description:_** <br>
      Using DoRothEA and TRRUST trancription factor- Target interaction databases, in this section significant transcription factors (sig-TFs) are identified as illustrated in the [Flowchart\_TFEA](https://github.com/vidhya2205/Transcriptomic-Profiling-of-Old-Age-Sarcoma-Patients-using-TCGA-RNA-seq-data/blob/main/Images/Methodology/TFEA%20Methodology.pdf). Then we use Cytoscape app and STRING network database to visualize the interactions of the sig-TF’s. FEA analysis of the sig-TF’s is done using the ShinyGO web based tool and the top 5 GO terms are visualized in R. <br>
      **_Inputs:_** 
        1. [Human DoRothEA TF-TG database\_paper](https://doi.org/10.1101/gr.240663.118)
        2. [TRRUST TF-TG database\_Github\_repository](https://github.com/bioinfonerd/Transcription-Factor-Databases/tree/master/Ttrust_v2)
        3. [ShinyGO Results\_csv](Documents/Transcription_Factor_Analysis/TF_FEA_Shiny_GO.csv) <br>
        
       **_Outputs:_** <br> This section produces 4 images and 2 csv 
        1. [DGEA of sig-TF's](Images/TFEA/Sig-TF_DGEA.pdf)
        2. [FEA of sig-TFs](Images/TFEA/Sig-TF_FEA.pdf)
        3. [Network for TF's identified by DoRothEA database cytoscape](Images/TFEA/TF_Dorothea_Network_Cytoscape.svg)
        4. [Network for TF's identified by TRRUST database_ cytoscape](Images/TFEA/TF_TRRUST_Network_Cytoscape.svg)
        5. [TF's from DoRothEA.csv](Documents/Transcription_Factor_Analysis/Transcription_factor_DoRothEA.csv)
        6. [TF's from TRRUST.csv](Documents/Transcription_Factor_Analysis/Transcription_factor_TRRUST.csv)
    5. **Section 4**:  Gene Specific Survival analysis (Prognostic markers) -
       **_Description:_** <br>
       This section performs a gene specific survival analysis of the OA sarcoma patients exclusively by comparing samples with high (expression> median) and low (expression\<median) values to identify genes that have a significant association with their lower survival. Cox regression and KM log- rank association test based results are used to select the significant survival associated genes (sig-Surv). Functional enrichment analysis of these genes is done using the enrichR package. Further, a forest plot to represent the sig-Surv genes, expression strata (high/low) and their HR’s is plotted. <br>
       **_Outputs:_** <br>
       This section produces 4 images and 1 csv
         1. [DGEA of significant survival associated genes](Images/Gene_Specific_Survival_Analysis/Sig-Survival_FEA.pdf)
         2. [FEA of significant survival associated genes](Images/Gene_Specific_Survival_Analysis/Sig-Survival_FEA.pdf)
         3. [KM Plot for the significant survival associated genes](Images/Gene_Specific_Survival_Analysis/combined_survival_curves_final.pdf)
         4. [Forest Plot (Cox) for the survival associated genes](Images/Gene_Specific_Survival_Analysis/Forest_plot_Gene_Specific_Survival_Analysis.pdf)
         5. [Gene Specific Survival Analysis all genes (31).csv](Documents/Gene_Specific_Survival_Analysis/Gene_Specific_Survival_Analysis.csv)

## **Acknowledgments**

The authors would like to express their gratitude to Adewale Ogunleye and Richard Agyekum from the Hackbio team for their mentorship in completing this research project. 
