Project proposal
================
Team name

``` r
library(tidyverse)
library(broom)
library(readr)
```

## 1. Introduction

For our project we are working with a data set called “Youth Risk
Behavior Surveillance System,” collected by the CDC. This data set looks
at demographics, environments, and behaviors in teenagers from 9-12th
grade across the country. According to the CDC the intent of this data
is to “determine how often unhealthy behaviors occur,assess whether
unhealthy behaviors increase, decrease, or stay the same over
time,provide data at the national, state, territorial and freely
associated state, tribal, and local levels, and provide data comparing
different groups of adolescents. The data is collected through surveys
given to students at both public and private high schools across the US.

Due to the size of the data we are looking at data from Maine only in
the years 2015 and 2017. The behaviors (variables) we will be looking at
specifically are:

\[1\] “Behaviors that Contribute to Unintentional Injuries” \[2\]
“Behaviors that Contribute to Violence”  
\[4\] “Cigarette Use”  
\[5\] “Other Tobacco Use”  
\[6\] “Alcohol Use”  
\[7\] “Other Drug Use”  
\[8\] “Sexual Behaviors”  
\[9\] “Physical Activity”

There are several questions we are interested in exploring through this
data:

1.  What is the relationship between tobacco use and physical activity?
2.  Are certain demographics of students more likely to engage in risky
    behaviors?
3.  How does age of initiation of use of a specific substance correlate
    with current use of that substance?
4.  Are students who use tobacco more likely to use alcohol or
    marijuana?

Add– why did we choose to look at this data set?

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

I’m not actually sure how to do this section.

## 4. Data analysis plan

Distribution in data gender, race, grade(see how many males vs. females,
etc.) then: then: Look at the correlation between tobacco use and
physical activity + asthma Tobacco use vs drug/alcohol use Initiation of
alcohol use compared to current alcohol use + demographics Initiation of
marijuana use vs current marijuana use + demographics
