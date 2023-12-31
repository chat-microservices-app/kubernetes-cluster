# user management set up

## Description

This is a user management set up for kubernetes cluster. This service will be used to create new users, store their information
update the other microservices that need the user information etc. The code can be found in the following git repository [user-management](https://github.com/chat-microservices-app/user-management-service)


## Prerequisites

Before setting up the user-management-service, you need to have a kubernetes cluster up and running. Additionally,
you need to ensure that you have run the docker-compose file in the root directory and the services described in there
are up and running correctly.

If the database is missing the credentials, that means you will need to set up the database as well with
the tables and the credentials. TODO: add the database set up instructions here or volume.


## Steps

Once you have the cluster up and running and ensure the services are running, deploy the secrets
with the following command

    kubectl apply -f user-management-secrets.yaml

Ensure the secrets are deployed correctly, and then deploy the user-management-service with the following command

    kubectl apply -f user-management-deployment.yaml

This will deploy the user-management-service in the cluster. Once the service is deployed, you can then expose the 
service in the cluster with the following command

    kubectl apply -f user-management-service.yaml

The app should be up and running now, and the service should be exposed in the cluster. You can check the status
of the service with the following command

    kubectl get svc user-management-service

You can also check the logs of the service with the following command

        kubectl logs -l app=user-management-service

This command will get all replicas of the user-management-service and print the logs of all the replicas. If you want to get the logs
of a specific replica, you can use the following command

        kubectl logs user-management-service-<generated-id>