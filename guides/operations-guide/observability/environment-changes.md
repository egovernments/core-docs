---
description: Steps to configure changes in the environment for deploying the tools
---

# Environment Changes

### Step-1: Update domain name

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXcAcgnpd1sONV8VMwmpbeLxvQNfXg8tPrcJbxmtCoWr57DJJgffGIu45gJIi9ypM3RAupajPF9Ms67227P1NHCkQ8gzYHi-x-zBb004TY3H_LXzSFNzuYWNMJz5EXqfsVNIYa42?key=iKnMqxt7hBWD34AV_hYyp26I" alt=""><figcaption></figcaption></figure>

### Step-2: Modify the role attribute path for Grafana access

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXe3RsXqzOY38gxGBz0DiL14Jdn9MXUdSctrLvFHItzLELVnSe3r3YE6T5oWdCzLHjknZ8fsY_2LAbdGiQ11rd5d6RXJn1hbo8-GQnRHu9ZDVERvOTYnnxx5g2w408BBhpKwrI_utg?key=iKnMqxt7hBWD34AV_hYyp26I" alt=""><figcaption></figcaption></figure>

### Step-3: Modify the retention, storage size ,cluster name and targets based on the specific requirements

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXeGKZEbbkc4lNd2mjRZjxvdfZ7uBR7gdCSirdUss8XrA9DvOAd092Vxzn7F2KkBT43fPbZExX1JXq4Oy60WHP_UmRzutRlZLiwSl0-SR7nPFJunvACfFMAtNqBmp6d58pR9J2Y54A?key=iKnMqxt7hBWD34AV_hYyp26I" alt=""><figcaption></figcaption></figure>

### Step-4: Adjust the volume size and update the retention period accordingly

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXfVfHPuId9mevuaTAdR7xUxTBkcoXCkvFpQCBYWbbJXGro8zihtlC4K1KTpzHSxOicRil7PtaZ8tw3J70EVmPdFS0Uu-ICvkNxquTFCgYX5ICjkNpq5N6Vr--gnPAemXwVTJ1tz_w?key=iKnMqxt7hBWD34AV_hYyp26I" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXdfB3bfygy5QRrB6UZuWOHqjGDbTg3BUeNekOMwLygi3_YI1lvcP6BJEVgYvEQvGD-Y4UP9uQs8xFGS3j7JWjux3FuMZrwQMEtGuruZDxnqKlhACn_CNs5heh4aoZe9QE0ahn3T?key=iKnMqxt7hBWD34AV_hYyp26I" alt=""><figcaption></figcaption></figure>

Optional:

S3&#x20;

### Step-5: Make the required changes in the env-secrets file

Changes to the Alertmanager configuration in the env-secrets.yaml file.

<figure><img src="../../../.gitbook/assets/image (333).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (334).png" alt=""><figcaption></figcaption></figure>

### Step-6: Oauth app configuration

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXfGORgumhubJBpKtQoLfvF6LJAzVkqk9CIN5HsaqWQDI6BuB7X89BaTocfiV3ECBueUtgdx6npicIqqZEPMF1KrikC5ravMwzu64APq26dyhWPBe7tkR8B5iuYvCDVam757X33IZg?key=iKnMqxt7hBWD34AV_hYyp26I" alt=""><figcaption></figcaption></figure>

### Step-7: Authentication configuration for Grafana in env-secrets.yaml

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXeDTien3e_yZlgNhTBJO7AYH8nc7cbIaazBpqbnGBuqAASn9v7FMs87cjCKH_UuPq1-VpWPubiApping0fFxx_9N2odQALWY7Enswj5FLG3su4wxemL_AmntSazIK_NWg1A8NMD?key=iKnMqxt7hBWD34AV_hYyp26I" alt=""><figcaption></figcaption></figure>

### Sample Env-Secrets File

