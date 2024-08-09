# Impact Of Heavy Reports On Platform

## Overview <a href="#overview" id="overview"></a>

Rainmaker has a reporting framework to configure new reports. As part of the report configuration, we have to write a native SQL query to get the required data for the report. So if the query takes huge time to execute or the query result has huge data, then it will impact the whole application's performance.

## Root Cause <a href="#root-cause" id="root-cause"></a>

The following cases are where we can see the application performance issue because of heavy reports.

* Filtering with long date range data or applying fewer filters which in turn returns huge data.
* Join the multiple tables for getting required data and missing creating an index on join columns.
* Implementing conditional logic inside the queries itself.
* Writing multiple sub-queries inside a single query for getting the required data.

## Impact <a href="#impact" id="impact"></a>

Because of heavy reports, the following are the impacts on the platform -

* When we execute a complex query on the database, a thread from the connection pool will block to execute the query.
* When threads from the connection pool are blocked completely, the application will become very slow for incoming requests.
* When max request timeout is crossed, the API gateway will return a timeout error, But still, the connection thread on the database is active, Then all these types of idle threads will occupy database resources like memory, and CPU which in turns increase the load on the database.
* Sometimes when running huge queries, the time taken by the query will lead to a broken pipe issue which causes more memory leaks and out-of-heap memory type issues. Because of this, the service will frequently restart automatically.
* If a query returns huge data, the browser will become unresponsive and the application will become unresponsive.
