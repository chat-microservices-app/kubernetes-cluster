# nginx controller set up

# DESCRIPTION

This is a simple nginx controller set up for kubernetes cluster. This controller will be used to route traffic to the
internal backend services running on pods based on the pod name. Ensure all microservices
are deployed and exposed to the cluster before you deploy the nginx controller.

# PREREQUISITES

Before you deploy the nginx controller, you need to have a kubernetes cluster up and
running. Additionally, you need to download the nginx ingress controller image from git
and deploy it in the cluster.

## STEPS

deploy the nginx ingress controller image in the cluster with the following command

    
    kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.8.1/deploy/static/provider/cloud/deploy.yaml
    

Once the controller is deployed, it will create a new namespace called ingress-nginx. Whenever you
want to check the status of the controller, you can use the following command

    kubectl get pods -n ingress-nginx

Ensure that the controller is up and running before you proceed to the next step. Once the controller
is up and running, you can deploy the nginx controller with the following command

    kubectl apply -f nginx-controller.deployment.yaml

this will set up the paths, rules and the host name for the nginx controller that will be used to expose
the internal services to the world. Once the controller is deployed, you can check the status of the
controller with the following command

    kubectl get pod nginx-controller

Deploy the service as well to expose the controller to the world with the following command

    kubectl apply -f nginx-controller.service.yaml

Once the service is deployed, if you are running the cluster in your host machine you will have to port forward the
service to the localhost with the following command

        kubectl port-forward svc/nginx-controller 443

Now you should be able to access the controller from the browser with the following url if you
have the cluster running in your host machine and have set up your network to route the traffic
from localhost to chatapp.com

        https://chatapp.com

In a cloud environment you will have to expose the service with a load balancer, and then you can
access the controller with the load balancer url.

