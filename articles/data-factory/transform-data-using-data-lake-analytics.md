---
title: Transform data using U-SQL script - Azure | Microsoft Docs
description: Learn how to process or transform data by running U-SQL scripts on Azure Data Lake Analytics compute service.
services: data-factory
documentationcenter: ''
author: nabhishek
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 08/01/2018
ms.author: abnarain
ms.openlocfilehash: cbe4d3931a5e7b279218a1f56a3842efbc238780
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867531"
---
# <a name="transform-data-by-running-u-sql-scripts-on-azure-data-lake-analytics"></a><span data-ttu-id="cf72f-103">Transform data by running U-SQL scripts on Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="cf72f-103">Transform data by running U-SQL scripts on Azure Data Lake Analytics</span></span> 
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-usql-activity.md)
> * [Current version](transform-data-using-data-lake-analytics.md)

<span data-ttu-id="cf72f-106">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span><span class="sxs-lookup"><span data-stu-id="cf72f-106">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="cf72f-107">It contains a sequence of activities where each activity performs a specific processing operation.</span><span class="sxs-lookup"><span data-stu-id="cf72f-107">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="cf72f-108">This article describes the **Data Lake Analytics U-SQL Activity** that runs a **U-SQL** script on an **Azure Data Lake Analytics** compute linked service.</span><span class="sxs-lookup"><span data-stu-id="cf72f-108">This article describes the **Data Lake Analytics U-SQL Activity** that runs a **U-SQL** script on an **Azure Data Lake Analytics** compute linked service.</span></span> 

