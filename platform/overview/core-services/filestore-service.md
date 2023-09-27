# FileStore Service

### Overview <a href="#overview" id="overview"></a>

An eGov core application which handles uploading different kinds of files to server including images and different document types.

### Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

1. Prior Knowledge of Java/J2EE.
2. Prior Knowledge of Spring Boot.
3. Prior Knowledge of REST APIs and related concepts like path parameters, headers, JSON etc.
4. Prior knowledge of aws and azure

### Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

The filestore application takes in a request object which contains an image/document or any kind of file and stores them in a disk/AWS/azure depending upon the configurations, additional implementations can be written for the app interface to interact with any other remote storages.

The request file to be uploaded is taken in form of multipart file part then saved to the storage and a uuid will returned as a unique identifier for that resource, which can be used to fetch the documents later.

Incase of images, the application will create three more additional copies of the file in the likes of large, medium and small for the usage of thumbnails or low quality images incase of mobile applications.

The search api takes the uuid, tenantid as mandatory url params and a few optional parameters and returns the presigned url of the files from the server, In case of images a single string containing multiple urls separated by commas will be returned representing different sizes of images stored.

### Setup And Configuration <a href="#setup-and-configuration" id="setup-and-configuration"></a>

The **Application** is present among the core group of applications available in the eGov-services git repository.  The spring boot application but needs **lombok** extension added in your ide to load it. Once the application is up and running API requests can be posted to the url and ids can be generated.&#x20;

&#x20;

\*\*in case of intellij the plugin can be installed directly, for eclipse the lombok jar location has to be added in eclipse.ini file in this format **-javaagent:lombok.jar**.

\
For the API information please refer the swagger yaml&#x20;

\
GOTO : [![](https://editor.swagger.io/dist/favicon-16x16.png)Swagger Editor](https://editor.swagger.io/)   and click on file -> import url&#x20;

\
Then add the raw url of the API doc in the pop up.&#x20;

[https://raw.githubusercontent.com/egovernments/DIGIT-OSS/master/core-services/docs/filestore-service-contract.yml](https://raw.githubusercontent.com/egovernments/DIGIT-OSS/master/core-services/docs/filestore-service-contract.yml)

\
Incase the url is unavailable, please go to the [docs folder](https://github.com/egovernments/DIGIT-OSS/tree/master/core-services/docs) of egov-services git repo and find the yaml for egov-filestroe.

The application needs at least one type of storage available for it to store the files either file-storage, AWS S3 or azure. More storage types can be added by extending the application interface also.

\
To work work any of the file storages there are some application properties which needs to be configured.

\
**DiskStorage:**

The mount path of the disk should be provided in the following variable to save files in the disc. **file.storage.mount.path=path.**

Following are the variables that needs to be populated based on the aws/azure account you are integrating with.

**How to enable Minio SDC:**

minio.url=[http://minio](http://minio/).backbone:9000(Minio server end point)

isS3Enabled=true(Should be true)

aws.secretkey={minio\_secretkey}

aws.key={minio\_accesskey}

fixed.bucketname=egov-rainmaker(Minio bucket name)

minio.source=minio

\
\


**How to enable AWS S3:**

minio.url=[https://s3.amazonaws.com](https://s3.amazonaws.com/)

isS3Enabled=true(Should be true)

aws.secretkey={s3\_secretkey}

aws.key={s3\_accesskey}

fixed.bucketname=egov-rainmaker(S3 bucket name)

minio.source=minio

**AZURE:**

**isAzureStorageEnabled** - informing the application whether Azure is available or not

**azure.defaultEndpointsProtocol -** type of protocol **https**

**azure.accountName -** name of the user account&#x20;

**azure.accountKey -** secret key of the user account

**NFS :**

**isnfsstorageenabled**-informing the application whether NFS is available or not \<True/False>

**file.storage.mount.path** - \<NFS location, example /filestore>

**source.disk -** diskStorage - name of storage

**disk.storage.host.url**=\<Main Domain URL>

**Allowed formats to be uploaded**\
The default format of the files is the use of set brackets with strings inside it - {"jpg", "png"}. Make sure to follow the same.

{% hint style="info" %}
_**allowed.formats.map:**_ {jpg:{'image/jpg','image/jpeg'},jpeg:{'image/jpeg','image/jpg'},png:{'image/png'},pdf:{'application/pdf'},odt:{'application/vnd.oasis.opendocument.text'},ods:{'application/vnd.oasis.opendocument.spreadsheet'},docx:{'application/x-tika-msoffice','application/x-tika-ooxml','application/vnd.oasis.opendocument.text'},doc:{'application/x-tika-msoffice','application/x-tika-ooxml','application/vnd.oasis.opendocument.text'},dxf:{'text/plain'},csv:{'text/plain'},txt:{'text/plain'},xlsx:{'application/x-tika-ooxml','application/x-tika-msoffice'},xls:{'application/x-tika-ooxml','application/x-tika-msoffice'\}}
{% endhint %}

The key in the map is the visible extension of the file types, the values on the right in curly braces are the respective tika types of the file. these values can be found in tika website or by passing the file through tika functions.

## Features <a href="#available-features" id="available-features"></a>

1. **Upload**\
   POST API to save the files in the server
2. **Search Files**\
   GET API to retrieve files based only on id and tenantid
3. **Search URLs** \
   GET API  to retrieve pre-signed URLs for a given array of ids

## Deployment Details <a href="#deployment-details" id="deployment-details"></a>

1. Deploy the latest version of Filestore Service.
2. Add role-action mapping for APIs.

## Integration Details <a href="#integration" id="integration"></a>

### Integration Scope <a href="#integration-scope" id="integration-scope"></a>

The filestore service is used to upload and store documents which citizens add while availing of services from ULBs.

### Integration Benefits <a href="#integration-benefits" id="integration-benefits"></a>

Can perform file upload independently without having to add fileupload specific logic in each module.

### Integration Steps <a href="#steps-to-integration" id="steps-to-integration"></a>

1. To integrate, the host of the filestore module should be overwritten in the helm chart.
2. `/filestore/v1/files` should be added as the endpoint for uploading files in the system
3. `/filestore/v1/files/url` should be added as the search endpoint. This method handles all requests to search existing files depending on different search criteria

### Postman Collection <a href="#postman-collection" id="postman-collection"></a>

[https://www.getpostman.com/collections/1b448834735adf1acc4a](https://www.getpostman.com/collections/1b448834735adf1acc4a)
