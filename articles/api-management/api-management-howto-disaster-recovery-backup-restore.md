---
title: Implement disaster recovery using backup and restore in Azure API Management | Microsoft Docs
description: Learn how to use backup and restore to perform disaster recovery in Azure API Management.
services: api-management
documentationcenter: ''
author: mikebudzynski
manager: erikre
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2018
ms.author: apimpm
ms.openlocfilehash: ed8c34a7e1e11d431d9a3b416067736da0d1612c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44779147"
---
# <a name="how-to-implement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a><span data-ttu-id="923d3-103">How to implement disaster recovery using service backup and restore in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="923d3-103">How to implement disaster recovery using service backup and restore in Azure API Management</span></span>

<span data-ttu-id="923d3-104">By choosing to publish and manage your APIs via Azure API Management you are taking advantage of many fault tolerance and infrastructure capabilities that you would otherwise have to design, implement, and manage.</span><span class="sxs-lookup"><span data-stu-id="923d3-104">By choosing to publish and manage your APIs via Azure API Management you are taking advantage of many fault tolerance and infrastructure capabilities that you would otherwise have to design, implement, and manage.</span></span> <span data-ttu-id="923d3-105">The Azure platform mitigates a large fraction of potential failures at a fraction of the cost.</span><span class="sxs-lookup"><span data-stu-id="923d3-105">The Azure platform mitigates a large fraction of potential failures at a fraction of the cost.</span></span>

<span data-ttu-id="923d3-106">To recover from availability problems affecting the region where your API Management service is hosted, you should be ready to reconstitute your service in a different region at any time.</span><span class="sxs-lookup"><span data-stu-id="923d3-106">To recover from availability problems affecting the region where your API Management service is hosted, you should be ready to reconstitute your service in a different region at any time.</span></span> <span data-ttu-id="923d3-107">Depending on your availability goals and recovery time objective, you might want to reserve a backup service in one or more regions and try to maintain their configuration and content in sync with the active service.</span><span class="sxs-lookup"><span data-stu-id="923d3-107">Depending on your availability goals and recovery time objective, you might want to reserve a backup service in one or more regions and try to maintain their configuration and content in sync with the active service.</span></span> <span data-ttu-id="923d3-108">The service "backup and restore" feature provides the necessary building block for implementing your disaster recovery strategy.</span><span class="sxs-lookup"><span data-stu-id="923d3-108">The service "backup and restore" feature provides the necessary building block for implementing your disaster recovery strategy.</span></span>

<span data-ttu-id="923d3-109">This guide shows how to authenticate Azure Resource Manager requests, and how to back up and restore your API Management service instances.</span><span class="sxs-lookup"><span data-stu-id="923d3-109">This guide shows how to authenticate Azure Resource Manager requests, and how to back up and restore your API Management service instances.</span></span>

> [!NOTE]
> <span data-ttu-id="923d3-110">The process for backing up and restoring an API Management service instance for disaster recovery can also be used for replicating API Management service instances for scenarios such as staging.</span><span class="sxs-lookup"><span data-stu-id="923d3-110">The process for backing up and restoring an API Management service instance for disaster recovery can also be used for replicating API Management service instances for scenarios such as staging.</span></span>
>
> <span data-ttu-id="923d3-111">Each backup expires after 30 days.</span><span class="sxs-lookup"><span data-stu-id="923d3-111">Each backup expires after 30 days.</span></span> <span data-ttu-id="923d3-112">If you attempt to restore a backup after the 30-day expiration period has expired, the restore will fail with a `Cannot restore: backup expired` message.</span><span class="sxs-lookup"><span data-stu-id="923d3-112">If you attempt to restore a backup after the 30-day expiration period has expired, the restore will fail with a `Cannot restore: backup expired` message.</span></span>
>
>

## <a name="authenticating-azure-resource-manager-requests"></a><span data-ttu-id="923d3-113">Authenticating Azure Resource Manager requests</span><span class="sxs-lookup"><span data-stu-id="923d3-113">Authenticating Azure Resource Manager requests</span></span>

