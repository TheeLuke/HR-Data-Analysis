# OData-and-PowerBI

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

Using this information, I will now construct the OData Endpoint URL(1):

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

The first transformation query I ran was using PowerBI. I updated the column headers to represent their respectable title, instead of for example, 'field_1'.
The next query, consisted of dropping columns 27-36, as I was not focused on querying this type of data in the dataset.


### References

1. https://www.bibb.pro/post/sharepoint-odata-in-power-query