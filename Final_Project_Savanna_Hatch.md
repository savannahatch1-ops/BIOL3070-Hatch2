Final Prohect
================
Savanna Hatch
2025-10-30

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

# STUDY QUESTION and HYPOTHESIS

## Questions

## Hypothesis

## Prediction

# METHODS

``` r
library(ggplot2)

age <- data.frame(category = c(" 0-4", " 5-11", "12-17", "18-24", "25-34", "35-64", "65+"), value = c(1.4, 2.4, 2.0, 3.8, 6.4, 11.5, 27.1))

ggplot(age, aes(x = category, y = value)) +
  geom_bar(stat = "identity", fill = "lightblue") + # stat="identity" uses y-values directly
  labs(title = "Asthma Deaths By Age", x = "Age (Years)", y = "Asthma-Related Deaths Per Million")
```

![](Final_Project_Savanna_Hatch_files/figure-gfm/age%20and%20deaths-1.png)<!-- -->

# DISCUSSION

# CONCLUSION

# REFERENCES