> [!IMPORTANT]
> <span data-ttu-id="923d3-114">The REST API for backup and restore uses Azure Resource Manager and has a different authentication mechanism than the REST APIs for managing your API Management entities.</span><span class="sxs-lookup"><span data-stu-id="923d3-114">The REST API for backup and restore uses Azure Resource Manager and has a different authentication mechanism than the REST APIs for managing your API Management entities.</span></span> <span data-ttu-id="923d3-115">The steps in this section describe how to authenticate Azure Resource Manager requests.</span><span class="sxs-lookup"><span data-stu-id="923d3-115">The steps in this section describe how to authenticate Azure Resource Manager requests.</span></span> <span data-ttu-id="923d3-116">For more information, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span><span class="sxs-lookup"><span data-stu-id="923d3-116">For more information, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span></span>

<span data-ttu-id="923d3-117">All of the tasks that you do on resources using the Azure Resource Manager must be authenticated with Azure Active Directory using the following steps:</span><span class="sxs-lookup"><span data-stu-id="923d3-117">All of the tasks that you do on resources using the Azure Resource Manager must be authenticated with Azure Active Directory using the following steps:</span></span>

* <span data-ttu-id="923d3-118">Add an application to the Azure Active Directory tenant.</span><span class="sxs-lookup"><span data-stu-id="923d3-118">Add an application to the Azure Active Directory tenant.</span></span>
* <span data-ttu-id="923d3-119">Set permissions for the application that you added.</span><span class="sxs-lookup"><span data-stu-id="923d3-119">Set permissions for the application that you added.</span></span>
* <span data-ttu-id="923d3-120">Get the token for authenticating requests to Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="923d3-120">Get the token for authenticating requests to Azure Resource Manager.</span></span>

### <a name="create-an-azure-active-directory-application"></a><span data-ttu-id="923d3-121">Create an Azure Active Directory application</span><span class="sxs-lookup"><span data-stu-id="923d3-121">Create an Azure Active Directory application</span></span>

1. <span data-ttu-id="923d3-122">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="923d3-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="923d3-123">Using the subscription that contains your API Management service instance, navigate to the **App registrations** tab in **Azure Active Directory** (Azure Active Directory > Manage/App registrations).</span><span class="sxs-lookup"><span data-stu-id="923d3-123">Using the subscription that contains your API Management service instance, navigate to the **App registrations** tab in **Azure Active Directory** (Azure Active Directory > Manage/App registrations).</span></span>

    > [!NOTE]
    > <span data-ttu-id="923d3-124">If the Azure Active Directory default directory is not visible to your account, contact the administrator of the Azure subscription to grant the required permissions to your account.</span><span class="sxs-lookup"><span data-stu-id="923d3-124">If the Azure Active Directory default directory is not visible to your account, contact the administrator of the Azure subscription to grant the required permissions to your account.</span></span>
3. <span data-ttu-id="923d3-125">Click **New application registration**.</span><span class="sxs-lookup"><span data-stu-id="923d3-125">Click **New application registration**.</span></span>

    <span data-ttu-id="923d3-126">The **Create** window appears on the right.</span><span class="sxs-lookup"><span data-stu-id="923d3-126">The **Create** window appears on the right.</span></span> <span data-ttu-id="923d3-127">That is where you enter the AAD app relevant information.</span><span class="sxs-lookup"><span data-stu-id="923d3-127">That is where you enter the AAD app relevant information.</span></span>
4. <span data-ttu-id="923d3-128">Enter a name for the application.</span><span class="sxs-lookup"><span data-stu-id="923d3-128">Enter a name for the application.</span></span>
5. <span data-ttu-id="923d3-129">For the application type, select **Native**.</span><span class="sxs-lookup"><span data-stu-id="923d3-129">For the application type, select **Native**.</span></span>
6. <span data-ttu-id="923d3-130">Enter a placeholder URL such as `http://resources` for the **Redirect URI**, as it is a required field, but the value is not used later.</span><span class="sxs-lookup"><span data-stu-id="923d3-130">Enter a placeholder URL such as `http://resources` for the **Redirect URI**, as it is a required field, but the value is not used later.</span></span> <span data-ttu-id="923d3-131">Click the check box to save the application.</span><span class="sxs-lookup"><span data-stu-id="923d3-131">Click the check box to save the application.</span></span>
7. <span data-ttu-id="923d3-132">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="923d3-132">Click **Create**.</span></span>

