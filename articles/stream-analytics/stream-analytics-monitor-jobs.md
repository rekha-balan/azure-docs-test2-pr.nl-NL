---
title: Monitor and manage Azure Stream Analytics jobs programmatically
description: This article describes how to programmatically monitor Stream Analytics jobs created via REST APIs, Azure SDK, or PowerShell.
services: stream-analytics
author: jseb225
ms.author: jeanb
manager: kfile
ms.reviewer: jasonh
ms.service: stream-analytics
ms.topic: conceptual
ms.date: 04/20/2017
ms.openlocfilehash: 2688f148185b1c1523178d190a7a2a76e6ceabef
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44809197"
---
# <a name="programmatically-create-a-stream-analytics-job-monitor"></a><span data-ttu-id="f1294-103">Programmatically create a Stream Analytics job monitor</span><span class="sxs-lookup"><span data-stu-id="f1294-103">Programmatically create a Stream Analytics job monitor</span></span>

<span data-ttu-id="f1294-104">This article demonstrates how to enable monitoring for a Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="f1294-104">This article demonstrates how to enable monitoring for a Stream Analytics job.</span></span> <span data-ttu-id="f1294-105">Stream Analytics jobs that are created via REST APIs, Azure SDK, or PowerShell do not have monitoring enabled by default.</span><span class="sxs-lookup"><span data-stu-id="f1294-105">Stream Analytics jobs that are created via REST APIs, Azure SDK, or PowerShell do not have monitoring enabled by default.</span></span> <span data-ttu-id="f1294-106">You can manually enable it in the Azure portal by going to the job’s Monitor page and clicking the Enable button or you can automate this process by following the steps in this article.</span><span class="sxs-lookup"><span data-stu-id="f1294-106">You can manually enable it in the Azure portal by going to the job’s Monitor page and clicking the Enable button or you can automate this process by following the steps in this article.</span></span> <span data-ttu-id="f1294-107">The monitoring data will show up in the Metrics area of the Azure portal for your Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="f1294-107">The monitoring data will show up in the Metrics area of the Azure portal for your Stream Analytics job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1294-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f1294-108">Prerequisites</span></span>

<span data-ttu-id="f1294-109">Before you begin this process, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="f1294-109">Before you begin this process, you must have the following:</span></span>

* <span data-ttu-id="f1294-110">Visual Studio 2017 or 2015</span><span class="sxs-lookup"><span data-stu-id="f1294-110">Visual Studio 2017 or 2015</span></span>
* <span data-ttu-id="f1294-111">[Azure .NET SDK](https://azure.microsoft.com/downloads/) downloaded and installed</span><span class="sxs-lookup"><span data-stu-id="f1294-111">[Azure .NET SDK](https://azure.microsoft.com/downloads/) downloaded and installed</span></span>
* <span data-ttu-id="f1294-112">An existing Stream Analytics job that needs to have monitoring enabled</span><span class="sxs-lookup"><span data-stu-id="f1294-112">An existing Stream Analytics job that needs to have monitoring enabled</span></span>

## <a name="create-a-project"></a><span data-ttu-id="f1294-113">Create a project</span><span class="sxs-lookup"><span data-stu-id="f1294-113">Create a project</span></span>

1. <span data-ttu-id="f1294-114">Create a Visual Studio C# .NET console application.</span><span class="sxs-lookup"><span data-stu-id="f1294-114">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="f1294-115">In the Package Manager Console, run the following commands to install the NuGet packages.</span><span class="sxs-lookup"><span data-stu-id="f1294-115">In the Package Manager Console, run the following commands to install the NuGet packages.</span></span> <span data-ttu-id="f1294-116">The first one is the Azure Stream Analytics Management .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="f1294-116">The first one is the Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="f1294-117">The second one is the Azure Monitor SDK that will be used to enable monitoring.</span><span class="sxs-lookup"><span data-stu-id="f1294-117">The second one is the Azure Monitor SDK that will be used to enable monitoring.</span></span> <span data-ttu-id="f1294-118">The last one is the Azure Active Directory client that will be used for authentication.</span><span class="sxs-lookup"><span data-stu-id="f1294-118">The last one is the Azure Active Directory client that will be used for authentication.</span></span>
   
   ```
   Install-Package Microsoft.Azure.Management.StreamAnalytics
   Install-Package Microsoft.Azure.Insights -Pre
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```
3. <span data-ttu-id="f1294-119">Add the following appSettings section to the App.config file.</span><span class="sxs-lookup"><span data-stu-id="f1294-119">Add the following appSettings section to the App.config file.</span></span>
   
   ```
   <appSettings>
     <!--CSM Prod related values-->
     <add key="ResourceGroupName" value="RESOURCE GROUP NAME" />
     <add key="JobName" value="YOUR JOB NAME" />
     <add key="StorageAccountName" value="YOUR STORAGE ACCOUNT"/>
     <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
     <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
     <add key="WindowsManagementUri" value="https://management.core.windows.net/" />
     <add key="AsaClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
     <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
     <add key="SubscriptionId" value="YOUR AZURE SUBSCRIPTION ID" />
     <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
   </appSettings>
   ```
   <span data-ttu-id="f1294-120">Replace values for *SubscriptionId* and *ActiveDirectoryTenantId* with your Azure subscription and tenant IDs.</span><span class="sxs-lookup"><span data-stu-id="f1294-120">Replace values for *SubscriptionId* and *ActiveDirectoryTenantId* with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="f1294-121">You can get these values by running the following PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="f1294-121">You can get these values by running the following PowerShell cmdlet:</span></span>
   
   ```
   Get-AzureAccount
   ```
4. <span data-ttu-id="f1294-122">Add the following using statements to the source file (Program.cs) in the project.</span><span class="sxs-lookup"><span data-stu-id="f1294-122">Add the following using statements to the source file (Program.cs) in the project.</span></span>
   
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
5. <span data-ttu-id="f1294-123">Add an authentication helper method.</span><span class="sxs-lookup"><span data-stu-id="f1294-123">Add an authentication helper method.</span></span>
   
     <span data-ttu-id="f1294-124">public static string GetAuthorizationHeader()</span><span class="sxs-lookup"><span data-stu-id="f1294-124">public static string GetAuthorizationHeader()</span></span>
   
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
     <span data-ttu-id="f1294-125">}</span><span class="sxs-lookup"><span data-stu-id="f1294-125">}</span></span>

