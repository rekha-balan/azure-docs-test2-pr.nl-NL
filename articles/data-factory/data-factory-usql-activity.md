---
title: Transform data using U-SQL script - Azure | Microsoft Docs
description: Learn how to process or transform data by running U-SQL scripts on Azure Data Lake Analytics compute service.
services: data-factory
documentationcenter: ''
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e17c1255-62c2-4e2e-bb60-d25274903e80
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/07/2017
ms.author: spelluru
ms.openlocfilehash: b41d906d6948f0f9e3cdb38b4a478b39f55ce219
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555797"
---
# <a name="transform-data-by-running-u-sql-scripts-on-azure-data-lake-analytics"></a><span data-ttu-id="7a5e8-103">Transform data by running U-SQL scripts on Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="7a5e8-103">Transform data by running U-SQL scripts on Azure Data Lake Analytics</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Hive Activity](data-factory-hive-activity.md) 
> * [Pig Activity](data-factory-pig-activity.md)
> * [MapReduce Activity](data-factory-map-reduce.md)
> * [Hadoop Streaming Activity](data-factory-hadoop-streaming-activity.md)
> * [Spark Activity](data-factory-spark.md)
> * [Machine Learning Batch Execution Activity](data-factory-azure-ml-batch-execution-activity.md)
> * [Machine Learning Update Resource Activity](data-factory-azure-ml-update-resource-activity.md)
> * [Stored Procedure Activity](data-factory-stored-proc-activity.md)
> * [Data Lake Analytics U-SQL Activity](data-factory-usql-activity.md)
> * [.NET Custom Activity](data-factory-use-custom-activities.md)

<span data-ttu-id="7a5e8-114">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-114">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="7a5e8-115">It contains a sequence of activities where each activity performs a specific processing operation.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-115">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="7a5e8-116">This article describes the **Data Lake Analytics U-SQL Activity** that runs a **U-SQL** script on an **Azure Data Lake Analytics** compute linked service.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-116">This article describes the **Data Lake Analytics U-SQL Activity** that runs a **U-SQL** script on an **Azure Data Lake Analytics** compute linked service.</span></span> 

> [!NOTE]
> Create an Azure Data Lake Analytics account before creating a pipeline with a Data Lake Analytics U-SQL Activity. To learn about Azure Data Lake Analytics, see [Get started with Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md).
> 
> Review the [Build your first pipeline tutorial](data-factory-build-your-first-pipeline.md) for detailed steps to create a data factory, linked services, datasets, and a pipeline. Use JSON snippets with Data Factory Editor or Visual Studio or Azure PowerShell to create Data Factory entities.
> 
> 

## <a name="azure-data-lake-analytics-linked-service"></a><span data-ttu-id="7a5e8-121">Azure Data Lake Analytics Linked Service</span><span class="sxs-lookup"><span data-stu-id="7a5e8-121">Azure Data Lake Analytics Linked Service</span></span>
<span data-ttu-id="7a5e8-122">You create an **Azure Data Lake Analytics** linked service to link an Azure Data Lake Analytics compute service to an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-122">You create an **Azure Data Lake Analytics** linked service to link an Azure Data Lake Analytics compute service to an Azure data factory.</span></span> <span data-ttu-id="7a5e8-123">The Data Lake Analytics U-SQL activity in the pipeline refers to this linked service.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-123">The Data Lake Analytics U-SQL activity in the pipeline refers to this linked service.</span></span> 

<span data-ttu-id="7a5e8-124">The following example provides JSON definition for an Azure Data Lake Analytics linked service.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-124">The following example provides JSON definition for an Azure Data Lake Analytics linked service.</span></span> 

```JSON
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<subscription id>",
            "resourceGroupName": "<resource group name>"
        }
    }
}
```

<span data-ttu-id="7a5e8-125">The following table provides descriptions for the properties used in the JSON definition.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-125">The following table provides descriptions for the properties used in the JSON definition.</span></span> 