```
cluster-configs:
   secrets:
       db:
           username: postgres
           password: test123
           flywayUsername: postgres
           flywayPassword: test123
       egov-filestore:
           awskey: jdfbjdfjvnbvdk
           awssecretkey: bxjcsvbvncajsb
       user:
           username: admin
           password: demo
       egov-enc-service:
           master_password: demo
           master_salt: q7.fr.cr
           master_initialvector: 9J&asfgrU-H2
       egov-notification-sms:
           username: demo
           password: demo
       egov-pg-service:
           axis_merchant_accesscode: demo
           axis_merchant_id: demo
           axis_merchant_pwd: demo
           axis_merchant_secretkey: demo
           axis_merchant_user: demo
           payu_merchant_key: demo
           payu_merchant_salt: demo
       egov-notification-mail:
           mailsenderusername: demo@demo
           mailsenderpassword: demo
       egov-location:
           gmapskey: jbsdbvxvcmbsmnx
       kafka:
           clusterID: HshRPdVrcvxWoB4kuTdEbawtq
       elasticsearch:
           password: <Password>
       oauth2:
           clientSecret: <Client Sec ID>    
           clientID: <Client ID>
       grafana:
           clientID: <OAuth-key>    ##change ID
           clientSecret: <OAuth-token> #change secrets key
       git-sync:
           ssh: |-
               -----BEGIN RSA PRIVATE KEY-----
               MIIEpAIBAAKCAQEAxMn4y2irJKb/dAQr4FZtiBbX+VfgeNWDO6Ure90CA+f5QcjL
               i0SHAbpvZ+PAPwZcYZMiOE7hdRh1xSiY7u1GQPcm1ZIboKSYahafq41XFzYGG3hk
               6GHC0RPPGhW4TQ8PWbUiReSndn2VE/VY+3DItS6kSwKazqfBWVqXZ9fkAQ0yUFT1
               M1rsdIZoeei9NH48UyDD4U2x/BEHMneElQbibwDuBrN/6DSzlIcgOMhePf272Nsf
               GOL/SA2YJx6k7gDHjEDZ/pz6MT9XjVcDjP9y8f2udObrzIopv3C0jRZp+rKM6PFU
               sLCtJSRoohmmYlexixhMFS/kAPP6Q8VyHeUcWwIDAQABAoIBAQCBZiW460yOP1l+
               mjeXvn0rnYnKpaQvEIbIs6VSP1NR6jmWrkhZfWghFMyozbPePXqFltBLomLSMpFO
               YZGemls14M6iZP7RtSmbqOC5V6lK0/VUHuiLfa0y+gmWp22XDi4T2O1+dApB+fYL
               N6uZOuJfcRoLUN0mwlx7OvyQBgAhR7r0eePcV+yvk35qSVlKw9KreAytvE9fmLcZ
               pH4jKSOFibAsDYYz9oVnwo5+aVvYl3oU2TyLwQFKmkZyKJsMOWtGw4+MVRO5/xre
               WzuR8QNY/z7/A2MNQlO4KjEqkv4m/z6lh9WaDXO+PbCRRARbFcS4ZUJgXgPhtFz3
               wiyXxExxAoGBAOP/GKktpUVMqtE3sXlJ4xS2l7e9w1t9kyceElXZl2FSJkqJe9Bt
               PJ9FdjbB4wlxF985PkOByvOQwsGMcuMOF+BlHW/KcA2LR2vsoBY6zGTJB35YqD2V
               lpdI3az0RugrYTCi3pHq/GVAc9h+V9S4+SvsuIZfrfXV+OwkeFh6gmG9AoGBANz1
               nbgdQk5ZIJJvr5Y0Hn2fTKGyvHsiu/MNL5axaYxD1BUAdPdW9x7nsI42ayIzERGr
               lLkO4YF4kC52LZj/wo3UlYq8ERMyH6tLnD4j/aFy4bqYAco89H43DBDAq59DTcM6
               2tF+VzTNaANI4bvOTnjMTmLEJ4zRDUnb9vkAX3v3AoGAQtjVUyz16waagrMQjt4x
               /S23+ABkWdvMnEh92bvtXXRnk60Rpz+P6abFDTL1rRwCgslWzxYr+hO0dmkGejn0
               mC8tXUx+ZAo1C5iaK0pcCSTD1LCLy1qjh4GutPn+HC4z1b27Ag9ipxEppg0NFWqS
               a+WBCKze5VgyHpJm0pJAzgUCgYASs6tMyRUyonKSUmevM+wcv93xlbpERdVYphYQ
               ECYZ3CfYOzirMq4p7HxSHSMGOwJH15j37N2DYtv5QsFrQMKL1KFvo6liUYzCp9yq
               mcs+3gVjELieEHi1Mh2QUW51RXIQgyvALYxeCMCz/ng0uCqGKOy9iVK7pXoVdUu7
               GZ/7UwKBgQDcgSKcRk17AZ5w6cTGV+POpTnHCwq8cC37t8YBRLBqXgbQObVGViYp
               D+t2DZeZ22VQCXbyBE8NTMi/9c+Zo+uguAe8tzroxhAP9uzsHw6qTb7QHQHZ/CPK
               wBkBi92ZelIXkby0L8ljdQKEDbhPc8MBpinoIQgJurbZvdvS9zhjuljLssw==
               -----END RSA PRIVATE KEY-----
           known_hosts: github.com ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCj7ndNxQowgcQnjshcLrqPEiiphnt+VTTvDP6mHBL9j1aNUkY4Ue1gvwnGLVlOhGeYrnZaMgRK6+PKCUXaDbC7qtbW8gIkhL7aGCsOr/C56SJMy/BCZfxd1nWzAOxSDPgVsmerOBYfNqltV9/hWCqBywINIR+5dIg6JTJ72pcEpEjcYgXkE2YEFXV1JHnsKgbLWNlhScqb2UmyRkQyytRLtL+38TGxkxCflmO+5Z8CSSNY7GidjMIZ7Q4zMjA2n1nGrlTDsskzwDCsw+wqFPGQA179cnfGWOWRVruj16z6XyvxvjJwbz0wQZ75XK5tKSb7FNyeIEs4TT4jk+S4dhPeAUC5y+bDYirYgM4GC7uEnztnZyaVWQ7B381AK4Qdrwt51ZqExKbQpTUNn+EjqoTwvqNj4kqx5QUCI0ThS/YkOxJCXmPUWZbhjpCg56i+2aB6CmK2JGhn57K5mj0MNdBXA4/WnwH6XoPWJzK5Nyu2zB3nAZp+S5hpQs+p1vN1/wsjk=
       alertmanager:
           config:
               global:
                   slack_api_url: https://hooks.slack.com     ##change the slack api url
                   resolve_timeout: 5m
               route:
                   group_by:
                       - alertname
                   group_wait: 30s
                   receiver: slack-notification
                   group_interval: 5m
                   repeat_interval: 10m
                   routes:
                       - receiver: slack-notification
                         match_re:
                           severity: warning|critical
                         continue: true
                       - receiver: email-notification
                         match:
                           severity: critical
               receivers:
                   - name: slack-notification
                     slack_configs:
                       - channel: '<slack-channel>'     ##change the slack channel name 
                         send_resolved: true
                         username: Alertmanager
                         title: |
                           [{{ .Status | toUpper }}{{ if eq .Status "firing" }}:{{ .Alerts.Firing | len }}{{ end }}] {{ .CommonLabels.alertname }}
                         text: |-
                           {{ range .Alerts -}}
                           {{- "\n" -}}
                           *Alert:* {{ .Annotations.summary }}
                           {{ if .Labels.severity }}*Severity:* `{{ .Labels.severity }}`{{ end }}
                           *Cluster:* {{ .Labels.cluster }}
                           *Details:*
                           {{ .Annotations.description }}
                           {{ end }}
                         color: |-
                           {{ if eq .Status "firing" -}}
                             {{ if eq .CommonLabels.severity "warning" -}}
                               warning
                             {{- else if eq .CommonLabels.severity "critical" -}}
                               danger
                             {{- else -}}
                               #439FE0
                             {{- end -}}
                           {{ else -}}
                             good
                           {{- end }}
                   - name: email-notification
                     email_configs:
                       - to: <Email ID>    ##change the Email ID to get the alert in the Email
                         from: <Email ID>
                         smarthost: smtp.gmail.com:587
                         auth_username: <Email ID>           # Ex: unified.alerts@egovernments.org
                         auth_password: <Password>           # Ex: mujp cgjj fhdv wieu
                         send_resolved: true
                         headers:
                           subject: |
                               [{{ .Status | toUpper }}{{ if eq .Status "firing" }}:{{ .Alerts.Firing | len }}{{ end }}] {{ .CommonLabels.cluster }} - {{ .CommonLabels.alertname }}
                         html: |-
                           <html>
                           <head>
                           <title>Alert!</title>
                           </head>
                           <body>
                           {{ range .Alerts }}
                           <ul>
                           <li> <b>Alert Name:</b> {{ .Labels.alertname }} </li>
                           <li> <b>Severity:</b> {{ if eq .Labels.severity "critical" }}<b style="color:red;">CRITICAL</b>{{ else if eq .Labels.severity "warning" }}<b style="color:orange;">WARNING</b>{{ else }}<b>{{ .Labels.severity | toUpper }}</b>{{ end }} </li>
                           <li> <b>Summary:-</b> {{ .Annotations.summary }} </li>
                           <li> <b>Cluster:-</b> {{ .Labels.cluster }} </li>
                           <li> <b>Details:</b>
                             <p style="margin-left: 20px; white-space: pre-wrap;"> {{ .Annotations.description }} </p>
                           </li>
                           </ul><br>
                           {{ end }}
                           </body></html>
                       
```

