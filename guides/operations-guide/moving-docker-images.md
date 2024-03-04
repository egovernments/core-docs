---
description: To move docker images from one container to another container.
---

# Moving Docker Images

## Pre-requisites:

* Install [Docker](https://docs.docker.com/engine/install/ubuntu/) in your local machine.
* [Docker hub ](https://hub.docker.com)account.

## Procedure:

* To move the existing docker images from one account to another account by changing tags.
* First, we have to login to the docker account in which the images are present.

```
sudo docker login -u <user_name> -p <password>
```

* We need to pull the image from the docker container to local machine.

```
sudo docker pull <image_name>:<image_tag>
```

* Next, we have to change the tag name to our required docker container tag

```
sudo docker tag <image_id> <new_tag>/<image_name>:<image_tag>
```

* Now, we have our required images with tags in our local machine. We need to push these images from local machine to destination container. First, login to the destination account using the above docker login command and then push the image using below command.

```
docker push <image_name>:<image_tag>
```

* Once successfully pushed, if you check in your docker hub account the images will be present.
