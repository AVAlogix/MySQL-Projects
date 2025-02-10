# Employee Wellness Incentive Analysis

## Problem Statement
The objective of this analysis is to leverage employee health and lifestyle data to implement a reward system that encourages a healthier workforce. The initiative focuses on two primary goals:

1. Identifying employees with healthy behaviors and low absenteeism to qualify for a $1,000 bonus under the Healthy Bonus Program.
2. Equitably distributing a total insurance budget of $983,221 towards wage increases or annual compensation for non-smokers, promoting non-smoking habits and overall well-being.

## Methodology
The following steps were undertaken to process and analyze the dataset using Power BI:

1. **Data Integration**: The dataset, stored in SQL format, was imported into Power BI Desktop.
2. **Visualization Setup**:
   - Three card visuals were created to display key metrics, including average absenteeism time.
   - Four donut charts were used to illustrate categorical distributions, such as education levels, smoking status, pet ownership, and alcohol consumption.
   - Two line charts were designed to analyze absenteeism trends by month and day of the week.
   - A treemap was created to display reasons for absenteeism, sorted in descending order with a gradient applied for clarity.
   - A scatterplot visual was incorporated to examine the relationship between transportation expenses and daily workload.
   - A smart narrative visual was added to summarize the dashboard’s insights.
3. **Dashboard Refinement**: Various graphical elements were fine-tuned to ensure coherence and usability.
4. **Report Publication**: The final dashboard was published to Power BI Service for accessibility and further review.

## SQL Query Used
```sql
-- Join tables
SELECT * FROM hr.absenteeism_at_work a
LEFT JOIN reasons r
ON a.Reason = r.Reason_ID
LEFT JOIN compensation b
ON a.ID = b.ID;

-- find the healthiest employees for the bonus
Select * from Absenteeism_at_work 
where `absenteeism_at_work`.`Social drinker` = 0 and `absenteeism_at_work`.`Social smoker` = 0
and `absenteeism_at_work`.`Body mass index` <25 and
`absenteeism_at_work`.`Absenteeism time in hours` < (select AVG(`absenteeism_at_work`.`Absenteeism time in hours`) from Absenteeism_at_work); 

-- compensation rate increase for non-smokers/ budget: $983,221 so .68 increase per hour/ $1,414.4 per year
select count(*) as nonsmokers from Absenteeism_at_work
where `absenteeism_at_work`.`Social smoker` = 0;

-- optimize this query
select 
a.ID,
r.Reason,
`Month of absence`,
`Body mass index`,
case when `Body mass index` <18.5 then 'Underweight'
     when `Body mass index` between 18.5 and 25 then 'Healthy Weight'
	 when `Body mass index` between 25 and 30 then 'Overweight'
	 when `Body mass index` >30 then 'Obese'
	 else 'Unknown' end as BMI_Category,
case when `Month of absence` IN (12,1,2) Then 'Winter'
     when `Month of absence` IN (3,4,5) Then 'Spring'
	 when `Month of absence` IN (6,7,8) Then 'Summer'
	 when `Month of absence` IN (9,10,11) Then 'Fall'
	 else 'Unknown' end as Season_Names,
`Month of absence`,
`Day of the week`,
`Transportation expense`,
`Education`,
`Son`,
`Social drinker`,
`Social smoker`,
`Pet`,
`Disciplinary failure`,
`Age`,
`Work load Average/day`,
`Absenteeism time in hours`
from Absenteeism_at_work a
left join compensation b
on a.ID = b.ID
left join Reasons r on
a.Reason = r.Reason_ID;
```

## Key Insights

### Employee Demographics & Absenteeism
   - Pie charts highlight absenteeism trends across various employee demographics, including education level, smoking status, drinking habits, and pet ownership.

### Absenteeism Trends
   - Line charts reveal fluctuations in absenteeism by month and day of the week, with notable spikes on Mondays (day 2).

### Absenteeism Causes
   - A bar graph categorizes reasons for employee absences, such as medical consultations, dental visits, and various health conditions. Understanding these causes can aid in developing targeted wellness programs.

### Transportation Costs & Workload Correlation
   - A scatterplot analysis suggests that transportation expenses rise in tandem with increased workloads. This may indicate a preference for costlier commuting methods on busier days due to time constraints or stress levels.

### Seasonal & Health Trends
   - Absenteeism data is analyzed across seasons to determine seasonal patterns.
   - Employee health is assessed through Body Mass Index (BMI) classifications, identifying underweight, healthy weight, overweight, and obese categories.

## Dashboard Snapshot
![absenteeism](https://github.com/user-attachments/assets/aba02fb9-188a-4b36-b5c9-f5c660d1347b)

## Data Source
- **Dataset Name**: Employee Health & Absenteeism Data
- **Source**: *https://github.com/Gaelim/work_incentive_program* *https://www.youtube.com/watch?v=oQSX_y2wfhc*
- **Format**: csv files


## Conclusion
The insights derived from this analysis provide valuable guidance for HR teams in optimizing workforce management strategies. By identifying key absenteeism trends, rewarding healthy behaviors, and promoting non-smoking initiatives, organizations can enhance employee well-being, reduce absentee rates, and improve overall productivity. Future recommendations include implementing wellness programs, optimizing work schedules, and introducing targeted incentives to foster a healthier workplace culture.