## <a name="create-management-clients"></a><span data-ttu-id="f1294-126">Create management clients</span><span class="sxs-lookup"><span data-stu-id="f1294-126">Create management clients</span></span>

<span data-ttu-id="f1294-127">The following code will set up the necessary variables and management clients.</span><span class="sxs-lookup"><span data-stu-id="f1294-127">The following code will set up the necessary variables and management clients.</span></span>

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

## <a name="enable-monitoring-for-an-existing-stream-analytics-job"></a><span data-ttu-id="f1294-128">Enable monitoring for an existing Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="f1294-128">Enable monitoring for an existing Stream Analytics job</span></span>

<span data-ttu-id="f1294-129">The following code enables monitoring for an **existing** Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="f1294-129">The following code enables monitoring for an **existing** Stream Analytics job.</span></span> <span data-ttu-id="f1294-130">The first part of the code performs a GET request against the Stream Analytics service to retrieve information about the particular Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="f1294-130">The first part of the code performs a GET request against the Stream Analytics service to retrieve information about the particular Stream Analytics job.</span></span> <span data-ttu-id="f1294-131">It uses the *Id* property (retrieved from the GET request) as a parameter for the Put method in the second half of the code, which sends a PUT request to the Insights service to enable monitoring for the Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="f1294-131">It uses the *Id* property (retrieved from the GET request) as a parameter for the Put method in the second half of the code, which sends a PUT request to the Insights service to enable monitoring for the Stream Analytics job.</span></span>

>[!WARNING]
><span data-ttu-id="f1294-132">If you have previously enabled monitoring for a different Stream Analytics job, either through the Azure portal or programmatically via the below code, **we recommend that you provide the same storage account name that you used when you previously enabled monitoring.**</span><span class="sxs-lookup"><span data-stu-id="f1294-132">If you have previously enabled monitoring for a different Stream Analytics job, either through the Azure portal or programmatically via the below code, **we recommend that you provide the same storage account name that you used when you previously enabled monitoring.**</span></span>
> 
> <span data-ttu-id="f1294-133">The storage account is linked to the region that you created your Stream Analytics job in, not specifically to the job itself.</span><span class="sxs-lookup"><span data-stu-id="f1294-133">The storage account is linked to the region that you created your Stream Analytics job in, not specifically to the job itself.</span></span>
> 
> <span data-ttu-id="f1294-134">All Stream Analytics jobs (and all other Azure resources) in that same region share this storage account to store monitoring data.</span><span class="sxs-lookup"><span data-stu-id="f1294-134">All Stream Analytics jobs (and all other Azure resources) in that same region share this storage account to store monitoring data.</span></span> <span data-ttu-id="f1294-135">If you provide a different storage account, it might cause unintended side effects in the monitoring of your other Stream Analytics jobs or other Azure resources.</span><span class="sxs-lookup"><span data-stu-id="f1294-135">If you provide a different storage account, it might cause unintended side effects in the monitoring of your other Stream Analytics jobs or other Azure resources.</span></span>
> 
> <span data-ttu-id="f1294-136">The storage account name that you use to replace `<YOUR STORAGE ACCOUNT NAME>` in the following code should be a storage account that is in the same subscription as the Stream Analytics job that you are enabling monitoring for.</span><span class="sxs-lookup"><span data-stu-id="f1294-136">The storage account name that you use to replace `<YOUR STORAGE ACCOUNT NAME>` in the following code should be a storage account that is in the same subscription as the Stream Analytics job that you are enabling monitoring for.</span></span>
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



## <a name="get-support"></a><span data-ttu-id="f1294-137">Get support</span><span class="sxs-lookup"><span data-stu-id="f1294-137">Get support</span></span>

<span data-ttu-id="f1294-138">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="f1294-138">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1294-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="f1294-139">Next steps</span></span>

* [<span data-ttu-id="f1294-140">Introduction to Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f1294-140">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="f1294-141">Get started using Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f1294-141">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="f1294-142">Scale Azure Stream Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="f1294-142">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="f1294-143">Azure Stream Analytics Query Language Reference</span><span class="sxs-lookup"><span data-stu-id="f1294-143">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="f1294-144">Azure Stream Analytics Management REST API Reference</span><span class="sxs-lookup"><span data-stu-id="f1294-144">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

