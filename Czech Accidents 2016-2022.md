### &nbsp;			Czech Accidents 2016-2022

&nbsp;	**Data Cleaning \& Data Preprocessing** 

**a. Importing the libraries needed**

**b. Importing and Reading the dataset**

**c. Checking the structure of the dataset i.e. rows and columns**

	**ii. Names of columns, datatypes and missing values %**

	**iia. The original dataset contains 707027 rows and 46 columns. Columns/Features that would be essential for the analysis were handpicked. czech\_copy is the name assigned to the new dataframe to be used.**

	**iii. czech\_copy contains 707027 rows and 27 columns**

	**iv. Dropna was applied to fix missing null values**

	**v. \[id and year\_of\_manufacture]'s datatype was converted from float64 to str**

	**vi. \[date]'s datatype was converted from str to datetime\[ns]; new columns\['Year\_Reported', 'Month\_Reported', 'Day\_Reported'] were created.**

	**vii. Checked for duplicates; there were no**



	**Data Visualizations** 

1. **Trend of Accidents over the years - from 2016 to 2019, there was a steady rise of accidents, but in 2020 due to covid restrictions worldwide, it dropped slightly. In 2021, it rose again but dropped in 2022. Since there is no data to show if that trend continued the downward trend, no insight can be made.**
2. **After further investigation it is shown that from 2016-2019 October recorded the highest number of accidents but since covid, it has been fluctuating** 
3. **The summary table gives a summary of events over the years\['Total\_killed\_Persons','Total\_severely\_injured\_persons', 'Total\_Slightly\_Injured\_Persons', 'Total\_Vehicles\_Involved'].**
4. **Accident Category - the most common accident type that occurs is the "collision with a moving non-rail vehicle" with over 130000 cases, it is followed closely by "collision with a vehicle parked, parked" with about ~121100 cases. Also looking at the most common accident type each year, it shows that "collision with a moving non-rail vehicle" was the most common between 2016(41.7%) - 2020(35.0%) and changing to "collision with a vehicle parked, parked" between 2021 -2022.**
5. **Main Causes of Accidents - "Driver not fully engaged while driving the vehicle" ie distracted drivers have been the main cause of most accidents in Czech over the years with it reaching its peak in 2020(20.5%).**
6. **Is the absence of traffic control also a main factor in these accidents - Yes, the lack of traffic control is main factor in these accidents, Fig 8 shows that there was no traffic control method at the site of these accidents(~71.8%). The traffic control vs Main cause of accidents table break it down further.**
7. **Is alcohol a contributing factor in these accidents - No, alcohol isn't a contributing factor in these accidents. No alcohol was found with the victims at the time of reports of a higher percentage of these accidents** 
8. **Category of Vehicles are involved - Passenger car without trailer ie private cars represent a higher percentage of the types of vehicles reported to be involved.**
8. 
**&nbsp;	Machine Learning**

1. **After a quick google search, it was discovered that certain machine learning techniques were suitable for this dataset, an example being RandomForest, Forecasting** 
1. 
**for this, RandomForestClassifier model was chosen for this** 

**2. New columns were created :**

	**total-injuries = severely\_injured\_persons + slightly\_injured\_persons**

	**crash\_severity = np.where(czech\_copy\['killed\_persons'] > 1, 'Fatal', np.where(czech\_copy\['severely\_injured\_person'] > 1, 'Severe', np.where(czech\_copy\['slightly\_injured\_persons' > 1, 'Slight', 'No Fatalities')))**

	**czech\_copy\[\['crash\_severity', 'total\_injuries']]**

	**features = \['number\_of\_vehicles', 'Month', 'Day']**

	**X = czech\_copy\[features]**

	**y = czech\_copy\['crash\_severity']**

**3. after applying the model, confusion\_matrix and classification\_report were used to verify the metrics of the model. The results of both show the following:**

	**a. The dataset used is severely imbalanced**

	**b. The model is ineffective when predicting severe or fatal accidents** 

	**c. Overall accuracy metric is misleading.**

**4. Applying the same model to the original dataset, the results shows thus:**

	**a. Class imbalance remains a core problem, it is a widespread issue in accident severity prediction(confirmed across many studies on similar datasets.**

	**b. The model still struggles to distinguish severity levels**

	**c. High accuracy as shown in the classification report is deceptive.**

**In summary, the dataset struggles with extreme class imbalance, this causes the model to overpredict non-fatal accidents while ignoring severe ones, rendering it unreliable for practical severity forecasting despite superficially good results. The model is reliable for spotting harmless accidents but unreliable for predicting harm.**

