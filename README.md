## Sample files for integrating with TrueSight Intelligence using python 3.x

# Summary

The intent of these files to to create a sample integration with TrueSight Intelligence for a fictitious Bike Dealership operating out of 3 locations(San Jose, Houston & Las Vegas). The integration generates metric data and also events associated with the data collected from the Dealership.
The data generated for this integration is random(bounded values) and based on some of the sample structures created in the file *randomdata.py*

The integration can be tried by running the bikesalesapp.py and passing the email address(used to sign up to the Intelligence account) and the API token(available in the Account Management UI in TrueSight Intelligence)

```
usage: bikesalesapp.py [-h] --email EMAIL --api API [--freq FREQ]

Sample integration with TrueSight Intelligence

optional arguments:
  -h, --help     show this help message and exit
  --email EMAIL  Your TrueSight Intelligence account email
  --api API      Your TrueSight Intelligence API token
  --freq FREQ    Polling frequency, defaults to 10 secs
```

The basic flow for the integration is as follows

* Get the credentials (email & API token)
* Define(Create) the metrics to be sent (one time setup)
* Send the measurements
* Send the events
* Wait for the polling duration and resend the measurements and events

# Details about the data being sent

* Basic metrics
  * Number of Bikes Sold
  * Number of Customers Visiting
  * Average wait time for customers Visiting
  * *All the metrics are grouped with the same type "Bike_Business_Metrics"*
* Application Name is *Bike Dealership*
* Sources
  * All the measurements are sent from 3 different sources corresponding to the 3 locations
  * Locations are San Jose, Houston & Las Vegas
* Events
  * Events are sent to indicate a sale of a Bike
  * Event contains the following information
    * time of sale(createdAt), location of the sale(source.ref)
    * Information about the sale (model, price) and demographic information about the buyer (age, sex, state)
    * other information like eventClass, applicationName etc.

# Organization of the files

* bikesalesapp.py - File which sends the metrics & events at a 10 sec interval, username and api token is passed as arguments while invoking the file
* randomdata.py - Contains arrays of data which is used in a random fashion
* definemetrics.py - Metric definitions
* sendmeasurements.py - Code to invoke the measurements API, uses random data to generate the values
* sendevents.py - Code to invoke the events API, randomly using the values provided in the randomdata.py file.
