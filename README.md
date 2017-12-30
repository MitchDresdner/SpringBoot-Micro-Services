#  Spring Cloud Microservices with Spring Boot

Based on lessons from [Ranga Rao Karanam's Udemy Course](https://www.udemy.com/microservices-with-spring-boot-and-spring-cloud/learn/v4/overview): Master Microservices with Spring Boot and Spring Cloud

Template cloud ready microservices using Spring Cloud

Base-Services: 
![alt text](https://github.com/MitchDresdner/SpringBoot-Micro-Services/blob/api-gateway/images/BaseServices.png "Currency conversion services")

These basic projects demonstrate
- Communications between Microservices
- Centralized Microservice Configuration with Spring Cloud Config Server
- Spring Cloud Bus to exchange messages about Configuration updates
- Simplified communication with other Microservices using Feign REST Client
- Client side load balancing with Ribbon
- Dynamic scaling using Ribbon and Eureka Naming Server
- API Gateway with Zuul
- Distributed tracing with Spring Cloud Sleuth and Zipkin
- Fault Tolerance with Zipkin

## Ports

|     Application       |     Port          |
| ------------- | ------------- |
| Limits Service | 8080, 8081, ... |
| Spring Cloud Config Server | 8888 |
|  |  |
| Currency Exchange Service | 8000, 8001, 8002, ..  |
| Currency Conversion Service | 8100, 8101, 8102, ... |
| Netflix Eureka Naming Server | 8761 |
| Netflix Zuul API Gateway Server | 8765 |
| Zipkin Distributed Tracing Server | 9411 |


## URLs

|     Application       |     URL          |
| ------------- | ------------- |
| Limits Service | http://localhost:8080/limits POST -> http://localhost:8080/application/refresh|
|Spring Cloud Config Server| http://localhost:8888/limits-service/default http://localhost:8888/limits-service/dev |
|  Currency Converter Service - Direct Call| http://localhost:8100/currency-converter/from/USD/to/INR/quantity/10|
|  Currency Converter Service - Feign| http://localhost:8100/currency-converter-feign/from/EUR/to/INR/quantity/10000|
| Currency Exchange Service | http://localhost:8000/currency-exchange/from/EUR/to/INR http://localhost:8001/currency-exchange/from/USD/to/INR|
| Eureka | http://localhost:8761/|
| Zuul - Currency Exchange & Exchange Services | http://localhost:8765/currency-exchange-service/currency-exchange/from/EUR/to/INR http://localhost:8765/currency-conversion-service/currency-converter-feign/from/USD/to/INR/quantity/10|
| Zipkin | http://localhost:9411/zipkin/ |
| Spring Cloud Bus Refresh | http://localhost:8080/bus/refresh |

## VM Argument

-Dserver.port=8001

### Workarounds as-of 30 Dec 2017
Feign throws Decode exception in M7, falling back to M3 to get support
``` 
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.0.0.M3</version>	<!-- M7 -->
		<relativePath/>
	</parent>
```