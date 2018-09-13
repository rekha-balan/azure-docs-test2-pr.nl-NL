---
title: Implement disaster recovery using backup and restore in Azure API Management | Microsoft Docs
description: Learn how to use backup and restore to perform disaster recovery in Azure API Management.
services: api-management
documentationcenter: ''
author: steved0x
manager: erikre
editor: ''
ms.assetid: 6f10be3c-f796-4a6c-bacd-7931b6aa82af
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 0cc764c9703920723d36e8216e68a036614296f1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549849"
---
# <a name="how-to-implement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a><span data-ttu-id="1bc32-103">How to implement disaster recovery using service backup and restore in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="1bc32-103">How to implement disaster recovery using service backup and restore in Azure API Management</span></span>
<span data-ttu-id="1bc32-104">By choosing to publish and manage your APIs via Azure API Management you are taking advantage of many fault tolerance and infrastructure capabilities that you would otherwise have to design, implement, and manage.</span><span class="sxs-lookup"><span data-stu-id="1bc32-104">By choosing to publish and manage your APIs via Azure API Management you are taking advantage of many fault tolerance and infrastructure capabilities that you would otherwise have to design, implement, and manage.</span></span> <span data-ttu-id="1bc32-105">The Azure platform mitigates a large fraction of potential failures at a fraction of the cost.</span><span class="sxs-lookup"><span data-stu-id="1bc32-105">The Azure platform mitigates a large fraction of potential failures at a fraction of the cost.</span></span>

<span data-ttu-id="1bc32-106">To recover from availability problems affecting the region where your API Management service is hosted you should be ready to reconstitute your service in a different region at any time.</span><span class="sxs-lookup"><span data-stu-id="1bc32-106">To recover from availability problems affecting the region where your API Management service is hosted you should be ready to reconstitute your service in a different region at any time.</span></span> <span data-ttu-id="1bc32-107">Depending on your availability goals and recovery time objective  you might want to reserve a backup service in one or more regions and try to maintain their configuration and content in sync with the active service.</span><span class="sxs-lookup"><span data-stu-id="1bc32-107">Depending on your availability goals and recovery time objective  you might want to reserve a backup service in one or more regions and try to maintain their configuration and content in sync with the active service.</span></span> <span data-ttu-id="1bc32-108">The service backup and restore feature provides the necessary building block for implementing your disaster recovery strategy.</span><span class="sxs-lookup"><span data-stu-id="1bc32-108">The service backup and restore feature provides the necessary building block for implementing your disaster recovery strategy.</span></span>

<span data-ttu-id="1bc32-109">This guide shows how to authenticate Azure Resource Manager requests, and how to backup and restore your API Management service instances.</span><span class="sxs-lookup"><span data-stu-id="1bc32-109">This guide shows how to authenticate Azure Resource Manager requests, and how to backup and restore your API Management service instances.</span></span>

> [!NOTE]
> <span data-ttu-id="1bc32-110">The process for backing up and restoring an API Management service instance for disaster recovery can also be used for replicating API Management service instances for scenarios such as staging.</span><span class="sxs-lookup"><span data-stu-id="1bc32-110">The process for backing up and restoring an API Management service instance for disaster recovery can also be used for replicating API Management service instances for scenarios such as staging.</span></span>
>
> <span data-ttu-id="1bc32-111">Note that each backup expires after 30 days.</span><span class="sxs-lookup"><span data-stu-id="1bc32-111">Note that each backup expires after 30 days.</span></span> <span data-ttu-id="1bc32-112">If you attempt to restore a backup after the 30 day expiration period has expired, the restore will fail with a `Cannot restore: backup expired` message.</span><span class="sxs-lookup"><span data-stu-id="1bc32-112">If you attempt to restore a backup after the 30 day expiration period has expired, the restore will fail with a `Cannot restore: backup expired` message.</span></span>
>
>

