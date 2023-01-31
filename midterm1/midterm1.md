---
title: "Midterm 1"
author: "Jonathan Der"
date: "2023-01-31"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your code should be organized, clean, and run free from errors. Remember, you must remove the `#` for any included code chunks to run. Be sure to add your name to the author header above.  

After the first 50 minutes, please upload your code (5 points). During the second 50 minutes, you may get help from each other- but no copy/paste. Upload the last version at the end of this time, but be sure to indicate it as final. If you finish early, you are free to leave.

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean! Use the tidyverse and pipes unless otherwise indicated. This exam is worth a total of 35 points. 

Please load the following libraries.

```r
library(tidyverse)
```

```
## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.2 ──
## ✔ ggplot2 3.4.0      ✔ purrr   1.0.0 
## ✔ tibble  3.1.8      ✔ dplyr   1.0.10
## ✔ tidyr   1.2.1      ✔ stringr 1.5.0 
## ✔ readr   2.1.3      ✔ forcats 0.5.2 
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
```

```r
library(janitor)
```

```
## 
## Attaching package: 'janitor'
## 
## The following objects are masked from 'package:stats':
## 
##     chisq.test, fisher.test
```

In the midterm 1 folder there is a second folder called `data`. Inside the `data` folder, there is a .csv file called `ecs21351-sup-0003-SupplementS1.csv`. These data are from Soykan, C. U., J. Sauer, J. G. Schuetz, G. S. LeBaron, K. Dale, and G. M. Langham. 2016. Population trends for North American winter birds based on hierarchical models. Ecosphere 7(5):e01351. 10.1002/ecs2.1351.  

Please load these data as a new object called `ecosphere`. In this step, I am providing the code to load the data, clean the variable names, and remove a footer that the authors used as part of the original publication.

```r
ecosphere <- read_csv("data/ecs21351-sup-0003-SupplementS1.csv", skip=2) %>% 
  clean_names() %>%
  slice(1:(n() - 18)) # this removes the footer
```

Problem 1. (1 point) Let's start with some data exploration. What are the variable names?

```r
names(ecosphere)
```

```
##  [1] "order"                       "family"                     
##  [3] "common_name"                 "scientific_name"            
##  [5] "diet"                        "life_expectancy"            
##  [7] "habitat"                     "urban_affiliate"            
##  [9] "migratory_strategy"          "log10_mass"                 
## [11] "mean_eggs_per_clutch"        "mean_age_at_sexual_maturity"
## [13] "population_size"             "winter_range_area"          
## [15] "range_in_cbc"                "strata"                     
## [17] "circles"                     "feeder_bird"                
## [19] "median_trend"                "lower_95_percent_ci"        
## [21] "upper_95_percent_ci"
```

Problem 2. (1 point) Use the function of your choice to summarize the data.

```r
summary(ecosphere)
```

