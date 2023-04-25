# Certificate Generation

The final step in this process is the creation of configs to create a voter registration PDF for the citizens to download. For this, we will make use of DIGIT’s PDF service which uses PDFMake and Mustache libraries to generate PDF. A detailed documentation on PDF service and generating PDFs using PDF service can be found here - [https://docs.digit.org/urban/platform/configure-digit/services-overview/core-services/pdf-generation-services](https://docs.digit.org/urban/platform/configure-digit/services-overview/core-services/pdf-generation-services)

For our guide, we will follow the following steps to set up PDF service locally and generate PDF for our voter registration service -

i) Clone [DIGIT Services](https://github.com/egovernments/DIGIT-OSS) repo.

```
> git clone -o upstream https://github.com/egovernments/DIGIT-OSS
```

ii) Clone [Configs](https://github.com/egovernments/configs) repo.

```
> git clone -o upstream https://github.com/egovernments/configs
```

iii) Now, go into the DIGIT-Dev repo and open up a terminal. Checkout DIGIT\_DEVELOPER\_GUIDE branch.

```
> cd DIGIT-Dev
> git checkout DIGIT_DEVELOPER_GUIDE
```

iv) Now, go inside configs folder and under pdf-service data config and format config folders, create file by the name of digit-developer-guide.json

```
> cd configs/pdf-service/data-config
> touch digit-developer-guide.json
```

Add the following content in this newly created data config file -