## <a name="authenticating-azure-resource-manager-requests"></a><span data-ttu-id="1bc32-113">Authenticating Azure Resource Manager requests</span><span class="sxs-lookup"><span data-stu-id="1bc32-113">Authenticating Azure Resource Manager requests</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1bc32-114">The REST API for backup and restore uses Azure Resource Manager and has a different authentication mechanism than the REST APIs for managing your API Management entities.</span><span class="sxs-lookup"><span data-stu-id="1bc32-114">The REST API for backup and restore uses Azure Resource Manager and has a different authentication mechanism than the REST APIs for managing your API Management entities.</span></span> <span data-ttu-id="1bc32-115">The steps in this section describe how to authenticate Azure Resource Manager requests.</span><span class="sxs-lookup"><span data-stu-id="1bc32-115">The steps in this section describe how to authenticate Azure Resource Manager requests.</span></span> <span data-ttu-id="1bc32-116">For more information, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span><span class="sxs-lookup"><span data-stu-id="1bc32-116">For more information, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span></span>
>
>

<span data-ttu-id="1bc32-117">All of the tasks that you do on resources using the Azure Resource Manager must be authenticated with Azure Active Directory using the following steps.</span><span class="sxs-lookup"><span data-stu-id="1bc32-117">All of the tasks that you do on resources using the Azure Resource Manager must be authenticated with Azure Active Directory using the following steps.</span></span>

* <span data-ttu-id="1bc32-118">Add an application to the Azure Active Directory tenant.</span><span class="sxs-lookup"><span data-stu-id="1bc32-118">Add an application to the Azure Active Directory tenant.</span></span>
* <span data-ttu-id="1bc32-119">Set permissions for the application that you added.</span><span class="sxs-lookup"><span data-stu-id="1bc32-119">Set permissions for the application that you added.</span></span>
* <span data-ttu-id="1bc32-120">Get the token for authenticating requests to Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1bc32-120">Get the token for authenticating requests to Azure Resource Manager.</span></span>

