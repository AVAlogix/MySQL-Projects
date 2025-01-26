Data source: Dog breeds details
https://www.kaggle.com/datasets/warcoder/dog-breeds-details/data


```sql
#List all breeds by life expectancy
SELECT Name, min_life_expectancy, max_life_expectancy, (min_life_expectancy + max_life_expectancy) / 2 AS avg_life_expectancy
FROM dog_breeds
ORDER BY avg_life_expectancy DESC;

#List breeds that are good with children and other dogs
SELECT Name
FROM dog_breeds
WHERE good_with_children = 'Yes' AND good_with_other_dogs = 'Yes';

#dentify breeds with the highest energy levels
SELECT Name, energy
FROM dog_breeds
WHERE energy = (SELECT MAX(energy) FROM dog_breeds);

#Find breeds with minimal grooming needs
SELECT Name, grooming
FROM dog_breeds
WHERE grooming = (SELECT MIN(grooming) FROM dog_breeds);

#Find breeds that are highly protective and trainable
SELECT Name, protectiveness, trainability
FROM dog_breeds
WHERE protectiveness >= 4 AND trainability >= 4;

# Smallest breeds by weight (minimum male weight)
SELECT Name, min_weight_male, min_weight_female
FROM dog_breeds
WHERE min_weight_male = (SELECT MIN(min_weight_male) FROM dog_breeds);

#Largest breeds by weight (maximum male weight)
SELECT Name, max_weight_male, max_weight_female
FROM dog_breeds
WHERE max_weight_male = (SELECT MAX(max_weight_male) FROM dog_breeds);

# Shortest breeds
SELECT Name, min_height_male, min_height_female
FROM dog_breeds
WHERE min_height_male = (SELECT MIN(min_height_male) FROM dog_breeds);

# Tallest breeds
SELECT Name, max_height_male, max_height_female
FROM dog_breeds
WHERE max_height_male = (SELECT MAX(max_height_male) FROM dog_breeds);

#Calculate the average shedding level across all breeds
SELECT AVG(shedding) AS avg_shedding
FROM dog_breeds;

#Find breeds that are good with strangers and have high playfulness
SELECT Name, good_with_strangers, playfulness
FROM dog_breeds
WHERE good_with_strangers = 'Yes' AND playfulness >= 4;

#Compare breeds based on barking level
SELECT Name, barking
FROM dog_breeds
ORDER BY barking DESC;

#Find breeds with low drooling but high energy
SELECT Name, drooling, energy
FROM dog_breeds
WHERE drooling <= 2 AND energy >= 4;

#Filter breeds that require both low grooming and low shedding
SELECT Name, grooming, shedding
FROM dog_breeds
WHERE grooming <= 2 AND shedding <= 2;
