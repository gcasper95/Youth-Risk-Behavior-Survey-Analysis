# Youth Risk Behavior Survey Analysis

**Date:** September 1st, 2025
<br>
**Author:** Gabriel Casper
<br>
**Email:** gcasper95@gmail.com
<br>
<br>
This report 
<br>

## Data Information

### Dataset

Youth Risk Behavior Surveillance System (YRBSS)
+ The Youth Risk Behavior Surveillance System is the largest public health surveillance system in the U.S. that monitors multiple health-related behaviors among high school students. While the first survey was taken in 1990, the earliest publicly available data is from 1991. The data is gathered, organized, and published in biennial periods, with the latest data being from 2023. The dataset includes the survey year, weight, stratum, primary sampling unit, record, age, sex, race, sexual orientation, and survey answers. The combined dataset user's guide can be found [here](https://www.cdc.gov/yrbs/media/pdf/2023/2023-YRBS-SADC-Documentation.pdf). An additional data user's guide containing analytical methods and documentation can be found [here](https://www.cdc.gov/yrbs/media/pdf/2023/2023_National_YRBS_Data_Users_Guide508.pdf).

<br>
The Dataset link is available below:
<br>
<br>

2023 Youth Risk Behavior Survey: [link](https://www.cdc.gov/yrbs/data/index.html#cdc_data_surveillance_section_2-combined-high-school)

### Data Preprocessing

Power BI
1. In the table titled 'Full Table', categorical columns for race, sex, and sexual identity were changed from type decimal number to type text, and the values were replaced with their corresponding variables found in the [2023 YRBS Combined Datasets User's Guide](https://www.cdc.gov/yrbs/media/pdf/2023/2023-YRBS-SADC-Documentation.pdf).
2. A second table titled 'Analysis Table' was created by duplicating the altered 'Full Table' in step one and removing all fields that were not used for visual analysis. The table was linked to the 'Full Table' with a cardinality of one-to-one and a bi-directional cross filter. The 'Analysis Table' was used for statistical analysis in Python.
3. Three separate dimensional tables were created for race, sex, and sexual identity. The dimensional tables were linked to the 'Full Table' with a cardinality of one-to-many and a singular direction cross filter from the dimensional tables to the 'Full Table'. The dimensional tables were used as a filtering method to eliminate any instances of blanks in visuals utilizing categorical fields.
4. In the DAX query view, 11 queries were created to return all fields in the 'Analysis Table' by year, from 2003 to 2023. The query results were copied in their entirety and pasted into Google Sheets and all dpulicated headers were removed. The table was then exported into CSV format for statistical analysis in Python.
5. In the table titled 'Heatmap Stats', imported from Python, the x and y column values were replaced with their corresponding Power BI risk behavior text descriptions used in the visualizations. The five columns containing the statistical values were unpivoted, resulting in two columns (Attribute & Value). The non-alphabetical characters in the attribute column were replaced with commas and split into three separate columns using the comma as a delimiter. A custom column named description was created in 'Heatmap Stats' to describe the statistic, the dependent variable, and the conditional variable. A second custom column named pairing label was created in 'Heatmap Stats' describing the risk behaviors. A third custom column named attribute names was created in 'Heatmap Stats' describing the statistical test used. Select values in the value column were replaced with null to remove them from the ranking visualizations, as the risks being assessed could not happen without the corresponding risks taking place.
<br>

Python
1. After importing the 'Analysis Table' created in Google Sheets, the dichotomous values in the survey answer fields were changed from one and two to one and zero for accurate mathematical operations.
2. A subset of the data was created by removing all non-dichotomous fields, with the purpose of being used in an unweighted pearson correlation heatmap.
3. After reviewing the weighted phi correlation heatmap, values between 0.40 and 0.99 were assessed for statistical analysis. Select pairings that met this criteria were excluded from analysis as thier interpretation would not be meaningful or valid. The reasons include, but are not limited to pairings that are considered preventative and not risk behaviors, pairings that have conceptual complexity beyond the scope of analysis, and pairings that have nested behaviors that cannot account for external factors influencing the dependent behaviors.
4. The pairings that were statistically analyzed were rounded to 4 decimal places prior to CSV format exporting as a way to provide enough detail for meaningful comparison while avoiding unnecessary complexity.
<br>

## Analysis Tools and Methods

### Tools

| Program/Package | Utilization |
|:--|:--|
|Google Sheets| Data restructuring, organization, and export |
|JupyterLab | Python code display, statistical analysis, & visualizations |
|Matplotlib | Graph creation & customization |
|NumPy | Mathematical calculations |
|Pandas | Data manipulation |
|Power BI| Data visualization & report generation |
|Seaborn | Graph creation & customization |

### Methods

1. Define Analysis Goal
   + Identify national risk behavior trends over 20 years (or using the available data) by identity categorization along with uncategorized risk behavior correlations to provide insight into which behaviors represent emerging or persistent problem areas for educators and policy makers so that they can prioritize interventions and resources to reduce the likelihood of their negative consequences.
2. Formulate Research Questions
   +  Which risk behavior trends are increasing or decreasing?
   +  Which demographic groups have a greater percentage of participation in certain risk behaviors?
   +  Which risk behaviors commonly co-occur, suggesting shared underlying factors?
   +  Do certain risk behaviors increase the likelihood of participation in other risk behaviors?
3. Exploratory Data Analysis (EDA)
   + Created 41 line graphs displaying weighted risk behavior participation trends for race, sex, and sexual identity in the following risk behavior categories:
     + Substance Risk Behaviors (15)
     + Sexual Risk Behaviors (10)
     + Mental Health Risk Behaviors (6)
     + Violence Risk Behaviors (10)
   + Created custom tooltips for each risk behavior category to display the total number of individuals who gave an answer, the total number of individuals who partook in the risk behavior, and the weighted percentage of participation based on demographic group.
   + Analyzed the correlation between the 41 risk behaviors using both the unweighted and weighted phi coefficient. Risk behavior pairs with a phi coefficient of 0.40 to 0.99 and found to have a meaningful/valid interpretation were measured for conditional probability, risk ratio, and odds ratio.
   + Created 3 bar graphs to display the top 10 paired risk factors by conditional probability, risk ratio, and odds ratio.

## Results

1. The majority of substance risk behavior trends are decreasing. On average, males have a higher percentage of participation than females, American Indian/Alaska Natives and Native Hawaiians/Other Pacific Islanders have a higher percentage of participation than other races, and those who identified as being part of a sexual minority had a higher percentage of participation than those who identified as heterosexual.
2.  The sexual risk behaviors contain increasing, decreasing, and stagnant trends. The percentage of individuals who have had sex and those who have had sex with 4 or more partners has decreased in the past 20 years for both race and sex demographics. The percentage of individuals who have experienced dating violence and have been forced to have sex has slowly increased for all demographics. Dating violence has increased since 2017 for all demographics except those who identified as Native Hawaiian/Other Pacific Islander.
3.  The majority of mental health risk behavior trends are increasing for all demographics, with injurious suicide attempts being the exception. Females had a higher rate of participation than males for all risk behaviors in this category. Individuals who identified as being a sexual minority or other/questioning had significantly higher participation rates than individuals who identified as heterosexual in all risk behaviors in this category. Individuals who identified as multiple races were among the highest percentage of participation in all risk behaviors in this category. 
4.  The violence risk behaviors contain increasing, decreasing, and stagnant trends. While the percentages of individuals who participated in physical fights and physical fights at school has decreased, the percentage of individuals who had a school absence for safety has increased for race and sex demographic groups. Females experienced more bullying in school and online than males, while males experienced more physical risk behaviors than females. Those who identified as being a sexual minority or other/questioning had higher percentages in all categories compared to those who identified as heterosexual.
5.  Almost every risk behavior trend shows a noticeable deviation in the year 2021, coinciding with the lockdowns and online schooling implemented as a direct result of COVID-19. While most risk behaviors showed a decrease from the previous survey period, a few risk behaviors increased.
6.  The top 10 paired risk behaviors for conditional probability are all substance related. The substance risk behaviors do not suggest that any particular substance is a gateway drug. There is a clear boundary between using substances commonly referred to as hard drugs increasing the probability of using other hard drugs, and using substances commonly referred to as soft drugs increasing the probability of using other soft drugs.
7.  The top 10 paired risk behaviors for risk ratio are substance related except for attempted suicide given considered suicide. The top 5 pairings for risk ratio are all commonly referred to as hard drugs and show that individuals are anywhere from 37 times to 90 times more likely to participate in a risk behavior given that its pairing has already been participated in.
8.  The top 10 paired risk behaviors for odds ratio, which determines the strength of their correlation, are substance related except for attempted suicide and considered suicide.

## Discussion

### Limitations

While the Youth Risk Behavior Survey provides useful and impactful information, the data is not completely accurate and credible. Several factors limit the accuracy of the data, including but not limited to:

+ Students misreporting behaviors due to recall bias or intentional misreporting due to social desirability bias and/or embarrassment.
+ The survey excludes high school dropouts, homeschooled individuals, and those who were absent on the day the survey was taken, thus skewing the data to favor those still in school and not absent.
+ Differences in participation rates among states, districts, and demographic subgroups which doesn't completely represent the national population, even when weights are applied.
+ Questionnaire wording and the available response options have changed over the past 20 years, affecting trend comparability.
+ The survey questions were reduced to yes/no responses, oversimplifying nuanced behaviors.

### Recommendations for Further Analysis

The following actions could be taken to improve data accuracy and identification of problem areas for intervention:

+ Prior to conducting the survey, proctors could remind students that survey questions should be answered truthfully for accurate data analysis, with emphasis on the fact that no identifying information is recorded and that there is no penalty or consequence for answering truthfully. While there is no penalty or consequence to the students for inaccurate answers, proctors could explain the value of and application of accurate data as it pertains to providing education and resources to areas where certain risk behaviors are more problematic.
+ Data collection could be extended beyond the current areas the survey is conducted (major metropolitan areas) by incorporating smaller cities and towns, increasing the likelihood that any statistics conducted would be more representative of the high school population than the current areas alone.
+ Data collection could be altered to offer homeschooled individuals the ability to partake in the survey, as well as allowing students who were absent on the day the survey was conducted the opportunity to complete the survey when they are present.
+ Additional categorization questions could be added to the survey in regards to certain risk behaviors, including but not limited to reasons for partaking in said risk behaviors, how the risk behavior has affected them, and whether or not the student would seek help if risk mitigating resources were offered.

## How to Reproduce the Analysis

1. Install the software and packages listed in the table below:
   1. Note: The specific integrated development environment (IDE) used was Anaconda Navigator for all Python related software and packages. All python related code should operate without issue in other IDEs that utilize Python. Anaconda Navigator can be downloaded [here](https://www.anaconda.com/download).
   2. Note: While Google Sheets was used as the intermediary data organization and export program, any spreadsheet program with a CSV export option can be used.

|Software/Packages|Version|
|:--|:--:|
|Google Sheets | N/A |
|JupyterLab | 4.4.3 |
|Matplotlib | 3.10.0 |
|NumPy | 2.2.5 |
|Pandas | 2.2.3 |
|Power BI| 2.146.1254.0 |
|Seaborn | 0.13.2 |

2. Download the 2023 National Combined High School YRBSS dataset [here](https://www.cdc.gov/yrbs/data/index.html).
3. Download the pbix file here (create pbix file link).
   1. If opting to recreate the Power BI report from scratch, open a blank Power BI project and import the downloaded dataset via Access Database, navigating to the location of where the dataset is stored on within the computer.
   2. Navigate to the dataset in Power Query and reproduce all table creations and transformations as found in the !!pbix file!!. Importation and transformation of the *Heatmap Stats* table will be conducted later. Select the 'Close and Apply' button in Power Query.
   3. With the home tab selected, create the *Race_Dim*, *Sex_Dim*, and *SexId_Dim* dimension tables by copying the corresponding DAX code from the !!pbix file!! for each table. Create a single measure in each table by copying the DAX code as found in the !!pbix file!!.
   4. Navigate to the model view in Power BI and copy the relationships as found in the !!pbix file!!.
   5. Recreate all tables, measures, and calculated columns (excluding the *Heatmap Stats* table, *Heatmap Measures* table and the associated calculated columns) as found in the !!pbix file!! by creating each individual table and copying the DAX code for each measure and calculated column.
   6. Create and name the 9 pages according to the !!pbix file!!. Recreate all visuals by adding the appropriate fields to the correct spot, copying all visual formatting, and copying all visual and page filters as found in the !!pbix file!!, excluding the *National Statistics* page.
      + Note: The background in the !!pbix file!! cannot be created in Power BI and is not available for reproduction. The background will not have any effect on any visuals, formatting, or calculations in the model.
   7. Navigate to the DAX query view. Copy and run all queries as found in the !!pbix file!!. Copy the entire table of each query and paste them into Google Sheets or the preferred spreadsheet program. The first row of the spreadsheet should contain the headers, and any duplicates of the header line should be removed. There should be no empty rows between each copy and paste. Once all tables have been put into the spreadsheet with the appropriate formatting, export the spreadsheet as a CSV file and store in an approriate location on the computer.
4. Open JupyterLab and replicate the ipynb notebook using one of the following methods:
   1. Copy the notebook URL from GitHub, navigate back to JupyterLab, select *Open from URL...* from the file tab, paste the URL in the pop-up text box, and select open.
   2. Download the notebook file from GitHub, navigate back to JupyterLab, and drag the downloaded notebook files into the file browser tab or copy the path of the notebook from its storage location and select *Open from Path...* from the file tab, paste the path in the pop-up text box, and select open.
   3. Copy and the individual cells from the GitHub file and paste them into a newly launched JupyterLab notebook, making note of which cells are code and which cells are markdown.
   4. In the JupyterLab notebook, run each cell starting with the top cell and moving down in sequential order to view the output. In order to view the outputs and visualizations, replace the current file path (located in the second code cell) with the previously saved CSV file path.
   5. Locate the *Heatmap_stats.csv* file after running the last code cell and store the file in an approriate place on the computer.
5. If recreating the Power BI report from scratch, return to the Power BI report and continue with the following instructions.
   1. Import the *Heatmap_stats.csv* file from its saved location. Open Power Query and copy all transformations from the applied steps in as found in the !!pbix file!!. Once completed, select the 'Close and Apply' button in Power Query.
   2. Create the *heatmap Measures* table, and recreate the measures by copying the DAX code as found in the !!pbix file!!.
   3. Navigate to the *National Statistics* page in the model view. Recreate the visuals by adding the appropriate fields to the correct spot, copying all visual formatting, and copying all visual and page filters as found in the !!pbix file!!.
  
## Licensing and Usage

### License Information

This repository is dual-licensed under:

- **GNU Affero General Public License v3.0 (AGPL-3.0)**  
  Applies to all source code in this repository (e.g., Python scripts, Jupyter Notebooks, and related functions).  
  See the [LICENSE-AGPL](https://choosealicense.com/licenses/agpl-3.0/) file for details.

- **Creative Commons Zero v1.0 Universal (CC0-1.0)**  
  Applies to all non-code assets in this repository (e.g., Power BI reports, visualizations, exported figures, and CSV files derived from analyses).  
  See the [LICENSE-CC0](https://choosealicense.com/licenses/cc0-1.0/) file for details.

In short:
- **Code** → Copyleft protected under AGPL (derivatives must remain open if distributed or served).  
- **Visualizations & Reports** → Released to the public domain via CC0, free for any reuse without attribution.

### Citation Information

Casper, g. (2025). *Youth-Risk-Behavior-Survey-Analysis* [GitHub repository]. GitHub. https://github.com/gcasper95/Youth-Risk-Behavior-Survey-Analysis/edit/main/