<span data-ttu-id="cf72f-109">Create an Azure Data Lake Analytics account before creating a pipeline with a Data Lake Analytics U-SQL Activity.</span><span class="sxs-lookup"><span data-stu-id="cf72f-109">Create an Azure Data Lake Analytics account before creating a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="cf72f-110">To learn about Azure Data Lake Analytics, see [Get started with Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cf72f-110">To learn about Azure Data Lake Analytics, see [Get started with Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span>


## <a name="azure-data-lake-analytics-linked-service"></a><span data-ttu-id="cf72f-111">Azure Data Lake Analytics linked service</span><span class="sxs-lookup"><span data-stu-id="cf72f-111">Azure Data Lake Analytics linked service</span></span>
<span data-ttu-id="cf72f-112">You create an **Azure Data Lake Analytics** linked service to link an Azure Data Lake Analytics compute service to an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="cf72f-112">You create an **Azure Data Lake Analytics** linked service to link an Azure Data Lake Analytics compute service to an Azure data factory.</span></span> <span data-ttu-id="cf72f-113">The Data Lake Analytics U-SQL activity in the pipeline refers to this linked service.</span><span class="sxs-lookup"><span data-stu-id="cf72f-113">The Data Lake Analytics U-SQL activity in the pipeline refers to this linked service.</span></span> 

<span data-ttu-id="cf72f-114">The following table provides descriptions for the generic properties used in the JSON definition.</span><span class="sxs-lookup"><span data-stu-id="cf72f-114">The following table provides descriptions for the generic properties used in the JSON definition.</span></span> 

| <span data-ttu-id="cf72f-115">Property</span><span class="sxs-lookup"><span data-stu-id="cf72f-115">Property</span></span>                 | <span data-ttu-id="cf72f-116">Description</span><span class="sxs-lookup"><span data-stu-id="cf72f-116">Description</span></span>                              | <span data-ttu-id="cf72f-117">Required</span><span class="sxs-lookup"><span data-stu-id="cf72f-117">Required</span></span>                                 |
| ------------------------ | ---------------------------------------- | ---------------------------------------- |
| <span data-ttu-id="cf72f-118">**type**</span><span class="sxs-lookup"><span data-stu-id="cf72f-118">**type**</span></span>                 | <span data-ttu-id="cf72f-119">The type property should be set to: **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="cf72f-119">The type property should be set to: **AzureDataLakeAnalytics**.</span></span> | <span data-ttu-id="cf72f-120">Yes</span><span class="sxs-lookup"><span data-stu-id="cf72f-120">Yes</span></span>                                      |
| <span data-ttu-id="cf72f-121">**accountName**</span><span class="sxs-lookup"><span data-stu-id="cf72f-121">**accountName**</span></span>          | <span data-ttu-id="cf72f-122">Azure Data Lake Analytics Account Name.</span><span class="sxs-lookup"><span data-stu-id="cf72f-122">Azure Data Lake Analytics Account Name.</span></span>  | <span data-ttu-id="cf72f-123">Yes</span><span class="sxs-lookup"><span data-stu-id="cf72f-123">Yes</span></span>                                      |
| <span data-ttu-id="cf72f-124">**dataLakeAnalyticsUri**</span><span class="sxs-lookup"><span data-stu-id="cf72f-124">**dataLakeAnalyticsUri**</span></span> | <span data-ttu-id="cf72f-125">Azure Data Lake Analytics URI.</span><span class="sxs-lookup"><span data-stu-id="cf72f-125">Azure Data Lake Analytics URI.</span></span>           | <span data-ttu-id="cf72f-126">No</span><span class="sxs-lookup"><span data-stu-id="cf72f-126">No</span></span>                                       |
| <span data-ttu-id="cf72f-127">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="cf72f-127">**subscriptionId**</span></span>       | <span data-ttu-id="cf72f-128">Azure subscription ID</span><span class="sxs-lookup"><span data-stu-id="cf72f-128">Azure subscription ID</span></span>                    | <span data-ttu-id="cf72f-129">No</span><span class="sxs-lookup"><span data-stu-id="cf72f-129">No</span></span>                                       |
| <span data-ttu-id="cf72f-130">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="cf72f-130">**resourceGroupName**</span></span>    | <span data-ttu-id="cf72f-131">Azure resource group name</span><span class="sxs-lookup"><span data-stu-id="cf72f-131">Azure resource group name</span></span>                | <span data-ttu-id="cf72f-132">No</span><span class="sxs-lookup"><span data-stu-id="cf72f-132">No</span></span>                                       |

### <a name="service-principal-authentication"></a><span data-ttu-id="cf72f-133">Service principal authentication</span><span class="sxs-lookup"><span data-stu-id="cf72f-133">Service principal authentication</span></span>
<span data-ttu-id="cf72f-134">The Azure Data Lake Analytics linked service requires a service principal authentication to connect to the Azure Data Lake Analytics service.</span><span class="sxs-lookup"><span data-stu-id="cf72f-134">The Azure Data Lake Analytics linked service requires a service principal authentication to connect to the Azure Data Lake Analytics service.</span></span> <span data-ttu-id="cf72f-135">To use service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it the access to both the Data Lake Analytics and the Data Lake Store it uses.</span><span class="sxs-lookup"><span data-stu-id="cf72f-135">To use service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it the access to both the Data Lake Analytics and the Data Lake Store it uses.</span></span> <span data-ttu-id="cf72f-136">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="cf72f-136">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="cf72f-137">Make note of the following values, which you use to define the linked service:</span><span class="sxs-lookup"><span data-stu-id="cf72f-137">Make note of the following values, which you use to define the linked service:</span></span>

* <span data-ttu-id="cf72f-138">Application ID</span><span class="sxs-lookup"><span data-stu-id="cf72f-138">Application ID</span></span>
* <span data-ttu-id="cf72f-139">Application key</span><span class="sxs-lookup"><span data-stu-id="cf72f-139">Application key</span></span> 
* <span data-ttu-id="cf72f-140">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="cf72f-140">Tenant ID</span></span>

<span data-ttu-id="cf72f-141">Grant service principal permission to your Azure Data Lake Anatlyics using the [Add User Wizard](../data-lake-analytics/data-lake-analytics-manage-use-portal.md#add-a-new-user).</span><span class="sxs-lookup"><span data-stu-id="cf72f-141">Grant service principal permission to your Azure Data Lake Anatlyics using the [Add User Wizard](../data-lake-analytics/data-lake-analytics-manage-use-portal.md#add-a-new-user).</span></span>

<span data-ttu-id="cf72f-142">Use service principal authentication by specifying the following properties:</span><span class="sxs-lookup"><span data-stu-id="cf72f-142">Use service principal authentication by specifying the following properties:</span></span>

| <span data-ttu-id="cf72f-143">Property</span><span class="sxs-lookup"><span data-stu-id="cf72f-143">Property</span></span>                | <span data-ttu-id="cf72f-144">Description</span><span class="sxs-lookup"><span data-stu-id="cf72f-144">Description</span></span>                              | <span data-ttu-id="cf72f-145">Required</span><span class="sxs-lookup"><span data-stu-id="cf72f-145">Required</span></span> |
| :---------------------- | :--------------------------------------- | :------- |
| <span data-ttu-id="cf72f-146">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="cf72f-146">**servicePrincipalId**</span></span>  | <span data-ttu-id="cf72f-147">Specify the application's client ID.</span><span class="sxs-lookup"><span data-stu-id="cf72f-147">Specify the application's client ID.</span></span>     | <span data-ttu-id="cf72f-148">Yes</span><span class="sxs-lookup"><span data-stu-id="cf72f-148">Yes</span></span>      |
| <span data-ttu-id="cf72f-149">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="cf72f-149">**servicePrincipalKey**</span></span> | <span data-ttu-id="cf72f-150">Specify the application's key.</span><span class="sxs-lookup"><span data-stu-id="cf72f-150">Specify the application's key.</span></span>           | <span data-ttu-id="cf72f-151">Yes</span><span class="sxs-lookup"><span data-stu-id="cf72f-151">Yes</span></span>      |
| <span data-ttu-id="cf72f-152">**tenant**</span><span class="sxs-lookup"><span data-stu-id="cf72f-152">**tenant**</span></span>              | <span data-ttu-id="cf72f-153">Specify the tenant information (domain name or tenant ID) under which your application resides.</span><span class="sxs-lookup"><span data-stu-id="cf72f-153">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="cf72f-154">You can retrieve it by hovering the mouse in the upper-right corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cf72f-154">You can retrieve it by hovering the mouse in the upper-right corner of the Azure portal.</span></span> | <span data-ttu-id="cf72f-155">Yes</span><span class="sxs-lookup"><span data-stu-id="cf72f-155">Yes</span></span>      |

<span data-ttu-id="cf72f-156">**Example: Service principal authentication**</span><span class="sxs-lookup"><span data-stu-id="cf72f-156">**Example: Service principal authentication**</span></span>
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "<account name>",
            "dataLakeAnalyticsUri": "<azure data lake analytics URI>",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": {
                "value": "<service principal key>",
                "type": "SecureString"
            },
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }       
    }
}
```

<span data-ttu-id="cf72f-157">To learn more about the linked service, see [Compute linked services](compute-linked-services.md).</span><span class="sxs-lookup"><span data-stu-id="cf72f-157">To learn more about the linked service, see [Compute linked services](compute-linked-services.md).</span></span>

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="cf72f-158">Data Lake Analytics U-SQL Activity</span><span class="sxs-lookup"><span data-stu-id="cf72f-158">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="cf72f-159">The following JSON snippet defines a pipeline with a Data Lake Analytics U-SQL Activity.</span><span class="sxs-lookup"><span data-stu-id="cf72f-159">The following JSON snippet defines a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="cf72f-160">The activity definition has a reference to the Azure Data Lake Analytics linked service you created earlier.</span><span class="sxs-lookup"><span data-stu-id="cf72f-160">The activity definition has a reference to the Azure Data Lake Analytics linked service you created earlier.</span></span> <span data-ttu-id="cf72f-161">To execute a Data Lake Analytics U-SQL script, Data Factory submits the script you specified to the Data Lake Analytics, and the required inputs and outputs is defined in the script for Data Lake Analytics to fetch and output.</span><span class="sxs-lookup"><span data-stu-id="cf72f-161">To execute a Data Lake Analytics U-SQL script, Data Factory submits the script you specified to the Data Lake Analytics, and the required inputs and outputs is defined in the script for Data Lake Analytics to fetch and output.</span></span> 

```json
{
    "name": "ADLA U-SQL Activity",
    "description": "description",
    "type": "DataLakeAnalyticsU-SQL",
    "linkedServiceName": {
        "referenceName": "<linked service name of Azure Data Lake Analytics>",
        "type": "LinkedServiceReference"
    },
    "typeProperties": {
        "scriptLinkedService": {
            "referenceName": "<linked service name of Azure Data Lake Store or Azure Storage which contains the U-SQL script>",
            "type": "LinkedServiceReference"
        },
        "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
        "degreeOfParallelism": 3,
        "priority": 100,
        "parameters": {
            "in": "/datalake/input/SearchLog.tsv",
            "out": "/datalake/output/Result.tsv"
        }
    }   
}
```

<span data-ttu-id="cf72f-162">The following table describes names and descriptions of properties that are specific to this activity.</span><span class="sxs-lookup"><span data-stu-id="cf72f-162">The following table describes names and descriptions of properties that are specific to this activity.</span></span> 

| <span data-ttu-id="cf72f-163">Property</span><span class="sxs-lookup"><span data-stu-id="cf72f-163">Property</span></span>            | <span data-ttu-id="cf72f-164">Description</span><span class="sxs-lookup"><span data-stu-id="cf72f-164">Description</span></span>                              | <span data-ttu-id="cf72f-165">Required</span><span class="sxs-lookup"><span data-stu-id="cf72f-165">Required</span></span> |
| :------------------ | :--------------------------------------- | :------- |
| <span data-ttu-id="cf72f-166">name</span><span class="sxs-lookup"><span data-stu-id="cf72f-166">name</span></span>                | <span data-ttu-id="cf72f-167">Name of the activity in the pipeline</span><span class="sxs-lookup"><span data-stu-id="cf72f-167">Name of the activity in the pipeline</span></span>     | <span data-ttu-id="cf72f-168">Yes</span><span class="sxs-lookup"><span data-stu-id="cf72f-168">Yes</span></span>      |
| <span data-ttu-id="cf72f-169">description</span><span class="sxs-lookup"><span data-stu-id="cf72f-169">description</span></span>         | <span data-ttu-id="cf72f-170">Text describing what the activity does.</span><span class="sxs-lookup"><span data-stu-id="cf72f-170">Text describing what the activity does.</span></span>  | <span data-ttu-id="cf72f-171">No</span><span class="sxs-lookup"><span data-stu-id="cf72f-171">No</span></span>       |
| <span data-ttu-id="cf72f-172">type</span><span class="sxs-lookup"><span data-stu-id="cf72f-172">type</span></span>                | <span data-ttu-id="cf72f-173">For Data Lake Analytics U-SQL activity, the activity type is  **DataLakeAnalyticsU-SQL**.</span><span class="sxs-lookup"><span data-stu-id="cf72f-173">For Data Lake Analytics U-SQL activity, the activity type is  **DataLakeAnalyticsU-SQL**.</span></span> | <span data-ttu-id="cf72f-174">Yes</span><span class="sxs-lookup"><span data-stu-id="cf72f-174">Yes</span></span>      |
| <span data-ttu-id="cf72f-175">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="cf72f-175">linkedServiceName</span></span>   | <span data-ttu-id="cf72f-176">Linked Service to Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="cf72f-176">Linked Service to Azure Data Lake Analytics.</span></span> <span data-ttu-id="cf72f-177">To learn about this linked service, see [Compute linked services](compute-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="cf72f-177">To learn about this linked service, see [Compute linked services](compute-linked-services.md) article.</span></span>  |<span data-ttu-id="cf72f-178">Yes</span><span class="sxs-lookup"><span data-stu-id="cf72f-178">Yes</span></span>       |
| <span data-ttu-id="cf72f-179">scriptPath</span><span class="sxs-lookup"><span data-stu-id="cf72f-179">scriptPath</span></span>          | <span data-ttu-id="cf72f-180">Path to folder that contains the U-SQL script.</span><span class="sxs-lookup"><span data-stu-id="cf72f-180">Path to folder that contains the U-SQL script.</span></span> <span data-ttu-id="cf72f-181">Name of the file is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="cf72f-181">Name of the file is case-sensitive.</span></span> | <span data-ttu-id="cf72f-182">Yes</span><span class="sxs-lookup"><span data-stu-id="cf72f-182">Yes</span></span>      |
| <span data-ttu-id="cf72f-183">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="cf72f-183">scriptLinkedService</span></span> | <span data-ttu-id="cf72f-184">Linked service that links the **Azure Data Lake Store** or **Azure Storage** that contains the script to the data factory</span><span class="sxs-lookup"><span data-stu-id="cf72f-184">Linked service that links the **Azure Data Lake Store** or **Azure Storage** that contains the script to the data factory</span></span> | <span data-ttu-id="cf72f-185">Yes</span><span class="sxs-lookup"><span data-stu-id="cf72f-185">Yes</span></span>      |
| <span data-ttu-id="cf72f-186">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="cf72f-186">degreeOfParallelism</span></span> | <span data-ttu-id="cf72f-187">The maximum number of nodes simultaneously used to run the job.</span><span class="sxs-lookup"><span data-stu-id="cf72f-187">The maximum number of nodes simultaneously used to run the job.</span></span> | <span data-ttu-id="cf72f-188">No</span><span class="sxs-lookup"><span data-stu-id="cf72f-188">No</span></span>       |
| <span data-ttu-id="cf72f-189">priority</span><span class="sxs-lookup"><span data-stu-id="cf72f-189">priority</span></span>            | <span data-ttu-id="cf72f-190">Determines which jobs out of all that are queued should be selected to run first.</span><span class="sxs-lookup"><span data-stu-id="cf72f-190">Determines which jobs out of all that are queued should be selected to run first.</span></span> <span data-ttu-id="cf72f-191">The lower the number, the higher the priority.</span><span class="sxs-lookup"><span data-stu-id="cf72f-191">The lower the number, the higher the priority.</span></span> | <span data-ttu-id="cf72f-192">No</span><span class="sxs-lookup"><span data-stu-id="cf72f-192">No</span></span>       |
| <span data-ttu-id="cf72f-193">parameters</span><span class="sxs-lookup"><span data-stu-id="cf72f-193">parameters</span></span>          | <span data-ttu-id="cf72f-194">Parameters to pass into the U-SQL script.</span><span class="sxs-lookup"><span data-stu-id="cf72f-194">Parameters to pass into the U-SQL script.</span></span>    | <span data-ttu-id="cf72f-195">No</span><span class="sxs-lookup"><span data-stu-id="cf72f-195">No</span></span>       |
| <span data-ttu-id="cf72f-196">runtimeVersion</span><span class="sxs-lookup"><span data-stu-id="cf72f-196">runtimeVersion</span></span>      | <span data-ttu-id="cf72f-197">Runtime version of the U-SQL engine to use.</span><span class="sxs-lookup"><span data-stu-id="cf72f-197">Runtime version of the U-SQL engine to use.</span></span> | <span data-ttu-id="cf72f-198">No</span><span class="sxs-lookup"><span data-stu-id="cf72f-198">No</span></span>       |
| <span data-ttu-id="cf72f-199">compilationMode</span><span class="sxs-lookup"><span data-stu-id="cf72f-199">compilationMode</span></span>     | <p><span data-ttu-id="cf72f-200">Compilation mode of U-SQL.</span><span class="sxs-lookup"><span data-stu-id="cf72f-200">Compilation mode of U-SQL.</span></span> <span data-ttu-id="cf72f-201">Must be one of these values: **Semantic:** Only perform semantic checks and necessary sanity checks, **Full:** Perform the full compilation, including syntax check, optimization, code generation, etc., **SingleBox:** Perform the full compilation, with TargetType setting to SingleBox.</span><span class="sxs-lookup"><span data-stu-id="cf72f-201">Must be one of these values: **Semantic:** Only perform semantic checks and necessary sanity checks, **Full:** Perform the full compilation, including syntax check, optimization, code generation, etc., **SingleBox:** Perform the full compilation, with TargetType setting to SingleBox.</span></span> <span data-ttu-id="cf72f-202">If you don't specify a value for this property, the server determines the optimal compilation mode.</span><span class="sxs-lookup"><span data-stu-id="cf72f-202">If you don't specify a value for this property, the server determines the optimal compilation mode.</span></span> | <span data-ttu-id="cf72f-203">No</span><span class="sxs-lookup"><span data-stu-id="cf72f-203">No</span></span> |

<span data-ttu-id="cf72f-204">Data Factory submits the See [SearchLogProcessing.txt Script Definition](#sample-u-sql-script) for the script definition.</span><span class="sxs-lookup"><span data-stu-id="cf72f-204">Data Factory submits the See [SearchLogProcessing.txt Script Definition](#sample-u-sql-script) for the script definition.</span></span> 

## <a name="sample-u-sql-script"></a><span data-ttu-id="cf72f-205">Sample U-SQL script</span><span class="sxs-lookup"><span data-stu-id="cf72f-205">Sample U-SQL script</span></span>

```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int,
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

