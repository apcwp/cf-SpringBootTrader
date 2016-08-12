# Creating the Configuration service.

All our microservices will retrieve their configuration from a Configuration service. We will use the Configuration service provided by the [Spring Cloud Services for PCF](https://network.pivotal.io/products/p-spring-cloud-services) 

Underneath the covers, this discovery service is implemented using the [Spring Cloud Config](http://cloud.spring.io/spring-cloud-config/).

### Exercise

1. Log in to the Apps Manager through your browser. The URL will be: `https://console.<your_cloud_foundry_url>/` 

Go the *Marketplace* and choose a *Config Server for Pivotal Cloud Foundry*.

When prompted for the name of the service, insert **"config-server"** and bind it to the space you are using to deploy your applications.

> You can pick any name of the service, however, the service is already specified in the manifest files, so it is easier to re-use that name. If you do modify the name, ensure you modify it in the manifest files as well.


2. To set up Configuration Service we need to provide it with a Git or Subversion repo where the configuration for your projects will be store. For this exercise we'll use Git repo and we'll do it via cli to demonstrate configuring services via CLI.

3. First clone the Git repo so that you can make changes to it, if you wish so 
  ```
  $ git clone https://github.com/hpejcinovic-pivotal/cf-SpringBootTrader-config.git
  ```  
4. Then configure the Config Server with the of the Git repo (make sure that in the uri bellow, you put the name of your repo)
  ```
 $ cf services 
  
 $ cf update-service config-server -c '{"git": { "uri": "https://github.com/hpejcinovic-pivotal/cf-SpringBootTrader-config"}}'
Updating service instance config-server as hpejcinovic@pivotal.io...
OK
  ```


You can now move on to [pushing the quote service](lab_pushquote.md)
