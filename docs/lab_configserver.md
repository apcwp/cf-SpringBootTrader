# Creating the Configuration service.

All our microservices will retrieve their configuration from a Configuration service. We will use the Configuration service provided by the [Spring Cloud Services for PCF](https://network.pivotal.io/products/p-spring-cloud-services) 

Underneath the covers, this discovery service is implemented using the [Spring Cloud Config](http://cloud.spring.io/spring-cloud-config/).

### Exercise

1. Log in to the Apps Manager through your browser. The URL will be: `https://console.<your_cloud_foundry_url>/`

Go the *Marketplace* and choose a *Config Server for Pivotal Cloud Foundry*.

When prompted for the name of the service, insert **"config-server"** and bind it to the space you are using to deploy your applications.

> You can pick any name of the service, however, the service is already specified in the manifest files, so it is easier to re-use that name. If you do modify the name, ensure you modify it in the manifest files as well.

2. Click on *Manage* for the service you created to open the service dashboard. It will prompt you to enter either a Git or Subversion URI. Choose Git and enter **https://github.com/dpinto-pivotal/cf-SpringBootTrader-config.git** as the URI.



You can now move on to [pushing the quote service](lab_pushquote.md)
