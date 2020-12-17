# SpringBoot + Flyway demo
Project, which demonstrate integration between db migration tool Flyway and SpringBoot framework.
 
# Some important parts of demo
## Migrations
Project has two migrations, which are containing in:
`src/main/resources/db.migration` - all migrations, which has project.

**V00001__Create_country_table.sql**
```mysql-sql
CREATE TABLE country (id INT, name VARCHAR(30)); 
```

**V00002__Add_test_data_to_country.sql**
```mysql-sql
-- adding test data
INSERT INTO country VALUES (1, 'Ukraine');
INSERT INTO country VALUES (2, 'Russia');
INSERT INTO country VALUES (3, 'Belorus');
```

## Properties
`src/main/resources/application.properties` - properties with data for connecting to DB.
Here is properties, which are using:
```properties
spring.datasource.url=jdbc:mysql://localhost:3306/flyway_demo_db
spring.datasource.username=root
spring.datasource.password=root
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
```

## Pom.xml
Project object model:
`pom.xml`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.2.11.RELEASE</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>
	<groupId>com.github.javarushcommunity</groupId>
	<artifactId>springboot-flyway-demo</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>SpringBoot + Flyway Demo</name>
	<description>Project demonstrates integration between SpringBoot and Flyway.</description>

	<properties>
		<java.version>1.8</java.version>
	</properties>

	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-jpa</artifactId>
		</dependency>
		<dependency>
			<groupId>org.flywaydb</groupId>
			<artifactId>flyway-core</artifactId>
		</dependency>

		<dependency>
			<groupId>mysql</groupId>
			<artifactId>mysql-connector-java</artifactId>
			<scope>runtime</scope>
		</dependency>
		<dependency>
			<groupId>org.projectlombok</groupId>
			<artifactId>lombok</artifactId>
			<optional>true</optional>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
			<exclusions>
				<exclusion>
					<groupId>org.junit.vintage</groupId>
					<artifactId>junit-vintage-engine</artifactId>
				</exclusion>
			</exclusions>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>

</project>

```

## Main class Application
Main class to run SpringBoot
`src/main/java/com/github/javarushcommunity/springbootflywaydemo.Application` - main class for running SpringBoot application.

```java
package com.github.javarushcommunity.springbootflywaydemo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {

	public static void main(String[] args) {
		SpringApplication.run(Application.class, args);
	}
}
```

