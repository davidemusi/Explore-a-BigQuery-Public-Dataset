# Explore-a-BigQuery-Public-Dataset


arrow_back
Explore a BigQuery Public Dataset
avatar image
00:37:40
Caution: When you are in the console, do not deviate from the lab instructions. Doing so may cause your account to be blocked. Learn more.

Username
student-00-6520ea16136d@qwiklabs.net
Password
m75G3bNfp4WX
GCP Project ID
qwiklabs-gcp-00-8232a999f436
Overview
Setup and requirements
Query a public dataset
Create a custom table
Create a dataset
Load the data into a new table
Query the table
End your lab
Explore a BigQuery Public Dataset
1 hour
Free
Rate Lab
Overview
Storing and querying massive datasets can be time consuming and expensive without the right hardware and infrastructure. Google BigQuery is an enterprise data warehouse that solves this problem by enabling super-fast SQL queries using the processing power of Google's infrastructure. Simply move your data into BigQuery and let us handle the hard work. You can control access to both the project and your data based on your business needs, such as giving others the ability to view or query your data.

You access BigQuery through the GCP Console, the command-line tool, or by making calls to the BigQuery REST API using a variety of client libraries such as Java, .NET, or Python. There are also a variety of third-party tools that you can use to interact with BigQuery, such as visualizing the data or loading the data. In this lab, you access BigQuery using the web UI.

You can use the BigQuery web UI in the GCP Console as a visual interface to complete tasks like running queries, loading data, and exporting data. This hands-on lab shows you how to query tables in a public dataset and how to load sample data into BigQuery through the GCP Console.

What you'll do
In this lab you:

Query a public dataset

Create a custom table

Load data into a table

Query a table

Setup and requirements
Qwiklabs setup
For each lab, you get a new GCP project and set of resources for a fixed time at no cost.

Make sure you signed into Qwiklabs using an incognito window.

Note the lab's access time (for example, img/time.png and make sure you can finish in that time block.

There is no pause feature. You can restart if needed, but you have to start at the beginning.

When ready, click img/start_lab.png.

Note your lab credentials. You will use them to sign in to Cloud Platform Console. img/open_google_console.png

Click Open Google Console.

Click Use another account and copy/paste credentials for this lab into the prompts.

If you use other credentials, you'll get errors or incur charges.

Accept the terms and skip the recovery resource page.
Do not click End Lab unless you are finished with the lab or want to restart it. This clears your work and removes the project.

Open BigQuery Console
In the Google Cloud Console, select Navigation menu > BigQuery:

BigQuery_menu.png

The Welcome to BigQuery in the Cloud Console message box opens. This message box provides a link to the quickstart guide and lists UI updates.

Click Done.

Query a public dataset
In this section, you load a public dataset, USA Names, into BigQuery, then query the dataset to determine the most common names in the US between 1910 and 2013.

Load USA Name dataset
In the left pane, click ADD DATA > Explore public datasets.
add-dataset.png

The Datasets window opens.

In the searchbox, type USA Names then Enter.

Click on the USA Names tile you see in the search results.

usa-names

Click VIEW DATASET.
BigQuery opens in a new browser tab. The project bigquery-public-data is added to your resources and you see the dataset usa_names listed in the left pane in your Resources tree.

usa-names-dataset.png

Query the USA Name dataset
Query bigquery-public-data.usa_names.usa_1910_2013 for the name and gender of the babies in this dataset, and then list the top 10 names in descending order.

Copy and paste the following query into the Query editor text area:

SELECT
  name, gender,
  SUM(number) AS total
FROM
  `bigquery-public-data.usa_names.usa_1910_2013`
GROUP BY
  name, gender
ORDER BY
  total DESC
LIMIT
  10
In the lower right of the window, view the query validator.
query-validator.png

BigQuery displays a green check mark icon if the query is valid. If the query is invalid, a red exclamation point icon is displayed. When the query is valid, the validator also shows the amount of data the query processes when you run it. This helps to determine the cost of running the query.

