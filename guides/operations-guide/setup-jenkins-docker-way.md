---
description: Jenkins for Build, Test and Deployment Automation
---

# Setup Jenkins - Docker way

While we are adopting the Microservices architecture, it also demands to have an efficient CI/CD tools like jenkins. Along the cloud-native application developement and deployment jenkins can also be run cloud-native.

Since all processes, including software build, test and deployment, are performed every two or four weeks, this is an ideal playground for automation tools like Jenkins: After the developer commits a code change to the repository, Jenkins will detect this change and will trigger the build and test process.  So Let's setup Jenkins as a docker container. Step-by-step.

## Installing Jenkins the Docker Way

### Tools and Versions used

* VM or EC2 Instance or a Standalone on-premisis machin
* Docker 1.12.1
* Jenkins 2.32.2
* Job DSL Plugin 1.58

### Prerequisites:

* Ubuntu or an Liniux  Machine
* Free RAM for the a VM/Machine  >\~ 4 GB.
* Docker Host is available.
* Tested with 3 vCPU (2 vCPU might work as well).



## Step 1: Install a Docker on the Host you provisioned for jenkins and Connect to the Host via SSH

If you are using an host already has docker installed, you can skip this step. Make sure that your host has enough memory.

We will run Jenkins in a [Docker](https://www.docker.com/) container in order to allow for maximum interoperability. This way, we always can use the latest Jenkins version without the need to control the java version used.

If you are new to Docker, you might want to read [this blog post](https://vocon-it.com/2015/09/28/what-are-containers-why-to-start-with-docker/).

Installing Docker on Windows and Mac can be a real challenge, but possible: here we will see an efficient way by using linux machine.&#x20;

**Prerequisites of this step:**

* I recommend to have direct access to the Internet: via Firewall, but without HTTP proxy.&#x20;
* Administration rights on you computer.

#### Step 2: Download Jenkins Image

This extra download step is optional, since the Docker image will be downloaded automatically in step 3, if it is not already found on the system:

<pre><code><strong>(dockerhost)$ sudo docker pull jenkins
</strong>Using default tag: latest
latest: Pulling from library/jenkins
Digest: sha256:8820149b54bfc5d05146b82150b5fdab583eef3e0499fb4ed630f77647a42942
Status: Image is up to date for jenkins:latest
</code></pre>

The version of the downloaded Jenkins image can be checked with following command:

<pre><code><strong>(dockerhost)$ sudo docker run -it --rm jenkins --version
</strong>2.19.3
</code></pre>

We are using version 2.9.13 currently. If you want to make sure that you use the exact same version as I have used in this blog, you can use the imagename `jenkins:2.19.3` in all docker commands instead of `jenkins` only.

> Note: The content of the jenkins image can be reviewed on [this link](https://imagelayers.io/?images=jenkins:2.3). There, we find that the image has an entrypoint `/bin/tini -- /usr/local/bin/jenkins.sh`, which we could override with the `--entrypoint bash` option, if we wanted to start a bash shell in the jenkins image. However, in Step 3, we will keep the entrypoint for now.

#### Step 3: Start Jenkins in interactive Terminal Mode

In this step, we will run Jenkins interactively (with `-it` switch instead of `-d` switch) to better see, what is happening. But first, we check that the port we will use is free:

<pre><code><strong>(dockerhost)$ sudo docker ps
</strong>CONTAINER ID        IMAGE                    COMMAND                  CREATED             STATUS              PORTS                                            NAMES
0ec82b4ca2fd        google/cadvisor:latest   "/usr/bin/cadvisor -l"   2 days ago          Up 2 days           0.0.0.0:8080->8080/tcp                           cadvisor
...
</code></pre>

Since we see that one of the standard ports of Jenkins (8080, 50000) is already occupied and I do not want to confuse the readers of this blog post by mapping the port to another host port, I just stop the cadvisor container for this „hello world“:

<pre><code><strong>(dockerhost)$ sudo docker stop cadvisor
</strong>cadvisor
</code></pre>

Jenkins will be in need of a persistent storage. For that, we create a new folder on the Docker host:

<pre><code><strong>(dockerhost)$ mkdir jenkins_home; cd jenkins_home
</strong></code></pre>

> Note: The content of the jenkins image can be reviewed on [this link](https://imagelayers.io/?images=jenkins:2.3). There, we find that the image has an entrypoint `/bin/tini -- /usr/local/bin/jenkins.sh`, which we could override with the `--entrypoint bash` option, if we wanted to start a bash shell in the jenkins image.

We start the Jenkins container with the jenkins\_home Docker host volume mapped to `/var/jenkins_home`:

<pre><code><strong>(dockerhost)$ sudo docker run -it --rm --name jenkins -p8080:8080 -p50000:50000 -v`pwd`:/var/jenkins_home jenkins
</strong>Running from: /usr/share/jenkins/jenkins.war
webroot: EnvVars.masterEnvVars.get("JENKINS_HOME")
Nov 30, 2016 6:12:14 PM Main deleteWinstoneTempContents
WARNING: Failed to delete the temporary Winstone file /tmp/winstone/jenkins.war
Nov 30, 2016 6:12:14 PM org.eclipse.jetty.util.log.JavaUtilLog info
INFO: Logging initialized @347ms
Nov 30, 2016 6:12:14 PM winstone.Logger logInternal
INFO: Beginning extraction from war file
Nov 30, 2016 6:12:14 PM org.eclipse.jetty.util.log.JavaUtilLog warn
WARNING: Empty contextPath
Nov 30, 2016 6:12:14 PM org.eclipse.jetty.util.log.JavaUtilLog info
INFO: jetty-9.2.z-SNAPSHOT
Nov 30, 2016 6:12:16 PM org.eclipse.jetty.util.log.JavaUtilLog info
INFO: NO JSP Support for /, did not find org.eclipse.jetty.jsp.JettyJspServlet
Jenkins home directory: /var/jenkins_home found at: EnvVars.masterEnvVars.get("JENKINS_HOME")
Nov 30, 2016 6:12:17 PM org.eclipse.jetty.util.log.JavaUtilLog info
INFO: Started w.@7674f035{/,file:/var/jenkins_home/war/,AVAILABLE}{/var/jenkins_home/war}
Nov 30, 2016 6:12:17 PM org.eclipse.jetty.util.log.JavaUtilLog info
INFO: Started ServerConnector@548d708a{HTTP/1.1}{0.0.0.0:8080}
Nov 30, 2016 6:12:17 PM org.eclipse.jetty.util.log.JavaUtilLog info
INFO: Started @3258ms
Nov 30, 2016 6:12:17 PM winstone.Logger logInternal
INFO: Winstone Servlet Engine v2.0 running: controlPort=disabled
Nov 30, 2016 6:12:17 PM jenkins.InitReactorRunner$1 onAttained
INFO: Started initialization
Nov 30, 2016 6:12:17 PM jenkins.InitReactorRunner$1 onAttained
INFO: Listed all plugins
Nov 30, 2016 6:12:19 PM jenkins.InitReactorRunner$1 onAttained
INFO: Prepared all plugins
Nov 30, 2016 6:12:19 PM jenkins.InitReactorRunner$1 onAttained
INFO: Started all plugins
Nov 30, 2016 6:12:19 PM jenkins.InitReactorRunner$1 onAttained
INFO: Augmented all extensions
Nov 30, 2016 6:12:20 PM jenkins.InitReactorRunner$1 onAttained
INFO: Loaded all jobs
Nov 30, 2016 6:12:20 PM hudson.model.AsyncPeriodicWork$1 run
INFO: Started Download metadata
Nov 30, 2016 6:12:20 PM hudson.model.AsyncPeriodicWork$1 run
INFO: Finished Download metadata. 97 ms
Nov 30, 2016 6:12:20 PM org.jenkinsci.main.modules.sshd.SSHD start
INFO: Started SSHD at port 44955
Nov 30, 2016 6:12:21 PM jenkins.util.groovy.GroovyHookScript execute
INFO: Executing /var/jenkins_home/init.groovy.d/tcp-slave-agent-port.groovy
Nov 30, 2016 6:12:22 PM jenkins.InitReactorRunner$1 onAttained
INFO: Completed initialization
Nov 30, 2016 6:12:22 PM org.springframework.context.support.AbstractApplicationContext prepareRefresh
INFO: Refreshing org.springframework.web.context.support.StaticWebApplicationContext@453fc3cf: display name [Root WebApplicationContext]; startup date [Wed Nov 30 18:12:22 UTC 2016]; root of context hierarchy
Nov 30, 2016 6:12:22 PM org.springframework.context.support.AbstractApplicationContext obtainFreshBeanFactory
INFO: Bean factory for application context [org.springframework.web.context.support.StaticWebApplicationContext@453fc3cf]: org.springframework.beans.factory.support.DefaultListableBeanFactory@79a53f4b
Nov 30, 2016 6:12:22 PM org.springframework.beans.factory.support.DefaultListableBeanFactory preInstantiateSingletons
INFO: Pre-instantiating singletons in org.springframework.beans.factory.support.DefaultListableBeanFactory@79a53f4b: defining beans [authenticationManager]; root of factory hierarchy
Nov 30, 2016 6:12:22 PM org.springframework.context.support.AbstractApplicationContext prepareRefresh
INFO: Refreshing org.springframework.web.context.support.StaticWebApplicationContext@7ea44b7: display name [Root WebApplicationContext]; startup date [Wed Nov 30 18:12:22 UTC 2016]; root of context hierarchy
Nov 30, 2016 6:12:22 PM org.springframework.context.support.AbstractApplicationContext obtainFreshBeanFactory
INFO: Bean factory for application context [org.springframework.web.context.support.StaticWebApplicationContext@7ea44b7]: org.springframework.beans.factory.support.DefaultListableBeanFactory@12544046
Nov 30, 2016 6:12:22 PM org.springframework.beans.factory.support.DefaultListableBeanFactory preInstantiateSingletons
INFO: Pre-instantiating singletons in org.springframework.beans.factory.support.DefaultListableBeanFactory@12544046: defining beans [filter,legacy]; root of factory hierarchy
Nov 30, 2016 6:12:22 PM jenkins.install.SetupWizard init
INFO:

*************************************************************
*************************************************************
*************************************************************

Jenkins initial setup is required. An admin user has been created and a password generated.
Please use the following password to proceed to installation:

0c4a8413a47943ac935a4902e3b8167e

This may also be found at: /var/jenkins_home/secrets/initialAdminPassword

*************************************************************
*************************************************************
*************************************************************

Nov 30, 2016 6:12:27 PM hudson.model.UpdateSite updateData
INFO: Obtained the latest update center data file for UpdateSource default
Nov 30, 2016 6:12:27 PM hudson.WebAppMain$3 run
INFO: Jenkins is fully up and running
--> setting agent port for jnlp
--> setting agent port for jnlp... done
</code></pre>

#### Step 4: Open Jenkins in a Browser

Now we want to connect to the Jenkins portal. For that, open a browser and open the URL

```
<your_jenkins_host>:8080
```

In our case, Jenkins is running in a container and we have mapped the container-port 8080 to the local port 8080 of the Docker host. On the Docker host, we can open the URL.

```
localhost:8080
```

The Jenkins login screen will open:

![2016-11-30-19\_36\_42-jenkins-jenkins](https://vocon-it.com/wp-content/uploads/2016/11/2016-11-30-19\_36\_42-jenkins-jenkins.png)

The admin password can be retrieved from the startup log, we have seen above (`0c4a8413a47943ac935a4902e3b8167e`), or we can find it by typing

<pre><code><strong>(dockerhost: .../jenkins_home)$ cat secrets/initialAdminPassword
</strong>0c4a8413a47943ac935a4902e3b8167e
</code></pre>

on the mapped jenkins\_home folder on the Docker host.

#### Step 5: Install Plugins

Let us install the suggested plugins:

<figure><img src="https://vocon-it.com/wp-content/uploads/2016/11/2016-11-30-19_37_43-setupwizard-jenkins.png" alt=""><figcaption></figcaption></figure>

This may take a while to finish:

<figure><img src="https://vocon-it.com/wp-content/uploads/2016/11/2016-11-30-19_39_38-setupwizard-jenkins.png" alt=""><figcaption></figcaption></figure>

#### Step 6: Create an Admin User and log in

Then we reach a page, where we can create an Admin user:

<figure><img src="https://vocon-it.com/wp-content/uploads/2016/11/2016-11-30-19_48_25-setupwizard-jenkins.png" alt=""><figcaption></figcaption></figure>

Let us do so and save and finish.

<figure><img src="https://vocon-it.com/wp-content/uploads/2016/11/2016-11-30-19_48_38-setupwizard-jenkins.png" alt=""><figcaption></figcaption></figure>

> Note: After this step, I have deleted the Jenkins container and started a new container attached to the same Jenkins Home directory. After that, all configuration and plugins were still available and we can delete containers after usage without loosing relevant information.

I have had a dinner break at this point. Maybe this is the reason I got following message when clicking the „Start using Jenkins“ button?

<figure><img src="https://vocon-it.com/wp-content/uploads/2016/11/2016-11-30-20_42_21-setupwizard-jenkins.png" alt=""><figcaption></figcaption></figure>

What ever. After clicking „retry“, we reach the login page:

<figure><img src="https://vocon-it.com/wp-content/uploads/2016/11/2016-11-30-20_44_53-jenkins.png" alt=""><figcaption></figcaption></figure>

#### Create a New Job

In the nex, we will create our first Jenkins job. I plan to trigger the Maven and/or Gradle build of a Java executable file upon detection of a code change.

<figure><img src="https://vocon-it.com/wp-content/uploads/2016/11/2016-11-30-20_47_12-dashboard-jenkins.png" alt=""><figcaption></figcaption></figure>

## Step 2: Install the Job DSL Plugin

The [Job DSL Plugin](https://wiki.jenkins-ci.org/display/JENKINS/Job+DSL+Plugin) can be installed like any other Jenkins plugin:

\-> ![Manage Jenkins](https://vocon-it.com/wp-content/uploads/2017/02/2017-02-14-19\_45\_32-dashboard-jenkins.png)\
\-> ![Manage Plugins](https://vocon-it.com/wp-content/uploads/2017/02/2017-02-14-19\_46\_30-manage-jenkins-jenkins.png)\
\-> ![Plugins - Available](https://vocon-it.com/wp-content/uploads/2017/02/2017-02-14-19\_47\_36-update-center-jenkins.png)

\-> ![Filter job-dsl](https://vocon-it.com/wp-content/uploads/2017/02/2017-02-25-11\_41\_52-update-center-jenkins.png) (with dash between job and dsl; wait for the filter to become active and do not press enter, otherwise you will get an error message)

\-> ![Install without restart](https://vocon-it.com/wp-content/uploads/2117/01/2017-02-11-20\_34\_21-update-center-jenkins.png)

<figure><img src="https://vocon-it.com/wp-content/uploads/2017/02/2017-02-24-20_00_15-update-center-jenkins.png" alt=""><figcaption></figcaption></figure>

<figure><img src="https://vocon-it.com/wp-content/uploads/2017/02/2017-02-24-20_08_27-update-center-jenkins.png" alt=""><figcaption></figcaption></figure>

## Step 3: Create Job DSL Jenkins Project

We create a Job DSL Job like follows:

\-> ![Back to Dashboard](https://vocon-it.com/wp-content/uploads/2017/02/2017-02-25-11\_48\_23-update-center-jenkins.png)

\-> ![New Item](https://vocon-it.com/wp-content/uploads/2016/12/2016-12-09-10\_25\_35-dashboard-jenkins.png)

<figure><img src="https://vocon-it.com/wp-content/uploads/2017/02/2017-02-24-20_10_41-new-item-jenkins.png" alt=""><figcaption></figcaption></figure>

<figure><img src="https://vocon-it.com/wp-content/uploads/2018/02/2017-02-15-19_42_31-new-item-jenkins.png" alt=""><figcaption></figcaption></figure>

\-> ![OK](https://vocon-it.com/wp-content/uploads/2018/02/2017-02-15-19\_45\_39-new-item-jenkins.png)

##

## Step 4: Configure Job DSL Project

\-> ![Add build step: Process Job DSLs](https://vocon-it.com/wp-content/uploads/2017/02/2017-02-24-20\_12\_34-jobdsljob-config-jenkins.png)

\-> if you have got a [Github](https://github.com/) account, fork [this open source Java Hello World software](https://github.com/oveits/java-maven-junit-helloworld) (originally created by of [LableOrg](https://github.com/LableOrg)) that will allow you to see, what happens with your Jenkins job, if you check in changed code. Moreover the hello world software allows you to perform [JUnit 4](http://junit.org/) tests, run [PowerMockito](https://code.google.com/p/powermock/) Mock services, run JUnit 4 Integration tests and calculate the code coverage using the tool [Cobertura](http://cobertura.github.io/cobertura/).

\-> [![Use the provided DSL script](https://vocon-it.com/wp-content/uploads/2017/02/2017-02-25-08\_47\_19-jobdsljob-config-jenkins.png)](https://vocon-it.com/wp-content/uploads/2017/02/2017-02-25-08\_47\_19-jobdsljob-config-jenkins.png)

\-> insert:

```
job('Job-DSL-Hello-World-Job') {
    scm {
        git('git://github.com/<org>/java-maven-junit-helloworld')
    }
    triggers {
        scm('H/15 * * * *')
    }
    steps {
        maven('-e clean test')
    }
}
```

here, exchange the username oveits by your own [Github](https://github.com/) username.\


<figure><img src="https://vocon-it.com/wp-content/uploads/2017/02/2017-02-25-11_50_36-jobdsljob-config-jenkins.png" alt=""><figcaption></figcaption></figure>

\-> ![Save](https://vocon-it.com/wp-content/uploads/2016/12/2016-12-22-19\_07\_35-github-triggered-build-config-jenkins.png)

## Step 5: Prepare Maven Usage

Goto Jenkins -> Manage Jenkins -> Global Tool Configuration (available for Jenkins >2.0)

<figure><img src="https://vocon-it.com/wp-content/uploads/2016/12/2016-12-09-11_34_55-manage-jenkins-jenkins.png" alt=""><figcaption></figcaption></figure>

<figure><img src="https://vocon-it.com/wp-content/uploads/2016/12/2016-12-09-11_35_26-global-tool-configuration-jenkins.png" alt=""><figcaption></figcaption></figure>

Scroll down to Maven -> ![Add Maven](https://vocon-it.com/wp-content/uploads/2016/12/2017-01-02-14\_38\_49-global-tool-configuration-jenkins.png)

<figure><img src="https://vocon-it.com/wp-content/uploads/2016/12/2017-01-02-14_32_46-global-tool-configuration-jenkins.png" alt=""><figcaption></figcaption></figure>

\-> choose Version (3.3.9 in my case)

\-> Add a name („Maven 3.3.9“ in my case)

\-> ![Save](https://vocon-it.com/wp-content/uploads/2016/12/2017-01-02-14\_26\_15-global-tool-configuration-jenkins.png)

Since we have checked „Install automatically“ above, I expect that it will be installed automatically on first usage.

## Step 6: Prepare Git Usage

As described in [this StackOverflow Q\&A](http://stackoverflow.com/questions/11122913/jenkins-git-tell-me-who-you-are-error-why-does-it-need-to-tag), we need to add the Git username and email address, since Jenkins tries to tag and commit on the Git repo, which requires those configuration items to be set. For that, we perform:

\-> ![2017-02-25-18\_04\_32-job-dsl-hello-world-job-1-console-jenkins](https://vocon-it.com/wp-content/uploads/2017/02/2017-02-25-18\_04\_32-job-dsl-hello-world-job-1-console-jenkins.png)

\-> ![Manage Jenkins](https://vocon-it.com/wp-content/uploads/2017/02/2017-02-14-19\_45\_32-dashboard-jenkins.png)

\-> ![Configure System](https://vocon-it.com/wp-content/uploads/2017/02/2017-02-25-18\_06\_36-manage-jenkins-jenkins.png)

\-> scroll down to „Git plugin“

\->&#x20;

<figure><img src="https://vocon-it.com/wp-content/uploads/2017/02/2017-02-25-18_07_51-configure-system-jenkins.png" alt=""><figcaption></figcaption></figure>

## Step 7: Create Jenkins Job from Code

### Step 7.1 Build Project

\-> ![Build Now](https://vocon-it.com/wp-content/uploads/2016/12/2017-01-02-15\_53\_05-github-triggered-build-jenkins.png)

### Step 7.2 (optional): Check Console Output

\-> ![Build History: click on latest #nnn](https://vocon-it.com/wp-content/uploads/2017/02/2017-02-25-11\_51\_50-jobdsljob-jenkins.png)

\-> ![Console Output](https://vocon-it.com/wp-content/uploads/2016/12/2017-01-02-15\_55\_38-github-triggered-build-2-jenkins.png)

<figure><img src="https://vocon-it.com/wp-content/uploads/2017/02/2017-02-25-11_53_18-jobdsljob-1-console-jenkins.png" alt=""><figcaption></figcaption></figure>

\->  ![Back to Project](https://vocon-it.com/wp-content/uploads/2017/02/2017-02-25-11\_56\_52-jobdsljob-1-console-jenkins.png)

### Step 7.3: Review automatically built Project

\-> ![2017-02-25-11\_48\_23-update-center-jenkins](https://vocon-it.com/wp-content/uploads/2017/02/2017-02-25-11\_48\_23-update-center-jenkins1.png)

<figure><img src="https://vocon-it.com/wp-content/uploads/2017/02/2017-02-25-11_59_46-dashboard-jenkins.png" alt=""><figcaption></figcaption></figure>

\-> ![Job-DSL-Hello-World-Job](https://vocon-it.com/wp-content/uploads/2017/02/2017-02-25-12\_00\_52-dashboard-jenkins.png)

<figure><img src="https://vocon-it.com/wp-content/uploads/2017/02/2017-02-25-12_03_05-job-dsl-hello-world-job-jenkins.png" alt=""><figcaption></figcaption></figure>

This is showing a build failure, since I had not performed Step 5 and 6 before. In your case, it should be showing a success (in blue). If you are experiencing problems here, check out the Appendices below.

\-> ![Configure](https://vocon-it.com/wp-content/uploads/2016/12/2017-01-02-15\_58\_57-github-triggered-build-jenkins.png)

\-> scroll down to Source Code Management

<figure><img src="https://vocon-it.com/wp-content/uploads/2017/02/2017-02-25-12_05_52-job-dsl-hello-world-job-config-jenkins.png" alt=""><figcaption></figcaption></figure>

\-> Scroll down to Build Triggers

<figure><img src="https://vocon-it.com/wp-content/uploads/2017/02/2017-02-25-12_07_25-job-dsl-hello-world-job-config-jenkins.png" alt=""><figcaption></figcaption></figure>

\-> Scroll down to Build

\-> verify that „Maven 3.3.9“ is chosen as defined in Step 5

\-> enter „-e clean test“ as Maven Goal

<figure><img src="https://vocon-it.com/wp-content/uploads/2017/02/2017-02-25-18_19_16-job-dsl-hello-world-job-config-jenkins.png" alt=""><figcaption></figcaption></figure>

\-> ![Build Now](https://vocon-it.com/wp-content/uploads/2016/12/2017-01-02-15\_53\_05-github-triggered-build-jenkins.png)

See, what happens by clicking on:

\-> Build History

\-> #nnn

\-> ![Console Output](https://vocon-it.com/wp-content/uploads/2016/12/2017-01-02-15\_55\_38-github-triggered-build-2-jenkins.png)

If everything went fine, we will see many downloads and a „BUILD SUCCESS“:

<figure><img src="https://vocon-it.com/wp-content/uploads/2017/02/2017-02-25-18_25_04-job-dsl-hello-world-job-3-console-jenkins.png" alt=""><figcaption></figcaption></figure>

## Appendix A: Solve Git Problem: „tell me who you are“

### Symptoms: Git Error: status code 128

In a new installation of Jenkins, Git does not seem to work out of the box. You can see this by choosing the Jenkins project Job-DSL-Hello-World-Job on the dashboard, then click „build now“, if the build was not already automatically triggered. Then:

\-> Build History

\-> [Last Build](http://localhost:8080/job/Job-DSL-Hello-World-Job/lastBuild/) (link works only, if Jenkins is running on localhost:8080 and you have chosen the same job name)

\-> ![Console Output](https://vocon-it.com/wp-content/uploads/2016/12/2017-01-02-15\_55\_38-github-triggered-build-2-jenkins.png)

There, we will see:

```
Caused by: hudson.plugins.git.GitException: Command "git tag -a -f -m Jenkins Build #1 jenkins-Job-DSL-Hello-World-Job-1" returned status code 128:
stdout: 
stderr: 
*** Please tell me who you are.

Run

  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"

to set your account's default identity.
Omit --global to set the identity only in this repository.

fatal: empty ident name (for <jenkins@61915398735e.(none)>) not allowed
```

### Resolution:

#### Step 1: Enter Git Username and Email

As described in [this StackOverflow Q\&A](http://stackoverflow.com/questions/11122913/jenkins-git-tell-me-who-you-are-error-why-does-it-need-to-tag): we can resolve this issue by either suppressing the git tagging, or (I think this is better) by adding your username and email address to git:

\-> ![2017-02-25-18\_04\_32-job-dsl-hello-world-job-1-console-jenkins](https://vocon-it.com/wp-content/uploads/2017/02/2017-02-25-18\_04\_32-job-dsl-hello-world-job-1-console-jenkins.png)

\-> ![Manage Jenkins](https://vocon-it.com/wp-content/uploads/2017/02/2017-02-14-19\_45\_32-dashboard-jenkins.png)

\-> ![Configure System](https://vocon-it.com/wp-content/uploads/2017/02/2017-02-25-18\_06\_36-manage-jenkins-jenkins.png)

\-> scroll down to „Git plugin“

\-> ![Git plugin; user.name = jenkins and user.email = admin@jenkins.org](https://vocon-it.com/wp-content/uploads/2017/02/2017-02-25-18\_07\_51-configure-system-jenkins.png)

Step 2: Re-run „Build Now“ on the Project

To test the new configuration, we go to

\-> the [Job-DSL-Hello-World-Job](http://localhost:8080/job/Job-DSL-Hello-World-Job/) and press

\-> [![Build Now](https://vocon-it.com/wp-content/uploads/2016/12/2017-01-02-15\_53\_05-github-triggered-build-jenkins.png)](http://localhost:8080/job/Job-DSL-Hello-World-Job/build?delay=0sec)

Now, we should see a BUILD SUCCESS like follows:

\-> Build History

\-> #nnn

\-> [![Console Output](https://vocon-it.com/wp-content/uploads/2016/12/2017-01-02-15\_55\_38-github-triggered-build-2-jenkins.png)](http://localhost:8080/job/Job-DSL-Hello-World-Job/lastBuild/console)

If everything went fine, we will a „BUILD SUCCESS“:

<figure><img src="https://vocon-it.com/wp-content/uploads/2017/02/2017-02-25-18_25_04-job-dsl-hello-world-job-3-console-jenkins.png" alt=""><figcaption></figcaption></figure>

## Appendix B: Maven Error: Cannot run program „mvn“

### Symptoms:

When running a Maven Goal, the following error may appear on the Console log:

```
FATAL: command execution failed
java.io.IOException: Cannot run program "mvn" (in directory "/var/jenkins_home/workspace/Job-DSL-Hello-World-Job"): error=2, No such file or directory
	at java.lang.ProcessBuilder.start(ProcessBuilder.java:1048)
	at hudson.Proc$LocalProc.(Proc.java:245)
	at hudson.Proc$LocalProc.(Proc.java:214)
	at hudson.Launcher$LocalLauncher.launch(Launcher.java:846)
	at hudson.Launcher$ProcStarter.start(Launcher.java:384)
	at hudson.Launcher$ProcStarter.join(Launcher.java:395)
	at hudson.tasks.Maven.perform(Maven.java:367)
	at hudson.tasks.BuildStepMonitor$1.perform(BuildStepMonitor.java:20)
	at hudson.model.AbstractBuild$AbstractBuildExecution.perform(AbstractBuild.java:779)
	at hudson.model.Build$BuildExecution.build(Build.java:205)
	at hudson.model.Build$BuildExecution.doRun(Build.java:162)
	at hudson.model.AbstractBuild$AbstractBuildExecution.run(AbstractBuild.java:534)
	at hudson.model.Run.execute(Run.java:1728)
	at hudson.model.FreeStyleBuild.run(FreeStyleBuild.java:43)
	at hudson.model.ResourceController.execute(ResourceController.java:98)
	at hudson.model.Executor.run(Executor.java:404)
Caused by: java.io.IOException: error=2, No such file or directory
	at java.lang.UNIXProcess.forkAndExec(Native Method)
	at java.lang.UNIXProcess.(UNIXProcess.java:247)
	at java.lang.ProcessImpl.start(ProcessImpl.java:134)
	at java.lang.ProcessBuilder.start(ProcessBuilder.java:1029)
	... 15 more
Build step 'Invoke top-level Maven targets' marked build as failure
Finished: FAILURE
```

Resolution:

Perform Step 5

<figure><img src="https://vocon-it.com/wp-content/uploads/2016/12/2017-01-02-14_32_46-global-tool-configuration-jenkins.png" alt=""><figcaption></figcaption></figure>

and

For Test, you can test a manual: choose the correct Maven version, when configuring a Maven build step like in Step 7:

<figure><img src="https://vocon-it.com/wp-content/uploads/2017/02/2017-02-25-18_19_16-job-dsl-hello-world-job-config-jenkins.png" alt=""><figcaption></figcaption></figure>

and verify that ![Build Now](https://vocon-it.com/wp-content/uploads/2016/12/2017-01-02-15\_53\_05-github-triggered-build-jenkins.png) does not throw the Maven error anymore.

For our case, we need to correct the Job DSL like follows:

In the Script, we had defined the step:

```
    steps {
        maven('-e clean test')
    }
```

However, we need to define the Maven Installation like follows:

```
    steps {
        maven {
            mavenInstallation("Maven 3.3.9")
            goals('-e clean test')
        }
    }
```

Here, the mavenInstallation needs to specify the exact same name, as the one we have chosen in Step 5 above.

After correction, we will receive the correct Maven goal

\-> JobDSL -> ![Build Now](https://vocon-it.com/wp-content/uploads/2016/12/2017-01-02-15\_53\_05-github-triggered-build-jenkins.png)

Now, we can check the Maven configuration:

\-> ![Jenkins Home leading to the Dashboard](https://vocon-it.com/wp-content/uploads/2017/02/2017-02-25-18\_04\_32-job-dsl-hello-world-job-1-console-jenkins.png)

\-> ![Job-DSL-Hello-World-Job](https://vocon-it.com/wp-content/uploads/2017/02/2017-02-25-12\_00\_52-dashboard-jenkins.png)

\-> ![Configure](https://vocon-it.com/wp-content/uploads/2016/12/2017-01-02-15\_58\_57-github-triggered-build-jenkins.png)

After scrolling down, we will see the correct Maven Version:

<figure><img src="https://vocon-it.com/wp-content/uploads/2017/02/2017-02-25-18_19_16-job-dsl-hello-world-job-config-jenkins.png" alt=""><figcaption></figcaption></figure>

DONE

## Appendix C: Updating Jenkins

Updating Jenkins (in my case: from 2.32.1 to 2.32.2) was as simple as following the steps below

> Note: you might want to make a backup of your jenkins\_home though. Just in case…

<pre><code><strong>(dockerhost)$ cd &#x3C;path_to_jenkins_home> # in my case: cd /user/jenkins_home/
</strong><strong>(dockerhost)$ docker pull jenkins # to update the jenkins image
</strong><strong>(dockerhost)$ docker rm jenkins # to make shure the container named jenkins is removed
</strong><strong>(dockerhost:jenkins_home)$ sudo docker run -d --rm --name jenkins -p8080:8080 -p50000:50000 -v`pwd`:/var/jenkins_home jenkins
</strong></code></pre>

However, after that, some data was unreadable:

[![2017-02-24-20\_04\_36-manage-old-data-jenkins](https://vocon-it.com/wp-content/uploads/2017/02/2017-02-24-20\_04\_36-manage-old-data-jenkins.png)](https://vocon-it.com/wp-content/uploads/2017/02/2017-02-24-20\_04\_36-manage-old-data-jenkins.png)

I have clicked

\-> Manage Jenkins\
\-> Manage\
\-> [![Discard Unreadable Data](https://vocon-it.com/wp-content/uploads/2017/02/2017-02-24-20\_05\_42-manage-old-data-jenkins.png)](https://vocon-it.com/wp-content/uploads/2017/02/2017-02-24-20\_05\_42-manage-old-data-jenkins.png)

to resolve the issue (hopefully…). At least, after that, the warning was gone.

## Appendix D: Job DSL Syntax

The reference for the Job DSL syntax can be found on the [Job DSL Plugin API pages](https://jenkinsci.github.io/job-dsl-plugin/). As an example, the syntax of Maven within a Freestyle project can be found on [this page](https://jenkinsci.github.io/job-dsl-plugin/#path/freeStyleJob-steps-maven) found via the path

\> freeStyleJob > steps > maven:

```
maven {

```

*   // Allows direct manipulation of the generated XML.

    [configure](https://jenkinsci.github.io/job-dsl-plugin/#path/freeStyleJob-steps-maven-configure)(Closure configureBlock)
*   // Specifies the goals to execute including other command line options.

    [goals](https://jenkinsci.github.io/job-dsl-plugin/#path/freeStyleJob-steps-maven-goals)(String goals)
*   // Skip injecting build variables as properties into the Maven process.

    [injectBuildVariables](https://jenkinsci.github.io/job-dsl-plugin/#path/freeStyleJob-steps-maven-injectBuildVariables)(boolean injectBuildVariables = true)
*   // Set to use isolated local Maven repositories.

    [localRepository](https://jenkinsci.github.io/job-dsl-plugin/#path/freeStyleJob-steps-maven-localRepository)(javaposse.jobdsl.dsl.helpers.LocalRepositoryLocation location)
*   // Specifies the Maven installation for executing this step.

    [mavenInstallation](https://jenkinsci.github.io/job-dsl-plugin/#path/freeStyleJob-steps-maven-mavenInstallation)(String name)
*   // Specifies the JVM options needed when launching Maven as an external process.

    [mavenOpts](https://jenkinsci.github.io/job-dsl-plugin/#path/freeStyleJob-steps-maven-mavenOpts)(String mavenOpts)
*   // Adds properties for the Maven build.

    [properties](https://jenkinsci.github.io/job-dsl-plugin/#path/freeStyleJob-steps-maven-properties)(Map props)
*   // Adds a property for the Maven build.

    [property](https://jenkinsci.github.io/job-dsl-plugin/#path/freeStyleJob-steps-maven-property)(String key, String value)
*   // Specifies the managed global Maven settings to be used.

    [providedGlobalSettings](https://jenkinsci.github.io/job-dsl-plugin/#path/freeStyleJob-steps-maven-providedGlobalSettings)(String settingsIdOrName)
*   // Specifies the managed Maven settings to be used.

    [providedSettings](https://jenkinsci.github.io/job-dsl-plugin/#path/freeStyleJob-steps-maven-providedSettings)(String settingsIdOrName)
*   // Specifies the path to the root POM.

    [rootPOM](https://jenkinsci.github.io/job-dsl-plugin/#path/freeStyleJob-steps-maven-rootPOM)(String rootPOM)

```
}
```

A Maven example can be found on the same page:

```
job('example') {
    steps {
        maven('verify')
        maven('clean verify', 'module-a/pom.xml')
        maven {
            goals('clean')
            goals('verify')
            mavenOpts('-Xms256m')
            mavenOpts('-Xmx512m')
            localRepository(LocalRepositoryLocation.LOCAL_TO_WORKSPACE)
            properties(skipTests: true)
            mavenInstallation('Maven 3.1.1')
            providedSettings('central-mirror')
        }
    }
}
```

## Summary

In this blog post, we have learned how to

1. Start and initialize Jenkins via Docker
2. Prepare the usage of Git and Maven
3. Install the Job DSL Plugin
4. Define a Jenkins Job via Groovy script
5. Create a Jenkins Job by a push of  the „Build now“ button
6. Review and run the automatically created Jenkins job

We have seen that the usage of the Job DSL is no rocket science. The only topic, we had to take care, is, that Git and Maven need to be prepared for first usage on a Jenkins server.

\
