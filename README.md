******REAL-TIME DASHBOARD******

### A REAL-TIME DASHBOARD USING STREAMING DATA  (A SIMULATED API FEED) #####


Power BI supports real-time data streaming through the Power BI Service and Power BI REST API. This process requires setting up a streaming dataset and pushing data into it through an API. 

1. Prepare Your Streaming Data (API Feed)
To use streaming data, you'll need an API that sends data at intervals..

For the sake of this example, let's assume we have an API that provides data in JSON format, like this:

json
{
  "timestamp": "2025-01-28T14:00:00Z",
  "temperature": 22.5,
  "humidity": 55.0
}

2. Set Up Power BI Streaming Dataset
 A Streaming Dataset is most commonly used for real-time visualizations.

Steps to Create a Streaming Dataset in Power BI:
Sign in to Power BI: Go to Power BI Service, sign in, and navigate to your workspace.

Create a Streaming Dataset:

Go to My Workspace (or another workspace you prefer).
Click on the Create button select Streaming Dataset.
Choose API as the source for your streaming dataset.
Define the dataset schema (the fields that your API will send). 


In this case:
timestamp (Date/Time)
temperature (Number)
humidity (Number)
Save the Dataset: After defining the fields, click on Create.

Get the Push URL: After creation, you’ll be given a Push URL that you will use to send data to Power BI.

3. Push Data to Power BI Using API
To stream data into Power BI, you will need to send data to the Push URL using an HTTP POST request. Here's how you can push data from a Python script or any other programming language.

Python :
To send data to Power BI,  use the requests library to send POST requests to the streaming dataset API.

Install the requests library :
pip install requests


import requests
import random
import time
from datetime import datetime

# Power BI Push URL (get this from the Streaming Dataset page in Power BI)
push_url = 'https://api.powerbi.com/beta/1e355c04-e0a4-42ed-8e2d-7351591f0ef1/datasets/37c984a5-3f1f-45ed-ad45-feed0286ef8c/rows?experience=power-bi&key=9ItD%2BiwC9ol7O0msgK97W%2FIyXDVatd95S7t2St1ehZVeGbycZUQWWj0GcNiPfeTwQCiptERyCIMFGrlsewZmPg%3D%3D'

def push_data_to_powerbi():
    while True:
        # Simulate receiving new data from an API
        data = {
            "timestamp": datetime.utcnow().strftime('%Y-%m-%dT%H:%M:%SZ'),
            "temperature": round(random.uniform(20, 30), 2),
            "humidity": round(random.uniform(40, 60), 2)
        }

Send data to POWER BI
response =requests.post(push_url,json=[data])
if response.status_code==200:
print(f"Data sent to power BI:{data}")
else:
print(f"Error sending data:{response.status_code},{response.text}")

wait for a few seconds before sending the next data
time.sleep(5)
 
# Start pushing data
push_data_to_powerbi()


In this script:
The push_url is the URL  get from Power BI after creating your streaming dataset.

The data sent to Power BI consists of timestamp, temperature, and humidity fields.
The script simulates the arrival of new data every 5 seconds, and it pushes that data to Power BI.


4. Create a Dashboard to Visualize the Data
Once streaming data is being sent to Power BI, can create a real-time dashboard using that data.

Steps to Create a Dashboard:
Go to Power BI Service: Open Power BI and navigate to your workspace.
Create a Report:
Click on Create > Report.
Select your streaming dataset as the data source.
Use the available fields (e.g., timestamp, temperature, humidity) to create visualizations (such as line charts, gauges, etc.).


Pin Visualizations to Dashboard:
Once your report is created, pin the visualizations (charts, graphs) to a dashboard.
This dashboard will now automatically update in real-time as new data is streamed.


Dashboardlink:https://app.powerbi.com/groups/d0789cf0-5bd7-40d7-b038-9d72dd9d0b0e/dashboards/1a497749-73bc-421a-a7d3-fe0c7795f7c4?experience=power-bi