### <a name="add-an-application"></a><span data-ttu-id="923d3-133">Add an application</span><span class="sxs-lookup"><span data-stu-id="923d3-133">Add an application</span></span>

1. <span data-ttu-id="923d3-134">Once the application is created, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="923d3-134">Once the application is created, click **Settings**.</span></span>
2. <span data-ttu-id="923d3-135">Click **Required permissions**.</span><span class="sxs-lookup"><span data-stu-id="923d3-135">Click **Required permissions**.</span></span>
3. <span data-ttu-id="923d3-136">Click **+Add**.</span><span class="sxs-lookup"><span data-stu-id="923d3-136">Click **+Add**.</span></span>
4. <span data-ttu-id="923d3-137">Press **Select an API**.</span><span class="sxs-lookup"><span data-stu-id="923d3-137">Press **Select an API**.</span></span>
5. <span data-ttu-id="923d3-138">Choose **Windows** **Azure Service Management API**.</span><span class="sxs-lookup"><span data-stu-id="923d3-138">Choose **Windows** **Azure Service Management API**.</span></span>
6. <span data-ttu-id="923d3-139">Press **Select**.</span><span class="sxs-lookup"><span data-stu-id="923d3-139">Press **Select**.</span></span> 

    ![Add permissions](./media/api-management-howto-disaster-recovery-backup-restore/add-app.png)

7. <span data-ttu-id="923d3-141">Click **Delegated Permissions** beside the newly added application, check the box for **Access Azure Service Management (preview)**.</span><span class="sxs-lookup"><span data-stu-id="923d3-141">Click **Delegated Permissions** beside the newly added application, check the box for **Access Azure Service Management (preview)**.</span></span>
8. <span data-ttu-id="923d3-142">Press **Select**.</span><span class="sxs-lookup"><span data-stu-id="923d3-142">Press **Select**.</span></span>
9. <span data-ttu-id="923d3-143">Click **Grant Permisssions**.</span><span class="sxs-lookup"><span data-stu-id="923d3-143">Click **Grant Permisssions**.</span></span>

### <a name="configuring-your-app"></a><span data-ttu-id="923d3-144">Configuring your app</span><span class="sxs-lookup"><span data-stu-id="923d3-144">Configuring your app</span></span>

<span data-ttu-id="923d3-145">Prior to invoking the APIs that generate the backup and restore it, it is necessary to get a token.</span><span class="sxs-lookup"><span data-stu-id="923d3-145">Prior to invoking the APIs that generate the backup and restore it, it is necessary to get a token.</span></span> <span data-ttu-id="923d3-146">The following example uses the [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) NuGet package to retrieve the token.</span><span class="sxs-lookup"><span data-stu-id="923d3-146">The following example uses the [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) NuGet package to retrieve the token.</span></span>

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System;

