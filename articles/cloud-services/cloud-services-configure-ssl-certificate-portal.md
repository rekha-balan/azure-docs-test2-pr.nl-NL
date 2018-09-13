---
title: Configure SSL for a cloud service  | Microsoft Docs
description: Learn how to specify an HTTPS endpoint for a web role and how to upload an SSL certificate to secure your application. These examples use the Azure portal.
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: ''
ms.assetid: 371ba204-48b6-41af-ab9f-ed1d64efe704
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/04/2017
ms.author: adegeo
ms.openlocfilehash: 25c96d50a518c249fe986ae72e5d23f2729a8331
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661283"
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="9245a-104">Configuring SSL for an application in Azure</span><span class="sxs-lookup"><span data-stu-id="9245a-104">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](cloud-services-configure-ssl-certificate-portal.md)
> * [Azure classic portal](cloud-services-configure-ssl-certificate.md)
> 

<span data-ttu-id="9245a-107">Secure Socket Layer (SSL) encryption is the most commonly used method of securing data sent across the internet.</span><span class="sxs-lookup"><span data-stu-id="9245a-107">Secure Socket Layer (SSL) encryption is the most commonly used method of securing data sent across the internet.</span></span> <span data-ttu-id="9245a-108">This common task discusses how to specify an HTTPS endpoint for a web role and how to upload an SSL certificate to secure your application.</span><span class="sxs-lookup"><span data-stu-id="9245a-108">This common task discusses how to specify an HTTPS endpoint for a web role and how to upload an SSL certificate to secure your application.</span></span>

> [!NOTE]
> The procedures in this task apply to Azure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md).
> 

<span data-ttu-id="9245a-110">This task uses a production deployment; information on using a staging deployment is provided at the end of this topic.</span><span class="sxs-lookup"><span data-stu-id="9245a-110">This task uses a production deployment; information on using a staging deployment is provided at the end of this topic.</span></span>

<span data-ttu-id="9245a-111">Read [this](cloud-services-how-to-create-deploy-portal.md) first if you have not yet created a cloud service.</span><span class="sxs-lookup"><span data-stu-id="9245a-111">Read [this](cloud-services-how-to-create-deploy-portal.md) first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="9245a-112">Step 1: Get an SSL certificate</span><span class="sxs-lookup"><span data-stu-id="9245a-112">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="9245a-113">To configure SSL for an application, you first need to get an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span><span class="sxs-lookup"><span data-stu-id="9245a-113">To configure SSL for an application, you first need to get an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="9245a-114">If you do not already have one, you need to obtain one from a company that sells SSL certificates.</span><span class="sxs-lookup"><span data-stu-id="9245a-114">If you do not already have one, you need to obtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="9245a-115">The certificate must meet the following requirements for SSL certificates in Azure:</span><span class="sxs-lookup"><span data-stu-id="9245a-115">The certificate must meet the following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="9245a-116">The certificate must contain a private key.</span><span class="sxs-lookup"><span data-stu-id="9245a-116">The certificate must contain a private key.</span></span>
* <span data-ttu-id="9245a-117">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span><span class="sxs-lookup"><span data-stu-id="9245a-117">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="9245a-118">The certificate's subject name must match the domain used to access the cloud service.</span><span class="sxs-lookup"><span data-stu-id="9245a-118">The certificate's subject name must match the domain used to access the cloud service.</span></span> <span data-ttu-id="9245a-119">You cannot obtain an SSL certificate from a certificate authority (CA) for the cloudapp.net domain.</span><span class="sxs-lookup"><span data-stu-id="9245a-119">You cannot obtain an SSL certificate from a certificate authority (CA) for the cloudapp.net domain.</span></span> <span data-ttu-id="9245a-120">You must acquire a custom domain name to use when access your service.</span><span class="sxs-lookup"><span data-stu-id="9245a-120">You must acquire a custom domain name to use when access your service.</span></span> <span data-ttu-id="9245a-121">When you request a certificate from a CA the certificate's subject name must match the custom domain name used to access your application.</span><span class="sxs-lookup"><span data-stu-id="9245a-121">When you request a certificate from a CA the certificate's subject name must match the custom domain name used to access your application.</span></span> <span data-ttu-id="9245a-122">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for \***.contoso.com** or **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="9245a-122">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for \***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="9245a-123">The certificate must use a minimum of 2048-bit encryption.</span><span class="sxs-lookup"><span data-stu-id="9245a-123">The certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="9245a-124">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span><span class="sxs-lookup"><span data-stu-id="9245a-124">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="9245a-125">A self-signed certificate is not authenticated through a CA and can use the cloudapp.net domain as the website URL.</span><span class="sxs-lookup"><span data-stu-id="9245a-125">A self-signed certificate is not authenticated through a CA and can use the cloudapp.net domain as the website URL.</span></span> <span data-ttu-id="9245a-126">For example, the task below uses a self-signed certificate in which the common name (CN) used in the certificate is **sslexample.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="9245a-126">For example, the task below uses a self-signed certificate in which the common name (CN) used in the certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="9245a-127">Next, you must include information about the certificate in your service definition and service configuration files.</span><span class="sxs-lookup"><span data-stu-id="9245a-127">Next, you must include information about the certificate in your service definition and service configuration files.</span></span>