<span data-ttu-id="1bc32-121">The first step is to create an Azure Active Directory application.</span><span class="sxs-lookup"><span data-stu-id="1bc32-121">The first step is to create an Azure Active Directory application.</span></span> <span data-ttu-id="1bc32-122">Log into the [Azure Classic Portal](http://manage.windowsazure.com/) using the subscription that contains your API Management service instance and navigate to the **Applications** tab for your default Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1bc32-122">Log into the [Azure Classic Portal](http://manage.windowsazure.com/) using the subscription that contains your API Management service instance and navigate to the **Applications** tab for your default Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="1bc32-123">If the Azure Active Directory default directory is not visible to your account, contact the administrator of the Azure subscription to grant the required permissions to your account.</span><span class="sxs-lookup"><span data-stu-id="1bc32-123">If the Azure Active Directory default directory is not visible to your account, contact the administrator of the Azure subscription to grant the required permissions to your account.</span></span> <span data-ttu-id="1bc32-124">For information on locating your default directory, see "Locate your default directory in the Azure classic portal" in [Creating a Work or School identity in Azure Active Directory to use with Windows VMs](../virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1bc32-124">For information on locating your default directory, see "Locate your default directory in the Azure classic portal" in [Creating a Work or School identity in Azure Active Directory to use with Windows VMs](../virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
>
>

![Create Azure Active Directory application][api-management-add-aad-application]

<span data-ttu-id="1bc32-126">Click **Add**, **Add an application my organization is developing**, and choose **Native client application**.</span><span class="sxs-lookup"><span data-stu-id="1bc32-126">Click **Add**, **Add an application my organization is developing**, and choose **Native client application**.</span></span> <span data-ttu-id="1bc32-127">Enter a descriptive name, and click the next arrow.</span><span class="sxs-lookup"><span data-stu-id="1bc32-127">Enter a descriptive name, and click the next arrow.</span></span> <span data-ttu-id="1bc32-128">Enter a placeholder URL such as `http://resources` for the **Redirect URI**, as it is a required field, but the value is not used later.</span><span class="sxs-lookup"><span data-stu-id="1bc32-128">Enter a placeholder URL such as `http://resources` for the **Redirect URI**, as it is a required field, but the value is not used later.</span></span> <span data-ttu-id="1bc32-129">Click the check box to save the application.</span><span class="sxs-lookup"><span data-stu-id="1bc32-129">Click the check box to save the application.</span></span>

<span data-ttu-id="1bc32-130">Once the application is saved, click **Configure**, scroll down to the **permissions to other applications** section, and click **Add application**.</span><span class="sxs-lookup"><span data-stu-id="1bc32-130">Once the application is saved, click **Configure**, scroll down to the **permissions to other applications** section, and click **Add application**.</span></span>

![Add permissions][api-management-aad-permissions-add]

<span data-ttu-id="1bc32-132">Select **Windows** **Azure Service Management API** and click the checkbox to add the application.</span><span class="sxs-lookup"><span data-stu-id="1bc32-132">Select **Windows** **Azure Service Management API** and click the checkbox to add the application.</span></span>

![Add permissions][api-management-aad-permissions]

<span data-ttu-id="1bc32-134">Click **Delegated Permissions** beside the newly added **Windows** **Azure Service Management API** application, check the box for **Access Azure Service Management (preview)**, and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="1bc32-134">Click **Delegated Permissions** beside the newly added **Windows** **Azure Service Management API** application, check the box for **Access Azure Service Management (preview)**, and click **Save**.</span></span>

![Add permissions][api-management-aad-delegated-permissions]

<span data-ttu-id="1bc32-136">Prior to invoking the APIs that generate the backup and restore it, it is necessary to get a token.</span><span class="sxs-lookup"><span data-stu-id="1bc32-136">Prior to invoking the APIs that generate the backup and restore it, it is necessary to get a token.</span></span> <span data-ttu-id="1bc32-137">The following example uses the [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) nuget package to retrieve the token.</span><span class="sxs-lookup"><span data-stu-id="1bc32-137">The following example uses the [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) nuget package to retrieve the token.</span></span>

```c#
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System;

namespace GetTokenResourceManagerRequests
{
    class Program
    {
        static void Main(string[] args)
        {
            var authenticationContext = new AuthenticationContext("https://login.windows.net/{tenant id}");
            var result = authenticationContext.AcquireToken("https://management.azure.com/", {application id}, new Uri({redirect uri});

            if (result == null) {
                throw new InvalidOperationException("Failed to obtain the JWT token");
            }

            Console.WriteLine(result.AccessToken);

            Console.ReadLine();
        }
    }
}
```

<span data-ttu-id="1bc32-138">Replace `{tentand id}`, `{application id}`, and `{redirect uri}` using the following instructions.</span><span class="sxs-lookup"><span data-stu-id="1bc32-138">Replace `{tentand id}`, `{application id}`, and `{redirect uri}` using the following instructions.</span></span>

<span data-ttu-id="1bc32-139">Replace `{tenant id}` with the tenant id of the Azure Active Directory application you just created.</span><span class="sxs-lookup"><span data-stu-id="1bc32-139">Replace `{tenant id}` with the tenant id of the Azure Active Directory application you just created.</span></span> <span data-ttu-id="1bc32-140">You can access the id by clicking **View endpoints**.</span><span class="sxs-lookup"><span data-stu-id="1bc32-140">You can access the id by clicking **View endpoints**.</span></span>

![Endpoints][api-management-aad-default-directory]

![Endpoints][api-management-endpoint]

<span data-ttu-id="1bc32-143">Replace `{application id}` and `{redirect uri}` using the **Client Id** and  the URL from the **Redirect Uris** section from your Azure Active Directory application's **Configure** tab.</span><span class="sxs-lookup"><span data-stu-id="1bc32-143">Replace `{application id}` and `{redirect uri}` using the **Client Id** and  the URL from the **Redirect Uris** section from your Azure Active Directory application's **Configure** tab.</span></span>

![Resources][api-management-aad-resources]

<span data-ttu-id="1bc32-145">Once the values are specified, the code example should return a token similar to the following example.</span><span class="sxs-lookup"><span data-stu-id="1bc32-145">Once the values are specified, the code example should return a token similar to the following example.</span></span>

![Token][api-management-arm-token]

<span data-ttu-id="1bc32-147">Before calling the backup and restore operations described in the following sections, set the authorization request header for your REST call.</span><span class="sxs-lookup"><span data-stu-id="1bc32-147">Before calling the backup and restore operations described in the following sections, set the authorization request header for your REST call.</span></span>

```c#
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

## <span data-ttu-id="1bc32-148"><a name="step1"> </a>Back up an API Management service</span><span class="sxs-lookup"><span data-stu-id="1bc32-148"><a name="step1"> </a>Back up an API Management service</span></span>
<span data-ttu-id="1bc32-149">To back up an API Management service issue the following HTTP request:</span><span class="sxs-lookup"><span data-stu-id="1bc32-149">To back up an API Management service issue the following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

<span data-ttu-id="1bc32-150">where:</span><span class="sxs-lookup"><span data-stu-id="1bc32-150">where:</span></span>

* <span data-ttu-id="1bc32-151">`subscriptionId` - id of the subscription containing the API Management service you are attempting to backup</span><span class="sxs-lookup"><span data-stu-id="1bc32-151">`subscriptionId` - id of the subscription containing the API Management service you are attempting to backup</span></span>
* <span data-ttu-id="1bc32-152">`resourceGroupName` - a string in the form of 'Api-Default-{service-region}' where `service-region` identifies the Azure region where the API Management service you are trying to backup is hosted, e.g. `North-Central-US`</span><span class="sxs-lookup"><span data-stu-id="1bc32-152">`resourceGroupName` - a string in the form of 'Api-Default-{service-region}' where `service-region` identifies the Azure region where the API Management service you are trying to backup is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="1bc32-153">`serviceName` - the name of the API Management service you are making a backup of specified at the time of its creation</span><span class="sxs-lookup"><span data-stu-id="1bc32-153">`serviceName` - the name of the API Management service you are making a backup of specified at the time of its creation</span></span>
* <span data-ttu-id="1bc32-154">`api-version` - replace  with `2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="1bc32-154">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="1bc32-155">In the body of the request, specify the target Azure storage account name, access key, blob container name, and backup name:</span><span class="sxs-lookup"><span data-stu-id="1bc32-155">In the body of the request, specify the target Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for the backup},  
    accessKey : {access key for the account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="1bc32-156">Set the value of the `Content-Type` request header to `application/json`.</span><span class="sxs-lookup"><span data-stu-id="1bc32-156">Set the value of the `Content-Type` request header to `application/json`.</span></span>

<span data-ttu-id="1bc32-157">Backup is a long running operation that may take multiple minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="1bc32-157">Backup is a long running operation that may take multiple minutes to complete.</span></span>  <span data-ttu-id="1bc32-158">If the request was successful and the backup process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span><span class="sxs-lookup"><span data-stu-id="1bc32-158">If the request was successful and the backup process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="1bc32-159">Make 'GET' requests to the URL in the `Location` header to find out the status of the operation.</span><span class="sxs-lookup"><span data-stu-id="1bc32-159">Make 'GET' requests to the URL in the `Location` header to find out the status of the operation.</span></span> <span data-ttu-id="1bc32-160">While the backup is in progress you will continue to receive a '202 Accepted' status code.</span><span class="sxs-lookup"><span data-stu-id="1bc32-160">While the backup is in progress you will continue to receive a '202 Accepted' status code.</span></span> <span data-ttu-id="1bc32-161">A Response code of `200 OK` will indicate successful completion of the backup operation.</span><span class="sxs-lookup"><span data-stu-id="1bc32-161">A Response code of `200 OK` will indicate successful completion of the backup operation.</span></span>

<span data-ttu-id="1bc32-162">Please note the following constraints when making a backup request.</span><span class="sxs-lookup"><span data-stu-id="1bc32-162">Please note the following constraints when making a backup request.</span></span>

* <span data-ttu-id="1bc32-163">**Container** specified in the request body **must exist**.</span><span class="sxs-lookup"><span data-stu-id="1bc32-163">**Container** specified in the request body **must exist**.</span></span>
* <span data-ttu-id="1bc32-164">While backup is in progress you **should not attempt any service management operations** such as SKU upgrade or downgrade, domain name change, etc.</span><span class="sxs-lookup"><span data-stu-id="1bc32-164">While backup is in progress you **should not attempt any service management operations** such as SKU upgrade or downgrade, domain name change, etc.</span></span>
* <span data-ttu-id="1bc32-165">Restore of a **backup is guaranteed only for 30 days** since the moment of its creation.</span><span class="sxs-lookup"><span data-stu-id="1bc32-165">Restore of a **backup is guaranteed only for 30 days** since the moment of its creation.</span></span>
* <span data-ttu-id="1bc32-166">**Usage data** used for creating analytics reports **is not included** in the backup.</span><span class="sxs-lookup"><span data-stu-id="1bc32-166">**Usage data** used for creating analytics reports **is not included** in the backup.</span></span> <span data-ttu-id="1bc32-167">Use [Azure API Management REST API][Azure API Management REST API] to periodically retrieve analytics reports for safekeeping.</span><span class="sxs-lookup"><span data-stu-id="1bc32-167">Use [Azure API Management REST API][Azure API Management REST API] to periodically retrieve analytics reports for safekeeping.</span></span>
* <span data-ttu-id="1bc32-168">The frequency with which you perform service backups will affect your recovery point objective.</span><span class="sxs-lookup"><span data-stu-id="1bc32-168">The frequency with which you perform service backups will affect your recovery point objective.</span></span> <span data-ttu-id="1bc32-169">To minimize it we advise implementing regular backups as well as performing on-demand backups after making important changes to your API Management service.</span><span class="sxs-lookup"><span data-stu-id="1bc32-169">To minimize it we advise implementing regular backups as well as performing on-demand backups after making important changes to your API Management service.</span></span>
* <span data-ttu-id="1bc32-170">**Changes** made to the service configuration (e.g. APIs, policies, developer portal appearance) while backup operation is in process **might not be included in the backup and therefore will be lost**.</span><span class="sxs-lookup"><span data-stu-id="1bc32-170">**Changes** made to the service configuration (e.g. APIs, policies, developer portal appearance) while backup operation is in process **might not be included in the backup and therefore will be lost**.</span></span>

## <span data-ttu-id="1bc32-171"><a name="step2"> </a>Restore an API Management service</span><span class="sxs-lookup"><span data-stu-id="1bc32-171"><a name="step2"> </a>Restore an API Management service</span></span>
<span data-ttu-id="1bc32-172">To restore an API Management service from a previously created backup make the following HTTP request:</span><span class="sxs-lookup"><span data-stu-id="1bc32-172">To restore an API Management service from a previously created backup make the following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

<span data-ttu-id="1bc32-173">where:</span><span class="sxs-lookup"><span data-stu-id="1bc32-173">where:</span></span>

* <span data-ttu-id="1bc32-174">`subscriptionId` - id of the subscription containing the API Management service you are restoring a backup into</span><span class="sxs-lookup"><span data-stu-id="1bc32-174">`subscriptionId` - id of the subscription containing the API Management service you are restoring a backup into</span></span>
* <span data-ttu-id="1bc32-175">`resourceGroupName` - a string in the form of 'Api-Default-{service-region}' where `service-region` identifies the Azure region where the API Management service you are restoring a backup into is hosted, e.g. `North-Central-US`</span><span class="sxs-lookup"><span data-stu-id="1bc32-175">`resourceGroupName` - a string in the form of 'Api-Default-{service-region}' where `service-region` identifies the Azure region where the API Management service you are restoring a backup into is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="1bc32-176">`serviceName` - the name of the API Management service being restored into specified at the time of its creation</span><span class="sxs-lookup"><span data-stu-id="1bc32-176">`serviceName` - the name of the API Management service being restored into specified at the time of its creation</span></span>
* <span data-ttu-id="1bc32-177">`api-version` - replace  with `2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="1bc32-177">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="1bc32-178">In the body of the request, specify the backup file location, i.e. Azure storage account name, access key, blob container name, and backup name:</span><span class="sxs-lookup"><span data-stu-id="1bc32-178">In the body of the request, specify the backup file location, i.e. Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for the backup},  
    accessKey : {access key for the account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="1bc32-179">Set the value of the `Content-Type` request header to `application/json`.</span><span class="sxs-lookup"><span data-stu-id="1bc32-179">Set the value of the `Content-Type` request header to `application/json`.</span></span>

<span data-ttu-id="1bc32-180">Restore is a long running operation that may take up to 30 or more minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="1bc32-180">Restore is a long running operation that may take up to 30 or more minutes to complete.</span></span>  <span data-ttu-id="1bc32-181">If the request was successful and the restore process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span><span class="sxs-lookup"><span data-stu-id="1bc32-181">If the request was successful and the restore process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="1bc32-182">Make 'GET' requests to the URL in the `Location` header to find out the status of the operation.</span><span class="sxs-lookup"><span data-stu-id="1bc32-182">Make 'GET' requests to the URL in the `Location` header to find out the status of the operation.</span></span> <span data-ttu-id="1bc32-183">While the restore is in progress you will continue to receive '202 Accepted' status code.</span><span class="sxs-lookup"><span data-stu-id="1bc32-183">While the restore is in progress you will continue to receive '202 Accepted' status code.</span></span> <span data-ttu-id="1bc32-184">A response code of `200 OK` will indicate successful completion of the restore operation.</span><span class="sxs-lookup"><span data-stu-id="1bc32-184">A response code of `200 OK` will indicate successful completion of the restore operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1bc32-185">**The SKU** of the service being restored into **must match** the SKU of the backed up service being restored.</span><span class="sxs-lookup"><span data-stu-id="1bc32-185">**The SKU** of the service being restored into **must match** the SKU of the backed up service being restored.</span></span>
>
> <span data-ttu-id="1bc32-186">**Changes** made to the service configuration (e.g. APIs, policies, developer portal appearance) while restore operation is in progress **could be overwritten**.</span><span class="sxs-lookup"><span data-stu-id="1bc32-186">**Changes** made to the service configuration (e.g. APIs, policies, developer portal appearance) while restore operation is in progress **could be overwritten**.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="1bc32-187">Next steps</span><span class="sxs-lookup"><span data-stu-id="1bc32-187">Next steps</span></span>
<span data-ttu-id="1bc32-188">Check out the following Microsoft blogs for two different walkthroughs of the backup/restore process.</span><span class="sxs-lookup"><span data-stu-id="1bc32-188">Check out the following Microsoft blogs for two different walkthroughs of the backup/restore process.</span></span>

* [<span data-ttu-id="1bc32-189">Replicate Azure API Management Accounts</span><span class="sxs-lookup"><span data-stu-id="1bc32-189">Replicate Azure API Management Accounts</span></span>](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
  * <span data-ttu-id="1bc32-190">Thank you to Gisela for her contribution to this article.</span><span class="sxs-lookup"><span data-stu-id="1bc32-190">Thank you to Gisela for her contribution to this article.</span></span>
* [<span data-ttu-id="1bc32-191">Azure API Management: Backing Up and Restoring Configuration</span><span class="sxs-lookup"><span data-stu-id="1bc32-191">Azure API Management: Backing Up and Restoring Configuration</span></span>](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * <span data-ttu-id="1bc32-192">The approach detailed by Stuart does not match the official guidance but it is very interesting.</span><span class="sxs-lookup"><span data-stu-id="1bc32-192">The approach detailed by Stuart does not match the official guidance but it is very interesting.</span></span>

[Backup an API Management service]: #step1
[Restore an API Management service]: #step2


[Azure API Management REST API]: http://msdn.microsoft.com/library/azure/dn781421.aspx

[api-management-add-aad-application]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-disaster-recovery-backup-restore/api-management-add-aad-application.png

[api-management-aad-permissions]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions.png
[api-management-aad-permissions-add]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions-add.png
[api-management-aad-delegated-permissions]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-delegated-permissions.png
[api-management-aad-default-directory]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-default-directory.png
[api-management-aad-resources]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-resources.png
[api-management-arm-token]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-disaster-recovery-backup-restore/api-management-arm-token.png
[api-management-endpoint]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-disaster-recovery-backup-restore/api-management-endpoint.png








