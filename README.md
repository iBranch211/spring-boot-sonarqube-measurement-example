# Spring Boot Sonarqube Example
> Spring Boot Sonarqube Example
>
<img src="https://github.com/susimsek/spring-boot-sonarqube-measurement-example/blob/main/images/spring-boot-sonarqube-measurement-example.png" alt="Spring Boot Sonarqube Example" width="100%" height="100%"/> 

## Sonarqube Docker Compose Installation

At the root of your project, please run

```sh
docker-compose -f sonarqube/docker-compose.yml up -d
```

Change sonarqube admin password

```sh
curl -u admin:admin -X POST "http://localhost:9000/api/users/change_password?login=admin&previousPassword=admin&password=root"
```

Create project in sonarqube with this project key 

```sh
spring-boot-sonarqube-measurement-example
```

## Using Sonar

Edit these properties in json files sonar-project.properties.

```sh
sonar.host.url=http://localhost:9000
sonar.login=admin
sonar.password=root
```


At the root of your project, please run

```sh
./mvnw verify sonar:sonar
```

Once the analysis completes, it will be available on the Sonar dashboard, which by default is available on http://localhost:9000/.

<img src="https://github.com/susimsek/spring-boot-sonarqube-measurement-example/blob/main/images/sonarqube-dashboard.png" alt="Spring Boot Sonarqube Dashboard Example" width="100%" height="100%"/>

## Prerequisites

* Java 11
* Maven 3.3+
* Docker 19.03+
* Docker Compose 1.25+
* Sonarqube


## Installation


```sh
./mvnw compile jib:dockerBuild
```


```sh
docker-compose up -d 
```

## Used Technologies

* Spring Boot 2.5.1
* Spring Boot Web
* Spring Boot Actuator
* Spring Boot Dev tools
* Spring Boot Test
* Properties Maven Plugin
* Sonar Maven Plugin 
* Maven Surefire Plugin
* Jacoco Maven Plugin
* Jib Maven Plugin
* Maven Enforcer Plugin


