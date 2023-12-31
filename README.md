# Kubernetes Cluster set up

## Description

This is the kubernetes cluster set up for the chat application. This cluster will be used to orchestrate the microservices
and deploy them in the cluster.

## Prerequisites

Before setting up the cluster, you will need to run the docker-compose file in the root directory to ensure that all the
services are up and running. You will also need to have a kubernetes cluster up and running. I am using docker desktop
which comes with a kubernetes cluster. If you are using docker desktop, you can enable the kubernetes cluster in the
settings.

If you are using a cloud provider, follow the instructions on their website to set up a kubernetes cluster.
The instructions for setting up the cluster will be different for each cloud provider.


## Steps

Ensure you set up the microservices first before the nginx-ingress-controller.

Each directory has a README.md file that describes how to set it up in the cluster. Follow the instructions in the README.md