```json
{
  "key": "btcertificate",
  "DataConfigs": {
    "serviceName": "rainmaker-common",
    "version": "1.0.0",
    "baseKeyPath": "$.BirthRegistrationApplications.*",
    "entityIdPath":"$.id",
    "isCommonTableBorderRequired": true,
    "mappings": [
      {
        "mappings": [
          {
            "direct": [
              {
                "variable": "logoImage",
                "url":"https://raw.githubusercontent.com/egovernments/egov-web-app/master/web/rainmaker/dev-packages/egov-ui-kit-dev/src/assets/images/pblogo.png",
                "type":"image"
              },
              {
                "variable": "applicantName",
                "value": {
                  "path": "$.babyFirstName"
                }
              },
              {
                "variable": "applicationNo",
                "value": {
                  "path": "$.applicationNumber"
                }
              },
              {
                "variable": "address",
                "value": {
                  "path": "$.address.city"
                }
              },
              {
                "variable": "birthIdIssueDate",
                "value": {
                  "path": "$.auditDetails.createdTime"
                },
                "type": "date"
              },
              {
                "variable": "signedCertificateData",
                "value": {
                  "path": "$.signedCertificate"
                }
              },
              {
                "variable": "to",
                "value": {
                  "path": "PDF_STATIC_LABEL_CONSOLIDATED_RECEIPT_TO"
                },
                "type": "label",
                "localisation":{
                  "required":true,
                  "prefix": null,
                  "module":"rainmaker-common"
                }
              },
              {
                "variable": "municipal_corportaion",
                "value": {
                  "path": "PDF_STATIC_LABEL_CONSOLIDATED_TLCERTIFICATE_MUNICIPAL_CORPORATION"
                },
                "type": "label",
                "localisation":{
                  "required":true,
                  "prefix": null,
                  "module":"rainmaker-common"
                }
              },
              {
                "variable": "corporation_contact",
                "value": {
                  "path": "PDF_STATIC_LABEL_CONSOLIDATED_TLCERTIFICATE_LICENSE_CORPORATION_CONTACT"
                },
                "type": "label",
                "localisation":{
                  "required":true,
                  "prefix": null,
                  "module":"rainmaker-common"
                }
              },
              {
                "variable": "corporation_website",
                "value": {
                  "path": "PDF_STATIC_LABEL_CONSOLIDATED_TLCERTIFICATE_LICENSE_CORPORATION_WEBSITE"
                },
                "type": "label",
                "localisation":{
                  "required":true,
                  "prefix": null,
                  "module":"rainmaker-common"
                }
              },
              {
                "variable": "corporation_email",
                "value": {
                  "path": "PDF_STATIC_LABEL_CONSOLIDATED_TLCERTIFICATE_LICENSE_CORPORATION_EMAIL"
                },
                "type": "label",
                "localisation":{
                  "required":true,
                  "prefix": null,
                  "module":"rainmaker-common"
                }
              },
              {
                "variable": "application_no",
                "value": {
                  "path": "PDF_STATIC_LABEL_CONSOLIDATED_TLCERTIFICATE_APPLICATION_NO"
                },
                "type": "label",
                "localisation":{
                  "required":true,
                  "prefix": null,
                  "module":"rainmaker-common"
                }
              },
              {
                "variable": "reciept_no",
                "value": {
                  "path": "PDF_STATIC_LABEL_CONSOLIDATED_TLCERTIFICATE_RECIEPT_NO"
                },
                "type": "label",
                "localisation":{
                  "required":true,
                  "prefix": null,
                  "module":"rainmaker-common"
                }
              },
              {
                "variable": "financial_year",
                "value": {
                  "path": "PDF_STATIC_LABEL_CONSOLIDATED_TLCERTIFICATE_FINANCIAL_YEAR"
                },
                "type": "label",
                "localisation":{
                  "required":true,
                  "prefix": null,
                  "module":"rainmaker-common"
                }
              },
              {
                "variable": "trade_name",
                "value": {
                  "path": "PDF_STATIC_LABEL_CONSOLIDATED_TLCERTIFICATE_TRADE_NAME"
                },
                "type": "label",
                "localisation":{
                  "required":true,
                  "prefix": null,
                  "module":"rainmaker-common"
                }
              },
              {
                "variable": "trade_owner_name",
                "value": {
                  "path": "PDF_STATIC_LABEL_CONSOLIDATED_TLCERTIFICATE_TRADE_OWNER_NAME"
                },
                "type": "label",
                "localisation":{
                  "required":true,
                  "prefix": null,
                  "module":"rainmaker-common"
                }
              },
              {
                "variable": "trade_owner_contact",
                "value": {
                  "path": "PDF_STATIC_LABEL_CONSOLIDATED_TLCERTIFICATE_TRADE_OWNER_CONTACT"
                },
                "type": "label",
                "localisation":{
                  "required":true,
                  "prefix": null,
                  "module":"rainmaker-common"
                }
              },
              {
                "variable": "trade_address",
                "value": {
                  "path": "PDF_STATIC_LABEL_CONSOLIDATED_TLCERTIFICATE_TRADE_ADDRESS"
                },
                "type": "label",
                "localisation":{
                  "required":true,
                  "prefix": null,
                  "module":"rainmaker-common"
                }
              },
              {
                "variable": "trade_type",
                "value": {
                  "path": "PDF_STATIC_LABEL_CONSOLIDATED_TLCERTIFICATE_TRADE_TYPE"
                },
                "type": "label",
                "localisation":{
                  "required":true,
                  "prefix": null,
                  "module":"rainmaker-common"
                }
              },
              {
                "variable": "accessories_label",
                "value": {
                  "path": "PDF_STATIC_LABEL_CONSOLIDATED_TLCERTIFICATE_ACCESSORIES_LABEL"
                },
                "type": "label",
                "localisation":{
                  "required":true,
                  "prefix": null,
                  "module":"rainmaker-common"
                }
              },
              {
                "variable": "trade_license_fee",
                "value": {
                  "path": "PDF_STATIC_LABEL_CONSOLIDATED_TLCERTIFICATE_TRADE_LICENSE_FEE"
                },
                "type": "label",
                "localisation":{
                  "required":true,
                  "prefix": null,
                  "module":"rainmaker-common"
                }
              },
              {
                "variable": "license_issue_date",
                "value": {
                  "path": "PDF_STATIC_LABEL_CONSOLIDATED_TLCERTIFICATE_LICENSE_ISSUE_DATE"
                },
                "type": "label",
                "localisation":{
                  "required":true,
                  "prefix": null,
                  "module":"rainmaker-common"
                }
              },
              {
                "variable": "license_validity",
                "value": {
                  "path": "PDF_STATIC_LABEL_CONSOLIDATED_TLCERTIFICATE_LICENSE_VALIDITY"
                },
                "type": "label",
                "localisation":{
                  "required":true,
                  "prefix": null,
                  "module":"rainmaker-common"
                }
              },
              {
                "variable": "approved_by",
                "value": {
                  "path": "PDF_STATIC_LABEL_CONSOLIDATED_TLCERTIFICATE_APPROVED_BY"
                },
                "type": "label",
                "localisation":{
                  "required":true,
                  "prefix": null,
                  "module":"rainmaker-common"
                }
              },
              {
                "variable": "commissioner",
                "value": {
                  "path": "PDF_STATIC_LABEL_CONSOLIDATED_TLCERTIFICATE_COMMISSIONER"
                },
                "type": "label",
                "localisation":{
                  "required":true,
                  "prefix": null,
                  "module":"rainmaker-common"
                }
              }
            ]
          },
          {
            "externalAPI": [
              {
                "path": "http://localhost:8082/egov-mdms-service/v1/_get",
                "queryParam": "moduleName=tenant&masterName=tenants&tenantId=pb&filter=%5B?(@.code=='{$.tenantId}')%5D",
                "apiRequest": null,
                "responseMapping":[
                  {
                    "variable":"ulb-address",
                    "value":"$.MdmsRes.tenant.tenants[0].address"
                  },
                  {
                    "variable":"corporationContact",
                    "value":"$.MdmsRes.tenant.tenants[0].contactNumber"
                  },
                  {
                    "variable":"corporationWebsite",
                    "value":"$.MdmsRes.tenant.tenants[0].domainUrl"
                  },
                  {
                    "variable":"corporationEmail",
                    "value":"$.MdmsRes.tenant.tenants[0].emailId"
                  }
                ]
              },
              {
                "path": "http://localhost:8288/filestore/v1/files/url",
                "queryParam": "tenantId=pb,fileStoreIds=$.tradeLicenseDetail.applicationDocuments[?(@.documentType== 'OWNERPHOTO')].fileStoreId",
                "apiRequest": null,
                "requesttype": "GET",
                "responseMapping":[
                  {
                    "variable":"userpic",
                    "value":"$.fileStoreIds[0].url",
                    "type": "image"
                  }
                ]
              },
              {
                "path": "http://localhost:8282/egov-workflow-v2/egov-wf/process/_search",
                "queryParam": "businessIds=$.applicationNumber,history=true,tenantId=$.tenantId",
                "apiRequest": null,
                "responseMapping":[
                  {
                    "variable":"approvedBy",
                    "value":"$.ProcessInstances[?(@.action == 'APPROVE')].assigner.name"
                  }

                ]
              }

            ]
          },
          {
            "qrcodeConfig": [
              {
                "variable": "qrCode",
                "value": "{{signedCertificateData}}"
              }
            ]
          }
        ]

      }
    ]
  }
}
```

