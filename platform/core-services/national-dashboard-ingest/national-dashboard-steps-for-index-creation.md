# National Dashboard: Steps for Index Creation

### Overview <a href="#overview" id="overview"></a>

_This document aims to list out the steps needed to be followed to create national dashboard indexes._

### Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

1. Prior Knowledge of ElasticSearch

### Steps for index creation <a href="#steps-for-index-creation" id="steps-for-index-creation"></a>

For understanding purposes we are listing out the steps needed to be followed to create **property tax** index for national dashboard.

1. Open Kibana
2. Create index using the following query -

{% code lineNumbers="true" %}
```
PUT pt-national-dashboard
{}
```
{% endcode %}

3\. Add corresponding field mappings for the created index -

{% code lineNumbers="true" %}
```
 PUT pt-national-dashboard/_mapping/nss
 {
        "properties" : {
          "assessedPropertiesForUsageCategory" : {
            "type" : "long"
          },
          "assessments" : {
            "type" : "long"
          },
          "cessForUsageCategory" : {
            "type" : "long"
          },
          "createdBy" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "createdTime" : {
            "type" : "long"
          },
          "date" : {
            "type" : "date",
            "format" : "dd-MM-yyyy HH:mm:ss||dd-MM-yyyy||epoch_millis||dd-MM-yyyy'T'HH:mm:ss.SSSZ"
          },
          "financialYear" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "interestForUsageCategory" : {
            "type" : "long"
          },
          "lastModifiedBy" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "lastModifiedTime" : {
            "type" : "long"
          },
          "module" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "penaltyForUsageCategory" : {
            "type" : "long"
          },
          "propertiesRegisteredForFinancialYear" : {
            "type" : "long"
          },
          "propertyTaxForUsageCategory" : {
            "type" : "long"
          },
          "rebateForUsageCategory" : {
            "type" : "long"
          },
          "region" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "state" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "todaysClosedApplications" : {
            "type" : "long"
          },
          "todaysCollectionForUsageCategory" : {
            "type" : "long"
          },
          "todaysTotalApplications" : {
            "type" : "long"
          },
          "transactionsForUsageCategory" : {
            "type" : "long"
          },
          "ulb" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "usageCategory" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "ward" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          }
        }
      }
```
{% endcode %}