```
##     order              family          common_name        scientific_name   
##  Length:551         Length:551         Length:551         Length:551        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##      diet           life_expectancy      habitat          urban_affiliate   
##  Length:551         Length:551         Length:551         Length:551        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##  migratory_strategy   log10_mass    mean_eggs_per_clutch
##  Length:551         Min.   :0.480   Min.   : 1.000      
##  Class :character   1st Qu.:1.365   1st Qu.: 3.000      
##  Mode  :character   Median :1.890   Median : 4.000      
##                     Mean   :2.012   Mean   : 4.527      
##                     3rd Qu.:2.685   3rd Qu.: 5.000      
##                     Max.   :4.040   Max.   :17.000      
##                                                         
##  mean_age_at_sexual_maturity population_size     winter_range_area  
##  Min.   : 0.200              Min.   :    15000   Min.   :       11  
##  1st Qu.: 1.000              1st Qu.:  1100000   1st Qu.:   819357  
##  Median : 1.000              Median :  4900000   Median :  2189639  
##  Mean   : 1.592              Mean   : 18446745   Mean   :  5051047  
##  3rd Qu.: 2.000              3rd Qu.: 18000000   3rd Qu.:  6778598  
##  Max.   :12.500              Max.   :300000000   Max.   :185968946  
##                              NA's   :273                            
##   range_in_cbc        strata          circles       feeder_bird       
##  Min.   :  0.00   Min.   :  1.00   Min.   :   2.0   Length:551        
##  1st Qu.:  2.35   1st Qu.:  3.00   1st Qu.:  46.5   Class :character  
##  Median : 30.30   Median : 11.00   Median : 184.0   Mode  :character  
##  Mean   : 38.48   Mean   : 32.43   Mean   : 558.9                     
##  3rd Qu.: 72.95   3rd Qu.: 42.00   3rd Qu.: 661.0                     
##  Max.   :100.00   Max.   :159.00   Max.   :3202.0                     
##                                                                       
##   median_trend   lower_95_percent_ci upper_95_percent_ci
##  Min.   :0.739   Min.   :0.5780      Min.   :    0.798  
##  1st Qu.:0.993   1st Qu.:0.9675      1st Qu.:    1.011  
##  Median :1.009   Median :0.9930      Median :    1.027  
##  Mean   :1.016   Mean   :0.9857      Mean   :   33.709  
##  3rd Qu.:1.030   3rd Qu.:1.0140      3rd Qu.:    1.055  
##  Max.   :1.396   Max.   :1.3080      Max.   :18000.000  
## 
```

Problem 3. (2 points) How many distinct orders of birds are represented in the data?

```r
ecosphere %>%
  summarize(distinct_orders = n_distinct(order))
```

```
## # A tibble: 1 × 1
##   distinct_orders
##             <int>
## 1              19
```

**Problem 4. (2 points) Which habitat has the highest diversity (number of species) in the data?**

```r
ecosphere %>%
  group_by(habitat) %>%
  tally()
```

```
## # A tibble: 7 × 2
##   habitat       n
##   <chr>     <int>
## 1 Grassland    36
## 2 Ocean        44
## 3 Shrubland    82
## 4 Various      45
## 5 Wetland     153
## 6 Woodland    177
## 7 <NA>         14
```

