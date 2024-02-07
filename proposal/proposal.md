Project proposal
================
Team name

``` r
library(tidyverse)
library(broom)
library(readr)
```

## 1. Introduction

## 2. Data

``` r
youth_risk <- read_csv("../data/DASH_-_Youth_Risk_Behavior_Surveillance_System__YRBSS___High_School____Including_Sexual_Orientation_20240207.csv")
```

    ## Rows: 188760 Columns: 41
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (27): LocationAbbr, LocationDesc, DataSource, Topic, Subtopic, ShortQues...
    ## dbl (10): YEAR, Greater_Risk_Data_Value, Greater_Risk_Low_Confidence_Limit, ...
    ## lgl  (4): Greater_Risk_Data_Value_Footnote_Symbol, Greater_Risk_Data_Value_F...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
#View(youth_risk)
```

``` r
new_youth_risk_df <- youth_risk %>% 
  select("Topic", "Subtopic", "ShortQuestionText", "YEAR", "LocationAbbr", "Greater_Risk_Question", "Description", "Lesser_Risk_Question", "Sample_Size", "Sex", "Race", "Grade", "SexualIdentity", "SexOfSexualContacts")
```

## 3. Ethics review

## 4. Data analysis plan
