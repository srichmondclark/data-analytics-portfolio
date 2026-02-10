data-analytics-portfolio
 README.md
 behavioural-data-analysis/
 README.md
 analysis.R


# Behavioural Data Analysis

## Project Overview
This project explores factors that influence reaction time using a simulated behavioural dataset.
The analysis demonstrates data cleaning, exploratory data analysis, statistical testing,
and regression modelling using R.

## Objectives
- Prepare and clean behavioural data for analysis
- Explore relationships between key variables
- Apply statistical methods to test hypotheses
- Communicate findings using clear visualisations

## Methods
- Data cleaning and transformation
- Exploratory Data Analysis (EDA)
- ANOVA
- Linear regression
- Data visualisation using ggplot2

## Key Findings
- Reaction time increased with task difficulty
- Sleep duration showed an association with faster reaction times
- Task difficulty was the strongest predictor in the regression model

## Limitations
- Dataset was simulated for learning purposes
- Results are illustrative rather than definitive

## Tools Used
- R
- RStudio
- tidyverse
- ggplot2

set.seed(123)

data <- data.frame(
  age = sample(18:60, 150, replace = TRUE),
  sleep_hours = round(runif(150, 4, 9), 1),
  task_difficulty = sample(c("Easy", "Medium", "Hard"), 150, replace = TRUE),
  reaction_time = round(rnorm(150, mean = 550, sd = 80), 0)
)

library(dplyr)

data <- data %>%
  mutate(
    task_difficulty = factor(task_difficulty, levels = c("Easy", "Medium", "Hard"))
  )

library(ggplot2)

ggplot(data, aes(x = task_difficulty, y = reaction_time)) +
  geom_boxplot() +
  labs(title = "Reaction Time by Task Difficulty")


anova_result <- aov(reaction_time ~ task_difficulty, data = data)
summary(anova_result)


model <- lm(reaction_time ~ age + sleep_hours + task_difficulty, data = data)
summary(model)
