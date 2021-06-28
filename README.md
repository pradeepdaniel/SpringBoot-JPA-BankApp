# Sample Banking Application using Java 11 or greater, Spring Boot, Oracle cloud & JPA

RESTful API to simulate simple banking operations to learn Spring, JPA & Oracle Cloud. 

This application uses Oracle in cloud.oracle.com as the Database and hence the JARS and configurations.

## Requirements

*	CRUD operations for customers and accounts.
*	Support deposits and withdrawals on accounts.
*	Internal transfer support (i.e. a customer may transfer funds from one account to another).


## Getting Started

1. Checkout the project from GitHub

```
git clone https://github.com/pradeepdaniel/Spring-JPA-BankApp

```
2. Enable Lombok support on your IDE

Refer to the following link for instructions:

```
https://projectlombok.org/setup/eclipse

```
3. Open IDE of your choice and Import as existing maven project in your workspace

```
- Import existing maven project
- Run mvn clean install
- If using STS, Run As Spring Boot App

```
4. Default port for the api is 8034


### Prerequisites

* Java 11 or higher
* Spring Tool Suite 4 or similar IDE
* [Maven](https://maven.apache.org/) - Dependency Management

Oracle Maven dependencies can be installed manually since they are not available in Maven repository due to licensing restrictions

The Oracle JDBC JAr can be downloaded from https://www.oracle.com/database/technologies/appdev/jdbc-ucp-183-downloads.html

> mvn install:install-file -Dfile=<JAR PATH>/ojdbc8.jar -DgroupId=com.oracle.jdbc -DartifactId=ojdbc8 -Dversion=18.3.0.0 -Dpackaging=jar
> mvn install:install-file -Dfile=<JAR PATH>/upc.jar -DgroupId=com.oracle.jdbc -DartifactId=upc -Dversion=18.3.0.0 -Dpackaging=jar
> mvn install:install-file -Dfile=<JAR PATH>/ons.jar -DgroupId=com.oracle.jdbc -DartifactId=ons -Dversion=18.3.0.0 -Dpackaging=jar
> mvn install:install-file -Dfile=<JAR PATH>/oraclepki.jar -DgroupId=com.oracle.jdbc -DartifactId=oraclepki -Dversion=18.3.0.0 -Dpackaging=jar
> mvn install:install-file -Dfile=<JAR PATH>/osdt_cert.jar -DgroupId=com.oracle.jdbc -DartifactId=osdt_cert -Dversion=18.3.0.0 -Dpackaging=jar
> mvn install:install-file -Dfile=<JAR PATH>/osdt_core.jar -DgroupId=com.oracle.jdbc -DartifactId=osdt_core -Dversion=18.3.0.0 -Dpackaging=jar

If you are using oracle cloud DB please follow the below link to download the wallet and other config
https://docs.oracle.com/en/cloud/paas/autonomous-database/adbsa/connect-jdbc-thin-wallet.html#GUID-EBBB5D6B-118D-48BD-8D68-A3954EC92D2B

### Maven Dependencies

```
spring-boot-starter-actuator
spring-boot-starter-data-jpa
spring-boot-starter-security
spring-boot-starter-web
spring-boot-devtools
lombok - to reduce boilerplate code
springfox-swagger2
springfox-swagger-ui
spring-boot-starter-test
spring-security-test
Oracle JDBC & UPC
```

## Swagger

Please find the Rest API documentation in the below url

```
http://localhost:8034/bankapp/swagger-ui.html

```
# This project by default uses Oracle cloud Autonomous database so it uses the below JARS
ojdbc8
upc
ons
oraclepki
osdt_cert
osdt_core

The connection URL will look like below unlike the traditional
jdbc:oracle:thin:@<DB Name>_high?TNS_ADMIN=/Users/<username>/wallet/wallet_<DB NAME>/

To get this working need to change this to regular URL if connecting to local (on  non cloud) oracle

#Disable the CORS
I had challenges in doing POST REST calls to disable the CORS in the SpringBootSecurityConfiguration
http.csrf().disable();

## Testing the Rest Api

1. Please use the Swagger url to perform CRUD operations. 

http://localhost:8034/bankapp/accounts/add/456654
```
{
"accountBalance": 450000000,
"accountCreated": "2021-06-26T17:17:23.000Z",
"accountNumber": 34000001,
"accountStatus": "ACTIVE",
"accountType": "SAVINGS",
"bankInformation": {
"branchAddress": {
"address1": "LANE 1",
"address2": "LANE 2",
"city": "New City",
"country": "New Conutry",
"state": "NEW",
"zip": "6DFT45"
},
"branchCode": 12323,
"branchName": "NYB",
"routingNumber": 3242
}
}
```
http://localhost:8034/bankapp/customers/234324
```
{
  "contactDetails": {
    "emailId": "name@gmail.com",
    "homePhone": "1000200030",
    "workPhone": "4000500060"
  },
  "customerAddress": {
    "address1": "address1",
    "address2": "address2",
    "city": "city",
    "country": "country",
    "state": "state",
    "zip": "234234"
  },
  "customerNumber": 234324,
  "firstName": "firstName",
  "lastName": "lastName",
  "middleName": "middleName",
  "status": "ACTIVE"
}

```
Taken the base code from https://github.com/sbathina/BankApp 
and made changes to work with Oracle Cloud and Security