| <span data-ttu-id="7a5e8-126">Property</span><span class="sxs-lookup"><span data-stu-id="7a5e8-126">Property</span></span> | <span data-ttu-id="7a5e8-127">Description</span><span class="sxs-lookup"><span data-stu-id="7a5e8-127">Description</span></span> | <span data-ttu-id="7a5e8-128">Required</span><span class="sxs-lookup"><span data-stu-id="7a5e8-128">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7a5e8-129">Type</span><span class="sxs-lookup"><span data-stu-id="7a5e8-129">Type</span></span> |<span data-ttu-id="7a5e8-130">The type property should be set to: **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-130">The type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="7a5e8-131">Yes</span><span class="sxs-lookup"><span data-stu-id="7a5e8-131">Yes</span></span> |
| <span data-ttu-id="7a5e8-132">accountName</span><span class="sxs-lookup"><span data-stu-id="7a5e8-132">accountName</span></span> |<span data-ttu-id="7a5e8-133">Azure Data Lake Analytics Account Name.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-133">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="7a5e8-134">Yes</span><span class="sxs-lookup"><span data-stu-id="7a5e8-134">Yes</span></span> |
| <span data-ttu-id="7a5e8-135">dataLakeAnalyticsUri</span><span class="sxs-lookup"><span data-stu-id="7a5e8-135">dataLakeAnalyticsUri</span></span> |<span data-ttu-id="7a5e8-136">Azure Data Lake Analytics URI.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-136">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="7a5e8-137">No</span><span class="sxs-lookup"><span data-stu-id="7a5e8-137">No</span></span> |
| <span data-ttu-id="7a5e8-138">authorization</span><span class="sxs-lookup"><span data-stu-id="7a5e8-138">authorization</span></span> |<span data-ttu-id="7a5e8-139">Authorization code is automatically retrieved after clicking **Authorize** button in the Data Factory Editor and completing the OAuth login.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-139">Authorization code is automatically retrieved after clicking **Authorize** button in the Data Factory Editor and completing the OAuth login.</span></span> |<span data-ttu-id="7a5e8-140">Yes</span><span class="sxs-lookup"><span data-stu-id="7a5e8-140">Yes</span></span> |
| <span data-ttu-id="7a5e8-141">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="7a5e8-141">subscriptionId</span></span> |<span data-ttu-id="7a5e8-142">Azure subscription id</span><span class="sxs-lookup"><span data-stu-id="7a5e8-142">Azure subscription id</span></span> |<span data-ttu-id="7a5e8-143">No (If not specified, subscription of the data factory is used).</span><span class="sxs-lookup"><span data-stu-id="7a5e8-143">No (If not specified, subscription of the data factory is used).</span></span> |
| <span data-ttu-id="7a5e8-144">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="7a5e8-144">resourceGroupName</span></span> |<span data-ttu-id="7a5e8-145">Azure resource group name</span><span class="sxs-lookup"><span data-stu-id="7a5e8-145">Azure resource group name</span></span> |<span data-ttu-id="7a5e8-146">No (If not specified, resource group of the data factory is used).</span><span class="sxs-lookup"><span data-stu-id="7a5e8-146">No (If not specified, resource group of the data factory is used).</span></span> |
| <span data-ttu-id="7a5e8-147">sessionId</span><span class="sxs-lookup"><span data-stu-id="7a5e8-147">sessionId</span></span> |<span data-ttu-id="7a5e8-148">session id from the OAuth authorization session.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-148">session id from the OAuth authorization session.</span></span> <span data-ttu-id="7a5e8-149">Each session id is unique and may only be used once.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-149">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="7a5e8-150">The session Id is auto-generated in the Data Factory Editor.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-150">The session Id is auto-generated in the Data Factory Editor.</span></span> |<span data-ttu-id="7a5e8-151">Yes</span><span class="sxs-lookup"><span data-stu-id="7a5e8-151">Yes</span></span> |

<span data-ttu-id="7a5e8-152">The authorization code you generated by using the **Authorize** button expires after sometime.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-152">The authorization code you generated by using the **Authorize** button expires after sometime.</span></span> <span data-ttu-id="7a5e8-153">See the following table for the expiration times for different types of user accounts.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-153">See the following table for the expiration times for different types of user accounts.</span></span> <span data-ttu-id="7a5e8-154">You may see the following error message when the authentication **token expires**: Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-154">You may see the following error message when the authentication **token expires**: Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="7a5e8-155">AADSTS70008: The provided access grant is expired or revoked.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-155">AADSTS70008: The provided access grant is expired or revoked.</span></span> <span data-ttu-id="7a5e8-156">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21:09:31Z</span><span class="sxs-lookup"><span data-stu-id="7a5e8-156">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21:09:31Z</span></span>

