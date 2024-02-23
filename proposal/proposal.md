Project proposal
================
Ella and Leo

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
glimpse(new_youth_risk_df)
```

    ## Rows: 188,760
    ## Columns: 12
    ## $ YEAR                    <dbl> 2017, 2017, 2017, 2017, 2017, 2017, 2017, 2017…
    ## $ Topic                   <chr> "Unintentional Injuries and Violence", "Uninte…
    ## $ Subtopic                <chr> "Behaviors that Contribute to Unintentional In…
    ## $ ShortQuestionText       <chr> "Drinking and driving", "Drinking and driving"…
    ## $ Greater_Risk_Data_Value <dbl> 4.2920, 5.4859, 10.3536, 10.4129, 10.3849, 0.6…
    ## $ Lesser_Risk_Data_Value  <dbl> 95.7080, 94.5141, 89.6464, 89.5871, 89.6151, 9…
    ## $ Sample_Size             <dbl> 5138, 2469, 193, 230, 423, 1824, 4451, 137, 34…
    ## $ Sex                     <chr> "Total", "Total", "Total", "Total", "Total", "…
    ## $ Race                    <chr> "Total", "Total", "Total", "Total", "Total", "…
    ## $ Grade                   <chr> "Total", "Total", "Total", "Total", "Total", "…
    ## $ SexualIdentity          <chr> "Total", "Total", "Total", "Total", "Total", "…
    ## $ SexOfSexualContacts     <chr> "Total", "Opposite sex only", "Same sex only",…

``` r
# new_youth_risk_df %>%
#   filter(Subtopic != c("Suicide-Related Behaviors", "Fruit and fruit juices", "Milk", "Obesity and Overweight", "Sleep")) 
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

``` r
new_youth_risk_df %>%
  filter(Subtopic == "Milk") %>%
  group_by(ShortQuestionText, Race) %>%
  summarise(Greater_Risk_Data_Value = round(mean(Greater_Risk_Data_Value, na.rm =TRUE), digits = 0)) %>%
  arrange(desc(Greater_Risk_Data_Value)) %>%
  filter(Race != "Total")
```

    ## `summarise()` has grouped output by 'ShortQuestionText'. You can override using
    ## the `.groups` argument.

    ## # A tibble: 28 × 3
    ## # Groups:   ShortQuestionText [4]
    ##    ShortQuestionText          Race                        Greater_Risk_Data_Va…¹
    ##    <chr>                      <chr>                                        <dbl>
    ##  1 Milk drinking >= 3 glasses Asian                                           93
    ##  2 Milk drinking >= 3 glasses Black or African American                       91
    ##  3 Milk drinking >= 3 glasses Multiple Race                                   91
    ##  4 Milk drinking >= 3 glasses White                                           90
    ##  5 Milk drinking >= 3 glasses Hispanic or Latino                              89
    ##  6 Milk drinking >= 3 glasses American Indian or Alaska …                     88
    ##  7 Milk drinking >= 2 glasses Asian                                           81
    ##  8 Milk drinking >= 2 glasses Multiple Race                                   79
    ##  9 Milk drinking >= 2 glasses Black or African American                       78
    ## 10 Milk drinking >= 2 glasses Hispanic or Latino                              78
    ## # ℹ 18 more rows
    ## # ℹ abbreviated name: ¹​Greater_Risk_Data_Value

## 3. Ethics review

## 4. Data analysis plan

<<<<<<< HEAD
We have discussed the variables we will use in the introduction. At this
point we don’t plan on using additional data. To begin we will first we
will look at the distribution in data of gender, sexual orientation,
race, and grade. This will allow us to visualize data for both the total
answers as well as specific groups within the data set.  
Some ideas we have to visualize data for our specific questions are: To
look at the correlation between tobacco use and physical activity we
will use a scatterplot, because this will allow us to calculate the
correlation coefficient. To look at the initiation of substance use vs
current use we could use ? because ?
=======
What variables will you visualize to explore your research questions? We
will be focusing primarily on gender, race, grade, and physical activity
Will there be any other data that you need to find to help with your
research question? Very preliminary exploratory data analysis, including
some summary statistics and visualizations, along with some explanation
on how they help you learn more about your data. (You can add to these
later as you work on your project.) The data visualization(s) that you
believe will be useful in exploring your question(s). (You can update
these later as you work on your project.)

We would first like to look at distribution in data biased on gender,
race, and grade (see how many males vs. females, etc.). This
visualization will probably be a scatter plot and will tell us if the
demographics represented in the data seem proportional. Then we will
look at the correlation between tobacco use and physical activity and
asthma. We will most likely visualize this in a density plots or a
barplot. Then we will look at tobacco use vs drug/alcohol use. We will
most likely visualize this in a barplot. Then we will look at the
correlation between the initiation of alcohol use compared to current
alcohol use + demographics (gender, race, and grade). We will most
likely visualize this in a density plots or a barplot. Then we will look
at the correlation between the initiation of marijuana use vs current
marijuana use + demographics (gender, race, and grade). We will most
likely visualize this in a density plots or a barplot.
>>>>>>> d75cc983c464e3381b77908b303770c2203166d1
