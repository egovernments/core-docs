# Insert & Delete Data - Steps

### Steps to delete the records: <a href="#steps-to-delete-the-records" id="steps-to-delete-the-records"></a>

Refer to the sample below to delete the data for the month of July module-wise in the Postgres database:

delete from nss\_ingest\_data where dataKey like '%-07-2022:FIRE%';

delete from nss\_ingest\_data where dataKey like '%-07-2022:TL%';

delete from nss\_ingest\_data where dataKey like '%-07-2022:WS%';

delete from nss\_ingest\_data where dataKey like '%-07-2022:PGR%';

delete from nss\_ingest\_data where dataKey like '%-07-2022:PT%';

delete from nss\_ingest\_data where dataKey like '%-07-2022:MCOLLECT%';

### Steps to delete the records from ES: <a href="#steps-to-delete-the-records-from-es" id="steps-to-delete-the-records-from-es"></a>

Adjust the module and the date range accordingly.

Check the records before deleting.

{% hint style="info" %}
**Note:** Deleting data from both ES and Postgres is mandated to avoid duplication of data.
{% endhint %}

{% code lineNumbers="true" %}
```
GET firenoc-national-dashboard/_search
{
  "query": {
    "bool": {
      "must": [
      {
          "range": {
            "date": {
              "gte": 1656613800000,
              "lte": 1658773799000,
              "format": "epoch_millis"
            }
          }
        }
      ]
    }
  }
}

POST firenoc-national-dashboard/_delete_by_query
{
  "query": {
    "bool": {
      "must": [
      {
          "range": {
            "date": {
              "gte": 1656613800000,
              "lte": 1658773799000,
              "format": "epoch_millis"
            }
          }
        }
      ]
    }
  }
}

```
{% endcode %}
