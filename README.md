# Credit-Risk-Analysis-Identifying-Loan-Default-Patterns
A data-driven project focused on predicting loan default risk by analyzing customer application and previous loan data. It employs comprehensive data preprocessing and exploratory data analysis in Python to uncover critical borrower characteristics and provide actionable insights for financial institutions to reduce losses.

Project Overview
This project focuses on analyzing customer application data and their previous loan application history to identify patterns associated with loan default. The goal is to help financial institutions, like banks, make more informed decisions when approving loans, thereby reducing financial risk.

Source- https://www.kaggle.com/datasets/gauravduttakiit/loan-defaulter/data?select=previous_application.csv

Problem Statement
A significant challenge for lending institutions is managing the risk of loan defaults. By understanding the characteristics of customers who are likely to default, banks can optimize their loan approval processes, minimize losses, and ensure sustainable growth. This project aims to provide actionable insights to achieve this.

Datasets
The analysis utilizes two primary datasets:

application_data.csv: Contains information about the current loan applications, including demographic details, income, credit amount, and the TARGET variable (0 for non-defaulter, 1 for defaulter).

previous_application.csv: Provides historical data on past loan applications made by the customers.

Methodology
The project follows a structured data analysis pipeline:

1. Data Import and Initial Exploration
Purpose: To bring the raw data into the Python environment and get a first look at its shape and sample entries.

Loading Data: Both application_data.csv and previous_application.csv are loaded into pandas DataFrames.

Initial Inspection: Basic checks like head() and shape are performed to understand the dataset structure. We come to know that there are 122 rows, so we would try to filter out the less important columns.

app.isnull() first creates a boolean DataFrame.

.sum() then counts the True values (which are treated as 1) for each column, effectively giving us the total number of missing values per column.

2. Feature Selection
This phase focuses on reducing dimensionality and cleaning the datasets by handling missing values and irrelevant features.

Missing Value Analysis:

Calculated the percentage of missing values for each column.

Columns with 
ge 40% missing data were identified and dropped from the application_data to ensure data quality.

Flag Column Analysis:

Identified columns starting with FLAG_ (e.g., FLAG_OWN_CAR, FLAG_EMAIL).

Visualized their distribution against the TARGET variable using count plots.

Converted 'N'/'Y' values to 0/1 for correlation analysis.

Dropped all FLAG_ columns from application_data as their individual correlation with TARGET was found to be low, simplifying the model.

External Score Correlation:

Analyzed the correlation between EXT_SOURCE_2, EXT_SOURCE_3, and TARGET.

EXT_SOURCE_2 and EXT_SOURCE_3 were dropped due to their high correlation with each other and potential redundancy for direct insights.

3. Feature Engineering
This step involves handling remaining missing values and transforming existing features to make them more suitable for analysis.

Missing Value Imputation:

CNT_FAM_MEMBERS: Imputed with the mode (most frequent value).

OCCUPATION_TYPE: Imputed with the mode.

NAME_TYPE_SUITE: Imputed with the mode.

AMT_ANNUITY: Imputed with the mean value.

AMT_REQ_CREDIT_BUREAU_* columns: Imputed with the median value.

AMT_GOODS_PRICE: Imputed with the median value.

CNT_PAYMENT (in previous_application): Imputed with 0 for missing values, based on analysis of NAME_CONTRACT_STATUS for nulls.

AMT_GOODS_PRICE (in previous_application): Imputed with the median value.

AMT_ANNUITY (in previous_application): Imputed with the median value.

PRODUCT_COMBINATION (in previous_application): Imputed with the mode.

Value Modification:

Converted all DAYS_ columns (e.g., DAYS_EMPLOYED, DAYS_BIRTH) to absolute values for easier interpretation (as they were originally negative).

Outlier Detection & Binning:

Analyzed distributions and quantiles for key numerical features (AMT_GOODS_PRICE, AMT_INCOME_TOTAL, AMT_CREDIT, AMT_ANNUITY, DAYS_EMPLOYED, DAYS_BIRTH).

Created categorical ranges (bins) for these numerical features to facilitate grouped analysis and identify specific segments (e.g., AMT_GOODS_PRICE_RANGE, DAYS_EMPLOYED_RANGE).

4. Data Analysis
This section delves into understanding the relationships between different features and the TARGET variable.

Univariate Analysis (Categorical Variables):

Iterated through all object-type variables.

Used countplot to visualize the distribution of each category against the TARGET (defaulters vs. non-defaulters).

Calculated and visualized the default percentage for each category to identify high-risk and low-risk segments.

Univariate Analysis (Numerical Variables):

Examined the distribution of key numerical variables using kdeplot.

Separated data into 'defaulters' and 'repayers' to analyze their unique correlation patterns.

Bivariate Analysis:

Calculated and unstacked correlation matrices for both defaulters and repayers to find highly correlated variable pairs.

Used kdeplot to compare the distributions of numerical variables for defaulters vs. non-defaulters (e.g., AMT_CREDIT vs. TARGET).

Used pairplot for a holistic view of relationships among key amount variables.

Data Merging:

Merged application_data and previous_application DataFrames on SK_ID_CURR to combine information for a more comprehensive analysis.

Analyzed the relationship between NAME_CASH_LOAN_PURPOSE, NAME_CONTRACT_STATUS, and TARGET in the merged dataset.

Key Insights & Conclusions
Based on the analysis, here are the primary insights and recommendations for the bank:

Target Customer Segments (Safer to Lend To):
Contract Type: Customers who have taken Cash Loans are less likely to default.

Gender: Female customers show a lower default rate (~7%) compared to males.

Accompaniment: Unaccompanied individuals have a reasonable default rate (~8.5%).

Income Type: Working individuals, Commercial Associates, and Pensioners are safer segments.

Education: Customers with Higher Education have a significantly lower default rate (less than 5%).

Family Status: Married individuals are a safer target (default rate ~8%).

Housing: People owning a house/apartment are generally safer (~8% default rate).

Occupation: Accountants, Core Staff, Managers, and Laborers are safer to target (default rate 
le 7.5% to 10%).

Organization Type: "Others," "Business Entity Type 3," and "Self Employed" organizations are good to target (default rate around 10%).

Amount Segments (Recommended):
Credit Amount: The credit amount should ideally not be more than $1,000,000.

Annuity: Annuity payments can be set around $50,000 (depending on the eligibility).

Income Bracket: Customers with an income bracket below $1,000,000 are generally safer.

Previous Application Behavior: 80-90% of customers whose previous applications were canceled or refused are repayers in the current data. The bank can consider analyzing and potentially targeting these segments with caution.

Precautions (Segments to Avoid or Approach with Caution):
Organization Type: Loans to individuals from "Transport Type 3" organizations should be avoided.

Occupation: Low-Skill Laborers and Drivers tend to be higher defaulters and should be avoided.

Previous Application Behavior: Offers that were previously unused by high-income customers show a higher number of defaulters in the current data; this segment should be avoided.

Tools and Libraries
Python: The core programming language for the project.

Pandas: For data manipulation and analysis.

NumPy: For numerical operations.

Matplotlib: For creating static, interactive, and animated visualizations.

Seaborn: For creating informative and attractive statistical graphics.

