# Security Service set up

## Description

This is a simple security service set up for kubernetes cluster. This service will be used to authenticate the users and
authorize the users to access the resources in the cluster. This service will also be used to generate the jwt tokens
for the users. The code can be found in the following git repository [security-service](https://github.com/chat-microservices-app/security-service)


## Prerequisites

Before setting up the security-service, you need to have a kubernetes cluster up and running. Additionally,
you need to ensure that you have run the docker-compose file in the root directory and the services described in there
are up and running correctly.

## Steps

Once you have the cluster up and running and ensure the services are running,
you can then deploy the security-service with the following command

    kubectl apply -f security-service.deployment.yaml

This will deploy the security-service in the cluster. Once the service is deployed you can
then expose the service in the cluster with the following command

    kubectl apply -f security-service.yaml

The app should be up and running now, and the service should be exposed in the cluster. You can check the status
of the service with the following command

    kubectl get svc security-service

You can also check the logs of the service with the following command
    
        kubectl logs -l app=security-service

This command will get all replicas of the security-service and print the logs of all the replicas. If you want to get the logs
of a specific replica, you can use the following command

        kubectl logs security-service-<generated-id>
