# Employee Sentiment Analysis — Final Report

**Author:** Tejas Khadloya  
**Project:** Employee Sentiment Analysis  
**Dataset:** test.xlsx  
**Date:** July 14, 2025  

## Introduction

This report presents a comprehensive end-to-end analysis of employee sentiment and engagement using an internal communications dataset. The analysis workflow includes robust sentiment labeling, exploratory data analysis, score aggregation, employee ranking and risk identification, and predictive modeling with fully documented methods and observations.

## Approach & Methodology

### 1. Data Loading & Inspection

- Data was loaded from `test.xlsx` containing columns: Subject, Body, Date, and From.
- Inspected for missing values and correct data types—no significant omissions found.
- Data structure was reviewed to ensure a reliable foundation for all following analysis steps.

### 2. Sentiment Labeling

- **VADER** sentiment analyzer was used as the primary model for labeling messages as Positive, Negative, or Neutral.
    - Thresholds:  
      - Compound score ≥ 0.05 → Positive  
      - Compound score ≤ –0.05 → Negative  
      - Otherwise → Neutral  
    - Justification: Chosen thresholds align with VADER defaults and have been checked for appropriateness using sample inspection.
- **TextBlob** was used in parallel for additional validation.
    - Model agreement statistics: 66.91% of messages received matching labels from both models.
    - Differences and reasoning were fully documented.
- The final sentiment label for each message is based on VADER, ensuring both robustness and reproducibility.

### 3. Exploratory Data Analysis (EDA)

- Examined data structure, types, and missing values.
- Counted and visualized sentiment label distribution.
- Visualized monthly sentiment trends.
- Performed boxplot analysis of message length across sentiment categories.
- Listed top 10 most active senders.
- Detected outlier months with unusually high messaging or sentiment activity.

**Interpretations were provided after every visualization**, highlighting their business relevance and guiding next steps.

### 4. Employee Monthly Sentiment Score Calculation

- Each communication:  
    - Positive: +1  
    - Negative: -1  
    - Neutral: 0  
- Monthly scores are the sum per employee, resetting every new month.
- Results are structured for downstream ranking and risk analysis.

### 5. Employee Ranking

- For each month:
    - **Top 3 Positive Employees:** Highest scores, ranked by score (descending) then alphabetically.
    - **Top 3 Negative Employees:** Lowest scores, ranked by score (ascending) then alphabetically.
- All-month rankings are exported to Excel for transparency.
- Bar charts visually highlight exceptional positive contributors and distributed or concentrated negative sentiment.
- Narrative explanations accompany all outputs, making the findings actionable.

### 6. Flight Risk Identification

- Flight risk is defined as any employee sending 4+ negative emails within any rolling 30-day window, per project instructions.
- Each flagged employee appears only once, even if multiple risk windows exist.
- Results are printed and saved for HR/leadership review.

### 7. Predictive Modeling

- Linear regression predicts each employee's monthly sentiment score using these features:
    - Message count
    - Total length
    - Average length
    - Total words
    - Average words
- The dataset is split 80/20 for train/test evaluation.
- Model metrics:
    - R² Score: 0.72  (Strong real-world predictive power; model explains 72% of variance in monthly scores)
    - Mean Absolute Error (MAE): 1.40  (On average, predictions are 1.4 sentiment points from actual)
- Actual vs. predicted plots and interpretation illustrate model fit and highlight occasional outliers.
- Coefficient table shows **message count is the dominant driver** of positive sentiment; other features have weaker or marginal effects.

## Key Findings

### Sentiment Distribution

- Majority of messages: Positive (1,528)
- Neutral messages: 511
- Negative messages: 152  
Interpretation: Communication climate is generally positive, with some evidence of disengagement/complaint.

### Monthly Sentiment Trends

- Employee sentiment is stably positive month-to-month.
- Neutral/negative messages did not display persistent spikes, but rare months with high activity were flagged for context-specific review.
Interpretation: No overwhelming periods of negativity; most changes seemed minor and periodic.

### Message Length by Sentiment

- Positive and negative messages tend to be longer than neutral ones.
- Negative outliers are unusually verbose, potentially signifying detailed complaints.
Interpretation: Brevity in neutral communications may indicate disengagement; verbosity in negativity could reflect greater issue detail.

### Top Senders

- Most active senders are central to communication patterns and potentially to company morale.
Interpretation: Engagement monitoring should prioritize these individuals and watch for shifts in their communication style or frequency.

### Employee Rankings (Sample: January 2010)

| Rank | Employee Email              | Sentiment Score | Category  |
|------|-----------------------------|----------------|-----------|
| 1    | kayne.coulter@enron.com     | 13             | Positive  |
| 2    | eric.bass@enron.com         | 9              | Positive  |
| 3    | lydia.delgado@enron.com     | 9              | Positive  |
| 1    | bobette.riner@ipgdirect.com | 1              | Negative  |
| 2    | johnny.palmer@enron.com     | 1              | Negative  |
| 3    | rhonda.denton@enron.com     | 1              | Negative  |

Interpretation: January 2010 saw strong positive contributions from the top three, especially one clear standout. Negative scores were tied and low—negative sentiment was distributed, not concentrated.

### Flight Risk Employees

