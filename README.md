# Trigger Selection Analysis for Anticipatory Action (AA) - Djibouti 2024

Author - Nitin Magima

Date - March 2024

Version - 1.0

### Purpose
The Jupyter Notebook aims to support the AA trigger selection analysis in Djibouti during the relevant seasons such as March-April-May (MAM), July-August-September (JAS), and October-November-December (OND).

### Audience
Tailored for government officials in agriculture, water resources, and disaster management sectors.

### Objectives
To provide an in-depth analysis of trigger selection during MAM, JAS, and OND using the Design Tool API.

### Summary

There are two questions that a decision-maker needs to keep in mind while picking triggers for different thresholds.

- How often does the decision-maker want the AA mechanism to trigger?
A decision-maker must decide how often the funds need to be disbursed and the size of the disbursement across the project's lifespan. For example, if a project is over ten years, funds can be disbursed from a $10 million fund in the following thresholds, depending on the frequency. 

1 in 3 years (funds are possibly disbursed three times)
1 in 5 years (funds are possibly disbursed two times)
1 in 10 years (funds are possibly disbursed one time)

During the deployment and monitoring of AA, a decision-maker should be aware that the trigger mechanism meeting the criteria is independent of the disbursement frequency. The frequency of triggers can be assessed on a month-to-month basis or year-to-year basis, depending on the stakeholders’ preferences. 

- Does the threshold cover previous historical loss events or bad years considered important by the decision maker?
Another factor to consider while defining the threshold is the historical loss events. Decision-makers use the historical loss events collected from research and stakeholder engagement. Historical loss events are gathered from relevant stakeholders through participatory processes. These events are then used to define different thresholds for drought severity and frequency. 

The Jupyter Notebooks produces heatmaps, histograms, and box plots for the respective seasons. For each season, it focuses on the high severity and moderate severity trigger levels and further divides for each severity at the national and regional levels. It also performs risk analysis at the national and regional levels. 

For each severity level during the stakeholder workshop, bad years highlighting years affected by drought were collected. Using these bad years and a range of frequencies ideally from 5 to 50, the Design Tool API pulls from the design tool and produces a table, with the data set description seen below. 

The data is filtered for the years that have not been triggered and a list is provided. The data is then filtered only for the years that have been triggered and a heatmap is produced. Looking at the heatmap, the user can decide what would be appropriate triggers for high severity at the national level, and similarly for the regional level for each season.  

After that, if the user wants to decide what kind of threshold protocol should be used above which the forecast should be still triggered, the trigger difference has been shown here as a box plot and also as quantile data.

The Jupyter Notebooks then produces analysis to inform strategies for decision-makers with varying risk preferences using Expected Value (EV) and Risk-Adjusted Return on Prediction (RARoP).

EV is calculated by assigning a value or cost to each type of decision outcome ('Worthy Action', 'Act in Vain', 'Worthy Inaction', and 'Fail to Act'). 

RARoP involves adjusting the "return" (or benefit) of correct decisions ('Worthy Action' and 'Worthy Inaction') by the "volatility" (or uncertainty, represented by the proportion of incorrect decisions, 'Act in Vain' and 'Fail to Act') and the decision-maker's risk tolerance.

The Jupyter Notebook also analyzes and visualize three critical metrics—accuracy, sensitivity, and specificity—across different frequencies for each administrative name within a dataset. These metrics help evaluate the performance of the forecast for decision-making. Here's a summary of what each metric represents and how they are derived:

Accuracy
Accuracy measures the proportion of all predictions that the model got right; it's the most intuitive performance measure. It is calculated as the sum of true positives ('Worthy Action') and true negatives ('Worthy Inaction') divided by the total number of cases. This metric gives a general idea of the model's performance across both positive and negative classes but doesn't provide details on how it performs within each class.

Sensitivity
Sensitivity, also known as the True Positive Rate or Recall, measures the proportion of actual positives that are correctly identified by the model. It is calculated by dividing the number of true positives ('Worthy Action') by the sum of true positives and false negatives ('Fail to Act'). Sensitivity is crucial for cases where missing a positive case (e.g., failing to identify a disease in a patient) has significant consequences.

