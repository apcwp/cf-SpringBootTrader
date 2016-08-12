
# cf-SpringBootTrader

Microservice version of the Spring Trader app using spring boot

![Spring Trader](/docs/springtrader2.png)

#Introduction

This repository holds a collection of micro services that work together to present a trading application surfaced though a web UI, but more interfaces can be created that re-utilise the microservices.

It was created to support workshops and demonstrations of building and using `microservices` architectures and running these in **Cloud Foundry** (although it is possible to run these on other runtimes).

The workshops follow a series of exercises, or labs, and you can find links to the guides for these exercises [below](#workshops).

##Table of Contents

1. [Architecture](#architecture)
2. [Deploying the application](#deployment)
3. [Workshops](#workshops)



#Architecture
The system is composed of 4 microservices. The relationship between the microservices is illustrated below.

![architecture](/docs/microservices_relationship.png)

##1. Quote Microservice
This service is a spring boot application responsible for providing up to date company and ticker/quote information. It does this by providing a REST api with 2 calls:
* ``/quotes?q={symbols}``
Returns an up to date quote for each symbol in the comma-delimited list.
* ``/company/{search}``
Returns a list of companies that have the search parameter in their names or symbols.

This application has no dependencies apart from an external service - [markitondemand](http://dev.markitondemand.com/) - to retrieve the real time data.

##2. Account Microservice
This service is a spring boot application responsible for creating and managing user accounts.

It stores the accounts in a RDBMS store and uses a spring JPA respository to accomplish this. It provides several REST api calls for other services to consume its services.

##3. Portfolio Microservice
This service is a spring boot application responsible for managing portfolios - these are collections of holdings, which in turn are collection of orders on a particular share.

This service accepts orders (both BUY and SELL) and stores these in a RDBMS store - *it does not have to be the same RDBMS as the Account service, but it can be!* It provides REST api calls for other services to consume its services.

This service is dependent on the Account service above to ensure the logged in user has enough funds to buy stock as well as keeping the account funds up to date. It is also dependent on the Quote service to retrieve up to date quote information and calculate the current value of portfolios.

##4. Web Microservice
This service is a spring boot application providing the web interface.

The web interface is built using bootstrap and Thymeleaf and uses a Spring controller to delegate calls to the relevant services:
* Account service
* Quote service
* Portfolio service

#Deployment

To deploy the microservices please follow the guides of the [workshop below](#workshops).

Each guide includes instructions on how to deploy and run to:
  - Pivotal Cloud Foundry with [Spring Cloud Services for PCF](https://network.pivotal.io/products/p-spring-cloud-services) installed.
  - Cloud Foundry without Spring Cloud Services.
  - [Pivotal Web Services](http://run.pivotal.io)
  - local machine.

#Workshops:

The following guides describe how to setup the environment and deploy the microservices to **Cloud Foundry**.

At Pivotal we love education, not just educating ourselves, but also educating others. As such, these guides follow the *"teaching you how to fish"* principle - Rather than giving you line by line/command by command instructions, we provide guidelines and links to documentation where you can read and learn more.

1. [Setting up the environment] [setup]
2. [Creating a discovery service] [registry]
3. [Creating a circuit breaker dashboard] [circuitbreaker]
4. [creating the configuration service][configserver]
5. [Pushing the Quote service] [pushquote]
6. [Pushing all the services] [pushall]
7. [Scaling the services] [scale]
8. [Blue/Green deployments] [bluegreen]


[setup]: docs/lab_setup.md
[registry]: docs/lab_registryserver.md
[circuitbreaker]: docs/lab_circuitbreaker.md
[configserver]: docs/lab_configserver.md
[pushquote]: docs/lab_pushquote.md
[pushall]: docs/lab_pushall.md
[scale]: docs/lab_scale.md
[bluegreen]: docs/lab_bluegreen.md