<span data-ttu-id="cf72f-206">In above script example, the input and output to the script is defined in **@in** and **@out** parameters.</span><span class="sxs-lookup"><span data-stu-id="cf72f-206">In above script example, the input and output to the script is defined in **@in** and **@out** parameters.</span></span> <span data-ttu-id="cf72f-207">The values for **@in** and **@out** parameters in the U-SQL script are passed dynamically by Data Factory using the ‘parameters’ section.</span><span class="sxs-lookup"><span data-stu-id="cf72f-207">The values for **@in** and **@out** parameters in the U-SQL script are passed dynamically by Data Factory using the ‘parameters’ section.</span></span> 

<span data-ttu-id="cf72f-208">You can specify other properties such as degreeOfParallelism and priority as well in your pipeline definition for the jobs that run on the Azure Data Lake Analytics service.</span><span class="sxs-lookup"><span data-stu-id="cf72f-208">You can specify other properties such as degreeOfParallelism and priority as well in your pipeline definition for the jobs that run on the Azure Data Lake Analytics service.</span></span>

## <a name="dynamic-parameters"></a><span data-ttu-id="cf72f-209">Dynamic parameters</span><span class="sxs-lookup"><span data-stu-id="cf72f-209">Dynamic parameters</span></span>
<span data-ttu-id="cf72f-210">In the sample pipeline definition, in and out parameters are assigned with hard-coded values.</span><span class="sxs-lookup"><span data-stu-id="cf72f-210">In the sample pipeline definition, in and out parameters are assigned with hard-coded values.</span></span> 

