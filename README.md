# SharePoint O-Data Pipeline to Power BI Analysis

## How to Use

This repository is a data pipeline and analysis project. It is meant to demonstrate the process I took to understanding SharePoint, the O-Data pipeline, and implementing it into Power BI.

## I. SharePoint OData

### Step 1: Sharepoint Data Setup

First, I needed to create my own SharePoint site to begin testing data on. To do this, I used Microsoft's free trial program for Businesses. Next, I populated the site with [HR Analytics](https://www.kaggle.com/datasets/anshika2301/hr-analytics-dataset/data?select=HR_Analytics.csv) found from Kaggle. It consisted of 38 columns of employee data ranging from information about their demographic to company information like time training and years at a company.

With this information, I created a list on my Sharepoint site and imported the CSV.

### Step 2: Implement Sharepoint Connection

The next step is to setup the Sharepoint OData endpoint URL so that it can connect to PowerBI for visualizations. 
To start, I took note of the sharepoint site I was working on:

```https://theeluke.sharepoint.com/sites/test```

And also saved the name of the list I imported from the HR analytics:

```"HR Analytics"```

Using this information, I will now construct the OData Endpoint URL[1]:

```https://https://theeluke.sharepoint.com/sites/test/_api/web/lists/getbytitle('HR Analytics')/items```

## II. Power BI

### Step 1: Setting up OData feed

To be able to retrieve the data from the SharePoint site into Power BI, I had to setup the OData feed using the endpoint URL I created.
The process I took:
- Selected "Get data from external sources"
- Typed and selected "OData feed"
- Using the basic URL selection, I entered the OData Endpoint URL that was made in Part 1, Step 2 and confirmed the URL.
- Next, I selected that I was using an organization account, and signed in confirming the OData feed pipeline.

### Step 2: Transform Data

Multiple transformations were made to refine the dataset. The key transformations include: 
- removing duplicates based on the employee's ID
- Removing columns that were not neccessary for analysis
- Renamed column headers to appropriate titles
- Fixed number columns from presenting as type 'text' to 'whole number'.

### Step 3: Building out the pages

#### Page 1.
This page is an HR Dashboard that overviews general information into the HR dataset. It contains information about employee attrition, the number of employees based on department, and other information regarding employees at the company. DAX Measure was required to use to accurately represent the Attrition Rate through Power BI.

``` 
Attrition Rate = 
DIVIDE(
    CALCULATE(
        DISTINCTCOUNT(HR_Analytics[EmpID]),
        HR_Analytics[Attrition] = "TRUE"
    ),
    DISTINCTCOUNT(HR_Analytics[EmpID])
)
```

#### Page 2.
This page delves deeper into employee attrition, analyzing turnover rates across different departments and specific position titles. It visualizes how attrition relates to factors such as salary brackets and the total number of years employees have been with the company. Interactive filters allow for exploring attrition patterns based on age range, marital status, distance from home, and job level.

#### Page 3.
This page provides an overview of the company's workforce composition. It includes charts showing the distribution of employees by their field of education and age range. It also shows the gender breakdown within each department. A detailed table lists individual employee data including age, gender, department, position, and years at the company.

### Page 4.
This page focuses on analyzing employee compensation. It presents the distribution of monthly income across the workforce, including a breakdown by specific position titles and comparisons between genders within those roles. It also visualizes the number of employees within defined monthly income brackets.
- Learned how to download new visualizations and apply columns and style

## III. Wrap up
This was a data analysis project connecting SharePoint O-data to Power BI through a data feed pipeline. I imported an HR analytics database to build out a dashboard and analysis in Power BI. Through this process, I learned hands on experience using Power BI and how to connect and use SharePoint O-Data feed.


### References

1. https://www.bibb.pro/post/sharepoint-odata-in-power-query