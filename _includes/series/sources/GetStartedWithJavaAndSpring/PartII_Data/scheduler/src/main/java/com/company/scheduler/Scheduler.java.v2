package com.company.scheduler;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.boot.autoconfigure.domain.EntityScan;
import org.springframework.data.jpa.repository.config.EnableJpaRepositories;

@SpringBootApplication
@EntityScan("com.company.library")
@EnableJpaRepositories("com.company.library")
public class Scheduler {
    public static void main(String[] args) {
        SpringApplication.run(Scheduler.class, args);
    }
}