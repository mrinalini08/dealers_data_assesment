
# Problem Statement:

## Part 1: ETL process
+ Create an ETL process to extract Mars Weather twitter account, Transform and Load the Date, Temperature High, Temperature Low, pressure to a csv file:

1. Scrape the latest [Mars Weather twitter account](https://twitter.com/marswxreport?lang=en) from the page
2. Extract tweet text(Date, Temperature High, Temperature Low, pressure) for the weather report
3. Load as a csv file with these 4 columns called mars_weather.csv


Sample text:
`Sol 1801 (Aug 30, 2017), Sunny, high -21C/-5F, low -80C/-112F, pressure at 8.82 hPa, daylight 06:09-17:55`

Sample Result:

| Date | Temperature High | Temperature Low | pressure |
| ----------- | ----------- | ----------- | ----------- |
| Aug 30, 2017 | -21 | -80 | 8.82|
| Sep 30, 2018 | 15 | 31 | 10 |

Data Source: [Mars Weather twitter account](https://twitter.com/marswxreport?lang=en)

## Part 2: Data Visualizaion
+ Create a scatter plot for Temperature High and pressure from the previous result by using matplotlib

# Requirements:

+ Develop a web scraper
+ Develop a ETL process 
+ Visualize the weather data with scatter plot
+ Publish your code along with any data sets used on your GitHub page
+ Create a Readme for your project on how to use, build, install, and run
+ Create any additional instructions / documentation as you see helpful
+ Must pass the unit tests created by the interviewer (will not be disclosed to you ahead of time)
+ Test must be returned within 48 hours (will check the latest commit timestamp on your GitHub for qualification)

# Expected Result:
1. Output as csv file: weather data with 4 cols(Date, Temperature High, Temperature Low, pressure) 
2. Scatter Plot for Temperature High and Pressure

Sample Result:

| Date | Temperature High | Temperature Low | pressure |
| ----------- | ----------- | ----------- | ----------- |
| Aug 30, 2017 | -21 | -80 | 8.82|
| Sep 30, 2018 | 15 | 31 | 10 |


# Required Technical Stack:

+ Must be created Python ONLY
+ Can use any open source frameworks, packages that are available through public code artifactories (e.g., pandas, requests) {cannot use unpublished GitHub source code}
+ Bonus points for limiting the number of open source frameworks utilized to deliver the functionality



# Test Scoring - Minimum to consider for interview (75%)
+ Project scaffolding and Git friendliness (10%)
+ Clean & self-documented code (30%)
+ Web Scraper (20%)
+ Data Cleaning & Transformation (20%)
+ Data Visualization (20%)

# Post Test Interview process:

+ There will be 2 interviews after the test has been successfully submitted
+ 1 Interview will be focused on submitted exercise, code review, and requirements validation
+ 1 Interview will be focused on your experience working in —> agile environments, interactions with QA Automation teams, technical collaboration style, and ability to receive and provide honest feedback to team
