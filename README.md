
# Web Scraping Project Summary

## Objective

This project involves web scraping data from the Fake Python Jobs website using Python, the BeautifulSoup library, and the requests module. The extracted data is then cleaned and prepared for analysis.

## Steps Taken

**1. Importing Libraries**
   
```python
from bs4 import BeautifulSoup
import requests
import pandas as pd
```
The essential libraries for web scraping and data manipulation were imported:

**BeautifulSoup:** For parsing HTML content.
**requests:** To fetch web pages.
**pandas:** For data organization and cleaning.

**2. Extracting Data**

The website URL was accessed, and job-related details were scraped:

```python
url = "https://realpython.github.io/fake-jobs/"
source = requests.get(url)
soup = BeautifulSoup(source.content, 'html.parser')
jobs = soup.find_all('div', class_='column is-half')
```
Empty lists were initialized to store job details (jobtitles, companies, locations, and dates). A loop iterated through the HTML structure to extract:

- Job Title
- Company Name
- Location
- Date

 ```python
  # Loop to extract data
  
for job in jobs:
    jobtitle = job.find('h2', class_='title is-5').get_text()
    company = job.find('h3', class_='subtitle is-6 company').get_text()
    location = job.find('p', class_='location').get_text()
    date = job.find('time', datetime="2021-04-08").get_text()
    
    # Append data to respective lists
    jobtitles.append(jobtitle)
    companies.append(company)
    locations.append(location)
    dates.append(date)
```
**3. Creating a DataFrame**

The extracted data was compiled into a pandas DataFrame:

```python
df = pd.DataFrame({
    "Job Title": jobtitles,
    "Company": companies,
    "Location": locations,
    "Date": dates
})
```
**4. Data Cleaning**

- a. Removing Special Characters
The Location column contained newline characters (\n) and additional text. These were removed using str.replace and str.split:

```python
df['Location'] = df['Location'].str.replace('\n', "").str.split(',', expand=True)[0]
```
- b. Changing Data Types
The Date column, initially stored as a string, was converted to a datetime object:

```python
df['Date'] = pd.to_datetime(df['Date'])
```
5. Verifying the Dataset
The dataset's structure was analyzed using:

  - df.info() to confirm no missing values.
  - df.shape to ensure the expected number of rows and columns.
Sample output
```python
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 100 entries, 0 to 99
Data columns (total 4 columns):

|#   | Column     | Non-Null Count  |  Dtype       |          
|--- | ------     |--------------   | -------------|      
| 0  | Job Title  | 100 non-null    | object       | 
| 1  | Company    | 100 non-null    |object        | 
| 2  | Location   | 100 non-null    |object        |
|3   | Date       |100 non-null     |datetime64[ns]|
```
 ## Final Dataset

| Job Title                 | Company                        | Location         | Date       |
|---------------------------|--------------------------------|------------------|------------|
| Senior Python Developer   | Payne, Roberts and Davis       | Stewartbury      | 2021-04-08 |
| Energy engineer           | Vasquez-Davidson               | Christopherville | 2021-04-08 |
| Legal executive           | Jackson, Chambers and Levy     | Port Ericaburgh  | 2021-04-08 |
| Fitness centre manager    | Savage-Bradley                 | East Seanview    | 2021-04-08 |
| Product manager           | Ramirez Inc                    | North Jamieview  | 2021-04-08 |


## Outcome
The dataset is clean and ready for analysis. This project highlights the following skills:

  - Web scraping using BeautifulSoup.
  - Data extraction, cleaning, and preparation.
  - Working with HTML structures and handling unstructured data.




