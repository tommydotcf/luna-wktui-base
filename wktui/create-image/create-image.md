# Creation of Images for the Oracle Container Engine for Kubernetes (OKE) on Oracle Cloud Infrastructure (OCI)
## Introduction

**Primary Image** - The image containing the Oracle Fusion Middleware software. It is used as the basis of all containers that run WebLogic Servers for the domain.

**Auxiliary Image** - The image that supplies the WebLogic Deploy Tooling software and the model files. At runtime, the auxiliary image’s content is merged with the primary image’s content.
    ![Image Structure](images/ImageStructure.png)

In this Lab, We specify WebLogic server 12.2.1.3.0-ol8 image as Primary Image. Also, we create an auxiliary image, and push it to Oracle Container Image Registry repository using the generated authentication token. 

### Objectives

In this lab, you will:

* Enter WebLogic Server Image tag inside the Primary Image Tag.
* Create an Auxiliary Image and push the image to Oracle Cloud Container Image Registry.

### Prerequisites

* Accepted the license for WebLogic Server Images, Created Repository and Generated Authentication token in lab 2.
* You should have a text editor.

## Task 1: Enter details of Primary Container Image 


In lab 1, we accepted the license agreement for WebLogic Server Images. In this task, we use WebLogic Server 12.2.1.3.0-ol8 image as Primary Image.

1. Click *Image*. We already preset *Image Tag* with the below value. 

    ```bash
    <copy>container-registry.oracle.com/middleware/weblogic:12.2.1.3-ol8</copy>
    ```
    ![Primary Image](images/PrimaryImage.png)
    > **For your information only:**<br>
    > The primary image is the one used for running the domain. One primary image can be reused for hundreds of domains. The primary image contains the OS, JDK, and FMW software installations.


## Task 2: Prepare Auxiliary Image and Push the Auxiliary Image 

In this task, We are creating an Auxiliary image, which we will push to the Oracle Cloud Container Registry.

1. To create the Auxiliary Image Tag, we need the following information:

    * End point for the Region
    * Tenancy Namespace

    You can find out your *Region Name* in top right corner in the Oracle Cloud Console.
    ![Region Name](images/RegionName.png)

2. To find out the endpoint for your Region, select this URL [https://docs.oracle.com/en-us/iaas/Content/Registry/Concepts/registryprerequisites.htm#Availab](https://docs.oracle.com/en-us/iaas/Content/Registry/Concepts/registryprerequisites.htm#Availab). In my case, it is *UK South (London)* as the region name, thus its endpoint is *lhr.ocir.io*. Find out your endpoint for your own *Region Name* and save it in your text editor.
    ![Region Endpoints](images/RegionEndpoints.png)

3. In lab 1, you already noted the tenancy namespace in your text editor. If not, then for finding the Namespace of the tenancy, select the *Hamburger Menu* -> *Developer Services* -> *Container Registry*, as shown. Select your own compartment, you will find the Namespace as shown.
    ![Tenancy Namespace](images/TenancyNamespace.png)

4. Now you have both the Tenancy Namespace and Endpoint for your region. Copy the following command and paste it in your text editor. Then replace the `END_POINT_OF_YOUR_REGION` with the endpoint of your region name, `NAMESPACE_OF_YOUR_TENANCY` with your tenancy's namespace. Click on *Auxiliary Image* tab as shown.
    ![Auxiliary Tab](images/AuxiliaryTab.png)

    ````bash
    <copy>END_POINT_OF_YOUR_REGION/NAMESPACE_OF_YOUR_TENANCY/test-model:v1</copy>
    ````

> For example, in my case Auxiliary Image tag is `lhr.ocir.io/tenancynamespace/test-model:v1`.

5. In the previous step, you also determined the tenancy namespace.
Enter the  Auxiliary Image Registry Push Username as follows: `NAMESPACE_OF_YOUR_TENANCY`/`YOUR_ORACLE_CLOUD_USERNAME`. <br>
* Replace `NAMESPACE_OF_YOUR_TENANCY` with your tenancy's namespace
* Replace `YOUR_ORACLE_CLOUD_USERNAME` with your Oracle Cloud Account user name and then copy the replaced username from your text editor and paste it in the *Auxiliary Image Registry Push Username*.
> For example, in my case Auxiliary Image Registry Push Username is `tenancynamespace/lab.user@oracle.com`.
* For Password, copy and paste the Authentication Token from your text editor(or wherever you saved it) and paste it in the *Auxiliary Image Registry Push Username*.
    ![Auxiliary Image Details](images/AuxiliaryImageDetails.png)

6. Click *Create Auxiliary Image*.
    ![Create Auxiliary Image](images/CreateAuxiliaryImage.png)

7. As we already prepared the model in Lab 2, so click on *No*.
    ![Prepare Model](images/PrepareModel.png)

8. Select *Downloads* folder where we want to save *WebLogic Deployer* and click *Select* as shown.
    ![WDT Location](images/WDTLocation.png)

9. Once Auxiliary images is successfully created, On *Create Auxiliary Image Complete* window, click *Ok*.
    ![Auxiliary Created](images/AuxiliaryCreated.png)
    > **For your information only:**<br>
    >  An auxiliary image is domain-specific. The auxiliary image contains the data that defines the domain.

10. Click *Push Auxiliary Image* to push the image in repository inside your Oracle Cloud Container Image Registry.
    ![Push Auxiliary](images/PushAuxiliary.png)
11. Once image is successfully pushed, On *Push Image Complete* window, click *Ok*. 
    ![Auxiliary Pushed](images/AuxiliaryPushed.png)



## Acknowledgements

* **Author** -  Ankit Pandey
* **Contributors** - Maciej Gruszka, Sid Joshi
* **Last Updated By/Date** - Kamryn Vinson, March 2022