# Tracer Library

## Overview

Tracer is a library that intercepts API calls to DIGIT services with imported tracer and logs errors.

A new utility method has been added to the tracer using which modules can prepare error details and invoke this utility method to persist these error objects on the database for retrying them.

## Configuration Details

Here are the steps using which any module can utilize this functionality to store error objects -

1. The concerned module has to prepare error details.
2. The concerned module can then make a call to `exceptionHandler` method which takes a list of `errorDetails` as its argument. This method will do a couple of enrichments and then emit these `errorDetails` to Kafka for indexer service to pick it up and persist.
3. Create an index with the name - `egov-tracer-error-details` using this command on Kibana -

`PUT egov-tracer-error-details { }`

4\. Create mapping for this index -

{% code lineNumbers="true" %}
```
PUT /egov-tracer-error-details/general/_mapping
{
  "properties" : {
          "Data" : {
            "properties" : {
              "@timestamp" : {
                "type" : "date"
              },
              "apiDetails" : {
                "properties" : {
                  "contentType" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "id" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "requestBody" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "url" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  }
                }
              },
              "auditDetails" : {
                "properties" : {
                  "createdTime" : {
                    "type" : "long"
                  },
                  "lastModifiedTime" : {
                    "type" : "long"
                  }
                }
              },
              "errors" : {
                "properties" : {
                  "errorCode" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "errorMessage" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "exception" : {
                    "properties" : {
                      "code" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "localizedMessage" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "message" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "stackTrace" : {
                        "properties" : {
                          "className" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "fileName" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "lineNumber" : {
                            "type" : "long"
                          },
                          "methodName" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "nativeMethod" : {
                            "type" : "boolean"
                          }
                        }
                      }
                    }
                  },
                  "type" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  }
                }
              },
              "retryCount" : {
                "type" : "long"
              },
              "status" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "uuid" : {
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
        }
}
```
{% endcode %}

5\. Setup indexer with the following indexer configuration file -

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">configs/egov-indexer/egov-error-queue-indexer.yml at dpg-1125 · egovernments/configs](https://github.com/egovernments/configs/blob/dpg-1125/egov-indexer/egov-error-queue-indexer.yml)

6\. Now, whenever `exceptionHandler` method will be invoked, `errorDetails` will be persisted on the index that was created in step 3.

