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
# View(youth_risk)
```

``` r
new_youth_risk_df <- youth_risk %>% 
  select("YEAR", "Topic", "Subtopic", "ShortQuestionText", "Greater_Risk_Data_Value", "Lesser_Risk_Data_Value", "Sample_Size", "Sex", "Race", "Grade", "SexualIdentity", "SexOfSexualContacts")
```

``` r
new_youth_risk_df %>%
  filter(Subtopic == "Milk") %>%
  group_by(ShortQuestionText) %>%
  mutate(Greater_Risk_Data_Value = round(Greater_Risk_Data_Value, digits = 0)) %>%
  arrange(desc(Greater_Risk_Data_Value))
```

    ## # A tibble: 10,560 × 12
    ## # Groups:   ShortQuestionText [4]
    ##     YEAR Topic             Subtopic ShortQuestionText     Greater_Risk_Data_Va…¹
    ##    <dbl> <chr>             <chr>    <chr>                                  <dbl>
    ##  1  2017 Dietary Behaviors Milk     Milk drinking >= 2 g…                    100
    ##  2  2017 Dietary Behaviors Milk     Milk drinking >= 3 g…                    100
    ##  3  2017 Dietary Behaviors Milk     Milk drinking >= 3 g…                    100
    ##  4  2017 Dietary Behaviors Milk     Milk drinking >= 3 g…                    100
    ##  5  2017 Dietary Behaviors Milk     Milk drinking >= 3 g…                    100
    ##  6  2015 Dietary Behaviors Milk     Milk drinking >= 3 g…                    100
    ##  7  2015 Dietary Behaviors Milk     Milk drinking >= 3 g…                    100
    ##  8  2015 Dietary Behaviors Milk     Milk drinking >= 3 g…                    100
    ##  9  2017 Dietary Behaviors Milk     Milk drinking >= 3 g…                     99
    ## 10  2017 Dietary Behaviors Milk     Milk drinking >= 2 g…                     98
    ## # ℹ 10,550 more rows
    ## # ℹ abbreviated name: ¹​Greater_Risk_Data_Value
    ## # ℹ 7 more variables: Lesser_Risk_Data_Value <dbl>, Sample_Size <dbl>,
    ## #   Sex <chr>, Race <chr>, Grade <chr>, SexualIdentity <chr>,
    ## #   SexOfSexualContacts <chr>

## 3. Ethics review

## 4. Data analysis plan


