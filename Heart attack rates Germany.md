Source of Dataset: Heart Attack in Youth Vs Adult in Germany -

Heart Attack Predictions in Youth Vs Adult in Germany(StateWise) By Ankush Panday

DOI:10.34740/kaggle/dsv/10404540

```sql
SELECT *
FROM heatattacks.heart_attack_germany;

#State Comparison: Which states have the highest or lowest heart attack cases?
SELECT 
    State, 
    SUM(Heart_Attack_Incidence) AS Total_Heart_Attack_Cases
FROM  heart_attack_germany
GROUP BY State
ORDER BY Total_Heart_Attack_Cases DESC;

#Youth vs. Adult: Are heart attacks more common in adults than youth?
SELECT 
    Age_Group, 
    SUM(Heart_Attack_Incidence) AS Total_Heart_Attack_Cases
FROM heart_attack_germany
WHERE Age_Group IN ('Youth', 'Adult')
GROUP BY Age_Group
ORDER BY Total_Heart_Attack_Cases DESC;

# Gender Trends: Do men or women experience more heart attacks?
SELECT 
    Gender, 
    SUM(Heart_Attack_Incidence) AS Total_Heart_Attack_Cases
FROM heart_attack_germany
GROUP BY Gender
ORDER BY Total_Heart_Attack_Cases DESC;

#Lifestyle Impact: How does smoking or diet quality affect heart attack rates?
SELECT 
    Smoking_Status, 
    Diet_Quality, 
    SUM(Heart_Attack_Incidence) AS Total_Heart_Attack_Cases
FROM heart_attack_germany
GROUP BY Smoking_Status, Diet_Quality
ORDER BY Total_Heart_Attack_Cases DESC;

#Risk Factor Analysis: Which factors (BMI, hypertension, cholesterol, etc.) are strongly linked to heart attacks?
SELECT 
    AVG(BMI) AS Avg_BMI,
    SUM(Hypertension) AS Total_Hypertension_Cases,
    AVG(Cholesterol_Level) AS Avg_Cholesterol_Level,
    SUM(Diabetes) AS Total_Diabetes_Cases,
    SUM(Family_History) AS Total_Family_History_Cases,
    SUM(Heart_Attack_Incidence) AS Total_Heart_Attack_Cases
FROM heart_attack_germany;

#Statewise Patterns: Are rural or urban areas more affected in certain states?
SELECT State, Urban_Rural, SUM(Heart_Attack_Incidence) AS Total_Heart_Attack_Cases
FROM heart_attack_germany
GROUP BY State, Urban_Rural
ORDER BY State, Total_Heart_Attack_Cases DESC;

# Time Trends: Have heart attack rates increased or decreased over the years?
SELECT Year, SUM(Heart_Attack_Incidence) AS Total_Heart_Attack_Cases
FROM heart_attack_germany
GROUP BY Year
ORDER BY Year ASC;

#Socioeconomic Status Impact: Does being in a low-income group increase heart attack risk?
SELECT Socioeconomic_Status, SUM(Heart_Attack_Incidence) AS Total_Heart_Attack_Cases
FROM heart_attack_germany
GROUP BY Socioeconomic_Status
ORDER BY Total_Heart_Attack_Cases DESC;

#Calculate Heart Attack Rate Per Year Per Location
SELECT Year, State, Urban_Rural, SUM(Heart_Attack_Incidence) AS Total_Heart_Attack_Cases
FROM heart_attack_germany
GROUP BY Year, State, Urban_Rural
ORDER BY Year ASC, State, Urban_Rural;
