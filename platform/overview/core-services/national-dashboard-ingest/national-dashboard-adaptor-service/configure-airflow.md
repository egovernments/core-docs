# Configure Airflow

## Configure Airflow Variables <a href="#configure-the-airflow-variables" id="configure-the-airflow-variables"></a>

<figure><img src="../../../../../.gitbook/assets/image-20220818-102218.png" alt=""><figcaption></figcaption></figure>

| Key             | Value                                                                                                                                                                                                    | Remark                          |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------- |
| password        | eGov@123                                                                                                                                                                                                 |                                 |
| username        | SYSTEMSU1                                                                                                                                                                                                | for Upyog                       |
| username\_state | SYSTEMSU3                                                                                                                                                                                                | for staging                     |
| token           | ZWdvdi11c2VyLWNsaWVudDo=                                                                                                                                                                                 |                                 |
| tenantid        | pg                                                                                                                                                                                                       |                                 |
| usertype        | SYSYTEM                                                                                                                                                                                                  |                                 |
| totalulb\_url   | [https://raw.githubusercontent.com/egovernments/punjab-mdms-data/master/data/pb/tenant/tenants.json](https://raw.githubusercontent.com/egovernments/punjab-mdms-data/master/data/pb/tenant/tenants.json) | for reading the ulb’s of punjab |

## Configure Connections <a href="#configure-the-connections" id="configure-the-connections"></a>

<figure><img src="../../../../../.gitbook/assets/image-20220818-102252.png" alt=""><figcaption></figcaption></figure>

| ConnectionId      | Connection Type     | Host                                                                               |      |                      |                                                      |
| ----------------- | ------------------- | ---------------------------------------------------------------------------------- | ---- | -------------------- | ---------------------------------------------------- |
| es\_conn          | ElasticSearch       | elasticsearch-data-v1.es-cluster                                                   | 9200 |                      | For the ES server                                    |
| digit -auth-state | <p>HTTP</p><p> </p> | [http://staging.digit.org](http://staging.digit.org/)                              |      | <p>https</p><p> </p> | <p>For the auth api conenction - Staging</p><p> </p> |
| digit-auth        |                     | [![](https://upyog.niua.org/citizen/browser-icon.png)NUGP](http://upyog.niua.org/) |      |                      | For the auth api conenction - UPYOG                  |
