ggplot2: Reverse Engineer 1 (Assignment 3)
================
ggSeminar
Fall 2021

## Assignment Code

The following code renders the assignment plot. The actual plot is not
rendered here, because it does not render well in html.

``` r
library(tidyverse)
library(patchwork)

Eur <- population %>% 
  filter(country %in% c("Croatia", "Spain", "France", "Poland", "Hungary", "Sweden")) %>%
  mutate(pop_mil = population/1000000)
  
g1 <- ggplot(Eur, aes(x = year, y = pop_mil)) +
  geom_line(size = 2, aes(color = country)) +
  scale_color_brewer(name = " ",palette = "Dark2") +
  theme_classic(base_size = 15) +
  ylab("Population (millions)") +
  xlab("Year") +
  theme(legend.position = 'bottom') +
  ggtitle("A) Populations on the same scale")

g2 <- ggplot(Eur, aes(x = year, y = pop_mil)) +
  geom_line(size = 2, aes(color = country)) +
  scale_color_brewer(name = " ",palette = "Dark2") +
  theme_classic(base_size = 15) +
  ylab("Population (millions)") +
  xlab("Year") +
  facet_wrap(~country, scales = 'free_y', nrow = 2) +
  theme(legend.position = 'none') +
  theme(strip.background = element_rect(fill="#ffcc00")) +
  theme(strip.text.x = element_text(colour = "#003399", face = "bold")) +
  ggtitle("B) Populations on their own scale")

g1 / g2
```