Run the code below to learn about the `slice` function. Look specifically at the examples (at the bottom) for `slice_max()` and `slice_min()`. If you are still unsure, try looking up examples online (https://rpubs.com/techanswers88/dplyr-slice). Use this new function to answer question 5 below.

```r
?slice_max
```

Problem 5. (4 points) Using the `slice_max()` or `slice_min()` function described above which species has the largest and smallest winter range?

```r
large_winter_range <- ecosphere %>%
dplyr::slice_max(winter_range_area)
large_winter_range
```

```
## # A tibble: 1 × 21
##   order     family commo…¹ scien…² diet  life_…³ habitat urban…⁴ migra…⁵ log10…⁶
##   <chr>     <chr>  <chr>   <chr>   <chr> <chr>   <chr>   <chr>   <chr>     <dbl>
## 1 Procella… Proce… Sooty … Puffin… Vert… Long    Ocean   No      Long        2.9
## # … with 11 more variables: mean_eggs_per_clutch <dbl>,
## #   mean_age_at_sexual_maturity <dbl>, population_size <dbl>,
## #   winter_range_area <dbl>, range_in_cbc <dbl>, strata <dbl>, circles <dbl>,
## #   feeder_bird <chr>, median_trend <dbl>, lower_95_percent_ci <dbl>,
## #   upper_95_percent_ci <dbl>, and abbreviated variable names ¹​common_name,
## #   ²​scientific_name, ³​life_expectancy, ⁴​urban_affiliate, ⁵​migratory_strategy,
## #   ⁶​log10_mass
```


```r
small_winter_range <- ecosphere %>%
  dplyr::slice_min(winter_range_area)
small_winter_range
```

```
## # A tibble: 1 × 21
##   order     family commo…¹ scien…² diet  life_…³ habitat urban…⁴ migra…⁵ log10…⁶
##   <chr>     <chr>  <chr>   <chr>   <chr> <chr>   <chr>   <chr>   <chr>     <dbl>
## 1 Passerif… Alaud… Skylark Alauda… Seed  Short   Grassl… No      Reside…    1.57
## # … with 11 more variables: mean_eggs_per_clutch <dbl>,
## #   mean_age_at_sexual_maturity <dbl>, population_size <dbl>,
## #   winter_range_area <dbl>, range_in_cbc <dbl>, strata <dbl>, circles <dbl>,
## #   feeder_bird <chr>, median_trend <dbl>, lower_95_percent_ci <dbl>,
## #   upper_95_percent_ci <dbl>, and abbreviated variable names ¹​common_name,
## #   ²​scientific_name, ³​life_expectancy, ⁴​urban_affiliate, ⁵​migratory_strategy,
## #   ⁶​log10_mass
```

Problem 6. (2 points) The family Anatidae includes ducks, geese, and swans. Make a new object `ducks` that only includes species in the family Anatidae. Restrict this new dataframe to include all variables except order and family.

```r
duck <- ecosphere %>%
filter(family == "Anatidae")%>%
select(-order)
duck
```

```
## # A tibble: 44 × 20
##    family  commo…¹ scien…² diet  life_…³ habitat urban…⁴ migra…⁵ log10…⁶ mean_…⁷
##    <chr>   <chr>   <chr>   <chr> <chr>   <chr>   <chr>   <chr>     <dbl>   <dbl>
##  1 Anatid… "Ameri… Anas r… Vege… Long    Wetland No      Short      3.09     9  
##  2 Anatid… "Ameri… Anas a… Vege… Middle  Wetland No      Short      2.88     7.5
##  3 Anatid… "Barro… Buceph… Inve… Middle  Wetland No      Modera…    2.96    10.5
##  4 Anatid… "Black… Branta… Vege… Long    Wetland No      Modera…    3.11     3.5
##  5 Anatid… "Black… Melani… Inve… Middle  Wetland No      Modera…    3.02     9.5
##  6 Anatid… "Black… Dendro… Vege… Short   Wetland No      Withdr…    2.88    13.5
##  7 Anatid… "Blue-… Anas d… Vege… Middle  Wetland No      Modera…    2.56    10  
##  8 Anatid… "Buffl… Buceph… Inve… Middle  Wetland No      Short      2.6      8.5
##  9 Anatid… "Cackl… Branta… Vege… Middle  Wetland Yes     Short      3.45     5  
## 10 Anatid… "Canva… Aythya… Vege… Middle  Wetland No      Short      3.08     8  
## # … with 34 more rows, 10 more variables: mean_age_at_sexual_maturity <dbl>,
## #   population_size <dbl>, winter_range_area <dbl>, range_in_cbc <dbl>,
## #   strata <dbl>, circles <dbl>, feeder_bird <chr>, median_trend <dbl>,
## #   lower_95_percent_ci <dbl>, upper_95_percent_ci <dbl>, and abbreviated
## #   variable names ¹​common_name, ²​scientific_name, ³​life_expectancy,
## #   ⁴​urban_affiliate, ⁵​migratory_strategy, ⁶​log10_mass, ⁷​mean_eggs_per_clutch
```

Problem 7. (2 points) We might assume that all ducks live in wetland habitat. Is this true for the ducks in these data? If there are exceptions, list the species below.
**common eider**

```r
duck %>%
  tabyl(common_name, habitat)
```

```
##                     common_name Ocean Wetland
##             American Black Duck     0       1
##                 American Wigeon     0       1
##              Barrow's Goldeneye     0       1
##                     Black Brant     0       1
##                    Black Scoter     0       1
##    Black-bellied Whistling-Duck     0       1
##                Blue-winged Teal     0       1
##                      Bufflehead     0       1
##  Cackling and Canada Goose \xa0     0       1
##                      Canvasback     0       1
##                   Cinnamon Teal     0       1
##                    Common Eider     1       0
##                Common Goldeneye     0       1
##                Common Merganser     0       1
##                   Emperor Goose     0       1
##                 Eurasian Wigeon     0       1
##          Fulvous Whistling-Duck     0       1
##                         Gadwall     0       1
##                   Greater Scaup     0       1
##     Greater White-fronted Goose     0       1
##               Green-winged Teal     0       1
##                  Harlequin Duck     0       1
##                Hooded Merganser     0       1
##                      King Eider     0       1
##                    Lesser Scaup     0       1
##                Long-tailed Duck     0       1
##                         Mallard     0       1
##                    Mottled Duck     0       1
##                       Mute Swan     0       1
##                Northern Pintail     0       1
##               Northern Shoveler     0       1
##          Red-breasted Merganser     0       1
##                         Redhead     0       1
##                Ring-necked Duck     0       1
##                    Ross's Goose     0       1
##                      Ruddy Duck     0       1
##                      Snow Goose     0       1
##                 Steller's Eider     0       1
##                     Surf Scoter     0       1
##                  Trumpeter Swan     0       1
##                     Tufted Duck     0       1
##                     Tundra Swan     0       1
##             White-winged Scoter     0       1
##                       Wood Duck     0       1
```

Problem 8. (4 points) In ducks, how is mean body mass associated with migratory strategy? Do the ducks that migrate long distances have high or low average body mass?

```r
duck %>%
  group_by(migratory_strategy) %>%
   summarise(mean_body_mass = mean(log10_mass))
```

```
## # A tibble: 5 × 2
##   migratory_strategy mean_body_mass
##   <chr>                       <dbl>
## 1 Long                         2.87
## 2 Moderate                     3.11
## 3 Resident                     4.03
## 4 Short                        2.98
## 5 Withdrawal                   2.92
```

Problem 9. (2 points) Accipitridae is the family that includes eagles, hawks, kites, and osprey. First, make a new object `eagles` that only includes species in the family Accipitridae. Next, restrict these data to only include the variables common_name, scientific_name, and population_size.

```r
eagles <- ecosphere %>%
filter(family == "Accipitridae")%>%
select(common_name, scientific_name, population_size)
eagles
```

```
## # A tibble: 20 × 3
##    common_name         scientific_name          population_size
##    <chr>               <chr>                              <dbl>
##  1 Bald Eagle          Haliaeetus leucocephalus              NA
##  2 Broad-winged Hawk   Buteo platypterus                1700000
##  3 Cooper's Hawk       Accipiter cooperii                700000
##  4 Ferruginous Hawk    Buteo regalis                      80000
##  5 Golden Eagle        Aquila chrysaetos                 130000
##  6 Gray Hawk           Buteo nitidus                         NA
##  7 Harris's Hawk       Parabuteo unicinctus               50000
##  8 Hook-billed Kite    Chondrohierax uncinatus               NA
##  9 Northern Goshawk    Accipiter gentilis                200000
## 10 Northern Harrier    Circus cyaneus                    700000
## 11 Red-shouldered Hawk Buteo lineatus                   1100000
## 12 Red-tailed Hawk     Buteo jamaicensis                2000000
## 13 Rough-legged Hawk   Buteo lagopus                     300000
## 14 Sharp-shinned Hawk  Accipiter striatus                500000
## 15 Short-tailed Hawk   Buteo brachyurus                      NA
## 16 Snail Kite          Rostrhamus sociabilis                 NA
## 17 Swainson's Hawk     Buteo swainsoni                   540000
## 18 White-tailed Hawk   Buteo albicaudatus                    NA
## 19 White-tailed Kite   Elanus leucurus                       NA
## 20 Zone-tailed Hawk    Buteo albonotatus                     NA
```

Problem 10. (4 points) In the eagles data, any species with a population size less than 250,000 individuals is threatened. Make a new column `conservation_status` that shows whether or not a species is threatened.

```r
names(eagles)
```

```
## [1] "common_name"     "scientific_name" "population_size"
```


```r
eagles %>%
mutate(conservation_status = ifelse(population_size < 250000, "threatened", population_size)) %>%
arrange(population_size)
```

```
## # A tibble: 20 × 4
##    common_name         scientific_name          population_size conservation_s…¹
##    <chr>               <chr>                              <dbl> <chr>           
##  1 Harris's Hawk       Parabuteo unicinctus               50000 threatened      
##  2 Ferruginous Hawk    Buteo regalis                      80000 threatened      
##  3 Golden Eagle        Aquila chrysaetos                 130000 threatened      
##  4 Northern Goshawk    Accipiter gentilis                200000 threatened      
##  5 Rough-legged Hawk   Buteo lagopus                     300000 3e+05           
##  6 Sharp-shinned Hawk  Accipiter striatus                500000 5e+05           
##  7 Swainson's Hawk     Buteo swainsoni                   540000 540000          
##  8 Cooper's Hawk       Accipiter cooperii                700000 7e+05           
##  9 Northern Harrier    Circus cyaneus                    700000 7e+05           
## 10 Red-shouldered Hawk Buteo lineatus                   1100000 1100000         
## 11 Broad-winged Hawk   Buteo platypterus                1700000 1700000         
## 12 Red-tailed Hawk     Buteo jamaicensis                2000000 2e+06           
## 13 Bald Eagle          Haliaeetus leucocephalus              NA <NA>            
## 14 Gray Hawk           Buteo nitidus                         NA <NA>            
## 15 Hook-billed Kite    Chondrohierax uncinatus               NA <NA>            
## 16 Short-tailed Hawk   Buteo brachyurus                      NA <NA>            
## 17 Snail Kite          Rostrhamus sociabilis                 NA <NA>            
## 18 White-tailed Hawk   Buteo albicaudatus                    NA <NA>            
## 19 White-tailed Kite   Elanus leucurus                       NA <NA>            
## 20 Zone-tailed Hawk    Buteo albonotatus                     NA <NA>            
## # … with abbreviated variable name ¹​conservation_status
```

Problem 11. (2 points) Consider the results from questions 9 and 10. Are there any species for which their threatened status needs further study? How do you know?

```r
eagles %>%
  select(common_name,population_size) %>%
  arrange(population_size)
```

```
## # A tibble: 20 × 2
##    common_name         population_size
##    <chr>                         <dbl>
##  1 Harris's Hawk                 50000
##  2 Ferruginous Hawk              80000
##  3 Golden Eagle                 130000
##  4 Northern Goshawk             200000
##  5 Rough-legged Hawk            300000
##  6 Sharp-shinned Hawk           500000
##  7 Swainson's Hawk              540000
##  8 Cooper's Hawk                700000
##  9 Northern Harrier             700000
## 10 Red-shouldered Hawk         1100000
## 11 Broad-winged Hawk           1700000
## 12 Red-tailed Hawk             2000000
## 13 Bald Eagle                       NA
## 14 Gray Hawk                        NA
## 15 Hook-billed Kite                 NA
## 16 Short-tailed Hawk                NA
## 17 Snail Kite                       NA
## 18 White-tailed Hawk                NA
## 19 White-tailed Kite                NA
## 20 Zone-tailed Hawk                 NA
```

```r
#View(eagles)
```
**Bald eagles, Gray Hawk, Hook-billed Kite , Short-tailed Hawk, Snail Kite, White-tailed Hawk, 	
White-tailed Kite , and Zone-tailed Hawk because their population size is denoted by NA**

Problem 12. (4 points) Use the `ecosphere` data to perform one exploratory analysis of your choice. The analysis must have a minimum of three lines and two functions. You must also clearly state the question you are attempting to answer.
**What species lays the most eggs per clutch?**

```r
eagles_eggs <- ecosphere %>%
filter(family == "Accipitridae")%>%
select(common_name, mean_eggs_per_clutch, population_size)
eagles_eggs
```

```
## # A tibble: 20 × 3
##    common_name         mean_eggs_per_clutch population_size
##    <chr>                              <dbl>           <dbl>
##  1 Bald Eagle                           2                NA
##  2 Broad-winged Hawk                    2.5         1700000
##  3 Cooper's Hawk                        4.5          700000
##  4 Ferruginous Hawk                     3             80000
##  5 Golden Eagle                         2.5          130000
##  6 Gray Hawk                            2                NA
##  7 Harris's Hawk                        9             50000
##  8 Hook-billed Kite                     2.5              NA
##  9 Northern Goshawk                     3            200000
## 10 Northern Harrier                     4            700000
## 11 Red-shouldered Hawk                  3.5         1100000
## 12 Red-tailed Hawk                      3           2000000
## 13 Rough-legged Hawk                    4.5          300000
## 14 Sharp-shinned Hawk                   4.5          500000
## 15 Short-tailed Hawk                    2                NA
## 16 Snail Kite                           3                NA
## 17 Swainson's Hawk                      3            540000
## 18 White-tailed Hawk                    2.5              NA
## 19 White-tailed Kite                    4.5              NA
## 20 Zone-tailed Hawk                     1.5              NA
```

```r
eagles_eggs %>%
  arrange(mean_eggs_per_clutch)
```

```
## # A tibble: 20 × 3
##    common_name         mean_eggs_per_clutch population_size
##    <chr>                              <dbl>           <dbl>
##  1 Zone-tailed Hawk                     1.5              NA
##  2 Bald Eagle                           2                NA
##  3 Gray Hawk                            2                NA
##  4 Short-tailed Hawk                    2                NA
##  5 Broad-winged Hawk                    2.5         1700000
##  6 Golden Eagle                         2.5          130000
##  7 Hook-billed Kite                     2.5              NA
##  8 White-tailed Hawk                    2.5              NA
##  9 Ferruginous Hawk                     3             80000
## 10 Northern Goshawk                     3            200000
## 11 Red-tailed Hawk                      3           2000000
## 12 Snail Kite                           3                NA
## 13 Swainson's Hawk                      3            540000
## 14 Red-shouldered Hawk                  3.5         1100000
## 15 Northern Harrier                     4            700000
## 16 Cooper's Hawk                        4.5          700000
## 17 Rough-legged Hawk                    4.5          300000
## 18 Sharp-shinned Hawk                   4.5          500000
## 19 White-tailed Kite                    4.5              NA
## 20 Harris's Hawk                        9             50000
```
**body weight based on vore**

```r
eagles_vore <- ecosphere %>%
filter(family == "Accipitridae")%>%
select(common_name, diet, log10_mass)
eagles_vore
```

```
## # A tibble: 20 × 3
##    common_name         diet          log10_mass
##    <chr>               <chr>              <dbl>
##  1 Bald Eagle          Vertebrates         3.67
##  2 Broad-winged Hawk   Vertebrates         2.66
##  3 Cooper's Hawk       Vertebrates         2.63
##  4 Ferruginous Hawk    Vertebrates         3.17
##  5 Golden Eagle        Vertebrates         3.63
##  6 Gray Hawk           Vertebrates         2.63
##  7 Harris's Hawk       Vertebrates         2.93
##  8 Hook-billed Kite    Invertebrates       2.49
##  9 Northern Goshawk    Vertebrates         2.94
## 10 Northern Harrier    Vertebrates         2.59
## 11 Red-shouldered Hawk Invertebrates       2.78
## 12 Red-tailed Hawk     Vertebrates         3.04
## 13 Rough-legged Hawk   Vertebrates         2.98
## 14 Sharp-shinned Hawk  Vertebrates         2.12
## 15 Short-tailed Hawk   Vertebrates         2.71
## 16 Snail Kite          Invertebrates       2.57
## 17 Swainson's Hawk     Vertebrates         2.98
## 18 White-tailed Hawk   Vertebrates         3.01
## 19 White-tailed Kite   Vertebrates         2.54
## 20 Zone-tailed Hawk    Vertebrates         2.88
```



Please provide the names of the students you have worked with with during the exam:

```r
#Jacob Yousif
```

Please be 100% sure your exam is saved, knitted, and pushed to your github repository. No need to submit a link on canvas, we will find your exam in your repository.
