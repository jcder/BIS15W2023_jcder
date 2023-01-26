---
title: "Lab 3 Homework"
author: "JOnathan Der"
date: "2023-01-26"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---

## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the tidyverse

```r
library(tidyverse)
```

## Mammals Sleep
1. For this assignment, we are going to use built-in data on mammal sleep patterns. From which publication are these data taken from? Since the data are built-in you can use the help function in R.

```r
library(readr)
readr::read_csv("mammals_sleep_allison_cicchetti_1976.csv")
```

```
## Rows: 62 Columns: 11
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (1): species
## dbl (10): body weight in kg, brain weight in g, slow wave ("nondreaming") sl...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## # A tibble: 62 × 11
##    species       body …¹ brain…² slow …³ parad…⁴ total…⁵ maxim…⁶ gesta…⁷ preda…⁸
##    <chr>           <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>
##  1 African elep… 6.65e+3  5712    -999    -999       3.3    38.6     645       3
##  2 African gian… 1   e+0     6.6     6.3     2       8.3     4.5      42       3
##  3 Arctic Fox    3.38e+0    44.5  -999    -999      12.5    14        60       1
##  4 Arctic groun… 9.2 e-1     5.7  -999    -999      16.5  -999        25       5
##  5 Asian elepha… 2.55e+3  4603       2.1     1.8     3.9    69       624       3
##  6 Baboon        1.06e+1   180.      9.1     0.7     9.8    27       180       4
##  7 Big brown bat 2.3 e-2     0.3    15.8     3.9    19.7    19        35       1
##  8 Brazilian ta… 1.6 e+2   169       5.2     1       6.2    30.4     392       4
##  9 Cat           3.3 e+0    25.6    10.9     3.6    14.5    28        63       1
## 10 Chimpanzee    5.22e+1   440       8.3     1.4     9.7    50       230       1
## # … with 52 more rows, 2 more variables: `sleep exposure index (1-5)` <dbl>,
## #   `overall danger index (1-5)` <dbl>, and abbreviated variable names
## #   ¹​`body weight in kg`, ²​`brain weight in g`,
## #   ³​`slow wave ("nondreaming") sleep (hrs/day)`,
## #   ⁴​`paradoxical ("dreaming") sleep (hrs/day)`,
## #   ⁵​`total sleep (hrs/day)  (sum of slow wave and paradoxical sleep)`,
## #   ⁶​`maximum life span (years)`, ⁷​`gestation time (days)`, …
```

2. Store these data into a new data frame `sleep`.

```r
#sleep <-readr::read_csv("mammals_sleep_allison_cicchetti_1976.csv")
sleep <- msleep
```

3. What are the dimensions of this data frame (variables and observations)? How do you know? Please show the *code* that you used to determine this below. 
**There are 62 rows and 11 columns based on the number given by dim(msleep) and nrow(sleep)**

```r
dim(sleep)
```

```
## [1] 83 11
```

```r
nrow(sleep)
```

```
## [1] 83
```

**4. Are there any NAs in the data? How did you determine this? Please show your code.**
**yes**


```r
is.na(sleep)
```

