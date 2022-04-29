# Deployment of WebLogic Domain to the Oracle Container Engine for Kubernetes (OKE) on Oracle Cloud Infrastructure (OCI) From WebLogic Kubernetes Toolkit UI

## Introduction

In this lab, we deploy the WebLogic Domain to kubernetes cluster. In primary image section, we specify the oracle account credential. In auxiliary image section, we specify oracle cloud account credential. Here we also specify the replica for the cluster.

### Objectives

In this lab, you will:

* Deploy the WebLogic Domain to Kubernetes Cluster.

### Prerequisites

* You should have a text editor.

## Task 1: Deploy the WebLogic Domain to the Oracle Kubernetes Cluster

In this task, we deploy the Kubernetes custom resource for the WebLogic domain to Kubernetes Cluster.

1. Scroll down, enter the following in Primary Image section, Enter  Oracle account username and password in *Image Registry Pull Username* and *Image Registry Pull Password* respectively. Enter your Oracle email id in *Image Registry Pull Email Address*. These are the same credential which you used to accept license for *weblogic* images in Oracle Container Registry.
    ![Primary Image Details](images/46.png)
    > **For your information only:**<br>
    > We are pulling the image from the Oracle Container Registry, so we are specifying the credential, which we used to accept the license agreement for WebLogic Server Images.


3. Scroll down, enter the following in Auxiliary Image section, from text file copy and paste *Image Registry Username* and *OCI Auth Token* in *Image Registry Pull Username* and *Image Registry Pull Password* respectively. Enter your Cloud email id in *Image Registry Pull Email Address*. These are the same credential which you used to push Auxiliary images in Oracle Cloud Container Image Registry.
    ![Auxiliary Image Details](images/47.png)

4.  In *Clusters* section, click on *Edit* icon as shown.
    ![Cluster Resize](images/48.png)

5. Enter *2* as *Replicas* and then Click *OK*. The size of replica decides the number of managed server in the *Running* state after successfull deployment of WebLogic Domain to Kubernetes cluster.
    ![Cluster Replicas](images/49.png)

6. In Datasources section, double click to edit *passwords* for two datasource. You can give *tiger* as password in both the datasources. Once done, click *Deploy Domain*.
    ![Datasoure Password](images/50.png)
    > This deploy WebLogic Domain test-domain to Kubernetes namespace *test-domain-ns*.

7. Once you see *WebLogic Domain Deployment to Kubernetes Complete* window, Click *OK*.
    ![Deployment Complete](images/51.png)

8. Go back to terminal, Click *Activities* and select the *Terminal* window. Copy the following command and paste it terminal. You should see the similar output, where pod for introspector run first then for the Admin Server and later pods for managed server goes in the *Running* state.

    ````bash
    <copy>kubectl get pods -n test-domain-ns -w</copy>
    ````

    ![Pod Status](images/52.png)
    > Leave this command to run as it is. we will monitor output of it.

9. You can also get the domain status through *WebLogic Kubernetes Toolkit UI*. Go back to *WebLogic Kubernetes Toolkit UI* and click *Get Domain Status*. In Domain Status window, Scroll down to see status of all server pods then click *OK*.
    ![Domain Status](images/53.png)


## Acknowledgements

* **Author** -  Ankit Pandey
* **Contributors** - Maciej Gruszka, Sid Joshi
* **Last Updated By/Date** - Kamryn Vinson, March 2022