<span data-ttu-id="9245a-128"><a name="modify"> </a></span><span class="sxs-lookup"><span data-stu-id="9245a-128"><a name="modify"> </a></span></span>

## <a name="step-2-modify-the-service-definition-and-configuration-files"></a><span data-ttu-id="9245a-129">Step 2: Modify the service definition and configuration files</span><span class="sxs-lookup"><span data-stu-id="9245a-129">Step 2: Modify the service definition and configuration files</span></span>
<span data-ttu-id="9245a-130">Your application must be configured to use the certificate, and an HTTPS endpoint must be added.</span><span class="sxs-lookup"><span data-stu-id="9245a-130">Your application must be configured to use the certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="9245a-131">As a result, the service definition and service configuration files need to be updated.</span><span class="sxs-lookup"><span data-stu-id="9245a-131">As a result, the service definition and service configuration files need to be updated.</span></span>

1. <span data-ttu-id="9245a-132">In your development environment, open the service definition file (CSDEF), add a **Certificates** section within the **WebRole** section, and include the following information about the certificate (and intermediate certificates):</span><span class="sxs-lookup"><span data-stu-id="9245a-132">In your development environment, open the service definition file (CSDEF), add a **Certificates** section within the **WebRole** section, and include the following information about the certificate (and intermediate certificates):</span></span>
   
   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Certificates>
            <Certificate name="SampleCertificate" 
                        storeLocation="LocalMachine" 
                        storeName="My"
                        permissionLevel="limitedOrElevated" />
            <!-- IMPORTANT! Unless your certificate is either
            self-signed or signed directly by the CA root, you
            must include all the intermediate certificates
            here. You must list them here, even if they are
            not bound to any endpoints. Failing to list any of
            the intermediate certificates may cause hard-to-reproduce
            interoperability problems on some clients.-->
            <Certificate name="CAForSampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="CA"
                        permissionLevel="limitedOrElevated" />
        </Certificates>
    ...
    </WebRole>
    ```
   
   <span data-ttu-id="9245a-133">The **Certificates** section defines the name of our certificate, its location, and the name of the store where it is located.</span><span class="sxs-lookup"><span data-stu-id="9245a-133">The **Certificates** section defines the name of our certificate, its location, and the name of the store where it is located.</span></span>
   
   <span data-ttu-id="9245a-134">Permissions (`permisionLevel` attribute) can be set to one of the following:</span><span class="sxs-lookup"><span data-stu-id="9245a-134">Permissions (`permisionLevel` attribute) can be set to one of the following:</span></span>
   
   | <span data-ttu-id="9245a-135">Permission Value</span><span class="sxs-lookup"><span data-stu-id="9245a-135">Permission Value</span></span> | <span data-ttu-id="9245a-136">Description</span><span class="sxs-lookup"><span data-stu-id="9245a-136">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="9245a-137">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="9245a-137">limitedOrElevated</span></span> |<span data-ttu-id="9245a-138">**(Default)** All role processes can access the private key.</span><span class="sxs-lookup"><span data-stu-id="9245a-138">**(Default)** All role processes can access the private key.</span></span> |
   | <span data-ttu-id="9245a-139">elevated</span><span class="sxs-lookup"><span data-stu-id="9245a-139">elevated</span></span> |<span data-ttu-id="9245a-140">Only elevated processes can access the private key.</span><span class="sxs-lookup"><span data-stu-id="9245a-140">Only elevated processes can access the private key.</span></span> |

2. <span data-ttu-id="9245a-141">In your service definition file, add an **InputEndpoint** element within the **Endpoints** section to enable HTTPS:</span><span class="sxs-lookup"><span data-stu-id="9245a-141">In your service definition file, add an **InputEndpoint** element within the **Endpoints** section to enable HTTPS:</span></span>
   
   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Endpoints>
            <InputEndpoint name="HttpsIn" protocol="https" port="443" 
                certificate="SampleCertificate" />
        </Endpoints>
    ...
    </WebRole>
    ```