Specificity
Specificity, or the True Negative Rate, measures the proportion of actual negatives that are correctly identified by the model. It is calculated by dividing the number of true negatives ('Worthy Inaction') by the sum of true negatives and false positives ('Act in Vain'). Specificity is particularly important in situations where falsely identifying negatives as positives (e.g., falsely diagnosing a healthy person as sick) can lead to unnecessary anxiety or treatment.

Decision Maptools
1. [OND season](https://iridl.ldeo.columbia.edu/fbfmaproom2/djibouti-ond)
1. [JAS season](https://iridl.ldeo.columbia.edu/fbfmaproom2/djibouti)
1. [MAM season](https://iridl.ldeo.columbia.edu/fbfmaproom2/djibouti-mam)

IMPORTANT - DISCLAIMER AND RIGHTS STATEMENT
This is a set of scripts written by the Financial Instruments Team at the International Research Institute for Climate and Society (IRI) part of The Columbia Climate School, Columbia University They are shared for educational purposes only.  Anyone who uses this code or its functionality or structure assumes full liability and should inform and credit IRI.


## YAML Description

In the config.yaml file, you will see that the structure of the YAML file is such that each country's map room has 
been listed, along with these variables.

1. maproom: to access the appropriate maproom
2. country: country name. The difference between the maproom variable and the country variable is that the maproom 
sometimes has the season hyphenated in it. This is why the maproom variable from the country variable has to be different
3. target_season: The target season is the season the maproom targetsmode: mode refers to the geographic level of the 
data. If you want the full country, it would be ‘0’, the next level (probably region) would be ‘1’, district (this case) 
would be ‘2’, and so on for as many levels are configured. Different admin levels are described in terms of both 
name and key, where the name is the admin level name and the key is the admin level in integer.
4. season:This field refers to the season you need data from, for now, all maptools have just one season, 
so this field will be always season1. This does not need to be changed. 
5. predictor=pnep: This refers to the variable that is predicting the season, in this case, ‘pnep’ refers to the IRI 
forecast result. It can change to total rainfall, average rainfall, or any other data set included in the tool. 
You can review all available predictors in the dropdown menu in the tool. To find the ID to use for a given variable, 
see the config file https://github.com/iridl/python-maprooms/blob/master/fbfmaproom/fbfmaproom-sample.yaml
6. predictand: This refers to the variable on which the forecast result will be compared and used to calculate 
the skill. It is usually labeled as bad years since we want to know how many of the known bad years are captured by 
the forecast. The available options are the same as for predictor (see above)
7. year: year of the season
8. issue_month0: the month you want the forecast result from. It is important to note that month counting starts at zero.
9. freq: This refers to the frequency of the event you want the forecast for. It corresponds to the ‘frequency of event’
slider in the tool
10. include_upcoming=false: This field states that the forecast for the upcoming season is not included in the 
historical statistics used to calculate the forecast or the skill. We usually include only past seasons in the 
historical data. 
11. design_tool: link to the design/maptool. Updates in the "Additional Resouces" tab in the front end
12. report: link to the AA reports.Updates in the "Additional Resouces" tab in the front end
13. username: use username if the maproom is behind a sign-in wall
14. password: use username if the maproom is behind a sign-in wall
15. threshold_protocol:The threshold protocol is decided during the respective country working groups to see if 
additional points are required to determine whether the forecast will be triggered or not
16. need_valid_keys: assign value True, without quotes (don't use "True"), if using admin1_list
17. admin1_list: this field refers to the list of keys or admin level 1 the AA project is focusing on. The admin1 list 
is there in case only certain admin1 units need to be shown in the trigger monitoring table, this list needs to be 
updated. To see the full list of keys, go to the data folder and see the respective maproom CSV file. If it's not there, 
you can use the get_admin1_data.py to create the CSV files in the data folder, and then open the CSV file that reflects 
your maproom name to update the admin1_list.

IMPORTANT - DISCLAIMER AND RIGHTS STATEMENT
This is a set of scripts written by the Financial Instruments Team at the International Research Institute for Climate and Society (IRI) part of The Columbia Climate School, Columbia University They are shared for educational purposes only.  Anyone who uses this code or its functionality or structure assumes full liability and should inform and credit IRI.