## Data 512A Au 20: Final Project Proposal - A case analysis on 911 Calls

## Motivation/problem statement 

Be it an extreme personal crisis and community wide disasters, 911 is the first access point for those seeking emergency response across America. 911 workers receive calls and expertly dispatch emergency service professionals and equipment to render life-saving assistance to those in need which is why we rely on this system to assure the public’s safety every day. As per the 911 statistics published by the National Emergency Number Association [NENA](https://www.nena.org/page/911Statistics),

> “An estimated 240 million calls are made to 9-1-1 in the U.S. each year.”

Thus making the analysis of 911 calls a major initiative to help provide huge and largely untapped opportunity for researchers and practitioners to inform and transform policing policy and practice including developing alternatives to police emergency response. This project aims at analyzing the 911 call for service data to discover hidden trends and patterns to determine areas of high call volume, perform spatial analysis to understand factors that contribute high call volumes and look at the overall call response rate. Further, the analysis will seek to explore the various sources of non-emergency 911 calls and their relative proportions to one another which will be crucial to understanding the nuisances caused by the non-emergency calls.

## Background work

Due to the magnitude of its importance and extent to which it causes an impact, there are several ongoing works by various organizations to understand this dataset. Below are some of the examples which served as a motivation factors for the inception of this project.

**The Tamir Rice case**
> On November 22, 2014, a 911 caller to the Cleveland Police Department reported a “guy with a gun” pointing it at people at a neighborhood recreation center. The 911 caller said the person was “probably a juvenile” and the gun was “probably fake.” The call was quickly relayed to the police dispatcher, who sent the closest available unit to the scene. However, the critical clarifying information—that the subject was probably a juvenile and the gun was probably fake—was never passed along to the responding officers. Minutes later, a Cleveland police officer and his trainee arrived at the scene, pulled their cruiser right up on the subject, and within seconds shot and killed 12-year-old Tamir Rice.

An [article](https://www.policeforum.org/assets/EmergencyCommunications.pdf) published by the police executive Research forum spells out the key issues of withholding critical information from a 911 call dispatcher by examining controversial incidents involving police use of force. The Tamir Rice case highlighted the importance of the police dispatch function in these incidents. When 911 dispatchers are able to provide responding officers with critically important information about the nature of a call for service, there is a much better chance of a successful outcome. But if officers arrive at the scene unaware of key facts, the risks to everyone multiplies.

Another [article](https://www.ncjrs.gov/pdffiles1/nij/226874.pdf) published in the National Institute of Justice NIJ journal, uses 911 calls for service, field interview reports, crime incident narrative reports and site security logs to detect terrorism threats. An excerpt from the article states,

> “Our study showed that simple analytic processes could produce operationally relevant findings from 911 calls.”

In the [paper](http://hpcf-files.umbc.edu/research/papers/IS789_Project_Report-HPCF-2019-29.pdf), “Analysis and Prediction of 911 Calls based on Location using Spark Big Data Platform”, the authors use various ML algorithms to predict the number of calls from a particular location using longitude and latitude data with an intention to help manage police resources.

## Research questions & methodology

The above articles/papers and various other incidents like Tamir Rice where a trivial data error may have been the difference between life and death calls for modest changes addressing the 911 systems. With this in mind, I intend to analyze the dataset and explore answers to some of the questions like the most common reason for calling 911, neighborhoods making the most frequent 911 calls and the number of non-emergency calls made. In addition to the above questions, I would like to research some more areas as specified in my questions below.

### Q1 – What is the average call response rate by incident type?
Incident types are classified as ALS (Advance Life Service), BLS (Basic Life Service), FIRE (fire incident), MEDI (Medical Service Provided) and OTHE (service provided by CFD that are not classified as a fire response). It would be interesting to look at the pattern here to see if some incident types have a higher response rate, as it should be for life services than others.

### Q2 – What reasons contribute more to non-emergency 911 calls?
911 lines are designated for emergency calls, such as reporting a crime in progress, reporting a fire, or requesting an ambulance. Using 911 for non-emergency calls may delay help for people caught in real emergencies.

### Q3 – Determine the pattern between Day of the Week and Time of the Day (Morning, Afternoon, Evening, and Night) for the 911 calls.
Knowing the most common calls that are made in the evening, for example, could be a very useful information. Identifying such patterns help predicting where the police force might be needed the most at a given time and hence aid in better resource management.


### Methodology

For the first question, I intend to use the Create_Time_Incident field which records when the response data was submitted and the Arrival_Time_Primary_Unit which is the attribute that records when the first response team arrived on scene at the incident. A call response rate is defined as difference between the above two field which will then be converted into seconds.I have chosen this field as it would be the right approach to calculate the response rate and converting it to seconds would be helpful in understanding patterns that are intuitive, easy to interpret.I will be using a histogram/timeseries plot to explore and answer this question.

For the second question, the reasons for non-emergency 911 calls is not a straightforward number and needs to be obtained by extracting disposition codes from ‘disposition text’ columns and performing a lookup with the fire disposition codes published in the City of Cincinnati website. This approach would give us a good guesstimate of the number of non-emergency calls and the reasons contributing to it and creating a barchart will provide enough evidence to this question.

For the third question, to enable this pattern finding, the CREATE_TIME_INCIDENT column will be divided into two columns-day of week and time of day. The column will be split such that each date will be represented as the respective day of the week, for example Monday, Tuesday and so on. The time of day will be divided into four different values: Morning, Afternoon, Evening and Night based on the time. The time 6 AM to less than 12 PM will be classified as Morning, 12 PM to less than 4 PM will be classified as Afternoon, 4 PM to less than 9 PM will be classified as Evening and time from 9 PM to less than 6 AM will be classified as Night.The data can then be visualized using heatmaps to understand the pattern.

## Data used

The dataset used for this project is obtained from the City of Cincinnati's computer aided dispatch (CAD) database which contains fire incident responses including emergency medical services (EMS) calls, fires, rescue incidents, and all other services handled by the Fire Department. This dataset is updated daily and is available as a public domain which allows to freely share and use the data for any purpose and without any restrictions.

Link to the website can be found [here](https://data.cincinnati-oh.gov/Safety/Cincinnati-Fire-Incidents-CAD-including-EMS-ALS-BL/vnsz-a3wp). <br/>
Link to the **dataset** can be accessed using the API Endpoint which can be found [here](https://data.cincinnati-oh.gov/resource/vnsz-a3wp.json).

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

