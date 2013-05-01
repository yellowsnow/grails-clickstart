
# Grails on CloudBees

Press the button to build, test and deploy this instantly:

<a href="https://grandcentral.cloudbees.com/?CB_clickstart=https://raw.github.com/Cloudbees-community/grails-clickstart/master/clickstart.json"><img src="https://d3ko533tu1ozfq.cloudfront.net/clickstart/deployInstantly.png"/></a>




# Manual setup on CloudBees

Instructions for a manual setup with the [CloudBees SDK](http://wiki.cloudbees.com/bin/view/RUN/BeesSDK).

## Create a Tomcat6 container

```
bees app:create -a community/grails-clickstart jvmPermSize=128
```

Please not the extra `jvmPermSize` for Grails framework.

## Set Grails Environment to 'production'

```
bees config:set -a community/grails-clickstart -P grails.env=production
```

See [Grails Doc > Environments](http://www.grails.org/Environments).

## Create a MySQL Database

```
bees db:create community/grails-clickstart
```

## Bind the MySQL Database to the Tomcat container

```
bees app:bind -a community/grails-clickstart -db community/grails-clickstart -as mydb
```

This binding injects in the container:

* System properties
  * `DATABASE_URL_MYDB` starting with `mysql:` (e.g. "mysql://ec2-x-y-z-w.compute-1.amazonaws.com:3306/grails-clickstart")
  * `DATABASE_USERNAME_MYDB`
  * `DATABASE_PASSWORD_MYDB`
* a JNDI datasource `java:comp/env/jdbc/mydb`

More details on [RUN@cloud >> Binding services (resources) to applications](http://wiki.cloudbees.com/bin/view/RUN/Resource+Management)

## Create a Jenkins job based on Grails Wrapper

Create a Jenkins job as described in [DEV@cloud » Continuous Integration with Grails and Jenkins](https://developer.cloudbees.com/bin/view/DEV/CI_With_Grails_And_Jenkins).

# To run the application locally

Use the [Grails Wrapper](http://grails.org/doc/2.2.0/ref/Command%20Line/wrapper.html)

    grailsw run-app


