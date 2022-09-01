# Module 5 Lesson 4 Lab 7: Deploy Azure Health Data Services workspace and FHIR service

### Overview

In this lab, you will deploy an **Azure Health Data Services workspace** containing a **FHIR service** instance. In addition, you will set up Postman as your application for testing the FHIR service API.

**FHIR service** is the core component for reading, writing, and querying structured health data in Azure Health Data Services. You may have heard of the predecessor to FHIR service – called Azure API for FHIR (Microsoft's first generally available FHIR PaaS solution). For this training, we will be focusing on the new Azure Health Data Services FHIR service, which has some big advantages over its predecessor (like transaction bundles, workspace level configuration, and performance improvements for search, import, and export).

**Azure Health Data Services workspace relationship with FHIR, DICOM, and MedTech services**

In the Azure health ecosystem, the Azure Health Data Services workspace is a logical container for associated healthcare service instances such as FHIR, DICOM (Digital Imaging and Communications in Medicine), and MedTech services. You can provision multiple FHIR, DICOM, and MedTech services in a single workspace to meet your solution needs.

![Graphical user interface, application, Teams Description automatically generated](media/2790d5724c13d7d735b0307ba2d2b36e.png)

The workspace also creates a compliance boundary (HIPAA, HITRUST) within which protected health information can travel. This means that [Role-Based Access Control (RBAC)](https://docs.microsoft.com/azure/healthcare-apis/configure-azure-rbac), private network data transit with [Private Link](https://docs.microsoft.com/azure/healthcare-apis/healthcare-apis-configure-private-link), and [event messages](https://docs.microsoft.com/azure/healthcare-apis/events/events-deploy-portal) can all be configured at the workspace level – reducing your system management complexity.

### Learning objectives

In this lab, you will:

-   Explain the difference between workspaces and services in Azure Health Data Services
-   Use a template to deploy a FHIR service instance inside an Azure Health Data Services workspace
-   Create an AAD service client for Postman and grant it access to your FHIR service
-   Configure and use Postman for sending web API requests to your FHIR service

### Step 1: Deploy Azure Health Data Services workspace and FHIR service to your Azure environment

In the first part of this lab, you will

-   Use a template to deploy resources with the Azure Portal. This template will deploy

    [Azure Health Data Services workspace](https://docs.microsoft.com/en-us/azure/healthcare-apis/workspace-overview)

-   [FHIR service](https://docs.microsoft.com/en-us/azure/healthcare-apis/fhir/overview)

    [FHIR Loader (for Lab-03)](https://docs.microsoft.com/en-us/azure/healthcare-apis/fhir/overview)

-   [FHIR-Proxy (for Lab-07)](https://github.com/microsoft/fhir-proxy)
1.  To begin, CTRL+click (Windows or Linux) or CMD+click (Mac) on the Deploy to Azure button below to open the deployment form in a new browser tab.

    ![](media/88401a321e9ab43984e628a8e64bfe2b.png)

1.  Select or fill in the parameter values (see image below).

    Important: In order to successfully deploy resources with this ARM template, the user must have [Owner](https://docs.microsoft.com/en-us/azure/role-based-access-control/built-in-roles#owner) rights for the [Resource Group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal) where the components are deployed. Before running the ARM template, it is recommended to create a new resource group first and check that you have Owner permissions. Once you confirm that you have Owner rights, then select that resource group in the dropdown menu when you fill out the deployment form (see \#3 below).

2.  Enter a custom **Deployment Prefix**. This prefix will be prepended to the names of all created resources ("trn05" is shown as an example prefix).
3.  Make sure to select the "true" values as shown.
1.  Click **Review + create** when ready, and then click **Create** on the next page.

    ![Graphical user interface Description automatically generated](media/27eaba55814ebace0e92de6b1f3cf487.png)

Note: This deployment typically takes 20 minutes. During the deployment, you can read the instructions linked in Step 2 below. When the deployment finishes, go ahead and proceed with those instructions.

To learn more about the resources deployed with this ARM template, view [here.](https://github.com/microsoft/azure-health-data-services-workshop/blob/main/resources/docs/FHIR-Starter_ARM_template_README.md#deployed-components)

### Step 2 - Set up Postman and test FHIR service

In the next part of this lab, you will

-   Visit another page and follow the instructions on setting up Postman.

    Make API calls to test FHIR service using Postman.

To begin, **CTRL+click** (Windows or Linux) or **CMD+click** (Mac) on the link below to open a Postman tutorial in a new browser tab.

[Postman Setup Tutorial](https://github.com/microsoft/azure-health-data-services-workshop/blob/main/resources/docs/FHIR-Starter_ARM_template_README.md#deployed-components)

Follow the instructions and return here when finished.

What does success look like for Lab 7?

-   Azure Health Data Services workspace and FHIR service deployed and available in Azure.

    Other Azure resources for later labs successfully deployed. Template deployment must show no errors.

-   App registration created in Azure Active Directory for use with Postman and your FHIR service.

    Postman set up and able to connect with your FHIR service.

    -   Capability Statement from your FHIR service – received.

        {

        "resourceType": "CapabilityStatement",

        "url": "/metadata",

        "version": "1.0.0.0",

        "name": "Microsoft FHIR service 2.2.61 Capability Statement",

        "status": "draft",

        "experimental": true,

        "date": "2022-02-18T00:06:47.9408665+00:00",

        "publisher": "Microsoft",

        "more below ..." : "..."

        }

-   POST AuthorizeGetToken call in Postman to obtain an AAD access token – succeeded.

    POST Save Patient call in Postman to populate FHIR service with a Patient Resource – succeeded.

-   GET List Patients call in Postman to retrieve a bundle with at least one Patient Resource from your FHIR service – succeeded
