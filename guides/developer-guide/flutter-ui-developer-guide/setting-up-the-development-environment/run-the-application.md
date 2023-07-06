# Run the Application

## Overview

Once the development environment setup is completed, we have to run the application locally, This document says how to run the works\_shg\_app in a local device



1. Clone the repo [https://github.com/egovernments/DIGIT-Works](https://github.com/egovernments/DIGIT-Works)

&#x20;                git clone https://github.com/egovernments/DIGIT-Works.git&#x20;

2. To run the application in the local environment, add the `.env` file in the root folder of the project  (`frontend/works_shg_app`)-

&#x20;     **Sample .env config:**&#x20;

`BASE_URL='https://works-dev.digit.org/'`

`MDMS_API_PATH='egov-mds-service/v1/_search'`

`GLOBAL_ASSETS='https://works-dev.digit.org/works-dev-asset/worksGlobalConfig.json'`

`ENV_NAME="DEV"`

![](<../../../../.gitbook/assets/image (17).png>)\


3. Run below commands  in your terminal from root of the project (frontend/works\_shg\_app)

**flutter clean** : To clean the build cache.

**flutter pub get** : To install the dependencies packages

<figure><img src="https://lh3.googleusercontent.com/SHrZwG_c2Vn1-bkZ-3exFhlQXb4IkoIY51DPH_UWHmuJ46wPOCaOe3TdAcvmZ4GbzhJMuagpOCt-LdqTwCRFyKJMGGQYTuJsz3jyamSW0iT_K76909l1mo0nTYRc2roKa7O6pDAK_ZYKyVlXbrwE7t0" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh3.googleusercontent.com/dhkc5EZMRB6vrTv4AWh6hoi_23ucWOKDTMke3yPBhf_IxX0LegcejIcHxFD6x85LrNB94dj3VkkA6tsHUFT8uCYI8EZce9zfFESUXp5NJ4zhQLcqGPIQFflSYEQiuSmVHS2ceRbW8SXdLvxU-WO2zqw" alt=""><figcaption></figcaption></figure>

4. Enable the desired device or browser  to run the application using the below command\
   **flutter run** : To start the application

<figure><img src="https://lh5.googleusercontent.com/l37Ter4BROECfKSXZ2-GMf6PeAolByl-JddJRvcvxFSIGDB0oPaPbpPlaSrKnUIhavpaGgrafHTU3PWKTcsAUPF4z95y1IG4v_OkakNt8MdJre1Rsl8qOlQLUJkft7Vup_HsTB33ArFzjST_Qqqqqks" alt=""><figcaption></figcaption></figure>

You can access flutter dev tools for debugging purpose from the link in the terminal

<figure><img src="https://lh6.googleusercontent.com/qGIR_8duLahPvljlOBLJF9LVyZjSDreye6QganNQGMAQigP4m8K2GbnPfCmCRrFeIakfgywAJ1vTHlutpZN24ElseB3V9yelV9wQE5015gaYK9l9SygvJuh-9RmqlS5d9ioUiRZE5Th5FmoC_5L6k74" alt=""><figcaption></figcaption></figure>