v) Now, under `format-config` folder, again create a file by the name of `digit-developer-guide.json` and put the following content into it -

```json
{
  "key": "vtcertificate",
  "config": {
    "defaultStyle": {
      "font": "Cambay"
    },
    "content": [
      {
        "image": "{{qrCode}}",
        "absolutePosition" : {
          "x" : 480,
          "y" : 5
        },
        "width": 100,
        "height": 100
      },
      {
        "style":"noc-head",
        "table":{
          "widths":[
            "*"
          ],
          "body":[
            [
              {
                "image": "{{userpic}}",
                "width": 70,
                "height": 82,
                "alignment": "center",
                "margin": [
                  0,
                  10,
                  0,
                  10
                ]
              }
            ],
            [
              {
                "stack": [
                  {
                    "text":"{{municipal_corportaion}}",
                    "style":"receipt-logo-header"
                  },
                  {
                    "text":"{{ulb-address}}",
                    "style":"receipt-logo-sub-header"
                  },
                  {
                    "style": "noc-head",
                    "table": {
                      "widths": [
                        "*",
                        "*"
                      ],
                      "body": [
                        [
                          {
                            "text": "{{corporation_contact}} : {{corporationContact}} ",
                            "style": "receipt-sub-address-sub-header"

                          }
                        ]
                      ]
                    },
                    "layout": "noBorders"
                  },
                  {
                    "style": "noc-head",
                    "table": {
                      "widths": [
                        "*",
                        "*"
                      ],
                      "body": [
                        [
                          {
                            "text": "{{corporation_website}} : {{corporationWebsite}}",
                            "style": "receipt-sub-website-sub-header"

                          }
                        ]
                      ]
                    },
                    "layout": "noBorders"
                  },
                  {
                    "style": "noc-head",
                    "table": {
                      "widths": [
                        "*",
                        "*"
                      ],
                      "body": [
                        [
                          {
                            "text": "{{corporation_email}} : {{corporationEmail}}",
                            "style": "receipt-sub-email-sub-header"

                          }
                        ]
                      ]
                    },
                    "layout": "noBorders"
                  }
                ],
                "alignment":"left",
                "margin":[
                  0,
                  10,
                  0,
                  0
                ]
              }
            ],
            [
              {
                "stack": [
                  {
                    "text":"Birth Certificate",
                    "style":"receipt-sub-logo-header"
                  },
                  {
                    "style":"noc-head",
                    "table":{
                      "widths":[
                        "35%",
                        "65%"
                      ],
                      "body":[
                        [
                          {
                            "text":"Applicant Name",
                            "style":"receipt-sub-logo-sub-header"
                          },
                          {
                            "text":"{{applicantName}}",
                            "style":"receipt-sub-logo-sub-header"
                          }
                        ]
                      ]
                    },
                    "layout":"noBorders"
                  },
                  {
                    "style":"noc-head",
                    "table":{
                      "widths":[
                        "35%",
                        "65%"
                      ],
                      "body":[
                        [
                          {
                            "text":"Application Number",
                            "style":"receipt-sub-logo-sub-header"
                          },
                          {
                            "text":"{{applicationNo}}",
                            "style":"receipt-sub-logo-sub-header"
                          }
                        ]
                      ]
                    },
                    "layout":"noBorders"
                  },
                  {
                    "style":"noc-head",
                    "table":{
                      "widths":[
                        "35%",
                        "65%"
                      ],
                      "body":[
                        [
                          {
                            "text":"Applicant Address",
                            "style":"receipt-sub-logo-sub-header"
                          },
                          {
                            "text":"{{address}}",
                            "style":"receipt-sub-logo-sub-header"
                          }
                        ]
                      ]
                    },
                    "layout":"noBorders"
                  },
                  {
                    "style":"noc-head",
                    "table":{
                      "widths":[
                        "35%",
                        "65%"
                      ],
                      "body":[
                        [
                          {
                            "text":"Certificate Issue Date",
                            "style":"receipt-sub-logo-sub-header"
                          },
                          {
                            "text":"{{birthIdIssueDate}}",
                            "style":"receipt-sub-logo-sub-header"
                          }
                        ]
                      ]
                    },
                    "layout":"noBorders"
                  }
                ],
                "alignment":"left",
                "margin":[
                  0,
                  10,
                  0,
                  0
                ]
              }
            ]
          ]
        },
        "layout":"noBorders"
      },
      {
        "style":"receipt-approver",
        "columns": [
          {
            "text":[
              {
                "text":"{{approved_by}} ",
                "bold": true
              },
              {
                "text":" {{approvedBy}}",
                "bold": false
              }
            ],
            "alignment":"left"
          },
          {
            "text":[
              {
                "text":"{{commissioner}}",
                "bold": true
              }
            ],
            "alignment":"right"
          }
        ]
      }
    ],
    "styles": {
      "noc-head": {
        "margin": [
          -30,
          -35,
          0,
          -2
        ]
      },
      "receipt-approver": {
        "color": "#000000",
        "fontSize": 14,
        "letterSpacing": 0.6,
        "alignment": "center",
        "margin": [
          -10,
          50,
          0,
          1
        ]
      },
      "receipt-logo-header": {
        "color": "#000000",
        "fontSize": 20,
        "letterSpacing": 0.74,
        "alignment": "center",
        "margin": [
          0,
          0,
          0,
          5
        ]
      },
      "receipt-sub-logo-header": {
        "color": "#000000",
        "fontSize": 18,
        "letterSpacing": 0.74,
        "alignment": "center",
        "margin": [
          0,
          5,
          0,
          5
        ]
      },
      "receipt-logo-sub-header": {
        "color": "#484848",
        "fontSize": 14,
        "letterSpacing": 0.6,
        "alignment": "center",
        "margin": [
          0,
          5,
          0,
          0
        ]
      },
      "receipt-sub-logo-sub-header": {
        "color": "#484848",
        "fontSize": 14,
        "letterSpacing": 0.6,
        "alignment": "left",
        "margin": [
          50,
          40,
          0,
          0
        ]
      },
      "receipt-sub-address-sub-header": {
        "color": "#484848",
        "fontSize": 14,
        "letterSpacing": 0.1,
        "alignment": "right",
        "margin": [
          50,
          30,
          -90,
          0
        ]
      },
      "receipt-sub-website-sub-header": {
        "color": "#484848",
        "fontSize": 14,
        "letterSpacing": 0.1,
        "alignment": "right",
        "margin": [
          50,
          30,
          -120,
          0
        ]
      },
      "receipt-sub-email-sub-header": {
        "color": "#484848",
        "fontSize": 14,
        "letterSpacing": 0.1,
        "alignment": "right",
        "margin": [
          50,
          30,
          -110,
          0
        ]
      }
    }
  }
}
```

