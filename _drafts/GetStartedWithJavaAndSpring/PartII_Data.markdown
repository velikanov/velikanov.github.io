---
layout: post
title:  "Get started with Java and Spring"
subtitle: "Part II. Data"
series: get_started_with_java_and_spring
goal: "Define all the needed entities and repositories"
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

_./library/src/main/java/com/company/library/entity/Video.java_
{% highlight java %}
package com.company.library.entity;

import org.hibernate.annotations.CreationTimestamp;
import org.hibernate.annotations.UpdateTimestamp;

import javax.persistence.*;
import java.util.Date;

@Entity
public class Video {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Integer id;
    @Column(nullable = false)
    private String title;
    @Column(unique = true, nullable = false)
    private Integer externalId;
    @Column(nullable = false)
    private String imageUrl;
    @Column(nullable = false)
    private String duration;

    @CreationTimestamp
    @Column(updatable = false)
    private Date createdDate;
    @UpdateTimestamp
    @Column
    private Date modifiedDate;

    public Integer getId() {
        return id;
    }

    public String getTitle() {
        return title;
    }
    public void setTitle(String title) {
        this.title = title;
    }

    public Integer getExternalId() {
        return externalId;
    }
    public void setExternalId(Integer externalId) {
        this.externalId = externalId;
    }

    public String getImageUrl() {
        return imageUrl;
    }
    public void setImageUrl(String imageUrl) {
        this.imageUrl = imageUrl;
    }

    public String getDuration() {
        return duration;
    }
    public void setDuration(String duration) {
        this.duration = duration;
    }

    public Date getCreatedDate() {
        return createdDate;
    }
    public void setCreatedDate(Date createdDate) {
        this.createdDate = createdDate;
    }

    public Date getModifiedDate() {
        return modifiedDate;
    }
    public void setModifiedDate(Date modifiedDate) {
        this.modifiedDate = modifiedDate;
    }
}
{% endhighlight %}

#### Creating repositories

#### Writing data

#### Fetching data