3. <span data-ttu-id="9245a-142">In your service definition file, add a **Binding** element within the **Sites** section.</span><span class="sxs-lookup"><span data-stu-id="9245a-142">In your service definition file, add a **Binding** element within the **Sites** section.</span></span> <span data-ttu-id="9245a-143">This adds an HTTPS binding to map the endpoint to your site:</span><span class="sxs-lookup"><span data-stu-id="9245a-143">This adds an HTTPS binding to map the endpoint to your site:</span></span>
   
   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="HttpsIn" endpointName="HttpsIn" />
                </Bindings>
            </Site>
        </Sites>
    ...
    </WebRole>
    ```
   
   <span data-ttu-id="9245a-144">All of the required changes to the service definition file have been completed, but you still need to add the certificate information to the service configuration file.</span><span class="sxs-lookup"><span data-stu-id="9245a-144">All of the required changes to the service definition file have been completed, but you still need to add the certificate information to the service configuration file.</span></span>
4. <span data-ttu-id="9245a-145">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** section within the **Role** section, replacing the sample thumbprint value shown below with that of your certificate:</span><span class="sxs-lookup"><span data-stu-id="9245a-145">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** section within the **Role** section, replacing the sample thumbprint value shown below with that of your certificate:</span></span>
   
   ```xml
    <Role name="Deployment">
    ...
        <Certificates>
            <Certificate name="SampleCertificate" 
                thumbprint="9427befa18ec6865a9ebdc79d4c38de50e6316ff" 
                thumbprintAlgorithm="sha1" />
            <Certificate name="CAForSampleCertificate"
                thumbprint="79d4c38de50e6316ff9427befa18ec6865a9ebdc" 
                thumbprintAlgorithm="sha1" />
        </Certificates>
    ...
    </Role>
    ```

<span data-ttu-id="9245a-146">(The example above uses **sha1** for the thumbprint algorithm.</span><span class="sxs-lookup"><span data-stu-id="9245a-146">(The example above uses **sha1** for the thumbprint algorithm.</span></span> <span data-ttu-id="9245a-147">Specify the appropriate value for your certificate's thumbprint algorithm.)</span><span class="sxs-lookup"><span data-stu-id="9245a-147">Specify the appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="9245a-148">Now that the service definition and service configuration files have been updated, package your deployment for uploading to Azure.</span><span class="sxs-lookup"><span data-stu-id="9245a-148">Now that the service definition and service configuration files have been updated, package your deployment for uploading to Azure.</span></span> <span data-ttu-id="9245a-149">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that will overwrite the certificate information you just inserted.</span><span class="sxs-lookup"><span data-stu-id="9245a-149">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that will overwrite the certificate information you just inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="9245a-150">Step 3: Upload a certificate</span><span class="sxs-lookup"><span data-stu-id="9245a-150">Step 3: Upload a certificate</span></span>
<span data-ttu-id="9245a-151">Connect to the portal and...</span><span class="sxs-lookup"><span data-stu-id="9245a-151">Connect to the portal and...</span></span>

1. <span data-ttu-id="9245a-152">Select your cloud service in the Portal, select your **Cloud Service**.</span><span class="sxs-lookup"><span data-stu-id="9245a-152">Select your cloud service in the Portal, select your **Cloud Service**.</span></span> <span data-ttu-id="9245a-153">(Which is in the **All resources** section.)</span><span class="sxs-lookup"><span data-stu-id="9245a-153">(Which is in the **All resources** section.)</span></span> 
   
    ![Publish your cloud service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-configure-ssl-certificate-portal/browse.png)

2. <span data-ttu-id="9245a-155">Click **Certificates**.</span><span class="sxs-lookup"><span data-stu-id="9245a-155">Click **Certificates**.</span></span>
   
    ![Click the certificates icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-configure-ssl-certificate-portal/certificate-item.png)

3. <span data-ttu-id="9245a-157">Provide the **File**, **Password**, then click **Upload**.</span><span class="sxs-lookup"><span data-stu-id="9245a-157">Provide the **File**, **Password**, then click **Upload**.</span></span>

## <a name="step-4-connect-to-the-role-instance-by-using-https"></a><span data-ttu-id="9245a-158">Step 4: Connect to the role instance by using HTTPS</span><span class="sxs-lookup"><span data-stu-id="9245a-158">Step 4: Connect to the role instance by using HTTPS</span></span>
<span data-ttu-id="9245a-159">Now that your deployment is up and running in Azure, you can connect to it using HTTPS.</span><span class="sxs-lookup"><span data-stu-id="9245a-159">Now that your deployment is up and running in Azure, you can connect to it using HTTPS.</span></span>

1. <span data-ttu-id="9245a-160">Click the **Site URL** to open up the web browser.</span><span class="sxs-lookup"><span data-stu-id="9245a-160">Click the **Site URL** to open up the web browser.</span></span>
   
   ![Click on Site URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-configure-ssl-certificate-portal/navigate.png)

2. <span data-ttu-id="9245a-162">In your web browser, modify the link to use **https** instead of **http**, and then visit the page.</span><span class="sxs-lookup"><span data-stu-id="9245a-162">In your web browser, modify the link to use **https** instead of **http**, and then visit the page.</span></span>
   
   > [!NOTE]
   > If you are using a self-signed certificate, when you browse to an HTTPS endpoint that's associated with the self-signed certificate you may see a certificate error in the browser. Using a certificate signed by a trusted certification authority eliminates this problem; in the meantime, you can ignore the error. (Another option is to add the self-signed certificate to the user's trusted certificate authority certificate store.)
   > 
   > 
   
   ![Site preview](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-configure-ssl-certificate-portal/show-site.png)
   
   > [!TIP]
   > If you want to use SSL for a staging deployment instead of a production deployment, you'll first need to determine the URL used for the staging deployment. Once your cloud service has been deployed, the URL to the staging environment is determined by the **Deployment ID** GUID in this format: `https://deployment-id.cloudapp.net/`  
   > 
   > Create a certificate with the common name (CN) equal to the GUID-based URL (for example, **328187776e774ceda8fc57609d404462.cloudapp.net**). Use the portal to add the certificate to your staged cloud service. Then, add the certificate information to your CSDEF and CSCFG files, repackage your application, and update your staged deployment to use the new package.
   > 

## <a name="next-steps"></a><span data-ttu-id="9245a-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="9245a-172">Next steps</span></span>
* <span data-ttu-id="9245a-173">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9245a-173">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="9245a-174">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9245a-174">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="9245a-175">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9245a-175">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="9245a-176">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9245a-176">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>




