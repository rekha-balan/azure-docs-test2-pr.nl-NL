---
title: Transform data using U-SQL script - Azure | Microsoft Docs
description: Learn how to process or transform data by running U-SQL scripts on Azure Data Lake Analytics compute service.
services: data-factory
documentationcenter: ''
author: douglaslMS
manager: craigg
ms.assetid: e17c1255-62c2-4e2e-bb60-d25274903e80
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 10/01/2017
ms.author: douglasl
robots: noindex
ms.openlocfilehash: 534fbeaa8ba3c27c8d3f3bbcc59717d8bdb5c654
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866137"
---
# <a name="transform-data-by-running-u-sql-scripts-on-azure-data-lake-analytics"></a><span data-ttu-id="d04fe-103">Transform data by running U-SQL scripts on Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="d04fe-103">Transform data by running U-SQL scripts on Azure Data Lake Analytics</span></span> 
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](data-factory-usql-activity.md)
> * [Version 2 (current version)](../transform-data-using-data-lake-analytics.md)

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [U-SQL Activity in V2](../transform-data-using-data-lake-analytics.md).

<span data-ttu-id="d04fe-108">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span><span class="sxs-lookup"><span data-stu-id="d04fe-108">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="d04fe-109">It contains a sequence of activities where each activity performs a specific processing operation.</span><span class="sxs-lookup"><span data-stu-id="d04fe-109">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="d04fe-110">This article describes the **Data Lake Analytics U-SQL Activity** that runs a **U-SQL** script on an **Azure Data Lake Analytics** compute linked service.</span><span class="sxs-lookup"><span data-stu-id="d04fe-110">This article describes the **Data Lake Analytics U-SQL Activity** that runs a **U-SQL** script on an **Azure Data Lake Analytics** compute linked service.</span></span> 

