# Service Discovery using HashiCorp Consul

This is Service Discovery (SD) test to illustrate how HashiCorp Consul works.

The test stage contains the following nodes:

- Consul server (SD server)
- Fabio (Load balancer)
- Web #1 (test nore #1)
- Web #2 (test nore #2)

## Build the test stage

To build the SD test stage please navigate to `deploy/sd` directory of the project and execute the following command:

```shell
docker-compose build
```

## Start the test stage

To start services (docker containers) of the SD test stage please navigate to `deploy/sd` directory of the project and execute the below command:

```shell
docker-compose up
```

After starting of the all four containers you'll be able to open the following pages in a browser:

- HashiCorp Consul Web UI: <http://33.10.0.2:8500/ui>
    Navigate on `Services` and `Nodes` tabs to review information about started nodes
- Fabio Web UI: <http://33.10.0.100:9998/routes>
    Here you can check nodes registered in LB
- Fabio LB URL for Web nodes: <http://33.10.0.100:9999/>
    Navigates on one of registered Web nodes.
- Direct URL on Web node #1: <http://33.10.0.11:80>  or  <http://localhost:8081>
- Direct URL on Web node #2: <http://33.10.0.12:80>  or  <http://localhost:8082>

## Test of Load Balancing and Service Discovery

As already mentioned above, the test SD stage contains two targer Web nodes to test load balancing using Fabio LB.
You can open <http://33.10.0.100:9999/> URL and refresh the page few times (Ctrl + F5) - and you should be able see that the page provides by different Web node each time. Because these nodes have been regester initially (during the stage start) using Consul's client config.

Now imagine that we need to add a couple of additional Web nodes to handle raised load.
For that we can use even not `docker-compose` commands, for example:

```shell
docker run -d --network=sd_consul_network --ip="33.10.0.13" -p 8083:80 --env NODE=web_3 --env PRIVATE_IP_ADDRESS=33.10.0.13 --env LOAD_BALANCER=33.10.0.100 web_consul:latest
```

and

```shell
docker run -d --network=sd_consul_network --ip="33.10.0.14" -p 8084:80 --env NODE=web_4 --env PRIVATE_IP_ADDRESS=33.10.0.14 --env LOAD_BALANCER=33.10.0.100 web_consul:latest
```

After execution of them, new two Web nodes will appear in Consul and Fabio automatically. And as a result, the load will be distributed among all four nodes.
