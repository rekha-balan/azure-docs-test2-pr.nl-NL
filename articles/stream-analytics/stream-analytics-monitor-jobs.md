---
title: programmatically Monitor jobs on Stream Analytics | Microsoft Docs
description: Learn how to programmatically monitor Stream Analytics jobs created via REST APIs, Azure SDK, or Powershell.
keywords: .net monitor, job monitor, monitoring app
services: stream-analytics
documentationcenter: ''
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 2ec02cc9-4ca5-4a25-ae60-c44be9ad4835
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/04/2017
ms.author: jeffstok
ms.openlocfilehash: dc19bec960edff15feffc41bee1bbc63eeff5c6d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551285"
---
# <a name="programmatically-create-a-stream-analytics-job-monitor"></a><span data-ttu-id="99b01-104">Programmatically create a Stream Analytics job monitor</span><span class="sxs-lookup"><span data-stu-id="99b01-104">Programmatically create a Stream Analytics job monitor</span></span>
 <span data-ttu-id="99b01-105">This article demonstrates how to enable monitoring for a Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="99b01-105">This article demonstrates how to enable monitoring for a Stream Analytics job.</span></span> <span data-ttu-id="99b01-106">Stream Analytics jobs created via REST APIs, Azure SDK, or Powershell do not have monitoring enabled by default.</span><span class="sxs-lookup"><span data-stu-id="99b01-106">Stream Analytics jobs created via REST APIs, Azure SDK, or Powershell do not have monitoring enabled by default.</span></span>  <span data-ttu-id="99b01-107">You can manually enable this in the Azure portal by navigating to the job’s Monitor page and clicking the Enable button or you can automate this process by following the steps in this article.</span><span class="sxs-lookup"><span data-stu-id="99b01-107">You can manually enable this in the Azure portal by navigating to the job’s Monitor page and clicking the Enable button or you can automate this process by following the steps in this article.</span></span> <span data-ttu-id="99b01-108">The monitoring data will show up in the Metrics area of the Azure portal for your Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="99b01-108">The monitoring data will show up in the Metrics area of the Azure portal for your Stream Analytics job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99b01-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="99b01-109">Prerequisites</span></span>
<span data-ttu-id="99b01-110">Before you begin this article, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="99b01-110">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="99b01-111">Visual Studio 2017 or 2015.</span><span class="sxs-lookup"><span data-stu-id="99b01-111">Visual Studio 2017 or 2015.</span></span>
* <span data-ttu-id="99b01-112">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="99b01-112">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="99b01-113">An existing Stream Analytics job that needs monitoring enabled.</span><span class="sxs-lookup"><span data-stu-id="99b01-113">An existing Stream Analytics job that needs monitoring enabled.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="99b01-114">Create a project</span><span class="sxs-lookup"><span data-stu-id="99b01-114">Create a project</span></span>
1. <span data-ttu-id="99b01-115">Create a Visual Studio C# .Net console application.</span><span class="sxs-lookup"><span data-stu-id="99b01-115">Create a Visual Studio C# .Net console application.</span></span>
2. <span data-ttu-id="99b01-116">In the Package Manager Console, run the following commands to install the NuGet packages.</span><span class="sxs-lookup"><span data-stu-id="99b01-116">In the Package Manager Console, run the following commands to install the NuGet packages.</span></span> <span data-ttu-id="99b01-117">The first one is the Azure Stream Analytics Management .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="99b01-117">The first one is the Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="99b01-118">The second one is the Azure Monitor SDK which will be used to enable monitoring.</span><span class="sxs-lookup"><span data-stu-id="99b01-118">The second one is the Azure Monitor SDK which will be used to enable monitoring.</span></span> <span data-ttu-id="99b01-119">The last one is the Azure Active Directory client that will be used for authentication.</span><span class="sxs-lookup"><span data-stu-id="99b01-119">The last one is the Azure Active Directory client that will be used for authentication.</span></span>
   
   ```
   Install-Package Microsoft.Azure.Management.StreamAnalytics
   Install-Package Microsoft.Azure.Insights -Pre
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```
3. <span data-ttu-id="99b01-120">Add the following appSettings section to the App.config file.</span><span class="sxs-lookup"><span data-stu-id="99b01-120">Add the following appSettings section to the App.config file.</span></span>
   
   ```
   <appSettings>
     <!--CSM Prod related values-->
     <add key="ResourceGroupName" value="RESOURCE GROUP NAME" />
     <add key="JobName" value="YOUR JOB NAME" />
     <add key="StorageAccountName" value="YOUR STORAGE ACCOUNT"/>
     <add key="ActiveDirectoryEndpoint" value="https://login.windows.net/" />
     <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
     <add key="WindowsManagementUri" value="https://management.core.windows.net/" />
     <add key="AsaClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
     <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
     <add key="SubscriptionId" value="YOUR AZURE SUBSCRIPTION ID" />
     <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
   </appSettings>
   ```
   <span data-ttu-id="99b01-121">Replace values for *SubscriptionId* and *ActiveDirectoryTenantId* with your Azure subscription and tenant IDs.</span><span class="sxs-lookup"><span data-stu-id="99b01-121">Replace values for *SubscriptionId* and *ActiveDirectoryTenantId* with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="99b01-122">You can get these values by running the following PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="99b01-122">You can get these values by running the following PowerShell cmdlet:</span></span>
   
   ```
   Get-AzureAccount
   ```