| <span data-ttu-id="7a5e8-157">User type</span><span class="sxs-lookup"><span data-stu-id="7a5e8-157">User type</span></span> | <span data-ttu-id="7a5e8-158">Expires after</span><span class="sxs-lookup"><span data-stu-id="7a5e8-158">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="7a5e8-159">User accounts NOT managed by Azure Active Directory (@hotmail.com, @live.com, etc.)</span><span class="sxs-lookup"><span data-stu-id="7a5e8-159">User accounts NOT managed by Azure Active Directory (@hotmail.com, @live.com, etc.)</span></span> |<span data-ttu-id="7a5e8-160">12 hours</span><span class="sxs-lookup"><span data-stu-id="7a5e8-160">12 hours</span></span> |
| <span data-ttu-id="7a5e8-161">Users accounts managed by Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="7a5e8-161">Users accounts managed by Azure Active Directory (AAD)</span></span> |<span data-ttu-id="7a5e8-162">14 days after the last slice run.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-162">14 days after the last slice run.</span></span> <br/><br/><span data-ttu-id="7a5e8-163">90 days, if a slice based on OAuth-based linked service runs at least once every 14 days.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-163">90 days, if a slice based on OAuth-based linked service runs at least once every 14 days.</span></span> |

<span data-ttu-id="7a5e8-164">To avoid/resolve this error, reauthorize using the **Authorize** button when the **token expires** and redeploy the linked service.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-164">To avoid/resolve this error, reauthorize using the **Authorize** button when the **token expires** and redeploy the linked service.</span></span> <span data-ttu-id="7a5e8-165">You can also generate values for **sessionId** and **authorization** properties programmatically using code in the following section.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-165">You can also generate values for **sessionId** and **authorization** properties programmatically using code in the following section.</span></span> 

### <a name="to-programmatically-generate-sessionid-and-authorization-values"></a><span data-ttu-id="7a5e8-166">To programmatically generate sessionId and authorization values</span><span class="sxs-lookup"><span data-stu-id="7a5e8-166">To programmatically generate sessionId and authorization values</span></span>

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