- Identified (based on 4+ negative emails within any 30-day rolling window):
    - bobette.riner@ipgdirect.com
    - sally.beck@enron.com
    - johnny.palmer@enron.com
    - don.baughman@enron.com

Interpretation: These individuals warrant proactive engagement and potential HR support.

### Linear Regression Model

- **R² Score:** 0.72  
- **MAE:** 1.40

Feature Importances (Coefficients):

| Feature         | Coefficient | Interpretation                                                                       |
|-----------------|:-----------:|-------------------------------------------------------------------------------------|
| message_count   |   0.57      | Most predictive; more monthly activity = higher sentiment                            |
| total_words     |   0.01      | Minor positive influence                                                            |
| avg_length      |   0.00      | Small positive effect                                                               |
| avg_words       |  -0.00      | Very weak negative, not predictive beyond message_count                             |
| total_length    |  -0.00      | Negligible                                                                          |

Interpretation: Frequent, regular communication is a strong signal of higher sentiment, while just writing longer or wordier emails isn't by itself a predictor of improved attitude or engagement.

## Visualizations (Summary of Outputs)

- **Bar chart:** Sentiment label distribution.
- **Stacked bar chart:** Monthly sentiment trends.
- **Boxplot:** Message length per sentiment.
- **Grouped bar chart:** Top 3 positive/negative employees each month.
- **Scatter plot:** Actual vs. predicted sentiment scores (model fit).
- **Excel**: Monthly employee rankings and flight risk employee lists.

## Recommendations

- **Proactive HR Engagement:** Intervene early with employees flagged as flight risks.
- **Recognize/Support Top Performers:** Publicly acknowledge consistently positive employees; support those with ongoing negative sentiment.
- **Ongoing Monitoring:** Repeat sentiment and ranking analysis on a regular schedule.
- **Model Improvement:** Consider using richer text-based features or additional metadata for even better predictive accuracy.

## Project Reproducibility and Structure

- All steps are sequentially titled, human-commented, and include rationale and technical logic.
- Every major section’s output is clearly spaced and interpreted, ensuring readability and stakeholder utility.
- The pipeline allows any stakeholder to follow the narrative from data to findings to recommended action without reference to the code alone.

# README.md — Summary

## Employee Sentiment Analysis — README

**Project:** Employee Sentiment Analysis  
**Author:** Tejas Khadloya

### Objective

To analyze employee message data and provide interpretable, actionable insights about morale, engagement, and potential attrition risk, using robust NLP and data science workflows.

### Project Highlights

- Labeled every message from raw data as Positive, Neutral, or Negative using **VADER** (primary) and **TextBlob** (benchmarking).
- Performed comprehensive **exploratory data analysis** (EDA) with detailed interpretations after each chart or table.
- Computed **monthly sentiment scores** for each employee, resetting every new month.
- Generated and interpreted **ranked lists**:  
    - Top 3 Positive/Negative employees per month.
    - Explained each month’s rankings and visualized leaderboards.
- **Flagged flight risk employees**:  
    - Anyone sending 4+ negative emails in any rolling 30-day window.
    - List: bobette.riner@ipgdirect.com, sally.beck@enron.com, johnny.palmer@enron.com, don.baughman@enron.com
- Built a **linear regression model**:
    - Used message counts, lengths, and word counts to forecast monthly sentiment scores.
    - R² Score: 0.72, MAE: 1.40.
    - Most important feature: message_count (frequency).
    - Plots and coefficient tables included, all explained in plain language.

### Key Insights & Recommendations

- **Employee morale is high overall,** with a minority of negative outliers.
- **Monthly engagement stability** is strong, but rare periods have greater negative or neutral messaging — these deserve closer review.
- **Frequent communicators drive positivity.** Encourage open, regular exchanges; targeted support should be offered to risk-flagged individuals.
- **Model forecasts are reliable,** supporting data-driven HR decisions.

### Deliverables Structure

- `LLM-Final-Assessment.ipynb` — Step-by-step code and detailed narrative, ready for review or rerun.
- `visualization/` folder — All key charts, plots, and Excel outputs for visualization and monthly rankings.
- This `README.md` — Summary of findings, outcome tables, and recommendations.

### How to Use This Project

1. Open and run the notebook/cell file (`LLM-Final-Assessment.ipynb`).
2. Review the in-line outputs and observations after each section.
3. Examine the visualizations and exported Excel/CSV files for reference and leadership review.
4. Use the interpretation comments to shape next steps or HR interventions.

### Top Three Positive and Negative Employees (Sample: Jan 2010)

| Rank | Employee Email              | Sentiment Score | Category  |
|------|-----------------------------|----------------|-----------|
| 1    | kayne.coulter@enron.com     | 13             | Positive  |
| 2    | eric.bass@enron.com         | 9              | Positive  |
| 3    | lydia.delgado@enron.com     | 9              | Positive  |
| 1    | bobette.riner@ipgdirect.com | 1              | Negative  |
| 2    | johnny.palmer@enron.com     | 1              | Negative  |
| 3    | rhonda.denton@enron.com     | 1              | Negative  |

### Flight Risk Employees

- bobette.riner@ipgdirect.com
- sally.beck@enron.com
- johnny.palmer@enron.com
- don.baughman@enron.com


**End of Report & README**
