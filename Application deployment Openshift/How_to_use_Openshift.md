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

## Step 3 Deploy your application

### Dotnet CORE (C#)
Once you are inside , you can use a Git repo to upload a .NET Core 2.0 app using the image stream (IS). 

Here are URLs to use:

* NET Core 2.0 source-to-image builder: registry.access.redhat.com/dotnet/dotnet-20-rhel7
* NET Core 2.0 runtime image: registry.access.redhat.com/dotnet/dotnet-20-runtime-rhel7

Use the right URL for the right purpose in the following command:

```
$ oc new-app registry.access.redhat.com/dotnet/dotnet-20-rhel7~https://github.com/openshift-evangelists/dotnet-core-2.0-example.git
```

your output should look like this when the application was created sucesfully:

```
$ oc status
In project my project (myproject-fuseki) on server https://api.starter-ca-central-1.openshift.com:443

svc/dotnet-core-20-example - 172.30.166.111:8080
  dc/dotnet-core-20-example deploys istag/dotnet-core-20-example:latest <-
    bc/dotnet-core-20-example source builds https://github.com/openshift-evangelists/dotnet-core-2.0-example.git on istag/dotnet-20-rhel7:latest
    deployment #1 deployed 3 minutes ago - 1 pod

View details with 'oc describe <resource>/<name>' or list everything with 'oc get all'.
```

Your app should start deploying now. 




Important sidenote: Minishift does not support dotnetcore base images.  


### Apache + MySQL (PHP)
### Nodejs (JS)
### Tomcat (Java)













Configure autobuild (after git trigger)






> Short blurb about what your product does.

[![NPM Version][npm-image]][npm-url]
[![Build Status][travis-image]][travis-url]
[![Downloads Stats][npm-downloads]][npm-url]

One to two paragraph statement about your product and what it does.

![](header.png)

## Installation

OS X & Linux:

```sh
npm install my-crazy-module --save
```

Windows:

```sh
edit autoexec.bat
```

## Usage example

A few motivating and useful examples of how your product can be used. Spice this up with code blocks and potentially more screenshots.

_For more examples and usage, please refer to the [Wiki][wiki]._

## Development setup

Describe how to install all development dependencies and how to run an automated test-suite of some kind. Potentially do this for multiple platforms.

```sh
make install
npm test
```

## Release History

* 0.2.1
    * CHANGE: Update docs (module code remains unchanged)
* 0.2.0
    * CHANGE: Remove `setDefaultXYZ()`
    * ADD: Add `init()`
* 0.1.1
    * FIX: Crash when calling `baz()` (Thanks @GenerousContributorName!)
* 0.1.0
    * The first proper release
    * CHANGE: Rename `foo()` to `bar()`
* 0.0.1
    * Work in progress

## Meta

Your Name – [@YourTwitter](https://twitter.com/dbader_org) – YourEmail@example.com

Distributed under the XYZ license. See ``LICENSE`` for more information.

[https://github.com/yourname/github-link](https://github.com/dbader/)

## Contributing

1. Fork it (<https://github.com/yourname/yourproject/fork>)
2. Create your feature branch (`git checkout -b feature/fooBar`)
3. Commit your changes (`git commit -am 'Add some fooBar'`)
4. Push to the branch (`git push origin feature/fooBar`)
5. Create a new Pull Request

<!-- Markdown link & img dfn's -->
[npm-image]: https://img.shields.io/npm/v/datadog-metrics.svg?style=flat-square
[npm-url]: https://npmjs.org/package/datadog-metrics
[npm-downloads]: https://img.shields.io/npm/dm/datadog-metrics.svg?style=flat-square
[travis-image]: https://img.shields.io/travis/dbader/node-datadog-metrics/master.svg?style=flat-square
[travis-url]: https://travis-ci.org/dbader/node-datadog-metrics
[wiki]: https://github.com/yourname/yourproject/wiki