<span data-ttu-id="7a5e8-167">See [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics for details about the Data Factory classes used in the code.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-167">See [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics for details about the Data Factory classes used in the code.</span></span> <span data-ttu-id="7a5e8-168">Add a reference to: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll for the WindowsFormsWebAuthenticationDialog class.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-168">Add a reference to: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll for the WindowsFormsWebAuthenticationDialog class.</span></span> 

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="7a5e8-169">Data Lake Analytics U-SQL Activity</span><span class="sxs-lookup"><span data-stu-id="7a5e8-169">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="7a5e8-170">The following JSON snippet defines a pipeline with a Data Lake Analytics U-SQL Activity.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-170">The following JSON snippet defines a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="7a5e8-171">The activity definition has a reference to the Azure Data Lake Analytics linked service you created earlier.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-171">The activity definition has a reference to the Azure Data Lake Analytics linked service you created earlier.</span></span>   

```JSON
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

<span data-ttu-id="7a5e8-172">The following table describes names and descriptions of properties that are specific to this activity.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-172">The following table describes names and descriptions of properties that are specific to this activity.</span></span> 

| <span data-ttu-id="7a5e8-173">Property</span><span class="sxs-lookup"><span data-stu-id="7a5e8-173">Property</span></span> | <span data-ttu-id="7a5e8-174">Description</span><span class="sxs-lookup"><span data-stu-id="7a5e8-174">Description</span></span> | <span data-ttu-id="7a5e8-175">Required</span><span class="sxs-lookup"><span data-stu-id="7a5e8-175">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7a5e8-176">type</span><span class="sxs-lookup"><span data-stu-id="7a5e8-176">type</span></span> |<span data-ttu-id="7a5e8-177">The type property must be set to **DataLakeAnalyticsU-SQL**.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-177">The type property must be set to **DataLakeAnalyticsU-SQL**.</span></span> |<span data-ttu-id="7a5e8-178">Yes</span><span class="sxs-lookup"><span data-stu-id="7a5e8-178">Yes</span></span> |
| <span data-ttu-id="7a5e8-179">scriptPath</span><span class="sxs-lookup"><span data-stu-id="7a5e8-179">scriptPath</span></span> |<span data-ttu-id="7a5e8-180">Path to folder that contains the U-SQL script.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-180">Path to folder that contains the U-SQL script.</span></span> <span data-ttu-id="7a5e8-181">Name of the file is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-181">Name of the file is case-sensitive.</span></span> |<span data-ttu-id="7a5e8-182">No (if you use script)</span><span class="sxs-lookup"><span data-stu-id="7a5e8-182">No (if you use script)</span></span> |
| <span data-ttu-id="7a5e8-183">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="7a5e8-183">scriptLinkedService</span></span> |<span data-ttu-id="7a5e8-184">Linked service that links the storage that contains the script to the data factory</span><span class="sxs-lookup"><span data-stu-id="7a5e8-184">Linked service that links the storage that contains the script to the data factory</span></span> |<span data-ttu-id="7a5e8-185">No (if you use script)</span><span class="sxs-lookup"><span data-stu-id="7a5e8-185">No (if you use script)</span></span> |
| <span data-ttu-id="7a5e8-186">script</span><span class="sxs-lookup"><span data-stu-id="7a5e8-186">script</span></span> |<span data-ttu-id="7a5e8-187">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-187">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="7a5e8-188">For example: "script": "CREATE DATABASE test".</span><span class="sxs-lookup"><span data-stu-id="7a5e8-188">For example: "script": "CREATE DATABASE test".</span></span> |<span data-ttu-id="7a5e8-189">No (if you use scriptPath and scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="7a5e8-189">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="7a5e8-190">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="7a5e8-190">degreeOfParallelism</span></span> |<span data-ttu-id="7a5e8-191">The maximum number of nodes simultaneously used to run the job.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-191">The maximum number of nodes simultaneously used to run the job.</span></span> |<span data-ttu-id="7a5e8-192">No</span><span class="sxs-lookup"><span data-stu-id="7a5e8-192">No</span></span> |
| <span data-ttu-id="7a5e8-193">priority</span><span class="sxs-lookup"><span data-stu-id="7a5e8-193">priority</span></span> |<span data-ttu-id="7a5e8-194">Determines which jobs out of all that are queued should be selected to run first.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-194">Determines which jobs out of all that are queued should be selected to run first.</span></span> <span data-ttu-id="7a5e8-195">The lower the number, the higher the priority.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-195">The lower the number, the higher the priority.</span></span> |<span data-ttu-id="7a5e8-196">No</span><span class="sxs-lookup"><span data-stu-id="7a5e8-196">No</span></span> |
| <span data-ttu-id="7a5e8-197">parameters</span><span class="sxs-lookup"><span data-stu-id="7a5e8-197">parameters</span></span> |<span data-ttu-id="7a5e8-198">Parameters for the U-SQL script</span><span class="sxs-lookup"><span data-stu-id="7a5e8-198">Parameters for the U-SQL script</span></span> |<span data-ttu-id="7a5e8-199">No</span><span class="sxs-lookup"><span data-stu-id="7a5e8-199">No</span></span> |

<span data-ttu-id="7a5e8-200">See [SearchLogProcessing.txt Script Definition](#script-definition) for the script definition.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-200">See [SearchLogProcessing.txt Script Definition](#script-definition) for the script definition.</span></span> 

## <a name="sample-input-and-output-datasets"></a><span data-ttu-id="7a5e8-201">Sample input and output datasets</span><span class="sxs-lookup"><span data-stu-id="7a5e8-201">Sample input and output datasets</span></span>
### <a name="input-dataset"></a><span data-ttu-id="7a5e8-202">Input dataset</span><span class="sxs-lookup"><span data-stu-id="7a5e8-202">Input dataset</span></span>
<span data-ttu-id="7a5e8-203">In this example, the input data resides in an Azure Data Lake Store (SearchLog.tsv file in the datalake/input folder).</span><span class="sxs-lookup"><span data-stu-id="7a5e8-203">In this example, the input data resides in an Azure Data Lake Store (SearchLog.tsv file in the datalake/input folder).</span></span> 

```JSON
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

### <a name="output-dataset"></a><span data-ttu-id="7a5e8-204">Output dataset</span><span class="sxs-lookup"><span data-stu-id="7a5e8-204">Output dataset</span></span>
<span data-ttu-id="7a5e8-205">In this example, the output data produced by the U-SQL script is stored in an Azure Data Lake Store (datalake/output folder).</span><span class="sxs-lookup"><span data-stu-id="7a5e8-205">In this example, the output data produced by the U-SQL script is stored in an Azure Data Lake Store (datalake/output folder).</span></span> 

```JSON
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

### <a name="sample-data-lake-store-linked-service"></a><span data-ttu-id="7a5e8-206">Sample Data Lake Store Linked Service</span><span class="sxs-lookup"><span data-stu-id="7a5e8-206">Sample Data Lake Store Linked Service</span></span>
<span data-ttu-id="7a5e8-207">Here is the definition of the sample Azure Data Lake Store linked service used by the input/output datasets.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-207">Here is the definition of the sample Azure Data Lake Store linked service used by the input/output datasets.</span></span> 

```JSON
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>"
        }
    }
}
```

<span data-ttu-id="7a5e8-208">See [Move data to and from Azure Data Lake Store](data-factory-azure-datalake-connector.md) article for descriptions of JSON properties.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-208">See [Move data to and from Azure Data Lake Store](data-factory-azure-datalake-connector.md) article for descriptions of JSON properties.</span></span> 

## <a name="sample-u-sql-script"></a><span data-ttu-id="7a5e8-209">Sample U-SQL Script</span><span class="sxs-lookup"><span data-stu-id="7a5e8-209">Sample U-SQL Script</span></span>

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

<span data-ttu-id="7a5e8-210">The values for **@in** and **@out** parameters in the U-SQL script are passed dynamically by ADF using the ‘parameters’ section.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-210">The values for **@in** and **@out** parameters in the U-SQL script are passed dynamically by ADF using the ‘parameters’ section.</span></span> <span data-ttu-id="7a5e8-211">See the ‘parameters’ section in the pipeline definition.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-211">See the ‘parameters’ section in the pipeline definition.</span></span>

<span data-ttu-id="7a5e8-212">You can specify other properties such as degreeOfParallelism and priority as well in your pipeline definition for the jobs that run on the Azure Data Lake Analytics service.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-212">You can specify other properties such as degreeOfParallelism and priority as well in your pipeline definition for the jobs that run on the Azure Data Lake Analytics service.</span></span>

## <a name="dynamic-parameters"></a><span data-ttu-id="7a5e8-213">Dynamic parameters</span><span class="sxs-lookup"><span data-stu-id="7a5e8-213">Dynamic parameters</span></span>
<span data-ttu-id="7a5e8-214">In the sample pipeline definition, in and out parameters are assigned with hard-coded values.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-214">In the sample pipeline definition, in and out parameters are assigned with hard-coded values.</span></span> 

```JSON
"parameters": {
    "in": "/datalake/input/SearchLog.tsv",
    "out": "/datalake/output/Result.tsv"
}
```

<span data-ttu-id="7a5e8-215">It is possible to use dynamic parameters instead.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-215">It is possible to use dynamic parameters instead.</span></span> <span data-ttu-id="7a5e8-216">For example:</span><span class="sxs-lookup"><span data-stu-id="7a5e8-216">For example:</span></span> 

```JSON
"parameters": {
    "in": "$$Text.Format('/datalake/input/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)",
    "out": "$$Text.Format('/datalake/output/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)"
}
```

<span data-ttu-id="7a5e8-217">In this case, input files are still picked up from the /datalake/input folder and output files are generated in the /datalake/output folder.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-217">In this case, input files are still picked up from the /datalake/input folder and output files are generated in the /datalake/output folder.</span></span> <span data-ttu-id="7a5e8-218">The file names are dynamic based on the slice start time.</span><span class="sxs-lookup"><span data-stu-id="7a5e8-218">The file names are dynamic based on the slice start time.</span></span>  

