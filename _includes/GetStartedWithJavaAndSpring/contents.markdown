This article is designed mostly for computer engineers with non-Java/Spring programming background who want to get
started with new technology fast and flawlessly.

Though it doesn’t cover most valuable principles in deployment, migrating and development, it can be used as good
introductory view on new technology.

I won’t explain every step of this guide but will try to serve you with valuable links where you would get much more
information.

What you’ll learn here:
* bootstrap a new modular project with Maven
* build our modules with Spring Boot as a core foundation
* define all the needed entities and repositories
* using Liquibase for database migrations
* setting and getting fast data with Spring Redis (using Jedis, yes, the library for Redis)
* managing containers in every environment painlessly with Docker
* deploying the application using Ansible, Ansible Vault and… the Makefile
* render view layer of your application with Thymeleaf templating engine
* make your work seamless using recipes for IntelliJ IDEA

Throughout our journey we’ll build a simple Tube application which will crawl some videos from another website and
present it on our website.