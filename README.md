# STAT 240 Project: Precipitation Trends in the Midwest (1980–2020) and Climate Change

## Introduction
Climate change has raised concerns about shifts in precipitation patterns worldwide, with major implications for agriculture, water resources, and ecosystems. In this project, we focused on the Midwest region of the United States to answer the question:  

**Has the average annual precipitation in the Midwest significantly changed between 1980–2000 and 2001–2020?**

Understanding these shifts helps improve climate adaptation strategies. Our analysis found **no convincing evidence** that the mean monthly precipitation between the two periods is significantly different.

---

## Data

**Region:** Midwest (Illinois, Indiana, Iowa, Michigan, Minnesota, Missouri, Ohio, Wisconsin)  
**Source:** [NOAA National Centers for Environmental Information (NCEI)](https://www.ncei.noaa.gov/)  
- [1980–2000 precipitation data](https://www.ncei.noaa.gov/access/monitoring/climate-at-a-glance/regional/time-series/102/pcp/1/0/1980-2000)  
- [2001–2020 precipitation data](https://www.ncei.noaa.gov/access/monitoring/climate-at-a-glance/regional/time-series/102/pcp/1/0/2001-2020)  

**Structure:**  
- Monthly precipitation values (inches), 1980–2020  
- 504 data points total (252 per time period)  
- Cleaned dataset ensured no duplicates or missing months  

We used **monthly averages** instead of yearly totals to capture seasonal patterns and increase the number of observations.

---

## Methods

**Data Processing**
- Combined datasets, removed duplicates  
- Reformatted dates for consistency  
- Grouped by month to calculate mean, standard deviation, and sample size  

**Visualization (R/ggplot2)**
- Smoothed time-series plot (1980–2020)  
- Residual plots to check assumptions (linearity, heteroscedasticity)  

**Statistical Test**
- **Two-sample t-test (Welch’s t-test)**  
- Null Hypothesis (H₀): μ₁ = μ₂ (no difference in mean monthly precipitation)  
- Alternative Hypothesis (H₁): μ₁ ≠ μ₂ (difference exists)  
- α = 0.05  

---

## Results

**Welch Two-Sample t-test**
- t = -1.029, df = 487.75, p-value = 0.304  
- 95% CI: [-0.386, 0.121]  
- Means:  
  - 1980–2000: 2.61 in  
  - 2001–2020: 2.74 in  

**Interpretation:**  
Since *p > 0.05*, we fail to reject H₀. There is no statistically significant difference in mean monthly precipitation between the two time periods.  

**Visual Insights:**  
- Precipitation remained relatively stable until ~2005, after which averages increased slightly.  
- By 2020, monthly averages rose to ~3.0 in compared to ~2.6 in in 1980, but the difference was not statistically significant.  

---

## Discussion

**Key Takeaway:**  
The data does not provide convincing evidence of significant precipitation changes in the Midwest between 1980–2000 and 2001–2020.  

**Considerations:**  
- Natural variability (e.g., El Niño/La Niña) may mask trends  
- Climate change impacts may emerge over longer timescales  
- Factors such as land use, jet stream shifts, and evaporation could also play roles  

**Limitations:**  
- 40-year scope may be too short to detect long-term climate shifts  
- Potential inaccuracies in older data collection methods  
- Missing values and technological changes in measurement  

---

## Future Questions
- Are specific states within the Midwest more affected than others?  
- How do other indicators (temperature, humidity) change alongside precipitation?  
- Has the variability (not just the mean) of precipitation shifted over time?  

---

## Recommendations
1. **Extend timeframe**: Include more recent years to capture ongoing trends.  
2. **Explore other variables**: Incorporate temperature, humidity, and land-use changes.  
3. **Refine spatial analysis**: Examine precipitation patterns at state or sub-regional levels.  

---

