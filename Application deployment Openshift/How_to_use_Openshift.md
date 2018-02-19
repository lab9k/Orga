# How to deploy an application on Openshift

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

### Dotnet CORE (C#)
Once you are inside , you can use a Git repo to upload a .NET Core 2.0 app using the image stream (IS). 

Here are URLs to use:

* NET Core 2.0 source-to-image builder: registry.access.redhat.com/dotnet/dotnet-20-rhel7
* NET Core 2.0 runtime image: registry.access.redhat.com/dotnet/dotnet-20-runtime-rhel7

Use the right URL for the right purpose in the following command:

```
$ oc new-app registry.access.redhat.com/dotnet/dotnet-20-rhel7~https://github.com/openshift-evangelists/dotnet-core-2.0-example.git
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


### Apache httpd











### Nodejs (JS)

### Tomcat (Java)



## Step 4: Create a route for your application




## Step 5: Configure autobuild (after git commit)