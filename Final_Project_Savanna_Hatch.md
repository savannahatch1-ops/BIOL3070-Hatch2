Final Project
================
Savanna Hatch
2025-12-06

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

Asthma is a chronic disease that results in many symptoms such as
coughing, shortness of breath, and wheezing (Sockrider & Fussner, 2020).
Asthma has become more prevalent in areas that are experiencing rapid
urbanization (Paciência and Cavaleiro, 2020). This paper focuses on the
whether or not areas with higher population densities in urbanized areas
are a predictor for higher asthma levels. This was done by examining
recent asthma data collected by the CDC and the current population
levels in both the individual states and the U.S. census regions. ANOVA
tests were run to test the relations between population density by state
and by region with the associated asthma prevalence rates. The test done
for asthma prevalence and U.S region showed significant correlation
between higher asthma rates and the Northeast region with a p-value of
0.0192. The other ANOVA tests showed no significance and were
inconclusive. It was found that there was a significant correlation
between the Northeast region and asthma levels, and a boxplot of
population density within the regions showed a possible correlation with
higher population density.

# BACKGROUND

Asthma is a chronic disease, presented as inflammation in the lungs and
airways, that typically shows symptoms such as coughing, shortness of
breath, tightness in the chest, and wheezing (Sockrider & Fussner,
2020). It also involves remodeling of the airway. This is seen in the
thickening of the airway walls (Elias et. al, 1999). There are many
different triggers that can lead to asthmatic symptoms. These triggers
include things such as strong odors, chemicals, dust, and allergens (Win
and Hussain, 2009). Asthma, along with other allergic diseases has
become more prevalent as urbanization has increased (Kudo et. al, 2013).
In many areas that are experiencing rapid urbanization and
westernization, asthma prevalence has also increased (Paciência and
Cavaleiro, 2020). This paper focuses on the impact of higher population
densities in urbanized areas on the asthma prevalence within that
population.

# STUDY QUESTION and HYPOTHESIS

## Questions

Does the rate of asthma increase in areas with higher population
densities?

## Hypothesis

Areas or states with a higher population density per square mile will
have a higher prevalence of asthma.

## Prediction

Smaller states that have high populations will have a higher prevalance
of asthma, and larger states with low populations will have lower
prevalance of asthma.

# METHODS

Recent asthma data was collected from the Center for Disease Control
(CDC) as well as the current population number and population density
for each state. Data was organized both by state and by region. Regions
consisted of West, South, Northeast, and North Central United States
(Figure 1). Asthma Prevalence was compared between states using a bar
graph (Figure 2) and a map visualization (Figure 3), and then between
states in relation to the overall state population (Figure 4). Asthma
Prevalence was also compared between state by Population Density per
Square Mile (Figure 5), and then it was compared between region (Figure
6). An ANOVA test was performed to determine whether there was a
significant relation between individual state Population Density and
Asthma Prevalence. A second ANOVA test was run to determine if there was
a significant relation between U.S. Region and Asthma Prevalence. A
Tukey pairwise comparison was performed to show which, if any, region
had a significant difference from the others in the Region and Asthma
Prevalence relationship. A third ANOVA test was performed to determine
if there was a significant relation between the average population
density per region and Asthma Prevalence.

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

Figure 1: The U.S. divided into four regions: West, South, Northeast,
and North Central.

![](Final_Project_Savanna_Hatch_files/figure-gfm/bar%20graph-1.png)<!-- -->

Figure 2: This figure shows the Asthma Prevalence percentages per U.S.
state.

``` r
library(ggplot2)
library(maps)
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
Figure 3: This figure shows the prevalence of asthma by state with
higher rates of asthma shown in darker colors.

``` r
ggplot(asthma_data, aes(x = population, y = prevalence)) +
  geom_point(aes(color=region)) +
  geom_text(aes(label = state_abrv), vjust = -0.5, size = 3)+
  labs(title = "Population vs. Asthma Prevalence by State",
       x = "Population",
       y = "Asthma Prevalence (%)",
       color = "Regions") +
  theme_minimal()
```

<img src="Final_Project_Savanna_Hatch_files/figure-gfm/scatter plot-1.png" style="display: block; margin: auto;" />
Figure 4: This figure shows the comparison by state of Population to
Asthma Prevalence

``` r
# Load libraries
library(ggplot2)

# Create plot
ggplot(asthma_data, aes(x = pop_density_sqmile, y = prevalence, colour = region)) +
  geom_point() +
  theme_minimal() +
  labs(title = "Population Density vs Asthma Prevalence by State", x = 'Population Per Square Mile', y = 'Percent With Current Asthma', colour = "Region") 
```

<img src="Final_Project_Savanna_Hatch_files/figure-gfm/pop density graph-1.png" style="display: block; margin: auto;" />
Figure 5: This plot shows the comparison by state of Population Density
(per square mile) to Asthma Prevalence (Percent With Current Asthma)

``` r
library(ggplot2)

ggplot(asthma_data, aes(x = region, y = prevalence, fill= region)) +
  geom_boxplot() +
  labs(title = "Asthma Prevalence by U.S. Region",
       x = "Region",
       y = "Asthma Prevalence (%)",
       fill = "Region") +
  theme_minimal()
