# Beginner-Level Challenge: Aggregating TEDDY Data
This repository contains the scripts used to generate the AI-ready dataset for the Beginner-level Data Centric Challenge using data from the Environmental Determinants of Diabetes in the Young (TEDDY) study. Participants were instructed to 1) prepare a single raw dataset by aggregating all data files associated with one or more longitudinal studies on T1D listed below, and 2) augment the single dataset to ensure AI-readiness.

ICF Incoperated (Inc.), led by Dr. Ratna Thangudu, performed a multi-step enhancement process for optimal usability and AI-readiness of TEDDY data. The team normalized various data elements, encoded categorical variables, and addressed missing values from a dataset that can affect data analysis—called “missingness” — to prepare an AI-ready data file with multiple applications. Applications included predictive models for identifying risk factors and outcomes related to type 1 diabetes and suitability for time-to-event analyses to understand development of diabetes. ICF Inc. selected the prize to co-author a challenge results publication/abstract with NIDDK for submission to a journal or professional meeting. The link to the publication will be made available once published.

## Summary of Challenge Datasets
To make dataset file sizes more manageable to merge in the NIDDK-CR Analytics Workbench environment hosted by AWS, while enabling Challengers to retain as many features as possible, the NIDDK-CR Support Team performed feature redactions and participant sampling (as described in the table below) prior to making the data available in the Workbench environment. This sampling schema retained the maximum number of participants and features that can be successfully merged in the Workbench environment, while maintaining a justifiable and useful study design for many potential use-cases, including multiple disease outcomes and life-course events. 

| Study | Datasets |  Features *    |Participants| Sampling Schema |Data Dictionary|
|------:|----------|----------------|------------|-----------------|----------------|
|TEDDY|    48     |8,351          | 234,614    |* All (n = 409) disease cases for T1D in TEDDY, identified by MaskID appearing in DIABETES_DIAGNOSIS dataset**
* n = 409 non-disease controls, selected by simple random sample***
|[TEDDY_Data Challenge_Data Dictionary.pdf](https://repository.niddk.nih.gov/media/studies/teddy/TEDDY_Data_Challenge_Data_Dictionary.pdf))|
