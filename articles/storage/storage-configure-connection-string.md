---
title: Configure a connection string for Azure Storage | Microsoft Docs
description: Configure a connection string for an Azure storage account. A connection string contains the information needed to authenticate access to a storage account from your application at runtime.
services: storage
documentationcenter: ''
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: ecb0acb5-90a9-4eb2-93e6-e9860eda5e53
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: marsma
ms.openlocfilehash: 01aa506e2b47fc29a70592e670a206a2b74248a4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563088"
---
# <a name="configure-azure-storage-connection-strings"></a><span data-ttu-id="4e107-104">Configure Azure Storage connection strings</span><span class="sxs-lookup"><span data-stu-id="4e107-104">Configure Azure Storage connection strings</span></span>

<span data-ttu-id="4e107-105">A connection string includes the authentication information required for your application to access data in an Azure Storage account at runtime.</span><span class="sxs-lookup"><span data-stu-id="4e107-105">A connection string includes the authentication information required for your application to access data in an Azure Storage account at runtime.</span></span> <span data-ttu-id="4e107-106">You can configure connection strings to:</span><span class="sxs-lookup"><span data-stu-id="4e107-106">You can configure connection strings to:</span></span>

* <span data-ttu-id="4e107-107">Connect to the Azure storage emulator.</span><span class="sxs-lookup"><span data-stu-id="4e107-107">Connect to the Azure storage emulator.</span></span>
* <span data-ttu-id="4e107-108">Access a storage account in Azure.</span><span class="sxs-lookup"><span data-stu-id="4e107-108">Access a storage account in Azure.</span></span>
* <span data-ttu-id="4e107-109">Access specified resources in Azure via a shared access signature (SAS).</span><span class="sxs-lookup"><span data-stu-id="4e107-109">Access specified resources in Azure via a shared access signature (SAS).</span></span>

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

## <a name="storing-your-connection-string"></a><span data-ttu-id="4e107-110">Storing your connection string</span><span class="sxs-lookup"><span data-stu-id="4e107-110">Storing your connection string</span></span>
<span data-ttu-id="4e107-111">Your application needs to access the connection string at runtime to authenticate requests made to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="4e107-111">Your application needs to access the connection string at runtime to authenticate requests made to Azure Storage.</span></span> <span data-ttu-id="4e107-112">You have several options for storing your connection string:</span><span class="sxs-lookup"><span data-stu-id="4e107-112">You have several options for storing your connection string:</span></span>

