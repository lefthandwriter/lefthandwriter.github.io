---
layout: post
title: Using the ChargePoint API with Python
date: 2018-06-22
categories: software
icon: rails
---
Here's a short post on my recent experience getting data from the ChargePoint API using Zeep in Python. The end-goal was to then design an SQL database based on the type of data returned by the API call, for an EV project I'm working on.

## Figuring out the API
First up was to figure out the API. The ChargePoint API is a SOAP API, which was new to me as I'd only worked with REST APIs up to this point. I did a quick lookup to find a software package that I could work with and settled with [Zeep](https://github.com/mvantellingen/python-zeep), a Python package. I found this [tutorial](https://medium.com/@adriennedomingus/using-zeep-to-make-soap-requests-in-python-c575ea0ee954) particularly helpful in getting started with Zeep.

Next was figuring out the endpoint. The ChargePoint manual that's available online doesn't explain this explicitly, but I managed to find the WSDL [here](http://volttron.readthedocs.io/en/releases-4.1/specifications/chargepoint_driver.html).

With this sorted, I then looked at the [ChargePoint manual](https://na.chargepoint.com/UI/downloads/en/ChargePoint_Web_Services_API_Guide_Ver4.1_Rev4.pdf) to see the types of methods available for an API call, and the information returned. My goal was to create a local database that stored the stations available in the network and the list of historical charging sessions. The two methods I needed were in Chapter 9 on Usage Analysis, and Chapter 10 on Station Management. Basically, the `getChargingSessionData` method returns parameters such as the sessionID, userID, stationID, stationName, startTime, endTime, Energy, and Address, while the `getStations` method returns the station information.

## Designing the database
With the response parameters from the API methods in hand, I laid out all the information available from an API call, and then designed the SQL database on hand. Basically, I created one table for each of the following entities: station, port, pricing, user, session, and payment. Each of these tables has a primary key, i.e. the station table has the stationID as its primary key, the port table has the portID as its primary key, and so on. I also included foreign keys for cross-referencing between tables, such as the stationID in the session table as a foreign key referencing the stationID in the station table. 

Here's a diagram of the database schema:

<img src="{{ lefthandwriter.github.io }}images/databaseSchema.png">
<!-- ![Schema](https://github.com/lefthandwriter/ChargePointAPI/blob/master/images/databaseSchema.png?raw=true) -->
<!-- ![Schema]({{site.url}}{{site.baseurl}}/assets/img/hp_narrators.png) -->


## The code
I wrote code to pull data from the API and populate the database using SQLite in Python. This was a process of creating the tables -> pull data from the API -> populate the rows in the appropriate table.

The code is written in such a way so that the user would enter a range from which to query data from, specified by a startTime and endTime, in Python datetime format. Since the ChargePoint API only allows a maximum of 100 sessions returned per API call, I set it so that it would make one call per day in the range, under the assumption that not more than 100 charging sessions are encountered per day. This works if your organization is relatively small like the one we have at Tech, but you'd need to modify the code otherwise.

I've posted the code on Github [here](https://github.com/lefthandwriter/ChargePointAPI).