```

<img src="Final_Project_Savanna_Hatch_files/figure-gfm/box plot-1.png" style="display: block; margin: auto;" />
Figure 6: This figure shows the comparison of Asthma Prevalence between
regions.

``` r
library(ggplot2)

ggplot(asthma_data, aes(x = region, y = pop_density_sqmile, fill= region)) +
  geom_boxplot() +
  labs(title = "Population Density by U.S. Region",
       x = "Region",
       y = "Population Density (square mile)",
       fill = "Region") +
  theme_minimal()
```

<img src="Final_Project_Savanna_Hatch_files/figure-gfm/box plot population vs region-1.png" style="display: block; margin: auto;" />
Figure 7: This figure shows the comparison of population density between
regions.

``` r
# load necessary libraries

library("car")
library("lme4")

# create a linear model for population density per square mile and asthma prevalence by state

m1 <- lm(prevalence ~ pop_density_sqmile, data=asthma_data)

# perform statistical test

Anova(m1)
summary(m1)
```

``` r
# load necessary libraries

library(emmeans)

# create a linear model for US region and asthma prevalence

m2 <- lm(prevalence ~ region, data=asthma_data) 

# perform statistical test 

Anova(m2) 
summary(m2)



# pairwise comparison

pairs(emmeans(m2, "region"))
```

``` r
# create a linear model for average population density per region and asthma prevalence

r1 <- lm(prevalence ~ density, data=region_data)

# perform statistical test

Anova(r1)
summary(r1)
```

# DISCUSSION

When comparing Asthma Prevalence between U.S. regions, it was found that
the Northeast region had a significant difference in Asthma rates. An
ANOVA test resulted in a p-value of 0.0192 showing a slight statistical
significance in at least one of the regions. This means that the Asthma
Prevalence percentage can be predicted using population density in the
significant regions. A Tukey pairwise comparison showed that all regions
were significantly lower than the Northeast region with p-values of
0.00419 for the South, 0.00558 for the North Central, and 0.02671 for
the West region. When comparing Asthma Prevalence between U.S. states,
it was found that there was no statistical significance in Asthma
Prevalence in relation to Population Density per Square Mile. This ANOVA
test resulted in a p-value of 0.6668. There was no evidence to show that
asthma rates increase with higher population densities. When comparing
Asthma Prevalence between U.S. regions, it was found that there was no
statistical significance in Asthma Prevalence in relation to the average
population density per region. This ANOVA test resulted in a p-value of
0.129. However, this test only included four variables and may be
unreliable due to the lack of testable factors.

# CONCLUSION

Asthma is a chronic respiratory disease that is not predictable
according to population or population density. It is somewhat
predictable according to U.S. region. The Northeast region of the U.S.
is a significant predictor of Asthma Prevalence in the states included
in that region. It is possible that future studies with increased data
may show more significance in other U.S. regions that could lead to
predictors other than the Northeast region of Asthma Prevalence rates.

# REFERENCES

1.  Asthma and Allergy Foundation of America. (n.d.). Air pollution and
    asthma. Asthma & Allergy Foundation of America.
    <https://aafa.org/asthma/asthma-triggers-causes/air-pollution-smog-asthma/>

2.  Centers for Disease Control and Prevention. (2024, November 21).
    Most recent asthma data. U.S. Department of Health and Human
    Services.
    <https://www.cdc.gov/asthma-data/about/most-recent-asthma-data.html>

3.  ChatGPT. OpenAI, version Jan 2025. Used as a reference for functions
    such as ggplot(), creating the map and troubleshooting error
    messages. Accessed 2025-11-10.

4.  Elias, J. A., Zhu, Z., Chupp, G., & Homer, R. J. (1999, October 15).
    Airway remodeling in asthma. The Journal of Clinical Investigation.
    <https://www.jci.org/articles/view/8124>?..

5.  Kudo, M., Ishigatsubo, Y., & Aoki, I. (2013, September 9). Pathology
    of asthma. Frontiers.
    <https://www.frontiersin.org/journals/microbiology/articles/10.3389/fmicb.2013.00263/full>

6.  National Heart, Lung, and Blood Institute. (2025). Asthma. U.S.
    Department of Health and Human Services.
    <https://www.nhlbi.nih.gov/health/asthma>

7.  Paciência, I., & Cavaleiro Rufo, J. (2020). Urban-level
    environmental factors related to pediatric asthm… : Porto Biomedical
    Journal.
    <https://journals.lww.com/pbj/FullText/2020/02000/Urban_level_environmental_factors_related_to.2.aspx>

8.  Sockrider, M., & Fussner, L. (2020). What is asthma? \| American
    Journal of Respiratory and Critical Care Medicine.
    <https://www.atsjournals.org/doi/10.1164/rccm.2029P25>

9.  Win, P. H., & Hussain, I. (2009, May 22). Asthma triggers: What
    really matters?. Clinical Asthma.
    <https://pmc.ncbi.nlm.nih.gov/articles/PMC7152189/>