namespace GetTokenResourceManagerRequests
{
    class Program
    {
        static void Main(string[] args)
        {
            var authenticationContext = new AuthenticationContext("https://login.microsoftonline.com/{tenant id}");
            var result = authenticationContext.AcquireTokenAsync("https://management.azure.com/", "{application id}", new Uri("{redirect uri}"), new PlatformParameters(PromptBehavior.Auto)).Result;

            if (result == null) {
                throw new InvalidOperationException("Failed to obtain the JWT token");
            }

            Console.WriteLine(result.AccessToken);

            Console.ReadLine();
        }
    }
}
```

<span data-ttu-id="923d3-147">Replace `{tentand id}`, `{application id}`, and `{redirect uri}` using the following instructions:</span><span class="sxs-lookup"><span data-stu-id="923d3-147">Replace `{tentand id}`, `{application id}`, and `{redirect uri}` using the following instructions:</span></span>

1. <span data-ttu-id="923d3-148">Replace `{tenant id}` with the tenant id of the Azure Active Directory application you created.</span><span class="sxs-lookup"><span data-stu-id="923d3-148">Replace `{tenant id}` with the tenant id of the Azure Active Directory application you created.</span></span> <span data-ttu-id="923d3-149">You can access the id by clicking **App registrations** -> **Endpoints**.</span><span class="sxs-lookup"><span data-stu-id="923d3-149">You can access the id by clicking **App registrations** -> **Endpoints**.</span></span>

    ![Endpoints][api-management-endpoint]
2. <span data-ttu-id="923d3-151">Replace `{application id}` with the value you get by navigating to the **Settings** page.</span><span class="sxs-lookup"><span data-stu-id="923d3-151">Replace `{application id}` with the value you get by navigating to the **Settings** page.</span></span>
3. <span data-ttu-id="923d3-152">Replace the `{redirect uri}` with the value from the **Redirect URIs** tab of your Azure Active Directory application.</span><span class="sxs-lookup"><span data-stu-id="923d3-152">Replace the `{redirect uri}` with the value from the **Redirect URIs** tab of your Azure Active Directory application.</span></span>

    <span data-ttu-id="923d3-153">Once the values are specified, the code example should return a token similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="923d3-153">Once the values are specified, the code example should return a token similar to the following example:</span></span>

    ![Token][api-management-arm-token]

    > [!NOTE]
    > <span data-ttu-id="923d3-155">The token may expire after a certain period.</span><span class="sxs-lookup"><span data-stu-id="923d3-155">The token may expire after a certain period.</span></span> <span data-ttu-id="923d3-156">Execute the code sample again to generate a new token.</span><span class="sxs-lookup"><span data-stu-id="923d3-156">Execute the code sample again to generate a new token.</span></span>

## <a name="calling-the-backup-and-restore-operations"></a><span data-ttu-id="923d3-157">Calling the backup and restore operations</span><span class="sxs-lookup"><span data-stu-id="923d3-157">Calling the backup and restore operations</span></span>

<span data-ttu-id="923d3-158">The REST APIs are [Api Management Service - Backup](https://docs.microsoft.com/rest/api/apimanagement/apimanagementservice/backup) and [Api Management Service - Restore](https://docs.microsoft.com/rest/api/apimanagement/apimanagementservice/restore).</span><span class="sxs-lookup"><span data-stu-id="923d3-158">The REST APIs are [Api Management Service - Backup](https://docs.microsoft.com/rest/api/apimanagement/apimanagementservice/backup) and [Api Management Service - Restore](https://docs.microsoft.com/rest/api/apimanagement/apimanagementservice/restore).</span></span>

<span data-ttu-id="923d3-159">Before calling the "backup and restore" operations described in the following sections, set the authorization request header for your REST call.</span><span class="sxs-lookup"><span data-stu-id="923d3-159">Before calling the "backup and restore" operations described in the following sections, set the authorization request header for your REST call.</span></span>

```csharp
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

### <span data-ttu-id="923d3-160"><a name="step1"> </a>Back up an API Management service</span><span class="sxs-lookup"><span data-stu-id="923d3-160"><a name="step1"> </a>Back up an API Management service</span></span>
<span data-ttu-id="923d3-161">To back up an API Management service issue the following HTTP request:</span><span class="sxs-lookup"><span data-stu-id="923d3-161">To back up an API Management service issue the following HTTP request:</span></span>

```
POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}
```

<span data-ttu-id="923d3-162">where:</span><span class="sxs-lookup"><span data-stu-id="923d3-162">where:</span></span>

