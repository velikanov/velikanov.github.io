---
layout: post
title:  "Get started with Java and Spring"
subtitle: "Part II. Data"
series: get_started_with_java_and_spring
goal: "Read and write the data"
repo_link: "https://github.com/velikanov/tube/tree/part2_data"
date: 2017-10-12 18:47:28 +0300
---
{% include series.html %}

## Part II. Data

{% include sources.html %}

### Introduction
[Spring Data JPA](https://projects.spring.io/spring-data-jpa/) is the best way to bootstrap your database interaction
facilities in the application.

[JPA](https://en.wikipedia.org/wiki/Java_Persistence_API) itself provides you with the ability to describe entities,
relations and many more while Spring Data JPA is used to interact with entities easily through Repositories.

### Action
#### Defining entities
Let's start with defining of Video entity.

At the beginning it will store the base information about our videos like title, thumbnail and duration.

Also we need to store the external id of the video to make sure that we don't need to fetch this video second time.

_`./library/src/main/java/com/company/library/domain/Video.java`_
{% highlight java %}
{% include {{ sources_path }}/library/src/main/java/com/company/library/domain/Video.java.v1 %}
{% endhighlight %}

Here we have defined some key abilities for our main entity like
[Generated Id](https://en.wikibooks.org/wiki/Java_Persistence/Identity_and_Sequencing#Sequencing) and
[Creation/Update Timestamps](https://www.thoughts-on-java.org/persist-creation-update-timestamps-hibernate/).

Also we have an unique External ID that we will use to avoid duplicates in our data storage.

#### Creating repositories
Definitely we want to search for videos in our database.

And [Spring JPA Repositories](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#repositories) come in
very handy for us.

Let's define our Video Repository and some methods inside to retrieve our videos.

_`./library/src/main/java/com/company/library/domain/VideoRepository.java`_
{% highlight java %}
{% include {{ sources_path }}/library/src/main/java/com/company/library/domain/VideoRepository.java.v1 %}
{% endhighlight %}

That's the Spring way to describe repository methods. And it really rocks, 'cause you don't really need to implement all
the data retrieving logic. Take a closer look - it's just an interface that describes needed data retrieval methods.

You just write that you want to fetch the particular page of most recent entries and… that's all!

#### Configuring the Scheduler
First of all we have to fetch some videos to store them in our database.

We need to run a periodic task that will run with one minure intervals and watch the updates on external website.

We'll start from defining the Spring Boot Application that will search for any
[scheduled tasks](https://spring.io/guides/gs/scheduling-tasks/) and run them as we configure.

_`./scheduler/src/main/java/com/company/scheduler/Scheduler.java`_
{% highlight java %}
{% include {{ sources_path }}/scheduler/src/main/java/com/company/scheduler/Scheduler.java.v1 %}
{% endhighlight %}

Here we have defined our Spring Boot Application and allowed to run it using Scheduler class.

But first we have to define our database connection in `application.properties` file - the main
[Spring Boot configuration file]((http://www.baeldung.com/properties-with-spring)).

> By the way, you can find more about possible properties [here](https://docs.spring.io/spring-boot/docs/current/reference/html/common-application-properties.html).

_`./scheduler/src/main/resources/application.properties`_
{% highlight ini %}
{% include {{ sources_path }}/scheduler/src/main/resources/application.properties.v1 %}
{% endhighlight %}

Here we have defined our DSN with auto reconnection feature and without using SSL just to suppress the non-secured
connection warning.

Also we specified the SQL Dialect used by [Hibernate](http://hibernate.org/) data framework.

That's almost all but we need to have a database running so we can kickstart it using [Docker](https://www.docker.com/)
with [Docker Compose](https://docs.docker.com/compose/) like this.

If you are a Mac OS user you definitely want to use 
[Docker for Mac](https://docs.docker.com/docker-for-mac/install/#download-docker-for-mac). Especially its Edge version.

_`./docker-compose.yml`_
{% highlight yaml %}
{% include {{ sources_path }}/docker-compose.yml.v1 %}
{% endhighlight %}

Start the database container using `docker-compose up` command from inside the directory where `docker-compose.yml` is
located and we'll have our shiny new database server running and listening on our host 3306 port.

Sure we need to include the MySQL dependency in case to be able to interact with MySQL database.

_`./pom.xml`_
{% highlight xml %}
{% include {{ sources_path }}/pom.xml.v1 %}
{% endhighlight %}

And finally we are ready to run our Scheduler application.

#### Preparations

Right now our application doesn't make any sense. It runs and dies without any useful goals achieved.

So we have to schedule our operations.

Let's write a basic crawler interface and service that will implement the crawling method.

Then we just call this service from our scheduled task and actually write data to the database.

_`./scheduler/src/main/java/com/company/scheduler/crawler/Crawler.java`_
{% highlight java %}
{% include {{ sources_path }}/scheduler/src/main/java/com/company/scheduler/crawler/Crawler.java.v1 %}
{% endhighlight %}

Right now we need our crawlers to do just one thing - crawl. No remorse.

_`./scheduler/src/main/java/com/company/scheduler/crawler/VideoCrawler.java`_
{% highlight java %}
{% include {{ sources_path }}/scheduler/src/main/java/com/company/scheduler/crawler/VideoCrawler.java.v1 %}
{% endhighlight %}

This is the place where all the hard work will be made.

Our crawler is a 
[Component](https://www.concretepage.com/spring/spring-auto-detection-with-component-service-repository-and-controller-stereotype-annotation-example-using-componentscan-and-component-scan#component)
that will be found by Spring Boot Component Scan and can be [Autowired](http://www.baeldung.com/spring-autowire) in
other components.

_`./scheduler/src/main/java/com/company/scheduler/schedule/CrawlSchedules.java`_
{% highlight java %}
{% include {{ sources_path }}/scheduler/src/main/java/com/company/scheduler/schedule/CrawlSchedules.java.v1 %}
{% endhighlight %}

And this is our almighty Video Crawler that will be called after 60 seconds has passed since last call or at the start
of our application.

Finally we can run our Scheduler application and realise that we have our Video Crawler running.

#### Fetching data

Now we can start to actually crawl videos from external source and store them in our object layer.

As we getting started with YouTube we will need an [API key](https://developers.google.com/youtube/v3/getting-started)
to be able to get videos updates.

When we have obtained API key we can start to implement our fetcher.

First of all we need to store the API key somewhere not in source code.

So let's do this inside our `application.properties` file.

_`./scheduler/src/main/resources/application.properties`_
{% highlight ini %}
{% include {{ sources_path }}/scheduler/src/main/resources/application.properties.v2 %}
{% endhighlight %}

{% include sources.html %}
