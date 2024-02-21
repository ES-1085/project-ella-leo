# data

We started with the "Youth Risk Behavior Surveillance System," collected by the CDC. It has 188,760 rows and  41 columns. In order to work with it more efficiently we paired it down and created a new data frame called "new_youth_risk_df" it has 188,760 rows and 12 total columns.

## name of data file

- `Year`: Year the data is from (either 2015 or 2017)
- `Subtopic`: Grouping of short question text by topic  
- `ShortQuestionText`: shorted text of full question
- `Greater_Risk_Data_Value`: percentage of respondes who answered yes to short question text 
- `Lesser_Risk_Data_Value`: percentage of respondes who answered no to short question text 
- `Sample_Size`: sample size for the question
- `Sex`: Gender of respondent
- `Race`: Race of respondent
- `Grade`: Grade of respondent
- `SexualIndentity`: Sexual orientation of respondents
- `SexOfSexualContacts`: sex of respondents sexual contacts
