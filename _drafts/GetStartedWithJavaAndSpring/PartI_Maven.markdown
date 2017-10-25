---
layout: post
title: "Get started with Java and Spring"
subtitle: "Part I. Maven"
series: get_started_with_java_and_spring
goal: "Bootstrap a new modular project with Maven"
date: 2017-10-12 18:47:27 +0300
---
{% include series.html %}

{{page.path}}

## Part I. Maven
### Introduction
[Apache Maven](https://maven.apache.org/) is not just a dependency manager (like PHP’s 
[Composer](https://getcomposer.org/) is) but a full stack project management solution which helps you to bootstrap 
your application using all the dependencies needed, build it and deploy.

### Action
#### Creating a project
Let’s start with creating a new Maven project with `File → New → Project…`

Find and select project category Maven and choose your project SDK (for now it’s 1.8).
If you haven’t any then you need to install JDK e.g. from 
[Oracle official website](http://www.oracle.com/technetwork/java/javase/downloads/index.html). 

For now we won’t create our application from any
[archetype](https://maven.apache.org/guides/introduction/introduction-to-archetypes.html). Click `Next`.

![Creating a project. Step 1]({{ "/assets/img/GetStartedWithJavaAndSpring/PartI_Maven/Action_CreatingAProject/Step1.png" }})

Now we need to enter our company name (called GroupId) e.g. `com.company` and application name (called ArtifactId) e.g.
`tube`. Let’s leave version as it is.

![Creating a project. Step 2]({{ "/assets/img/GetStartedWithJavaAndSpring/PartI_Maven/Action_CreatingAProject/Step2.png" }})

Then we choose the location of our project and finally we can start.

![Creating a project. Step 3]({{ "/assets/img/GetStartedWithJavaAndSpring/PartI_Maven/Action_CreatingAProject/Step3.png" }})

#### Working with Maven
After the project creation you’ll be asked to Auto-Import all the Maven dependencies.

I prefer to do this, because if you do so then you won’t need to reimport projects manually after any dependency
updates in your [POM file](https://maven.apache.org/guides/introduction/introduction-to-the-pom.html).

You can enable Auto-Import later in IntelliJ IDEA Preferences: `Build, Execution, Deployment → Build Tools → Maven →
Importing` and checking the `Import Maven projects automatically` box.

![Working with Maven. Import Maven projects automatically]({{ "/assets/img/GetStartedWithJavaAndSpring/PartI_Maven/WorkingWithMaven/ImportMavenProjectsAutomatically.png" }})

We’ll start with three submodules in our project:
* `Library` - the main entity and repository storage.
* `Presenter` - our web frontend.
* `Scheduler` - the data handler.

Let's write modules definition (under `<modules>` section) in our root `pom.xml`:

{% highlight xml %}
{% include series/GetStartedWithJavaAndSpring/PartI_Maven/pom.xml.v1 %}
{% endhighlight %}

Then we can bootstrap all our modules using IntelliJ IDEA's intentions.

Choose `Create Module with parent` to share all the common dependencies and plugins between the modules by defining
a parent.

Or you can create all the directory structure by yourself:
{% highlight sh %}
.
├── library
|   ├── src
|   |   └── main
|   |       └── java
|   └── pom.xml
├── presenter
|   ├── src
|   |   └── main
|   |       ├── java
|   |       └── resources
|   └── pom.xml
└── scheduler
    ├── src
    |   └── main
    |       ├── java
    |       └── resources
    └── pom.xml
{% endhighlight %}

Then we'll be able to define our modules' `pom.xml` files.

_./library/pom.xml_
{% highlight xml %}
{% include series/GetStartedWithJavaAndSpring/PartI_Maven/library/pom.xml.v1 %}
{% endhighlight %}

_./presenter/pom.xml_
{% highlight xml %}
{% include series/GetStartedWithJavaAndSpring/PartI_Maven/presenter/pom.xml.v1 %}
{% endhighlight %}

_./scheduler/pom.xml_
{% highlight xml %}
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <parent>
        <groupId>com.company</groupId>
        <artifactId>tube</artifactId>
        <version>1.0-SNAPSHOT</version>
    </parent>

    <groupId>com.company</groupId>
    <artifactId>scheduler</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>jar</packaging>
</project>
{% endhighlight %}

#### Dependency management
Now we need our Presenter and Scheduler to be dependent on Library module and
[Spring Boot](https://projects.spring.io/spring-boot/).

We'll just kickstart our whole project under Spring Boot parent like this (we're using the latest version here but you
can take whichever you want [here](https://projects.spring.io/spring-boot/#quick-start)):

_./pom.xml_
{% highlight xml %}
<project …>
    …

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.0.0.M5</version>
    </parent>

    <repositories>
        <repository>
            <id>spring-milestones</id>
            <name>Spring Milestones</name>
            <url>https://repo.spring.io/libs-milestone</url>
            <snapshots>
                <enabled>false</enabled>
            </snapshots>
        </repository>
    </repositories>
</project>
{% endhighlight %}

Now all our modules will be packed with brand new Spring Boot Framework inside. 

We also need to accompany our modules with database interaction ability so we include the Spring Boot Data JPA starter
module.

_./pom.xml_
{% highlight xml %}
<project …>
    …

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
        </dependency>
    </dependencies>
</project>
{% endhighlight %}

Now we're ready to get started with database interaction which we'll cover in [next chapter]({{ series_next_article.url | relative_url }}) of this guide.
