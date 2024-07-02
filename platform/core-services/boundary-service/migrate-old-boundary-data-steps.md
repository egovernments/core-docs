# Migrate Old Boundary Data - Steps

## Overview

This document provides information on migrating location data from an older JSON-based configuration to a newly developed boundary service. A boundary-migration service has been created to facilitate this process. Users can migrate the data to the new boundary service by calling a single API.

## Steps

Below is the step-by-step procedure for the same:-

1. Import the boundary migration service from [here](https://github.com/egovernments/Digit-Core/tree/boundary-migration-service/core-services/boundary-migration) in an IDE (preferably IntelliJ) and start the service after building it.
2. Copy the boundary-data JSON that needs to be migrated as an example we are taking [boundary-data of Phagwara (Punjab)](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/phagwara/egov-location/boundary-data.json#L1C1-L1C1). and adding RequestInfo inside this as shown below.

```
{
	“RequestInfo”: {} ,
	“tenantId”: ”default” ,
    “moduleName”: “egov-location” ,
    “TenantBoundary”: []
}
```

3. Open Postman and create a new HTTP endpoint with a path as

```
http://localhost:8081/boundary/_migrate
```

and the above as the endpoint request body.&#x20;

<mark style="background-color:blue;">**PS:**</mark> <mark style="background-color:blue;"></mark><mark style="background-color:blue;">The boundary-migration service is assumed to run on port 8081. If it is running on a different port, check the active port and update the path accordingly.</mark>

4. Send the request and if the endpoint path and request body are correct the response would be 200 OK.

**Below is a reference CURL:**

{% code lineNumbers="true" %}
```
curl --location 'http://localhost:8081/boundary/_migrate' \
--header 'Content-Type: application/json' \
--data '{
    "RequestInfo": {
        "apiId": "string",
        "ver": "string",
        "ts": 0,
        "action": "string",
        "did": "string",
        "key": "string",
        "msgId": "string",
        "requesterId": "string",
        "authToken": "string",
        "userInfo": {
            "tenantId": "string",
            "id": 0,
            "uuid": "string"
        }
    },
    "tenantId": "pb.phagwara",
    "moduleName": "egov-location",
    "TenantBoundary": [
        {
            "hierarchyType": {
                "code": "ADMIN",
                "name": "ADMIN"
            },
            "boundary": {
                "id": 1,
                "boundaryNum": 1,
                "name": "Phagwara",
                "localname": "Phagwara",
                "longitude": null,
                "latitude": null,
                "label": "City",
                "code": "pb.phagwara",
                "children": [
                    {
                        "id": "4b486f04-4f31-4cf7-bf03-62d725ace784",
                        "boundaryNum": 1,
                        "name": "Phagwara",
                        "localname": "Phagwara",
                        "longitude": null,
                        "latitude": null,
                        "label": "Zone",
                        "code": "PZN1",
                        "children": [
                            {
                                "id": "2583e7a6-140d-4f3c-9543-d7693849ed24",
                                "boundaryNum": 1,
                                "name": "WARD_1",
                                "localname": "WARD_1",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD1",
                                "children": []
                            },
                            {
                                "id": "b0b952ee-f53c-4c73-8063-be718fd93cdd",
                                "boundaryNum": 1,
                                "name": "WARD_2",
                                "localname": "WARD_2",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD2",
                                "children": [
                                    {
                                        "id": "3b0cdbae-b942-42fa-a03b-70c04e00d53d",
                                        "boundaryNum": 1,
                                        "name": "Asha Park Colony",
                                        "localname": "Asha Park Colony",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC10",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "ecf7079e-d3a4-4732-ad87-0b00b7b725bc",
                                        "boundaryNum": 1,
                                        "name": "Bhai Ghanaiya Ji Enclave",
                                        "localname": "Bhai Ghanaiya Ji Enclave",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC25",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "6d7d2816-f299-4618-b351-fa0699f246c7",
                                        "boundaryNum": 1,
                                        "name": "Bhai Ghanaiya Ji Nagar",
                                        "localname": "Bhai Ghanaiya Ji Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC26",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "170d78ed-726c-46a0-a8dc-242a7c81c038",
                                        "boundaryNum": 1,
                                        "name": "Chahal Nagar",
                                        "localname": "Chahal Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC33",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "91c96922-e36a-4a56-b2da-5a9c28787c07",
                                        "boundaryNum": 1,
                                        "name": "Dashmesh Nagar",
                                        "localname": "Dashmesh Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC40",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "307a4bc9-d238-4159-8727-32481c1514a6",
                                        "boundaryNum": 1,
                                        "name": "Green Park",
                                        "localname": "Green Park",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC65",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "98c41dd3-e192-415d-b225-1ddd48e6dbb8",
                                        "boundaryNum": 1,
                                        "name": "MANAV ENCLAVE",
                                        "localname": "MANAV ENCLAVE",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC109",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "deb0e5fe-aafe-436c-823c-9bc1d0c5d330",
                                        "boundaryNum": 1,
                                        "name": "N.R.I Enclave",
                                        "localname": "N.R.I Enclave",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC124",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "ea4caa8b-abe5-4526-8ec6-21fb9573989a",
                                        "boundaryNum": 1,
                                        "name": "New Vishwakarma Nagar",
                                        "localname": "New Vishwakarma Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC138",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "72614980-5782-4671-8080-95deecd28012",
                                        "boundaryNum": 1,
                                        "name": "Raja Garden Colony",
                                        "localname": "Raja Garden Colony",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC164",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "5e19000e-7fa1-48d0-9f56-8e16d47919dc",
                                "boundaryNum": 1,
                                "name": "WARD_3",
                                "localname": "WARD_3",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD3",
                                "children": [
                                    {
                                        "id": "9bf79ce5-5bf9-44fd-a769-8a2b5258d3a9",
                                        "boundaryNum": 1,
                                        "name": "Ashok Vihar",
                                        "localname": "Ashok Vihar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC11",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "5fddef40-00ab-406d-9b10-26bc24d8b9c8",
                                        "boundaryNum": 1,
                                        "name": "DR. SATISH NAGAR",
                                        "localname": "DR. SATISH NAGAR",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC48",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "78717620-b84b-4514-bc49-294bf3129e3b",
                                        "boundaryNum": 1,
                                        "name": "Green Avenue",
                                        "localname": "Green Avenue",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC62",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "6a3431c3-82b3-4509-a600-9f05e0682f27",
                                        "boundaryNum": 1,
                                        "name": "Green Valley",
                                        "localname": "Green Valley",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC66",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "a83f4eaf-41b3-43c7-9959-aafb4192b6ce",
                                        "boundaryNum": 1,
                                        "name": "Guru Nanak Nagar",
                                        "localname": "Guru Nanak Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC71",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "818b618b-de9e-4e21-9004-ef0fb0cc027c",
                                        "boundaryNum": 1,
                                        "name": "Hajipur",
                                        "localname": "Hajipur",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC76",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "2dc07769-a1b3-4505-9462-f6d9dc9bff30",
                                        "boundaryNum": 1,
                                        "name": "HARGOBIND ENCLAVE",
                                        "localname": "HARGOBIND ENCLAVE",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC80",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "1d600e07-0c64-45b9-9ae3-bba018d3d8c9",
                                        "boundaryNum": 1,
                                        "name": "Jeewan Nagar",
                                        "localname": "Jeewan Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC89",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "b8b69483-47e9-4c34-aac8-ca8ff851996a",
                                        "boundaryNum": 1,
                                        "name": "Khera Masit",
                                        "localname": "Khera Masit",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC99",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "2427abd1-031f-48e6-9451-3b9c84bf2e7c",
                                        "boundaryNum": 1,
                                        "name": "Kirti Nagar",
                                        "localname": "Kirti Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC103",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "940b4fad-9d75-43a0-b5de-ab4085293ff5",
                                        "boundaryNum": 1,
                                        "name": "MAIN KHALWARA ROAD",
                                        "localname": "MAIN KHALWARA ROAD",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC108",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "8976b9d9-a131-4e86-8854-e11d58f915b0",
                                        "boundaryNum": 1,
                                        "name": "NORTH AVENUE",
                                        "localname": "NORTH AVENUE",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC140",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "28303ef9-6448-46c4-8846-3d7d353d095b",
                                        "boundaryNum": 1,
                                        "name": "Palahi Road",
                                        "localname": "Palahi Road",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC145",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "01e9ee24-6012-4646-b5fa-b50d69ee9deb",
                                        "boundaryNum": 1,
                                        "name": "Parmar Colony",
                                        "localname": "Parmar Colony",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC148",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "87a38051-b43f-4791-949a-157e332f33b2",
                                "boundaryNum": 1,
                                "name": "WARD_4",
                                "localname": "WARD_4",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD4",
                                "children": [
                                    {
                                        "id": "48a2fbe5-ad7f-437d-9c42-6fded5532e02",
                                        "boundaryNum": 1,
                                        "name": "Dharam Kot",
                                        "localname": "Dharam Kot",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC44",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "5b8ee409-ac4c-4355-bc8f-a615b0839d60",
                                        "boundaryNum": 1,
                                        "name": "G T Road To Hoshiarpur Road",
                                        "localname": "G T Road To Hoshiarpur Road",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC52",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "946d6577-622d-40eb-96e8-ed05c68f414e",
                                        "boundaryNum": 1,
                                        "name": "Guru Nanak Avenue",
                                        "localname": "Guru Nanak Avenue",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC69",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "ce998365-0449-4420-b1c9-ebc0cde22b10",
                                        "boundaryNum": 1,
                                        "name": "Pritam Nagar",
                                        "localname": "Pritam Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC156",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "4315333c-eb5d-4755-9a3f-28a37ab527d7",
                                        "boundaryNum": 1,
                                        "name": "S.P Colony",
                                        "localname": "S.P Colony",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC172",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "f2dbff50-dd13-4ae0-ba14-4e5957f040c4",
                                "boundaryNum": 1,
                                "name": "WARD_5",
                                "localname": "WARD_5",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD5",
                                "children": [
                                    {
                                        "id": "2f05cf03-cbdc-4d1c-8989-4ef8be7a5dac",
                                        "boundaryNum": 1,
                                        "name": "Baba Gadhia To Dana Mandi",
                                        "localname": "Baba Gadhia To Dana Mandi",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC15",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "01b014f3-e54f-4472-a0df-8b513127ced9",
                                        "boundaryNum": 1,
                                        "name": "Bhularai Road",
                                        "localname": "Bhularai Road",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC28",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "23d91c85-332c-4efe-9b41-0507063ab65f",
                                        "boundaryNum": 1,
                                        "name": "City Heart Colony",
                                        "localname": "City Heart Colony",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC36",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "2c1891e0-adef-47e9-8e5e-77e4f2e0174c",
                                        "boundaryNum": 1,
                                        "name": "Guru Nanak Enclave",
                                        "localname": "Guru Nanak Enclave",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC70",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "23bdace2-452c-4b86-aca8-0f6123453487",
                                        "boundaryNum": 1,
                                        "name": "Purewal Nagar",
                                        "localname": "Purewal Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC161",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "ba7454af-1e75-463a-bd92-8b8aeb43261f",
                                        "boundaryNum": 1,
                                        "name": "Ranjit Nagar",
                                        "localname": "Ranjit Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC166",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "d09b83b0-824b-4b91-8401-29d496264911",
                                        "boundaryNum": 1,
                                        "name": "Ru Pinjni Mohalla",
                                        "localname": "Ru Pinjni Mohalla",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC171",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "7eb5cb43-e1d9-405f-813c-394812bb2372",
                                        "boundaryNum": 1,
                                        "name": "Sahibzada Ajit Singh Nagar",
                                        "localname": "Sahibzada Ajit Singh Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC175",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "3de89762-d4c6-482f-b571-d5e77d024f6f",
                                "boundaryNum": 1,
                                "name": "WARD_6",
                                "localname": "WARD_6",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD6",
                                "children": [
                                    {
                                        "id": "c90172a0-9b37-4aa0-8b17-a6f3d162f773",
                                        "boundaryNum": 1,
                                        "name": "Amar Nagar",
                                        "localname": "Amar Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC5",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "1339d160-8180-4db0-b551-f34438407988",
                                        "boundaryNum": 1,
                                        "name": "Gaunspur",
                                        "localname": "Gaunspur",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC56",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "b6afc7e5-5b43-4784-a2b8-d7078c8d628b",
                                        "boundaryNum": 1,
                                        "name": "Guru Ravidas Nagar",
                                        "localname": "Guru Ravidas Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC73",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "8d75a617-1f5d-4d41-83f0-fb70b606b1bc",
                                        "boundaryNum": 1,
                                        "name": "Harkrishan Nagar",
                                        "localname": "Harkrishan Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC81",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "d111f1a9-94c2-424b-b521-119ce6f6377b",
                                        "boundaryNum": 1,
                                        "name": "Kaulsar Mohalla",
                                        "localname": "Kaulsar Mohalla",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC96",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "444a1f25-ada9-4d43-a278-1c60fc8ffafa",
                                        "boundaryNum": 1,
                                        "name": "New Guru Harkrishan Nagar",
                                        "localname": "New Guru Harkrishan Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC132",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "152d261c-17e5-45ba-9f1a-233c84cb55f1",
                                        "boundaryNum": 1,
                                        "name": "New Sukhchain Nagar",
                                        "localname": "New Sukhchain Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC137",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "31a34d66-975e-4b62-ada2-837dd1053d44",
                                        "boundaryNum": 1,
                                        "name": "Ravinder Nagar",
                                        "localname": "Ravinder Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC168",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "5f05b1a8-ad9d-4e86-8614-52f3dfb583ac",
                                        "boundaryNum": 1,
                                        "name": "Shahid Joginder Singh Nagar",
                                        "localname": "Shahid Joginder Singh Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC186",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "64973403-9a02-4972-b567-2ef4e0e4b98b",
                                        "boundaryNum": 1,
                                        "name": "Taru Ka Wara",
                                        "localname": "Taru Ka Wara",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC206",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "5662f090-03d7-478c-98ba-f88b97a5e74d",
                                        "boundaryNum": 1,
                                        "name": "Vishwakarma Colony",
                                        "localname": "Vishwakarma Colony",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC213",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "d8b26439-9b40-4529-8cc2-1083a947a52b",
                                "boundaryNum": 1,
                                "name": "WARD_7",
                                "localname": "WARD_7",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD7",
                                "children": [
                                    {
                                        "id": "8e2cc725-b4f9-4d11-9e3a-f2ba18bd4f86",
                                        "boundaryNum": 1,
                                        "name": "Sukhchain Sahib Road",
                                        "localname": "Sukhchain Sahib Road",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC201",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "5a7548af-e9c4-491e-93dc-4987910197fc",
                                "boundaryNum": 1,
                                "name": "WARD_8",
                                "localname": "WARD_8",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD8",
                                "children": [
                                    {
                                        "id": "72ddd32d-2f81-4e64-9aa3-f926f4c4b29f",
                                        "boundaryNum": 1,
                                        "name": "Baba Fateh Singh Nagar",
                                        "localname": "Baba Fateh Singh Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC13",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "747d8981-54a1-4e2c-ac8f-24726ca47ade",
                                        "boundaryNum": 1,
                                        "name": "Basra Palace To Khothra Road",
                                        "localname": "Basra Palace To Khothra Road",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC23",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "31ac775c-b472-48df-926b-512022ff7e28",
                                        "boundaryNum": 1,
                                        "name": "Guru Hargobind Nagar",
                                        "localname": "Guru Hargobind Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC68",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "109d00d3-d57b-40fa-beee-6dd8bc144722",
                                        "boundaryNum": 1,
                                        "name": "Patel Nagar",
                                        "localname": "Patel Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC149",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "7178f938-e1df-46f7-82cf-77b90f4dcae5",
                                        "boundaryNum": 1,
                                        "name": "Sukhchain Nagar",
                                        "localname": "Sukhchain Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC200",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "47febeee-7ae4-4a4f-9e65-e0d3194709aa",
                                "boundaryNum": 1,
                                "name": "WARD_9",
                                "localname": "WARD_9",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD9",
                                "children": [
                                    {
                                        "id": "9d081b9f-a25e-4c0f-9191-eb148d1c3448",
                                        "boundaryNum": 1,
                                        "name": "Baba Gadhia",
                                        "localname": "Baba Gadhia",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC14",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "c9146974-f410-4e19-b4a5-9f2d40a75519",
                                        "boundaryNum": 1,
                                        "name": "Mohalla Subhash Nagar",
                                        "localname": "Mohalla Subhash Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC121",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "f6a1a4de-bbff-4a79-a695-8e4e8f8ece91",
                                        "boundaryNum": 1,
                                        "name": "New Professor Colony",
                                        "localname": "New Professor Colony",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC135",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "8c75e22c-4615-432a-b0b5-8f9a2e49c336",
                                        "boundaryNum": 1,
                                        "name": "Nri Colony",
                                        "localname": "Nri Colony",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC141",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "8494d7a6-d6ac-4602-8822-90fd7d016981",
                                        "boundaryNum": 1,
                                        "name": "Professor Colony",
                                        "localname": "Professor Colony",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC157",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "bfd0706f-911d-4a7a-9bc1-545c4aa1f704",
                                        "boundaryNum": 1,
                                        "name": "Saini Mohalla",
                                        "localname": "Saini Mohalla",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC176",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "8a03f7a6-50a6-4813-97f0-157f24aaedae",
                                        "boundaryNum": 1,
                                        "name": "Shiva Ji Nagar",
                                        "localname": "Shiva Ji Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC192",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "e7859953-e88e-4b5d-9405-03f5c056fc13",
                                        "boundaryNum": 1,
                                        "name": "Taki Mohalla",
                                        "localname": "Taki Mohalla",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC205",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "a9fc9918-e7d7-4123-9b74-8c0bedca779f",
                                        "boundaryNum": 1,
                                        "name": "Varinder Nagar",
                                        "localname": "Varinder Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC211",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "fa86ff48-9f41-4567-8b7d-77c3f702f22e",
                                        "boundaryNum": 1,
                                        "name": "Vikas Nagar",
                                        "localname": "Vikas Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC212",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "9f36c495-f1d9-45a9-a0a7-a54854fc1255",
                                "boundaryNum": 1,
                                "name": "WARD_10",
                                "localname": "WARD_10",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD10",
                                "children": [
                                    {
                                        "id": "e73d206e-1421-4bb4-aa5c-cdbbe0a3d74f",
                                        "boundaryNum": 1,
                                        "name": "Ankhi Nagar",
                                        "localname": "Ankhi Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC7",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "659869f5-ea47-49d9-bb95-cf0550f7fef5",
                                        "boundaryNum": 1,
                                        "name": "Kabir Nagar",
                                        "localname": "Kabir Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC92",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "4414d37b-d873-4369-a0f1-e72f38069947",
                                        "boundaryNum": 1,
                                        "name": "KHALSA ENCLAVE",
                                        "localname": "KHALSA ENCLAVE",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC97",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "a46e4140-e10a-469b-8c11-2bfeec8250a5",
                                        "boundaryNum": 1,
                                        "name": "Khalwara Gate",
                                        "localname": "Khalwara Gate",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC98",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "2b37c059-ded4-44dc-afc8-c77f634decaf",
                                "boundaryNum": 1,
                                "name": "WARD_11",
                                "localname": "WARD_11",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD11",
                                "children": [
                                    {
                                        "id": "c662b590-6427-4ac1-bbd6-6daba0f11f14",
                                        "boundaryNum": 1,
                                        "name": "Navi Dana Mandi",
                                        "localname": "Navi Dana Mandi",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC129",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "53f696e9-a1e5-4ba3-9208-7b80c479d218",
                                        "boundaryNum": 1,
                                        "name": "Plahi Gate",
                                        "localname": "Plahi Gate",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC152",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "73364e65-143d-4bf3-ad46-34a06899fb8d",
                                        "boundaryNum": 1,
                                        "name": "Sabzi Mandi",
                                        "localname": "Sabzi Mandi",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC173",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "b86f59fe-1541-4950-b1e6-673ad021722e",
                                        "boundaryNum": 1,
                                        "name": "Soond Colony",
                                        "localname": "Soond Colony",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC195",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "f4217655-10c6-4787-b3a8-19bb1ebd49af",
                                "boundaryNum": 1,
                                "name": "WARD_12",
                                "localname": "WARD_12",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD12",
                                "children": [
                                    {
                                        "id": "04c1fc6b-1567-4ae5-961a-1f0bc9e1abad",
                                        "boundaryNum": 1,
                                        "name": "Anand Nagar",
                                        "localname": "Anand Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC6",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "aadb1ce2-6a3b-4c4e-a28b-cf275da80a44",
                                        "boundaryNum": 1,
                                        "name": "Arjun Pura",
                                        "localname": "Arjun Pura",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC8",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "9ebd1986-8462-47c7-bd0a-411316b4c6ee",
                                        "boundaryNum": 1,
                                        "name": "Shahid Bhagat Singh Nagar",
                                        "localname": "Shahid Bhagat Singh Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC185",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "f8951d9f-311d-47bb-ab15-ada48db8af4f",
                                "boundaryNum": 1,
                                "name": "WARD_13",
                                "localname": "WARD_13",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD13",
                                "children": [
                                    {
                                        "id": "bb7ffa64-5a50-47ef-b85f-bdfd4f67bc41",
                                        "boundaryNum": 1,
                                        "name": "chora Khoo",
                                        "localname": "chora Khoo",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC34",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "e078fce2-4fac-489f-a514-a6d0f88a5b6e",
                                        "boundaryNum": 1,
                                        "name": "Naiya Wala Chowk",
                                        "localname": "Naiya Wala Chowk",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC125",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "404b5d49-0623-4d6a-8625-761a985a0494",
                                "boundaryNum": 1,
                                "name": "WARD_14",
                                "localname": "WARD_14",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD14",
                                "children": [
                                    {
                                        "id": "88de4f92-ea13-454d-905a-300f4b6177bb",
                                        "boundaryNum": 1,
                                        "name": "Daddal Mohalla",
                                        "localname": "Daddal Mohalla",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC38",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "c4b8c94b-a27f-4152-98c5-629db1c57c5c",
                                        "boundaryNum": 1,
                                        "name": "Lamian Mohalla",
                                        "localname": "Lamian Mohalla",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC106",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "88c486cf-59f4-437b-85cb-6959538c192c",
                                        "boundaryNum": 1,
                                        "name": "Purana Thanna",
                                        "localname": "Purana Thanna",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC158",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "a1fd1347-34d8-4893-b316-41ec5d0ff6c9",
                                        "boundaryNum": 1,
                                        "name": "Sachra Mohalla",
                                        "localname": "Sachra Mohalla",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC174",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "979d01f9-50a8-42f1-b579-f27b4ebb5c39",
                                        "boundaryNum": 1,
                                        "name": "Sarafa Bazar",
                                        "localname": "Sarafa Bazar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC182",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "8a3b208c-b984-4ffe-bea6-f2dcd0a44a2e",
                                        "boundaryNum": 1,
                                        "name": "Sudan Mohalla",
                                        "localname": "Sudan Mohalla",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC196",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "8fb3725d-0108-47ac-8442-54ffb4ef2946",
                                        "boundaryNum": 1,
                                        "name": "Sufia Mohalla",
                                        "localname": "Sufia Mohalla",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC198",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "39b65c52-d718-423b-b2c1-7354187da50f",
                                "boundaryNum": 1,
                                "name": "WARD_15",
                                "localname": "WARD_15",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD15",
                                "children": [
                                    {
                                        "id": "d748ca91-b717-43f4-a54a-66254bd4e2a2",
                                        "boundaryNum": 1,
                                        "name": "Ahluwalia Mohalla",
                                        "localname": "Ahluwalia Mohalla",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC4",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "50825d48-8d89-4230-866e-75584b1da514",
                                        "boundaryNum": 1,
                                        "name": "Bagh Sudan",
                                        "localname": "Bagh Sudan",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC17",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "c12e61ff-2967-42b9-bcad-ade13f7f1e10",
                                        "boundaryNum": 1,
                                        "name": "Sikha Mohalla",
                                        "localname": "Sikha Mohalla",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC193",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "4145cf2a-21a8-418c-97bc-f017fe57e2fa",
                                        "boundaryNum": 1,
                                        "name": "Tabacco Kutta Mohalla",
                                        "localname": "Tabacco Kutta Mohalla",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC203",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "81653fdc-688d-4ec2-a43c-e41237067a14",
                                "boundaryNum": 1,
                                "name": "WARD_16",
                                "localname": "WARD_16",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD16",
                                "children": [
                                    {
                                        "id": "5eac43ba-07fa-4db9-9113-2c4d1e1f5326",
                                        "boundaryNum": 1,
                                        "name": "Mehli Gate",
                                        "localname": "Mehli Gate",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC113",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "7efad2f8-b5b3-468e-8c16-d5628b2d030b",
                                        "boundaryNum": 1,
                                        "name": "Mohalla Karbala",
                                        "localname": "Mohalla Karbala",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC117",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "abb1070c-af44-4e34-bbe7-46abe3d550dc",
                                        "boundaryNum": 1,
                                        "name": "NIGAHAN MOHALLA",
                                        "localname": "NIGAHAN MOHALLA",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC139",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "e8ff961d-506c-4cab-9141-43a49d03ff26",
                                        "boundaryNum": 1,
                                        "name": "Shastri Nagar",
                                        "localname": "Shastri Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC189",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "d8aeefdb-dfd9-4bd3-8e6c-fc1743cb07a7",
                                        "boundaryNum": 1,
                                        "name": "Thanedar Mohalla",
                                        "localname": "Thanedar Mohalla",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC208",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "9a574042-1196-4775-a09b-806d9e7cc4c1",
                                "boundaryNum": 1,
                                "name": "WARD_17",
                                "localname": "WARD_17",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD17",
                                "children": [
                                    {
                                        "id": "181cb55f-3896-4f22-b1b3-84c211388f5e",
                                        "boundaryNum": 1,
                                        "name": "Aatisbaja Mohalla",
                                        "localname": "Aatisbaja Mohalla",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC1",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "f79c0d1a-10c0-41f4-89f2-5f0fa65fcb45",
                                        "boundaryNum": 1,
                                        "name": "Balmik Mohalla",
                                        "localname": "Balmik Mohalla",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC19",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "6de24561-b233-41ef-9a35-406da0a6102d",
                                        "boundaryNum": 1,
                                        "name": "Katehra Chowk",
                                        "localname": "Katehra Chowk",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC94",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "32fb89fb-f53e-4c7e-a3b6-75edb2f0e6f8",
                                        "boundaryNum": 1,
                                        "name": "Korhian Mohalla",
                                        "localname": "Korhian Mohalla",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC104",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "4a3de197-30b1-45c1-92e8-2f43bdcf929b",
                                        "boundaryNum": 1,
                                        "name": "Purbian Mohalla",
                                        "localname": "Purbian Mohalla",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC160",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "3d088be1-eb75-4e00-a0ae-37a4c947b29a",
                                        "boundaryNum": 1,
                                        "name": "Sandhura Mandir",
                                        "localname": "Sandhura Mandir",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC178",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "dc726240-5f54-4c12-bf42-3796f8dce0a7",
                                        "boundaryNum": 1,
                                        "name": "Sarabha Nagar",
                                        "localname": "Sarabha Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC181",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "d903c265-de9e-4395-b65e-49ce89924ca6",
                                "boundaryNum": 1,
                                "name": "WARD_18",
                                "localname": "WARD_18",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD18",
                                "children": [
                                    {
                                        "id": "9ead5fa0-cb6d-4f21-a6b3-1e4982728b76",
                                        "boundaryNum": 1,
                                        "name": "AROHYA MOHALLA",
                                        "localname": "AROHYA MOHALLA",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC9",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "28f5ff3e-0a3e-40d5-ab84-00705c3eadd2",
                                        "boundaryNum": 1,
                                        "name": "Avtar Nagar",
                                        "localname": "Avtar Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC12",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "71c89281-d450-44a1-8d3a-b3704b6ec8e2",
                                        "boundaryNum": 1,
                                        "name": "Cinema Road",
                                        "localname": "Cinema Road",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC35",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "c3b87a17-c17e-4996-ba8f-ad2f63f353c2",
                                        "boundaryNum": 1,
                                        "name": "G T Road Jal. To Ldh.",
                                        "localname": "G T Road Jal. To Ldh.",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC51",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "3014d968-a4a5-4a46-993c-127896012bba",
                                        "boundaryNum": 1,
                                        "name": "Gandhi Nagar",
                                        "localname": "Gandhi Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC55",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "01651392-82fb-4949-85b1-04e06da5101e",
                                        "boundaryNum": 1,
                                        "name": "JAINIA MOHALA",
                                        "localname": "JAINIA MOHALA",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC86",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "7da0f4c7-0552-453b-995c-01467187ab7f",
                                        "boundaryNum": 1,
                                        "name": "Mohalla Ohrian",
                                        "localname": "Mohalla Ohrian",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC119",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "e715b971-8d17-458f-8772-1e3aaeef2584",
                                        "boundaryNum": 1,
                                        "name": "Moti Bazar",
                                        "localname": "Moti Bazar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC123",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "e4b19c57-e909-41ff-80aa-d7c7480e000c",
                                        "boundaryNum": 1,
                                        "name": "Old Civil Hospital To Banga Road",
                                        "localname": "Old Civil Hospital To Banga Road",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC142",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "3d88ec8b-d97c-4936-a076-77abb4d0d84c",
                                        "boundaryNum": 1,
                                        "name": "Sarai Road",
                                        "localname": "Sarai Road",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC183",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "4aa27bfb-e11d-47fb-b5b5-241b8c4ad8ac",
                                "boundaryNum": 1,
                                "name": "WARD_19",
                                "localname": "WARD_19",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD19",
                                "children": [
                                    {
                                        "id": "8fe926ea-fa98-4afa-b787-a00dd59d059d",
                                        "boundaryNum": 1,
                                        "name": "Babbar Akali Market",
                                        "localname": "Babbar Akali Market",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC16",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "007712f5-46f7-4472-afc8-933f6beb0b9a",
                                        "boundaryNum": 1,
                                        "name": "Bansa Wala Bazar Road To Masit",
                                        "localname": "Bansa Wala Bazar Road To Masit",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC20",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "25e8b6fb-e36d-4325-ad28-57afbebcce7d",
                                        "boundaryNum": 1,
                                        "name": "Chadha Market",
                                        "localname": "Chadha Market",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC32",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "cea86efb-e5c4-41fa-89db-9e2f2e00ae3b",
                                        "boundaryNum": 1,
                                        "name": "Gandhi Chowk To Loha Mandi",
                                        "localname": "Gandhi Chowk To Loha Mandi",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC54",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "b735fbf3-49f5-4323-be08-15cd6cd9fd9b",
                                        "boundaryNum": 1,
                                        "name": "Gur Mandi Road",
                                        "localname": "Gur Mandi Road",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC67",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "30d4c060-2ceb-4905-a2c1-1ca8a9913609",
                                        "boundaryNum": 1,
                                        "name": "Handa Complex",
                                        "localname": "Handa Complex",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC78",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "0db8848b-7e82-4db1-ac9e-fdf0fede7e19",
                                        "boundaryNum": 1,
                                        "name": "Handa Markit",
                                        "localname": "Handa Markit",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC79",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "0fc4de79-4a57-43de-9b50-31afc181e534",
                                        "boundaryNum": 1,
                                        "name": "Improvement Trust Shahid Bhagat Singh Nagar Scheme No 3",
                                        "localname": "Improvement Trust Shahid Bhagat Singh Nagar Scheme No 3",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC82",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "ea192af6-4db5-4507-9687-f72b1cb11770",
                                        "boundaryNum": 1,
                                        "name": "Jalandhria Colony",
                                        "localname": "Jalandhria Colony",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC87",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "4dbcf906-51d9-4301-beff-814a090ca4ca",
                                        "boundaryNum": 1,
                                        "name": "Jalotian Mohalla",
                                        "localname": "Jalotian Mohalla",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC88",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "b60ee23c-6554-4968-a04d-9f5c65ffaa7e",
                                        "boundaryNum": 1,
                                        "name": "Jhatkaian Chowk",
                                        "localname": "Jhatkaian Chowk",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC90",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "a65bf2b2-7ef0-4e2d-9a1f-c10f34df832c",
                                        "boundaryNum": 1,
                                        "name": "Joshian Mohalla",
                                        "localname": "Joshian Mohalla",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC91",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "e70b1677-dd2e-4940-b0c4-7dfd1e3912a2",
                                        "boundaryNum": 1,
                                        "name": "Mohalla Thathiara",
                                        "localname": "Mohalla Thathiara",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC122",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "ddc39de9-80a0-4531-b500-c2914a4e5ed0",
                                        "boundaryNum": 1,
                                        "name": "New Hargobind Nagar",
                                        "localname": "New Hargobind Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC133",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "b92756e4-35b3-41bc-b1d1-cc33cad3e69e",
                                        "boundaryNum": 1,
                                        "name": "Old Post Office",
                                        "localname": "Old Post Office",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC143",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "c7cd4241-f5eb-47c0-abfd-56df5fe522b8",
                                        "boundaryNum": 1,
                                        "name": "Paper Chowk To Old Civil Hospital Both Side",
                                        "localname": "Paper Chowk To Old Civil Hospital Both Side",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC146",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "0382d9f7-1450-4a84-b6b4-6349806c8125",
                                        "boundaryNum": 1,
                                        "name": "Purani Dana Mandi",
                                        "localname": "Purani Dana Mandi",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC159",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "ecbdec29-34e8-4fe2-a231-29f842edebe8",
                                        "boundaryNum": 1,
                                        "name": "Singla Markit",
                                        "localname": "Singla Markit",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC194",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "1953cdb3-f939-4098-9a47-84c427e2a241",
                                "boundaryNum": 1,
                                "name": "WARD_20",
                                "localname": "WARD_20",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD20",
                                "children": [
                                    {
                                        "id": "c501d6e9-f283-4a14-a69a-fe6f4984733b",
                                        "boundaryNum": 1,
                                        "name": "Friend Colony (Railway Line)",
                                        "localname": "Friend Colony (Railway Line)",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC50",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "c0afb00f-9c82-4b42-a5d1-b8170c431e4a",
                                        "boundaryNum": 1,
                                        "name": "Prem Pura",
                                        "localname": "Prem Pura",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC155",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "8cdff150-c215-4882-aeaa-070a5f65bfac",
                                "boundaryNum": 1,
                                "name": "WARD_21",
                                "localname": "WARD_21",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD21",
                                "children": [
                                    {
                                        "id": "b3a51bb7-3d0a-4e0a-bc31-e06a1e73b8df",
                                        "boundaryNum": 1,
                                        "name": "Central Town",
                                        "localname": "Central Town",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC30",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "c553d400-0381-46e3-a725-5bc9c942301b",
                                        "boundaryNum": 1,
                                        "name": "Indira Nagar",
                                        "localname": "Indira Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC83",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "b23e4c2b-5d16-47b5-a5d6-bce64f1a0ce1",
                                        "boundaryNum": 1,
                                        "name": "J.C.T Mill",
                                        "localname": "J.C.T Mill",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC85",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "e56dc42f-8796-4d89-b2d8-2cb52d8dbfa7",
                                "boundaryNum": 1,
                                "name": "WARD_22",
                                "localname": "WARD_22",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD22",
                                "children": [
                                    {
                                        "id": "042e03d2-52ac-4917-a47e-589176ddc035",
                                        "boundaryNum": 1,
                                        "name": "New Model Town",
                                        "localname": "New Model Town",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC134",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "8562f68e-8294-4b04-950c-f8cdfad34ffb",
                                "boundaryNum": 1,
                                "name": "WARD_23",
                                "localname": "WARD_23",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD23",
                                "children": [
                                    {
                                        "id": "4e083cea-096d-465e-8fbe-f97fe58db11c",
                                        "boundaryNum": 1,
                                        "name": "Green Model Town Colony",
                                        "localname": "Green Model Town Colony",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC64",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "3f436742-61fd-4b94-8873-39dc8a766fd2",
                                        "boundaryNum": 1,
                                        "name": "Pipa Rangi",
                                        "localname": "Pipa Rangi",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC151",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "732bb0bc-3b0e-4615-870c-70231fbe6676",
                                        "boundaryNum": 1,
                                        "name": "ROYAL COLONY",
                                        "localname": "ROYAL COLONY",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC170",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "e3079a39-990d-4a4a-9f38-18f71691264c",
                                        "boundaryNum": 1,
                                        "name": "Sham Nagar",
                                        "localname": "Sham Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC188",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "d2809606-04a2-4d7f-8541-8c60e3f7c127",
                                        "boundaryNum": 1,
                                        "name": "SWAMI PARAM NAGAR",
                                        "localname": "SWAMI PARAM NAGAR",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC202",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "1cfb0c84-baae-4d4b-80ae-b80eb501fe1b",
                                "boundaryNum": 1,
                                "name": "WARD_24",
                                "localname": "WARD_24",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD24",
                                "children": [
                                    {
                                        "id": "8d86bf8e-2f31-4325-826b-505ad7ee1e06",
                                        "boundaryNum": 1,
                                        "name": "Kaulsar Colony",
                                        "localname": "Kaulsar Colony",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC95",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "73758d70-4ca8-4191-a890-e18815eacedc",
                                        "boundaryNum": 1,
                                        "name": "Khothran Road",
                                        "localname": "Khothran Road",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC101",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "5a75191a-f725-4faf-ae29-f0dfd3ea1eec",
                                "boundaryNum": 1,
                                "name": "WARD_25",
                                "localname": "WARD_25",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD25",
                                "children": [
                                    {
                                        "id": "59ed0253-d93c-455f-8c1c-f0ad760f9775",
                                        "boundaryNum": 1,
                                        "name": "C.R.P Colony",
                                        "localname": "C.R.P Colony",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC29",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "06c419cd-6f12-4e27-9d39-d66d8a1a8a3e",
                                "boundaryNum": 1,
                                "name": "WARD_26",
                                "localname": "WARD_26",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD26",
                                "children": [
                                    {
                                        "id": "f342a16a-27b8-4eec-a49e-00187947d80d",
                                        "boundaryNum": 1,
                                        "name": "Kirpa Nagar",
                                        "localname": "Kirpa Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC102",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "41e88dea-4320-4d84-9fa7-a660eff14a80",
                                        "boundaryNum": 1,
                                        "name": "Urban Estate",
                                        "localname": "Urban Estate",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC210",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "459fd571-a587-443f-b20f-21a36e197036",
                                "boundaryNum": 1,
                                "name": "WARD_27",
                                "localname": "WARD_27",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD27",
                                "children": [
                                    {
                                        "id": "0d9551ec-d0d3-43e0-9ef2-363be02d0a60",
                                        "boundaryNum": 1,
                                        "name": "Shiv Puri",
                                        "localname": "Shiv Puri",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC191",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "a1c1ba1d-9731-4179-abb4-485bc9dcae82",
                                "boundaryNum": 1,
                                "name": "WARD_28",
                                "localname": "WARD_28",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD28",
                                "children": [
                                    {
                                        "id": "cf484d3c-1b14-4fab-8bae-d273a29ffd79",
                                        "boundaryNum": 1,
                                        "name": "Dhank Chachoki",
                                        "localname": "Dhank Chachoki",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC43",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "cc21b530-f18f-4106-8f5a-0f319ebe16df",
                                "boundaryNum": 1,
                                "name": "WARD_29",
                                "localname": "WARD_29",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD29",
                                "children": [
                                    {
                                        "id": "e04454ed-0a76-4c83-9811-4c4ac079ab88",
                                        "boundaryNum": 1,
                                        "name": "Ek Jot Colony",
                                        "localname": "Ek Jot Colony",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC49",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "d51b44cc-d79a-450f-b94c-126516e593ee",
                                        "boundaryNum": 1,
                                        "name": "G.I Appartment",
                                        "localname": "G.I Appartment",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC53",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "17b12936-f2d5-4ccf-bfba-e3c39513fbc9",
                                        "boundaryNum": 1,
                                        "name": "Greater Enclave Khothran Road",
                                        "localname": "Greater Enclave Khothran Road",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC60",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "77eabb8b-f716-4cb8-a2d0-37763131ab7b",
                                        "boundaryNum": 1,
                                        "name": "Greater Kailash Colony",
                                        "localname": "Greater Kailash Colony",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC61",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "38a73763-e128-40cd-8f9d-749aff47fb0e",
                                "boundaryNum": 1,
                                "name": "WARD_30",
                                "localname": "WARD_30",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD30",
                                "children": [
                                    {
                                        "id": "6f236225-ac4b-44d4-b312-f43194437f4e",
                                        "boundaryNum": 1,
                                        "name": "Phagwara To Khera Road Crossing",
                                        "localname": "Phagwara To Khera Road Crossing",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC150",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "0a2003ae-6804-4742-a0b4-180017bfb05a",
                                        "boundaryNum": 1,
                                        "name": "Regency Colony (JCT)",
                                        "localname": "Regency Colony (JCT)",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC169",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "eeab00f2-bf5f-4483-9b82-35ef92545c77",
                                        "boundaryNum": 1,
                                        "name": "Sugar Mill Colony",
                                        "localname": "Sugar Mill Colony",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC199",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "b3246b01-4b10-44c1-919c-cfe4ee0a0333",
                                "boundaryNum": 1,
                                "name": "WARD_31",
                                "localname": "WARD_31",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD31",
                                "children": [
                                    {
                                        "id": "424f1f0f-26eb-493b-b1ca-a9bc3136e371",
                                        "boundaryNum": 1,
                                        "name": "Chachoki",
                                        "localname": "Chachoki",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC31",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "1ab64f5f-531f-4b83-a340-e5d52d86d75e",
                                        "boundaryNum": 1,
                                        "name": "Dashmesh Enclave",
                                        "localname": "Dashmesh Enclave",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC39",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "f24fa462-25c2-4af3-8916-6d72817692ba",
                                        "boundaryNum": 1,
                                        "name": "Onkar Nagar",
                                        "localname": "Onkar Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC144",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "9bc6cdce-d5e2-46a4-95d8-2a481e3bfcce",
                                "boundaryNum": 1,
                                "name": "WARD_32",
                                "localname": "WARD_32",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD32",
                                "children": [
                                    {
                                        "id": "c12a7c1a-c5c5-41dd-83b7-9aec7ca27e96",
                                        "boundaryNum": 1,
                                        "name": "Mahinder Nagar",
                                        "localname": "Mahinder Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC107",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "a8d197a2-4f91-49cd-9ee8-840ec9ccd109",
                                        "boundaryNum": 1,
                                        "name": "NANGAL KHERA",
                                        "localname": "NANGAL KHERA",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC127",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "77ea2744-d194-452b-ba05-673335b6b2bb",
                                        "boundaryNum": 1,
                                        "name": "Sant Nagar",
                                        "localname": "Sant Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC179",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "d7da539a-751b-408b-bb88-ffefdc4a57ab",
                                "boundaryNum": 1,
                                "name": "WARD_33",
                                "localname": "WARD_33",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD33",
                                "children": [
                                    {
                                        "id": "d4560be7-1730-4428-87c0-b8ce4b2200bc",
                                        "boundaryNum": 1,
                                        "name": "Govt. Labour Colony",
                                        "localname": "Govt. Labour Colony",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC59",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "2f7cc4a8-8ee1-48ef-8d91-1371e1cf5051",
                                        "boundaryNum": 1,
                                        "name": "Industrial Area",
                                        "localname": "Industrial Area",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC84",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "f013d21c-6cad-4348-acab-16b3a80fb3d2",
                                "boundaryNum": 1,
                                "name": "WARD_34",
                                "localname": "WARD_34",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD34",
                                "children": [
                                    {
                                        "id": "f3103634-6939-418e-ae55-afaa1bfeed88",
                                        "boundaryNum": 1,
                                        "name": "Guru Teg Bhadhur Nagar Tibbi",
                                        "localname": "Guru Teg Bhadhur Nagar Tibbi",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC74",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "c6aaaf8b-3885-43ec-a5f9-2560e6982cbb",
                                "boundaryNum": 1,
                                "name": "WARD_35",
                                "localname": "WARD_35",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD35",
                                "children": [
                                    {
                                        "id": "bf9bcfed-b774-42db-8e79-d124148c2310",
                                        "boundaryNum": 1,
                                        "name": "Mohalla Kishanpura",
                                        "localname": "Mohalla Kishanpura",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC118",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "c963cf41-f784-462e-83d4-02898cfef457",
                                        "boundaryNum": 1,
                                        "name": "Mohalla Sadhu Ram",
                                        "localname": "Mohalla Sadhu Ram",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC120",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "0a4c59f3-58d7-4e73-9b1d-0dbf8863893c",
                                        "boundaryNum": 1,
                                        "name": "Ratan Pura",
                                        "localname": "Ratan Pura",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC167",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "5670fa7b-6085-4d5a-b2f8-084b56b0478a",
                                "boundaryNum": 1,
                                "name": "WARD_36",
                                "localname": "WARD_36",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD36",
                                "children": [
                                    {
                                        "id": "c41adb85-5656-4989-baee-1e29083e7212",
                                        "boundaryNum": 1,
                                        "name": "Guru Nanak Pura",
                                        "localname": "Guru Nanak Pura",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC72",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "f2858cc5-6394-4268-ba8c-4ff4196df355",
                                "boundaryNum": 1,
                                "name": "WARD_37",
                                "localname": "WARD_37",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD37",
                                "children": [
                                    {
                                        "id": "7678aa46-a830-438a-a7a6-924708effefa",
                                        "boundaryNum": 1,
                                        "name": "Dev Nagar",
                                        "localname": "Dev Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC42",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "04c2af78-e308-439b-b256-1d3a664e8601",
                                        "boundaryNum": 1,
                                        "name": "KHERA ROAD",
                                        "localname": "KHERA ROAD",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC100",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "087d4ace-7d1d-427b-8c59-1529676b7086",
                                        "boundaryNum": 1,
                                        "name": "Model Town",
                                        "localname": "Model Town",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC114",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "c40b563d-2a34-4a78-ae12-81fbdb9f2cf0",
                                        "boundaryNum": 1,
                                        "name": "Railway Road",
                                        "localname": "Railway Road",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC163",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "2058cb80-e830-46ca-b286-bb9ebca493fc",
                                        "boundaryNum": 1,
                                        "name": "Sandhu Nagar",
                                        "localname": "Sandhu Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC177",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "180c0479-4951-48b3-bdb2-c9022d7191d8",
                                "boundaryNum": 1,
                                "name": "WARD_38",
                                "localname": "WARD_38",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD38",
                                "children": [
                                    {
                                        "id": "b10e0620-114d-4fd0-8fcf-afe2531ebc27",
                                        "boundaryNum": 1,
                                        "name": "Nehru Nagar",
                                        "localname": "Nehru Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC130",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "3b15a223-eb99-4f18-93e3-551f55d85d55",
                                        "boundaryNum": 1,
                                        "name": "Prem Nagar",
                                        "localname": "Prem Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC154",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "3eb55dfd-0cd4-4c85-87f9-3036c54c5c8b",
                                "boundaryNum": 1,
                                "name": "WARD_39",
                                "localname": "WARD_39",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD39",
                                "children": [
                                    {
                                        "id": "5f451b6e-7f73-4ac2-a201-c3dd37e7b11f",
                                        "boundaryNum": 1,
                                        "name": "Bhagat Pura",
                                        "localname": "Bhagat Pura",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC24",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "b48d07fd-a063-4bde-8dac-91e772bdbef8",
                                        "boundaryNum": 1,
                                        "name": "Satnam Pura",
                                        "localname": "Satnam Pura",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC184",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "976abf52-f6db-4264-80df-5cd592e1f547",
                                "boundaryNum": 1,
                                "name": "WARD_40",
                                "localname": "WARD_40",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD40",
                                "children": [
                                    {
                                        "id": "1855687d-283d-4bee-95ff-789ac2251251",
                                        "boundaryNum": 1,
                                        "name": "Basant Nagar",
                                        "localname": "Basant Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC22",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "ee9671a2-8e37-4567-8080-1704fd69fff8",
                                        "boundaryNum": 1,
                                        "name": "Preet Nagar",
                                        "localname": "Preet Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC153",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "a7ef0e80-4163-412a-a64b-c516f4859beb",
                                        "boundaryNum": 1,
                                        "name": "Rampura",
                                        "localname": "Rampura",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC165",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "65301710-b3b5-49f6-8d7a-6486f7b6d4e5",
                                "boundaryNum": 1,
                                "name": "WARD_41",
                                "localname": "WARD_41",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD41",
                                "children": []
                            },
                            {
                                "id": "c92bb27c-503b-4aa8-aacb-ada05a67c4bd",
                                "boundaryNum": 1,
                                "name": "WARD_42",
                                "localname": "WARD_42",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD42",
                                "children": [
                                    {
                                        "id": "c51a79c9-1e80-44de-8c34-077dc9ad78f2",
                                        "boundaryNum": 1,
                                        "name": "Gobind Pura",
                                        "localname": "Gobind Pura",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC58",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "4d8c63ac-db60-49f9-a7c1-b09f47d9c1c2",
                                "boundaryNum": 1,
                                "name": "WARD_43",
                                "localname": "WARD_43",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD43",
                                "children": [
                                    {
                                        "id": "532cba6a-db8e-4e3d-aa94-8b5d9de6a067",
                                        "boundaryNum": 1,
                                        "name": "Colony Dhian Singh",
                                        "localname": "Colony Dhian Singh",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC37",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "d3e1b430-bd8a-42bd-b6b6-9aa3b970d4ee",
                                        "boundaryNum": 1,
                                        "name": "Gaushala Road",
                                        "localname": "Gaushala Road",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC57",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "7f13a4b8-89d5-43b5-a407-6585eb446131",
                                        "boundaryNum": 1,
                                        "name": "Kot Rani",
                                        "localname": "Kot Rani",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC105",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "7e4d5364-5952-4436-b7ef-38856f5db545",
                                        "boundaryNum": 1,
                                        "name": "New Adarsh Nagar",
                                        "localname": "New Adarsh Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC131",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "42252013-3af5-41a8-9039-caf88fc1d1f9",
                                        "boundaryNum": 1,
                                        "name": "Shahid Udham Singh Nagar",
                                        "localname": "Shahid Udham Singh Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC187",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "da9344c7-99a7-495f-bead-c86c4bf43fdd",
                                "boundaryNum": 1,
                                "name": "WARD_44",
                                "localname": "WARD_44",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD44",
                                "children": [
                                    {
                                        "id": "ded3e68c-2f53-4af5-85c4-8596c50c0f7b",
                                        "boundaryNum": 1,
                                        "name": "Dhian Singh Colony",
                                        "localname": "Dhian Singh Colony",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC45",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "59b57fe0-c114-46de-bf73-ccd09ee4ab29",
                                        "boundaryNum": 1,
                                        "name": "Dhillon Nagar",
                                        "localname": "Dhillon Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC46",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "3a7bf83a-22a4-4142-be70-f0616647172d",
                                        "boundaryNum": 1,
                                        "name": "Nakodar Road To Chungi",
                                        "localname": "Nakodar Road To Chungi",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC126",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "00f82e0d-a529-499c-8031-82359b094b6a",
                                "boundaryNum": 1,
                                "name": "WARD_45",
                                "localname": "WARD_45",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD45",
                                "children": [
                                    {
                                        "id": "62e67128-53e6-4090-a1ea-a9f27d374617",
                                        "boundaryNum": 1,
                                        "name": "Green Land Colony",
                                        "localname": "Green Land Colony",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC63",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "ffd60164-b2a7-4ed6-b37a-d18a0377c358",
                                        "boundaryNum": 1,
                                        "name": "Mohalla Agnihotri",
                                        "localname": "Mohalla Agnihotri",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC115",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "aba2f091-de77-4680-b07b-e67c50f87c81",
                                        "boundaryNum": 1,
                                        "name": "Parbhakar Mohalla",
                                        "localname": "Parbhakar Mohalla",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC147",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "c62ea024-e282-48eb-b98d-8dcf3b95af11",
                                        "boundaryNum": 1,
                                        "name": "Sudhiran Mohalla",
                                        "localname": "Sudhiran Mohalla",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC197",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "a539dbd3-01c0-47f1-b08f-bd22b11b2af2",
                                "boundaryNum": 1,
                                "name": "WARD_46",
                                "localname": "WARD_46",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD46",
                                "children": [
                                    {
                                        "id": "69690d38-f907-411f-8dca-fcde12701936",
                                        "boundaryNum": 1,
                                        "name": "AggFaka",
                                        "localname": "AggFaka",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC3",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "88aa8167-47c4-4c7d-9c02-71d186e672b2",
                                        "boundaryNum": 1,
                                        "name": "Bakhshish Enclave",
                                        "localname": "Bakhshish Enclave",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC18",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "b30fc84f-599d-48aa-a401-82ea949ff652",
                                        "boundaryNum": 1,
                                        "name": "DR AMBEDKAR CHOWK",
                                        "localname": "DR AMBEDKAR CHOWK",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC47",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "e126fb7e-cdb2-4511-a37a-3a2195636ca3",
                                        "boundaryNum": 1,
                                        "name": "Hadiabad",
                                        "localname": "Hadiabad",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC75",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "2f95b5bf-3d3e-4b59-8f20-1a09e358210a",
                                        "boundaryNum": 1,
                                        "name": "HakuPura",
                                        "localname": "HakuPura",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC77",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "40520a54-5396-4bfa-b894-136d953f483d",
                                        "boundaryNum": 1,
                                        "name": "MANAWALI",
                                        "localname": "MANAWALI",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC111",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "bed68814-9c17-4115-8a03-84ff854cbbe6",
                                        "boundaryNum": 1,
                                        "name": "Mohalla Jagat Pura",
                                        "localname": "Mohalla Jagat Pura",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC116",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "89337e45-9077-42ad-91dd-ad0aff67ba5f",
                                        "boundaryNum": 1,
                                        "name": "Naurang Shahpur",
                                        "localname": "Naurang Shahpur",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC128",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "10ba4988-c69b-407b-94c4-567af667e781",
                                        "boundaryNum": 1,
                                        "name": "Qilla Mohalla",
                                        "localname": "Qilla Mohalla",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC162",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "1c762b3a-a45c-49c5-9449-7c58ef5f037e",
                                        "boundaryNum": 1,
                                        "name": "Sherwood Colony",
                                        "localname": "Sherwood Colony",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC190",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "0d04f8d3-719a-458b-9be3-fa208022baa5",
                                        "boundaryNum": 1,
                                        "name": "Taj Colony",
                                        "localname": "Taj Colony",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC204",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "30fc4146-64a2-4145-b41b-44d50b5b1b2c",
                                "boundaryNum": 1,
                                "name": "WARD_47",
                                "localname": "WARD_47",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD47",
                                "children": [
                                    {
                                        "id": "fe923b14-1895-4462-921d-006e1b830756",
                                        "boundaryNum": 1,
                                        "name": "Manav Nagar",
                                        "localname": "Manav Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC110",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "677bba9e-518d-40a5-8def-5b9b4be28596",
                                        "boundaryNum": 1,
                                        "name": "UPPAS MOHALA",
                                        "localname": "UPPAS MOHALA",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC209",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "a2289ba6-d37f-4e10-a4b3-0fb2a98e17a3",
                                "boundaryNum": 1,
                                "name": "WARD_48",
                                "localname": "WARD_48",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD48",
                                "children": [
                                    {
                                        "id": "1301f9a3-422b-470a-b7e7-405ecf88626f",
                                        "boundaryNum": 1,
                                        "name": "Basant Bagh",
                                        "localname": "Basant Bagh",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC21",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "763818ed-fa65-40e3-9ca1-5c37df6f1cb4",
                                        "boundaryNum": 1,
                                        "name": "Mansa Devi Nagar",
                                        "localname": "Mansa Devi Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC112",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "383f247a-c660-4ae6-98e5-16b866f2234e",
                                "boundaryNum": 1,
                                "name": "WARD_49",
                                "localname": "WARD_49",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD49",
                                "children": [
                                    {
                                        "id": "a8e57d20-9e4f-4115-8d4b-9f0928e64c84",
                                        "boundaryNum": 1,
                                        "name": "Kartar Estate",
                                        "localname": "Kartar Estate",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC93",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "274786ad-38ba-4fcd-9f77-595ff63b33fd",
                                        "boundaryNum": 1,
                                        "name": "Santokh Pura Mohalla",
                                        "localname": "Santokh Pura Mohalla",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC180",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "5c7519fd-d645-4a7f-8c14-9e67d2b67c07",
                                        "boundaryNum": 1,
                                        "name": "Teacher Colony",
                                        "localname": "Teacher Colony",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC207",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            },
                            {
                                "id": "46bb4f97-91a7-4135-a866-72cc1fc96ad1",
                                "boundaryNum": 1,
                                "name": "WARD_50",
                                "localname": "WARD_50",
                                "longitude": null,
                                "latitude": null,
                                "label": "Block",
                                "code": "WARD50",
                                "children": [
                                    {
                                        "id": "a19a68c9-cc8e-4ac1-a33a-42c8c3ad7765",
                                        "boundaryNum": 1,
                                        "name": "Adarsh Nagar",
                                        "localname": "Adarsh Nagar",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC2",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "df5ef036-f16e-4eea-9da7-f0fe1c85256c",
                                        "boundaryNum": 1,
                                        "name": "Bhanoki Road",
                                        "localname": "Bhanoki Road",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC27",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "19ed8f43-d190-4830-b333-010b6876a9b7",
                                        "boundaryNum": 1,
                                        "name": "Dashmesh Puri",
                                        "localname": "Dashmesh Puri",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC41",
                                        "area": "",
                                        "children": []
                                    },
                                    {
                                        "id": "b90543d6-637c-4012-a01d-1f80f0d562e5",
                                        "boundaryNum": 1,
                                        "name": "New Satnampura",
                                        "localname": "New Satnampura",
                                        "longitude": null,
                                        "latitude": null,
                                        "label": "Locality",
                                        "code": "PLC136",
                                        "area": "",
                                        "children": []
                                    }
                                ]
                            }
                        ]
                    }
                ]
            }
        }
    ]
}



'
```
{% endcode %}

