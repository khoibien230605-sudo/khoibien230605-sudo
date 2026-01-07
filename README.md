# Data Driven Insights for Airline Retention: Seasonal Trends, Churn Prediction, and Promotion Impact

## Analyze Customer Churn factors using MySQL and Power BI analytics.
Situation Analysis: 
The airline industry is highly competitive, so keeping customers loyal is essential for long-term success. Most airlines use loyalty programs to encourage repeat travel and build a strong customer base. However, the main challenge is that airlines have to deal with a massive amount of data. 

This makes it very difficult for them to analyze which specific factors truly drive customer retention and how to accurately measure customer lifetime value. Without these insights, it is hard for airlines to know exactly how to keep their passengers coming back.



## Objective
Optimize Retention Strategies To provide actionable recommendations for improving Customer Lifetime Value (CLV) by targeting the right customers at the right time with the right incentives.


## Data Understanding
2 datasets are being used as follows:

a) **Flight Activity**
|  Feature Name   |   Description  |
|-------------|-----------------------|
| Loyalty Number  | Customer's unique loyalty number |
| Year  | Year of the period|
| Month | Month of the period |
| Flights Booked | Number of flights booked for member only in the period |
| Flights with Companions | Number of flights booked with additional passengers in the period |.
| Total Flights | Sum of Flights Booked and Flights with Companions |
| Distance | Flight distance traveled in the period (km) |
| Points Accumulated | Loyalty points accumulated in the period |
| Points Redeemed | Loyalty points redeemed in the period |
| Dollar Cost Points Redeemed | Dollar equivalent for points redeemed in the period in CDN |

b) **Loyalty History**
|  Feature Name   |   Description  |
|-------------|-----------------------|
| Loyalty Number  | Customer's unique loyalty number |
| Country  | Country of residence |
| Province | Province of residence |
| City | City of residence |
| Postal Code | Postal code of residence |.
| Gender | Gender |
| Education | Highest education level (High school or lower > College > Bachelor > Master > Doctor) |
| Loyalty Card | Loyalty card status (Star > Nova > Aurora) |
| CLV | Customer lifetime value - total invoice value for all flights ever booked by member |
| Enrollment Type | Enrollment type (Standard / 2018 Promotion) |
| Enrollment Year | Year Member enrolled in membership program |
| Enrollment Month | Month Member enrolled in membership program |
| Cancellation Year | Year Member cancelled their membership |
| Cancellation Month | Month Member cancelled their membership |


## Research Questions

#### 1. In which months of the year do customers typically cancel their membership cards? If there's a seasonal pattern, should we launch a loyalty program in those months to "retain" them before it's too late?

#### 2. Did customers who canceled their cards show a decrease in flight booking frequency in the 3-6 months prior? This is the basis for building an "early warning" system for the customer service team.

#### 3. Did the "2018 Promotion" program attract loyal customers or just "deal hunters" who leave after using up their benefits?

## SQL and Google Collab Analysis
### Dataset Overview
The Customer Flight Activity table contains a comprehensive log of 405,624 flight records tracked over the analysis period. 
Complementing this, the Customer Loyalty History table provides demographic and membership profiles for 16,737 unique customers.
<img width="589" height="310" alt="Screenshot 2026-01-07 222048" src="https://github.com/user-attachments/assets/49efdfb6-2072-4f9b-bcbe-187cbf20b522" />
### Demographics
<img width="318" height="247" alt="Screenshot 2026-01-07 222844" src="https://github.com/user-attachments/assets/5fa34d4e-9f82-4b24-a64a-226051969baa" />

#### Education Level Distribution Analysis
This chart shows the education background of our customers. Understanding this helps us tailor our communication and services to their preferences.

Key Findings:

Dominant Group: Customers with a Bachelor’s degree make up the largest portion of our database, with over 10,000 individuals.

Secondary Group: The second-largest group consists of those with a College education (approximately 4,000+ individuals).

Minority Groups: There is a smaller representation of customers with High School or Below, Doctor, and Master degrees, each group having fewer than 1,000 members.

Conclusion & Insight: The majority of customers are highly educated (Bachelor’s degree or higher). This suggests that target audience is likely composed of professionals or skilled workers. 

#### Distribution of Loyalty Tiers

<img width="299" height="237" alt="image" src="https://github.com/user-attachments/assets/f9bb3507-d42b-4d30-87ec-0e51904ccf33" />


This chart shows how customers are divided among our three loyalty program tiers: Star, Nova, and Aurora.

- **Star Tier**: This is the most popular tier with over 7,000 members. It likely serves as the entry point for most customers.

- **Nova Tier**: This middle tier has a strong presence with nearly 6,000 members, showing that a large number of customers are actively engaging beyond the basic level.

- **Aurora Tier**: This is the most exclusive tier with roughly 3,500 members. While it has the lowest count, these are likely our most frequent and valuable travelers.

