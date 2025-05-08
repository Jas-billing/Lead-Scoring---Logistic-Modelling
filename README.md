# Lead-Scoring - Logistic-Regression
# X Education Lead Scoring & Intern Strategy

## Overview

This project addresses the challenge faced by X Education—an online course provider—in converting leads into paying customers. Although the company receives thousands of leads daily from various channels (websites, search engines, referrals, etc.), only about 30% of these leads are typically converted. Our objective is two-fold:

1. **Lead Scoring:**  
   Build a logistic regression model that assigns each lead a score between 0 and 100. A higher score signifies a “hot” lead (i.e., one that is highly likely to convert), while a lower score indicates a “cold” lead.

2. **Intern Strategy:**  
   During a two‑month period when the company hires sales interns, devise a strategy to aggressively convert as many of the high-potential leads as possible while respecting the interns’ capacity.

## Problem Statement

**Case Study Context:**  
X Education markets its online courses to industry professionals through multiple digital channels. When a visitor fills out a form on their website, they become a lead. However, despite having a large volume of leads, the conversion rate remains low. The CEO has suggested that by focusing on the most promising leads (i.e., “hot leads”), conversion could be improved to around 80%.

**Key Challenges:**
- The dataset contains approximately 9,000 leads with numerous features (e.g., Lead Source, Total Visits, Last Activity, etc.), some of which have missing values or placeholders such as “Select.”
- The predictive model must be robust, interpretable, and capable of assigning a meaningful “lead score” that helps the sales team focus on leads with the highest conversion probabilities.
- During the intern period (with a fixed calling capacity), the strategy should optimize which leads to contact based on the lead score.

## Code Approach & Methodology

The project is structured into the following key sections:

1. **Data Preparation & Cleaning**
   - **Handling Missing Values:**  
     Impute missing numbers with the median and categorical values with the mode. Convert placeholder strings (e.g., "Select", "Unknown") to `NaN` and then impute.
   - **Encoding:**  
     Convert binary variables with "Yes"/"No" into 1s and 0s. Use one-hot encoding for multi‑category columns.
   - **Dropping Unreliable Features:**  
     Drop columns where more than 70% of the values are missing.

2. **Exploratory Data Analysis (EDA)**
   - **Overall Conversion Rate:**  
     Calculate and display the average conversion rate from the data.
   - **Channel & Activity Analysis:**  
     Group data by “Lead Source”, “Lead Origin”, and “Last Activity” to identify which channels or customer behaviors yield higher conversion rates.
   - **Visualization:**  
     Use histograms, box plots, and correlation heatmaps to inspect distributions, identify outliers, and understand feature importance.

3. **Data Splitting & Preprocessing**
   - Split the dataset into training (70%) and test (30%) subsets.
   - Standardize numerical features using a scaler to ensure better model convergence.

4. **Feature Selection**
   - **Recursive Feature Elimination (RFE):**  
     Use logistic regression as the estimator in RFE to narrow down the set to the top 15 features.
   - **Multicollinearity Check:**  
     Calculate Variance Inflation Factor (VIF) and iteratively remove features with VIF > 5 to ensure model stability and interpretability.

5. **Model Building & Evaluation**
   - **Logistic Regression Model:**  
     Build and refine the logistic regression model using training data. The model is fit using the statsmodels package so that regression coefficients, p-values, adjusted pseudo R‑squared, and VIF can be inspected.
   - **Threshold Analysis:**  
     The model predicts the probability of conversion. By multiplying these probabilities by 100, a “lead score” (0–100) is obtained. A cutoff (first set at 0.3 and later optimized via cross-validation and precision-recall analysis) is then used to classify leads as “hot” or “cold.”
   - **Evaluation Metrics:**  
     Assess model performance using accuracy, precision, recall (sensitivity), specificity, F1 score, ROC AUC, and confusion matrices. Visualizations such as the ROC curve and calibration curve are provided.

6. **Intern Strategy for Aggressive Lead Conversion**
   - **Capacity Planning:**  
     Define the calling capacity of the intern team (e.g., 10 interns making 3 calls per day over 60 days).
   - **Threshold Optimization for Interns:**  
     Iterate over a range of lead score thresholds to determine how many leads would be called per day. Compare these numbers to the interns’ capacity.
   - **Strategy Recommendation:**  
     Recommend a threshold that maximizes the use of intern capacity without overwhelming the team, while ensuring that a sufficiently high proportion of leads are "hot." A multi-touch approach is also discussed if capacity utilization is low.