4. <span data-ttu-id="99b01-123">Add the following using statements to the source file (Program.cs) in the project.</span><span class="sxs-lookup"><span data-stu-id="99b01-123">Add the following using statements to the source file (Program.cs) in the project.</span></span>
   
   ```
     using System;
     using System.Configuration;
     using System.Threading;
     using Microsoft.Azure;
     using Microsoft.Azure.Management.Insights;
     using Microsoft.Azure.Management.Insights.Models;
     using Microsoft.Azure.Management.StreamAnalytics;
     using Microsoft.Azure.Management.StreamAnalytics.Models;
     using Microsoft.IdentityModel.Clients.ActiveDirectory;
   ```
5. <span data-ttu-id="99b01-124">Add an authentication helper method.</span><span class="sxs-lookup"><span data-stu-id="99b01-124">Add an authentication helper method.</span></span>
   
     <span data-ttu-id="99b01-125">public static string GetAuthorizationHeader()</span><span class="sxs-lookup"><span data-stu-id="99b01-125">public static string GetAuthorizationHeader()</span></span>
   
         {
             AuthenticationResult result = null;
             var thread = new Thread(() =>
             {
                 try
                 {
                     var context = new AuthenticationContext(
                         ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] +
                         ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
   
                     result = context.AcquireToken(
                         resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
                         clientId: ConfigurationManager.AppSettings["AsaClientId"],
                         redirectUri: new Uri(ConfigurationManager.AppSettings["RedirectUri"]),
                         promptBehavior: PromptBehavior.Always);
                 }
                 catch (Exception threadEx)
                 {
                     Console.WriteLine(threadEx.Message);
                 }
             });
   
             thread.SetApartmentState(ApartmentState.STA);
             thread.Name = "AcquireTokenThread";
             thread.Start();
             thread.Join();
   
             if (result != null)
             {
                 return result.AccessToken;
             }
   
             throw new InvalidOperationException("Failed to acquire token");
     <span data-ttu-id="99b01-126">}</span><span class="sxs-lookup"><span data-stu-id="99b01-126">}</span></span>

## <a name="create-management-clients"></a><span data-ttu-id="99b01-127">Create Management Clients</span><span class="sxs-lookup"><span data-stu-id="99b01-127">Create Management Clients</span></span>
<span data-ttu-id="99b01-128">The following code will set up the necessary variables and management clients.</span><span class="sxs-lookup"><span data-stu-id="99b01-128">The following code will set up the necessary variables and management clients.</span></span>

    string resourceGroupName = "<YOUR AZURE RESOURCE GROUP NAME>";
    string streamAnalyticsJobName = "<YOUR STREAM ANALYTICS JOB NAME>";

    // Get authentication token
    TokenCloudCredentials aadTokenCredentials =
        new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader());

    Uri resourceManagerUri = new
    Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    // Create Stream Analytics and Insights management client
    StreamAnalyticsManagementClient streamAnalyticsClient = new
    StreamAnalyticsManagementClient(aadTokenCredentials, resourceManagerUri);
    InsightsManagementClient insightsClient = new
    InsightsManagementClient(aadTokenCredentials, resourceManagerUri);