```
##        name genus  vore order conservation sleep_total sleep_rem sleep_cycle
##  [1,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
##  [2,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE        TRUE
##  [3,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
##  [4,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
##  [5,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
##  [6,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE       FALSE
##  [7,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
##  [8,] FALSE FALSE  TRUE FALSE         TRUE       FALSE      TRUE        TRUE
##  [9,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [10,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [11,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [12,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [13,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [14,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [15,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [16,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE        TRUE
## [17,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [18,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [19,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [20,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [21,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [22,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [23,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [24,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [25,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [26,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [27,] FALSE FALSE FALSE FALSE         TRUE       FALSE      TRUE        TRUE
## [28,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [29,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE       FALSE
## [30,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [31,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [32,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [33,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [34,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE       FALSE
## [35,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [36,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [37,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [38,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE       FALSE
## [39,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [40,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [41,] FALSE FALSE FALSE FALSE         TRUE       FALSE      TRUE        TRUE
## [42,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [43,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE       FALSE
## [44,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [45,] FALSE FALSE FALSE FALSE         TRUE       FALSE      TRUE        TRUE
## [46,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [47,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [48,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [49,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [50,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE       FALSE
## [51,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [52,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [53,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [54,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE       FALSE
## [55,] FALSE FALSE  TRUE FALSE        FALSE       FALSE     FALSE        TRUE
## [56,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [57,] FALSE FALSE  TRUE FALSE         TRUE       FALSE      TRUE        TRUE
## [58,] FALSE FALSE  TRUE FALSE         TRUE       FALSE     FALSE        TRUE
## [59,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [60,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [61,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE        TRUE
## [62,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [63,] FALSE FALSE  TRUE FALSE        FALSE       FALSE     FALSE        TRUE
## [64,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [65,] FALSE FALSE FALSE FALSE         TRUE       FALSE      TRUE        TRUE
## [66,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE        TRUE
## [67,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [68,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE       FALSE
## [69,] FALSE FALSE  TRUE FALSE         TRUE       FALSE     FALSE        TRUE
## [70,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [71,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [72,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [73,] FALSE FALSE  TRUE FALSE         TRUE       FALSE     FALSE       FALSE
## [74,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [75,] FALSE FALSE FALSE FALSE         TRUE       FALSE      TRUE        TRUE
## [76,] FALSE FALSE FALSE FALSE         TRUE       FALSE      TRUE        TRUE
## [77,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [78,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE        TRUE
## [79,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE       FALSE
## [80,] FALSE FALSE FALSE FALSE         TRUE       FALSE      TRUE        TRUE
## [81,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE        TRUE
## [82,] FALSE FALSE FALSE FALSE         TRUE       FALSE      TRUE        TRUE
## [83,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE       FALSE
##       awake brainwt bodywt
##  [1,] FALSE    TRUE  FALSE
##  [2,] FALSE   FALSE  FALSE
##  [3,] FALSE    TRUE  FALSE
##  [4,] FALSE   FALSE  FALSE
##  [5,] FALSE   FALSE  FALSE
##  [6,] FALSE    TRUE  FALSE
##  [7,] FALSE    TRUE  FALSE
##  [8,] FALSE    TRUE  FALSE
##  [9,] FALSE   FALSE  FALSE
## [10,] FALSE   FALSE  FALSE
## [11,] FALSE   FALSE  FALSE
## [12,] FALSE   FALSE  FALSE
## [13,] FALSE    TRUE  FALSE
## [14,] FALSE   FALSE  FALSE
## [15,] FALSE   FALSE  FALSE
## [16,] FALSE   FALSE  FALSE
## [17,] FALSE   FALSE  FALSE
## [18,] FALSE   FALSE  FALSE
## [19,] FALSE   FALSE  FALSE
## [20,] FALSE   FALSE  FALSE
## [21,] FALSE   FALSE  FALSE
## [22,] FALSE   FALSE  FALSE
## [23,] FALSE   FALSE  FALSE
## [24,] FALSE   FALSE  FALSE
## [25,] FALSE   FALSE  FALSE
## [26,] FALSE   FALSE  FALSE
## [27,] FALSE    TRUE  FALSE
## [28,] FALSE   FALSE  FALSE
## [29,] FALSE   FALSE  FALSE
## [30,] FALSE    TRUE  FALSE
## [31,] FALSE    TRUE  FALSE
## [32,] FALSE   FALSE  FALSE
## [33,] FALSE   FALSE  FALSE
## [34,] FALSE   FALSE  FALSE
## [35,] FALSE    TRUE  FALSE
## [36,] FALSE   FALSE  FALSE
## [37,] FALSE    TRUE  FALSE
## [38,] FALSE   FALSE  FALSE
## [39,] FALSE    TRUE  FALSE
## [40,] FALSE   FALSE  FALSE
## [41,] FALSE    TRUE  FALSE
## [42,] FALSE   FALSE  FALSE
## [43,] FALSE   FALSE  FALSE
## [44,] FALSE    TRUE  FALSE
## [45,] FALSE   FALSE  FALSE
## [46,] FALSE    TRUE  FALSE
## [47,] FALSE    TRUE  FALSE
## [48,] FALSE   FALSE  FALSE
## [49,] FALSE   FALSE  FALSE
## [50,] FALSE   FALSE  FALSE
## [51,] FALSE    TRUE  FALSE
## [52,] FALSE   FALSE  FALSE
## [53,] FALSE    TRUE  FALSE
## [54,] FALSE   FALSE  FALSE
## [55,] FALSE   FALSE  FALSE
## [56,] FALSE    TRUE  FALSE
## [57,] FALSE    TRUE  FALSE
## [58,] FALSE   FALSE  FALSE
## [59,] FALSE    TRUE  FALSE
## [60,] FALSE    TRUE  FALSE
## [61,] FALSE    TRUE  FALSE
## [62,] FALSE   FALSE  FALSE
## [63,] FALSE   FALSE  FALSE
## [64,] FALSE   FALSE  FALSE
## [65,] FALSE    TRUE  FALSE
## [66,] FALSE   FALSE  FALSE
## [67,] FALSE   FALSE  FALSE
## [68,] FALSE   FALSE  FALSE
## [69,] FALSE   FALSE  FALSE
## [70,] FALSE   FALSE  FALSE
## [71,] FALSE   FALSE  FALSE
## [72,] FALSE    TRUE  FALSE
## [73,] FALSE   FALSE  FALSE
## [74,] FALSE   FALSE  FALSE
## [75,] FALSE   FALSE  FALSE
## [76,] FALSE    TRUE  FALSE
## [77,] FALSE   FALSE  FALSE
## [78,] FALSE   FALSE  FALSE
## [79,] FALSE   FALSE  FALSE
## [80,] FALSE    TRUE  FALSE
## [81,] FALSE   FALSE  FALSE
## [82,] FALSE   FALSE  FALSE
## [83,] FALSE   FALSE  FALSE
```