* <span data-ttu-id="4e107-113">An application running on the desktop or on a device can store the connection string in an **app.config** or **web.config** file.</span><span class="sxs-lookup"><span data-stu-id="4e107-113">An application running on the desktop or on a device can store the connection string in an **app.config** or **web.config** file.</span></span> <span data-ttu-id="4e107-114">Add the connection string to the **AppSettings** section in these files.</span><span class="sxs-lookup"><span data-stu-id="4e107-114">Add the connection string to the **AppSettings** section in these files.</span></span>
* <span data-ttu-id="4e107-115">An application running in an Azure cloud service can store the connection string in the [Azure service configuration schema (.cscfg) file](https://msdn.microsoft.com/library/ee758710.aspx).</span><span class="sxs-lookup"><span data-stu-id="4e107-115">An application running in an Azure cloud service can store the connection string in the [Azure service configuration schema (.cscfg) file](https://msdn.microsoft.com/library/ee758710.aspx).</span></span> <span data-ttu-id="4e107-116">Add the connection string to the **ConfigurationSettings** section of the service configuration file.</span><span class="sxs-lookup"><span data-stu-id="4e107-116">Add the connection string to the **ConfigurationSettings** section of the service configuration file.</span></span>
* <span data-ttu-id="4e107-117">You can use your connection string directly in your code.</span><span class="sxs-lookup"><span data-stu-id="4e107-117">You can use your connection string directly in your code.</span></span> <span data-ttu-id="4e107-118">However, we recommend that you store your connection string in a configuration file in most scenarios.</span><span class="sxs-lookup"><span data-stu-id="4e107-118">However, we recommend that you store your connection string in a configuration file in most scenarios.</span></span>

<span data-ttu-id="4e107-119">Storing your connection string in a configuration file makes it easy to update the connection string to switch between the storage emulator and an Azure storage account in the cloud.</span><span class="sxs-lookup"><span data-stu-id="4e107-119">Storing your connection string in a configuration file makes it easy to update the connection string to switch between the storage emulator and an Azure storage account in the cloud.</span></span> <span data-ttu-id="4e107-120">You only need to edit the connection string to point to your target environment.</span><span class="sxs-lookup"><span data-stu-id="4e107-120">You only need to edit the connection string to point to your target environment.</span></span>

<span data-ttu-id="4e107-121">You can use the [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) to access your connection string at runtime regardless of where your application is running.</span><span class="sxs-lookup"><span data-stu-id="4e107-121">You can use the [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) to access your connection string at runtime regardless of where your application is running.</span></span>

## <a name="create-a-connection-string-for-the-storage-emulator"></a><span data-ttu-id="4e107-122">Create a connection string for the storage emulator</span><span class="sxs-lookup"><span data-stu-id="4e107-122">Create a connection string for the storage emulator</span></span>
[!INCLUDE [storage-emulator-connection-string-include](../../includes/storage-emulator-connection-string-include.md)]

<span data-ttu-id="4e107-123">For more information about the storage emulator, see [Use the Azure storage emulator for development and testing](storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="4e107-123">For more information about the storage emulator, see [Use the Azure storage emulator for development and testing](storage-use-emulator.md).</span></span>

## <a name="create-a-connection-string-for-an-azure-storage-account"></a><span data-ttu-id="4e107-124">Create a connection string for an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="4e107-124">Create a connection string for an Azure storage account</span></span>
<span data-ttu-id="4e107-125">To create a connection string for your Azure storage account, use the following format.</span><span class="sxs-lookup"><span data-stu-id="4e107-125">To create a connection string for your Azure storage account, use the following format.</span></span> <span data-ttu-id="4e107-126">Indicate whether you want to connect to the storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with the name of your storage account, and replace `myAccountKey` with your account access key:</span><span class="sxs-lookup"><span data-stu-id="4e107-126">Indicate whether you want to connect to the storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with the name of your storage account, and replace `myAccountKey` with your account access key:</span></span>

`DefaultEndpointsProtocol=[http|https];AccountName=myAccountName;AccountKey=myAccountKey`

<span data-ttu-id="4e107-127">For example, your connection string might look similar to:</span><span class="sxs-lookup"><span data-stu-id="4e107-127">For example, your connection string might look similar to:</span></span>

`DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=<account-key>`

<span data-ttu-id="4e107-128">Although Azure Storage supports both HTTP and HTTPS in a connection string, *HTTPS is highly recommended*.</span><span class="sxs-lookup"><span data-stu-id="4e107-128">Although Azure Storage supports both HTTP and HTTPS in a connection string, *HTTPS is highly recommended*.</span></span>

> [!TIP]
> <span data-ttu-id="4e107-129">You can find your storage account's connection strings in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4e107-129">You can find your storage account's connection strings in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4e107-130">Navigate to **SETTINGS** > **Access keys** in your storage account's menu blade to see connection strings for both primary and secondary access keys.</span><span class="sxs-lookup"><span data-stu-id="4e107-130">Navigate to **SETTINGS** > **Access keys** in your storage account's menu blade to see connection strings for both primary and secondary access keys.</span></span>
>

## <a name="create-a-connection-string-using-a-shared-access-signature"></a><span data-ttu-id="4e107-131">Create a connection string using a shared access signature</span><span class="sxs-lookup"><span data-stu-id="4e107-131">Create a connection string using a shared access signature</span></span>
[!INCLUDE [storage-use-sas-in-connection-string-include](../../includes/storage-use-sas-in-connection-string-include.md)]

## <a name="create-a-connection-string-for-an-explicit-storage-endpoint"></a><span data-ttu-id="4e107-132">Create a connection string for an explicit storage endpoint</span><span class="sxs-lookup"><span data-stu-id="4e107-132">Create a connection string for an explicit storage endpoint</span></span>
<span data-ttu-id="4e107-133">You can specify explicit service endpoints in your connection string instead of using the default endpoints.</span><span class="sxs-lookup"><span data-stu-id="4e107-133">You can specify explicit service endpoints in your connection string instead of using the default endpoints.</span></span> <span data-ttu-id="4e107-134">To create a connection string that specifies an explicit endpoint, specify the complete service endpoint for each service, including the protocol specification (HTTPS (recommended) or HTTP), in the following format:</span><span class="sxs-lookup"><span data-stu-id="4e107-134">To create a connection string that specifies an explicit endpoint, specify the complete service endpoint for each service, including the protocol specification (HTTPS (recommended) or HTTP), in the following format:</span></span>

```
DefaultEndpointsProtocol=[http|https];
BlobEndpoint=myBlobEndpoint;
FileEndpoint=myFileEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
AccountName=myAccountName;
AccountKey=myAccountKey
```

<span data-ttu-id="4e107-135">One scenario where you might wish to specify an explicit endpoint is when you've mapped your Blob storage endpoint to a [custom domain](storage-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="4e107-135">One scenario where you might wish to specify an explicit endpoint is when you've mapped your Blob storage endpoint to a [custom domain](storage-custom-domain-name.md).</span></span> <span data-ttu-id="4e107-136">In that case, you can specify your custom endpoint for Blob storage in your connection string.</span><span class="sxs-lookup"><span data-stu-id="4e107-136">In that case, you can specify your custom endpoint for Blob storage in your connection string.</span></span> <span data-ttu-id="4e107-137">You can optionally specify the default endpoints for the other services if your application uses them.</span><span class="sxs-lookup"><span data-stu-id="4e107-137">You can optionally specify the default endpoints for the other services if your application uses them.</span></span>

<span data-ttu-id="4e107-138">Here is an example of a connection string that specifies an explicit endpoint for the Blob service:</span><span class="sxs-lookup"><span data-stu-id="4e107-138">Here is an example of a connection string that specifies an explicit endpoint for the Blob service:</span></span>

```
# Blob endpoint only
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
AccountName=storagesample;
AccountKey=<account-key>
```

<span data-ttu-id="4e107-139">This example specifies explicit endpoints for all services, including a custom domain for the Blob service:</span><span class="sxs-lookup"><span data-stu-id="4e107-139">This example specifies explicit endpoints for all services, including a custom domain for the Blob service:</span></span>

```
# All service endpoints
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
FileEndpoint=https://myaccount.file.core.windows.net;
QueueEndpoint=https://myaccount.queue.core.windows.net;
TableEndpoint=https://myaccount.table.core.windows.net;
AccountName=storagesample;
AccountKey=<account-key>
```

<span data-ttu-id="4e107-140">The endpoint values in a connection string are used to construct the request URIs to the storage services, and dictate the form of any URIs that are returned to your code.</span><span class="sxs-lookup"><span data-stu-id="4e107-140">The endpoint values in a connection string are used to construct the request URIs to the storage services, and dictate the form of any URIs that are returned to your code.</span></span>

<span data-ttu-id="4e107-141">If you've mapped a storage endpoint to a custom domain and omit that endpoint from a connection string, then you will not be able to use that connection string to access data in that service from your code.</span><span class="sxs-lookup"><span data-stu-id="4e107-141">If you've mapped a storage endpoint to a custom domain and omit that endpoint from a connection string, then you will not be able to use that connection string to access data in that service from your code.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4e107-142">Service endpoint values in your connection strings must be well-formed URIs, including `https://` (recommended) or `http://`.</span><span class="sxs-lookup"><span data-stu-id="4e107-142">Service endpoint values in your connection strings must be well-formed URIs, including `https://` (recommended) or `http://`.</span></span> <span data-ttu-id="4e107-143">Because Azure Storage does not yet support HTTPS for custom domains, you *must* specify `http://` for any endpoint URI that points to a custom domain.</span><span class="sxs-lookup"><span data-stu-id="4e107-143">Because Azure Storage does not yet support HTTPS for custom domains, you *must* specify `http://` for any endpoint URI that points to a custom domain.</span></span>
>

### <a name="create-a-connection-string-with-an-endpoint-suffix"></a><span data-ttu-id="4e107-144">Create a connection string with an endpoint suffix</span><span class="sxs-lookup"><span data-stu-id="4e107-144">Create a connection string with an endpoint suffix</span></span>
<span data-ttu-id="4e107-145">To create a connection string for a storage service in regions or instances with different endpoint suffixes, such as for Azure China or Azure Government, use the following connection string format.</span><span class="sxs-lookup"><span data-stu-id="4e107-145">To create a connection string for a storage service in regions or instances with different endpoint suffixes, such as for Azure China or Azure Government, use the following connection string format.</span></span> <span data-ttu-id="4e107-146">Indicate whether you want to connect to the storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with the name of your storage account, replace `myAccountKey` with your account access key, and replace `mySuffix` with the URI suffix:</span><span class="sxs-lookup"><span data-stu-id="4e107-146">Indicate whether you want to connect to the storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with the name of your storage account, replace `myAccountKey` with your account access key, and replace `mySuffix` with the URI suffix:</span></span>

```
DefaultEndpointsProtocol=[http|https];
AccountName=myAccountName;
AccountKey=myAccountKey;
EndpointSuffix=mySuffix;
```

<span data-ttu-id="4e107-147">Here's an example connection string for storage services in Azure China:</span><span class="sxs-lookup"><span data-stu-id="4e107-147">Here's an example connection string for storage services in Azure China:</span></span>

```
DefaultEndpointsProtocol=https;
AccountName=storagesample;
AccountKey=<account-key>;
EndpointSuffix=core.chinacloudapi.cn;
```

## <a name="parsing-a-connection-string"></a><span data-ttu-id="4e107-148">Parsing a connection string</span><span class="sxs-lookup"><span data-stu-id="4e107-148">Parsing a connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="next-steps"></a><span data-ttu-id="4e107-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="4e107-149">Next steps</span></span>
* [<span data-ttu-id="4e107-150">Use the Azure storage emulator for development and testing</span><span class="sxs-lookup"><span data-stu-id="4e107-150">Use the Azure storage emulator for development and testing</span></span>](storage-use-emulator.md)
* [<span data-ttu-id="4e107-151">Azure Storage explorers</span><span class="sxs-lookup"><span data-stu-id="4e107-151">Azure Storage explorers</span></span>](storage-explorers.md)
* [<span data-ttu-id="4e107-152">Using Shared Access Signatures (SAS)</span><span class="sxs-lookup"><span data-stu-id="4e107-152">Using Shared Access Signatures (SAS)</span></span>](storage-dotnet-shared-access-signature-part-1.md)

