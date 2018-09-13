---
title: Management .NET SDK for Azure Stream Analytics
description: Get started with Stream Analytics Management .NET SDK. Learn how to set up and run analytics jobs. Create a project, inputs, outputs, and transformations.
services: stream-analytics
author: jseb225
ms.author: jeanb
manager: kfile
ms.reviewer: jasonh
ms.service: stream-analytics
ms.topic: conceptual
ms.date: 03/06/2017
ms.openlocfilehash: b57e22b979d0e47d294a89d41a945a665beacdc0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44787142"
---
# <a name="management-net-sdk-set-up-and-run-analytics-jobs-using-the-azure-stream-analytics-api-for-net"></a><span data-ttu-id="d2db7-105">Management .NET SDK: Set up and run analytics jobs using the Azure Stream Analytics API for .NET</span><span class="sxs-lookup"><span data-stu-id="d2db7-105">Management .NET SDK: Set up and run analytics jobs using the Azure Stream Analytics API for .NET</span></span>
<span data-ttu-id="d2db7-106">Learn how to set up and run analytics jobs using the Stream Analytics API for .NET using the Management .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="d2db7-106">Learn how to set up and run analytics jobs using the Stream Analytics API for .NET using the Management .NET SDK.</span></span> <span data-ttu-id="d2db7-107">Set up a project, create input and output sources, transformations, and start and stop jobs.</span><span class="sxs-lookup"><span data-stu-id="d2db7-107">Set up a project, create input and output sources, transformations, and start and stop jobs.</span></span> <span data-ttu-id="d2db7-108">For your analytics jobs, you can stream data from Blob storage or from an event hub.</span><span class="sxs-lookup"><span data-stu-id="d2db7-108">For your analytics jobs, you can stream data from Blob storage or from an event hub.</span></span>