<span data-ttu-id="d04fe-111">Create an Azure Data Lake Analytics account before creating a pipeline with a Data Lake Analytics U-SQL Activity.</span><span class="sxs-lookup"><span data-stu-id="d04fe-111">Create an Azure Data Lake Analytics account before creating a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="d04fe-112">To learn about Azure Data Lake Analytics, see [Get started with Azure Data Lake Analytics](../../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d04fe-112">To learn about Azure Data Lake Analytics, see [Get started with Azure Data Lake Analytics](../../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span>

<span data-ttu-id="d04fe-113">Review the [Build your first pipeline tutorial](data-factory-build-your-first-pipeline.md) for detailed steps to create a data factory, linked services, datasets, and a pipeline.</span><span class="sxs-lookup"><span data-stu-id="d04fe-113">Review the [Build your first pipeline tutorial](data-factory-build-your-first-pipeline.md) for detailed steps to create a data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="d04fe-114">Use JSON snippets with Data Factory Editor or Visual Studio or Azure PowerShell to create Data Factory entities.</span><span class="sxs-lookup"><span data-stu-id="d04fe-114">Use JSON snippets with Data Factory Editor or Visual Studio or Azure PowerShell to create Data Factory entities.</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="d04fe-115">Supported authentication types</span><span class="sxs-lookup"><span data-stu-id="d04fe-115">Supported authentication types</span></span>
<span data-ttu-id="d04fe-116">U-SQL activity supports below authentication types against Data Lake Analytics:</span><span class="sxs-lookup"><span data-stu-id="d04fe-116">U-SQL activity supports below authentication types against Data Lake Analytics:</span></span>
* <span data-ttu-id="d04fe-117">Service principal authentication</span><span class="sxs-lookup"><span data-stu-id="d04fe-117">Service principal authentication</span></span>
* <span data-ttu-id="d04fe-118">User credential (OAuth) authentication</span><span class="sxs-lookup"><span data-stu-id="d04fe-118">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="d04fe-119">We recommend that you use service principal authentication, especially for a scheduled U-SQL execution.</span><span class="sxs-lookup"><span data-stu-id="d04fe-119">We recommend that you use service principal authentication, especially for a scheduled U-SQL execution.</span></span> <span data-ttu-id="d04fe-120">Token expiration behavior can occur with user credential authentication.</span><span class="sxs-lookup"><span data-stu-id="d04fe-120">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="d04fe-121">For configuration details, see the [Linked service properties](#azure-data-lake-analytics-linked-service) section.</span><span class="sxs-lookup"><span data-stu-id="d04fe-121">For configuration details, see the [Linked service properties](#azure-data-lake-analytics-linked-service) section.</span></span>

## <a name="azure-data-lake-analytics-linked-service"></a><span data-ttu-id="d04fe-122">Azure Data Lake Analytics Linked Service</span><span class="sxs-lookup"><span data-stu-id="d04fe-122">Azure Data Lake Analytics Linked Service</span></span>
<span data-ttu-id="d04fe-123">You create an **Azure Data Lake Analytics** linked service to link an Azure Data Lake Analytics compute service to an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="d04fe-123">You create an **Azure Data Lake Analytics** linked service to link an Azure Data Lake Analytics compute service to an Azure data factory.</span></span> <span data-ttu-id="d04fe-124">The Data Lake Analytics U-SQL activity in the pipeline refers to this linked service.</span><span class="sxs-lookup"><span data-stu-id="d04fe-124">The Data Lake Analytics U-SQL activity in the pipeline refers to this linked service.</span></span> 

<span data-ttu-id="d04fe-125">The following table provides descriptions for the generic properties used in the JSON definition.</span><span class="sxs-lookup"><span data-stu-id="d04fe-125">The following table provides descriptions for the generic properties used in the JSON definition.</span></span> <span data-ttu-id="d04fe-126">You can further choose between service principal and user credential authentication.</span><span class="sxs-lookup"><span data-stu-id="d04fe-126">You can further choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="d04fe-127">Property</span><span class="sxs-lookup"><span data-stu-id="d04fe-127">Property</span></span> | <span data-ttu-id="d04fe-128">Description</span><span class="sxs-lookup"><span data-stu-id="d04fe-128">Description</span></span> | <span data-ttu-id="d04fe-129">Required</span><span class="sxs-lookup"><span data-stu-id="d04fe-129">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d04fe-130">**type**</span><span class="sxs-lookup"><span data-stu-id="d04fe-130">**type**</span></span> |<span data-ttu-id="d04fe-131">The type property should be set to: **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="d04fe-131">The type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="d04fe-132">Yes</span><span class="sxs-lookup"><span data-stu-id="d04fe-132">Yes</span></span> |
| <span data-ttu-id="d04fe-133">**accountName**</span><span class="sxs-lookup"><span data-stu-id="d04fe-133">**accountName**</span></span> |<span data-ttu-id="d04fe-134">Azure Data Lake Analytics Account Name.</span><span class="sxs-lookup"><span data-stu-id="d04fe-134">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="d04fe-135">Yes</span><span class="sxs-lookup"><span data-stu-id="d04fe-135">Yes</span></span> |
| <span data-ttu-id="d04fe-136">**dataLakeAnalyticsUri**</span><span class="sxs-lookup"><span data-stu-id="d04fe-136">**dataLakeAnalyticsUri**</span></span> |<span data-ttu-id="d04fe-137">Azure Data Lake Analytics URI.</span><span class="sxs-lookup"><span data-stu-id="d04fe-137">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="d04fe-138">No</span><span class="sxs-lookup"><span data-stu-id="d04fe-138">No</span></span> |
| <span data-ttu-id="d04fe-139">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="d04fe-139">**subscriptionId**</span></span> |<span data-ttu-id="d04fe-140">Azure subscription id</span><span class="sxs-lookup"><span data-stu-id="d04fe-140">Azure subscription id</span></span> |<span data-ttu-id="d04fe-141">No (If not specified, subscription of the data factory is used).</span><span class="sxs-lookup"><span data-stu-id="d04fe-141">No (If not specified, subscription of the data factory is used).</span></span> |
| <span data-ttu-id="d04fe-142">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="d04fe-142">**resourceGroupName**</span></span> |<span data-ttu-id="d04fe-143">Azure resource group name</span><span class="sxs-lookup"><span data-stu-id="d04fe-143">Azure resource group name</span></span> |<span data-ttu-id="d04fe-144">No (If not specified, resource group of the data factory is used).</span><span class="sxs-lookup"><span data-stu-id="d04fe-144">No (If not specified, resource group of the data factory is used).</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="d04fe-145">Service principal authentication (recommended)</span><span class="sxs-lookup"><span data-stu-id="d04fe-145">Service principal authentication (recommended)</span></span>
<span data-ttu-id="d04fe-146">To use service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it the access to Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d04fe-146">To use service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it the access to Data Lake Store.</span></span> <span data-ttu-id="d04fe-147">For detailed steps, see [Service-to-service authentication](../../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="d04fe-147">For detailed steps, see [Service-to-service authentication](../../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="d04fe-148">Make note of the following values, which you use to define the linked service:</span><span class="sxs-lookup"><span data-stu-id="d04fe-148">Make note of the following values, which you use to define the linked service:</span></span>
* <span data-ttu-id="d04fe-149">Application ID</span><span class="sxs-lookup"><span data-stu-id="d04fe-149">Application ID</span></span>
* <span data-ttu-id="d04fe-150">Application key</span><span class="sxs-lookup"><span data-stu-id="d04fe-150">Application key</span></span> 
* <span data-ttu-id="d04fe-151">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="d04fe-151">Tenant ID</span></span>

<span data-ttu-id="d04fe-152">Use service principal authentication by specifying the following properties:</span><span class="sxs-lookup"><span data-stu-id="d04fe-152">Use service principal authentication by specifying the following properties:</span></span>

| <span data-ttu-id="d04fe-153">Property</span><span class="sxs-lookup"><span data-stu-id="d04fe-153">Property</span></span> | <span data-ttu-id="d04fe-154">Description</span><span class="sxs-lookup"><span data-stu-id="d04fe-154">Description</span></span> | <span data-ttu-id="d04fe-155">Required</span><span class="sxs-lookup"><span data-stu-id="d04fe-155">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d04fe-156">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="d04fe-156">**servicePrincipalId**</span></span> | <span data-ttu-id="d04fe-157">Specify the application's client ID.</span><span class="sxs-lookup"><span data-stu-id="d04fe-157">Specify the application's client ID.</span></span> | <span data-ttu-id="d04fe-158">Yes</span><span class="sxs-lookup"><span data-stu-id="d04fe-158">Yes</span></span> |
| <span data-ttu-id="d04fe-159">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="d04fe-159">**servicePrincipalKey**</span></span> | <span data-ttu-id="d04fe-160">Specify the application's key.</span><span class="sxs-lookup"><span data-stu-id="d04fe-160">Specify the application's key.</span></span> | <span data-ttu-id="d04fe-161">Yes</span><span class="sxs-lookup"><span data-stu-id="d04fe-161">Yes</span></span> |
| <span data-ttu-id="d04fe-162">**tenant**</span><span class="sxs-lookup"><span data-stu-id="d04fe-162">**tenant**</span></span> | <span data-ttu-id="d04fe-163">Specify the tenant information (domain name or tenant ID) under which your application resides.</span><span class="sxs-lookup"><span data-stu-id="d04fe-163">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="d04fe-164">You can retrieve it by hovering the mouse in the upper-right corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d04fe-164">You can retrieve it by hovering the mouse in the upper-right corner of the Azure portal.</span></span> | <span data-ttu-id="d04fe-165">Yes</span><span class="sxs-lookup"><span data-stu-id="d04fe-165">Yes</span></span> |

<span data-ttu-id="d04fe-166">**Example: Service principal authentication**</span><span class="sxs-lookup"><span data-stu-id="d04fe-166">**Example: Service principal authentication**</span></span>
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a><span data-ttu-id="d04fe-167">User credential authentication</span><span class="sxs-lookup"><span data-stu-id="d04fe-167">User credential authentication</span></span>
<span data-ttu-id="d04fe-168">Alternatively, you can use user credential authentication for Data Lake Analytics by specifying the following properties:</span><span class="sxs-lookup"><span data-stu-id="d04fe-168">Alternatively, you can use user credential authentication for Data Lake Analytics by specifying the following properties:</span></span>

| <span data-ttu-id="d04fe-169">Property</span><span class="sxs-lookup"><span data-stu-id="d04fe-169">Property</span></span> | <span data-ttu-id="d04fe-170">Description</span><span class="sxs-lookup"><span data-stu-id="d04fe-170">Description</span></span> | <span data-ttu-id="d04fe-171">Required</span><span class="sxs-lookup"><span data-stu-id="d04fe-171">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d04fe-172">**authorization**</span><span class="sxs-lookup"><span data-stu-id="d04fe-172">**authorization**</span></span> | <span data-ttu-id="d04fe-173">Click the **Authorize** button in the Data Factory Editor and enter your credential that assigns the autogenerated authorization URL to this property.</span><span class="sxs-lookup"><span data-stu-id="d04fe-173">Click the **Authorize** button in the Data Factory Editor and enter your credential that assigns the autogenerated authorization URL to this property.</span></span> | <span data-ttu-id="d04fe-174">Yes</span><span class="sxs-lookup"><span data-stu-id="d04fe-174">Yes</span></span> |
| <span data-ttu-id="d04fe-175">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="d04fe-175">**sessionId**</span></span> | <span data-ttu-id="d04fe-176">OAuth session ID from the OAuth authorization session.</span><span class="sxs-lookup"><span data-stu-id="d04fe-176">OAuth session ID from the OAuth authorization session.</span></span> <span data-ttu-id="d04fe-177">Each session ID is unique and can be used only once.</span><span class="sxs-lookup"><span data-stu-id="d04fe-177">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="d04fe-178">This setting is automatically generated when you use the Data Factory Editor.</span><span class="sxs-lookup"><span data-stu-id="d04fe-178">This setting is automatically generated when you use the Data Factory Editor.</span></span> | <span data-ttu-id="d04fe-179">Yes</span><span class="sxs-lookup"><span data-stu-id="d04fe-179">Yes</span></span> |

<span data-ttu-id="d04fe-180">**Example: User credential authentication**</span><span class="sxs-lookup"><span data-stu-id="d04fe-180">**Example: User credential authentication**</span></span>
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a><span data-ttu-id="d04fe-181">Token expiration</span><span class="sxs-lookup"><span data-stu-id="d04fe-181">Token expiration</span></span>
<span data-ttu-id="d04fe-182">The authorization code you generated by using the **Authorize** button expires after sometime.</span><span class="sxs-lookup"><span data-stu-id="d04fe-182">The authorization code you generated by using the **Authorize** button expires after sometime.</span></span> <span data-ttu-id="d04fe-183">See the following table for the expiration times for different types of user accounts.</span><span class="sxs-lookup"><span data-stu-id="d04fe-183">See the following table for the expiration times for different types of user accounts.</span></span> <span data-ttu-id="d04fe-184">You may see the following error message when the authentication **token expires**: Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span><span class="sxs-lookup"><span data-stu-id="d04fe-184">You may see the following error message when the authentication **token expires**: Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="d04fe-185">AADSTS70008: The provided access grant is expired or revoked.</span><span class="sxs-lookup"><span data-stu-id="d04fe-185">AADSTS70008: The provided access grant is expired or revoked.</span></span> <span data-ttu-id="d04fe-186">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21:09:31Z</span><span class="sxs-lookup"><span data-stu-id="d04fe-186">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21:09:31Z</span></span>

| <span data-ttu-id="d04fe-187">User type</span><span class="sxs-lookup"><span data-stu-id="d04fe-187">User type</span></span> | <span data-ttu-id="d04fe-188">Expires after</span><span class="sxs-lookup"><span data-stu-id="d04fe-188">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="d04fe-189">User accounts NOT managed by Azure Active Directory (@hotmail.com, @live.com, etc.)</span><span class="sxs-lookup"><span data-stu-id="d04fe-189">User accounts NOT managed by Azure Active Directory (@hotmail.com, @live.com, etc.)</span></span> |<span data-ttu-id="d04fe-190">12 hours</span><span class="sxs-lookup"><span data-stu-id="d04fe-190">12 hours</span></span> |
| <span data-ttu-id="d04fe-191">Users accounts managed by Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="d04fe-191">Users accounts managed by Azure Active Directory (AAD)</span></span> |<span data-ttu-id="d04fe-192">14 days after the last slice run.</span><span class="sxs-lookup"><span data-stu-id="d04fe-192">14 days after the last slice run.</span></span> <br/><br/><span data-ttu-id="d04fe-193">90 days, if a slice based on OAuth-based linked service runs at least once every 14 days.</span><span class="sxs-lookup"><span data-stu-id="d04fe-193">90 days, if a slice based on OAuth-based linked service runs at least once every 14 days.</span></span> |

<span data-ttu-id="d04fe-194">To avoid/resolve this error, reauthorize using the **Authorize** button when the **token expires** and redeploy the linked service.</span><span class="sxs-lookup"><span data-stu-id="d04fe-194">To avoid/resolve this error, reauthorize using the **Authorize** button when the **token expires** and redeploy the linked service.</span></span> <span data-ttu-id="d04fe-195">You can also generate values for **sessionId** and **authorization** properties programmatically using code as follows:</span><span class="sxs-lookup"><span data-stu-id="d04fe-195">You can also generate values for **sessionId** and **authorization** properties programmatically using code as follows:</span></span>

```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```

<span data-ttu-id="d04fe-196">See [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics for details about the Data Factory classes used in the code.</span><span class="sxs-lookup"><span data-stu-id="d04fe-196">See [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics for details about the Data Factory classes used in the code.</span></span> <span data-ttu-id="d04fe-197">Add a reference to: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll for the WindowsFormsWebAuthenticationDialog class.</span><span class="sxs-lookup"><span data-stu-id="d04fe-197">Add a reference to: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll for the WindowsFormsWebAuthenticationDialog class.</span></span> 

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="d04fe-198">Data Lake Analytics U-SQL Activity</span><span class="sxs-lookup"><span data-stu-id="d04fe-198">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="d04fe-199">The following JSON snippet defines a pipeline with a Data Lake Analytics U-SQL Activity.</span><span class="sxs-lookup"><span data-stu-id="d04fe-199">The following JSON snippet defines a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="d04fe-200">The activity definition has a reference to the Azure Data Lake Analytics linked service you created earlier.</span><span class="sxs-lookup"><span data-stu-id="d04fe-200">The activity definition has a reference to the Azure Data Lake Analytics linked service you created earlier.</span></span>   

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This is a pipeline to compute events for en-gb locale and date less than 2012/02/19.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00Z",
        "end": "2015-08-08T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="d04fe-201">The following table describes names and descriptions of properties that are specific to this activity.</span><span class="sxs-lookup"><span data-stu-id="d04fe-201">The following table describes names and descriptions of properties that are specific to this activity.</span></span> 

| <span data-ttu-id="d04fe-202">Property</span><span class="sxs-lookup"><span data-stu-id="d04fe-202">Property</span></span>            | <span data-ttu-id="d04fe-203">Description</span><span class="sxs-lookup"><span data-stu-id="d04fe-203">Description</span></span>                              | <span data-ttu-id="d04fe-204">Required</span><span class="sxs-lookup"><span data-stu-id="d04fe-204">Required</span></span>                                 |
| :------------------ | :--------------------------------------- | :--------------------------------------- |
| <span data-ttu-id="d04fe-205">type</span><span class="sxs-lookup"><span data-stu-id="d04fe-205">type</span></span>                | <span data-ttu-id="d04fe-206">The type property must be set to **DataLakeAnalyticsU-SQL**.</span><span class="sxs-lookup"><span data-stu-id="d04fe-206">The type property must be set to **DataLakeAnalyticsU-SQL**.</span></span> | <span data-ttu-id="d04fe-207">Yes</span><span class="sxs-lookup"><span data-stu-id="d04fe-207">Yes</span></span>                                      |
| <span data-ttu-id="d04fe-208">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="d04fe-208">linkedServiceName</span></span>   | <span data-ttu-id="d04fe-209">Reference to the Azure Data Lake Analytics registered as a linked service in Data Factory</span><span class="sxs-lookup"><span data-stu-id="d04fe-209">Reference to the Azure Data Lake Analytics registered as a linked service in Data Factory</span></span> | <span data-ttu-id="d04fe-210">Yes</span><span class="sxs-lookup"><span data-stu-id="d04fe-210">Yes</span></span>                                      |
| <span data-ttu-id="d04fe-211">scriptPath</span><span class="sxs-lookup"><span data-stu-id="d04fe-211">scriptPath</span></span>          | <span data-ttu-id="d04fe-212">Path to folder that contains the U-SQL script.</span><span class="sxs-lookup"><span data-stu-id="d04fe-212">Path to folder that contains the U-SQL script.</span></span> <span data-ttu-id="d04fe-213">Name of the file is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="d04fe-213">Name of the file is case-sensitive.</span></span> | <span data-ttu-id="d04fe-214">No (if you use script)</span><span class="sxs-lookup"><span data-stu-id="d04fe-214">No (if you use script)</span></span>                   |
| <span data-ttu-id="d04fe-215">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="d04fe-215">scriptLinkedService</span></span> | <span data-ttu-id="d04fe-216">Linked service that links the storage that contains the script to the data factory</span><span class="sxs-lookup"><span data-stu-id="d04fe-216">Linked service that links the storage that contains the script to the data factory</span></span> | <span data-ttu-id="d04fe-217">No (if you use script)</span><span class="sxs-lookup"><span data-stu-id="d04fe-217">No (if you use script)</span></span>                   |
| <span data-ttu-id="d04fe-218">script</span><span class="sxs-lookup"><span data-stu-id="d04fe-218">script</span></span>              | <span data-ttu-id="d04fe-219">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span><span class="sxs-lookup"><span data-stu-id="d04fe-219">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="d04fe-220">For example: `"script": "CREATE DATABASE test"`.</span><span class="sxs-lookup"><span data-stu-id="d04fe-220">For example: `"script": "CREATE DATABASE test"`.</span></span> | <span data-ttu-id="d04fe-221">No (if you use scriptPath and scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="d04fe-221">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="d04fe-222">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="d04fe-222">degreeOfParallelism</span></span> | <span data-ttu-id="d04fe-223">The maximum number of nodes simultaneously used to run the job.</span><span class="sxs-lookup"><span data-stu-id="d04fe-223">The maximum number of nodes simultaneously used to run the job.</span></span> | <span data-ttu-id="d04fe-224">No</span><span class="sxs-lookup"><span data-stu-id="d04fe-224">No</span></span>                                       |
| <span data-ttu-id="d04fe-225">priority</span><span class="sxs-lookup"><span data-stu-id="d04fe-225">priority</span></span>            | <span data-ttu-id="d04fe-226">Determines which jobs out of all that are queued should be selected to run first.</span><span class="sxs-lookup"><span data-stu-id="d04fe-226">Determines which jobs out of all that are queued should be selected to run first.</span></span> <span data-ttu-id="d04fe-227">The lower the number, the higher the priority.</span><span class="sxs-lookup"><span data-stu-id="d04fe-227">The lower the number, the higher the priority.</span></span> | <span data-ttu-id="d04fe-228">No</span><span class="sxs-lookup"><span data-stu-id="d04fe-228">No</span></span>                                       |
| <span data-ttu-id="d04fe-229">parameters</span><span class="sxs-lookup"><span data-stu-id="d04fe-229">parameters</span></span>          | <span data-ttu-id="d04fe-230">Parameters for the U-SQL script</span><span class="sxs-lookup"><span data-stu-id="d04fe-230">Parameters for the U-SQL script</span></span>          | <span data-ttu-id="d04fe-231">No</span><span class="sxs-lookup"><span data-stu-id="d04fe-231">No</span></span>                                       |
| <span data-ttu-id="d04fe-232">runtimeVersion</span><span class="sxs-lookup"><span data-stu-id="d04fe-232">runtimeVersion</span></span>      | <span data-ttu-id="d04fe-233">Runtime version of the U-SQL engine to use</span><span class="sxs-lookup"><span data-stu-id="d04fe-233">Runtime version of the U-SQL engine to use</span></span> | <span data-ttu-id="d04fe-234">No</span><span class="sxs-lookup"><span data-stu-id="d04fe-234">No</span></span>                                       |
| <span data-ttu-id="d04fe-235">compilationMode</span><span class="sxs-lookup"><span data-stu-id="d04fe-235">compilationMode</span></span>     | <p><span data-ttu-id="d04fe-236">Compilation mode of U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d04fe-236">Compilation mode of U-SQL.</span></span> <span data-ttu-id="d04fe-237">Must be one of these values:</span><span class="sxs-lookup"><span data-stu-id="d04fe-237">Must be one of these values:</span></span></p> <ul><li><span data-ttu-id="d04fe-238">**Semantic:** Only perform semantic checks and necessary sanity checks.</span><span class="sxs-lookup"><span data-stu-id="d04fe-238">**Semantic:** Only perform semantic checks and necessary sanity checks.</span></span></li><li><span data-ttu-id="d04fe-239">**Full:** Perform the full compilation, including syntax check, optimization, code generation, etc.</span><span class="sxs-lookup"><span data-stu-id="d04fe-239">**Full:** Perform the full compilation, including syntax check, optimization, code generation, etc.</span></span></li><li><span data-ttu-id="d04fe-240">**SingleBox:** Perform the full compilation, with TargetType setting to SingleBox.</span><span class="sxs-lookup"><span data-stu-id="d04fe-240">**SingleBox:** Perform the full compilation, with TargetType setting to SingleBox.</span></span></li></ul><p><span data-ttu-id="d04fe-241">If you don't specify a value for this property, the server determines the optimal compilation mode.</span><span class="sxs-lookup"><span data-stu-id="d04fe-241">If you don't specify a value for this property, the server determines the optimal compilation mode.</span></span> </p> | <span data-ttu-id="d04fe-242">No</span><span class="sxs-lookup"><span data-stu-id="d04fe-242">No</span></span>                                       |

<span data-ttu-id="d04fe-243">See [SearchLogProcessing.txt Script Definition](#sample-u-sql-script) for the script definition.</span><span class="sxs-lookup"><span data-stu-id="d04fe-243">See [SearchLogProcessing.txt Script Definition](#sample-u-sql-script) for the script definition.</span></span> 

## <a name="sample-input-and-output-datasets"></a><span data-ttu-id="d04fe-244">Sample input and output datasets</span><span class="sxs-lookup"><span data-stu-id="d04fe-244">Sample input and output datasets</span></span>
### <a name="input-dataset"></a><span data-ttu-id="d04fe-245">Input dataset</span><span class="sxs-lookup"><span data-stu-id="d04fe-245">Input dataset</span></span>
<span data-ttu-id="d04fe-246">In this example, the input data resides in an Azure Data Lake Store (SearchLog.tsv file in the datalake/input folder).</span><span class="sxs-lookup"><span data-stu-id="d04fe-246">In this example, the input data resides in an Azure Data Lake Store (SearchLog.tsv file in the datalake/input folder).</span></span> 

```json
{
    "name": "DataLakeTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}    
```

### <a name="output-dataset"></a><span data-ttu-id="d04fe-247">Output dataset</span><span class="sxs-lookup"><span data-stu-id="d04fe-247">Output dataset</span></span>
<span data-ttu-id="d04fe-248">In this example, the output data produced by the U-SQL script is stored in an Azure Data Lake Store (datalake/output folder).</span><span class="sxs-lookup"><span data-stu-id="d04fe-248">In this example, the output data produced by the U-SQL script is stored in an Azure Data Lake Store (datalake/output folder).</span></span> 

```json
{
    "name": "EventsByRegionTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="sample-data-lake-store-linked-service"></a><span data-ttu-id="d04fe-249">Sample Data Lake Store Linked Service</span><span class="sxs-lookup"><span data-stu-id="d04fe-249">Sample Data Lake Store Linked Service</span></span>
<span data-ttu-id="d04fe-250">Here is the definition of the sample Azure Data Lake Store linked service used by the input/output datasets.</span><span class="sxs-lookup"><span data-stu-id="d04fe-250">Here is the definition of the sample Azure Data Lake Store linked service used by the input/output datasets.</span></span> 

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
        }
    }
}
```

<span data-ttu-id="d04fe-251">See [Move data to and from Azure Data Lake Store](data-factory-azure-datalake-connector.md) article for descriptions of JSON properties.</span><span class="sxs-lookup"><span data-stu-id="d04fe-251">See [Move data to and from Azure Data Lake Store](data-factory-azure-datalake-connector.md) article for descriptions of JSON properties.</span></span> 

## <a name="sample-u-sql-script"></a><span data-ttu-id="d04fe-252">Sample U-SQL Script</span><span class="sxs-lookup"><span data-stu-id="d04fe-252">Sample U-SQL Script</span></span>

```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM @in
    USING Extractors.Tsv(nullEscape:"#NULL#");

@rs1 =
    SELECT Start, Region, Duration
    FROM @searchlog
WHERE Region == "en-gb";

@rs1 =
    SELECT Start, Region, Duration
    FROM @rs1
    WHERE Start <= DateTime.Parse("2012/02/19");

OUTPUT @rs1   
    TO @out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

<span data-ttu-id="d04fe-253">The values for **@in** and **@out** parameters in the U-SQL script are passed dynamically by ADF using the ‘parameters’ section.</span><span class="sxs-lookup"><span data-stu-id="d04fe-253">The values for **@in** and **@out** parameters in the U-SQL script are passed dynamically by ADF using the ‘parameters’ section.</span></span> <span data-ttu-id="d04fe-254">See the ‘parameters’ section in the pipeline definition.</span><span class="sxs-lookup"><span data-stu-id="d04fe-254">See the ‘parameters’ section in the pipeline definition.</span></span>

<span data-ttu-id="d04fe-255">You can specify other properties such as degreeOfParallelism and priority as well in your pipeline definition for the jobs that run on the Azure Data Lake Analytics service.</span><span class="sxs-lookup"><span data-stu-id="d04fe-255">You can specify other properties such as degreeOfParallelism and priority as well in your pipeline definition for the jobs that run on the Azure Data Lake Analytics service.</span></span>

## <a name="dynamic-parameters"></a><span data-ttu-id="d04fe-256">Dynamic parameters</span><span class="sxs-lookup"><span data-stu-id="d04fe-256">Dynamic parameters</span></span>
<span data-ttu-id="d04fe-257">In the sample pipeline definition, in and out parameters are assigned with hard-coded values.</span><span class="sxs-lookup"><span data-stu-id="d04fe-257">In the sample pipeline definition, in and out parameters are assigned with hard-coded values.</span></span> 

```json
"parameters": {
    "in": "/datalake/input/SearchLog.tsv",
    "out": "/datalake/output/Result.tsv"
}
```

<span data-ttu-id="d04fe-258">It is possible to use dynamic parameters instead.</span><span class="sxs-lookup"><span data-stu-id="d04fe-258">It is possible to use dynamic parameters instead.</span></span> <span data-ttu-id="d04fe-259">For example:</span><span class="sxs-lookup"><span data-stu-id="d04fe-259">For example:</span></span> 

```json
"parameters": {
    "in": "$$Text.Format('/datalake/input/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)",
    "out": "$$Text.Format('/datalake/output/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)"
}
```

<span data-ttu-id="d04fe-260">In this case, input files are still picked up from the /datalake/input folder and output files are generated in the /datalake/output folder.</span><span class="sxs-lookup"><span data-stu-id="d04fe-260">In this case, input files are still picked up from the /datalake/input folder and output files are generated in the /datalake/output folder.</span></span> <span data-ttu-id="d04fe-261">The file names are dynamic based on the slice start time.</span><span class="sxs-lookup"><span data-stu-id="d04fe-261">The file names are dynamic based on the slice start time.</span></span>  


