# Clean way to validate business rules in Microservices

Blog: <https://bhuwanupadhyay/blog/clean-way-to-validate-business-rules-in-microservices/>

## Walkthrough

### Create a reactive Spring Boot application

To create a reactive Spring Boot application, we'll use [Spring Initializr](https://start.spring.io/). 
The application that we'll create uses: 

`Spring Boot 2.3.1.RELEASE` `Java 14` `Spring WebFlux` `Spring Data R2DBC`

#### Generate the application by using Spring Initializr
```shell
NAME='Clean way to validate business rules in Microservices' && \
PRJ=clean-way-to-validate-business-rules-in-microservices && \
cd "$HOME/BhuwanUpadhyay/lab" && mkdir -p $PRJ && cd $PRJ && \
curl https://start.spring.io/starter.tgz \
    -d dependencies=actuator,webflux,data-r2dbc \
    -d groupId=io.github.bhuwanupadhyay -d artifactId=$PRJ -d packageName=io.github.bhuwanupadhyay.example \
    -d applicationName=SpringBoot -d name="$NAME" -d description="$NAME" \
    -d language=java -d platformVersion=2.3.1.RELEASE -d javaVersion=14 \
    -o demo.tgz && tar -xzvf demo.tgz && rm -rf demo.tgz
```

#### Add the reactive PostgreSQL and H2 driver implementation

Open the generated project's pom.xml file, and then add the reactive PostgreSQL and H2 driver after the `spring-boot-starter-webflux` dependency, add the following text:

```xml
<dependency>
  <groupId>io.r2dbc</groupId>
  <artifactId>r2dbc-h2</artifactId>
  <scope>runtime</scope>
</dependency>
<dependency>
  <groupId>io.r2dbc</groupId>
  <artifactId>r2dbc-postgresql</artifactId>
  <scope>runtime</scope>
</dependency>
```

#### Configure Spring Boot to use Database for PostgreSQL and H2

Rename the `application.properties` file to `application.yaml`, and add the following text:

```yaml
logging:
  level:
    org.springframework.data.r2dbc: DEBUG
spring:
  profiles:
    active: h2
---
spring:
  profiles: h2
---
spring:
  profiles: postgresql
  r2dbc:
    password: password
    url: r2dbc:pool:postgres://localhost:5432/demo
    username: user
```

### Create the database schema