* <span data-ttu-id="923d3-163">`subscriptionId` - id of the subscription containing the API Management service you are attempting to back up</span><span class="sxs-lookup"><span data-stu-id="923d3-163">`subscriptionId` - id of the subscription containing the API Management service you are attempting to back up</span></span>
* <span data-ttu-id="923d3-164">`resourceGroupName` - name of the resource group of your Azure API Management service</span><span class="sxs-lookup"><span data-stu-id="923d3-164">`resourceGroupName` - name of the resource group of your Azure API Management service</span></span>
* <span data-ttu-id="923d3-165">`serviceName` - the name of the API Management service you are making a backup of specified at the time of its creation</span><span class="sxs-lookup"><span data-stu-id="923d3-165">`serviceName` - the name of the API Management service you are making a backup of specified at the time of its creation</span></span>
* <span data-ttu-id="923d3-166">`api-version` - replace  with `2018-06-01-preview`</span><span class="sxs-lookup"><span data-stu-id="923d3-166">`api-version` - replace  with `2018-06-01-preview`</span></span>

<span data-ttu-id="923d3-167">In the body of the request, specify the target Azure storage account name, access key, blob container name, and backup name:</span><span class="sxs-lookup"><span data-stu-id="923d3-167">In the body of the request, specify the target Azure storage account name, access key, blob container name, and backup name:</span></span>


```json
{
  "storageAccount": "{storage account name for the backup}",
  "accessKey": "{access key for the account}",
  "containerName": "{backup container name}",
  "backupName": "{backup blob name}"
}
```

<span data-ttu-id="923d3-168">Set the value of the `Content-Type` request header to `application/json`.</span><span class="sxs-lookup"><span data-stu-id="923d3-168">Set the value of the `Content-Type` request header to `application/json`.</span></span>

<span data-ttu-id="923d3-169">Backup is a long running operation that may take multiple minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="923d3-169">Backup is a long running operation that may take multiple minutes to complete.</span></span>  <span data-ttu-id="923d3-170">If the request was successful and the backup process was initiated, you receive a `202 Accepted` response status code with a `Location` header.</span><span class="sxs-lookup"><span data-stu-id="923d3-170">If the request was successful and the backup process was initiated, you receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="923d3-171">Make 'GET' requests to the URL in the `Location` header to find out the status of the operation.</span><span class="sxs-lookup"><span data-stu-id="923d3-171">Make 'GET' requests to the URL in the `Location` header to find out the status of the operation.</span></span> <span data-ttu-id="923d3-172">While the backup is in progress, you continue to receive a '202 Accepted' status code.</span><span class="sxs-lookup"><span data-stu-id="923d3-172">While the backup is in progress, you continue to receive a '202 Accepted' status code.</span></span> <span data-ttu-id="923d3-173">A Response code of `200 OK` indicates successful completion of the backup operation.</span><span class="sxs-lookup"><span data-stu-id="923d3-173">A Response code of `200 OK` indicates successful completion of the backup operation.</span></span>

<span data-ttu-id="923d3-174">Note the following constraints when making a backup request.</span><span class="sxs-lookup"><span data-stu-id="923d3-174">Note the following constraints when making a backup request.</span></span>

