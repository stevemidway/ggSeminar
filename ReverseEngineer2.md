ggplot2: Reverse Engineer 2 (Assignment 4)
================
ggSeminar
Fall 2021

## Assignment Code

The following code renders the assignment plot. The actual plot is not
rendered here, because it does not render well in html.

``` r
library(tidyverse)
library(Stat2Data)
library(ggsci)
library(RColorBrewer)
library(plyr)
library(patchwork)

df <- gss_cat

p1 <- df %>% 
  filter(marital %in% c("Divorced","Widowed")) %>%
ggplot(aes(y = age, x = as.factor(year))) +
  geom_violin(aes(fill = marital), alpha = 0.5) +
  theme_classic(base_size = 13) +
  scale_fill_jco() +
  scale_color_jco() +
  labs(x = "Year",
       y = "Age",
       fill = "Status",
       color = "Status",
       title = "Divorced and Widowed Ages") +
  theme(legend.position = "top") +
stat_summary(aes(group=marital, color = marital), 
               size = 2, fun=mean, geom="line")

p2 <- df %>% 
  filter(relig %in% c("Protestant","Hinduism",
                           "Buddhism","Jewish","Catholic")) %>%
  ggplot(aes(y = tvhours, x = relig, fill = relig)) +
  geom_jitter(alpha = 0.15) +
  geom_boxplot(color = "black",outlier.shape = NA, alpha = 0.6) +
  scale_fill_jama() +
  labs(x = "Religion",
       y = "TV Hours",
       fill = "Religion",
       color = "Religion",
       title = "Daily TV by Religion") +
  theme_classic(base_size = 13) +
  theme(legend.position = "none")

df2 <- df %>%
  filter(partyid %in% c("Strong republican","Independent",
                        "Strong democrat") & race %in% c("White"))

df2$partyid <- revalue(df2$partyid, c("Strong republican" = "Republican",
                       "Independent" = "Independent",
                       "Strong democrat" = "Democrat"))
p3 <- ggplot(df2) +
  geom_bar(mapping = aes(x = year, fill = partyid),
           position = "fill", color = "darkgray") +
  scale_fill_brewer(palette = "RdBu") +
  labs(x = "Year",
       y = "",
       fill = "Party",
       title = "Party Affiliation of White People") +
  scale_y_continuous(labels = scales::percent) +
  theme_classic(base_size = 13) +
  theme(legend.position = "top")

(p1 / p3) | p2
```
