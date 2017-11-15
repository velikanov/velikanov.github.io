---
layout: post
title: "Get started with Java and Spring"
subtitle: "Part I. Maven"
series: get_started_with_java_and_spring
goal: "Bootstrap a new modular project with Maven"
repo_link: "https://github.com/velikanov/tube/tree/part1_maven"
date: 2017-10-12 18:47:27 +0300
tags:
- java
- spring
---
## Part I. Maven

{% include sources.html %}

{% include series.html %}

### Introduction
[Apache Maven](https://maven.apache.org/) is not just a dependency manager (like PHP's 
[Composer](https://getcomposer.org/) is) but a full stack project management solution which helps you to bootstrap 
your application using all the dependencies needed, build it and deploy.

<!--more-->

### Action
#### Creating a project
Let's start with creating a new Maven project with `File → New → Project…`

Find and select project category Maven and choose your project SDK (for now it's 1.8).
If you haven't any then you need to install JDK e.g. from 
[Oracle official website](http://www.oracle.com/technetwork/java/javase/downloads/index.html). 

For now we won't create our application from any
[archetype](https://maven.apache.org/guides/introduction/introduction-to-archetypes.html). Click `Next`.

![Creating a project. Step 1]({{ images_path }}/Action/CreatingAProject/Step1.png)

Now we need to enter our company name (called GroupId) e.g. `com.company` and application name (called ArtifactId) e.g.
`tube`. We'll leave the version as it is.

![Creating a project. Step 2]({{ images_path }}/Action/CreatingAProject/Step2.png)

Then we choose the location of our project and finally we can start.

![Creating a project. Step 3]({{ images_path }}/Action/CreatingAProject/Step3.png)

#### Working with Maven
After the project creation you'll be asked to Auto-Import all the Maven dependencies.

I prefer to do this, because if you do so then you won't need to reimport projects manually after any dependency
updates in your [POM file](https://maven.apache.org/guides/introduction/introduction-to-the-pom.html).

You can enable Auto-Import later in IntelliJ IDEA Preferences: `Build, Execution, Deployment → Build Tools → Maven →
Importing` and checking the `Import Maven projects automatically` box.

![Working with Maven. Import Maven projects automatically]({{ images_path }}/Action/WorkingWithMaven/ImportMavenProjectsAutomatically.png)

We'll start with three submodules in our project:
* `Library` - the main entity and repository storage.
* `Presenter` - our web frontend.
* `Scheduler` - the data handler.

Now we have to write modules definition (under `<modules>` section) in our root `pom.xml`:

{% highlight xml linenos %}
{% include {{ sources_path }}/pom.xml.v1 %}
{% endhighlight %}

Then we can bootstrap all our modules using IntelliJ IDEA's intentions.

Choose `Create Module with parent` to share all the common dependencies and plugins between the modules by defining
a parent.

Or you can create all the directory structure by yourself:
{% highlight sh %}
{% include {{ sources_path }}/directory_structure.v1 %}
{% endhighlight %}

Be sure to mark all `src/main/java` directories as `Sources Root` (call context menu on `java` directory and select
`Mark Directory as → Sources Root`) and all `src/main/resources` as `Resources Root` respectively.

![Working with Maven. Mark Directory as]({{ images_path }}/Action/WorkingWithMaven/MarkDirectoryAs.jpg){: .nofullwidth }

Then we'll be able to define our modules' `pom.xml` files.

<code>./library/pom.xml</code>
{% highlight xml linenos %}
{% include {{ sources_path }}/library/pom.xml.v1 %}
{% endhighlight %}

<code>./presenter/pom.xml</code>
{% highlight xml linenos %}
{% include {{ sources_path }}/presenter/pom.xml.v1 %}
{% endhighlight %}

<code>./scheduler/pom.xml</code>
{% highlight xml linenos %}
{% include {{ sources_path }}/scheduler/pom.xml.v1 %}
{% endhighlight %}

#### Dependency management
Now we need our Presenter and Scheduler to be dependent on Library module and
[Spring Boot](https://projects.spring.io/spring-boot/).

<code>./presenter/pom.xml</code>
{% highlight xml linenos %}
{% include {{ sources_path }}/presenter/pom.xml.v2 %}
{% endhighlight %}

<code>./scheduler/pom.xml</code>
{% highlight xml linenos %}
{% include {{ sources_path }}/scheduler/pom.xml.v2 %}
{% endhighlight %}

Then we'll just kickstart our whole project under Spring Boot parent. We're using the latest version here but you can
take whichever you want [here](https://projects.spring.io/spring-boot/#quick-start).

<code>./pom.xml</code>
{% highlight xml linenos %}
{% include {{ sources_path }}/pom.xml.v2 %}
{% endhighlight %}

Now all our modules will be packed with brand new Spring Boot Framework inside. 

We also need to accompany our modules with database interaction ability so we include the Spring Boot Data JPA starter
module.

<code>./pom.xml</code>
{% highlight xml linenos %}
{% include {{ sources_path }}/pom.xml.v3 %}
{% endhighlight %}

Now we're ready to get started with database interaction which we'll cover in
[next chapter]({{ series_next_article.url | relative_url }}) of this guide.

{% include sources.html %}
