# Data 512A Au 20: Human-Centered Data Science Assignment 1 - Data Curation

## Objective:

The goal of this assignment is to construct, analyze and publish a dataset of monthly traffic on English Wikipedia from January 1 2008 through August 30 2020. All of the analysis will be performed on a single Jupyter notebook and all data collected from the API will be made available as 5 `JSON` files which will then be processed and combined to form the final `csv` file.The purpose of this assignment is to familiarize oneself with the Jupyter Notebook environment and some best practices for open scientific research in designing and implementing the project and making the project fully reproducible (from the data collection phase through the data analysis phase) by others using a GitHub repository.

## License of the source data and terms of use:

The Wikimedia REST API offers access to Wikimedia's content and metadata in machine-readable formats. Focused on high-volume use cases, it tightly integrates with Wikimedia's globally distributed caching infrastructure.

    The REST API along with its documentation is available for all major Wikimedia projects at the location /api/rest_v1/. For example, for the English Wikipedia it is available at https://en.wikipedia.org/api/rest_v1/
    For information on terms and condition - https://www.mediawiki.org/wiki/Wikimedia_REST_API#Terms_and_conditions
    For information on privacy policy - https://foundation.wikimedia.org/wiki/Privacy_policy

## API documentation:

For this assignment, the data is from the Wikipedia page traffic which is retrieved using two different Wikimedia REST API endpoints (Pagecounts and Pageviews).
        The Legacy Pagecounts API (documentation, endpoint) provides access to desktop and mobile traffic data from December 2007 through July 2016.
        The Pageviews API (documentation, endpoint) provides access to desktop, mobile web, and mobile app traffic data from July 2015 through last month.

## Data Processing:

For each of the 2 API, the data is collected for all available months and the raw results are saved as 5 separate JSON source data files with the naming convention – “apiname_accesstype_firstmonth-lastmonth.json”. The final data is a combination of all 5 .json files which is then saved as “en-wikipedia_traffic_200712-202008.csv”. Given below is the description of the columns available in the final csv.

| Column | Value |
| ------ | ----- |
| year | YYYY |
| month |	MM |
| pagecount_all_views |	No. of views for all users (desktop and mobile combined) from the Legacy Pagecounts API |
| pagecount_desktop_views | No. of views for desktop users from the Legacy Pagecounts API |	
| pagecount_mobile_views | No. of views for mobile users from the Legacy Pagecounts API |
| pageview_all_views | No. of views for all users (desktop and mobile combined) from the Pageviews API |
| pageview_desktop_views | No. of views for desktop users from the Pageviews API |
| pageview_mobile_views | No. of views for mobile users from the Pageviews API |

## Note:
    
    - For data collected from the Pageviews API, the monthly values for mobile-app and mobile-web was combined to create a total mobile traffic count for each month.
    - For all data, the value of timestamp was separated into four-digit year (YYYY) and two-digit month (MM) and values for day and hour was discarded.
    - For all months with 0 pageviews for a given access method (e.g. desktop-site, mobile-app), that value for that (column, month) was listed as 0.
    - The data from Pageview API (but not the Pagecount API) excludes users such as web crawlers or spiders.
    - There is about 1 year of overlapping traffic data between the two APIs.

