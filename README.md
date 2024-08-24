# Credit Card Complaints Analysis
---
## Table of Contents
1. [Project Overview](#project-overview)
2. [Data Overview](#data-overview)
3. [Objectives](#objectives)
4. [SQL and Tableau Calculated Fields](#sql-and-tableau-calculated-fields)
    - [SQL Queries](#sql-queries)
    - [Tableau Calculated Fields](#tableau-calculated-fields)
5. [Tableau Visualization](#tableau-visualization)
6. [Insights and Recommendations](#insights-and-recommendations)
7. [Conclusion](#conclusion)
8. [Additional Resources](#additional-resources)

## Project Overview
This project focuses on analyzing credit card complaints data, offering insights into common issues, response times, and geographic distribution. By leveraging Tableau, the analysis provides a visual representation of complaint trends, helping stakeholders address customer pain points more effectively.

## Data Overview
- **Credit Card Complaints Data:** This dataset includes complaints logged against various financial institutions, categorized by issues like billing disputes, identity theft, and others. It also includes details on company responses and the channels through which complaints were submitted.
- [**Download the Dataset**](https://public.tableau.com/vizql/v_202422408070112/javascripts/hybrid-window/min/index.html?id=1i5ldomqk%24rfy6-fx-sh-k1-34wbg3&moduleId=view_data)

## Objectives
- **Complaint Analysis:** Identify the most common types of complaints and track their frequency over time.
- **Response Analysis:** Evaluate the efficiency of the companies in responding to complaints.
- **Geographical Insights:** Analyze the distribution of complaints across different regions.
- **Customer Satisfaction:** Examine the correlation between the type of response and customer satisfaction.

## SQL and Tableau Calculated Fields

### SQL Queries
Here are some example SQL queries used in this project:

```sql
-- Create Database and Tables
CREATE DATABASE CreditCardComplaintsDB;

USE CreditCardComplaintsDB;

CREATE TABLE ComplaintsData (
    ComplaintID INT PRIMARY KEY,
    Issue VARCHAR(255),
    Company VARCHAR(100),
    State VARCHAR(50),
    SubmittedVia VARCHAR(50),
    DateReceived DATE,
    CompanyResponse VARCHAR(100),
    TimelyResponse VARCHAR(5),
    DateClosed DATE
);

-- Load Data
BULK INSERT ComplaintsData
FROM 'path_to_your/credit_card_complaints.csv'
WITH (FIELDTERMINATOR = ',', ROWTERMINATOR = '\n', FIRSTROW = 2);

-- Analyze Most Common Issues
SELECT 
    Issue,
    COUNT(*) AS ComplaintCount
FROM ComplaintsData
GROUP BY Issue
ORDER BY ComplaintCount DESC;
```

### Tableau Calculated Fields
Below are some Tableau Calculated Fields used for the analysis:

#### 1. **Total Complaints**
   - **Tableau Calculated Field:**
     ```tableau
     COUNT([ComplaintID])
     ```
   - **Purpose**: This field calculates the total number of complaints.

#### 2. **Timely Response Rate**
   - **Tableau Calculated Field:**
     ```tableau
     SUM(IF [TimelyResponse] = "Yes" THEN 1 ELSE 0 END) / COUNT([ComplaintID])
     ```
   - **Purpose**: This field calculates the rate of timely responses by dividing the number of timely responses by the total number of complaints.

#### 3. **Complaints Closed with Explanation or Relief**
   - **Tableau Calculated Field:**
     ```tableau
     SUM(IF [CompanyResponse] = "Closed with explanation" 
           OR [CompanyResponse] = "Closed with monetary relief" 
           THEN 1 ELSE 0 END) / COUNT([ComplaintID])
     ```
   - **Purpose**: This field calculates the rate of complaints closed with an explanation or monetary relief.

#### 4. **Complaints by State**
   - **Tableau Approach**:
     - To visualize complaints by state, you can drag the `State` dimension to the `Rows` or `Columns` shelf and `ComplaintID` to the `Text`, `Color`, or `Size` marks in Tableau. This gives a breakdown of total complaints per state without needing a specific calculated field.

## Tableau Visualization
The Tableau dashboard provides a detailed view of:

- **Total Complaints and Trends:** Track the number of complaints over time, with a focus on rolling 12-month averages.
- **Timely Response Rate:** Display the percentage of complaints that received a timely response.
- **Geographical Distribution:** Map of complaints across different states to identify hotspots.
- **Top Issues:** Visual representation of the most common complaint types.
- **Company Responses:** Breakdown of how companies respond to complaints.

You can view the Tableau dashboard [here](https://public.tableau.com/app/profile/noe.careme.fouotsa.manfouo/viz/CreditCardComplaints_17220260717800/CreditCardComplaints).

## Insights and Recommendations
Based on the analysis:

- **Billing Disputes:** These are the most common complaints, indicating a need for improved billing processes.
- **Geographical Focus:** States like California and Texas have higher complaint rates, suggesting targeted customer service improvements in these areas.
- **Response Efficiency:** While most complaints are closed with an explanation, a higher focus on providing monetary relief might improve customer satisfaction.
- **Submission Channels:** A majority of complaints are submitted online, highlighting the importance of a user-friendly web interface for complaint submission.

## Conclusion
This analysis provides critical insights into credit card complaint patterns, helping companies identify key areas for improvement in customer service and complaint resolution.

## Additional Resources
- [Download the Dataset](https://public.tableau.com/vizql/v_202422408070112/javascripts/hybrid-window/min/index.html?id=1i5ldomqk%24rfy6-fx-sh-k1-34wbg3&moduleId=view_data)
- [View Tableau Dashboard](https://public.tableau.com/app/profile/noe.careme.fouotsa.manfouo/viz/CreditCardComplaints_17220260717800/CreditCardComplaints)
---
