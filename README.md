# devops-demo-app

The main purpose of this one project is provide wide opportunities to test various actions and technologies in DevOps practice.
This is DevOps sandbox where you can play with testing, development, building and deployment of applications/libraries written in various program languages.

Have fun! :)

## Application

Simplest JS application to show greeting in a browser - devops-demo-app (dda).
Current implementation includes only frontend part and consist of HTML- and JS-code runs on Nginx server.

## Build process

To dokerize the greeting JS application execute the below comand:

```shell
docker build --tag=devops-demo-app-frontend -f docker/Dockerfile .
```

To run dokerized the greeting JS application use the following comand:

```shell
docker run -de -p 5001:80 --name=dda-frontend devops-demo-app-frontend
```