vi) Now, open PDF service (under core-services repository of DIGIT-Dev) on your IDE. Open `Environment.js` file and change the following properties to point to the local config files that have been created. For example, in my local setup I have pointed these to the local files that I created -

```
DATA_CONFIG_URLS: "file:///eGov/configs/pdf-service/data-config/digit-developer-guide.json",
FORMAT_CONFIG_URLS: "file:///eGov/configs/pdf-service/format-config/digit-developer-guide.json"
```

vii) Now, make sure that Kafka and Workflow services are running locally and port-forward the following services -

egov-user to port 8284

egov-localization to port 8286

egov-filestore to 8288

egov-mdms to 8082

viii) PDF service is now ready to be started up. Execute the following commands to start it up -

```
> npm install
> npm run dev
```

ix) Once PDF service is up hit the following cURL to look at the created PDF -

```bash
curl --location --request POST 'http://localhost:8081/pdf-service/v1/_createnosave?key=vtcertificate&tenantId=pb' \
--header 'authority: dev.digit.org' \
--header 'sec-ch-ua: " Not;A Brand";v="99", "Google Chrome";v="91", "Chromium";v="91"' \
--header 'accept: application/json' \
--header 'dnt: 1' \
--header 'sec-ch-ua-mobile: ?0' \
--header 'user-agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.101 Safari/537.36' \
--header 'content-type: application/json;charset=UTF-8' \
--header 'origin: https://dev.digit.org' \
--header 'sec-fetch-site: same-origin' \
--header 'sec-fetch-mode: cors' \
--header 'sec-fetch-dest: empty' \
--header 'referer: https://dev.digit.org/employee/tradelicence/search-preview?applicationNumber=PB-TL-2021-07-13-006531&tenantId=pb.amritsar' \
--header 'accept-language: en-GB,en-US;q=0.9,en;q=0.8' \
--header 'cookie: _ga=GA1.2.1990427088.1605864396; amplitude_id_fef1e872c952688acd962d30aa545b9edigit.org=eyJkZXZpY2VJZCI6IjQzYzEyMDE0LTNhNTYtNGRiMS1iNDQzLTA5NWU2Zjc3ZGU2MlIiLCJ1c2VySWQiOm51bGwsIm9wdE91dCI6ZmFsc2UsInNlc3Npb25JZCI6MTYyMjUyNjY2NTkxMywibGFzdEV2ZW50VGltZSI6MTYyMjUyNjcyMTQyNywiZXZlbnRJZCI6MiwiaWRlbnRpZnlJZCI6MSwic2VxdWVuY2VOdW1iZXIiOjN9' \
--data-raw '{
    "RequestInfo": {
        "apiId": "Rainmaker",
        "ver": ".01",
        "action": "_get",
        "did": "1",
        "key": "",
        "msgId": "20170310130900|en_IN",
        "requesterId": "",
        "authToken": "2c21ee1f-2b26-47bf-8ce8-39cc88b0ca3f",
        "responseType": "arraybuffer",
        "userInfo": {
            "id": 24226,
            "uuid": "40dceade-992d-4a8f-8243-19dda76a4171",
            "userName": "amr001",
            "name": "leela",
            "mobileNumber": "9814424443",
            "emailId": "leela@llgmail.com",
            "locale": null,
            "type": "EMPLOYEE",
            "roles": [
                {
                    "name": "PT Doc Verifier",
                    "code": "PT_DOC_VERIFIER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "PT Counter Employee",
                    "code": "PT_CEMP",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "PT Field Inspector",
                    "code": "PT_FIELD_INSPECTOR",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "PT Counter Approver",
                    "code": "PT_APPROVER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "Property Approver",
                    "code": "Property Approver",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "CSC Collection Operator",
                    "code": "CSC_COLL_OPERATOR",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "Employee",
                    "code": "EMPLOYEE",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "NoC counter employee",
                    "code": "NOC_CEMP",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "TL Counter Employee",
                    "code": "TL_CEMP",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "Anonymous User",
                    "code": "ANONYMOUS",
                    "tenantId": "pb"
                },
                {
                    "name": "TL Field Inspector",
                    "code": "TL_FIELD_INSPECTOR",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "TL Creator",
                    "code": "TL_CREATOR",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "NoC counter Approver",
                    "code": "NOC_APPROVER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "TL Approver",
                    "code": "TL_APPROVER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "Super User",
                    "code": "SUPERUSER",
                    "tenantId": "pb"
                },
                {
                    "name": "BPA Services Approver",
                    "code": "BPA_APPROVER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "Field Employee",
                    "code": "FEMP",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "Counter Employee",
                    "code": "CEMP",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "NoC Field Inpector",
                    "code": "NOC_FIELD_INSPECTOR",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "Super User",
                    "code": "SUPERUSER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "Grievance Officer",
                    "code": "GO",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "NoC Doc Verifier",
                    "code": "NOC_DOC_VERIFIER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "Collection Operator",
                    "code": "COLL_OPERATOR",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "TL doc verifier",
                    "code": "TL_DOC_VERIFIER",
                    "tenantId": "pb.amritsar"
                }
            ],
            "active": true,
            "tenantId": "pb.amritsar"
        }
    },
    "BirthRegistrationApplications": [
         {
            "id": "49e39cd5-a907-44ab-b654-1ff1bd121251",
            "tenantId": "pb.amritsar",
            "applicationNumber": "PB-BTR-2022-09-07-000377",
            "babyFirstName": "Rahul",
            "babyLastName": "Singh",
            "fatherMobileNumber": null,
            "motherMobileNumber": null,
            "doctorName": "Dr. Ram",
            "hospitalName": "Fortis",
            "placeOfBirth": "Palampur",
            "timeOfBirth": 12072001,
            "address": {
                "tenantId": "pb.amritsar",
                "doorNo": "1010",
                "latitude": 0.0,
                "longitude": 0.0,
                "addressId": null,
                "addressNumber": "34 GA",
                "type": "RESIDENTIAL",
                "addressLine1": "KP Layout",
                "addressLine2": "",
                "landmark": "Petrol pump",
                "city": "Amritsar",
                "pincode": "143501",
                "detail": "adetail",
                "buildingName": "Avigna Residence",
                "street": "12th Main",
                "locality": null,
                "registrationId": "aregistrationid",
                "id": "c5b2c706-7f49-4948-b1b4-4554eff54cb0"
            },
            "fatherOfApplicant": {
                "id": "61646440-d184-48f2-92b3-1b50a7babcf3",
                "userName": null,
                "password": null,
                "salutation": null,
                "name": null,
                "gender": null,
                "mobileNumber": null,
                "emailId": null,
                "altContactNumber": null,
                "pan": null,
                "aadhaarNumber": null,
                "permanentAddress": null,
                "permanentCity": null,
                "permanentPincode": null,
                "correspondenceCity": null,
                "correspondencePincode": null,
                "correspondenceAddress": null,
                "active": null,
                "dob": null,
                "pwdExpiryDate": null,
                "locale": null,
                "type": null,
                "signature": null,
                "accountLocked": null,
                "roles": null,
                "fatherOrHusbandName": null,
                "bloodGroup": null,
                "identificationMark": null,
                "photo": null,
                "createdBy": null,
                "createdDate": null,
                "lastModifiedBy": null,
                "lastModifiedDate": null,
                "otpReference": null,
                "tenantId": null
            },
            "motherOfApplicant": {
                "id": "99856298-68ba-479f-aa31-f2f4954102f6",
                "userName": null,
                "password": null,
                "salutation": null,
                "name": null,
                "gender": null,
                "mobileNumber": null,
                "emailId": null,
                "altContactNumber": null,
                "pan": null,
                "aadhaarNumber": null,
                "permanentAddress": null,
                "permanentCity": null,
                "permanentPincode": null,
                "correspondenceCity": null,
                "correspondencePincode": null,
                "correspondenceAddress": null,
                "active": null,
                "dob": null,
                "pwdExpiryDate": null,
                "locale": null,
                "type": null,
                "signature": null,
                "accountLocked": null,
                "roles": null,
                "fatherOrHusbandName": null,
                "bloodGroup": null,
                "identificationMark": null,
                "photo": null,
                "createdBy": null,
                "createdDate": null,
                "lastModifiedBy": null,
                "lastModifiedDate": null,
                "otpReference": null,
                "tenantId": null
            },
            "auditDetails": {
                "createdBy": "11b0e02b-0145-4de2-bc42-c97b96264807",
                "lastModifiedBy": "11b0e02b-0145-4de2-bc42-c97b96264807",
                "createdTime": 1662545605812,
                "lastModifiedTime": 1662545605812
            },
            "workflow": null
        }
    ]
}'
```