<span data-ttu-id="d2db7-109">See the [management reference documentation for the Stream Analytics API for .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="d2db7-109">See the [management reference documentation for the Stream Analytics API for .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>

<span data-ttu-id="d2db7-110">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable, complex event processing over streaming data in the cloud.</span><span class="sxs-lookup"><span data-stu-id="d2db7-110">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable, complex event processing over streaming data in the cloud.</span></span> <span data-ttu-id="d2db7-111">Stream Analytics enables customers to set up streaming jobs to analyze data streams, and allows them to drive near real-time analytics.</span><span class="sxs-lookup"><span data-stu-id="d2db7-111">Stream Analytics enables customers to set up streaming jobs to analyze data streams, and allows them to drive near real-time analytics.</span></span>  

> [!NOTE]
> <span data-ttu-id="d2db7-112">We have updated the sample code in this article with Azure Stream Analytics Management .NET SDK v2.x version.</span><span class="sxs-lookup"><span data-stu-id="d2db7-112">We have updated the sample code in this article with Azure Stream Analytics Management .NET SDK v2.x version.</span></span> <span data-ttu-id="d2db7-113">For sample code using the uses lagecy (1.x) SDK version, please see [Use the Management .NET SDK v1.x for Stream Analytics](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1).</span><span class="sxs-lookup"><span data-stu-id="d2db7-113">For sample code using the uses lagecy (1.x) SDK version, please see [Use the Management .NET SDK v1.x for Stream Analytics](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2db7-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d2db7-114">Prerequisites</span></span>
<span data-ttu-id="d2db7-115">Before you begin this article, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="d2db7-115">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="d2db7-116">Install Visual Studio 2017 or 2015.</span><span class="sxs-lookup"><span data-stu-id="d2db7-116">Install Visual Studio 2017 or 2015.</span></span>
* <span data-ttu-id="d2db7-117">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="d2db7-117">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="d2db7-118">Create an Azure Resource Group in your subscription.</span><span class="sxs-lookup"><span data-stu-id="d2db7-118">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="d2db7-119">The following is a sample Azure PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="d2db7-119">The following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="d2db7-120">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span><span class="sxs-lookup"><span data-stu-id="d2db7-120">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

        # Log in to your Azure account
        Add-AzureAccount

        # Select the Azure subscription you want to use to create the resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered to the subscription, remove the remark symbol (#) to run the Register-AzureRMProvider cmdlet to register the provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* <span data-ttu-id="d2db7-121">Set up an input source and output target for the job to connect to.</span><span class="sxs-lookup"><span data-stu-id="d2db7-121">Set up an input source and output target for the job to connect to.</span></span>

## <a name="set-up-a-project"></a><span data-ttu-id="d2db7-122">Set up a project</span><span class="sxs-lookup"><span data-stu-id="d2db7-122">Set up a project</span></span>
<span data-ttu-id="d2db7-123">To create an analytics job use the Stream Analytics API for .NET, first set up your project.</span><span class="sxs-lookup"><span data-stu-id="d2db7-123">To create an analytics job use the Stream Analytics API for .NET, first set up your project.</span></span>

1. <span data-ttu-id="d2db7-124">Create a Visual Studio C# .NET console application.</span><span class="sxs-lookup"><span data-stu-id="d2db7-124">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="d2db7-125">In the Package Manager Console, run the following commands to install the NuGet packages.</span><span class="sxs-lookup"><span data-stu-id="d2db7-125">In the Package Manager Console, run the following commands to install the NuGet packages.</span></span> <span data-ttu-id="d2db7-126">The first one is the Azure Stream Analytics Management .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="d2db7-126">The first one is the Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="d2db7-127">The second one is for Azure client authentication.</span><span class="sxs-lookup"><span data-stu-id="d2db7-127">The second one is for Azure client authentication.</span></span>
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 2.0.0
        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Version 2.3.1
3. <span data-ttu-id="d2db7-128">Add the following **appSettings** section to the App.config file:</span><span class="sxs-lookup"><span data-stu-id="d2db7-128">Add the following **appSettings** section to the App.config file:</span></span>
   
        <appSettings>
          <add key="ClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
          <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
          <add key="SubscriptionId" value="YOUR SUBSCRIPTION ID" />
          <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
        </appSettings>

    <span data-ttu-id="d2db7-129">Replace values for **SubscriptionId** and **ActiveDirectoryTenantId** with your Azure subscription and tenant IDs.</span><span class="sxs-lookup"><span data-stu-id="d2db7-129">Replace values for **SubscriptionId** and **ActiveDirectoryTenantId** with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="d2db7-130">You can get these values by running the following Azure PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d2db7-130">You can get these values by running the following Azure PowerShell cmdlet:</span></span>

        Get-AzureAccount

4. <span data-ttu-id="d2db7-131">Add the following reference in your .csproj file:</span><span class="sxs-lookup"><span data-stu-id="d2db7-131">Add the following reference in your .csproj file:</span></span>

        <Reference Include="System.Configuration" />

5. <span data-ttu-id="d2db7-132">Add the following **using** statements to the source file (Program.cs) in the project:</span><span class="sxs-lookup"><span data-stu-id="d2db7-132">Add the following **using** statements to the source file (Program.cs) in the project:</span></span>
   
        using System;
        using System.Collections.Generic;
        using System.Configuration;
        using System.Threading;
        using System.Threading.Tasks;
        
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Rest;
6. <span data-ttu-id="d2db7-133">Add an authentication helper method:</span><span class="sxs-lookup"><span data-stu-id="d2db7-133">Add an authentication helper method:</span></span>

   ```
   private static async Task<ServiceClientCredentials> GetCredentials()
   {
       var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(ConfigurationManager.AppSettings["ClientId"], new Uri("urn:ietf:wg:oauth:2.0:oob"));
       ServiceClientCredentials credentials = await UserTokenProvider.LoginWithPromptAsync(ConfigurationManager.AppSettings["ActiveDirectoryTenantId"], activeDirectoryClientSettings);
       
       return credentials;
    }
   ```

## <a name="create-a-stream-analytics-management-client"></a><span data-ttu-id="d2db7-134">Create a Stream Analytics management client</span><span class="sxs-lookup"><span data-stu-id="d2db7-134">Create a Stream Analytics management client</span></span>
<span data-ttu-id="d2db7-135">A **StreamAnalyticsManagementClient** object allows you to manage the job and the job components, such as input, output, and transformation.</span><span class="sxs-lookup"><span data-stu-id="d2db7-135">A **StreamAnalyticsManagementClient** object allows you to manage the job and the job components, such as input, output, and transformation.</span></span>

<span data-ttu-id="d2db7-136">Add the following code to the beginning of the **Main** method:</span><span class="sxs-lookup"><span data-stu-id="d2db7-136">Add the following code to the beginning of the **Main** method:</span></span>

   ```
    string resourceGroupName = "<YOUR AZURE RESOURCE GROUP NAME>";
    string streamingJobName = "<YOUR STREAMING JOB NAME>";
    string inputName = "<YOUR JOB INPUT NAME>";
    string transformationName = "<YOUR JOB TRANSFORMATION NAME>";
    string outputName = "<YOUR JOB OUTPUT NAME>";
    
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    
    // Get credentials
    ServiceClientCredentials credentials = GetCredentials().Result;
    
    // Create Stream Analytics management client
    StreamAnalyticsManagementClient streamAnalyticsManagementClient = new StreamAnalyticsManagementClient(credentials)
    {
        SubscriptionId = ConfigurationManager.AppSettings["SubscriptionId"]
    };
   ```

<span data-ttu-id="d2db7-137">The **resourceGroupName** variable's value should be the same as the name of the resource group you created or picked in the prerequisite steps.</span><span class="sxs-lookup"><span data-stu-id="d2db7-137">The **resourceGroupName** variable's value should be the same as the name of the resource group you created or picked in the prerequisite steps.</span></span>

<span data-ttu-id="d2db7-138">To automate the credential presentation aspect of job creation, refer to [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="d2db7-138">To automate the credential presentation aspect of job creation, refer to [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="d2db7-139">The remaining sections of this article assume that this code is at the beginning of the **Main** method.</span><span class="sxs-lookup"><span data-stu-id="d2db7-139">The remaining sections of this article assume that this code is at the beginning of the **Main** method.</span></span>

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="d2db7-140">Create a Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="d2db7-140">Create a Stream Analytics job</span></span>
<span data-ttu-id="d2db7-141">The following code creates a Stream Analytics job under the resource group that you have defined.</span><span class="sxs-lookup"><span data-stu-id="d2db7-141">The following code creates a Stream Analytics job under the resource group that you have defined.</span></span> <span data-ttu-id="d2db7-142">You will add an input, output, and transformation to the job later.</span><span class="sxs-lookup"><span data-stu-id="d2db7-142">You will add an input, output, and transformation to the job later.</span></span>

   ```
   // Create a streaming job
   StreamingJob streamingJob = new StreamingJob()
   {
       Tags = new Dictionary<string, string>()
       {
           { "Origin", ".NET SDK" },
           { "ReasonCreated", "Getting started tutorial" }
       },
       Location = "West US",
       EventsOutOfOrderPolicy = EventsOutOfOrderPolicy.Drop,
       EventsOutOfOrderMaxDelayInSeconds = 5,
       EventsLateArrivalMaxDelayInSeconds = 16,
       OutputErrorPolicy = OutputErrorPolicy.Drop,
       DataLocale = "en-US",
       CompatibilityLevel = CompatibilityLevel.OneFullStopZero,
       Sku = new Sku()
       {
           Name = SkuName.Standard
       }
   };
   StreamingJob createStreamingJobResult = streamAnalyticsManagementClient.StreamingJobs.CreateOrReplace(streamingJob, resourceGroupName, streamingJobName);
   ```

## <a name="create-a-stream-analytics-input-source"></a><span data-ttu-id="d2db7-143">Create a Stream Analytics input source</span><span class="sxs-lookup"><span data-stu-id="d2db7-143">Create a Stream Analytics input source</span></span>
<span data-ttu-id="d2db7-144">The following code creates a Stream Analytics input source with the blob input source type and CSV serialization.</span><span class="sxs-lookup"><span data-stu-id="d2db7-144">The following code creates a Stream Analytics input source with the blob input source type and CSV serialization.</span></span> <span data-ttu-id="d2db7-145">To create an event hub input source, use **EventHubStreamInputDataSource** instead of **BlobStreamInputDataSource**.</span><span class="sxs-lookup"><span data-stu-id="d2db7-145">To create an event hub input source, use **EventHubStreamInputDataSource** instead of **BlobStreamInputDataSource**.</span></span> <span data-ttu-id="d2db7-146">Similarly, you can customize the serialization type of the input source.</span><span class="sxs-lookup"><span data-stu-id="d2db7-146">Similarly, you can customize the serialization type of the input source.</span></span>

   ```
   // Create an input
   StorageAccount storageAccount = new StorageAccount()
   {
       AccountName = "<YOUR STORAGE ACCOUNT NAME>",
       AccountKey = "<YOUR STORAGE ACCOUNT KEY>"
   };
   Input input = new Input()
   {
       Properties = new StreamInputProperties()
       {
           Serialization = new CsvSerialization()
           {
               FieldDelimiter = ",",
               Encoding = Encoding.UTF8
           },
           Datasource = new BlobStreamInputDataSource()
           {
               StorageAccounts = new[] { storageAccount },
               Container = "<YOUR STORAGE BLOB CONTAINER>",
               PathPattern = "{date}/{time}",
               DateFormat = "yyyy/MM/dd",
               TimeFormat = "HH",
               SourcePartitionCount = 16
           }
       }
   };
   Input createInputResult = streamAnalyticsManagementClient.Inputs.CreateOrReplace(input, resourceGroupName, streamingJobName, inputName);
   ```

<span data-ttu-id="d2db7-147">Input sources, whether from Blob storage or an event hub, are tied to a specific job.</span><span class="sxs-lookup"><span data-stu-id="d2db7-147">Input sources, whether from Blob storage or an event hub, are tied to a specific job.</span></span> <span data-ttu-id="d2db7-148">To use the same input source for different jobs, you must call the method again and specify a different job name.</span><span class="sxs-lookup"><span data-stu-id="d2db7-148">To use the same input source for different jobs, you must call the method again and specify a different job name.</span></span>

## <a name="test-a-stream-analytics-input-source"></a><span data-ttu-id="d2db7-149">Test a Stream Analytics input source</span><span class="sxs-lookup"><span data-stu-id="d2db7-149">Test a Stream Analytics input source</span></span>
<span data-ttu-id="d2db7-150">The **TestConnection** method tests whether the Stream Analytics job is able to connect to the input source as well as other aspects specific to the input source type.</span><span class="sxs-lookup"><span data-stu-id="d2db7-150">The **TestConnection** method tests whether the Stream Analytics job is able to connect to the input source as well as other aspects specific to the input source type.</span></span> <span data-ttu-id="d2db7-151">For example, in the blob input source you created in an earlier step, the method will check that the Storage account name and key pair can be used to connect to the Storage account as well as check that the specified container exists.</span><span class="sxs-lookup"><span data-stu-id="d2db7-151">For example, in the blob input source you created in an earlier step, the method will check that the Storage account name and key pair can be used to connect to the Storage account as well as check that the specified container exists.</span></span>

   ```
   // Test the connection to the input
   ResourceTestStatus testInputResult = streamAnalyticsManagementClient.Inputs.Test(resourceGroupName, streamingJobName, inputName);
   ```

## <a name="create-a-stream-analytics-output-target"></a><span data-ttu-id="d2db7-152">Create a Stream Analytics output target</span><span class="sxs-lookup"><span data-stu-id="d2db7-152">Create a Stream Analytics output target</span></span>
<span data-ttu-id="d2db7-153">Creating an output target is very similar to creating a Stream Analytics input source.</span><span class="sxs-lookup"><span data-stu-id="d2db7-153">Creating an output target is very similar to creating a Stream Analytics input source.</span></span> <span data-ttu-id="d2db7-154">Like input sources, output targets are tied to a specific job.</span><span class="sxs-lookup"><span data-stu-id="d2db7-154">Like input sources, output targets are tied to a specific job.</span></span> <span data-ttu-id="d2db7-155">To use the same output target for different jobs, you must call the method again and specify a different job name.</span><span class="sxs-lookup"><span data-stu-id="d2db7-155">To use the same output target for different jobs, you must call the method again and specify a different job name.</span></span>

<span data-ttu-id="d2db7-156">The following code creates an output target (Azure SQL database).</span><span class="sxs-lookup"><span data-stu-id="d2db7-156">The following code creates an output target (Azure SQL database).</span></span> <span data-ttu-id="d2db7-157">You can customize the output target's data type and/or serialization type.</span><span class="sxs-lookup"><span data-stu-id="d2db7-157">You can customize the output target's data type and/or serialization type.</span></span>

   ```
   // Create an output
   Output output = new Output()
   {
       Datasource = new AzureSqlDatabaseOutputDataSource()
       {
           Server = "<YOUR DATABASE SERVER NAME>",
           Database = "<YOUR DATABASE NAME>",
           User = "<YOUR DATABASE LOGIN>",
           Password = "<YOUR DATABASE LOGIN PASSWORD>",
           Table = "<YOUR DATABASE TABLE NAME>"
       }
   };
   Output createOutputResult = streamAnalyticsManagementClient.Outputs.CreateOrReplace(output, resourceGroupName, streamingJobName, outputName);
   ```

## <a name="test-a-stream-analytics-output-target"></a><span data-ttu-id="d2db7-158">Test a Stream Analytics output target</span><span class="sxs-lookup"><span data-stu-id="d2db7-158">Test a Stream Analytics output target</span></span>
<span data-ttu-id="d2db7-159">A Stream Analytics output target also has the **TestConnection** method for testing connections.</span><span class="sxs-lookup"><span data-stu-id="d2db7-159">A Stream Analytics output target also has the **TestConnection** method for testing connections.</span></span>

   ```
   // Test the connection to the output
   ResourceTestStatus testOutputResult = streamAnalyticsManagementClient.Outputs.Test(resourceGroupName, streamingJobName, outputName);
   ```

## <a name="create-a-stream-analytics-transformation"></a><span data-ttu-id="d2db7-160">Create a Stream Analytics transformation</span><span class="sxs-lookup"><span data-stu-id="d2db7-160">Create a Stream Analytics transformation</span></span>
<span data-ttu-id="d2db7-161">The following code creates a Stream Analytics transformation with the query "select \* from Input" and specifies to allocate one streaming unit for the Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="d2db7-161">The following code creates a Stream Analytics transformation with the query "select \* from Input" and specifies to allocate one streaming unit for the Stream Analytics job.</span></span> <span data-ttu-id="d2db7-162">For more information on adjusting streaming units, see [Scale Azure Stream Analytics jobs](stream-analytics-scale-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="d2db7-162">For more information on adjusting streaming units, see [Scale Azure Stream Analytics jobs](stream-analytics-scale-jobs.md).</span></span>

   ```
   // Create a transformation
   Transformation transformation = new Transformation()
   {
       Query = "Select Id, Name from <your input name>", // '<your input name>' should be replaced with the value you put for the 'inputName' variable above or in a previous step
       StreamingUnits = 1
   };
   Transformation createTransformationResult = streamAnalyticsManagementClient.Transformations.CreateOrReplace(transformation, resourceGroupName, streamingJobName, transformationName);
   ```

<span data-ttu-id="d2db7-163">Like input and output, a transformation is also tied to the specific Stream Analytics job it was created under.</span><span class="sxs-lookup"><span data-stu-id="d2db7-163">Like input and output, a transformation is also tied to the specific Stream Analytics job it was created under.</span></span>

## <a name="start-a-stream-analytics-job"></a><span data-ttu-id="d2db7-164">Start a Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="d2db7-164">Start a Stream Analytics job</span></span>
<span data-ttu-id="d2db7-165">After creating a Stream Analytics job and its input(s), output(s), and transformation, you can start the job by calling the **Start** method.</span><span class="sxs-lookup"><span data-stu-id="d2db7-165">After creating a Stream Analytics job and its input(s), output(s), and transformation, you can start the job by calling the **Start** method.</span></span>

<span data-ttu-id="d2db7-166">The following sample code starts a Stream Analytics job with a custom output start time set to December 12, 2012, 12:12:12 UTC:</span><span class="sxs-lookup"><span data-stu-id="d2db7-166">The following sample code starts a Stream Analytics job with a custom output start time set to December 12, 2012, 12:12:12 UTC:</span></span>

   ```
   // Start a streaming job
   StartStreamingJobParameters startStreamingJobParameters = new StartStreamingJobParameters()
   {
       OutputStartMode = OutputStartMode.CustomTime,
       OutputStartTime = new DateTime(2012, 12, 12, 12, 12, 12, DateTimeKind.Utc)
   };
   streamAnalyticsManagementClient.StreamingJobs.Start(resourceGroupName, streamingJobName, startStreamingJobParameters);
   ```

## <a name="stop-a-stream-analytics-job"></a><span data-ttu-id="d2db7-167">Stop a Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="d2db7-167">Stop a Stream Analytics job</span></span>
<span data-ttu-id="d2db7-168">You can stop a running Stream Analytics job by calling the **Stop** method.</span><span class="sxs-lookup"><span data-stu-id="d2db7-168">You can stop a running Stream Analytics job by calling the **Stop** method.</span></span>

   ```
   // Stop a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Stop(resourceGroupName, streamingJobName);
   ```

## <a name="delete-a-stream-analytics-job"></a><span data-ttu-id="d2db7-169">Delete a Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="d2db7-169">Delete a Stream Analytics job</span></span>
<span data-ttu-id="d2db7-170">The **Delete** method will delete the job as well as the underlying sub-resources, including input(s), output(s), and transformation of the job.</span><span class="sxs-lookup"><span data-stu-id="d2db7-170">The **Delete** method will delete the job as well as the underlying sub-resources, including input(s), output(s), and transformation of the job.</span></span>

   ```
   // Delete a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Delete(resourceGroupName, streamingJobName);
   ```

## <a name="get-support"></a><span data-ttu-id="d2db7-171">Get support</span><span class="sxs-lookup"><span data-stu-id="d2db7-171">Get support</span></span>
<span data-ttu-id="d2db7-172">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="d2db7-172">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2db7-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="d2db7-173">Next steps</span></span>
<span data-ttu-id="d2db7-174">You've learned the basics of using a .NET SDK to create and run analytics jobs.</span><span class="sxs-lookup"><span data-stu-id="d2db7-174">You've learned the basics of using a .NET SDK to create and run analytics jobs.</span></span> <span data-ttu-id="d2db7-175">To learn more, see the following:</span><span class="sxs-lookup"><span data-stu-id="d2db7-175">To learn more, see the following:</span></span>

* [<span data-ttu-id="d2db7-176">Introduction to Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d2db7-176">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="d2db7-177">Get started using Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d2db7-177">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="d2db7-178">Scale Azure Stream Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="d2db7-178">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="d2db7-179">[Azure Stream Analytics Management .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="d2db7-179">[Azure Stream Analytics Management .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>
* [<span data-ttu-id="d2db7-180">Azure Stream Analytics Query Language Reference</span><span class="sxs-lookup"><span data-stu-id="d2db7-180">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="d2db7-181">Azure Stream Analytics Management REST API Reference</span><span class="sxs-lookup"><span data-stu-id="d2db7-181">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->
[5]: ./media/markdown-template-for-new-articles/octocats.png
[6]: ./media/markdown-template-for-new-articles/pretty49.png
[7]: ./media/markdown-template-for-new-articles/channel-9.png


<!--Link references-->
[azure.blob.storage]: http://azure.microsoft.com/documentation/services/storage/
[azure.blob.storage.use]: http://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-blobs/

[azure.event.hubs]: http://azure.microsoft.com/services/event-hubs/
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.forum]: http://go.microsoft.com/fwlink/?LinkId=512151

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
