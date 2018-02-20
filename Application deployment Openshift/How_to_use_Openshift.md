# How to deploy an application on Openshift

**Authors:** Ruben Alliet, Ruben Bruggeman

## Requirements before you continue

* The source coded of your application hosted on github
* You should have installed the Openshift CLI. You can download it [here](https://docs.openshift.org/latest/cli_reference/get_started_cli.html).


## Step 2: Login/register on Openshift


First make sure that you're registered on openshift.
Visit [this](https://manage.openshift.com/) website to login to openshift.  

You can use the free tier subscription or the payed subscribtion. 
now click on the right top of the page where the username is displayed.

![](copylogincommand.PNG)

Now paste the login command to your terminal/command prompt.
The command should look something like this:

```
oc login https://api.starter-ca-central-1.openshift.com --token=0wjddpyDNNfhsK_8cLCaiC6oKvy50B0medcPvGRXb8k
```

## Step 3: Select a project or make a new project to deploy your application in

After you login to your account you will get a list of projects that you can switch between

Use this command to select a project:
```
oc project <project-name>
```

If you do not have any existing projects, you can create one:
```
oc new-project <project-name>
```

To show a high level overview of the current project:
```
oc status
```

## Step 4: Deploy your application

All base images can be find on [Redhat](https://access.redhat.com/containers/)

### 4.1. Dotnet CORE (C#)

Enter the following command in your terminal to create your dotnet Core application.
Replace the git repo with yours and specify the name of your application:

```
$ oc new-app --name=myapp registry.access.redhat.com/dotnet/dotnet-20-rhel7~https://github.com/openshift-evangelists/dotnet-core-2.0-example.git
```

Your output should look like this when the application was created sucesfully:

```
$ oc status
In project my project (myproject-fuseki) on server https://api.starter-ca-central-1.openshift.com:443

svc/dotnet-core-20-example - 172.30.166.111:8080
  dc/dotnet-core-20-example deploys istag/dotnet-core-20-example:latest <-
    bc/dotnet-core-20-example source builds https://github.com/openshift-evangelists/dotnet-core-2.0-example.git on istag/dotnet-20-rhel7:latest
    deployment #1 deployed 3 minutes ago - 1 pod

View details with 'oc describe <resource>/<name>' or list everything with 'oc get all'.
```  

### 4.2. Nodejs (JavaScript)

Pointing oc new-app at source code kicks off a chain of events, for our example run:

```
$ oc new-app https://github.com/openshift/nodejs-ex -l name=myapp
```

The tool will inspect the source code, locate an appropriate image on DockerHub, create an ImageStream for that image, and then create the right build configuration, deployment configuration and service definition.

(The -l flag will apply a label of "name=myapp" to all the resources created by new-app, for easy management later.)

Check the status of your new nodejs app with the command:

```
$ oc status
```

Which should return something like:

```
In project nodejs (nodejs-echo) on server https://10.2.2.2:8443

svc/nodejs-ex - 172.30.108.183:8080
dc/nodejs-ex deploys istag/nodejs-ex:latest <-
bc/nodejs-ex builds https://github.com/openshift/nodejs-ex with openshift/nodejs:0.10
build #1 running for 7 seconds
deployment #1 waiting on image or update
```

You can check the status of the build with the following command:

```
oc status
```

Optional: to manually add a hostname as the route for you application, enter the following command:

```
oc expose svc/nodejs-ex --hostname=www.example.com
``` 

Note: You can find the URL, where your application is hosted, in the web console > **Applications** > **Services** and there you can choose the right service.
Note: If you also would like to connect a database, like MongoDB, please refer to step 5.2 .


### 4.3. Apache httpd

The base image initializes PHP v7.0 with Apache 2.4 for a webserver. The used repository below is a PHP project.

```
oc new-app registry.access.redhat.com/rhscl/php-70-rhel7~https://github.com/Jefwillems/skosmos.git
```

Your output should look like this when the application was created sucesfully:

```
[rbruggeman@localhost Orga]$ oc status
In project php-mysql-test on server https://api.starter-ca-central-1.openshift.com:443

http://skosmos-php-mysql-test.193b.starter-ca-central-1.openshiftapps.com to pod port 8080-tcp (svc/skosmos)
  dc/skosmos deploys istag/skosmos:latest <-
    bc/skosmos source builds https://github.com/Jefwillems/skosmos.git on istag/php-70-rhel7:latest 
    deployment #1 deployed 34 minutes ago - 1 pod

View details with 'oc describe <resource>/<name>' or list everything with 'oc get all'.

```  


### 4.4. Tomcat (Java)

Enter the following command in your terminal to create your NodeJS application. Replace the git repo with yours and specify the name of your application:

```
oc new-app --name=pillar-base nodejs~http://github.com/OpenShiftDemos/pillar-base
``` 

The output should look something like this:

```
--> Found image 6f7f7d9 (5 weeks old) in image stream "nodejs" in project "openshift" under tag "0.10" for "nodejs"

    Node.js 0.10 
    ------------ 
    Platform for building and running Node.js 0.10 applications

    Tags: builder, nodejs, nodejs010

    * A source build using source code from http://github.com/OpenShiftDemos/pillar-base will be created
      * The resulting image will be pushed to image stream "pillar-base:latest"
    * This image will be deployed in deployment config "pillar-base"
    * Port 8080/tcp will be load balanced by service "pillar-base"
      * Other containers can access this service through the hostname "pillar-base"

--> Creating resources with label app=pillar-base ...
    imagestream "pillar-base" created
    buildconfig "pillar-base" created
    deploymentconfig "pillar-base" created
    service "pillar-base" created
--> Success
    Build scheduled, use 'oc logs -f bc/pillar-base' to track its progress.
    Run 'oc status' to view your app
```

### 4.5. Tomcat 8 (Java)

Enter the following command in your terminal to create your Java application.
Replace the git repo with yours and specify the name of your application:

```
oc new-app --name=myapp jboss-webserver30-tomcat8-openshift~https://github.com/openshiftdemos/os-sample-java-web.git
``` 

The output should look something like this:

```
--> Found image 298446b (7 weeks old) in image stream "jboss-webserver30-tomcat8-openshift" in project "openshift" under tag "1.2" for "jboss-webserver30-tomcat8-openshift:1.2"

    JBoss Web Server 3.0
    --------------------
    Platform for building and running web applications on JBoss Web Server 3.0 - Tomcat v8

    Tags: builder, java, tomcat8

    * A source build using source code from https://github.com/openshiftdemos/os-sample-java-web.git will be created
      * The resulting image will be pushed to image stream "os-sample-java-web:latest"
    * This image will be deployed in deployment config "os-sample-java-web"
    * Ports 8080/tcp, 8443/tcp, 8778/tcp will be load balanced by service "os-sample-java-web"
      * Other containers can access this service through the hostname "os-sample-java-web"

--> Creating resources with label app=os-sample-java-web ...
    imagestream "os-sample-java-web" created
    buildconfig "os-sample-java-web" created
    deploymentconfig "os-sample-java-web" created
    service "os-sample-java-web" created
--> Success
    Build scheduled, use 'oc logs -f bc/os-sample-java-web' to track its progress.
    Run 'oc status' to view your app.
``` 


Now we can run "oc status" to get information about your deployment, the output should look like this:

```
http://myapp-sample-project.44fs.preview.openshiftapps.com to pod port 8080-tcp (svc/myapp)
  dc/myapp deploys istag/myapp:latest <-
    bc/myapp builds http://github.com/openshiftdemos/os-sample-java-web#master with openshift/jboss-webserver30-tomcat8-openshift:1.2
      build #1 succeeded 2 minutes ago - 74cdd67: README added (Jorge Morales Pou <jorgemoralespou@users.noreply.github.com>)
    deployment #1 deployed 2 minutes ago - 1 pod
``` 


## Step 5: Add a database to your application (MySQL or MongoDB)

**5.1. MySQL:**


**5.2. MongoDB:**

You may have noticed the index page "Page view count" reads "No database configured". Let's fix that by adding a MongoDB service. We could use the second OpenShift template example (nodejs-mongodb.json) but for the sake of demonstration let's point oc new-app at a DockerHub image:

Note: Please pay attention when you copy-paste the command below ! This command sets the environment variables !

```
$ oc new-app centos/mongodb-26-centos7 -e MONGODB_USER=admin MONGODB_DATABASE=mongo_db MONGODB_PASSWORD=secret MONGODB_ADMIN_PASSWORD=supersecret
```

Optional: To take a look at environment variables set for each pod, run `oc env pods --all --list`.

We need to add the environment variable MONGO_URL to our Node.js web app so that it will utilize our MongoDB, and enable the "Page view count" feature. Run:

```
$ oc set env dc/nodejs-ex MONGO_URL='mongodb://admin:secret@172.30.0.112:27017/mongo_db'
```

You should now have a Node.js welcome page showing the current hit count, as stored in a MongoDB database.


## Step 6: Create a route for your application

OpenShift automatically created a new service for our application we just deployed, according to the name of the application. Now, let’s expose that service if you haven't done that before. To do that, run this command:

```
oc expose svc <naam-app>
``` 

And you should see something like this as output:

```
route <naam-app> exposed
``` 


## Step 7: Rebuild your application or Configure autobuild (after git commit)

When you have made code changes to your project you probably want to rebuild your application. There are two options to rebuild you application manually or automatically:

1.Manual rebuild

```
oc start-build <naam-app>
``` 

2.Auto rebuild

Configure openshift to automize rebuild process after a git push.



## Sources:

* https://github.com/sclorg/nodejs-ex/blob/master/README.md#setting-environment-variables
