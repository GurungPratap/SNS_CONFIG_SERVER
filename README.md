# SNS_CONFIG_SERVER

SPRING CLOUD CONFIG SERVER implementation for SNS project

The Git-backed configuration API provided by our server can be queried using the following paths:
```shell
/{application}/{profile}[/{label}]
/{application}-{profile}.yml
/{label}/{application}-{profile}.yml
/{application}-{profile}.properties
/{label}/{application}-{profile}.properties
```

By default, the configuration values are read on the client’s startup and not again. You can force a bean to refresh its configuration
(that is, to pull updated values from the Config Server) by annotating the component with the Spring Cloud Config @RefreshScope 
and then triggering a refresh event. 

Also, you must add org.springframework.boot:spring-boot-starter-actuator to the client application’s classpath. 
You can invoke the refresh Actuator endpoint by sending an empty HTTP POST to the client’s refresh endpoint:
```shell
$ curl localhost:8080/actuator/refresh -d {} -H "Content-Type: application/json"
```

In a real microservice environment, there will be a large number of independent application services. 
Therefore is it not practical for the user to manually trigger the refresh event for all the related services whenever a property is changed.

The better approach is to trigger the refresh event for one service and broadcast the event through all other available services.
We can explore a way to trigger the refresh event for only one service and that event is automatically propagated (broadcasted) through all the other services. 
This can be achieved with Spring Cloud Bus.

## To Do: 

* get it working with a webhook on Github 
* Auto Refresh Properties for Clients using  Spring Cloud Config Bus
