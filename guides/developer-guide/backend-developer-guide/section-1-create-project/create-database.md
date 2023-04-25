# Create Database

**Overview:** Once PostgreSQL (v10) has been installed and the basic setup is done, we use Flyway to create the tables.&#x20;

**Steps:** The following properties should be configured in application.properties file to enable flyway migration:

```properties
spring.flyway.url=jdbc:postgresql://localhost:5432/birthregn
spring.flyway.user=birth
spring.flyway.password=birth #REPLACE
spring.flyway.table=public
spring.flyway.baseline-on-migrate=true
spring.flyway.outOfOrder=true
spring.flyway.locations=classpath:/db/migration/main
spring.flyway.enabled=true
```

Add the Flyway SQL scripts in the following structure under `resources/db/migration/main`:

![](<../../../../.gitbook/assets/image (53).png>)

Add the migration files to the _main_ folder. Specific nomenclature should be followed while naming the file. The file name should be in the following format:

```
V[YEAR][MONTH][DAY][HR][MIN][SEC]__modulecode_ …_ddl.sql

```

Example: **V20180920110535\_\_tl\_tradelicense\_ddl.sql**

For this sample service, we will be using the following SQL script to create the required tables.

```plsql
CREATE TABLE eg_bt_registration(
  id character varying(64),
  tenantId character varying(64),
  applicationNumber character varying(64),
  babyFirstName character varying(64),
  babyLastName character varying(64),
  fatherId character varying(64),
  motherId character varying(64),
  doctorName character varying(64),
  hospitalName character varying(64),
  placeOfBirth character varying(64),
  timeOfBirth bigint,
  createdBy character varying(64),
  lastModifiedBy character varying(64),
  createdTime bigint,
  lastModifiedTime bigint,
 CONSTRAINT uk_eg_bt_registration UNIQUE (id)
);
CREATE TABLE eg_bt_address(
   id character varying(64),
   tenantId character varying(64),
   doorNo character varying(64),
   latitude FLOAT,
   longitude FLOAT,
   buildingName character varying(64),
   addressId character varying(64),
   addressNumber character varying(64),
   type character varying(64),
   addressLine1 character varying(256),
   addressLine2 character varying(256),
   landmark character varying(64),
   street character varying(64),
   city character varying(64),
   locality character varying(64),
   pincode character varying(64),
   detail character varying(64),
   registrationId character varying(64),
   createdBy character varying(64),
   lastModifiedBy character varying(64),
   createdTime bigint,
   lastModifiedTime bigint,
   CONSTRAINT uk_eg_bt_address PRIMARY KEY (id),
   CONSTRAINT fk_eg_bt_address FOREIGN KEY (registrationId) REFERENCES eg_bt_registration (id)
     ON UPDATE CASCADE
     ON DELETE CASCADE
);
```

