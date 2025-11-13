Final Project
================
Savanna Hatch
2025-11-13

- [ABSTRACT](#abstract)
- [BACKGROUND](#background)
- [STUDY QUESTION and HYPOTHESIS](#study-question-and-hypothesis)
  - [Questions](#questions)
  - [Hypothesis](#hypothesis)
  - [Prediction](#prediction)
- [METHODS](#methods)
- [DISCUSSION](#discussion)
- [CONCLUSION](#conclusion)
- [REFERENCES](#references)

# ABSTRACT

# BACKGROUND

Asthma is a chronic disease, presented as inflammation in the lungs and
airways, that typically shows symptoms such as coughing, shortness of
breath, tightness in the chest, and wheezing (Sockrider & Fussner,
2020). It also involves remodeling of the airway. This is seen in the
thickening of the airway walls (Elias et. al, 1999). There are many
different triggers that can lead to asthmatic symptoms. These triggers
include things such as strong odors, chemicals, dust, and allergens (Win
and Hussain, 2009). Asthma, along with other allergic diseases has
become more prevalent as urbanization increases (Kudo et. al, 2013). In
many areas that are experiencing rapid urbanization and westernization,
asthma prevalence has also increased (Paciência and Cavaleiro, 2020).
This paper focuses on the impact of higher population densities in
urbanized areas on the asthma prevalence within that population.

``` r
library(ggplot2)

ggplot(asthma_data, aes(x = reorder(state, prevalence), y = prevalence)) +
  geom_col(fill = "steelblue") +
  coord_flip() +
  labs(title = "Asthma Prevalence by U.S. State",
       x = "State",
       y = "Asthma Prevalence (%)") +
  theme_minimal()
```

<img src="Final_Project_Savanna_Hatch_files/figure-gfm/bar plot per state-1.png" style="display: block; margin: auto;" />
This figure shows the Asthma Prevalence percentages per U.S. state.

# STUDY QUESTION and HYPOTHESIS

## Questions

Does the rate of asthma increase in areas with higher population
densities?

## Hypothesis

Areas or states with a higher population density per square mile will
have a higher prevalence of asthma.

## Prediction

Smaller states that have high populations will have a higher prevelance
of asthma, and larger states with low populations will have lower
prevelance of asthma.

# METHODS

``` r
# Load data
df <- read.csv("Comp Bio Data - Population Density.csv")
names(df)
```

    ##  [1] "State"                       "Number.With.Current.Asthma" 
    ##  [3] "Percent.With.Current.Athsma" "SE"                         
    ##  [5] "Population.Per.Square.Mile"  "Population"                 
    ##  [7] "Land.Area..mi.2."            "X"                          
    ##  [9] "X.1"                         "X.2"

``` r
# Load libraries
library(ggplot2)
library(viridis)  # Needed for viridis color scales
```

    ## Loading required package: viridisLite

``` r
# Create plot
ggplot(df, aes(x = Population.Per.Square.Mile, y = Percent.With.Current.Athsma, colour = State)) +
  geom_point() +
 scale_colour_viridis_d() +
  theme_minimal() +
  labs(title = "Population Density vs Asthma Prevalence by State", x = 'Population Per Square Mile', y = 'Percent With Current Asthma') 
```

<img src="Final_Project_Savanna_Hatch_files/figure-gfm/pop density graph-1.png" style="display: block; margin: auto;" />
This plot shows the comparison by state of Population Density (per
square mile) to Asthma Prevalence (Percent With Current Asthma)

``` r
library(ggplot2)
library(maps)
```

    ## 
    ## Attaching package: 'maps'

    ## The following object is masked from 'package:viridis':
    ## 
    ##     unemp

``` r
library(dplyr)

# Map data
states_map <- map_data("state")

# Merge map data with asthma data
map_data <- states_map %>%
  left_join(asthma_data, by = c("region" = "state_lower"))

ggplot(map_data, aes(long, lat, group = group, fill = prevalence)) +
  geom_polygon(color = "gray90", size = 0.3) +  # state borders
  geom_polygon(aes(fill = prevalence), color = "white") +
  coord_fixed(1.3) +
 scale_fill_gradientn(
  name = "Asthma Prevalence (%)",
  colors = c("yellow2", "orange", "red", "red4")
) +
  labs(
    title = "Asthma Prevalence by U.S. State",
  ) +
  theme_void() +
  theme(
    legend.position = "right",
    plot.title = element_text(size = 16, face = "bold"),
    plot.subtitle = element_text(size = 12)
  )
```

<img src="Final_Project_Savanna_Hatch_files/figure-gfm/prevalence by state-1.png" style="display: block; margin: auto;" />
This figure shows the prevalence of asthma by state with higher rates of
asthma shown in darker colors.

``` r
#just regions
# Get U.S. states map data
states_map <- map_data("state")

# Create a dataframe of states and their regions
state_regions <- data.frame(
  state = tolower(state.name),
  region = state.region
)

# Merge map data with region info
map_data <- states_map %>%
  left_join(state_regions, by = c("region" = "state"))

# Plot
ggplot(map_data, aes(x = long, y = lat, group = group, fill = region.y)) +
  geom_polygon(color = "white") +
  coord_fixed(1.3) +
  labs(title = "Four U.S. Census Regions",
       fill = "Region") +
  theme_void()
```

![](Final_Project_Savanna_Hatch_files/figure-gfm/regions%20by%20color-1.png)<!-- -->

``` r
ggplot(asthma_data, aes(x = population, y = prevalence)) +
  geom_point(aes(color=region)) +
  geom_text(aes(label = state_abrv), vjust = -0.5, size = 3)+
  labs(title = "Number of Individuals With Asthma vs. Asthma Prevalence by State",
       x = "Population",
       y = "Asthma Prevalence (%)") +
  theme_minimal()
```

<img src="Final_Project_Savanna_Hatch_files/figure-gfm/scatter plot-1.png" style="display: block; margin: auto;" />

# DISCUSSION

# CONCLUSION

# REFERENCES

1.  ChatGPT. OpenAI, version Jan 2025. Used as a reference for functions
    such as ggplot(), creating the map and troubleshooting error
    messages. Accessed 2025-11-10.

2.  Centers for Disease Control and Prevention. (2024, November 21).
    Most recent asthma data. U.S. Department of Health and Human
    Services.
    <https://www.cdc.gov/asthma-data/about/most-recent-asthma-data.html>

3.  Sockrider, M., & Fussner, L. (2020). What is asthma? \| American
    Journal of Respiratory and Critical Care Medicine.
    <https://www.atsjournals.org/doi/10.1164/rccm.2029P25>

4.  Kudo, M., Ishigatsubo, Y., & Aoki, I. (2013, September 9). Pathology
    of asthma. Frontiers.
    <https://www.frontiersin.org/journals/microbiology/articles/10.3389/fmicb.2013.00263/full>

5.https://pmc.ncbi.nlm.nih.gov/articles/PMC7152189/

6.https://www.jci.org/articles/view/8124?..&..&..&..

7.https://journals.lww.com/pbj/fulltext/2020/02000/Urban_level_environmental_factors_related_to.2.aspx
