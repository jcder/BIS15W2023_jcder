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
  tabyl(common_name, habitat) 
```

```
##                                                common_name Grassland Ocean
##                                             Abert's Towhee         0     0
##                                           Acorn Woodpecker         0     0
##                                        Allen's Hummingbird         0     0
##                                            Altamira Oriole         0     0
##                                            American Avocet         0     0
##                                           American Bittern         0     0
##                                        American Black Duck         0     0
##                                              American Coot         0     0
##                                              American Crow         0     0
##                                            American Dipper         0     0
##                                         American Goldfinch         0     0
##                                           American Kestrel         0     0
##                                     American Oystercatcher         0     1
##                                             American Pipit         1     0
##                                          American Redstart         0     0
##                                             American Robin         0     0
##                             American Three-toed Woodpecker         0     0
##                                      American Tree Sparrow         0     0
##                                     American White Pelican         0     0
##                                            American Wigeon         0     0
##                                          American Woodcock         0     0
##                                           Ancient Murrelet         0     1
##                                                    Anhinga         0     0
##                                         Anna's Hummingbird         0     0
##                                            Aplomado Falcon         1     0
##                               Arctic and Pacific Loon \xa6         0     0
##                                         Arizona Woodpecker         0     0
##                                    Ash-throated Flycatcher         0     0
##                                            Atlantic Puffin         0     1
##                                           Audubon's Oriole         0     0
##                                          Bachman's Sparrow         0     0
##                                            Baird's Sparrow         1     0
##                                                 Bald Eagle         0     0
##                                           Baltimore Oriole         0     0
##                                         Band-tailed Pigeon         0     0
##                                                   Barn Owl         0     0
##                                               Barn Swallow         0     0
##                                                 Barred Owl         0     0
##                                         Barrow's Goldeneye         0     0
##                      Bell's and Sagebrush Sparrow \xa0\xa0         0     0
##                                               Bell's Vireo         0     0
##                                          Belted Kingfisher         0     0
##                                         Bendire's Thrasher         0     0
##                                              Bewick's Wren         0     0
##                                                Black Brant         0     0
##                                            Black Guillemot         0     1
##                                        Black Oystercatcher         0     1
##                                               Black Phoebe         0     0
##                                                 Black Rail         0     0
##                                               Black Scoter         0     0
##                                              Black Skimmer         0     1
##                                            Black Turnstone         0     0
##                                              Black Vulture         0     0
##                                    Black-and-white Warbler         0     0
##                                    Black-backed Woodpecker         0     0
##                                       Black-bellied Plover         0     0
##                               Black-bellied Whistling-Duck         0     0
##                                        Black-billed Magpie         0     0
##                                     Black-capped Chickadee         0     0
##                                  Black-chinned Hummingbird         0     0
##                                      Black-chinned Sparrow         0     0
##                       Black-crested and Tufted Titmouse __         0     0
##                                  Black-crowned Night-Heron         0     0
##                                     Black-footed Albatross         0     1
##                                      Black-headed Grosbeak         0     0
##                                          Black-headed Gull         0     0
##                                     Black-legged Kittiwake         0     1
##                                         Black-necked Stilt         0     0
##                                Black-throated Blue Warbler         0     0
##                                Black-throated Gray Warbler         0     0
##                               Black-throated Green Warbler         0     0
##                                     Black-throated Sparrow         0     0
##  Black, Brown-capped, and Gray-crowned Rosy-Finch \xa4\xa4         0     0
##                                              Blue Grosbeak         0     0
##                                                   Blue Jay         0     0
##                                      Blue-gray Gnatcatcher         0     0
##    Blue-headed, Cassin's, and Plumbeous Vireo \xe0\xe0\xe0         0     0
##                                  Blue-throated Hummingbird         0     0
##                                           Blue-winged Teal         0     0
##              Boat-tailed and Great-tailed Grackle \xa6\xa6         0     0
##                                           Bohemian Waxwing         0     0
##                                           Bonaparte's Gull         0     0
##                                           Boreal Chickadee         0     0
##                                                 Boreal Owl         0     0
##                                         Brandt's Cormorant         0     1
##                                         Brewer's Blackbird         0     0
##                                           Brewer's Sparrow         0     0
##                                           Bridled Titmouse         0     0
##                                   Broad-billed Hummingbird         0     0
##                                   Broad-tailed Hummingbird         0     0
##                                          Broad-winged Hawk         0     0
##                                            Bronzed Cowbird         0     0
##                                                Brown Booby         0     1
##                                              Brown Creeper         0     0
##                                                  Brown Jay         0     0
##                                              Brown Pelican         0     1
##                                             Brown Thrasher         0     0
##                                   Brown-crested Flycatcher         0     0
##                                       Brown-headed Cowbird         0     0
##                                      Brown-headed Nuthatch         0     0
##                                                 Budgerigar         0     0
##                                   Buff-bellied Hummingbird         0     0
##                                                 Bufflehead         0     0
##                                           Bullock's Oriole         0     0
##                                              Burrowing Owl         1     0
##                                                    Bushtit         0     0
##                             Cackling and Canada Goose \xa0         0     0
##                                                Cactus Wren         0     0
##                       California and Canyon/Brown Towhee #         0     0
##                                          California Condor         0     0
##                                     California Gnatcatcher         0     0
##                                            California Gull         0     0
##                                           California Quail         0     0
##                                        California Thrasher         0     0
##                                       Calliope Hummingbird         0     0
##                                                 Canvasback         0     0
##                                                Canyon Wren         0     0
##                                           Cape May Warbler         0     0
##                                         Carolina Chickadee         0     0
##                                              Carolina Wren         0     0
##                                               Caspian Tern         0     0
##                                            Cassin's Auklet         0     1
##                                             Cassin's Finch         0     0
##                                          Cassin's Kingbird         0     0
##                                           Cassin's Sparrow         1     0
##                                               Cattle Egret         0     0
##                                               Cave Swallow         0     0
##                                              Cedar Waxwing         0     0
##                                  Chestnut-backed Chickadee         0     0
##                                 Chestnut-collared Longspur         1     0
##                                     Chestnut-sided Warbler         0     0
##                                           Chihuahuan Raven         0     0
##                                           Chipping Sparrow         0     0
##                                         Chuck-will's-widow         0     0
##                                                     Chukar         0     0
##                                              Cinnamon Teal         0     0
##                                               Clapper Rail         0     0
##                     Clark's and Western Grebe \xa4\xa4\xa4         0     0
##                                         Clark's Nutcracker         0     0
##                                       Clay-colored Sparrow         0     0
##                                        Clay-colored Thrush         0     0
##                                               Common Eider         0     1
##                                           Common Goldeneye         0     0
##                                             Common Grackle         0     0
##                                         Common Ground-Dove         0     0
##                                                Common Loon         0     0
##                                           Common Merganser         0     0
##                                             Common Moorhen         0     0
##                                               Common Murre         0     1
##                                                Common Myna         0     0
##                                            Common Pauraque         0     0
##                                            Common Poorwill         0     0
##                                               Common Raven         0     0
##                                             Common Redpoll         0     0
##                                                Common Tern         0     0
##                                        Common Yellowthroat         0     0
##                                              Cooper's Hawk         0     0
##                                        Costa's Hummingbird         0     0
##                 Couch's and Tropical Kingbird \xa0\xa0\xa0         0     0
##                                           Crested Caracara         0     0
##                                               Crested Myna         0     0
##                                           Crissal Thrasher         0     0
##                                      Curve-billed Thrasher         0     0
##                                            Dark-eyed Junco         0     0
##                                                 Dickcissel         1     0
##                                   Double-crested Cormorant         0     0
##                                                    Dovekie         0     1
##                                           Downy Woodpecker         0     0
##                                                     Dunlin         0     0
##                                           Dusky Flycatcher         0     0
##                                               Dusky Grouse         0     0
##                                    Dusky-capped Flycatcher         0     0
##                                                Eared Grebe         0     0
##                    Eastern and Mexican Whip-poor-will \xe0         0     0
##                               Eastern and Spotted Towhee _         0     0
##               Eastern and Western Screech-Owl \xa6\xa6\xa6         0     0
##                                           Eastern Bluebird         0     0
##                                         Eastern Meadowlark         1     0
##                                             Eastern Phoebe         0     0
##                                         Eastern Wood-Pewee         0     0
##                                               Elegant Tern         0     1
##                                             Elegant Trogon         0     0
##                                              Emperor Goose         0     0
##                                     Eurasian Collared-Dove         0     0
##                                      Eurasian Tree Sparrow         0     0
##                                            Eurasian Wigeon         0     0
##                                          European Starling         0     0
##                                           Evening Grosbeak         0     0
##                                           Ferruginous Hawk         1     0
##                                      Ferruginous Pygmy-Owl         0     0
##                                              Field Sparrow         0     0
##                                                  Fish Crow         0     0
##                                       Five-striped Sparrow         0     0
##                                          Florida Scrub-Jay         0     0
##                                             Forster's Tern         0     0
##                                                Fox Sparrow         0     0
##                                            Franklin's Gull         0     0
##                                     Fulvous Whistling-Duck         0     0
##                                                    Gadwall         0     0
##                                             Gambel's Quail         0     0
##                                            Gila Woodpecker         0     0
##                                             Gilded Flicker         0     0
##                                              Glaucous Gull         0     0
##                                       Glaucous-winged Gull         0     1
##                                                Glossy Ibis         0     0
##                                               Golden Eagle         0     0
##                                     Golden-crowned Kinglet         0     0
##                                     Golden-crowned Sparrow         0     0
##                                  Golden-fronted Woodpecker         0     0
##                                        Grasshopper Sparrow         0     0
##                                               Gray Catbird         0     0
##                                            Gray Flycatcher         0     0
##                                                  Gray Hawk         0     0
##                                                   Gray Jay         0     0
##                                             Gray Partridge         1     0
##                                    Great Black-backed Gull         0     0
##                                           Great Blue Heron         0     0
##                                            Great Cormorant         0     1
##                                   Great Crested Flycatcher         0     0
##                                                Great Egret         0     0
##                                             Great Gray Owl         0     0
##                                           Great Horned Owl         0     0
##                                             Great Kiskadee         0     0
##                                              Greater Pewee         0     0
##                                    Greater Prairie-Chicken         1     0
##                                         Greater Roadrunner         0     0
##                                        Greater Sage-Grouse         0     0
##                                              Greater Scaup         0     0
##                                Greater White-fronted Goose         0     0
##                                         Greater Yellowlegs         0     0
##                                                Green Heron         0     0
##                                                  Green Jay         0     0
##                                           Green Kingfisher         0     0
##                                             Green Parakeet         0     0
##                                        Green-tailed Towhee         0     0
##                                          Green-winged Teal         0     0
##                                          Groove-billed Ani         0     0
##                                           Gull-billed Tern         0     1
##                                                  Gyrfalcon         1     0
##                                           Hairy Woodpecker         0     0
##                                       Hammond's Flycatcher         0     0
##                                             Harlequin Duck         0     0
##                                              Harris's Hawk         0     0
##                                           Harris's Sparrow         0     0
##                                            Heermann's Gull         0     1
##                                          Henslow's Sparrow         1     0
##                                            Hepatic Tanager         0     0
##                                              Hermit Thrush         0     0
##                                             Hermit Warbler         0     0
##                                               Herring Gull         0     0
##                                                  Hill Myna         0     0
##                                              Hoary Redpoll         0     0
##                                           Hooded Merganser         0     0
##                                              Hooded Oriole         0     0
##                                           Hook-billed Kite         0     0
##                                               Horned Grebe         0     0
##                                                Horned Lark         1     0
##                                                House Finch         0     0
##                                              House Sparrow         0     0
##                                                 House Wren         0     0
##                                             Hutton's Vireo         0     0
##                             Iceland and Thayer's Gull \xa4         0     0
##                                                  Inca Dove         0     0
##                                             Indigo Bunting         0     0
##                                Juniper and Oak Titmouse ##         0     0
##                                                   Killdeer         0     0
##                                                 King Eider         0     0
##                                                  King Rail         0     0
##                                   Ladder-backed Woodpecker         0     0
##                                           Lapland Longspur         1     0
##                                               Lark Bunting         1     0
##                                               Lark Sparrow         0     0
##                                              Laughing Gull         0     1
##                                       Lawrence's Goldfinch         0     0
##                                             Lazuli Bunting         0     0
##                                         Le Conte's Sparrow         0     0
##                                        Le Conte's Thrasher         0     0
##                                              Least Bittern         0     0
##                                           Least Flycatcher         0     0
##                                                Least Grebe         0     0
##                                            Least Sandpiper         0     0
##                                                 Least Tern         0     1
##                                   Lesser Black-backed Gull         0     1
##                                           Lesser Goldfinch         0     0
##                                           Lesser Nighthawk         0     0
##                                     Lesser Prairie-Chicken         0     0
##                                               Lesser Scaup         0     0
##                                          Lesser Yellowlegs         0     0
##                                         Lewis's Woodpecker         0     0
##                                                    Limpkin         0     0
##                                          Lincoln's Sparrow         0     0
##                                          Little Blue Heron         0     0
##                                                Little Gull         0     0
##                                          Loggerhead Shrike         0     0
##                                         Long-billed Curlew         1     0
##                                      Long-billed Dowitcher         0     0
##                                       Long-billed Thrasher         0     0
##                                             Long-eared Owl         0     0
##                                           Long-tailed Duck         0     0
##                                      Louisiana Waterthrush         0     0
##                                     MacGillivray's Warbler         0     0
##                                    Magnificent Frigatebird         0     1
##                                    Magnificent Hummingbird         0     0
##                                           Magnolia Warbler         0     0
##                                                    Mallard         0     0
##                                             Marbled Godwit         0     0
##                                           Marbled Murrelet         0     1
##                                                 Marsh Wren         0     0
##                                          McCown's Longspur         1     0
##                                            McKay's Bunting         1     0
##                                                     Merlin         0     0
##                                                   Mew Gull         0     1
##                                          Mexican Chickadee         0     0
##                                                Mexican Jay         0     0
##                                              Monk Parakeet         0     0
##                                            Montezuma Quail         0     0
##                                               Mottled Duck         0     0
##                                          Mountain Bluebird         0     0
##                                         Mountain Chickadee         0     0
##                                            Mountain Plover         1     0
##                                             Mountain Quail         0     0
##                                              Mourning Dove         0     0
##                                                  Mute Swan         0     0
##                                          Nashville Warbler         0     0
##                    Nelson's and Saltmarsh Sparrow \xe0\xe0         0     0
##                                        Neotropic Cormorant         0     0
##                              Northern Beardless-Tyrannulet         0     0
##                                          Northern Bobwhite         0     0
##                                          Northern Cardinal         0     0
##                                           Northern Flicker         0     0
##                                            Northern Fulmar         0     1
##                                            Northern Gannet         0     1
##                                           Northern Goshawk         0     0
##                                           Northern Harrier         0     0
##                                          Northern Hawk Owl         0     0
##                                       Northern Mockingbird         0     0
##                                            Northern Parula         0     0
##                                           Northern Pintail         0     0
##                                         Northern Pygmy-Owl         0     0
##                              Northern Rough-winged Swallow         0     0
##                                      Northern Saw-whet Owl         0     0
##                                          Northern Shoveler         0     0
##                                            Northern Shrike         0     0
##                                       Northern Waterthrush         0     0
##                                          Northwestern Crow         0     0
##                                       Nuttall's Woodpecker         0     0
##                                              Olive Sparrow         0     0
##                                              Olive Warbler         0     0
##                                     Orange-crowned Warbler         0     0
##                                             Orchard Oriole         0     0
##                                                     Osprey         0     0
##                                                   Ovenbird         0     0
##                                      Pacific Golden-Plover         1     0
##                                   Pacific-slope Flycatcher         0     0
##                                            Painted Bunting         0     0
##                                           Painted Redstart         0     0
##                                               Palm Warbler         0     0
##                                           Parasitic Jaeger         0     1
##                                         Pectoral Sandpiper         0     0
##                                          Pelagic Cormorant         0     1
##                                           Peregrine Falcon         0     0
##                                                Phainopepla         0     0
##                                          Pied-billed Grebe         0     0
##                                           Pigeon Guillemot         0     1
##                                        Pileated Woodpecker         0     0
##                                              Pine Grosbeak         0     0
##                                                Pine Siskin         0     0
##                                               Pine Warbler         0     0
##                                                 Pinyon Jay         0     0
##                                              Piping Plover         0     1
##                                           Plain Chachalaca         0     0
##                                            Pomarine Jaeger         0     1
##                                             Prairie Falcon         1     0
##                                            Prairie Warbler         0     0
##                                       Prothonotary Warbler         0     0
##                                               Purple Finch         0     0
##                                           Purple Gallinule         0     0
##                                           Purple Sandpiper         0     0
##                                             Pygmy Nuthatch         0     0
##                                                Pyrrhuloxia         0     0
##                                                  Razorbill         0     1
##                                              Red Crossbill         0     0
##                                                   Red Knot         0     0
##                                     Red-bellied Woodpecker         0     0
##                                          Red-billed Pigeon         0     0
##                                     Red-breasted Merganser         0     0
##                                      Red-breasted Nuthatch         0     0
##                                     Red-breasted Sapsucker         0     0
##                                    Red-cockaded Woodpecker         0     0
##                                         Red-crowned Parrot         0     0
##                                        Red-faced Cormorant         0     1
##                                      Red-headed Woodpecker         0     0
##                                        Red-naped Sapsucker         0     0
##                                           Red-necked Grebe         0     0
##                                       Red-necked Phalarope         0     0
##                                        Red-shouldered Hawk         0     0
##                                            Red-tailed Hawk         0     0
##                                          Red-throated Loon         0     0
##                                       Red-winged Blackbird         0     0
##                                              Reddish Egret         0     0
##                                                    Redhead         0     0
##                                          Rhinoceros Auklet         0     1
##                                           Ring-billed Gull         0     0
##                                           Ring-necked Duck         0     0
##                                       Ring-necked Pheasant         1     0
##                                          Ringed Kingfisher         0     0
##                                             Rock Ptarmigan         1     0
##                                             Rock Sandpiper         0     0
##                                                  Rock Wren         0     0
##                                     Rose-breasted Grosbeak         0     0
##                                       Rose-ringed Parakeet         0     0
##                                          Roseate Spoonbill         0     0
##                                               Ross's Goose         0     0
##                                          Rough-legged Hawk         1     0
##                                                 Royal Tern         0     1
##                                       Ruby-crowned Kinglet         0     0
##                                  Ruby-throated Hummingbird         0     0
##                                                 Ruddy Duck         0     0
##                                          Ruddy Ground-dove         0     0
##                                            Ruddy Turnstone         0     0
##                                              Ruffed Grouse         0     0
##                                         Rufous Hummingbird         0     0
##                                     Rufous-crowned Sparrow         0     0
##                                      Rufous-winged Sparrow         0     0
##                                            Rusty Blackbird         0     0
##                                              Sage Thrasher         0     0
##                                                 Sanderling         0     0
##                                             Sandhill Crane         0     0
##                                              Sandwich Tern         0     1
##                                           Savannah Sparrow         1     0
##                                               Say's Phoebe         0     0
##                                               Scaled Quail         0     0
##                                  Scissor-tailed Flycatcher         0     0
##                                             Scott's Oriole         0     0
##                                            Seaside Sparrow         0     0
##                                                 Sedge Wren         0     0
##                                        Semipalmated Plover         0     0
##                                     Semipalmated Sandpiper         0     0
##                                         Sharp-shinned Hawk         0     0
##                                        Sharp-tailed Grouse         0     0
##                                              Shiny Cowbird         0     0
##                                     Short-billed Dowitcher         0     0
##                                            Short-eared Owl         1     0
##                                          Short-tailed Hawk         0     0
##                                    Short-tailed Shearwater         0     1
##                                                    Skylark         1     0
##                                           Smith's Longspur         1     0
##                                          Smooth-billed Ani         0     0
##                                                 Snail Kite         0     0
##                                               Snow Bunting         1     0
##                                                 Snow Goose         0     0
##                                                Snowy Egret         0     0
##                                                  Snowy Owl         1     0
##                                               Snowy Plover         0     1
##                                         Solitary Sandpiper         0     0
##                                               Song Sparrow         0     0
##                                           Sooty Shearwater         0     1
##                                                       Sora         0     0
##                                       Spot-breasted Oriole         0     0
##                                               Spotted Dove         0     0
##                                                Spotted Owl         0     0
##                                          Spotted Sandpiper         0     0
##                                            Sprague's Pipit         1     0
##                                              Spruce Grouse         0     0
##                                            Steller's Eider         0     0
##                                              Steller's Jay         0     0
##                                            Stilt Sandpiper         0     0
##                                             Summer Tanager         0     0
##                                                Surf Scoter         0     0
##                                                   Surfbird         0     0
##                                            Swainson's Hawk         0     0
##                                              Swamp Sparrow         0     0
##                                          Tennessee Warbler         0     0
##                                      Thick-billed Kingbird         0     0
##                                         Thick-billed Murre         0     1
##                                       Townsend's Solitaire         0     0
##                                         Townsend's Warbler         0     0
##                                               Tree Swallow         0     0
##                                       Tricolored Blackbird         0     0
##                                           Tricolored Heron         0     0
##                                            Tropical Parula         0     0
##                                             Trumpeter Swan         0     0
##                                                Tufted Duck         0     0
##                                                Tundra Swan         0     0
##                                             Turkey Vulture         0     0
##                                              Varied Thrush         0     0
##                                               Vaux's Swift         0     0
##                                                     Verdin         0     0
##                                       Vermilion Flycatcher         0     0
##                                             Vesper Sparrow         1     0
##                                 Violet-crowned Hummingbird         0     0
##                                       Violet-green Swallow         0     0
##                                              Virginia Rail         0     0
##                                          Wandering Tattler         0     0
##                                           Western Bluebird         0     0
##                                               Western Gull         0     1
##                                           Western Kingbird         0     0
##                                         Western Meadowlark         1     0
##                                          Western Sandpiper         0     0
##                                          Western Scrub-Jay         0     0
##                                            Western Tanager         0     0
##                                                   Whimbrel         0     0
##                                      Whiskered Screech-Owl         0     0
##                                                 White Ibis         0     0
##                                    White-breasted Nuthatch         0     0
##                                   White-collared Seedeater         0     0
##                                       White-crowned Pigeon         0     0
##                                      White-crowned Sparrow         0     0
##                                           White-eyed Vireo         0     0
##                                           White-faced Ibis         0     0
##                                    White-headed Woodpecker         0     0
##                                     White-rumped Sandpiper         0     0
##                                          White-tailed Hawk         1     0
##                                          White-tailed Kite         0     0
##                                     White-tailed Ptarmigan         1     0
##                                     White-throated Sparrow         0     0
##                                       White-throated Swift         0     0
##                                          White-tipped Dove         0     0
##                                     White-winged Crossbill         0     0
##                                          White-winged Dove         0     0
##                                      White-winged Parakeet         0     0
##                                        White-winged Scoter         0     0
##                                             Whooping Crane         0     0
##                                                Wild Turkey         0     0
##                                                     Willet         0     0
##                                     Williamson's Sapsucker         0     0
##                                           Willow Ptarmigan         0     0
##                                         Wilson's Phalarope         0     0
##                                            Wilson's Plover         0     1
##                                             Wilson's Snipe         0     0
##                                           Wilson's Warbler         0     0
##                                                Winter Wren         0     0
##                                                  Wood Duck         0     0
##                                                 Wood Stork         0     0
##                                                Wood Thrush         0     0
##                                        Worm-eating Warbler         0     0
##                                                    Wrentit         0     0
##                                                Yellow Rail         0     0
##                                             Yellow Warbler         0     0
##                                   Yellow-bellied Sapsucker         0     0
##                                         Yellow-billed Loon         0     0
##                                       Yellow-billed Magpie         0     0
##                                       Yellow-breasted Chat         0     0
##                                 Yellow-crowned Night-Heron         0     0
##                                          Yellow-eyed Junco         0     0
##                                         Yellow-footed Gull         0     0
##                                    Yellow-headed Blackbird         0     0
##                                      Yellow-rumped Warbler         0     0
##                                      Yellow-throated Vireo         0     0
##                                    Yellow-throated Warbler         0     0
##                                           Zone-tailed Hawk         0     0
##  Shrubland Various Wetland Woodland NA_
##          1       0       0        0   0
##          0       0       0        1   0
##          1       0       0        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       1       0        0   0
##          0       0       1        0   0
##          0       1       0        0   0
##          0       1       0        0   0
##          0       0       0        0   0
##          0       0       0        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       0        1   0
##          1       0       0        0   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       0        0   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       0       0        0   0
##          0       0       1        0   0
##          0       0       0        1   0
##          1       0       0        0   0
##          0       0       0        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       0        0   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       1       0        0   0
##          0       1       0        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          1       0       0        0   0
##          1       0       0        0   0
##          0       0       1        0   0
##          1       0       0        0   0
##          1       0       0        0   0
##          0       0       1        0   0
##          0       0       0        0   0
##          0       0       0        0   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       0        0   0
##          0       0       1        0   0
##          0       1       0        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       0        1   0
##          1       0       0        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       0        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       0        0   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       1       0        0   0
##          0       0       0        1   0
##          1       0       0        0   0
##          0       1       0        0   0
##          1       0       0        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       0        0   0
##          0       1       0        0   0
##          1       0       0        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       1       0        0   0
##          0       0       0        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       0        0   0
##          1       0       0        0   0
##          0       0       0        1   0
##          0       1       0        0   0
##          0       0       0        1   0
##          0       0       0        0   1
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       0       0        0   0
##          0       1       0        0   0
##          0       0       1        0   0
##          1       0       0        0   0
##          1       0       0        0   0
##          0       1       0        0   0
##          1       0       0        0   0
##          0       0       1        0   0
##          1       0       0        0   0
##          1       0       0        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       1       0        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       0        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       0        0   0
##          0       0       1        0   0
##          0       1       0        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       0        0   0
##          1       0       0        0   0
##          1       0       0        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       1       0        0   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       0        1   0
##          1       0       0        0   0
##          0       0       0        1   0
##          0       0       0        0   0
##          0       0       1        0   0
##          0       1       0        0   0
##          1       0       0        0   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       0        0   0
##          0       0       0        0   1
##          1       0       0        0   0
##          1       0       0        0   0
##          0       1       0        0   0
##          1       0       0        0   0
##          0       0       1        0   0
##          1       0       0        0   0
##          0       0       0        1   0
##          1       0       0        0   0
##          0       0       0        1   0
##          1       0       0        0   0
##          0       0       0        0   1
##          1       0       0        0   0
##          1       0       0        0   0
##          0       0       0        1   0
##          0       0       0        0   0
##          0       0       1        0   0
##          0       0       0        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       0        1   0
##          1       0       0        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       0        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       0        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       0        0   1
##          0       0       0        0   1
##          0       0       1        0   0
##          0       1       0        0   0
##          0       0       0        1   0
##          0       0       0        0   0
##          0       0       0        1   0
##          1       0       0        0   0
##          0       0       1        0   0
##          1       0       0        0   0
##          1       0       0        0   0
##          0       0       1        0   0
##          1       0       0        0   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       1        0   0
##          1       0       0        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       0        0   0
##          0       0       1        0   0
##          0       1       0        0   0
##          0       0       0        1   0
##          1       0       0        0   0
##          0       0       0        1   0
##          0       1       0        0   0
##          1       0       0        0   0
##          0       1       0        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       0        0   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       0        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       0        0   0
##          1       0       0        0   0
##          1       0       0        0   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       0        0   1
##          1       0       0        0   0
##          0       0       1        0   0
##          1       0       0        0   0
##          0       0       0        0   0
##          0       0       0        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       1        0   0
##          1       0       0        0   0
##          1       0       0        0   0
##          0       0       0        0   0
##          0       0       0        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       0        0   1
##          1       0       0        0   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       0        0   0
##          0       1       0        0   0
##          0       0       0        0   1
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       1        0   0
##          1       0       0        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       1       0        0   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       0       0        0   0
##          0       0       0        0   0
##          0       1       0        0   0
##          0       0       0        0   0
##          0       1       0        0   0
##          1       0       0        0   0
##          0       0       1        0   0
##          1       0       0        0   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       0        0   0
##          0       0       0        0   0
##          0       1       0        0   0
##          1       0       0        0   0
##          1       0       0        0   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          1       0       0        0   0
##          0       0       1        0   0
##          0       0       1        0   0
##          1       0       0        0   0
##          0       0       0        0   0
##          0       0       1        0   0
##          1       0       0        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       0        1   0
##          1       0       0        0   0
##          0       0       0        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       0        0   0
##          0       0       1        0   0
##          0       0       0        0   0
##          0       0       0        0   0
##          0       0       0        1   0
##          0       0       0        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       0        0   1
##          0       0       0        1   0
##          0       0       1        0   0
##          1       0       0        0   0
##          0       0       0        1   0
##          0       0       0        0   0
##          1       0       0        0   0
##          0       1       0        0   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       0        1   0
##          1       0       0        0   0
##          1       0       0        0   0
##          0       0       0        1   0
##          0       0       0        0   0
##          0       0       0        0   0
##          0       0       0        1   0
##          0       1       0        0   0
##          0       0       0        1   0
##          1       0       0        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       1       0        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          1       0       0        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       0        1   0
##          1       0       0        0   0
##          0       0       0        1   0
##          0       1       0        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       0       0        0   0
##          0       0       0        1   0
##          1       0       0        0   0
##          0       0       0        1   0
##          0       1       0        0   0
##          0       0       0        0   0
##          0       0       1        0   0
##          0       0       0        0   0
##          0       1       0        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       0        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       0        0   0
##          0       0       0        1   0
##          0       0       0        0   0
##          0       0       0        0   0
##          1       0       0        0   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       0        1   0
##          1       0       0        0   0
##          0       0       0        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       0        0   1
##          0       0       0        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       1       0        0   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       0        0   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       0        0   0
##          0       0       1        0   0
##          0       0       0        0   0
##          0       0       1        0   0
##          0       1       0        0   0
##          0       0       0        1   0
##          0       0       0        0   1
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       0        0   0
##          0       0       0        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       0        0   1
##          0       0       1        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          1       0       0        0   0
##          1       0       0        0   0
##          0       0       1        0   0
##          1       0       0        0   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       0        0   0
##          0       0       0        0   0
##          0       1       0        0   0
##          1       0       0        0   0
##          1       0       0        0   0
##          1       0       0        0   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       0        1   0
##          1       0       0        0   0
##          0       1       0        0   0
##          0       0       1        0   0
##          0       0       0        0   0
##          0       0       0        1   0
##          0       0       0        0   0
##          0       0       0        0   0
##          0       0       0        0   0
##          1       0       0        0   0
##          0       0       1        0   0
##          0       0       0        0   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       0        0   0
##          0       0       0        0   0
##          0       0       1        0   0
##          0       1       0        0   0
##          0       0       0        0   0
##          0       0       1        0   0
##          0       0       0        0   1
##          0       0       0        0   1
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       0        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       1       0        0   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       0        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       1       0        0   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       1       0        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          1       0       0        0   0
##          1       0       0        0   0
##          0       0       0        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       0       0        0   0
##          0       0       0        1   0
##          0       0       0        0   0
##          0       0       1        0   0
##          1       0       0        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       0        1   0
##          1       0       0        0   0
##          0       0       0        1   0
##          0       1       0        0   0
##          1       0       0        0   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       0        0   0
##          0       1       0        0   0
##          0       0       0        0   0
##          0       0       0        1   0
##          0       1       0        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       1       0        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       0        1   0
##          1       0       0        0   0
##          0       0       1        0   0
##          0       0       0        0   0
##          0       0       1        0   0
##          1       0       0        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          1       0       0        0   0
##          0       0       1        0   0
##          1       0       0        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       0        1   0
##          1       0       0        0   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       0       1        0   0
##          0       0       1        0   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       0        1   0
##          0       0       0        1   0
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
  filter()
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

Problem 11. (2 points) Consider the results from questions 9 and 10. Are there any species for which their threatened status needs further study? How do you know?


Problem 12. (4 points) Use the `ecosphere` data to perform one exploratory analysis of your choice. The analysis must have a minimum of three lines and two functions. You must also clearly state the question you are attempting to answer.


Please provide the names of the students you have worked with with during the exam:


Please be 100% sure your exam is saved, knitted, and pushed to your github repository. No need to submit a link on canvas, we will find your exam in your repository.