* <span data-ttu-id="923d3-175">**Container** specified in the request body **must exist**.</span><span class="sxs-lookup"><span data-stu-id="923d3-175">**Container** specified in the request body **must exist**.</span></span>
* <span data-ttu-id="923d3-176">While backup is in progress you **should not attempt any service management operations** such as SKU upgrade or downgrade, domain name change, etc.</span><span class="sxs-lookup"><span data-stu-id="923d3-176">While backup is in progress you **should not attempt any service management operations** such as SKU upgrade or downgrade, domain name change, etc.</span></span>
* <span data-ttu-id="923d3-177">Restore of a **backup is guaranteed only for 30 days** since the moment of its creation.</span><span class="sxs-lookup"><span data-stu-id="923d3-177">Restore of a **backup is guaranteed only for 30 days** since the moment of its creation.</span></span>
* <span data-ttu-id="923d3-178">**Usage data** used for creating analytics reports **is not included** in the backup.</span><span class="sxs-lookup"><span data-stu-id="923d3-178">**Usage data** used for creating analytics reports **is not included** in the backup.</span></span> <span data-ttu-id="923d3-179">Use [Azure API Management REST API][Azure API Management REST API] to periodically retrieve analytics reports for safekeeping.</span><span class="sxs-lookup"><span data-stu-id="923d3-179">Use [Azure API Management REST API][Azure API Management REST API] to periodically retrieve analytics reports for safekeeping.</span></span>
* <span data-ttu-id="923d3-180">The frequency with which you perform service backups affect your recovery point objective.</span><span class="sxs-lookup"><span data-stu-id="923d3-180">The frequency with which you perform service backups affect your recovery point objective.</span></span> <span data-ttu-id="923d3-181">To minimize it, the recommendation is implementing regular backups as well as performing on-demand backups after making important changes to your API Management service.</span><span class="sxs-lookup"><span data-stu-id="923d3-181">To minimize it, the recommendation is implementing regular backups as well as performing on-demand backups after making important changes to your API Management service.</span></span>
* <span data-ttu-id="923d3-182">**Changes** made to the service configuration (for example, APIs, policies, developer portal appearance) while backup operation is in process **might not be included in the backup and therefore will be lost**.</span><span class="sxs-lookup"><span data-stu-id="923d3-182">**Changes** made to the service configuration (for example, APIs, policies, developer portal appearance) while backup operation is in process **might not be included in the backup and therefore will be lost**.</span></span>

### <span data-ttu-id="923d3-183"><a name="step2"> </a>Restore an API Management service</span><span class="sxs-lookup"><span data-stu-id="923d3-183"><a name="step2"> </a>Restore an API Management service</span></span>
<span data-ttu-id="923d3-184">To restore an API Management service from a previously created backup make the following HTTP request:</span><span class="sxs-lookup"><span data-stu-id="923d3-184">To restore an API Management service from a previously created backup make the following HTTP request:</span></span>

```
POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}
```

<span data-ttu-id="923d3-185">where:</span><span class="sxs-lookup"><span data-stu-id="923d3-185">where:</span></span>

* <span data-ttu-id="923d3-186">`subscriptionId` - id of the subscription containing the API Management service you are restoring a backup into</span><span class="sxs-lookup"><span data-stu-id="923d3-186">`subscriptionId` - id of the subscription containing the API Management service you are restoring a backup into</span></span>
* <span data-ttu-id="923d3-187">`resourceGroupName` - name of the resource group containing the Azure API Management service you are restoring a backup into</span><span class="sxs-lookup"><span data-stu-id="923d3-187">`resourceGroupName` - name of the resource group containing the Azure API Management service you are restoring a backup into</span></span>
* <span data-ttu-id="923d3-188">`serviceName` - the name of the API Management service being restored into specified at the time of its creation</span><span class="sxs-lookup"><span data-stu-id="923d3-188">`serviceName` - the name of the API Management service being restored into specified at the time of its creation</span></span>
* <span data-ttu-id="923d3-189">`api-version` - replace  with `2018-06-01-preview`</span><span class="sxs-lookup"><span data-stu-id="923d3-189">`api-version` - replace  with `2018-06-01-preview`</span></span>

<span data-ttu-id="923d3-190">In the body of the request, specify the backup file location, that is, Azure storage account name, access key, blob container name, and backup name:</span><span class="sxs-lookup"><span data-stu-id="923d3-190">In the body of the request, specify the backup file location, that is, Azure storage account name, access key, blob container name, and backup name:</span></span>

```json
{
  "storageAccount": "{storage account name for the backup}",
  "accessKey": "{access key for the account}",
  "containerName": "{backup container name}",
  "backupName": "{backup blob name}"
}
```

<span data-ttu-id="923d3-191">Set the value of the `Content-Type` request header to `application/json`.</span><span class="sxs-lookup"><span data-stu-id="923d3-191">Set the value of the `Content-Type` request header to `application/json`.</span></span>

