# Usa-Mortality-Analysis-from-Kaggle-via-Pyspark
Application that analyzes the USA Mortality Dataset From Kaggle using Pyspark, Flask, CherryPy and Chart.js

Kaggle is a website that contains various types of datasets online and free, which one can analyze or apply machine learning techniques. 
This specific contains information about the USA MORTALITY for the last 11 years (2005-up to 2015). 
For each year, there is a csv file with the columns of the dataset for the various fields and for each there is a numeric code. Numeric codes are mapped to values via a json file. The dataset contains information on the age, sex, educational level and origin of the deceased, as well as codes on the cause of death, etc.
To match codes with values custom python dictionaries are created, which were used to better interpret the results of sparksql queries and diagrams.

Analysis of mortality data is essential to understanding the circumstances of death and the complexity of the issue across a country. The US government uses this data to determine life expectancy and to understand how death in the US is different from the rest of the world. In this dataset one can look for macroeconomic trends or analyze unique circumstances to look for answers to one of the great mysteries of existence.

The questions that are attempted be answered in this project are:
<b>A)</b> The life expectancy for the decade 2005-2015 and the fluctuations per year.
<b>B)</b> Comparison of causes of death such as Deaths from guns vs Automobiles
accidents.
<b>C)</b> Finding the most common disease as a cause of death.
<b>D)</b> Deaths per breed and their causes.

<b>A.</b>

The information provided by the dataset on the age of the deceased does not indicate the exact age of death of each person, but is divided into age intervals. The most accurate intervals are 5 years apart and are in the column titled age_recode_12. Therefore, we used this for our research.

The data are as follows:

01: Under 1 year (includes not stated infant ages)

02: 1 - 4 years

03: 5 - 14 years

04:15 - 24 years

05:25 - 34 years

06:35 - 44 years

07:45 - 54 years

08:55 - 64 years

09:65 - 74 years

10:75 - 84 years

11:85 years and over

12: Age not stated


For the calculation of the life expectancy of each year, the weighted average of the sum of each average value of the above sets was calculated on the number of deaths that belonged to each of them.
That is,
1 * (Number of deaths in the total age Under 1 year) + 3 * (Number of deaths in the total age 1-4 years) + ... + 85 * (Number of deaths in the total age 85 years and over)
               / (total number of deaths)

The results are as follows:

