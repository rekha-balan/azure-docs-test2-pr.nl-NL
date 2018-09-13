---
title: Configure SSL for a cloud service  | Microsoft Docs
description: Learn how to specify an HTTPS endpoint for a web role and how to upload an SSL certificate to secure your application. These examples use the Azure portal.
services: cloud-services
documentationcenter: .net
author: jpconnock
manager: timlt
editor: ''
ms.assetid: 371ba204-48b6-41af-ab9f-ed1d64efe704
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jeconnoc
ms.openlocfilehash: e3e7d271375cd9c3f49d8fedd963b5234dab7902
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44793512"
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="32593-104">Configuring SSL for an application in Azure</span><span class="sxs-lookup"><span data-stu-id="32593-104">Configuring SSL for an application in Azure</span></span>

<span data-ttu-id="32593-105">Secure Socket Layer (SSL) encryption is the most commonly used method of securing data sent across the internet.</span><span class="sxs-lookup"><span data-stu-id="32593-105">Secure Socket Layer (SSL) encryption is the most commonly used method of securing data sent across the internet.</span></span> <span data-ttu-id="32593-106">This common task discusses how to specify an HTTPS endpoint for a web role and how to upload an SSL certificate to secure your application.</span><span class="sxs-lookup"><span data-stu-id="32593-106">This common task discusses how to specify an HTTPS endpoint for a web role and how to upload an SSL certificate to secure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="32593-107">The procedures in this task apply to Azure Cloud Services; for App Services, see [this](../app-service/app-service-web-tutorial-custom-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="32593-107">The procedures in this task apply to Azure Cloud Services; for App Services, see [this](../app-service/app-service-web-tutorial-custom-ssl.md).</span></span>
>

<span data-ttu-id="32593-108">This task uses a production deployment.</span><span class="sxs-lookup"><span data-stu-id="32593-108">This task uses a production deployment.</span></span> <span data-ttu-id="32593-109">Information on using a staging deployment is provided at the end of this topic.</span><span class="sxs-lookup"><span data-stu-id="32593-109">Information on using a staging deployment is provided at the end of this topic.</span></span>

<span data-ttu-id="32593-110">Read [this](cloud-services-how-to-create-deploy-portal.md) first if you have not yet created a cloud service.</span><span class="sxs-lookup"><span data-stu-id="32593-110">Read [this](cloud-services-how-to-create-deploy-portal.md) first if you have not yet created a cloud service.</span></span>

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="32593-111">Step 1: Get an SSL certificate</span><span class="sxs-lookup"><span data-stu-id="32593-111">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="32593-112">To configure SSL for an application, you first need to get an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span><span class="sxs-lookup"><span data-stu-id="32593-112">To configure SSL for an application, you first need to get an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="32593-113">If you do not already have one, you need to obtain one from a company that sells SSL certificates.</span><span class="sxs-lookup"><span data-stu-id="32593-113">If you do not already have one, you need to obtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="32593-114">The certificate must meet the following requirements for SSL certificates in Azure:</span><span class="sxs-lookup"><span data-stu-id="32593-114">The certificate must meet the following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="32593-115">The certificate must contain a private key.</span><span class="sxs-lookup"><span data-stu-id="32593-115">The certificate must contain a private key.</span></span>
* <span data-ttu-id="32593-116">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span><span class="sxs-lookup"><span data-stu-id="32593-116">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="32593-117">The certificate's subject name must match the domain used to access the cloud service.</span><span class="sxs-lookup"><span data-stu-id="32593-117">The certificate's subject name must match the domain used to access the cloud service.</span></span> <span data-ttu-id="32593-118">You cannot obtain an SSL certificate from a certificate authority (CA) for the cloudapp.net domain.</span><span class="sxs-lookup"><span data-stu-id="32593-118">You cannot obtain an SSL certificate from a certificate authority (CA) for the cloudapp.net domain.</span></span> <span data-ttu-id="32593-119">You must acquire a custom domain name to use when access your service.</span><span class="sxs-lookup"><span data-stu-id="32593-119">You must acquire a custom domain name to use when access your service.</span></span> <span data-ttu-id="32593-120">When you request a certificate from a CA, the certificate's subject name must match the custom domain name used to access your application.</span><span class="sxs-lookup"><span data-stu-id="32593-120">When you request a certificate from a CA, the certificate's subject name must match the custom domain name used to access your application.</span></span> <span data-ttu-id="32593-121">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for \***.contoso.com** or **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="32593-121">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for \***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="32593-122">The certificate must use a minimum of 2048-bit encryption.</span><span class="sxs-lookup"><span data-stu-id="32593-122">The certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="32593-123">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span><span class="sxs-lookup"><span data-stu-id="32593-123">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="32593-124">A self-signed certificate is not authenticated through a CA and can use the cloudapp.net domain as the website URL.</span><span class="sxs-lookup"><span data-stu-id="32593-124">A self-signed certificate is not authenticated through a CA and can use the cloudapp.net domain as the website URL.</span></span> <span data-ttu-id="32593-125">For example, the following task uses a self-signed certificate in which the common name (CN) used in the certificate is **sslexample.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="32593-125">For example, the following task uses a self-signed certificate in which the common name (CN) used in the certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="32593-126">Next, you must include information about the certificate in your service definition and service configuration files.</span><span class="sxs-lookup"><span data-stu-id="32593-126">Next, you must include information about the certificate in your service definition and service configuration files.</span></span>

<span data-ttu-id="32593-127"><a name="modify"> </a></span><span class="sxs-lookup"><span data-stu-id="32593-127"><a name="modify"> </a></span></span>

## <a name="step-2-modify-the-service-definition-and-configuration-files"></a><span data-ttu-id="32593-128">Step 2: Modify the service definition and configuration files</span><span class="sxs-lookup"><span data-stu-id="32593-128">Step 2: Modify the service definition and configuration files</span></span>
<span data-ttu-id="32593-129">Your application must be configured to use the certificate, and an HTTPS endpoint must be added.</span><span class="sxs-lookup"><span data-stu-id="32593-129">Your application must be configured to use the certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="32593-130">As a result, the service definition and service configuration files need to be updated.</span><span class="sxs-lookup"><span data-stu-id="32593-130">As a result, the service definition and service configuration files need to be updated.</span></span>

1. <span data-ttu-id="32593-131">In your development environment, open the service definition file (CSDEF), add a **Certificates** section within the **WebRole** section, and include the following information about the certificate (and intermediate certificates):</span><span class="sxs-lookup"><span data-stu-id="32593-131">In your development environment, open the service definition file (CSDEF), add a **Certificates** section within the **WebRole** section, and include the following information about the certificate (and intermediate certificates):</span></span>

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

   <span data-ttu-id="32593-132">The **Certificates** section defines the name of our certificate, its location, and the name of the store where it is located.</span><span class="sxs-lookup"><span data-stu-id="32593-132">The **Certificates** section defines the name of our certificate, its location, and the name of the store where it is located.</span></span>

   <span data-ttu-id="32593-133">Permissions (`permisionLevel` attribute) can be set to one of the following values:</span><span class="sxs-lookup"><span data-stu-id="32593-133">Permissions (`permisionLevel` attribute) can be set to one of the following values:</span></span>

   | <span data-ttu-id="32593-134">Permission Value</span><span class="sxs-lookup"><span data-stu-id="32593-134">Permission Value</span></span> | <span data-ttu-id="32593-135">Description</span><span class="sxs-lookup"><span data-stu-id="32593-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="32593-136">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="32593-136">limitedOrElevated</span></span> |<span data-ttu-id="32593-137">**(Default)** All role processes can access the private key.</span><span class="sxs-lookup"><span data-stu-id="32593-137">**(Default)** All role processes can access the private key.</span></span> |
   | <span data-ttu-id="32593-138">elevated</span><span class="sxs-lookup"><span data-stu-id="32593-138">elevated</span></span> |<span data-ttu-id="32593-139">Only elevated processes can access the private key.</span><span class="sxs-lookup"><span data-stu-id="32593-139">Only elevated processes can access the private key.</span></span> |

2. <span data-ttu-id="32593-140">In your service definition file, add an **InputEndpoint** element within the **Endpoints** section to enable HTTPS:</span><span class="sxs-lookup"><span data-stu-id="32593-140">In your service definition file, add an **InputEndpoint** element within the **Endpoints** section to enable HTTPS:</span></span>

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

3. <span data-ttu-id="32593-141">In your service definition file, add a **Binding** element within the **Sites** section.</span><span class="sxs-lookup"><span data-stu-id="32593-141">In your service definition file, add a **Binding** element within the **Sites** section.</span></span> <span data-ttu-id="32593-142">This element adds an HTTPS binding to map the endpoint to your site:</span><span class="sxs-lookup"><span data-stu-id="32593-142">This element adds an HTTPS binding to map the endpoint to your site:</span></span>

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

   <span data-ttu-id="32593-143">All the required changes to the service definition file have been completed; but, you still need to add the certificate information to the service configuration file.</span><span class="sxs-lookup"><span data-stu-id="32593-143">All the required changes to the service definition file have been completed; but, you still need to add the certificate information to the service configuration file.</span></span>
4. <span data-ttu-id="32593-144">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** value with that of your certificate.</span><span class="sxs-lookup"><span data-stu-id="32593-144">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** value with that of your certificate.</span></span> <span data-ttu-id="32593-145">The following code sample provides details of the **Certificates** section, except for the thumbprint value.</span><span class="sxs-lookup"><span data-stu-id="32593-145">The following code sample provides details of the **Certificates** section, except for the thumbprint value.</span></span>

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

<span data-ttu-id="32593-146">(This example uses **sha1** for the thumbprint algorithm.</span><span class="sxs-lookup"><span data-stu-id="32593-146">(This example uses **sha1** for the thumbprint algorithm.</span></span> <span data-ttu-id="32593-147">Specify the appropriate value for your certificate's thumbprint algorithm.)</span><span class="sxs-lookup"><span data-stu-id="32593-147">Specify the appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="32593-148">Now that the service definition and service configuration files have been updated, package your deployment for uploading to Azure.</span><span class="sxs-lookup"><span data-stu-id="32593-148">Now that the service definition and service configuration files have been updated, package your deployment for uploading to Azure.</span></span> <span data-ttu-id="32593-149">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that will overwrite the certificate information you just inserted.</span><span class="sxs-lookup"><span data-stu-id="32593-149">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that will overwrite the certificate information you just inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="32593-150">Step 3: Upload a certificate</span><span class="sxs-lookup"><span data-stu-id="32593-150">Step 3: Upload a certificate</span></span>
<span data-ttu-id="32593-151">Connect to the Azure portal and...</span><span class="sxs-lookup"><span data-stu-id="32593-151">Connect to the Azure portal and...</span></span>

1. <span data-ttu-id="32593-152">In the **All resources** section of the Portal, select your cloud service.</span><span class="sxs-lookup"><span data-stu-id="32593-152">In the **All resources** section of the Portal, select your cloud service.</span></span>

    ![Publish your cloud service](media/cloud-services-configure-ssl-certificate-portal/browse.png)

2. <span data-ttu-id="32593-154">Click **Certificates**.</span><span class="sxs-lookup"><span data-stu-id="32593-154">Click **Certificates**.</span></span>

    ![Click the certificates icon](media/cloud-services-configure-ssl-certificate-portal/certificate-item.png)

3. <span data-ttu-id="32593-156">Click **Upload** at the top of the certificates area.</span><span class="sxs-lookup"><span data-stu-id="32593-156">Click **Upload** at the top of the certificates area.</span></span>

    ![Click the Upload menu item](media/cloud-services-configure-ssl-certificate-portal/Upload_menu.png)

4. <span data-ttu-id="32593-158">Provide the **File**, **Password**, then click **Upload** at the bottom of the data entry area.</span><span class="sxs-lookup"><span data-stu-id="32593-158">Provide the **File**, **Password**, then click **Upload** at the bottom of the data entry area.</span></span>

## <a name="step-4-connect-to-the-role-instance-by-using-https"></a><span data-ttu-id="32593-159">Step 4: Connect to the role instance by using HTTPS</span><span class="sxs-lookup"><span data-stu-id="32593-159">Step 4: Connect to the role instance by using HTTPS</span></span>
<span data-ttu-id="32593-160">Now that your deployment is up and running in Azure, you can connect to it using HTTPS.</span><span class="sxs-lookup"><span data-stu-id="32593-160">Now that your deployment is up and running in Azure, you can connect to it using HTTPS.</span></span>

1. <span data-ttu-id="32593-161">Click the **Site URL** to open up the web browser.</span><span class="sxs-lookup"><span data-stu-id="32593-161">Click the **Site URL** to open up the web browser.</span></span>

   ![Click the Site URL](media/cloud-services-configure-ssl-certificate-portal/navigate.png)

2. <span data-ttu-id="32593-163">In your web browser, modify the link to use **https** instead of **http**, and then visit the page.</span><span class="sxs-lookup"><span data-stu-id="32593-163">In your web browser, modify the link to use **https** instead of **http**, and then visit the page.</span></span>

   > [!NOTE]
   > <span data-ttu-id="32593-164">If you are using a self-signed certificate, when you browse to an HTTPS endpoint that's associated with the self-signed certificate you may see a certificate error in the browser.</span><span class="sxs-lookup"><span data-stu-id="32593-164">If you are using a self-signed certificate, when you browse to an HTTPS endpoint that's associated with the self-signed certificate you may see a certificate error in the browser.</span></span> <span data-ttu-id="32593-165">Using a certificate signed by a trusted certification authority eliminates this problem; in the meantime, you can ignore the error.</span><span class="sxs-lookup"><span data-stu-id="32593-165">Using a certificate signed by a trusted certification authority eliminates this problem; in the meantime, you can ignore the error.</span></span> <span data-ttu-id="32593-166">(Another option is to add the self-signed certificate to the user's trusted certificate authority certificate store.)</span><span class="sxs-lookup"><span data-stu-id="32593-166">(Another option is to add the self-signed certificate to the user's trusted certificate authority certificate store.)</span></span>
   >
   >

   ![Site preview](media/cloud-services-configure-ssl-certificate-portal/show-site.png)

   > [!TIP]
   > <span data-ttu-id="32593-168">If you want to use SSL for a staging deployment instead of a production deployment, you'll first need to determine the URL used for the staging deployment.</span><span class="sxs-lookup"><span data-stu-id="32593-168">If you want to use SSL for a staging deployment instead of a production deployment, you'll first need to determine the URL used for the staging deployment.</span></span> <span data-ttu-id="32593-169">Once your cloud service has been deployed, the URL to the staging environment is determined by the **Deployment ID** GUID in this format: `https://deployment-id.cloudapp.net/`</span><span class="sxs-lookup"><span data-stu-id="32593-169">Once your cloud service has been deployed, the URL to the staging environment is determined by the **Deployment ID** GUID in this format: `https://deployment-id.cloudapp.net/`</span></span>  
   >
   > <span data-ttu-id="32593-170">Create a certificate with the common name (CN) equal to the GUID-based URL (for example, **328187776e774ceda8fc57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="32593-170">Create a certificate with the common name (CN) equal to the GUID-based URL (for example, **328187776e774ceda8fc57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="32593-171">Use the portal to add the certificate to your staged cloud service.</span><span class="sxs-lookup"><span data-stu-id="32593-171">Use the portal to add the certificate to your staged cloud service.</span></span> <span data-ttu-id="32593-172">Then, add the certificate information to your CSDEF and CSCFG files, repackage your application, and update your staged deployment to use the new package.</span><span class="sxs-lookup"><span data-stu-id="32593-172">Then, add the certificate information to your CSDEF and CSCFG files, repackage your application, and update your staged deployment to use the new package.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="32593-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="32593-173">Next steps</span></span>
* <span data-ttu-id="32593-174">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="32593-174">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="32593-175">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="32593-175">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="32593-176">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="32593-176">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="32593-177">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="32593-177">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
