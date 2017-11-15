---
layout: post
title:  "Get started with Java and Spring"
subtitle: "Part III. Fast Data"
series: get_started_with_java_and_spring
goal: "Setting and getting fast data with Redis"
date: 2017-10-12 18:47:29 +0300
---
{% include series.html %}

## Part III. Fast Data
### Introduction

### Action
#### Using Redis in project



#### Creating repositories
Definitely we want to search for videos in our database.

And [Spring JPA Repositories](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#repositories) come in
very handy for us.

So now we have to define our Video Repository and some methods inside to retrieve our videos.

<code>./library/src/main/java/com/company/library/domain/VideoRepository.java</code>
{% highlight java linenos %}
{% include {{ sources_path }}/library/src/main/java/com/company/library/domain/VideoRepository.java.v1 %}
{% endhighlight %}

That's the Spring way to describe repository methods. And it really rocks, 'cause you don't really need to implement all
the data retrieving logic. Take a closer look - it's just an interface that describes needed data retrieval methods.

You just write that you want to fetch the particular page of most recent entries and… that's it!
