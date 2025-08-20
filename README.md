Introduction
As climate change becomes more prevalent worldwide, shifts in weather patterns have become increasingly apparent. Precipitation trends, in particular, are key indicators of how climate change impacts a given area, influencing agriculture, water resources, and the environment. As the global climate changes, scientists have raised concerns about changing precipitation patterns across the United States and the world. Although changes in precipitation alone do not necessarily imply climate change, they are a fundamental part of broader climate patterns.

For our project, we are focusing specifically on the Midwest region of the United States. The question we aim to answer is: Has the average annual precipitation in the Midwest significantly changed due to climate change between the time periods 1980–2000 and 2001–2020?

This question matters because shifts in precipitation patterns can have major impacts across the regions, so understanding these changes helps improve climate adaptation strategies. We hope to better understand whether the effects of climate change are evident in long-term precipitation patterns within the Midwest. 

We concluded that we do not have convincing evidence that the mean annual precipitation between 1980-2000 and 2001-2020 is different.

Background

Data Sources
Raw Data: The raw data was collected from NCEI Regional Time Series, collected and maintained by National Centers for Environmental Information. This set of data tracks the precipitation in the midwestern region from 1980-2000 and 2001-2020. 
This data was collected as each year progressed, each year The total precipitation in inches was recorded. This dataset collected totals from 1980-2020. 
1980-2000 precipitation data: https://www.ncei.noaa.gov/access/monitoring/climate-at-a-glance/regional/time-series/102/pcp/1/0/1980-2000
2001-2020 precipitation data: https://www.ncei.noaa.gov/access/monitoring/climate-at-a-glance/regional/time-series/102/pcp/1/0/2001-2020

About the Data
In this study, the Midwest refers to the eight states typically considered part of the “Upper Midwest” per NOAA’s regional breakdown: Illinois, Indiana, Iowa, Michigan, Minnesota, Missouri, Ohio, and Wisconsin. The data was collected from the NOAA National Centers for Environmental Information (NCEI), which manages and provides access to one of the world’s largest archives of environmental data.

Variables
Annual/Seasonal Precipitation: Quantifies the precipitation in inches, annually and seasonally, across the two study periods.
Time Intervals: Denotes each month within the specified years.

Data Structure
Single Row Representation: Each row signifies the mean monthly precipitation within each year.
Population Representation: The broader data context includes precipitation data from across the United States, though our focus is on the Midwest.
Sample Size: Consists of 504 data points in total, with 252 from each time interval.
We chose to use monthly precipitation averages instead of yearly totals so we could see more detailed seasonal patterns and have more data points to make our analysis stronger.
Data Cleansing and Processing & Supporting Graph
The dataset was processed to ensure accuracy and relevance for analysis. Months with insufficient or no data provided were excluded, which did not apply since we are using each month as an interval. The cleaned dataset was grouped by month to calculate the mean, standard deviation, and sample size for each group.

#Combine dataset and make it unique
combined_precip <- rbind(precip_1980_2000, precip_2000_2020) %>% distinct(Date, Value, .keep_all = TRUE) #Edit Data to get combined Dataset w/ no duplicates

#Fix the dates, so it looks visually appealing 
combined_precip$Date <- as.Date(paste0(combined_precip$Date, "01"), format = "%Y%m%d")

plot_1980_2020 <- ggplot(combined_precip, aes(x = Date, y = Value))+
  geom_smooth() +
  labs (x = "Date (year)", y = "Precipitation (in)") +
  theme_light()

Plot_1980_2020
Meaning: The precipitation remained stable up until 2005, where there was an increase in the avg precipitation. By 2020, the average was about 3in as opposed to 1980 where it was about 2.6in.

Residual Graph
# Residual plot, but with combined Data set
combined_precip$residuals <- resid(model_all_data)
ggplot(combined_precip, aes(x = Date, y = residuals)) +
  geom_point(color = 'lightgreen') +
  geom_hline(yintercept = 0, linetype = "dashed", color= 'darkred') +
  labs(title = "Residual Plot: Precipitation over Time",
       y = "Residuals",
       x = "Date") +
  theme_minimal()

There are two residual plots, one made with the combined data set while the other was made with each data set (1980 - 2000 & 2000-2020).

