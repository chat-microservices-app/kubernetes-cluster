# Media Service Set-up


## Description

Media service is a microservice that is used to handle the media related logic in the chat app
such as uploading a new media file, getting the media file, etc. The code can be found in the following git repository
[media-service](https://github.com/chat-microservices-app/media-service)
## Prerequisites

Before setting up the media-service, you need to have a kubernetes cluster up and running. Additionally,
you need to ensure that you have run the docker-compose file in the root directory and the services described in there
are up and running correctly.

This service utilizes a cloud storage service (aws and S3 buckets) to store the media files. Therefore,
you will need to set up the aws credentials in each of the pods that will be running the media-service.

I have created a secret in the cluster call aws-credentials that will be used to
store the aws credentials, however due to security reasons, I have not included the credentials in the repository.
Therefore, you will need to create the secret in the cluster with the following command and add the credentials in
there.

    kubectl apply -f name-of-the-secret-file.yaml

Alternatively, you can run a command and not have your credentials store in a file.

    kubectl create secret generic aws-credentials \
    --from-literal=aws_access_key_id=<your-access-key-id> \
    --from-literal=aws_secret_access_key=<your-secret-access-key> 

Notice that the secret name is aws-credentials, and the data names are also those names.
The reason for this is that in the deployment, I have set it up so that it will look for the secret with the name aws-credentials
and look at those specific names to set up the credentials. If you change the names make sure they match
to the names in the deployment file.

## Steps

Once you have the cluster up and running and ensure the services are running, deploy the secrets
with the following command

Ensure the secrets are deployed correctly, and then deploy the media-service with the following command

    kubectl apply -f media-service-deployment.yaml

You can then deploy the service to expose the pod to the internal cluster with the following command

    kubectl apply -f media-service.yaml

The service should be up and running now, and you can check the status of the service with the following command

    kubectl get svc media-service

You can also check the logs of the service with the following command

    kubectl logs -l app=media-service

This command will get all replicas of the media-service and print 
the logs of all the replicas. If you want to get the logs
of a specific replica, you can use the following command

    kubectl logs media-service-<generated-id>


