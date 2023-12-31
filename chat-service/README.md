# chat-service set up
 
## Description

chat-service is a microservice that is used to handle the chat related logic in the chat app
such as creating a new chat room, sending messages to a chat room, getting the messages, etc. 
The code can be found in the following git repository [chat-service](https://github.com/chat-microservices-app/chat-service)


## Prerequisites

Before setting up the chat-service, you need to have a kubernetes cluster up and running. Additionally,
you need to ensure that you have run the docker-compose file in the root directory and the services described in there
are up and running correctly. 

If the database is missing the credentials, that means you will need to set up the database as well with
the tables and the credentials. TODO: add the database set up instructions here.


## Steps

Once you have the cluster up and running and ensure the services are running, deploy the secrets
with the following command

    kubectl apply -f chat-service.secrets.yaml

Ensure the secrets are deployed correctly, and then deploy the chat application with the following command

    kubectl apply -f chat-service.deployment.yaml

This will deploy the chat-service in the cluster. Once the service is deployed, you can check the status of the
service with the following command

    kubectl get pod chat-service

Deploy the service as well to expose the service in the cluster with the following command

    kubectl apply -f chat-service.service.yaml

The app should be up and running now, and the service should be exposed in the cluster. You can check the status

    kubectl get svc chat-service

You can also check the logs of the service with the following command

        kubectl logs -l app=chat-service

This command will get all replicas of the chat-service and print the logs of all the replicas. If you want to get the logs
of a specific replica, you can use the following command

        kubectl logs chat-service-<generated-id>