## Create KMS Key & Configure SOPs&#x20;

Follow the below steps to create a KMS key and configure SOPs for encryption and decryption.

### 1. Create IAM User & Attach Policies

* Go to AWS Management Console.
* Go to IAM and click Policies on the left-hand side of the toolbar.&#x20;
* Click Create Policy and then press Next. Click on JSON add the below policy and click Next.

```
{

   "Version": "2012-10-17",

   "Statement": [

       {

           "Sid": "AllowCreateRole",

           "Effect": "Allow",

           "Action": "iam:CreateRole",

           "Resource": "arn:aws:iam::349271159511:role/*"

       }

   ]

}
```

* &#x20;Give the name to the policy and Create Policy.
* &#x20;Now click on Users in the console on the left side.
* &#x20;Click Add User, provide the name of the specific user and click Next.
* In permission options click Attach Policies directly. Select Administration Access, AWSKeyManagementServicePoweruser and also attach the policy which you have created in the previous steps and then click Next.
* Verify the name of the user and the 3 policies attached or not and then click Create User.

### 2. Create KMS Key

* Go to AWS Management Console.
* Go to KMS and Custom Managed Keys. Click Create Key.
* In Configure Key, use the default options and then click Next. Provide Name in alias and the give the administrator access to the IAM user created in the previous step. Select the users to give permissions to encrypt and decrypt using this key and then click Next.
* Attach the below policy in the key policy and then click finish. Make sure to provide the IAM user you created in the below-highlighted placeholder.

