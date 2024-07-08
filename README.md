# Beginner-Level Challenge: Aggregating TEDDY Data
This repository contains the scripts used to generate the AI-ready dataset for the Beginner-level Data Centric Challenge using data from the Environmental Determinants of Diabetes in the Young (TEDDY) study. Participants were instructed to 1) prepare a single raw dataset by aggregating all data files associated with the TEDDY study, and 2) augment the single dataset to ensure AI-readiness.

ICF Incorporated (ICF Inc.), led by Dr. Ratna Thangudu, performed a multi-step enhancement process for optimal usability and AI-readiness of TEDDY data. The team normalized various data elements, encoded categorical variables, and addressed missing values from a dataset that can affect data analysis—called “missingness” — to prepare an AI-ready data file with multiple applications. Applications included predictive models for identifying risk factors and outcomes related to type 1 diabetes and suitability for time-to-event analyses to understand development of diabetes. ICF Inc. selected the prize to co-author a challenge results publication/abstract with NIDDK for submission to a journal or professional meeting. The link to the publication will provided on this GitHub page once published.

For more information about the Data Centric Challenge, submission requirements, and guidance on AI-readiness, visit the official [Challenge.gov](https://www.challenge.gov/?challenge=niddk-central-repository-data-centric-challenge&tab=overview) page.

## Summary of Challenge Datasets
To make dataset file sizes more manageable to merge in the NIDDK-CR Analytics Workbench environment hosted by AWS, while enabling Challengers to retain as many features as possible, the NIDDK-CR Support Team performed feature redactions and participant sampling (as described in the table below) prior to making the data available to Challengers for the Data Centric Challenge. This sampling schema retained the maximum number of participants and features that can be successfully merged in the Workbench environment, while maintaining a justifiable and useful study design for many potential use-cases, including multiple disease outcomes and life-course events. 

| Study | Datasets |  Features *    |Participants| Sampling Schema |Data Dictionary |
|------:|----------|----------------|------------|-----------------|----------------|
|TEDDY|    48     |8,351            | 234,614    | All (n = 408) disease cases for T1D in TEDDY, identified by MaskID appearing in DIABETES_DIAGNOSIS dataset**. Subset (n = 409) non-disease controls, selected by simple random sample***.| [TEDDY_Data Challenge_Data Dictionary.pdf](https://repository.niddk.nih.gov/media/studies/teddy/TEDDY_Data_Challenge_Data_Dictionary.pdf)|

(*) Features that were fully empty (i.e., no non-missing values), free-text, or non-informative (i.e., all entries have the same value, or administrative variable) have been redacted from the study datasets. Please reference the [NIDDKCR_Data Challenge_TEDDY Redactions](https://github.com/niddk-data-challenge/Beginner-Level-Challenge-AI-Ready-TEDDY-Dataset/blob/3d84e4dc073dcf050ee96b76b12fff7cde55c749/Challenge%20Dataset%20Information/NIDDKCR_Data%20Challenge_TEDDY%20Redactions.xlsx) file that contains a list of features that were redacted/dropped from the TEDDY datasets.

(**) Disease cases were identified by MaskID appearance in DIABETES_DIAGNOSIS dataset, excluding those MaskIDs with PERCLINICALIMPLEMENTATION == “1”, indicating clinically determined false positives. Please reference the [NIDDKCR_Data Challenge_MaskIDs](https://github.com/niddk-data-challenge/Beginner-Level-Challenge-AI-Ready-TEDDY-Dataset/blob/81ad7018b2c1171a92c6b954fa737ef895f09b72/Challenge%20Dataset%20Information/NIDDKCR_Data%20Challenge_TEDDY%20MaskIDs.xlsx) file that contains the list of MaskIDs that were included in the Challenge-specific datasets for TEDDY.

(***) Non-disease controls were sampled from MaskIDs in ENROLLMENT_FORM dataset after excluding MaskIDs of (n = 408) disease cases. Please reference the [NIDDKCR_Data Challenge_MaskIDs](https://github.com/niddk-data-challenge/Beginner-Level-Challenge-AI-Ready-TEDDY-Dataset/blob/81ad7018b2c1171a92c6b954fa737ef895f09b72/Challenge%20Dataset%20Information/NIDDKCR_Data%20Challenge_TEDDY%20MaskIDs.xlsx) file that contains the list of MaskIDs that were included in the Challenge-specific datasets for TEDDY.

> [!Important]
> Documentation used to preprocess the TEDDY datasets to generate the Challenge-specific datasets described above are available in the [Challenge Dataset Information](https://github.com/niddk-data-challenge/Beginner-Level-Challenge-AI-Ready-TEDDY-Dataset/tree/8e33d338da451cbfb14079f8a6dd97cdbb032e9e/Challenge%20Dataset%20Information) folder. Please reference the [NIDDKCR_Data Challenge_TEDDY Redactions](https://github.com/niddk-data-challenge/Beginner-Level-Challenge-AI-Ready-TEDDY-Dataset/blob/3d84e4dc073dcf050ee96b76b12fff7cde55c749/Challenge%20Dataset%20Information/NIDDKCR_Data%20Challenge_TEDDY%20Redactions.xlsx) file that contains a list of features that were redacted/dropped from the TEDDY datasets to generate the Challenge-specific datasets. The [NIDDKCR_Data Challenge_MaskIDs](https://github.com/niddk-data-challenge/Beginner-Level-Challenge-AI-Ready-TEDDY-Dataset/blob/81ad7018b2c1171a92c6b954fa737ef895f09b72/Challenge%20Dataset%20Information/NIDDKCR_Data%20Challenge_TEDDY%20MaskIDs.xlsx) file contains the list of MaskIDs that were included in the Challenge-specific datasets for TEDDY.

If you are requesting access to, or have access to the TEDDY data from the NIDDK-CR, please reference this documentation to replicate the Challenge-specific datasets that were made available to participants for the Data Centric Challenge.

### Study Documentation
Additional information about the TEDDY study and corresponding documentation (e.g., protocols/MOPs, data collection instruments, etc.) are available on the NIDDK-CR website: https://repository.niddk.nih.gov/studies/teddy/

## Generating the AI-Ready Dataset

### Title of Project: A Semantic Data Model to Generate AI-Ready Dataset: Beginner Challenge 

#### _AI-Ready Scripts_
> [!IMPORTANT]
> Scripts created by the winning team (ICF Inc.) to generate the AI-ready dataset for TrialNet are available in the [AI-Ready Scripts](link) folder. Instructions on running the scripts and the data dictionary can be found in the README in this folder. Additional information about the AI-ready dataset, data enhancement steps and methods used to generate the AI-ready data, handling of missingness, and potential use-cases for the AI-ready dataset are described in detail below.

#### _Description of AI-Ready Dataset_
For the beginner-level challenge, we performed a multi-step enhancement process for optimal usability of The Environmental Determinants of Diabetes in the Young (TEDDY) study. Initially we transformed the 50+ studies into a single RAW file ensuring data completeness, accommodating multiple records per MaskID, and handling specific study nuances. For generating the AI-Ready dataset, observations were structured based on timepoints, and various data elements underwent normalization, including time value formatting, code standardization, and text processing. Categorical variables were encoded, generating additional columns where necessary. These refinements result in a standardized, cleaned dataset suitable for diverse AI applications in Type 1 Diabetes research. We have detailed the various enhancements and transformations in this document. More in-depth documentation is provided as inline documentation within the code, the data dictionary, and the README files. 

#### _Data Enhancements and Methods used for preparing AI-ready dataset_
To produce initial the RAW file, the following transformations were done: 

- When reading in each file, columns were checked for completeness. Those with <5% observations (relative to the number of participants in that particular study) were removed. 

- For studies with multiple records per case, additional columns were added representing each observation such that each participant was represented by one row in the final table. 

- For the “TEST_RESULTS” study, each observation was split into its own set of columns. 

- File names were appended to the beginning of the column names for every file. 

To produce the final "AI Ready" file, the initial transformations were to: 

- For studies which had observations corresponding to different timepoints: 

- The observations were split into bins based on the median number of records per case (or a maximum of 3). When there were multiple values per bin, the mean of numeric values was taken, or the mode (first in case of a tie) of categorical values was taken. 

- Where observations were not differentiated by timepoint, the summary (mean/mode) for that column was taken. 

- For columns containing time values, after correcting any formatting errors, all time values were converted to the total minutes since midnight. 

- Codes were kept in either uppercase or lowercase except for language codes, which were converted to lowercase according to ISO 639 recommendations, and country codes, which were converted to uppercase according to ISO 3166 recommendations. 

- For text columns that contained values other than codes or time, the processing included removing contractions, white spaces, and punctuation, converting the text to lowercase, and checking all words longer than four characters for misspellings using the pyspellchecker module. We reviewed the list of identified misspellings, and any false hits (such as medication names) were added to the "do not change" list. For true misspellings that were not corrected properly by pyspellchecker, we assigned a proper correction and stored them in a dictionary for the final misspelling corrections. 

- All the null values in the text columns have been substituted with the phrase 'not reported'. 

- For the categorical columns, we used one-hot encoding where each categorical variable in a column is represented by a binary vector. This resulted in creating additional columns for each categorical variable, with the column names including the categorical variable. If a categorical variable was present, its corresponding value in the column is set to “1”, and if it was not present, the value is set to “0”. The MaskID column was the only categorical column that was not included in the encoding process.

#### _How did you handle missing data_
For string missing values, we replaced them with phrase "not reported". For numeric missing values, we evaluated the completeness of the numeric features and kept the tsfeatures with more than 50% completeness. To impute the missing values, we used the Multiple Imputation by Chained Equation algorithm. This algorithm performs multiple regression over the sample data and takes averages of them. We implemented this algorithm using the fancyimpute Python library. 

When binning the observations by timepoint, cases where a value was missing during a particular observation were replaced with the value of the closest timepoint. 

#### _Potential Use-cases for AI-Ready Dataset_
The NIDDK-CR Data Centric Challenge involved transforming data from 50 studies into a single raw data file and making it AI-ready through various transformations. The initial RAW file was generated by checking column completeness, generating a wide format to handle timepoint data with multiple records per Mask ID, splitting the diagnostic test-type columns to individual properties, and appending file names to column names to maintain traceability. 

For the AI-ready file, additional transformations included formatting time values, text normalization, spelling correction, preserving codes, and replacing null values. The observations were grouped into bins based on timepoints, and for non-timepoint observations, mean/mode summaries were taken. Missing values were imputed using Multiple Imputation by Chained Equation algorithm.  

Some potential use cases for the AI-ready dataset we generated include: 

- With time values formatted, the dataset is suitable for time-to-event analyses, crucial for understanding the development of Type 1 Diabetes over time. 

- Normalized text facilitates natural language processing (NLP) applications, enabling sentiment analysis or extracting meaningful insights from textual data. 

- The imputed and cleaned dataset is helpful to building predictive models for identifying risk factors or predicting outcomes related to Type 1 Diabetes. 

- The log documenting changes made to each feature ensures transparency and traceability in research, supporting comprehensive reporting and reproducibility of results. 
 
We believe these use cases demonstrate the versatility and readiness of the dataset for a range of AI applications in Type 1 Diabetes research. 
