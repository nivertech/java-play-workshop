<link href="index.css" rel="stylesheet" type="text/css">

<a id="top">Heroku Workshop - Java & Play framework</a>
=======================================================

    Document Date: January 16, 2013
    Document Home: http://java-play-todo-list.herokuapp.com

[Download the PDF](workbook.pdf)

This workshop will give you an introduction to building a relatively simple Java applications with the Play framework, deploying the application to Heroku.

* [Chapter 1: Getting Started with Java & Play on Heroku](#chapter1)
* [Chapter 2: Building a RESTful API](#chapter2)
* [Chapter 3: Integrating with Force.com](#chapter3)
* [Chapter 4: Distributed Sessions on Heroku](#chapter4)
* [Chapter 5: Real-time Push notifications](#chapter5)
* [Chapter 6: Performance Monitoring with New Relic](#chapter6)
* [Chapter 7: Searching Logs with Papertrail](#chapter7)
* [Appendix A: Further Learning](#appendix-a)


Prerequisites
-------------

Before you get started you will need to have an account with Heroku, the Heroku toolbelt and a working SSH connection to Heroku:

* Create an Heroku Account (if you dont already have one)
    1. In your browser navigate to: [https://heroku.com/signup](https://heroku.com/signup)
    2. Enter your email address
    3. Select `Sign Up`
    4. Check your email and navigate to the verification page
    5. On the command line, run `heroku login` to connect to Heroku and upload your public key.  If you do not have a public key then one will be created for you.

* Check network (SSH) access to heroku.com
    1. For Linux or MacOSX, either use an SSH client or `telnet` to verify the network connectin by running one of the following in a command prompt / terminal.  On Microsoft Windows you can use a tool called [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html):

            ssh -T heroku.com 22

    2. If the connection is refused then you will need to ask your network administrators to open up SSH access to `heroku.com` (port 22).


* Java SE 6 or greater:

    1. Check wich version of Java you are running on the command line using `java -version`

        $ java -version
        java version "1.6.0_37"
        Java(TM) SE Runtime Environment (build 1.6.0_37-b06-434-10M3909)
        Java HotSpot(TM) 64-Bit Server VM (build 20.12-b01-434, mixed mode)

    [http://www.oracle.com/technetwork/java/javase/downloads/index.html](http://www.oracle.com/technetwork/java/javase/downloads/index.html)

* Download & install Play framework version 2:

     [Download Play 2 framework](http://download.playframework.org/releases/)

Download the latest 2.0 RC version and extract the archive to a location where you have both read and write access.  For example, create a ~/apps/play folder and extract the archive there.

*(Play updates files within its own folder, so don’t install to /opt, /usr/local or anywhere else you’d need special permission to write to.)*

* Configure Play

    1. Add the folder you extracted Play framework into onto the system PATH.

        Linux and MacOSX:

        `export PATH=$PATH:/path/to/play20`

        Windows uses a global environment variable. Update the PATH in the environment variables to add the path to the Play framework folder, ensure you don’t use a path with spaces.

    2. On Linux & MacOSX, make sure that the play script is executable, otherwise do a `chmod a+x play`

    3. Test play is working by running `play help` on the command line


Now that everything is setup you are ready to create your first application on Heroku.

[Back to top...](#top)


<a id="chapter1">Chapter 1: Getting Started with Java & Play on Heroku</a>
-------------------------------------------------------------------------

Goals: In this chapter you will learn how to instantly deploy an application on Heroku using the Heroku Toolbelt.  You will also learn how to run the new application locally, make changes, and synchronize the changes with Heroku.  Then you will learn how to instantly scale your application, set configuration parameters through environment variables, and view your application's log entries.

Get started:




<a id="chapter2">Chapter 2: Building a RESTful API</a>
------------------------------------------------------






<a id="chapter6">Chapter 6: Performance Monitoring with New Relic</a>
---------------------------------------------------------------------

Goals: With the New Relic Heroku Add-on you can easily setup application performance monitoring and reporting.  This chapter will teach you how to add New Relic to your application.

New Relic provides an in-depth view into the performance and memory usage of applications on Heroku.

Start by adding the New Relic Add-on:

1. Navigate in your browser to [https://addons.heroku.com/newrelic](https://addons.heroku.com/newrelic)
2. Select `Add` for the free "Standard" level of service
3. Select your application from the drop-down
4. Select `+`

Now your application needs to be configured to use the New Relic Java agent:

1. Download the newest New Relic Java Agent zip file from [http://download.newrelic.com/newrelic/java-agent/newrelic-api/](http://download.newrelic.com/newrelic/java-agent/newrelic-api/)
2. Unzip the archive
3. Copy the `newrelic.jar` and `newrelic.yml` files into the root directory of your project

Commit these new files to your Git repository and push the new version to Heroku:


You need to change the default `JAVA_OPTS` environment variable for your application to the Java process to use the New Relic Java agent.

1. In Eclipse, in the `My Heroku Applications` view select the application's context menu
2. Select `App Info`
3. Select the `Environment Variables` tab
4. Select the environment variable with the key of `JAVA_OPTS`
5. Select `Edit`
6. In the `Value` field enter `-Xmx384m -Xss512k -XX:+UseCompressedOops -javaagent:newrelic.jar`
7. Select `OK`

Test the application on Heroku in your browser and verify that it works as expected.

You can now browse the New Relic Dashboard:

1. In your browser navigate to [https://api.heroku.com/myapps](https://api.heroku.com/myapps)
2. Select the application you added New Relic to
3. Select the `Add-ons` drop-down
4. Select `New Relic`

Explore the New Relic dashboard.  (Note: It might take a few minutes for some data to appear in the dashboard.)


<a id="chapter7">Chapter 7: Searching Logs with Papertrail</a>
--------------------------------------------------------------

Goals: This chapter will teach you how to add the Paptertrail Heroku Add-on to your application.  Papertrail provides a robust web interface for searching your application's logs and setting alerts for specific searches.

To add the Papertrail Add-on:

1. Navigate in your browser to [https://addons.heroku.com/papertrail](https://addons.heroku.com/papertrail)
2. Select `Add` for the free "Choklad" level of service
3. Select your application from the drop-down
4. Select `+`
5. Open the `Add-ons` drop-down for your application
6. Select `Papertrail`

After a minute or so Papertrail will have your latest logs.

Enter a search term like `WARN` in the search box at the bottom of the screen.  You will then see all of the log entries for your application which match that term.

You can setup Papertrail to notify you via email when new log entries matching your search are received:

1. Select `Save Search`
2. Enter a name for the saved search
3. Select `Save & Setup Alert`
4. Select `Emails`
5. In the `Recipients` field enter your email address
6. Choose a `Frequency`
7. Select `Update`

The next time your application has a log event that matches your search, you will receive an email notification.


<a id="appendix-a">Appendix A: Further Learning</a>
-------------------------------------------------

Heroku Basics:

* [How Heroku Works](http://heroku.com/how)
* [Heroku Dev Center](http://devcenter.heroku.com)

Java on Heroku:

* [Java on Heroku Dev Center](https://devcenter.heroku.com/categories/java)
* [Get started with Java on Heroku in your browser](http://java.heroku.com)
* [Heroku Eclipse Plugin](http://eclipse-plugin.herokuapp.com)

Integrating Java with Force.com:

* [Rich SObjects Library](https://github.com/ryanbrainard/richsobjects)
* [Force.com REST API Docs](http://www.salesforce.com/us/developer/docs/api_rest/index.htm)
* [Force.com Developer Resources](http://developer.force.com)

Cloud Application Architecture:

* [12 Factor App](http://12factor.net)