```
{

   "Version": "2012-10-17",

   "Id": "key-consolepolicy-3",

   "Statement": [

       {

           "Sid": "Enable IAM User Permissions",

           "Effect": "Allow",

           "Principal": {

               "AWS": "arn:aws:iam::349271159511:root"

           },

           "Action": "kms:*",

           "Resource": "*"

       },

       {

           "Sid": "Allow access for Key Administrators",

           "Effect": "Allow",

           "Principal": {

               "AWS": "arn:aws:iam::349271159511:role/aws-reserved/sso.amazonaws.com/ap-south-1/AWSReservedSSO_AdministratorAccess_3b9b4bb9eebf66ac"

           },

           "Action": [

               "kms:Create*",

               "kms:Describe*",

               "kms:Enable*",

               "kms:List*",

               "kms:Put*",

               "kms:Update*",

               "kms:Revoke*",

               "kms:Disable*",

               "kms:Get*",

               "kms:Delete*",

               "kms:TagResource",

               "kms:UntagResource",

               "kms:ScheduleKeyDeletion",

               "kms:CancelKeyDeletion"

           ],

           "Resource": "*"

       },

       {

           "Sid": "Allow use of the key",

           "Effect": "Allow",

           "Principal": {

               "AWS": "arn:aws:iam::349271159511:user/<IAM USER>"

           },

           "Action": [

               "kms:Decrypt",

               "kms:DescribeKey"

           ],

           "Resource": "arn:aws:kms:ap-south-1:349271159511:key/29adbf26-7b85-4469-8c9e-f8050fd19a8e"

       },

       {

           "Sid": "Allow attachment of persistent resources",

           "Effect": "Allow",

           "Principal": {

               "AWS": "arn:aws:iam::349271159511:role/aws-reserved/sso.amazonaws.com/ap-south-1/AWSReservedSSO_AdministratorAccess_3b9b4bb9eebf66ac"

           },

           "Action": [

               "kms:CreateGrant",

               "kms:ListGrants",

               "kms:RevokeGrant"

           ],

           "Resource": "*",

           "Condition": {

               "Bool": {

                   "kms:GrantIsForAWSResource": "true"

               }

           }

       }

   ]

}
```

* Copy the arn value after creating the KMS Key.

### 3. Placing the KMS arn value in the deployment manifest file

* Go to the below code and add the arn key in .sops.yaml file.

```
DIGIT-DevOps/blob/DIGIT-2.9LTS-monitoring/deploy-as-code/charts/.sops.yaml
```

* Next, cd to deploy-as-code and run the below command.

```
sops --encrypt --in-place charts/env-secrets.yaml
```

* Now to see the encrypted secrets. We can decrypt the secrets using the below command.

```
sops -d environments/env-secrets.yaml
```
