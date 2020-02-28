Apache Ignite Deployment on EKS
===============================

This repository contains configuration files that can be used to deploy an Apache Ignite cluster with Native Persistence within EKS environment.

Below are the steps required to recreate a deployment presented during a live demo here: https://www.gridgain.com/resources/webinars/how-apache-ignite-deployments-in-kubernetes

Cluster Deployment
------------------

Step 1: Create namespace

    kubectl create namespace ignite

Step 2: Create service

    kubectl create -f service.yaml

Step 3: Create service account

    kubectl create sa ignite -n ignite

Step 4: Create cluster role

    kubectl create -f cluster-role.yaml

Step 5: Create config map

    kubectl create configmap ignite-config -n ignite --from-file=node-configuration.xml

Step 6: Create stateful set

    kubectl create -f stateful-set.yaml

Step 7: Check that nodes successfully started and formed a topology

    kubectl get pods -n ignite
    kubectl logs ignite-cluster-0 -n ignite
    kubectl logs ignite-cluster-1 -n ignite
  

Web Agent Deployment
--------------------

Step 1: Get service DNS name

    kubectl describe service ignite-service -n ignite

Step 2: Login to the Web Console and acquire security token

Step 3: Update `NODE_URI` and `TOKENS` variables in web-agent.yaml

Step 4: Create Web Agent deployment

    kubectl create -f web-agent.yaml
