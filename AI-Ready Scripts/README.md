## TEDDY AI-Ready Scripts - Instructions

**In this project, there are three scripts:** qualityChecks_Team7.ipynb, data_processing_TEDDY.ipynb and TEDDY_data_dictionary.ipynb

The script **qualityChecks_Team7.ipynb** is used to QA the 48 TEDDY study files using the TEDDY_data_dictionary_v1.2.json (A Json format file transformed from TEDDY_Data_Challenge_Data_Dictionary.pdf)

The script **data_processing_TEDDY.ipynb** is used to preprocess 48 TEDDY data sets to generate the raw merged data set file "Raw-Dataset.csv", the AI-ready dataset file "TEDDY_data_final.csv". 

**The preprocesses contain:**

**1. Merging multiple datasets:**

1.1 Produce the raw dataset: Files are read in and columns with <5% completeness are filtered out. 
      For files with multiple records per case, each record was placed in separate "observation_#" columns, corresponding to timepoint if one was available.
      For the TEST_RESULTS study, the dataframe was split by test-type before adding the additional observation_columns specific to that test type.

1.2 Studies/columns without observation designations were left as-is.
      Studies with observations corresponding to timepoints binned, using either the median number of bins or a max of 3. The mean of numeric columns were taken, or the mode (first/earliest value in case of a tie) for
      categorical/string columns.
      Studies with observations but no timepoint were collapsed to one observation/record using either the mean or mode.

**2. Processing texts:**

2.1 Time values with any formatting errors were corrected.

2.2 Codes were kept in either uppercase or lowercase except for language codes, which were converted to lowercase according to ISO 639 recommendations, and country codes, which were converted to uppercase according to ISO 3166 recommendations.

2.3 For text contains values other than codes or time, the processing included removing contractions, white spaces, and punctuation, converting the text to lowercase, and checking all words longer than four characters for  misspellings using the pyspellchecker module. We reviewed the list of identified misspellings, and any false hits (such as medication names) were added to the "do not change" list. For true misspellings that were not 
corrected properly by pyspellchecker, we assigned a proper correction and stored them in a dictionary for the final misspelling corrections. 

**3. Processing missing values:**
   
3.1 For the numeric missing values,the features with more than 50% completeness were kept for imputation. The Multiple Imputation by Chained Equation algorithm were appied to performe multiple regression over the sample data and take averages of them.

3.2 For the categorical missing values, we replaced them using “not reported”. 

**4. Processing categorical features:** One-Hot Encoding was performed for the categorical features. 

The script **TEDDY_data_dictionary.ipynb** is used to generate the data dictionary file "TEDDY_data_dictionary.xlsx" which indicates the column information in the the AI-ready dataset file.
