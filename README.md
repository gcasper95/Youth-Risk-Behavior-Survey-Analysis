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
4. In the table titled 'Heatmap Stats', imported from Python, the x and y column values were replaced with their corresponding Power BI risk behavior text descriptions used in the visualizations. The five columns containing the statistical values were unpivoted, resulting in two columns (Attribute & Value). The non-alphabetical characters in the attribute column were replaced with commas and split into three separate columns using the comma as a delimiter. A custom column named description was created in 'Heatmap Stats' to describe the statistic, the dependent variable, and the conditional variable. A second custom column named pairing label was created in 'Heatmap Stats' describing the risk behaviors. A third custom column named attribute names was created in 'Heatmap Stats' describing the statistical test used. Select values in the value column were replaced with null to remove them from the ranking visualizations, as the risks being assessed could not happen without the corresponding risks taking place.

Python
1. After importing the 'Analysis Table' from Power BI, the dichotomous values in the survey answer fields were changed from one and two to one and zero for accurate mathematical operations.
2. A subset of the data was created by removing all non-dichotomous fields, with the purpose of being used in an unweighted pearson correlation heatmap.
3. After reviewing the weighted phi correlation heatmap, values between 0.40 and 0.99 were assessed for statistical analysis. 
