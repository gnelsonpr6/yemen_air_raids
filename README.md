# The Conflict in Yemen: Predicting Civilian Casualties
Team: Max Bermont, Eileen Hartnett, Garrett Nelson

![Yemen Map](./images/yemen_map.png)

### Problem Statement 

Yemen is currently experiencing one of the world’s worst humanitarian crises. More than three and a half million people have been displaced by the ongoing conflict. Millions of people depend on humanitarian assistance for survival.

Doctors Without Borders/Médecins Sans Frontières (MSF) has treated over 119,000 people with injuries related to the war since March 2015. However, insecurity and access constraints prevented them from collecting reliable data on the humanitarian needs across the country.

Using an open source dataset produced by The Yemen Data Project, **we aim to build a model that predicts the number of civilian casualties to expect if a certain area is attacked.** This information will provide a more accurate prediction of how much aid to allocate towards medical resources, funding, and personnel based on location of the attack.  

### Contents:
- [Problem Statement](#Problem-Statement)
- [Background](#Background)
- [Executive Summary](#Executive-Summary)
- [Project Repo Contents](#Project-Repo-Contents)
- [Data Dictionary](#Data-Dictionary)
- [Data Source](#Data-Source)
- [Conclusions and Recommendations](#Conclusions-and-Recommendations)
- [References](#References)

### Background:

The conflict in Yemen involves a complicated civil war influenced by foreign actors that roots back to the Arab Spring in 2011. The uprising led to the removal of the authoritarian president, Ali Abdullah Saleh, who handed power over to Abdrabbuh Mansour Hadi. The transition however did not bring stability to Yemen. In 2014 the Houthi Shia Muslim group seized control of the northern Saada region, and the capital Sanaa, forcing President Hadi into exile. In 2015, a Saudi Arabian-led coalition, backed by the US, UK, and France, commenced air strikes against the Houthis. The Saudi-led coalition feared that Iran, which is a Shia-majority state,  was backing the Houthi rebellion, a claim that Iran denied. Within Yemen, divisions deepened. On the anti-Houthi side, militias include separatists seeking independence for south Yemen and factions who oppose the idea. Since the airstrikes began in 2015, more than 233,000 people have died and more than 20 million Yemenis are at risk of famine. 

**The role of Doctors Without Borders/Médecins Sans Frontières (MSF) in Yemen:**

Doctors Without Borders/Médecins Sans Frontières (MSF) medical projects in Yemen are among their biggest worldwide. 

The following text is from the [Doctors Without Borders website](https://www.doctorswithoutborders.org/what-we-do/countries/yemen#How%20we%E2%80%99re%20helping%20people%20caught%20in%20Yemen%E2%80%99s%20humanitarian%20crisis)

As an organization providing medical aid to people in Yemen, MSF worked in 13 hospitals and health centers and provided support to more than 20 health facilities across 12 governorates in 2018. However, repeated attacks on medical staff and structures during the year forced us to suspend activities in several areas.

Insecurity and access constraints also prevented us—and other organizations—from collecting reliable data on the nutritional and humanitarian needs across the country. Our teams treated 5,700 children for malnutrition across Hajjah, Sa’ada, Amran, Ibb, and Taiz governorates, but saw no signs of impending famine—contrary to what the UN and others were suggesting.

### Executive Summary

The project consists of three main notebooks: 
- The **data_clean.ipynb** notebook begins by importing and cleaning data downloaded from the data yemen project (more information on our data source below). Data cleaning involved renaming columns in a pythonic format, looking at value counts within columns, cleaning values within cells, looking at where we had null values and imputing nulls with either the mean or median if it made sense or with ‘unknown’ if categorical. We saved the cleaned data to the clean_df.csv file.
- The **eda_notebook.ipynb** notebook visually explores the relationships between the variables and the target.
- The **modeling_neural_network_casualties.ipynb**  notebook we build a regressive neural network that will predict civilian casualties of the Yemen conflict, when knowing the location of an air raid. 

### Project Repo Contents
**Main Contents:**
- [Raw Data](./data/raw_yemen_data.csv)
- [Clean Data](./data/clean_df.csv)
- [Data Cleaning Notebook](./main_notebooks/data_clean.ipynb)
- [EDA Notebook](./main_notebooks/eda_notebook.ipynb)
- [Modeling Notebook - Neural Network](./main_notebooks/modeling_neural_network_casualties.ipynb)
- [Plots and Images](./images)

**Appendix:**

We explored a few other models in the following notebooks
- [Modeling Notebook - ARIMA](./main_notebooks/modeling_arima.ipynb)
- [Modeling Notebook - Neural Network looking at Governorate](./main_notebooks/modeling_neural_network_governorate.ipynb)
- [Modeling Notebook - Random Forest](./main_notebooks/modeling_random_forest.ipynb)

### Data Dictionary

|Feature|Data type|Description|
|---|---|---|
|incident_id|int64|unique attack identifier|
|governorate|object|city attacked|
|district|object|district in city|
|area|object|area attacked|
|target|object|target attacked|
|main_category|object|category of attacked target|
|sub_category|object|sub-category of attacked target|
|min_air_raids|float64|min Air attacks|
|max_air_raids|float64|max Air attacks|
|civilian_casualties|int64|fatalities and injuries combined|
|fatalities|int64|number of deaths|
|woman_fatalities|int64|number of female deaths|
|child_fatalities|int64|number of child deaths|
|injured|int64|number of injuries|
|woman_injured|int64|number of women injured|
|child_injured|float64|number of children injured|
|confirmed_time|object|hour of the attack|
|time_of_day|object|morning, afternoon, or night|


### Data Source

**The data:**

The following text is from the Yemen Data Project, providing a brief background on the current conflict and an overview of the dataset:  https://yemendataproject.org/data.html 

The first data collection project by the Yemen Data Project focuses on the aerial bombardments in Yemen from March 2015 to date and includes detailed data on all air raids conducted by the military coalition led by Saudi Arabia and the United Arab Emirates, which also includes participation by Egypt, Morocco (until 2019), Jordan, Sudan, Kuwait, Qatar (until 2017) and Bahrain. The military coalition is backed by the United States and the United Kingdom, amongst other western nations, with the U.S. providing intelligence and logistical support and the UK supporting the coalition in every practical way short of engaging in combat. Both the U.S. and the UK have military personnel deployed at the Saudi command-and-control centre for coalition airstrikes.

The dataset lists the date of incident, geographical location, type of target, target category and sub-category, and, where known, time of day. Each incident indicates a stated number of air raids, which in turn may comprise multiple air strikes. It is not possible to generate an average number of air strikes per air raid as these vary greatly, from a couple of airstrikes up to several dozen per air-raid. YDP’s dataset records the unverified numbers of individual air strikes that constitute a recorded single air raid. For more explanation on air raids and air strikes please see our methodology.

Given the open source collection of the data, geolocation information of air raids is not available. However, location details are broken down from governorate to district and then area.

**Data Collection Methodology:** 

The following text is from the Yemen Data Project, explaining their methodology for collecting air raid and civilian casualty data: https://yemendataproject.org/methodology-1.html

**Air raids**
The data has been collected through open sources and cross-referenced using a wide range of information. These include local and international news agencies and media reports; social media accounts, including Twitter, Facebook, YouTube, and other video footage, and WhatsApp; reports from international and national NGOs; official records from local authorities; and reports by international human rights groups. Where independent reporting is not available, the data has been cross-referenced with sources from opposing sides to the conflict as to ensure the reporting is as accurate and impartial as possible.

The dataset lists target category and subcategory for each incident, apart from incidents where no information on the target is available. The target category chosen for each incident refers to the original use of the target, e.g. a school hit by an airstrike is referred to as a school building, with no further assessment on its use at the time of the airstrike or the circumstances that led to the airstrike.

As the data is collected using open sources and as there is a general lack of transparency from the parties to the conflict, as well as a lack of independent reporting on the ground, the data presented has been verified and cross-referenced to the extent possible. It is important to note, however, that due to the context of the current situation in Yemen there are significant challenges in accessing independent sources for verification of incidents. The data presents our best current understanding of the incidents included and are reported in good faith.

The data has been collected with the purpose of creating a statistical overview of the impact of the aerial bombardments in Yemen, especially in regard to geographical spread and its targeting.

**Air Strikes v Air Raids**
In YDP's data, an air raid refers to one incident. One air raid incident includes all air strikes on a single location within approximately one hour and therefore may comprise multiple airstrikes. Air strikes per air raid can vary greatly from a couple to several dozen per air raid. Due to the variations in quality of information on air strike counts and the challenges of verifying each individual strike on a single target or location, an air raid in YDP data, therefore, presents the most conservative estimate.

The required minimum for a recorded air raid incident is one airstrike. The maximum is the unverified number of air strikes, which is also noted in the details of the data. This unverified number of air strikes ranges from minimum airstrikes: 19,511 to maximum airstrikes: 45,563 for the first four years of the air campaign.

**Civilian casualties**
Casualty figures are a best estimate of numbers and are presented in good faith. YDP recognizes the limitations in the accuracy of the figures. Open source reporting of casualty numbers is often scarce or biased. Locations of bombings can be in very remote areas, or with limited access to multiple or independent sources that results in open source reporting of significantly different casualty numbers for the same incident. The process of the civilian casualty data collation includes in-depth research into incidents with civilian casualties, reviewing video material, published lists of victim names and cross-referencing with human rights groups and other entities collecting data on civilian casualties.

The research process is as meticulous as possible, and to remove bias or inflation in casualty numbers, the lowest reported casualty number is recorded in the data, unless verified numbers from human rights groups on the ground are available, in which case they are used. This means that the civilian casualty data we present is the least civilian casualties reported from airstrikes.


### Conclusions and Recommendations
- We used a neural network model to predict the number of casualties in order to appropriately allocate aid as real time information on the ground may not be that accurate in the midst of a crisis.  

- Based on the data provided we are able to predict the number of casualties based on location hit with approximately 90% accuracy.

- We would recommend further research to look at the impact of landmines and IEDs on the number of casualties in order to improve accuracy in predicting aid allocation.



### References
https://yemendataproject.org/ 

https://www.bbc.com/news/world-middle-east-44466574

https://www.npr.org/2021/02/08/965497266/critic-of-u-s-role-in-yemen-responds-to-bidens-plans-to-pull-back 

https://interactive.aljazeera.com/aje/2018/Saudi-Arabia-air-raids-on-Yemen/index.html#2019

https://www.doctorswithoutborders.org/what-we-do/countries/yemen#How%20we%E2%80%99re%20helping%20people%20caught%20in%20Yemen%E2%80%99s%20humanitarian%20crisis
