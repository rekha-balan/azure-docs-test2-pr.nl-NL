---
title: How to use the service management API (Python) - feature guide
description: Learn how to programmatically perform common service management tasks from Python.
services: cloud-services
documentationcenter: python
author: lmazuel
manager: wpickett
editor: ''
ms.assetid: 61538ec0-1536-4a7e-ae89-95967fe35d73
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 04/05/2017
ms.author: lmazuel
ms.openlocfilehash: 90f417768d58c42df9b786b5c50d96970f133548
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553844"
---
# <a name="how-to-use-service-management-from-python"></a><span data-ttu-id="0c047-103">How to use Service Management from Python</span><span class="sxs-lookup"><span data-stu-id="0c047-103">How to use Service Management from Python</span></span>
> [!NOTE]
> <span data-ttu-id="0c047-104">Service Management API is being replaced with the new Resource Management API, currently available in a preview release.</span><span class="sxs-lookup"><span data-stu-id="0c047-104">Service Management API is being replaced with the new Resource Management API, currently available in a preview release.</span></span>  <span data-ttu-id="0c047-105">See the [Azure Resource Management documentation](http://azure-sdk-for-python.readthedocs.org/) for details on using the new Resource Management API from Python.</span><span class="sxs-lookup"><span data-stu-id="0c047-105">See the [Azure Resource Management documentation](http://azure-sdk-for-python.readthedocs.org/) for details on using the new Resource Management API from Python.</span></span>
> 
> 

<span data-ttu-id="0c047-106">This guide shows you how to programmatically perform common service management tasks from Python.</span><span class="sxs-lookup"><span data-stu-id="0c047-106">This guide shows you how to programmatically perform common service management tasks from Python.</span></span> <span data-ttu-id="0c047-107">The **ServiceManagementService** class in the [Azure SDK for Python](https://github.com/Azure/azure-sdk-for-python) supports programmatic access to much of the service management-related functionality that is available in the [Azure classic portal][management-portal] (such as **creating, updating, and deleting cloud services, deployments, data management services, and virtual machines**).</span><span class="sxs-lookup"><span data-stu-id="0c047-107">The **ServiceManagementService** class in the [Azure SDK for Python](https://github.com/Azure/azure-sdk-for-python) supports programmatic access to much of the service management-related functionality that is available in the [Azure classic portal][management-portal] (such as **creating, updating, and deleting cloud services, deployments, data management services, and virtual machines**).</span></span> <span data-ttu-id="0c047-108">This functionality can be useful in building applications that need programmatic access to service management.</span><span class="sxs-lookup"><span data-stu-id="0c047-108">This functionality can be useful in building applications that need programmatic access to service management.</span></span>

## <span data-ttu-id="0c047-109"><a name="WhatIs"> </a>What is Service Management</span><span class="sxs-lookup"><span data-stu-id="0c047-109"><a name="WhatIs"> </a>What is Service Management</span></span>
<span data-ttu-id="0c047-110">The Service Management API provides programmatic access to much of the service management functionality available through the [Azure classic portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="0c047-110">The Service Management API provides programmatic access to much of the service management functionality available through the [Azure classic portal][management-portal].</span></span> <span data-ttu-id="0c047-111">The Azure SDK for Python allows you to manage your cloud services and storage accounts.</span><span class="sxs-lookup"><span data-stu-id="0c047-111">The Azure SDK for Python allows you to manage your cloud services and storage accounts.</span></span>

<span data-ttu-id="0c047-112">To use the Service Management API, you need to [create an Azure account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0c047-112">To use the Service Management API, you need to [create an Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <span data-ttu-id="0c047-113"><a name="Concepts"> </a>Concepts</span><span class="sxs-lookup"><span data-stu-id="0c047-113"><a name="Concepts"> </a>Concepts</span></span>
<span data-ttu-id="0c047-114">The Azure SDK for Python wraps the [Azure Service Management API][svc-mgmt-rest-api], which is a REST API.</span><span class="sxs-lookup"><span data-stu-id="0c047-114">The Azure SDK for Python wraps the [Azure Service Management API][svc-mgmt-rest-api], which is a REST API.</span></span> <span data-ttu-id="0c047-115">All API operations are performed over SSL and mutually authenticated using X.509 v3 certificates.</span><span class="sxs-lookup"><span data-stu-id="0c047-115">All API operations are performed over SSL and mutually authenticated using X.509 v3 certificates.</span></span> <span data-ttu-id="0c047-116">The management service may be accessed from within a service running in Azure, or directly over the Internet from any application that can send an HTTPS request and receive an HTTPS response.</span><span class="sxs-lookup"><span data-stu-id="0c047-116">The management service may be accessed from within a service running in Azure, or directly over the Internet from any application that can send an HTTPS request and receive an HTTPS response.</span></span>

## <span data-ttu-id="0c047-117"><a name="Installation"> </a>Installation</span><span class="sxs-lookup"><span data-stu-id="0c047-117"><a name="Installation"> </a>Installation</span></span>
<span data-ttu-id="0c047-118">All the features described in this article are available in the `azure-servicemanagement-legacy` package, which you can install using pip.</span><span class="sxs-lookup"><span data-stu-id="0c047-118">All the features described in this article are available in the `azure-servicemanagement-legacy` package, which you can install using pip.</span></span> <span data-ttu-id="0c047-119">For more information about installation (for example, if you are new to Python), see this article: [Installing Python and the Azure SDK](../python-how-to-install.md)</span><span class="sxs-lookup"><span data-stu-id="0c047-119">For more information about installation (for example, if you are new to Python), see this article: [Installing Python and the Azure SDK](../python-how-to-install.md)</span></span>

## <span data-ttu-id="0c047-120"><a name="Connect"> </a>How to: Connect to service management</span><span class="sxs-lookup"><span data-stu-id="0c047-120"><a name="Connect"> </a>How to: Connect to service management</span></span>
<span data-ttu-id="0c047-121">To connect to the Service Management endpoint, you need your Azure subscription ID and a valid management certificate.</span><span class="sxs-lookup"><span data-stu-id="0c047-121">To connect to the Service Management endpoint, you need your Azure subscription ID and a valid management certificate.</span></span> <span data-ttu-id="0c047-122">You can obtain your subscription ID through the [Azure classic portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="0c047-122">You can obtain your subscription ID through the [Azure classic portal][management-portal].</span></span>

> [!NOTE]
> <span data-ttu-id="0c047-123">It is now possible to use certificates created with OpenSSL when running on Windows.</span><span class="sxs-lookup"><span data-stu-id="0c047-123">It is now possible to use certificates created with OpenSSL when running on Windows.</span></span>  <span data-ttu-id="0c047-124">It requires Python 2.7.4 or later.</span><span class="sxs-lookup"><span data-stu-id="0c047-124">It requires Python 2.7.4 or later.</span></span> <span data-ttu-id="0c047-125">We recommend users to use OpenSSL instead of .pfx, since support for .pfx certificates will likely be removed in the future.</span><span class="sxs-lookup"><span data-stu-id="0c047-125">We recommend users to use OpenSSL instead of .pfx, since support for .pfx certificates will likely be removed in the future.</span></span>
> 
> 

### <a name="management-certificates-on-windowsmaclinux-openssl"></a><span data-ttu-id="0c047-126">Management certificates on Windows/Mac/Linux (OpenSSL)</span><span class="sxs-lookup"><span data-stu-id="0c047-126">Management certificates on Windows/Mac/Linux (OpenSSL)</span></span>
<span data-ttu-id="0c047-127">You can use [OpenSSL](http://www.openssl.org/) to create your management certificate.</span><span class="sxs-lookup"><span data-stu-id="0c047-127">You can use [OpenSSL](http://www.openssl.org/) to create your management certificate.</span></span>  <span data-ttu-id="0c047-128">You actually need to create two certificates, one for the server (a `.cer` file) and one for the client (a `.pem` file).</span><span class="sxs-lookup"><span data-stu-id="0c047-128">You actually need to create two certificates, one for the server (a `.cer` file) and one for the client (a `.pem` file).</span></span> <span data-ttu-id="0c047-129">To create the `.pem` file, execute:</span><span class="sxs-lookup"><span data-stu-id="0c047-129">To create the `.pem` file, execute:</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="0c047-130">To create the `.cer` certificate, execute:</span><span class="sxs-lookup"><span data-stu-id="0c047-130">To create the `.cer` certificate, execute:</span></span>

    openssl x509 -inform pem -in mycert.pem -outform der -out mycert.cer

<span data-ttu-id="0c047-131">For more information about Azure certificates, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="0c047-131">For more information about Azure certificates, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="0c047-132">For a complete description of OpenSSL parameters, see the documentation at [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span><span class="sxs-lookup"><span data-stu-id="0c047-132">For a complete description of OpenSSL parameters, see the documentation at [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span></span>

<span data-ttu-id="0c047-133">After you have created these files, you need to upload the `.cer` file to Azure via the "Upload" action of the "Settings" tab of the [Azure classic portal][management-portal], and you need to make note of where you saved the `.pem` file.</span><span class="sxs-lookup"><span data-stu-id="0c047-133">After you have created these files, you need to upload the `.cer` file to Azure via the "Upload" action of the "Settings" tab of the [Azure classic portal][management-portal], and you need to make note of where you saved the `.pem` file.</span></span>

<span data-ttu-id="0c047-134">After you have obtained your subscription ID, created a certificate, and uploaded the `.cer` file to Azure, you can connect to the Azure management endpoint by passing the subscription id and the path to the `.pem` file to **ServiceManagementService**:</span><span class="sxs-lookup"><span data-stu-id="0c047-134">After you have obtained your subscription ID, created a certificate, and uploaded the `.cer` file to Azure, you can connect to the Azure management endpoint by passing the subscription id and the path to the `.pem` file to **ServiceManagementService**:</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = '<path_to_.pem_certificate>'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="0c047-135">In the preceding example, `sms` is a **ServiceManagementService** object.</span><span class="sxs-lookup"><span data-stu-id="0c047-135">In the preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="0c047-136">The **ServiceManagementService** class is the primary class used to manage Azure services.</span><span class="sxs-lookup"><span data-stu-id="0c047-136">The **ServiceManagementService** class is the primary class used to manage Azure services.</span></span>

### <a name="management-certificates-on-windows-makecert"></a><span data-ttu-id="0c047-137">Management certificates on Windows (MakeCert)</span><span class="sxs-lookup"><span data-stu-id="0c047-137">Management certificates on Windows (MakeCert)</span></span>
<span data-ttu-id="0c047-138">You can create a self-signed management certificate on your machine using `makecert.exe`.</span><span class="sxs-lookup"><span data-stu-id="0c047-138">You can create a self-signed management certificate on your machine using `makecert.exe`.</span></span>  <span data-ttu-id="0c047-139">Open a **Visual Studio command prompt** as an **administrator** and use the following command, replacing *AzureCertificate* with the certificate name you would like to use.</span><span class="sxs-lookup"><span data-stu-id="0c047-139">Open a **Visual Studio command prompt** as an **administrator** and use the following command, replacing *AzureCertificate* with the certificate name you would like to use.</span></span>

    makecert -sky exchange -r -n "CN=AzureCertificate" -pe -a sha1 -len 2048 -ss My "AzureCertificate.cer"

<span data-ttu-id="0c047-140">The command creates the `.cer` file, and installs it in the **Personal** certificate store.</span><span class="sxs-lookup"><span data-stu-id="0c047-140">The command creates the `.cer` file, and installs it in the **Personal** certificate store.</span></span> <span data-ttu-id="0c047-141">For more information, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="0c047-141">For more information, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span>

<span data-ttu-id="0c047-142">After you have created the certificate, you need to upload the `.cer` file to Azure via the "Upload" action of the "Settings" tab of the [Azure classic portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="0c047-142">After you have created the certificate, you need to upload the `.cer` file to Azure via the "Upload" action of the "Settings" tab of the [Azure classic portal][management-portal].</span></span>

<span data-ttu-id="0c047-143">After you have obtained your subscription ID, created a certificate, and uploaded the `.cer` file to Azure, you can connect to the Azure management endpoint by passing the subscription id and the location of the certificate in your **Personal** certificate store to **ServiceManagementService** (again, replace *AzureCertificate* with the name of your certificate):</span><span class="sxs-lookup"><span data-stu-id="0c047-143">After you have obtained your subscription ID, created a certificate, and uploaded the `.cer` file to Azure, you can connect to the Azure management endpoint by passing the subscription id and the location of the certificate in your **Personal** certificate store to **ServiceManagementService** (again, replace *AzureCertificate* with the name of your certificate):</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = 'CURRENT_USER\\my\\AzureCertificate'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="0c047-144">In the preceding example, `sms` is a **ServiceManagementService** object.</span><span class="sxs-lookup"><span data-stu-id="0c047-144">In the preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="0c047-145">The **ServiceManagementService** class is the primary class used to manage Azure services.</span><span class="sxs-lookup"><span data-stu-id="0c047-145">The **ServiceManagementService** class is the primary class used to manage Azure services.</span></span>

## <span data-ttu-id="0c047-146"><a name="ListAvailableLocations"> </a>How to: List available locations</span><span class="sxs-lookup"><span data-stu-id="0c047-146"><a name="ListAvailableLocations"> </a>How to: List available locations</span></span>
<span data-ttu-id="0c047-147">To list the locations that are available for hosting services, use the **list\_locations** method:</span><span class="sxs-lookup"><span data-stu-id="0c047-147">To list the locations that are available for hosting services, use the **list\_locations** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_locations()
    for location in result:
        print(location.name)

<span data-ttu-id="0c047-148">When you create a cloud service or storage service you need to provide a valid location.</span><span class="sxs-lookup"><span data-stu-id="0c047-148">When you create a cloud service or storage service you need to provide a valid location.</span></span> <span data-ttu-id="0c047-149">The **list\_locations** method always returns an up-to-date list of the currently available locations.</span><span class="sxs-lookup"><span data-stu-id="0c047-149">The **list\_locations** method always returns an up-to-date list of the currently available locations.</span></span> <span data-ttu-id="0c047-150">As of this writing, the available locations are:</span><span class="sxs-lookup"><span data-stu-id="0c047-150">As of this writing, the available locations are:</span></span>

* <span data-ttu-id="0c047-151">West Europe</span><span class="sxs-lookup"><span data-stu-id="0c047-151">West Europe</span></span>
* <span data-ttu-id="0c047-152">North Europe</span><span class="sxs-lookup"><span data-stu-id="0c047-152">North Europe</span></span>
* <span data-ttu-id="0c047-153">Southeast Asia</span><span class="sxs-lookup"><span data-stu-id="0c047-153">Southeast Asia</span></span>
* <span data-ttu-id="0c047-154">East Asia</span><span class="sxs-lookup"><span data-stu-id="0c047-154">East Asia</span></span>
* <span data-ttu-id="0c047-155">Central US</span><span class="sxs-lookup"><span data-stu-id="0c047-155">Central US</span></span>
* <span data-ttu-id="0c047-156">North Central US</span><span class="sxs-lookup"><span data-stu-id="0c047-156">North Central US</span></span>
* <span data-ttu-id="0c047-157">South Central US</span><span class="sxs-lookup"><span data-stu-id="0c047-157">South Central US</span></span>
* <span data-ttu-id="0c047-158">West US</span><span class="sxs-lookup"><span data-stu-id="0c047-158">West US</span></span>
* <span data-ttu-id="0c047-159">East US</span><span class="sxs-lookup"><span data-stu-id="0c047-159">East US</span></span>
* <span data-ttu-id="0c047-160">Japan East</span><span class="sxs-lookup"><span data-stu-id="0c047-160">Japan East</span></span>
* <span data-ttu-id="0c047-161">Japan West</span><span class="sxs-lookup"><span data-stu-id="0c047-161">Japan West</span></span>
* <span data-ttu-id="0c047-162">Brazil South</span><span class="sxs-lookup"><span data-stu-id="0c047-162">Brazil South</span></span>
* <span data-ttu-id="0c047-163">Australia East</span><span class="sxs-lookup"><span data-stu-id="0c047-163">Australia East</span></span>
* <span data-ttu-id="0c047-164">Australia Southeast</span><span class="sxs-lookup"><span data-stu-id="0c047-164">Australia Southeast</span></span>

## <span data-ttu-id="0c047-165"><a name="CreateCloudService"> </a>How to: Create a cloud service</span><span class="sxs-lookup"><span data-stu-id="0c047-165"><a name="CreateCloudService"> </a>How to: Create a cloud service</span></span>
<span data-ttu-id="0c047-166">When you create an application and run it in Azure, the code and configuration together are called an Azure [cloud service][cloud service] (known as a *hosted service* in earlier Azure releases).</span><span class="sxs-lookup"><span data-stu-id="0c047-166">When you create an application and run it in Azure, the code and configuration together are called an Azure [cloud service][cloud service] (known as a *hosted service* in earlier Azure releases).</span></span> <span data-ttu-id="0c047-167">The **create\_hosted\_service** method allows you to create a new hosted service by providing a hosted service name (which must be unique in Azure), a label (automatically encoded to base64), a description, and a location.</span><span class="sxs-lookup"><span data-stu-id="0c047-167">The **create\_hosted\_service** method allows you to create a new hosted service by providing a hosted service name (which must be unique in Azure), a label (automatically encoded to base64), a description, and a location.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myhostedservice'
    label = 'myhostedservice'
    desc = 'my hosted service'
    location = 'West US'

    sms.create_hosted_service(name, label, desc, location)

<span data-ttu-id="0c047-168">You can list all the hosted services for your subscription with the **list\_hosted\_services** method:</span><span class="sxs-lookup"><span data-stu-id="0c047-168">You can list all the hosted services for your subscription with the **list\_hosted\_services** method:</span></span>

    result = sms.list_hosted_services()

    for hosted_service in result:
        print('Service name: ' + hosted_service.service_name)
        print('Management URL: ' + hosted_service.url)
        print('Location: ' + hosted_service.hosted_service_properties.location)
        print('')

<span data-ttu-id="0c047-169">If you want to get information about a particular hosted service, you can do so by passing the hosted service name to the **get\_hosted\_service\_properties** method:</span><span class="sxs-lookup"><span data-stu-id="0c047-169">If you want to get information about a particular hosted service, you can do so by passing the hosted service name to the **get\_hosted\_service\_properties** method:</span></span>

    hosted_service = sms.get_hosted_service_properties('myhostedservice')

    print('Service name: ' + hosted_service.service_name)
    print('Management URL: ' + hosted_service.url)
    print('Location: ' + hosted_service.hosted_service_properties.location)

<span data-ttu-id="0c047-170">After you have created a cloud service, you can deploy your code to the service with the **create\_deployment** method.</span><span class="sxs-lookup"><span data-stu-id="0c047-170">After you have created a cloud service, you can deploy your code to the service with the **create\_deployment** method.</span></span>

## <span data-ttu-id="0c047-171"><a name="DeleteCloudService"> </a>How to: Delete a cloud service</span><span class="sxs-lookup"><span data-stu-id="0c047-171"><a name="DeleteCloudService"> </a>How to: Delete a cloud service</span></span>
<span data-ttu-id="0c047-172">You can delete a cloud service by passing the service name to the **delete\_hosted\_service** method:</span><span class="sxs-lookup"><span data-stu-id="0c047-172">You can delete a cloud service by passing the service name to the **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service('myhostedservice')

<span data-ttu-id="0c047-173">Before you can delete a service, all deployments for the service must first be deleted.</span><span class="sxs-lookup"><span data-stu-id="0c047-173">Before you can delete a service, all deployments for the service must first be deleted.</span></span> <span data-ttu-id="0c047-174">(See [How to: Delete a deployment](#DeleteDeployment) for details.)</span><span class="sxs-lookup"><span data-stu-id="0c047-174">(See [How to: Delete a deployment](#DeleteDeployment) for details.)</span></span>

## <span data-ttu-id="0c047-175"><a name="DeleteDeployment"> </a>How to: Delete a deployment</span><span class="sxs-lookup"><span data-stu-id="0c047-175"><a name="DeleteDeployment"> </a>How to: Delete a deployment</span></span>
<span data-ttu-id="0c047-176">To delete a deployment, use the **delete\_deployment** method.</span><span class="sxs-lookup"><span data-stu-id="0c047-176">To delete a deployment, use the **delete\_deployment** method.</span></span> <span data-ttu-id="0c047-177">The following example shows how to delete a deployment named `v1`.</span><span class="sxs-lookup"><span data-stu-id="0c047-177">The following example shows how to delete a deployment named `v1`.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment('myhostedservice', 'v1')

## <span data-ttu-id="0c047-178"><a name="CreateStorageService"> </a>How to: Create a storage service</span><span class="sxs-lookup"><span data-stu-id="0c047-178"><a name="CreateStorageService"> </a>How to: Create a storage service</span></span>
<span data-ttu-id="0c047-179">A [storage service](../storage/storage-create-storage-account.md) gives you access to Azure [Blobs](../storage/storage-python-how-to-use-blob-storage.md), [Tables](../storage/storage-python-how-to-use-table-storage.md), and [Queues](../storage/storage-python-how-to-use-queue-storage.md).</span><span class="sxs-lookup"><span data-stu-id="0c047-179">A [storage service](../storage/storage-create-storage-account.md) gives you access to Azure [Blobs](../storage/storage-python-how-to-use-blob-storage.md), [Tables](../storage/storage-python-how-to-use-table-storage.md), and [Queues](../storage/storage-python-how-to-use-queue-storage.md).</span></span> <span data-ttu-id="0c047-180">To create a storage service, you need a name for the service (between 3 and 24 lowercase characters and unique within Azure), a description, a label (up to 100 characters, automatically encoded to base64), and a location.</span><span class="sxs-lookup"><span data-stu-id="0c047-180">To create a storage service, you need a name for the service (between 3 and 24 lowercase characters and unique within Azure), a description, a label (up to 100 characters, automatically encoded to base64), and a location.</span></span> <span data-ttu-id="0c047-181">The following example shows how to create a storage service by specifying a location.</span><span class="sxs-lookup"><span data-stu-id="0c047-181">The following example shows how to create a storage service by specifying a location.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mystorageaccount'
    label = 'mystorageaccount'
    location = 'West US'
    desc = 'My storage account description.'

    result = sms.create_storage_account(name, desc, label, location=location)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

<span data-ttu-id="0c047-182">Note in the preceding example that the status of the **create\_storage\_account** operation can be retrieved by passing the result returned by **create\_storage\_account** to the **get\_operation\_status** method.</span><span class="sxs-lookup"><span data-stu-id="0c047-182">Note in the preceding example that the status of the **create\_storage\_account** operation can be retrieved by passing the result returned by **create\_storage\_account** to the **get\_operation\_status** method.</span></span>  

<span data-ttu-id="0c047-183">You can list your storage accounts and their properties with the **list\_storage\_accounts** method:</span><span class="sxs-lookup"><span data-stu-id="0c047-183">You can list your storage accounts and their properties with the **list\_storage\_accounts** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_storage_accounts()
    for account in result:
        print('Service name: ' + account.service_name)
        print('Location: ' + account.storage_service_properties.location)
        print('')

## <span data-ttu-id="0c047-184"><a name="DeleteStorageService"> </a>How to: Delete a storage service</span><span class="sxs-lookup"><span data-stu-id="0c047-184"><a name="DeleteStorageService"> </a>How to: Delete a storage service</span></span>
<span data-ttu-id="0c047-185">You can delete a storage service by passing the storage service name to the **delete\_storage\_account** method.</span><span class="sxs-lookup"><span data-stu-id="0c047-185">You can delete a storage service by passing the storage service name to the **delete\_storage\_account** method.</span></span> <span data-ttu-id="0c047-186">Deleting a storage service deletes all data stored in the service (blobs, tables, and queues).</span><span class="sxs-lookup"><span data-stu-id="0c047-186">Deleting a storage service deletes all data stored in the service (blobs, tables, and queues).</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_storage_account('mystorageaccount')

## <span data-ttu-id="0c047-187"><a name="ListOperatingSystems"> </a>How to: List available operating systems</span><span class="sxs-lookup"><span data-stu-id="0c047-187"><a name="ListOperatingSystems"> </a>How to: List available operating systems</span></span>
<span data-ttu-id="0c047-188">To list the operating systems that are available for hosting services, use the **list\_operating\_systems** method:</span><span class="sxs-lookup"><span data-stu-id="0c047-188">To list the operating systems that are available for hosting services, use the **list\_operating\_systems** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_operating_systems()

    for os in result:
        print('OS: ' + os.label)
        print('Family: ' + os.family_label)
        print('Active: ' + str(os.is_active))

<span data-ttu-id="0c047-189">Alternatively, you can use the **list\_operating\_system\_families** method, which groups the operating systems by family:</span><span class="sxs-lookup"><span data-stu-id="0c047-189">Alternatively, you can use the **list\_operating\_system\_families** method, which groups the operating systems by family:</span></span>

    result = sms.list_operating_system_families()

    for family in result:
        print('Family: ' + family.label)
        for os in family.operating_systems:
            if os.is_active:
                print('OS: ' + os.label)
                print('Version: ' + os.version)
        print('')

## <span data-ttu-id="0c047-190"><a name="CreateVMImage"> </a>How to: Create an operating system image</span><span class="sxs-lookup"><span data-stu-id="0c047-190"><a name="CreateVMImage"> </a>How to: Create an operating system image</span></span>
<span data-ttu-id="0c047-191">To add an operating system image to the image repository, use the **add\_os\_image** method:</span><span class="sxs-lookup"><span data-stu-id="0c047-191">To add an operating system image to the image repository, use the **add\_os\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mycentos'
    label = 'mycentos'
    os = 'Linux' # Linux or Windows
    media_link = 'url_to_storage_blob_for_source_image_vhd'

    result = sms.add_os_image(label, media_link, name, os)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

<span data-ttu-id="0c047-192">To list the operating system images that are available, use the **list\_os\_images** method.</span><span class="sxs-lookup"><span data-stu-id="0c047-192">To list the operating system images that are available, use the **list\_os\_images** method.</span></span> <span data-ttu-id="0c047-193">It includes all platform images and user images:</span><span class="sxs-lookup"><span data-stu-id="0c047-193">It includes all platform images and user images:</span></span>

    result = sms.list_os_images()

    for image in result:
        print('Name: ' + image.name)
        print('Label: ' + image.label)
        print('OS: ' + image.os)
        print('Category: ' + image.category)
        print('Description: ' + image.description)
        print('Location: ' + image.location)
        print('Media link: ' + image.media_link)
        print('')

## <span data-ttu-id="0c047-194"><a name="DeleteVMImage"> </a>How to: Delete an operating system image</span><span class="sxs-lookup"><span data-stu-id="0c047-194"><a name="DeleteVMImage"> </a>How to: Delete an operating system image</span></span>
<span data-ttu-id="0c047-195">To delete a user image, use the **delete\_os\_image** method:</span><span class="sxs-lookup"><span data-stu-id="0c047-195">To delete a user image, use the **delete\_os\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.delete_os_image('mycentos')

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

## <span data-ttu-id="0c047-196"><a name="CreateVM"> </a>How to: Create a virtual machine</span><span class="sxs-lookup"><span data-stu-id="0c047-196"><a name="CreateVM"> </a>How to: Create a virtual machine</span></span>
<span data-ttu-id="0c047-197">To create a virtual machine, you first need to create a [cloud service](#CreateCloudService).</span><span class="sxs-lookup"><span data-stu-id="0c047-197">To create a virtual machine, you first need to create a [cloud service](#CreateCloudService).</span></span>  <span data-ttu-id="0c047-198">Then create the virtual machine deployment using the **create\_virtual\_machine\_deployment** method:</span><span class="sxs-lookup"><span data-stu-id="0c047-198">Then create the virtual machine deployment using the **create\_virtual\_machine\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set the location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    # Name of an os image as returned by list_os_images
    image_name = 'OpenLogic__OpenLogic-CentOS-62-20120531-en-us-30GB.vhd'

    # Destination storage account container/blob where the VM disk
    # will be created
    media_link = 'url_to_target_storage_blob_for_vm_hd'

    # Linux VM configuration, you can use WindowsConfigurationSet
    # for a Windows VM instead
    linux_config = LinuxConfigurationSet('myhostname', 'myuser', 'mypassword', True)

    os_hd = OSVirtualHardDisk(image_name, media_link)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=os_hd,
        role_size='Small')

## <span data-ttu-id="0c047-199"><a name="DeleteVM"> </a>How to: Delete a virtual machine</span><span class="sxs-lookup"><span data-stu-id="0c047-199"><a name="DeleteVM"> </a>How to: Delete a virtual machine</span></span>
<span data-ttu-id="0c047-200">To delete a virtual machine, you first delete the deployment using the **delete\_deployment** method:</span><span class="sxs-lookup"><span data-stu-id="0c047-200">To delete a virtual machine, you first delete the deployment using the **delete\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment(service_name='myvm',
        deployment_name='myvm')

<span data-ttu-id="0c047-201">The cloud service can then be deleted using the **delete\_hosted\_service** method:</span><span class="sxs-lookup"><span data-stu-id="0c047-201">The cloud service can then be deleted using the **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service(service_name='myvm')

## <a name="how-to-create-a-virtual-machine-from-a-captured-virtual-machine-image"></a><span data-ttu-id="0c047-202">How To: Create a Virtual Machine from a Captured Virtual Machine Image</span><span class="sxs-lookup"><span data-stu-id="0c047-202">How To: Create a Virtual Machine from a Captured Virtual Machine Image</span></span>
<span data-ttu-id="0c047-203">To capture a VM image, you first call the **capture\_vm\_image** method:</span><span class="sxs-lookup"><span data-stu-id="0c047-203">To capture a VM image, you first call the **capture\_vm\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    # replace the below three parameters with actual values
    hosted_service_name = 'hs1'
    deployment_name = 'dep1'
    vm_name = 'vm1'

    image_name = vm_name + 'image'
    image = CaptureRoleAsVMImage    ('Specialized',
        image_name,
        image_name + 'label',
        image_name + 'description',
        'english',
        'mygroup')

    result = sms.capture_vm_image(
            hosted_service_name,
            deployment_name,
            vm_name,
            image
        )

<span data-ttu-id="0c047-204">Next, to make sure that you have successfully captured the image, use the **list\_vm\_images** api, and make sure your image is displayed in the results:</span><span class="sxs-lookup"><span data-stu-id="0c047-204">Next, to make sure that you have successfully captured the image, use the **list\_vm\_images** api, and make sure your image is displayed in the results:</span></span>

    images = sms.list_vm_images()

<span data-ttu-id="0c047-205">To finally create the virtual machine using the captured image, use the **create\_virtual\_machine\_deployment** method as before, but this time pass in the vm_image_name instead</span><span class="sxs-lookup"><span data-stu-id="0c047-205">To finally create the virtual machine using the captured image, use the **create\_virtual\_machine\_deployment** method as before, but this time pass in the vm_image_name instead</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set the location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=None,
        role_size='Small',
        vm_image_name = image_name)

<span data-ttu-id="0c047-206">To learn more about how to capture a Linux Virtual Machine, see [How to Capture a Linux Virtual Machine.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="0c047-206">To learn more about how to capture a Linux Virtual Machine, see [How to Capture a Linux Virtual Machine.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="0c047-207">To learn more about how to capture a Windows Virtual Machine, see [How to Capture a Windows Virtual Machine.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="0c047-207">To learn more about how to capture a Windows Virtual Machine, see [How to Capture a Windows Virtual Machine.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="0c047-208"><a name="What's Next"> </a>Next Steps</span><span class="sxs-lookup"><span data-stu-id="0c047-208"><a name="What's Next"> </a>Next Steps</span></span>
<span data-ttu-id="0c047-209">Now that you've learned the basics of service management, you can access the [Complete API reference documentation for the Azure Python SDK](http://azure-sdk-for-python.readthedocs.org/) and perform complex tasks easily to manage your python application.</span><span class="sxs-lookup"><span data-stu-id="0c047-209">Now that you've learned the basics of service management, you can access the [Complete API reference documentation for the Azure Python SDK](http://azure-sdk-for-python.readthedocs.org/) and perform complex tasks easily to manage your python application.</span></span>

<span data-ttu-id="0c047-210">For more information, see the [Python Developer Center](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="0c047-210">For more information, see the [Python Developer Center](/develop/python/).</span></span>

[What is Service Management]: #WhatIs
[Concepts]: #Concepts
[How to: Connect to service management]: #Connect
[How to: List available locations]: #ListAvailableLocations
[How to: Create a cloud service]: #CreateCloudService
[How to: Delete a cloud service]: #DeleteCloudService
[How to: Create a deployment]: #CreateDeployment
[How to: Update a deployment]: #UpdateDeployment
[How to: Move deployments between staging and production]: #MoveDeployments
[How to: Delete a deployment]: #DeleteDeployment
[How to: Create a storage service]: #CreateStorageService
[How to: Delete a storage service]: #DeleteStorageService
[How to: List available operating systems]: #ListOperatingSystems
[How to: Create an operating system image]: #CreateVMImage
[How to: Delete an operating system image]: #DeleteVMImage
[How to: Create a virtual machine]: #CreateVM
[How to: Delete a virtual machine]: #DeleteVM
[Next Steps]: #NextSteps
[management-portal]: https://manage.windowsazure.com/
[svc-mgmt-rest-api]: http://msdn.microsoft.com/library/windowsazure/ee460799.aspx


[cloud service]:/services/cloud-services/

