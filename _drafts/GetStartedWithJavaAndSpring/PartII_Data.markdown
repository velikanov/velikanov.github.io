---
layout: post
title:  "Get started with Java and Spring"
subtitle: "Part II. Data"
series: get_started_with_java_and_spring
goal: "Read and write the data"
date: 2017-10-12 18:47:28 +0300
---
{% include series.html %}

## Part II. Data
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

_`./library/src/main/java/com/company/library/entity/Video.java`_
{% highlight java %}
{% include {{ sources_path }}/library/src/main/java/com/company/library/entity/Video.java.v1 %}
{% endhighlight %}

Here we have defined some key abilities for our main entity like
[Generated Id](https://en.wikibooks.org/wiki/Java_Persistence/Identity_and_Sequencing#Sequencing) and
[Creation/Update Timestamps](https://www.thoughts-on-java.org/persist-creation-update-timestamps-hibernate/).

#### Creating repositories
Definitely we want to search for videos in our database.

And [Spring JPA Repositories](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#repositories) come in
very handy for us.

Let's define our Video Repository and some methods inside to retrieve our videos.

_`./library/src/main/java/com/company/library/repository/VideoRepository.java`_
{% highlight java %}
{% include {{ sources_path }}/library/src/main/java/com/company/library/repository/VideoRepository.java.v1 %}
{% endhighlight %}

That's the Spring way to describe repository methods. And it really rocks, 'cause you don't really need to implement all
the data retrieving logic. Take a closer look - it's just an interface that describes needed data retrieval methods.

You just write that you want to fetch the particular page of most recent entries and… that's all!

#### Writing data

#### Fetching data
