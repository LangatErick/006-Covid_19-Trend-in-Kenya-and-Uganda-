# 006-Covid_19-Trend-in-Kenya-and-Uganda-
As the world is in the midst of a once-in-a-century pandemic phase, it would be natural for Data Science students to look closely into the data being generated daily.
![image](https://github.com/LangatErick/Learning_Labs-10-Covid_19-Trend-in-Kenya-and-Uganda-/assets/124883947/396cb598-a859-4360-808c-80ef165c107f)

## covid-19 Trend

```{r warning=FALSE, message=FALSE}
library(tidyverse)
library(modeltime)
# library(tidymodels)
library(rmarkdown)
library(dplyr)
library(parsnip)
library(rsample)
library(timetk)
library(rlang)
# ls("package:rlang")
```

```{r warning=FALSE, message=FALSE}
df <- read_csv("WHO-COVID-19-global-data.csv") %>% 
              as_tibble()
str(df)
head(df)


```

Filter

```{r}
names(df)
```

```{r warning=FALSE, message=FALSE}
#filter Kenya and Uganda
df <- df %>% dplyr::filter(Country %in% c('Kenya', 'Uganda') &
                      Date_reported>="2021-01-12"
                    ) %>% 
                      mutate(Date=Date_reported) %>% 
               select(Country, Date,
                  New_cases, Cumulative_cases,
                 Cumulative_deaths)
# nrow(df)
```

```{r warning=FALSE, message=FALSE}
df %>%
    group_by(Country) %>%
    plot_time_series(Date, New_cases,
                   #.facet_ncol  = 2,     # 2-column layout
                  #.interactive = FALSE,
               #.facet_vars     = c(symbol, year), # add groups/facets
                .color_var      = Country,  # color by year
               .facet_ncol     = 4,
              .facet_scales   = "free",
             .facet_collapse = TRUE,# combine group strip text into 1 line
            .interactive    = FALSE,
            .title = 'Trend of Daily Reported Cases Of Covid-19 in Kenya and Uganda'
                     )
```
![image](https://github.com/LangatErick/Learning_Labs-10-Covid_19-Trend-in-Kenya-and-Uganda-/assets/124883947/ab390bcc-a0af-4076-a3b1-8c2040ab57b4)

```{r warning=FALSE, message=FALSE}
theme_set(theme_test())
df %>%
    group_by(Country) %>%
    plot_time_series(Date, Cumulative_cases,
                   #.facet_ncol  = 2,     # 2-column layout
                  #.interactive = FALSE,
               #.facet_vars     = c(symbol, year), # add groups/facets
                .color_var      = Country,  # color by year
               .facet_ncol     = 4,
              .facet_scales   = "free",
             .facet_collapse = TRUE,# combine group strip text into 1 line
            .interactive    = FALSE,
            .line_color = "#2c3e50",
            .line_size = 0.5,
            .title = "Trend of Covid-19 Cumulative Cases in Kenya and Uganda",
            .smooth_color = "#3366FF",
                     )
```
![image](https://github.com/LangatErick/Learning_Labs-10-Covid_19-Trend-in-Kenya-and-Uganda-/assets/124883947/703dc72d-3d8e-474d-8531-01e6060e7b72)

```{r}
df %>%
    group_by(Country) %>%
    plot_time_series(Date, Cumulative_deaths,
                   #.facet_ncol  = 2,     # 2-column layout
                  #.interactive = FALSE,
               #.facet_vars     = c(symbol, year), # add groups/facets
                .color_var      = Country,  # color by year
               .facet_ncol     = 4,
              .facet_scales   = "free",
             .facet_collapse = TRUE,# combine group strip text into 1 line
            .interactive    = FALSE,
            .line_color = "#2c3e50",
            .line_size = 0.5,
            .title = "Trend of Covid-19 Cumulative Deaths in Kenya and Uganda",
            .smooth_color = "#3366FF",
                     )
```
![image](https://github.com/LangatErick/Learning_Labs-10-Covid_19-Trend-in-Kenya-and-Uganda-/assets/124883947/94b3a9f9-da9f-4157-a379-66e8d852e3ad)
