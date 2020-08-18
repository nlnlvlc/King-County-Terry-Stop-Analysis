# King County Terry Stop Prediction and Analyses


## Outline:
-----------------------------------------
    ├── data                       <- Copy of source data from King County Terry Stops
    ├── README.md                  <- The project layout (this file)
    ├── notebooks                  <- This includes the main notebooks covering EDA and Analysis of each feature as a predictor
    │
    ├── mod03_presentation.key      <- Non-technical presentation

## Introduction: 

In <a href='https://www.oyez.org/cases/1967/67'>Terry v. Ohio</a>, a landmark Supreme Court case in 1967-8, the court found that a police officer was not in violation of the "unreasonable search and seizure" clause of the Fourth Amendment, even though he stopped and frisked a couple of suspects only because their behavior was suspicious. Thus was born the notion of "reasonable suspicion", according to which an agent of the police may e.g. temporarily detain a person, even in the absence of clearer evidence that would be required for full-blown arrests etc. Terry Stops are stops made of suspicious drivers.

Terry Stops, most popularly known in the New York City Stop-and-frisk program, have long been criticized for disproportionately targeting Black and Latino citizens as well as having minimum impact on criminal behavior in the most heavily policed regions.

The goal for this project is to analyze the trends in King County's Terry Stops to identify potential predictors in Terry Stop subjects and the resulting actions taken by officers.

## Dataset:

The Government of Seattle, the seat of King County, Washington, self-publishes data pertaining to the county's City Business, Education, Finance, Community, and Public Safety public sector. Seattle publicly publishes officer reported Terry Stop data of 34521 unique stops (at the time of report) between  Oct 01, 2015 and May 07, 2019 sourced <a href='https://data.seattle.gov/Public-Safety/Terry-Stops/28ny-9ts8'>here</a>.  

The ISIC archive contained a total of 2285 malignant images. Since that is the class we are most interested in, only 2285 benign images were obtained to keep the classes balanced, for a total of 4570 images. 

These images were split into a train, test, and validation set. First, the images were split at an 80/20 ratio to create the train and test sets. Then another 80/20 train/validation split was made to create the validation set. 

Feature | Purpose | 
--- | :---: | 
Subject Age Group | Age Group of the Stopped Subject |
Subject ID | Unique IDs given to stopped subjects |
GO / SC Num | Num related to Terry Stop report type |
Terry Stop ID | Unique ID given to each unique Terry Stop |
Stop Resolution | Broad category to classify the end resolution decided by officer |
Weapon Type | Type of weapon discovered during Stop (if applicable) |
Officer ID | Unique ID given to each unique officer |
Officer YOB | Year of Birth of reporting officer |
Officer Gender | Gender of reporting officer |
Officer Race | Race of reporting officer |
Subject Perceived Race | Perceived race of individual subjects as reported by officer, not subject |
Reported Date | Date of stop |
Initial Call Type | Initial call type/activity that initiated stop as reported by officer |
Call Type | Revised call type reported at the end of each stop |
Officer Squad | Squad to which reporting officer is assigned |
Arrest Flag | Flags whether or not an arrest was made during stop |
Frisk Flag | Flags whether or not a Frisk was performed during stop |
Precint | Precint to which the reporting officer is assigned |
Sector | Sector to which the reporting officer is assigned |
Beat | Beat to which the reporting officer is assigned |

## Methodology:

The goal was to predict two main features: predict received race of the subject during each unique stop; and predict the percentage of performed Frisks during a stop.

First, we analyzed the population data for King County using publicly available Census estimates for each individual racial group in King County.

Race/Ethnicity | King County Census Estimates | 
--- | :---: | 
American Indian/Alaska Native| 4.0% |
Asian | 13.7% |
Black | 7.7% |
Hispanic | 6.6% |
Multi-Racial | 4.4% |
Other | 0.2% |
White | 66.3% |

Next we compared those estimates to the Perceived Subject Race of actual stops

Race/Ethnicity | King County Census Estimates | Terry Stop % |
--- | :---: | :---: |
American Indian/Alaska Native| 4.0% | 3.22% |
Asian | 13.7% | 3.05% |
Black | 7.7% | 30.86% |
Hispanic | 6.6% | 4.96% |
Multi-Racial | 4.4% | 2.39% |
Other | 0.2% | .44% |
White | 66.3% | 50.45% |

Since each unique stop is a associated with 23 features, predictions for race were split into three sets: Predicting Subject Race by Officer Race; Predicting Race by Total Office Demographic (age, race, gender, location); and Predicting Race by Additional (officer independent) Features. Our goal is to identify the strongest features that influence potential disparities in Subject Race.

Frisk predictions were assessed using only information that was gathered in specific stops to identify potential patterns within a unique stop which might lead to a Frisk being performed.

## Results:

The analysis shows a disproportionate number of Black subjects for Terry Stops. Despite making up on 7.7% of the King County population, 30.86% of all Teery Stop subjects were Black, a 300% overrepresentation (expected difference ranging between -.0012 and .0044%). Further analysis shows that White subjects, despite being the most populice group in King County, only make up a majority of stopped subjects if looking at subjects between the ages of 26 - 35, and even then only about 10% more than subjects in other racial groups.

Though a disparity is noticeable, officer race, demographics, and additional features were not great, individual predictors of the subject's race. The officer location (Precint, Sector, and Beat) however, did play a strong role in predicting the subject's race.

Frisk actions were able to be more strongly predicted looking at unique officers and ages, suggesting Frisks were more likely to be predicted by individual officers.

## Conclusion:

A <a href='https://5harad.com/papers/100M-stops.pdf?utm_source=The+Appeal&utm_campaign=3a050d7014-EMAIL_CAMPAIGN_2018_08_09_04_14_COPY_01&utm_medium=email&utm_term=0_72df992d84-3a050d7014-58394763'>study</a> examing over 90 Million traffic stops found that Black and Latinx subjects are stopped at nearly twice the rate as White subjects. While the study also found that rates of positive searches for contraband were fairly similar, they also noted that the threshold officers used to determine justifiable suspicion was much lower for Black and Latinx subjects. <a href='https://www.nap.edu/read/24928/chapter/9#252'>Other research</a> has shown that proactive policing in Black nieghborhoods has lead to more stops and police interactions with less than reasonable justification. This hyperfocus on Black neighborhoods and preventing crime contributes to higher rates of reported crime and Black subjects. Both studies highlight that these biases cannot be extrapolated from available data, alone.

From the provided data, we cannot identify a feature to predict the race of subjects or establish whether or not a stop was reasonable. When it came to Officer's race, sector, beat, and precinct, a significant number of entries were missing, potentially affecting their strength as a predictor of subjects stopped.
