# Life Expectancy Analysis Report

## 1. Introduction
The dataset taken is: https://www.kaggle.com/datasets/kumarajarshi/life-expectancy-who
This project analyzes the factors affecting the life expectancy of different countries based on data from the World Health Organization (WHO) between the years 2000 and 2015.
Since the dataset is historical (2000-2015) and relies on complex national metrics like GDP and Resource Composition, this project focuses on **Analysis** rather than creating a prediction tool for individual users. The goal is to understand *what* makes life expectancy go up or down, rather than predicting how long a specific person will live.

## 2. Data Preprocessing (Cleaning the Data)
Before running any analysis, the raw data had to be prepared to ensure accuracy. The following steps were taken:

1.  **Handling Missing Values:** The dataset had several missing numbers (e.g., some countries did not report their Hepatitis B coverage or GDP for certain years). These missing values were filled using the **mean (average)** of the respective columns so that the analysis would not be biased by empty data.
2.  **Outlier Detection and Correction:** Some data points were extreme values that did not fit the general pattern (e.g., a country with an unusually high GDP or extremely low mortality rate compared to the rest). These are called "outliers."
    * **Why we fixed them:** If left alone, these extreme values could confuse the model and "pull" the trend line in the wrong direction, making the results inaccurate.
    * **The Fix:** We identified these outliers and adjusted or removed them to ensure the model focuses on the general trends rather than the exceptions.
3.  **Categorical Data Encoding:** Computers understand numbers, not words. The "Status" column (which says if a country is "Developing" or "Developed") was converted into binary numbers (0 for Developing, 1 for Developed).
4.  **Splitting the Data:** The data was divided into two parts:
    * **Training Set (80%):** Used to teach the model the relationships between the features and life expectancy.
    * **Testing Set (20%):** Used to test how accurate the model is on data it hasn't seen before.

## 3. Methodology: Linear Regression Model
To find the relationship between the different factors (like Schooling, HIV/AIDS, GDP) and Life Expectancy, a **Multiple Linear Regression** model was used.
This model allows us to create a mathematical equation that draws a straight line through the data points. It helps us see exactly how much one variable (like Schooling) affects the target (Life Expectancy) while keeping all other variables constant.
After training, the model achieved an accuracy score (R-squared value) of approximately **82%**. This means our model can explain 82% of the variations in life expectancy based on the provided data.

## 4. The Linear Equation and Coefficients
The Linear Regression model produces a mathematical equation. Instead of complex symbols, it can be understood simply as:

**Life Expectancy = Baseline + (Coefficient 1 x Schooling) + (Coefficient 2 x HIV/AIDS) + ...**

Based on our analysis, the **Baseline Life Expectancy** (Intercept) is **68.32 years**.

The specific impact of each factor is determined by its **Coefficient**:

**Top Positive Factors (Increases Life Expectancy):**
* **Schooling (+2.37):** Education has the highest positive impact.
* **Income Composition of Resources (+1.97):** How productively resources are used.
* **BMI (+0.99):** Better nutritional status correlates with longer life.

**Top Negative Factors (Decreases Life Expectancy):**
* **HIV/AIDS (-2.59):** This is the most damaging factor.
* **Adult Mortality (-2.18):** Higher death rates among adults naturally lower the average.
* **Alcohol (-0.74):** Higher alcohol consumption correlates with lower life expectancy.

---

## 5. Example Scenario (Policy Impact Analysis)
This scenario demonstrates how a government can use this mathematical model to choose between two very different strategies: investing in education (Positive Factor) or fighting a disease (Negative Factor).

**The Situation:**
A developing country is suffering from an HIV crisis and also has low literacy rates. The government has enough budget to fix only **one** problem this year. They want to know which option will increase the average Life Expectancy the most.

**The Model Coefficients:**
* **Schooling (Positive Factor):** +2.37
    *(Meaning: For every 1 extra year of schooling, average life expectancy increases by 2.37 years)*
* **HIV/AIDS (Negative Factor):** -2.59
    *(Meaning: For every 1 unit increase in HIV deaths, average life expectancy decreases by 2.59 years)*

### Option A: Invest in Education
The government implements a policy to keep children in school longer.
* **Action:** The policy increases the average **Schooling** duration by **1 year**.
* **Calculation:** 1 (year) x 2.37 (coefficient)
* **Result:** Life Expectancy **increases by 2.37 years**.

### Option B: Fight the HIV/AIDS Crisis
The government invests in better healthcare to reduce HIV/AIDS deaths (measured in deaths per 1,000 live births).
* **Action:** The policy successfully **reduces** the HIV/AIDS death index by **1 unit**.
* **Calculation:** -1 (reduction) x -2.59 (negative coefficient)
    *(Note: Reducing a negative factor creates a positive outcome)*
* **Result:** Life Expectancy **increases by 2.59 years**.

### **Conclusion of Scenario:**
By comparing the numbers, the government can see that **Option B (Fighting HIV/AIDS)** yields a higher increase in life expectancy (**2.59 years**) compared to Option A (**2.37 years**). The model mathematically proves that tackling the critical health crisis (HIV) will have a slightly larger immediate impact than increasing education for this specific dataset.

---

## 6. Limitations
* **Date Range:** The dataset is limited to 2000-2015. Trends may have changed post-2015 (e.g., due to COVID-19).
* **Average Data:** The data represents national averages. It does not account for inequalities within a country (e.g., rich vs. poor regions).
* **Causality:** While the model shows correlation (relationships), it does not strictly prove causation.

## 7. Conclusion
This analysis successfully identifies the critical drivers of life expectancy. We concluded that **Schooling** is the most significant positive factor, while **HIV/AIDS** is the most significant negative factor. By quantifying these relationships, we provide a data-driven basis for governments to prioritize their development goals effectively.