5. Show a list of the column names is this data frame.

```r
names(sleep)
```

```
##  [1] "name"         "genus"        "vore"         "order"        "conservation"
##  [6] "sleep_total"  "sleep_rem"    "sleep_cycle"  "awake"        "brainwt"     
## [11] "bodywt"
```

**6. How many herbivores are represented in the data?  **

**32 herbavores**

```r
table(sleep$`vore`)
```

```
## 
##   carni   herbi insecti    omni 
##      19      32       5      20
```

**7. We are interested in two groups; small and large mammals. Let's define small as less than or equal to 1kg body weight and large as greater than or equal to 200kg body weight. Make two new dataframes (large and small) based on these parameters.**


```r
small <- filter(sleep, `bodywt` <= 1 )
small
```

```
## # A tibble: 36 × 11
##    name  genus vore  order conse…¹ sleep…² sleep…³ sleep…⁴ awake  brainwt bodywt
##    <chr> <chr> <chr> <chr> <chr>     <dbl>   <dbl>   <dbl> <dbl>    <dbl>  <dbl>
##  1 Owl … Aotus omni  Prim… <NA>       17       1.8  NA       7    0.0155   0.48 
##  2 Grea… Blar… omni  Sori… lc         14.9     2.3   0.133   9.1  0.00029  0.019
##  3 Vesp… Calo… <NA>  Rode… <NA>        7      NA    NA      17   NA        0.045
##  4 Guin… Cavis herbi Rode… domest…     9.4     0.8   0.217  14.6  0.0055   0.728
##  5 Chin… Chin… herbi Rode… domest…    12.5     1.5   0.117  11.5  0.0064   0.42 
##  6 Star… Cond… omni  Sori… lc         10.3     2.2  NA      13.7  0.001    0.06 
##  7 Afri… Cric… omni  Rode… <NA>        8.3     2    NA      15.7  0.0066   1    
##  8 Less… Cryp… omni  Sori… lc          9.1     1.4   0.15   14.9  0.00014  0.005
##  9 Big … Epte… inse… Chir… lc         19.7     3.9   0.117   4.3  0.0003   0.023
## 10 Euro… Erin… omni  Erin… lc         10.1     3.5   0.283  13.9  0.0035   0.77 
## # … with 26 more rows, and abbreviated variable names ¹​conservation,
## #   ²​sleep_total, ³​sleep_rem, ⁴​sleep_cycle
```