Click Run.
The query results opens below the Query editor. At the top of the Query results section, BigQuery displays the time elapsed and the data processed by the query. Below the time is the table that displays the query results. The header row contains the name of the column as specified in GROUP BY in the query.

79dfab8f4004d7a7.png

Create a custom table
In this section, you create a custom table, load data into it, and then run a query against the table.

Download the data to your local computer
The file you're downloading contains approximately 7 MB of data about popular baby names, and it is provided by the US Social Security Administration.

Download the baby names zip file to your local computer.

Unzip the file onto your computer.

The zip file contains a NationalReadMe.pdf file that describes the dataset. Learn more about the dataset.

Open the file named yob2014.txt to see what the data looks like. The file is a comma-separated value (CSV) file with the following three columns: name, sex (M or F), and number of children with that name. The file has no header row.

Note the location of the yob2014.txt file so that you can find it later.

Create a dataset
In this section, you create a dataset to hold your table, add data to your project, then make the data table you'll query against.

Datasets help you control access to tables and views in a project. This lab uses only one table, but you still need a dataset to hold the table.

Back in the console, in the left pane, in the Resources section, click your GCP Project ID (it will start with qwiklabs).
bq-console.png

Your project opens under the Query editor.

On the right side in the project section, click CREATE DATASET.

On the Create dataset page:

For Dataset ID, enter babynames.
For Data location, choose United States (US).
For Default table expiration, leave the default value.
Currently, the public datasets are stored in the US multi-region location. For simplicity, place your dataset in the same location.

create-dataset.png

Click Create dataset at the bottom of the panel.

Load the data into a new table
In this section, you load data into the table you made.

Click babynames found in the left pane in the Resources section, and then click Create table.
Use the default values for all settings unless otherwise indicated.

On the Create table page:

For Source, choose Upload from the Create table from: dropdown menu.

For Select file, click Browse, navigate to the yob2014.txt file and click Open.

For File format, choose CSV from the dropdown menu.

For Table name, enter names_2014.

In the Schema section, click the Edit as text toggle and paste the following schema definition in the text box.

name:string,gender:string,count:integer

create-table.png

Click Create table (at the bottom of the window).

Wait for BigQuery to create the table and load the data. While BigQuery loads the data, a (1 running) string displays beside the Job history in the left pane. The string disappears after the data is loaded.

Preview the table
In the left pane, select babynames > names_2014 in the navigation panel.
In the details panel, click the Preview tab.
87469f59db3ee2ab.png

Quick quiz. You need a table to hold the dataset

True

False

Query the table
Now that you've loaded data into your table, you can run queries against it. The process is identical to the previous example, except that this time, you're querying your table instead of a public table.

In the Query editor, click Compose new query.

Copy and paste the following query into the Query editor. This query retrieves the top 5 baby names for US males in 2014.

SELECT
 name, count
FROM
 `babynames.names_2014`
WHERE
 gender = 'M'
ORDER BY count DESC LIMIT 5
Click Run. The results are displayed below the query window.
a77eadeafdf06a84.png

Quick quiz. Check which you can use to access BigQuery

Web UI

Make calls to BigQuery REST API

Third-party tools

Command line tool

Congratulations!
You queried a public dataset, then created a custom table, loaded data into it, and then ran a query against that table.

End your lab
When you have completed your lab, click End Lab. Qwiklabs removes the resources you’ve used and cleans the account for you.

You will be given an opportunity to rate the lab experience. Select the applicable number of stars, type a comment, and then click Submit.

The number of stars indicates the following:

1 star = Very dissatisfied
2 stars = Dissatisfied
3 stars = Neutral
4 stars = Satisfied
5 stars = Very satisfied
You can close the dialog box if you don't want to provide feedback.

For feedback, suggestions, or corrections, please use the Support tab.

Copyright 2019 Google LLC All rights reserved. Google and the Google logo are trademarks of Google LLC. All other company and product names may be trademarks of the respective companies with which they are associated.