![alt text](https://github.com/AM1241/Usa-Mortality-Analysis-from-Kaggle-via-Pyspark/blob/main/images/img1.png?raw=true)

2005: 70.5 years

2006: 70.4 years

2007: 70.5 years

2008: 70.7 years

2009: 70.6 years

2010: 71.0 years

2011: 71.08 years

2012: 71.1 years

2013: 71.2 years

2014: 71.16 years

2015: 71.19 years

It makes sense to have a significant margin of inaccuracy in the price of each year, due to the lack of more specific data.

<b>B.</b>

The following is a comparison of two of the most discussed causes of death in a society, as the measures to deal with them depend to a large extent on the human factor. There were 353159 deaths caused by gunfire and 429525 due to a car accident in 11 years 2005-2015.

2005
deaths of firearms are: 30426 deaths of vehicles are: 45711
2006
deaths of firearms are: 30612 deaths of vehicles are: 45694
2007
deaths of firearms are: 30964 deaths of vehicles are: 44299
2008
deaths of firearms are: 31335 deaths of vehicles are: 40129
2009
deaths of firearms are: 31073 deaths of vehicles are: 36473
2010
deaths of firearms are: 31382 deaths of vehicles are: 35590
2011
deaths of firearms are: 31961 deaths of vehicles are: 35519
2012
deaths of firearms are: 33158 deaths of vehicles are: 36679
2013
deaths of firearms are: 33208 deaths of vehicles are: 35650
2014
deaths of firearms are: 33184 deaths of vehicles are: 35688
2015
deaths of firearms are: 35856 deaths of vehicles are: 38093

![alt text](https://github.com/AM1241/Usa-Mortality-Analysis-from-Kaggle-via-Pyspark/blob/main/images/img2.png?raw=true)

<b>C.</b>

In 11th, the two main causes of death each year were searched from the field with the most detailed description of causes 358_cause_recode (456 items). It is noteworthy that in each year the two main causes are each time the same (All other forms of chronic ischemic heart disease (I20, I25.1-I25.9) and Of trachea, bronchus and lung (C33-C34)).

The results of each year are as follows:

2005:
All other forms of chronic ischemic heart disease (I20, I25.1-I25.9): 228656
Of trachea, bronchus and lung (C33-C34): 159405

2006:
All other forms of chronic ischemic heart disease (I20, I25.1-I25.9): 219304
Of trachea, bronchus and lung (C33-C34): 158786

2007:
All other forms of chronic ischemic heart disease (I20, I25.1-I25.9): 210552
Of trachea, bronchus and lung (C33-C34): 158889

2008:
All other forms of chronic ischemic heart disease (I20, I25.1-I25.9): 208809
Of trachea, bronchus and lung (C33-C34): 158808

2009
All other forms of chronic ischemic heart disease (I20, I25.1-I25.9): 200067
Of trachea, bronchus and lung (C33-C34): 158269

2010:
All other forms of chronic ischemic heart disease (I20, I25.1-I25.9): 196116
Of trachea, bronchus and lung (C33-C34): 158425

2011:
All other forms of chronic ischemic heart disease (I20, I25.1-I25.9): 192773
Of trachea, bronchus and lung (C33-C34): 157148

2012:
All other forms of chronic ischemic heart disease (I20, I25.1-I25.9): 190869
Of trachea, bronchus and lung (C33-C34): 157647

2013:
All other forms of chronic ischemic heart disease (I20, I25.1-I25.9): 190265
Of trachea, bronchus and lung (C33-C34): 156369

2014:
All other forms of chronic ischemic heart disease (I20, I25.1-I25.9): 186696
Of trachea, bronchus and lung (C33-C34): 155749

2015:
All other forms of chronic ischemic heart disease (I20, I25.1-I25.9): 188413
Of trachea, bronchus and lung (C33-C34): 153952

<b>D</b>

In the last question we looked for the causes of death of each human race separately for the whole 11 years. Each entry was separated according to the race field (16 items), which contains the most data in relation to the other fields in the dataset that relate to human race indication. An important observation is that this field does not separate the race of Spanish origin from the whites.
Below are some examples of visualizing the results of four races from those in this field, the dataset.


![alt text](https://github.com/AM1241/Usa-Mortality-Analysis-from-Kaggle-via-Pyspark/blob/main/images/img4.1.png?raw=true)


Whites: The total number of deaths throughout the 11 years is 23,703,335.

Unusual diseases: 4,223,428,

Ischemic heart disease: 3,741,934,

Non-ischemic heart disease: 1,780,478,

Tracheal cancers: 1,507,723,

Chronic Respiratory Problems: 1,415,205


![alt text](https://github.com/AM1241/Usa-Mortality-Analysis-from-Kaggle-via-Pyspark/blob/main/images/img4.2.png?raw=true)


Colored: The total number of deaths throughout the 11 years is 3,258,257.

Unusual diseases: 528,724,

Ischemic heart disease: 454,375,

Non-ischemic heart disease: 237,692,

Cerebrovascular diseases: 237,692,

Tracheal cancers: 182,243



![alt text](https://github.com/AM1241/Usa-Mortality-Analysis-from-Kaggle-via-Pyspark/blob/main/images/img4.3.png?raw=true)


Native American: The total number of deaths throughout the 11 years is 174,392.

Unusual diseases: 30,221,

Ischemic heart disease: 21,037,

Unspecified accidents: 11,961,

Diabetes: 9,749,

Other malignancies: 8,890




![alt text](https://github.com/AM1241/Usa-Mortality-Analysis-from-Kaggle-via-Pyspark/blob/main/images/img4.4.png?raw=true)


Filipinos living in the US: The total number of deaths throughout the 11 years is 106,432.

Ischemic heart disease: 17,866,

Unusual diseases: 14,391

Cerebrovascular diseases: 8,825,

Other malignancies: 7,230

Tracheal cancers: 6,774