```json
"parameters": {
    "in": "/datalake/input/SearchLog.tsv",
    "out": "/datalake/output/Result.tsv"
}
```

<span data-ttu-id="cf72f-211">It is possible to use dynamic parameters instead.</span><span class="sxs-lookup"><span data-stu-id="cf72f-211">It is possible to use dynamic parameters instead.</span></span> <span data-ttu-id="cf72f-212">For example:</span><span class="sxs-lookup"><span data-stu-id="cf72f-212">For example:</span></span> 

```json
"parameters": {
    "in": "/datalake/input/@{formatDateTime(pipeline().parameters.WindowStart,'yyyy/MM/dd')}/data.tsv",
    "out": "/datalake/output/@{formatDateTime(pipeline().parameters.WindowStart,'yyyy/MM/dd')}/result.tsv"
}
```

<span data-ttu-id="cf72f-213">In this case, input files are still picked up from the /datalake/input folder and output files are generated in the /datalake/output folder.</span><span class="sxs-lookup"><span data-stu-id="cf72f-213">In this case, input files are still picked up from the /datalake/input folder and output files are generated in the /datalake/output folder.</span></span> <span data-ttu-id="cf72f-214">The file names are dynamic based on the window start time being passed in when pipeline gets triggered.</span><span class="sxs-lookup"><span data-stu-id="cf72f-214">The file names are dynamic based on the window start time being passed in when pipeline gets triggered.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="cf72f-215">Next steps</span><span class="sxs-lookup"><span data-stu-id="cf72f-215">Next steps</span></span>
<span data-ttu-id="cf72f-216">See the following articles that explain how to transform data in other ways:</span><span class="sxs-lookup"><span data-stu-id="cf72f-216">See the following articles that explain how to transform data in other ways:</span></span> 

