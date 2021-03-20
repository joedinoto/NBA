---
title: "NBA Data"
author: "Joe DiNoto"
date: "3/20/2021"
output: 
  html_document: 
    keep_md: yes
---



First, load packages.


```r
library(tidyverse)
library(ggplot2)
library(dplyr)
library(tidytuesdayR)
library(scales)
```

Second, grab the data.


```r
player_data <- read.csv("player_data.xls")
players <- read.csv("Players.xls")
seasons_stats <- read.csv("Seasons_Stats.csv")
```

Grab the player name, year, and team. 

```r
nba <- seasons_stats %>%
  select(Year, Player, Tm) %>%
  filter(!is.na(Year)) #remove NAs 
```

What are the range of years? 


```r
summary(nba$Year)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##    1950    1981    1996    1993    2007    2017
```

Which player stayed with a team the longest? (1950-2017)

```r
nba %>%
  count(Player,Tm, sort=TRUE) %>%
  head(20)
```

```
##                  Player  Tm  n
## 1           Kobe Bryant LAL 20
## 2         Dirk Nowitzki DAL 19
## 3        John Stockton* UTA 19
## 4            Tim Duncan SAS 19
## 5          Karl Malone* UTA 18
## 6        Reggie Miller* IND 18
## 7      Hakeem Olajuwon* HOU 17
## 8        John Havlicek* BOS 16
## 9           Tony Parker SAS 16
## 10        Manu Ginobili SAS 15
## 11       Patrick Ewing* NYK 15
## 12          Paul Pierce BOS 15
## 13      David Robinson* SAS 14
## 14       Dolph Schayes* SYR 14
## 15          Jerry West* LAL 14
## 16          Joe Dumars* DET 14
## 17 Kareem Abdul-Jabbar* LAL 14
## 18        Kevin Garnett MIN 14
## 19       Robert Parish* BOS 14
## 20        Udonis Haslem MIA 14
```

What is the distribution of how long a player stays with a team?


```r
nba %>%
  count(Player,Tm, sort=TRUE) %>%
  ggplot(aes(Player,n)) +
  geom_line()
```

![](NBA_files/figure-html/unnamed-chunk-6-1.png)<!-- -->