## <a name="enable-monitoring-for-an-existing-stream-analytics-job"></a><span data-ttu-id="99b01-129">Enable Monitoring For an Existing Stream Analytics Job</span><span class="sxs-lookup"><span data-stu-id="99b01-129">Enable Monitoring For an Existing Stream Analytics Job</span></span>
<span data-ttu-id="99b01-130">The following code will enable monitoring for an **existing** Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="99b01-130">The following code will enable monitoring for an **existing** Stream Analytics job.</span></span> <span data-ttu-id="99b01-131">The first part of the code performs a GET request against the Stream Analytics service to retrieve information about the particular Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="99b01-131">The first part of the code performs a GET request against the Stream Analytics service to retrieve information about the particular Stream Analytics job.</span></span> <span data-ttu-id="99b01-132">It uses the “Id” property (retrieved from the GET request) as a parameter for the Put method in the second half of the code which sends a PUT request to the Insights service to enable monitoring for the Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="99b01-132">It uses the “Id” property (retrieved from the GET request) as a parameter for the Put method in the second half of the code which sends a PUT request to the Insights service to enable monitoring for the Stream Analytics job.</span></span>

> [!WARNING]
> <span data-ttu-id="99b01-133">If you have previously enabled monitoring for a different Stream Analytics job, either through the Azure portal or programmatically via the below code, **it is recommended that you provide the same storage account name that you did when you previously enabled monitoring.**</span><span class="sxs-lookup"><span data-stu-id="99b01-133">If you have previously enabled monitoring for a different Stream Analytics job, either through the Azure portal or programmatically via the below code, **it is recommended that you provide the same storage account name that you did when you previously enabled monitoring.**</span></span>
> 
> <span data-ttu-id="99b01-134">The storage account is linked to the region you created your Stream Analytics job in, not specifically to the job itself.</span><span class="sxs-lookup"><span data-stu-id="99b01-134">The storage account is linked to the region you created your Stream Analytics job in, not specifically to the job itself.</span></span>
> 
> <span data-ttu-id="99b01-135">All Stream Analytics job (and all other Azure resources) in that same region share this storage account to store monitoring data.</span><span class="sxs-lookup"><span data-stu-id="99b01-135">All Stream Analytics job (and all other Azure resources) in that same region share this storage account to store monitoring data.</span></span> <span data-ttu-id="99b01-136">If you provide a different storage account, it may cause unintended side effects to the monitoring of your other Stream Analytics jobs and/or other Azure resources.</span><span class="sxs-lookup"><span data-stu-id="99b01-136">If you provide a different storage account, it may cause unintended side effects to the monitoring of your other Stream Analytics jobs and/or other Azure resources.</span></span>
> 
> <span data-ttu-id="99b01-137">The storage account name used to replace ```“<YOUR STORAGE ACCOUNT NAME>”``` below should be a storage account that is in the same subscription as the Stream Analytics job you are enabling monitoring for.</span><span class="sxs-lookup"><span data-stu-id="99b01-137">The storage account name used to replace ```“<YOUR STORAGE ACCOUNT NAME>”``` below should be a storage account that is in the same subscription as the Stream Analytics job you are enabling monitoring for.</span></span>
> 
> 

    // Get an existing Stream Analytics job
    JobGetParameters jobGetParameters = new JobGetParameters()
    {
        PropertiesToExpand = "inputs,transformation,outputs"
    };
    JobGetResponse jobGetResponse = streamAnalyticsClient.StreamingJobs.Get(resourceGroupName, streamAnalyticsJobName, jobGetParameters);

    // Enable monitoring
    ServiceDiagnosticSettingsPutParameters insightPutParameters = new ServiceDiagnosticSettingsPutParameters()
    {
            Properties = new ServiceDiagnosticSettings()
            {
                StorageAccountName = "<YOUR STORAGE ACCOUNT NAME>"
            }
    };
    insightsClient.ServiceDiagnosticSettingsOperations.Put(jobGetResponse.Job.Id, insightPutParameters);



## <a name="get-support"></a><span data-ttu-id="99b01-138">Get support</span><span class="sxs-lookup"><span data-stu-id="99b01-138">Get support</span></span>
<span data-ttu-id="99b01-139">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="99b01-139">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="99b01-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="99b01-140">Next steps</span></span>
* [<span data-ttu-id="99b01-141">Introduction to Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="99b01-141">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="99b01-142">Get started using Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="99b01-142">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="99b01-143">Scale Azure Stream Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="99b01-143">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="99b01-144">Azure Stream Analytics Query Language Reference</span><span class="sxs-lookup"><span data-stu-id="99b01-144">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="99b01-145">Azure Stream Analytics Management REST API Reference</span><span class="sxs-lookup"><span data-stu-id="99b01-145">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

