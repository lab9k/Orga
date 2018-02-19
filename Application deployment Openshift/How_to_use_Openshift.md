# How to deploy an application on Openshift

## Requirements before you continue
* The source coded of your application hosted on github
* 

## Step 1: Login/register on Openshift
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

## Step 2: Select a project or make a new project to deploy your application in

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

## Step 3: Deploy your application

All base images can be find on [Redhat](https://access.redhat.com/containers/)

### a.Dotnet CORE (C#)

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

### b.Apache + MySQL (PHP)



### c.Nodejs (JavaScript)

### Apache httpd











### Nodejs (JS)

### Tomcat (Java)
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

### d.Tomcat 8 (Java)

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


## Step 4: Create a route for your application
OpenShift automatically created a new service for our application we just deployed, according to the name of the application. Now, let’s expose that service, to do that, run this command:

```
oc expose svc myapp
``` 

And you should see something like this as output:

```
route "myapp" exposed
``` 


## Step 5: Rebuild your application or Configure autobuild (after git commit)

When you have made code changes to your project you probably want to rebuild your application. There are two options to rebuild you application manually or automatically:

1.Manual rebuild

```
oc start-build myapp
``` 

2.Auto rebuild
Configure openshift to automize rebuild process after a git push.
