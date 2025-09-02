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
1. The categorical columns for race, sex, and sexual identity were changed from type decimal number to type text, and the values were replaced with their corresponding variables found in the [2023 YRBS Combined Datasets User's Guide](https://www.cdc.gov/yrbs/media/pdf/2023/2023-YRBS-SADC-Documentation.pdf).
2. A second table was created by duplicating the altered full table in step 1 and removing all fields that were not used for analysis. 