<span data-ttu-id="923d3-192">Restore is a long running operation that may take up to 30 or more minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="923d3-192">Restore is a long running operation that may take up to 30 or more minutes to complete.</span></span> <span data-ttu-id="923d3-193">If the request was successful and the restore process was initiated, you receive a `202 Accepted` response status code with a `Location` header.</span><span class="sxs-lookup"><span data-stu-id="923d3-193">If the request was successful and the restore process was initiated, you receive a `202 Accepted` response status code with a `Location` header.</span></span> <span data-ttu-id="923d3-194">Make 'GET' requests to the URL in the `Location` header to find out the status of the operation.</span><span class="sxs-lookup"><span data-stu-id="923d3-194">Make 'GET' requests to the URL in the `Location` header to find out the status of the operation.</span></span> <span data-ttu-id="923d3-195">While the restore is in progress, you continue to receive '202 Accepted' status code.</span><span class="sxs-lookup"><span data-stu-id="923d3-195">While the restore is in progress, you continue to receive '202 Accepted' status code.</span></span> <span data-ttu-id="923d3-196">A response code of `200 OK` indicates successful completion of the restore operation.</span><span class="sxs-lookup"><span data-stu-id="923d3-196">A response code of `200 OK` indicates successful completion of the restore operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="923d3-197">**The SKU** of the service being restored into **must match** the SKU of the backed-up service being restored.</span><span class="sxs-lookup"><span data-stu-id="923d3-197">**The SKU** of the service being restored into **must match** the SKU of the backed-up service being restored.</span></span>
>
> <span data-ttu-id="923d3-198">**Changes** made to the service configuration (for example, APIs, policies, developer portal appearance) while restore operation is in progress **could be overwritten**.</span><span class="sxs-lookup"><span data-stu-id="923d3-198">**Changes** made to the service configuration (for example, APIs, policies, developer portal appearance) while restore operation is in progress **could be overwritten**.</span></span>

> [!NOTE]
> <span data-ttu-id="923d3-199">Backup and restore operations can also be performed with Powershell *Backup-AzureRmApiManagement* and *Restore-AzureRmApiManagement* commands respectively.</span><span class="sxs-lookup"><span data-stu-id="923d3-199">Backup and restore operations can also be performed with Powershell *Backup-AzureRmApiManagement* and *Restore-AzureRmApiManagement* commands respectively.</span></span>

## <a name="next-steps"></a><span data-ttu-id="923d3-200">Next steps</span><span class="sxs-lookup"><span data-stu-id="923d3-200">Next steps</span></span>

<span data-ttu-id="923d3-201">Check out the following resources for different walkthroughs of the backup/restore process.</span><span class="sxs-lookup"><span data-stu-id="923d3-201">Check out the following resources for different walkthroughs of the backup/restore process.</span></span>

* [<span data-ttu-id="923d3-202">Replicate Azure API Management Accounts</span><span class="sxs-lookup"><span data-stu-id="923d3-202">Replicate Azure API Management Accounts</span></span>](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
* [<span data-ttu-id="923d3-203">Automating API Management Backup and Restore with Logic Apps</span><span class="sxs-lookup"><span data-stu-id="923d3-203">Automating API Management Backup and Restore with Logic Apps</span></span>](https://github.com/Azure/api-management-samples/tree/master/tutorials/automating-apim-backup-restore-with-logic-apps)
* <span data-ttu-id="923d3-204">[Azure API Management: Backing Up and Restoring Configuration](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  *The approach detailed by Stuart does not match the official guidance but it is interesting.*</span><span class="sxs-lookup"><span data-stu-id="923d3-204">[Azure API Management: Backing Up and Restoring Configuration](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
*The approach detailed by Stuart does not match the official guidance but it is interesting.*</span></span>

[Backup an API Management service]: #step1
[Restore an API Management service]: #step2

[Azure API Management REST API]: http://msdn.microsoft.com/library/azure/dn781421.aspx

[api-management-add-aad-application]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-add-aad-application.png

[api-management-aad-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions.png
[api-management-aad-permissions-add]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions-add.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-delegated-permissions.png
[api-management-aad-default-directory]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-default-directory.png
[api-management-aad-resources]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-resources.png
[api-management-arm-token]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-arm-token.png
[api-management-endpoint]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-endpoint.png