* [<span data-ttu-id="cf72f-217">Hive activity</span><span class="sxs-lookup"><span data-stu-id="cf72f-217">Hive activity</span></span>](transform-data-using-hadoop-hive.md)
* [<span data-ttu-id="cf72f-218">Pig activity</span><span class="sxs-lookup"><span data-stu-id="cf72f-218">Pig activity</span></span>](transform-data-using-hadoop-pig.md)
* [<span data-ttu-id="cf72f-219">MapReduce activity</span><span class="sxs-lookup"><span data-stu-id="cf72f-219">MapReduce activity</span></span>](transform-data-using-hadoop-map-reduce.md)
* [<span data-ttu-id="cf72f-220">Hadoop Streaming activity</span><span class="sxs-lookup"><span data-stu-id="cf72f-220">Hadoop Streaming activity</span></span>](transform-data-using-hadoop-streaming.md)
* [<span data-ttu-id="cf72f-221">Spark activity</span><span class="sxs-lookup"><span data-stu-id="cf72f-221">Spark activity</span></span>](transform-data-using-spark.md)
* [<span data-ttu-id="cf72f-222">.NET custom activity</span><span class="sxs-lookup"><span data-stu-id="cf72f-222">.NET custom activity</span></span>](transform-data-using-dotnet-custom-activity.md)
* [<span data-ttu-id="cf72f-223">Machine Learning Batch Execution activity</span><span class="sxs-lookup"><span data-stu-id="cf72f-223">Machine Learning Batch Execution activity</span></span>](transform-data-using-machine-learning.md)
* [<span data-ttu-id="cf72f-224">Stored procedure activity</span><span class="sxs-lookup"><span data-stu-id="cf72f-224">Stored procedure activity</span></span>](transform-data-using-stored-procedure.md)
