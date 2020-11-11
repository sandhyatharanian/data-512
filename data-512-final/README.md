## Data 512A Au 20: Human-Centered Data Science Final Project Proposal - A case analysis on 911 Calls 

## **Motivation/problem statement**

Be it an extreme personal crisis and community wide disasters, 911 is the first access point for those seeking emergency response across America. 911 workers receive calls and expertly dispatch emergency service professionals and equipment to render life-saving assistance to those in need which is why we rely on this system to assure the public’s safety every day. 

This project aims at analyzing the emergency calls dataset to discover hidden trends and patterns to determine areas of high call volume, perform spatial analysis to understand factors that contribute these high call volumes and look at the overall call response rate. Further, the analysis will seek to explore the various sources of non-emergency 911 calls and their relative proportions to one another which will be crucial to adequately understand the nuisances caused by the non-emergency calls.

## **Data used**

The dataset used for this project is obtained from the City of Cincinnati's computer aided dispatch (CAD) database which contains fire incident responses including emergency medical services (EMS) calls, fires, rescue incidents, and all other services handled by the Fire Department. This dataset is updated daily and is available as a public domain which allows to freely share and use the data for any purpose and without any restrictions.

Link to the dataset can be found [here](https://data.cincinnati-oh.gov/Safety/Cincinnati-Fire-Incidents-CAD-including-EMS-ALS-BL/vnsz-a3wp)

API Endpoint can be accessed [here](https://data.cincinnati-oh.gov/resource/vnsz-a3wp.json)

## Data description

The dataset consists of the following attributes along with the description for each column as provided by the Cincinnati fire incidents data dictionary.

This data seem to contain the required information needed to evaluate the call volume and its origin. Neighborhood and community council neighborhood fields can be used as a close proxy to determine the origin. Latitude and longitude data can be used to perform further spatial analysis to understand the factors contributing to the call volume. Create time incident and arrival time primary unit fields can be used to understand the call response rate.

## License Information

The license information for the dataset can be found [here](https://opendatacommons.org/licenses/pddl/1-0/).


## Ethical Implications
The emergency call data has been anonymized to exclude any personally identifiable information as stated in the disclaimer below from the City of Cincinnati’s website. This is makes me comfortable to use this dataset for the purpose of this final project.
“Disclaimer: In compliance with privacy laws, all Public Safety datasets are anonymized and appropriately redacted prior to publication on the City of Cincinnati’s Open Data Portal. This means that for all public safety datasets: (1) the last two digits of all addresses have been replaced with “XX,” and in cases where there is a single digit street address, the entire address number is replaced with "X"; and (2) Latitude and Longitude have been randomly skewed to represent values within the same block area (but not the exact location) of the incident.”

## Unknowns and dependencies
City of Cincinnati’s Performance and Data Analytics team facilitates standard processing to most raw data prior to publication. Processing includes but is not limited: address verification, geocoding, decoding attributes, and addition of administrative areas (i.e. Census, neighborhoods, police districts, etc.).
To perform spatial analysis we would need to leverage other dataset. Furthermore, I need to do a few joins on the data given to address all questions I am interested in, which adds complexity to the data munging part of this project.