**Note: Below steps are for when you deploy your code to the DIGIT env, not for local development. You may choose to do his when you build and deploy.**&#x20;

#### Deployment of PDF service

Go to your fork of the DIGIT-DevOps repository. Under the `deploy-as-code/helm/environments` directory, find the deployment helm chart that was used to deploy DIGIT. &#x20;

In the deployment helm chart (which was used to setup the DIGIT environment), find "pdf-service". Find the `"data-config-urls"` property and add the path to your new PDF config file here. For this module, we have added `file:///work-dir/configs/pdf-service/data-config/digit-developer-guide.json` to the end of the `data-config-urls`. The code block is shown below for reference:

```yaml
pdf-service:
  replicas: 1
  initContainers:
    gitSync:
      repo: "git@github.com:egovernments/configs"
      branch: "DEV"
  data-config-urls: "file:///work-dir/configs/pdf-service/data-config/tradelicense-receipt.json,file:///work-dir/configs/pdf-service/data-config/property-receipt.json,file:///work-dir/configs/pdf-service/data-config/property-bill.json,file:///work-dir/configs/pdf-service/data-config/tradelicense-bill.json,file:///work-dir/configs/pdf-service/data-config/firenoc-receipt.json,file:///work-dir/configs/pdf-service/data-config/pt-receipt.json,file:///work-dir/configs/pdf-service/data-config/tl-receipt.json,file:///work-dir/configs/pdf-service/data-config/consolidatedbill.json,file:///work-dir/configs/pdf-service/data-config/consolidatedreceipt.json,file:///work-dir/configs/pdf-service/data-config/tlapplication.json,file:///work-dir/configs/pdf-service/data-config/ws-consolidatedacknowlegment.json,file:///work-dir/configs/pdf-service/data-config/ws-consolidatedsewerageconnection.json,file:///work-dir/configs/pdf-service/data-config/tlcertificate.json,file:///work-dir/configs/pdf-service/data-config/buildingpermit.json,file:///work-dir/configs/pdf-service/data-config/ptmutationcertificate.json,file:///work-dir/configs/pdf-service/data-config/tlrenewalcertificate.json,file:///work-dir/configs/pdf-service/data-config/bpa-revocation.json,file:///work-dir/configs/pdf-service/data-config/ws-applicationsewerage.json,file:///work-dir/configs/pdf-service/data-config/ws-applicationwater.json,file:///work-dir/configs/pdf-service/data-config/buildingpermit-low.json,file:///work-dir/configs/pdf-service/data-config/misc-receipt.json,file:///work-dir/configs/pdf-service/data-config/ws-estimationnotice.json,file:///work-dir/configs/pdf-service/data-config/ws-sanctionletter.json,file:///work-dir/configs/pdf-service/data-config/ws-bill.json,file:///work-dir/configs/pdf-service/data-config/ws-onetime-receipt.json,file:///work-dir/configs/pdf-service/data-config/occupancy-certificate.json, file:///work-dir/configs/pdf-service/data-config/bill-amendment.json, file:///work-dir/configs/pdf-service/data-config/bill-amendment-note.json, file:///work-dir/configs/pdf-service/data-config/fsm-receipt.json, file:///work-dir/configs/pdf-service/data-config/sewerage-bill-amendment-note.json, file:///work-dir/configs/pdf-service/data-config/mcollect-bill.json, file:///work-dir/configs/pdf-service/data-config/mcollect-challan.json,file:///work-dir/configs/pdf-service/data-config/birth-certificate-pdf.json, file:///work-dir/configs/pdf-service/data-config/death-certificate.json,file:///work-dir/configs/pdf-service/data-config/ws-waterdisconnection.json,file:///work-dir/configs/pdf-service/data-config/ws-sewagedisconnection.json,file:///work-dir/configs/pdf-service/data-config/ws-waterdisconnectionnotice.json,file:///work-dir/configs/pdf-service/data-config/ws-seweragedisconnectionnotice.json,file:///work-dir/configs/pdf-service/data-config/ws-sewerageconnectiondetails.json,file:///work-dir/configs/pdf-service/data-config/ws-waterconnectiondetails-metered.json,file:///work-dir/configs/pdf-service/data-config/ws-waterconnectiondetails-nonmetered.json,file:///work-dir/configs/pdf-service/data-config/digit-developer-guide.json"
```

Raise a PR for this to the appropriate branch of DevOps which was forked/used to create the deployment.

Once that is merged, restart the PDF service in the k8s cluster. It will pick up the latest config from this file above.

_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