#### Data Exploration
<img width="411" height="338" alt="Screenshot 2026-01-07 232308" src="https://github.com/user-attachments/assets/f4a0ebf4-0f13-4ecc-838f-ce4fd8fdf37d" />

Peak periods: July (7.26 trips) and December (6.17 trips)

Insight: Demand surges in summer and during the Christmas season, making these periods the most lucrative for revenue generation


## KPIs Calculations
### Churn Count by Month & Monthly Churn Rate

<img width="540" height="455" alt="image" src="https://github.com/user-attachments/assets/f83be4f1-396a-494b-ba19-32d77bc3cbba" />

- **Churn Count by Month**: 16737
- **Monthly Churn Rate**: 100.00
### Flight Frequency Velocity

<img width="799" height="653" alt="image" src="https://github.com/user-attachments/assets/1dad19ff-b1b5-41c8-8c49-29073ef27415" />


This analysis highlights how customer behavior changed between the two periods (Months 4–6 and Months 1–3).

Significant Growth (Positive Trend)
Several loyalty members show a strong increase in flight activity. These customers are becoming more active:

Member 148258: This member shows the highest growth. They went from almost no flights (0.66) to over 9 flights per month.

Member 107420: Their activity doubled, increasing from 4.6 flights to 9.6 flights per month.

Members 138025 and 138065: Both saw a solid increase of 4 flights per month, showing improved engagement.

### Average CLV

<img width="924" height="394" alt="image" src="https://github.com/user-attachments/assets/a80ed1b1-b5f2-4164-a02d-38043f628389" />

#### Average Customer Lifetime Value (Avg_CLV)
1. 2018 Promotion Group
- **Average CLV**: 8,046.51

- **Total Customers**: 971

Observation: This group has the highest average value per customer in the table. Even though the group is smaller, these customers contribute more value individually than standard members.

2. Standard Enrollment Group
- **Average CLV**: 7,985.35

- **Total Customers**: 15,766

Observation: This is the largest customer segment. While their individual average value is slightly lower than the promotion group, they represent the bulk of the total revenue due to the high number of customers.

3. Comparison
- **The Difference**: Customers from the 2018 Promotion have an average lifetime value that is 61.16 higher than Standard customers.
- **Calculation**: $8,046.51 - 7,985.35 = 61.16$
  
Summary: The 2018 Promotion was successful in attracting "high-value" customers who spend more on average than those in the Standard group.

## Data Modeling (Power BI)

The data is organized into a Star Schema to optimize performance and reporting in Power BI. It consists of two Dimension tables and one Fact table.
### Dimension Tables (Dim)
Dimension tables provide descriptive context for the data. In this model, we have two main dimension tables:

- **DimCustomer**: Contains detailed personal information about each loyalty member.

Key Components: `Loyalty Number`, `City, Province`, `Country`, `Gender`, `Education`, `Marital Status`, `and Salary`.


- **DimLoyaltyStatus**: Contains information regarding the customer's membership status and enrollment history.

Key Components: `Enrollment Type` (Standard vs. 2018 Promotion), `Enrollment Date` (Month/Year), `Cancellation Date`, `Loyalty Card Type`, `Member Status`, and `Customer Lifetime Value` (CLV).

### Fact Table (Fact)
The Fact table contains the quantitative data (measurements) used for calculation and analysis.

FactFlightActivity: This is the central table that records all flight-related transactions and activities.

Key Components: `Total Flights`, `Distance`, `Points Accumulated`, `Points Redeemed`, and `Dollar Cost of Points Redeemed`.

Relationships: This table is linked to the Dimension tables via the Loyalty Number.

<img width="905" height="716" alt="Screenshot 2026-01-08 011328" src="https://github.com/user-attachments/assets/6afa0da7-a132-440f-8f19-2c323ec39a3e" />

### Key DAX Planning
- **Avg Flights per Users**
- **Redemption Rate %**
- **Total Cancelled Customer**
- **Avg Cost Per Point**
- **Avg CLV**
- **Cancellation Rate %**
## Dashboard & Visualizations
The dashboard provides a comprehensive view of the collection:

Dashboard Overview
![baba4a35-2557-4903-a2ae-64feecac8aab](https://github.com/user-attachments/assets/7394642a-9f46-4dcd-a64d-ac1730dabfdc)

<img width="582" height="437" alt="image" src="https://github.com/user-attachments/assets/5239766f-3990-45c2-a51b-4eeb718fd5f6" />


- **KPI Cards**: Avg Flights per User (4.14); Redemption Rate (0.22%); Total Cancelled Customer (17K); Avg Cost Per Point (0.08); Avg CLV (7.99K); Cancellation Rate of 2018 Promotion (11.8%); Cancellation Rate of Standdard (2.2%).
- **Acquisition Trend (Line Chart+Bar Chart)**

## Insights & Recommendations

## Technologies
The project is created with:
- Google Collab
- MySQL
- PowerBI