Heteroscedasticity: The spread seems fairly scattered, but towards the end there are more vertical spread. This means a mostly normal heteroscedasticity.

Linearity: The residuals seem to be scattered fairly evenly across time - this means the linearity assumption holds up.

Statistical Analysis

Hypotheses
Null hypothesis: μ1 = μ2
Alternative hypothesis: μ1 ≠ μ2.

Parameters
μ1 is the average amount of precipitation over each month between 1980 and 2000
μ2 is the average amount of precipitation over each month between 2001 and 2020

Assumptions
Independence: We can assume independence for our datasets since precipitation levels from a given year do not depend on precipitation levels from any other year.
Symmetric: Using the Central Limit Theorem, we can assume the dataset is approximately symmetric

Statistical Test
Two sample t-test for a difference in means
Significance level: α = 0.05 

Test Statistic and Null Distribution
Two Sample t-test
#filter out 2000, so only one data set would have it
precip_2001_2020 <- combined_precip %>%
  filter(Date > "2000-12-01")

value_1980_2000 <- precip_1980_2000$Value 
value_2001_2020 <- precip_2001_2020$Value
t.test(value_1980_2000,value_2001_2020) 
## H₀: μ₁ − μ₂ = 0 (means are equal) H₁: μ₁ − μ₂ ≠ 0 (means are not equal ^ so this form is correct, do not change the value for mu)
Results
Welch Two Sample t-test

data:  value_1980_2000 and value_2001_2020
t = -1.029, df = 487.75, p-value = 0.304
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -0.3858787  0.1206128
sample estimates:
mean of x mean of y 
 2.610159  2.742792

Results and Interpretation
We fail to reject the null hypothesis because our p-value is greater than alpha. Therefore, we do not have convincing evidence that the true mean difference between mean of precipitation over each month between 1980 and 2000 and mean of precipitation over each month between 2001 and 2020 is different.

Discussion

Further Interpretation
Since we rejected the null hypothesis that the mean precipitation from 1980–2000 and 2001–2020 are equal, there is statistically significant evidence of a change in precipitation in the Midwest. This suggests that precipitation patterns have not significantly shifted over time. Such changes can be influenced by a range of factors, including climate change, environmental variability, human activities, and the region's adaptability. For instance, El Niño and La Niña are recurring climatic events that affect global weather by altering air circulation, ocean temperatures, and moisture distribution. The observed changes in precipitation may reflect the combined effects of human-induced climate change and natural climate variability. These findings highlight the importance of continued monitoring and adaptable environmental planning in the Midwest. 

For non-statistical readers
Our analysis shows that there is no significant change in average monthly precipitation in the Midwest between the two periods. While small differences in precipitation might actually exist, they are not large enough to conclude that a meaningful shift has occurred. Although precipitation patterns may still be influenced by factors like climate change, many other factors including natural weather cycles, changes in land use, and atmospheric patterns also contribute. 

Shortcomings of the Analysis
Other variables: Climate change is not the only factor that influences precipitation levels. Precipitation can also be influenced by elevation, proximity to bodies of water, different latitudes, patterns of air masses, and human-related activities. While climate change is a main driver of precipitation change, it certainly is not the only factor.
Data collection discrepancies: Weather-related technology has significantly improved since 1980, so the techniques by which the data was collected for each year might not be completely accurate for older years.
Missing data: Both data sets had missing values, so we had to clean the data to remove those values. Those missing values affect the summary statistics of the data and could have an impact on the overall results.
Time Span: The analysis is limited to a 20-year period for each interval. A longer time span would provide better insight into precipitation trends and would make the data easier to compare.

Additional Questions
Are specific states or sub-regions within the Midwest more affected than others?
Are other climate indicators (e.g., temperature, humidity) also shifting significantly in the Midwest during the same periods?
Is the variability/standard deviation of precipitation also changing over time?

Recommendations
Create larger time intervals: Incorporating more recent data could confirm whether the trend continues or if there are signs of stabilization or reversal.
Analyze other causes of precipitation change: Explore potential causes like changes in jet stream patterns, increased evaporation due to rising temperatures, or human factors such as deforestation or urbanization.
