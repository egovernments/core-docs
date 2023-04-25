# Creation of Dockerhub account

**Docker Hub:** It is a service provided by Docker for finding and sharing container images with our team. Key features include: Private Repositories: Push and pull container images. Automated Builds: Automatically build container images from GitHub and Bitbucket and push them to Docker Hub.

Users get access to free public repositories for storing and sharing images or can choose a **subscription plan** for private repositories.

#### **What is the use of Docker Hub repository?**

Docker Hub repositories allow you share container images with your team, customers, or the Docker community at large. Docker images are pushed to Docker Hub through the docker push command. A single Docker Hub repository can hold many Docker images.

#### **Docker Hub provides the following major features:**

* **Repositories:** Push and Pull container images.
* **Teams and Organization:** Manage access to private repositories of contanier images.
* **Docker Offical Images:** Pull and use high-quality container images provided by Docker.
* **Docker Verified Publisher Images:** Pull and use high-quality container images provided by extrernal vendors.
* **Builds:** Automatically build container images from GitHub and push them to Docker Hub.
* **Webhooks:** Trigger actions after a successful to repository to integrate Docker Hub with other services.

The following steps containes instructions on how to easily get Login to Docker Hub.

### **Step 1:** Sign up for Docker account.

* Follow the link below to create a Docker ID.

{% embed url="https://hub.docker.com/signup" %}

### **Step 2: Create your first repository.**

* Sign in to [https://hub.docker.com/](https://hub.docker.com/)
* Click and create a Repository on the Docker Hub welcome page.

<figure><img src="../../../.gitbook/assets/Screenshot from 2022-12-12 11-51-12.png" alt=""><figcaption></figcaption></figure>

* Name it in <**Your-username>**.
* Set the visibility to private.

<figure><img src="../../../.gitbook/assets/Screenshot from 2022-12-12 12-02-48.png" alt=""><figcaption></figcaption></figure>

* Click create.

&#x20;     You have created your first repository.

<figure><img src="../../../.gitbook/assets/Screenshot from 2022-12-12 12-04-31.png" alt=""><figcaption></figcaption></figure>

### Step 3: Download and Install Docker Desktop:

&#x20;  You will need to download Docker desktop to build, push and pull container images.

* Download and install Docker desktop by following link given below

{% embed url="https://docs.docker.com/desktop/" %}

* Sign in to the Docker desktop application using the Docker ID you have just created.

### Step 4: Pull and run a container image from Docker Hub:

* Run the following command to pull the image from Docker Hub.

```
$ docker pull hello-world
```

* Run the image locally.

```
$ docker run hello-world
```

&#x20;   Then the **output** will be similar to;

```
Hello from Docker!
This message shows that your installation appears to be working correctly.
* To try something more ambitious, you can run an Ubuntu contanier with:
$ docker run -it ubuntu bash   
```

### &#x20;    Step 5: Build and push a container image to Docker Hub from your   computer:

* Start by creating a <mark style="color:blue;">Dockerfile</mark> to specify your application.
* Run the command to build your Docker image.

```
$ docker build -t <your_username>/my_repo 
```

* Run your Docker image locally.

```
$ docker run <your_username>/my_repo
```

* Login in to a Docker registry.

```
$ docker login [OPTIONS] [SERVER]
```

&#x20;     Options:

| Name             | Description                  |
| ---------------- | ---------------------------- |
| --password , -p  | password                     |
| --password-stdin | take the password from stdin |
| --username , -u  | username                     |

* Push your Docker image Docker Hub.&#x20;

```
$ docker push <your_username>/my_repo
```

Your repository in Docker Hub should now display new Latest tags under **Tags.**

