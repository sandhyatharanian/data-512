## Data 512A Au 20: Final Project Proposal - A case analysis on 911 Calls

## Introduction 

The 911 system was designed to provide a universal, easy-to-remember number for people to reach police, fire or emergency medical assistance from any phone in any location, without having to look up specific phone numbers. In 1966, the National Academy of Sciences published "[Accidental Death and Disability: The Neglected Disease of Modern Society](https://www.ems.gov/pdf/1997-Reproduction-AccidentalDeathDissability.pdf),” a landmark report highlighting how accidental death and injury, particularly from motor vehicle crashes, had become an epidemic in the U.S. The report urged a series of steps to reduce these needless deaths and injuries, including exploring the “feasibility of designating a single, nationwide, telephone number to summon an ambulance.” Before 911 system, individuals needed to dial local 10-digit phone numbers to reach police, fire or emergency services. Two years later, a Senator in Haleyville, Alabama placed the first 911 call. It wasn’t long before other cities followed the trend. Only six days later, the second 911 call was placed in Nome, Alaska. Since then, the system expanded nationwide and is continuously improving to keep pace with advancing technology.

## Data used

The dataset used for this project is obtained from the City of Cincinnati's computer aided dispatch (CAD) database which contains fire incident responses including emergency medical services (EMS) calls, fires, rescue incidents, and all other services handled by the Fire Department. This dataset contains emergency call data from 1/1/2015 to today and is updated daily. The dataset is available as a public domain which allows to freely share and use the data for any purpose and without any restrictions.

Link to the website can be found [here](https://data.cincinnati-oh.gov/Safety/Cincinnati-Fire-Incidents-CAD-including-EMS-ALS-BL/vnsz-a3wp) and the dataset can be accessed using the API Endpoint which can be found [here](https://data.cincinnati-oh.gov/resource/vnsz-a3wp.json).

## Data description

The dataset consists of the following attributes along with the description for each column as provided by the Cincinnati fire incidents data dictionary.


| Column | Datatype | Description                                               |
| ------ | ------- | ---------------------------------------------------------- |
| address_x | Text | This attribute is the street name that the incident occurred on |
| latitude_x | Number | The latitude coordinates of the incident |
| longitude_x | Number | The longitude coordinates of the incident |
| agency | Text |
| create_time_incident | Floating Timestamp | This attribute is the date/timestamp when the response data was submitted into the CAD system |
| disposition_text | Text | The disposition of each incident is the outcome of the incident response |
| event_number | Text | The unique identifier of the incident|
| incident_type_id | Text | The problem code of the incident that is used to describe the issue |
| incident_type_desc | Text | The text description of the corresponding problem code (Incident_Type_Id)|
| neighborhood | Text | The listed neighborhood of the incident using the Statistical Neighborhood Approximations (SNA) |
| arrival_time_primary_unit | Floating Timestamp | This attribute is the date/timestamp when the first CFD apparatus arrived on scene at the incident |
| beat | Text | This attribute indicates what fire response area the incident belongs to |
| closed_time_incident | Floating Timestamp | This attribute is the date/timestamp when the incident is marked complete in the CAD system |
| dispatch_time_primary_unit | Floating Timestamp | This attribute is the date/timestamp when first apparatus was dispatched to respond to an incident |
| cfd_incident_type | Text | This attribute shows the breakdown of the incident type classification. ALS = Advance Life Service, BLS = Basic Life Service, FIRE = fire incident, MEDI = Medical Service Provided, OTHE = service provided by CFD but are not classified as a fire response |
| cfd_incident_type_group | Text | The high-level incident type category for each incident |
| community_council_neighborhood | Text | The listed neighborhood of the incident using community council defined boundaries |



This data seem to contain the required information needed to evaluate the call volume and its origin. Neighborhood and community council neighborhood fields can be used as a close proxy to determine the origin. Latitude and longitude data can be used to perform further spatial analysis to understand the factors contributing to the call volume. Create time incident and arrival time primary unit fields can be used to understand the call response rate.

**Note-** Initially, I wanted to analyze the City of Seattle dataset however the latitude and longitude informations are temporarily unavailable due to a current bug. Next, I looked at exploring the SFO dataset, but it contains 5.41M records consuming all my system resources slowing down the system performance considerably.  

## License Information

License information for the dataset can be found [here](https://opendatacommons.org/licenses/pddl/1-0/).


## Ethical Implications

The call data has been anonymized to exclude any personally identifiable information as stated in the disclaimer below from the City of Cincinnati’s website. This is makes me comfortable to use the dataset for the purpose of this final project.

> “Disclaimer: In compliance with privacy laws, all Public Safety datasets are anonymized and appropriately redacted prior to publication on the City of Cincinnati’s Open Data Portal. This means that for all public safety datasets: (1) the last two digits of all addresses have been replaced with “XX,” and in cases where there is a single digit street address, the entire address number is replaced with "X"; and (2) Latitude and Longitude have been randomly skewed to represent values within the same block area (but not the exact location) of the incident.”

## Unknowns and dependencies

- City of Cincinnati’s Performance and Data Analytics team facilitates standard processing to most raw data prior to publication. Processing includes but is not limited to address verification, geocoding, decoding attributes, and addition of administrative areas.
- To perform enhanced spatial analysis, I might need to leverage other demographic datasets and perform a few joins which could add to the complexity in data munging part of this project.