```r
large <- filter(sleep, `bodywt` >= 200)
large
```

```
## # A tibble: 7 × 11
##   name    genus vore  order conse…¹ sleep…² sleep…³ sleep…⁴ awake brainwt bodywt
##   <chr>   <chr> <chr> <chr> <chr>     <dbl>   <dbl>   <dbl> <dbl>   <dbl>  <dbl>
## 1 Cow     Bos   herbi Arti… domest…     4       0.7   0.667  20     0.423   600 
## 2 Asian … Elep… herbi Prob… en          3.9    NA    NA      20.1   4.60   2547 
## 3 Horse   Equus herbi Peri… domest…     2.9     0.6   1      21.1   0.655   521 
## 4 Giraffe Gira… herbi Arti… cd          1.9     0.4  NA      22.1  NA       900.
## 5 Pilot … Glob… carni Ceta… cd          2.7     0.1  NA      21.4  NA       800 
## 6 Africa… Loxo… herbi Prob… vu          3.3    NA    NA      20.7   5.71   6654 
## 7 Brazil… Tapi… herbi Peri… vu          4.4     1     0.9    19.6   0.169   208.
## # … with abbreviated variable names ¹​conservation, ²​sleep_total, ³​sleep_rem,
## #   ⁴​sleep_cycle
```

8. What is the mean weight for both the small and large mammals?

```r
mean(large$`bodywt`, na.rm = TRUE)
```

```
## [1] 1747.071
```


```r
small_mean <- small$`bodywt`
mean(small_mean, na.rm = TRUE)
```

```
## [1] 0.2596667
```

9. Using a similar approach as above, do large or small animals sleep longer on average?  
**Small anaimals sleep longer**

```r
mean(small$`sleep_total`)
```

```
## [1] 12.65833
```


```r
mean(large$`sleep_total`)
```

```
## [1] 3.3
```

10. Which animal is the sleepiest among the entire dataframe?
**Little Brown BAt**

```r
sleep_ordered <- select(sleep, "name" ,"sleep_total")
sort(sleep_ordered$sleep_total, decreasing = TRUE)
```

```
##  [1] 19.9 19.7 19.4 18.1 18.0 17.4 17.0 16.6 15.9 15.8 15.8 15.6 14.9 14.9 14.6
## [16] 14.5 14.4 14.4 14.3 14.2 13.8 13.7 13.5 13.0 12.8 12.8 12.5 12.5 12.5 12.5
## [31] 12.1 11.5 11.3 11.1 11.0 11.0 10.9 10.6 10.4 10.3 10.3 10.1 10.1 10.1 10.0
## [46]  9.8  9.8  9.7  9.6  9.5  9.4  9.4  9.1  9.1  8.9  8.7  8.7  8.6  8.4  8.4
## [61]  8.3  8.0  7.7  7.0  6.3  6.3  6.2  5.6  5.4  5.3  5.3  5.2  4.4  4.0  3.9
## [76]  3.8  3.5  3.3  3.1  3.0  2.9  2.7  1.9
```


```r
filter(sleep, sleep_total == 19.9)
```

```
## # A tibble: 1 × 11
##   name    genus vore  order conse…¹ sleep…² sleep…³ sleep…⁴ awake brainwt bodywt
##   <chr>   <chr> <chr> <chr> <chr>     <dbl>   <dbl>   <dbl> <dbl>   <dbl>  <dbl>
## 1 Little… Myot… inse… Chir… <NA>       19.9       2     0.2   4.1 0.00025   0.01
## # … with abbreviated variable names ¹​conservation, ²​sleep_total, ³​sleep_rem,
## #   ⁴​sleep_cycle
```

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
