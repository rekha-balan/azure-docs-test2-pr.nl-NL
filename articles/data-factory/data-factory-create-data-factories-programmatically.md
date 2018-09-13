---
title: Create data pipelines by using Azure .NET SDK | Microsoft Docs
description: Learn how to programmatically create, monitor, and manage Azure data factories by using Data Factory SDK.
services: data-factory
documentationcenter: ''
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b0a357be-3040-4789-831e-0d0a32a0bda5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: spelluru
ms.openlocfilehash: 280737097038ff328d487477279ce4f204b0ac0c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555794"
---
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a><span data-ttu-id="5b694-103">Create, monitor, and manage Azure data factories using Azure Data Factory .NET SDK</span><span class="sxs-lookup"><span data-stu-id="5b694-103">Create, monitor, and manage Azure data factories using Azure Data Factory .NET SDK</span></span>
## <a name="overview"></a><span data-ttu-id="5b694-104">Overview</span><span class="sxs-lookup"><span data-stu-id="5b694-104">Overview</span></span>
<span data-ttu-id="5b694-105">You can create, monitor, and manage Azure data factories programmatically using Data Factory .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="5b694-105">You can create, monitor, and manage Azure data factories programmatically using Data Factory .NET SDK.</span></span> <span data-ttu-id="5b694-106">This article contains a walkthrough that you can follow to create a sample .NET console application that creates and monitors a data factory.</span><span class="sxs-lookup"><span data-stu-id="5b694-106">This article contains a walkthrough that you can follow to create a sample .NET console application that creates and monitors a data factory.</span></span> <span data-ttu-id="5b694-107">See [Data Factory Class Library Reference](https://msdn.microsoft.com/library/mt415893.aspx) for details about Data Factory .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="5b694-107">See [Data Factory Class Library Reference](https://msdn.microsoft.com/library/mt415893.aspx) for details about Data Factory .NET SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b694-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5b694-108">Prerequisites</span></span>
* <span data-ttu-id="5b694-109">Visual Studio 2012 or 2013 or 2015</span><span class="sxs-lookup"><span data-stu-id="5b694-109">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="5b694-110">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="5b694-110">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="5b694-111">Add a native client application to Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5b694-111">Add a native client application to Azure Active Directory.</span></span> <span data-ttu-id="5b694-112">See [Integrating applications with Azure Active Directory](../active-directory/active-directory-integrating-applications.md) for steps to add the application.</span><span class="sxs-lookup"><span data-stu-id="5b694-112">See [Integrating applications with Azure Active Directory](../active-directory/active-directory-integrating-applications.md) for steps to add the application.</span></span> <span data-ttu-id="5b694-113">Note down the **CLIENT ID** and **REDIRECT URI** on the **CONFIGURE** page.</span><span class="sxs-lookup"><span data-stu-id="5b694-113">Note down the **CLIENT ID** and **REDIRECT URI** on the **CONFIGURE** page.</span></span> <span data-ttu-id="5b694-114">See [Copy Activity tutorial using .NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md) article for detailed steps.</span><span class="sxs-lookup"><span data-stu-id="5b694-114">See [Copy Activity tutorial using .NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md) article for detailed steps.</span></span> 
* <span data-ttu-id="5b694-115">Get your Azure **subscription ID** and **tenant ID**.</span><span class="sxs-lookup"><span data-stu-id="5b694-115">Get your Azure **subscription ID** and **tenant ID**.</span></span> <span data-ttu-id="5b694-116">See [Get Azure subscription and tenant IDs](#get-azure-subscription-and-tenant-ids) for instructions.</span><span class="sxs-lookup"><span data-stu-id="5b694-116">See [Get Azure subscription and tenant IDs](#get-azure-subscription-and-tenant-ids) for instructions.</span></span>
* <span data-ttu-id="5b694-117">Download and install NuGet packages for Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="5b694-117">Download and install NuGet packages for Azure Data Factory.</span></span> <span data-ttu-id="5b694-118">Instructions are in the walkthrough.</span><span class="sxs-lookup"><span data-stu-id="5b694-118">Instructions are in the walkthrough.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="5b694-119">Walkthrough</span><span class="sxs-lookup"><span data-stu-id="5b694-119">Walkthrough</span></span>
1. <span data-ttu-id="5b694-120">Using Visual Studio 2012 or 2013, create a C# .NET console application.</span><span class="sxs-lookup"><span data-stu-id="5b694-120">Using Visual Studio 2012 or 2013, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="5b694-121">Launch **Visual Studio 2012/2013/2015**.</span><span class="sxs-lookup"><span data-stu-id="5b694-121">Launch **Visual Studio 2012/2013/2015**.</span></span>
   2. <span data-ttu-id="5b694-122">Click **File**, point to **New**, and click **Project**.</span><span class="sxs-lookup"><span data-stu-id="5b694-122">Click **File**, point to **New**, and click **Project**.</span></span>
   3. <span data-ttu-id="5b694-123">Expand **Templates**, and select **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="5b694-123">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="5b694-124">In this walkthrough, you use C#, but you can use any .NET language.</span><span class="sxs-lookup"><span data-stu-id="5b694-124">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="5b694-125">Select **Console Application** from the list of project types on the right.</span><span class="sxs-lookup"><span data-stu-id="5b694-125">Select **Console Application** from the list of project types on the right.</span></span>
   5. <span data-ttu-id="5b694-126">Enter **DataFactoryAPITestApp** for the **Name**.</span><span class="sxs-lookup"><span data-stu-id="5b694-126">Enter **DataFactoryAPITestApp** for the **Name**.</span></span>
   6. <span data-ttu-id="5b694-127">Select **C:\ADFGetStarted** for the **Location**.</span><span class="sxs-lookup"><span data-stu-id="5b694-127">Select **C:\ADFGetStarted** for the **Location**.</span></span>
   7. <span data-ttu-id="5b694-128">Click **OK** to create the project.</span><span class="sxs-lookup"><span data-stu-id="5b694-128">Click **OK** to create the project.</span></span>
2. <span data-ttu-id="5b694-129">Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="5b694-129">Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="5b694-130">In the **Package Manager Console**, execute the following commands one-by-one.</span><span class="sxs-lookup"><span data-stu-id="5b694-130">In the **Package Manager Console**, execute the following commands one-by-one.</span></span>

    ```
    Install-Package Microsoft.Azure.Management.DataFactories
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213
    ```
4. <span data-ttu-id="5b694-131">Add the following **appSetttings** section to the **App.config** file.</span><span class="sxs-lookup"><span data-stu-id="5b694-131">Add the following **appSetttings** section to the **App.config** file.</span></span> <span data-ttu-id="5b694-132">These configuration values are used by the **GetAuthorizationHeader** method.</span><span class="sxs-lookup"><span data-stu-id="5b694-132">These configuration values are used by the **GetAuthorizationHeader** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="5b694-133">Replace values for **AdfClientId**, **RedirectUri**, **SubscriptionId**, and **ActiveDirectoryTenantId** with your own values.</span><span class="sxs-lookup"><span data-stu-id="5b694-133">Replace values for **AdfClientId**, **RedirectUri**, **SubscriptionId**, and **ActiveDirectoryTenantId** with your own values.</span></span>

    ```XML
    <appSettings>
        <add key="ActiveDirectoryEndpoint" value="https://login.windows.net/" />
        <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
        <add key="WindowsManagementUri" value="https://management.core.windows.net/" />
    
        <!-- Replace the following values with your own -->
        <add key="AdfClientId" value="Your AAD application ID" />
        <add key="RedirectUri" value="Your AAD application's redirect URI" />
        <add key="SubscriptionId" value="your subscription ID" />
        <add key="ActiveDirectoryTenantId" value="your tenant ID" />
    </appSettings>
    ```
5. <span data-ttu-id="5b694-134">Add the following **using** statements to the source file (Program.cs) in the project.</span><span class="sxs-lookup"><span data-stu-id="5b694-134">Add the following **using** statements to the source file (Program.cs) in the project.</span></span>

    ```csharp
    using System.Configuration;
    using System.Collections.ObjectModel;
    using System.Threading;
    using System.Threading.Tasks;

    using Microsoft.Azure;
    using Microsoft.Azure.Management.DataFactories;
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Common.Models;

    using Microsoft.IdentityModel.Clients.ActiveDirectory;

    ```
6. <span data-ttu-id="5b694-135">Add the following code that creates an instance of **DataPipelineManagementClient** class to the **Main** method.</span><span class="sxs-lookup"><span data-stu-id="5b694-135">Add the following code that creates an instance of **DataPipelineManagementClient** class to the **Main** method.</span></span> <span data-ttu-id="5b694-136">You use this object to create a data factory, a linked service, input and output datasets, and a pipeline.</span><span class="sxs-lookup"><span data-stu-id="5b694-136">You use this object to create a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="5b694-137">You also use this object to monitor slices of a dataset at runtime.</span><span class="sxs-lookup"><span data-stu-id="5b694-137">You also use this object to monitor slices of a dataset at runtime.</span></span>

    ```csharp
    // create data factory management client
    string resourceGroupName = "resourcegroupname";
    string dataFactoryName = "APITutorialFactorySP";
    
    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
        GetAuthorizationHeader().Result);
    
    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);
    
    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!NOTE]
   > <span data-ttu-id="5b694-138">Replace the **resourcegroupname** with the name of your Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="5b694-138">Replace the **resourcegroupname** with the name of your Azure resource group.</span></span> <span data-ttu-id="5b694-139">You can create a resource group using the [New-AzureResourceGroup](https://msdn.microsoft.com/library/Dn654594.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5b694-139">You can create a resource group using the [New-AzureResourceGroup](https://msdn.microsoft.com/library/Dn654594.aspx) cmdlet.</span></span>
7. <span data-ttu-id="5b694-140">Add the following code that creates a **data factory** to the **Main** method.</span><span class="sxs-lookup"><span data-stu-id="5b694-140">Add the following code that creates a **data factory** to the **Main** method.</span></span>

    ```csharp
    // create a data factory
    Console.WriteLine("Creating a data factory");
    client.DataFactories.CreateOrUpdate(resourceGroupName,
        new DataFactoryCreateOrUpdateParameters()
        {
            DataFactory = new DataFactory()
            {
                Name = dataFactoryName,
                Location = "westus",
                Properties = new DataFactoryProperties()
            }
        }
    );
    ```
8. <span data-ttu-id="5b694-141">Add the following code that creates a **linked service** to the **Main** method.</span><span class="sxs-lookup"><span data-stu-id="5b694-141">Add the following code that creates a **linked service** to the **Main** method.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5b694-142">Use **account name** and **account key** of your Azure storage account for the **ConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="5b694-142">Use **account name** and **account key** of your Azure storage account for the **ConnectionString**.</span></span>

    ```csharp
    // create a linked service
    Console.WriteLine("Creating a linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "LinkedService-AzureStorage",
                Properties = new LinkedServiceProperties
                (
                    new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>")
                )
            }
        }
    );
    ```
9. <span data-ttu-id="5b694-143">Add the following code that creates **input and output datasets** to the **Main** method.</span><span class="sxs-lookup"><span data-stu-id="5b694-143">Add the following code that creates **input and output datasets** to the **Main** method.</span></span>

    <span data-ttu-id="5b694-144">The **FolderPath** for the input blob is set to **adftutorial/** where **adftutorial** is the name of the container in your blob storage.</span><span class="sxs-lookup"><span data-stu-id="5b694-144">The **FolderPath** for the input blob is set to **adftutorial/** where **adftutorial** is the name of the container in your blob storage.</span></span> <span data-ttu-id="5b694-145">If this container does not exist in your Azure blob storage, create a container with this name: **adftutorial** and upload a text file to the container.</span><span class="sxs-lookup"><span data-stu-id="5b694-145">If this container does not exist in your Azure blob storage, create a container with this name: **adftutorial** and upload a text file to the container.</span></span>

    <span data-ttu-id="5b694-146">The FolderPath for the output blob is set to: **adftutorial/apifactoryoutput/{Slice}** where **Slice** is dynamically calculated based on the value of **SliceStart** (start date-time of each slice.)</span><span class="sxs-lookup"><span data-stu-id="5b694-146">The FolderPath for the output blob is set to: **adftutorial/apifactoryoutput/{Slice}** where **Slice** is dynamically calculated based on the value of **SliceStart** (start date-time of each slice.)</span></span>

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "DatasetBlobSource";
    string Dataset_Destination = "DatasetBlobDestination";
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                LinkedServiceName = "LinkedService-AzureStorage",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/",
                    FileName = "emp.txt"
                },
                External = true,
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
    
                Policy = new Policy()
                {
                    Validation = new ValidationPolicy()
                    {
                        MinimumRows = 1
                    }
                }
            }
        }
    });
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Destination,
            Properties = new DatasetProperties()
            {
    
                LinkedServiceName = "LinkedService-AzureStorage",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/apifactoryoutput/{Slice}",
                    PartitionedBy = new Collection<Partition>()
                    {
                        new Partition()
                        {
                            Name = "Slice",
                            Value = new DateTimePartitionValue()
                            {
                                Date = "SliceStart",
                                Format = "yyyyMMdd-HH"
                            }
                        }
                    }
                },
    
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
            }
        }
    });
    ```
10. <span data-ttu-id="5b694-147">Add the following code that **creates and activates a pipeline** to the **Main** method.</span><span class="sxs-lookup"><span data-stu-id="5b694-147">Add the following code that **creates and activates a pipeline** to the **Main** method.</span></span> <span data-ttu-id="5b694-148">This pipeline has a **CopyActivity** that takes **BlobSource** as a source and **BlobSink** as a sink.</span><span class="sxs-lookup"><span data-stu-id="5b694-148">This pipeline has a **CopyActivity** that takes **BlobSource** as a source and **BlobSink** as a sink.</span></span>

    <span data-ttu-id="5b694-149">The Copy Activity performs the data movement in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="5b694-149">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="5b694-150">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span><span class="sxs-lookup"><span data-stu-id="5b694-150">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="5b694-151">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="5b694-151">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span>

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2014, 8, 9, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
    string PipelineName = "PipelineBlobSample";
    
    client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new PipelineCreateOrUpdateParameters()
    {
        Pipeline = new Pipeline()
        {
            Name = PipelineName,
            Properties = new PipelineProperties()
            {
                Description = "Demo Pipeline for data transfer between blobs",
    
                // Initial value for pipeline's active period. With this, you won't need to set slice status
                Start = PipelineActivePeriodStartTime,
                End = PipelineActivePeriodEndTime,
    
                Activities = new List<Activity>()
                {
                    new Activity()
                    {
                        Name = "BlobToBlob",
                        Inputs = new List<ActivityInput>()
                        {
                            new ActivityInput()
                {
                                Name = Dataset_Source
                            }
                        },
                        Outputs = new List<ActivityOutput>()
                        {
                            new ActivityOutput()
                            {
                                Name = Dataset_Destination
                            }
                        },
                        TypeProperties = new CopyActivity()
                        {
                            Source = new BlobSource(),
                            Sink = new BlobSink()
                            {
                                WriteBatchSize = 10000,
                                WriteBatchTimeout = TimeSpan.FromMinutes(10)
                            }
                        }
                    }
    
                },
            }
        }
    });
    ```
11. <span data-ttu-id="5b694-152">Add the following helper method used by the **Main** method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="5b694-152">Add the following helper method used by the **Main** method to the **Program** class.</span></span> <span data-ttu-id="5b694-153">This method pops a dialog box that that lets you provide **user name** and **password** that you use to log in to Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5b694-153">This method pops a dialog box that that lets you provide **user name** and **password** that you use to log in to Azure portal.</span></span>

    ```csharp
    public static async Task<string> GetAuthorizationHeader()
    {
        var context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
        AuthenticationResult result = await context.AcquireTokenAsync(
            resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
            clientId: ConfigurationManager.AppSettings["AdfClientId"],
            redirectUri: new Uri(ConfigurationManager.AppSettings["RedirectUri"]),
            promptBehavior: PromptBehavior.Always);

        if (result != null)
            return result.AccessToken;

        throw new InvalidOperationException("Failed to acquire token");
    }
    ```
12. <span data-ttu-id="5b694-154">Add the following code to the **Main** method to get the status of a data slice of the output dataset.</span><span class="sxs-lookup"><span data-stu-id="5b694-154">Add the following code to the **Main** method to get the status of a data slice of the output dataset.</span></span> <span data-ttu-id="5b694-155">There is only one slice expected in this sample.</span><span class="sxs-lookup"><span data-stu-id="5b694-155">There is only one slice expected in this sample.</span></span>

    ```csharp
    // Pulling status within a timeout threshold
    DateTime start = DateTime.Now;
    bool done = false;
    
    while (DateTime.Now - start < TimeSpan.FromMinutes(5) && !done)
    {
        Console.WriteLine("Pulling the slice status");
        // wait before the next status check
        Thread.Sleep(1000 * 12);
    
        var datalistResponse = client.DataSlices.List(resourceGroupName, dataFactoryName, Dataset_Destination,
            new DataSliceListParameters()
            {
                DataSliceRangeStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString(),
                DataSliceRangeEndTime = PipelineActivePeriodEndTime.ConvertToISO8601DateTimeString()
            });
    
        foreach (DataSlice slice in datalistResponse.DataSlices)
        {
            if (slice.State == DataSliceState.Failed || slice.State == DataSliceState.Ready)
            {
                Console.WriteLine("Slice execution is done with status: {0}", slice.State);
                done = true;
                break;
            }
            else
            {
                Console.WriteLine("Slice status is: {0}", slice.State);
            }
        }
    }
    ```
13. <span data-ttu-id="5b694-156">**(optional)** Add the following code to get run details for a data slice to the **Main** method.</span><span class="sxs-lookup"><span data-stu-id="5b694-156">**(optional)** Add the following code to get run details for a data slice to the **Main** method.</span></span>

    ```csharp
    Console.WriteLine("Getting run details of a data slice");
    
    // give it a few minutes for the output slice to be ready
    Console.WriteLine("\nGive it a few minutes for the output slice to be ready and press any key.");
    Console.ReadKey();
    
    var datasliceRunListResponse = client.DataSliceRuns.List(
        resourceGroupName,
        dataFactoryName,
        Dataset_Destination,
        new DataSliceRunListParameters()
        {
            DataSliceStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString()
        });
    
    foreach (DataSliceRun run in datasliceRunListResponse.DataSliceRuns)
    {
        Console.WriteLine("Status: \t\t{0}", run.Status);
        Console.WriteLine("DataSliceStart: \t{0}", run.DataSliceStart);
        Console.WriteLine("DataSliceEnd: \t\t{0}", run.DataSliceEnd);
        Console.WriteLine("ActivityId: \t\t{0}", run.ActivityName);
        Console.WriteLine("ProcessingStartTime: \t{0}", run.ProcessingStartTime);
        Console.WriteLine("ProcessingEndTime: \t{0}", run.ProcessingEndTime);
        Console.WriteLine("ErrorMessage: \t{0}", run.ErrorMessage);
    }
    
    Console.WriteLine("\nPress any key to exit.");
    Console.ReadKey();
    ```
14. <span data-ttu-id="5b694-157">In the Solution Explorer, expand the project: **DataFactoryAPITestApp**, right-click **References**, and click **Add Reference**.</span><span class="sxs-lookup"><span data-stu-id="5b694-157">In the Solution Explorer, expand the project: **DataFactoryAPITestApp**, right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="5b694-158">Select check box for `System.Configuration` assembly and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="5b694-158">Select check box for `System.Configuration` assembly and click **OK**.</span></span>
15. <span data-ttu-id="5b694-159">Build the console application.</span><span class="sxs-lookup"><span data-stu-id="5b694-159">Build the console application.</span></span> <span data-ttu-id="5b694-160">Click **Build** on the menu and click **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="5b694-160">Click **Build** on the menu and click **Build Solution**.</span></span>
16. <span data-ttu-id="5b694-161">Confirm that there is at least one file in the adftutorial container in your Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="5b694-161">Confirm that there is at least one file in the adftutorial container in your Azure blob storage.</span></span> <span data-ttu-id="5b694-162">If not, create Emp.txt file in Notepad with the following content and upload it to the adftutorial container.</span><span class="sxs-lookup"><span data-stu-id="5b694-162">If not, create Emp.txt file in Notepad with the following content and upload it to the adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
17. <span data-ttu-id="5b694-163">Run the sample by clicking **Debug** -> **Start Debugging** on the menu.</span><span class="sxs-lookup"><span data-stu-id="5b694-163">Run the sample by clicking **Debug** -> **Start Debugging** on the menu.</span></span> <span data-ttu-id="5b694-164">When you see the **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="5b694-164">When you see the **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
18. <span data-ttu-id="5b694-165">Use the Azure portal to verify that the data factory **APITutorialFactory** is created with the following artifacts:</span><span class="sxs-lookup"><span data-stu-id="5b694-165">Use the Azure portal to verify that the data factory **APITutorialFactory** is created with the following artifacts:</span></span>
    * <span data-ttu-id="5b694-166">Linked service: **LinkedService_AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="5b694-166">Linked service: **LinkedService_AzureStorage**</span></span>
    * <span data-ttu-id="5b694-167">Dataset: **DatasetBlobSource** and **DatasetBlobDestination**.</span><span class="sxs-lookup"><span data-stu-id="5b694-167">Dataset: **DatasetBlobSource** and **DatasetBlobDestination**.</span></span>
    * <span data-ttu-id="5b694-168">Pipeline: **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="5b694-168">Pipeline: **PipelineBlobSample**</span></span>
19. <span data-ttu-id="5b694-169">Verify that an output file is created in the **apifactoryoutput** folder in the **adftutorial** container.</span><span class="sxs-lookup"><span data-stu-id="5b694-169">Verify that an output file is created in the **apifactoryoutput** folder in the **adftutorial** container.</span></span>

## <a name="log-in-without-popup-dialog-box"></a><span data-ttu-id="5b694-170">Log in without popup dialog box</span><span class="sxs-lookup"><span data-stu-id="5b694-170">Log in without popup dialog box</span></span>
<span data-ttu-id="5b694-171">The sample code in the walkthrough launches a dialog box for you to enter Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="5b694-171">The sample code in the walkthrough launches a dialog box for you to enter Azure credentials.</span></span> <span data-ttu-id="5b694-172">If you need to sign in programmatically without using a dialog-box, see [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="5b694-172">If you need to sign in programmatically without using a dialog-box, see [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5b694-173">Add a Web application to Azure Active Directory and note down the client ID and client secret of the application.</span><span class="sxs-lookup"><span data-stu-id="5b694-173">Add a Web application to Azure Active Directory and note down the client ID and client secret of the application.</span></span>
>
>

### <a name="example"></a><span data-ttu-id="5b694-174">Example</span><span class="sxs-lookup"><span data-stu-id="5b694-174">Example</span></span>
<span data-ttu-id="5b694-175">Create GetAuthorizationHeaderNoPopup method.</span><span class="sxs-lookup"><span data-stu-id="5b694-175">Create GetAuthorizationHeaderNoPopup method.</span></span>

```csharp
public static async Task<string> GetAuthorizationHeaderNoPopup()
{
    var authority = new Uri(new Uri("https://login.windows.net"), ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
    var context = new AuthenticationContext(authority.AbsoluteUri);
    var credential = new ClientCredential(
        ConfigurationManager.AppSettings["AdfClientId"],
    ConfigurationManager.AppSettings["AdfClientSecret"]);
    
    AuthenticationResult result = await context.AcquireTokenAsync(
        ConfigurationManager.AppSettings["WindowsManagementUri"],
    credential);

    if (result != null)
        return result.AccessToken;

    throw new InvalidOperationException("Failed to acquire token");
}
```

<span data-ttu-id="5b694-176">Replace **GetAuthorizationHeader** call with a call to **GetAuthorizationHeaderNoPopup** in the **Main** function:</span><span class="sxs-lookup"><span data-stu-id="5b694-176">Replace **GetAuthorizationHeader** call with a call to **GetAuthorizationHeaderNoPopup** in the **Main** function:</span></span>

```csharp
TokenCloudCredentials aadTokenCredentials =
    new TokenCloudCredentials(
    ConfigurationManager.AppSettings["SubscriptionId"],
    GetAuthorizationHeaderNoPopup().Result);
```

<span data-ttu-id="5b694-177">Here is how you can create the Active Directory application, service principal, and then assign it to the Data Factory Contributor role:</span><span class="sxs-lookup"><span data-stu-id="5b694-177">Here is how you can create the Active Directory application, service principal, and then assign it to the Data Factory Contributor role:</span></span>

1. <span data-ttu-id="5b694-178">Create the AD application.</span><span class="sxs-lookup"><span data-stu-id="5b694-178">Create the AD application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "MyADAppForADF" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.myadappforadf.org/example" -Password "Pass@word1"
    ```
2. <span data-ttu-id="5b694-179">Create the AD service principal.</span><span class="sxs-lookup"><span data-stu-id="5b694-179">Create the AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
3. <span data-ttu-id="5b694-180">Add service principal to the Data Factory Contributor role.</span><span class="sxs-lookup"><span data-stu-id="5b694-180">Add service principal to the Data Factory Contributor role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
4. <span data-ttu-id="5b694-181">Get the application ID.</span><span class="sxs-lookup"><span data-stu-id="5b694-181">Get the application ID.</span></span>

    ```PowerShell
    $azureAdApplication
    ```

<span data-ttu-id="5b694-182">Note down the application ID and the password (client secret) and use it in the walkthrough.</span><span class="sxs-lookup"><span data-stu-id="5b694-182">Note down the application ID and the password (client secret) and use it in the walkthrough.</span></span>

## <a name="get-azure-subscription-and-tenant-ids"></a><span data-ttu-id="5b694-183">Get Azure subscription and tenant IDs</span><span class="sxs-lookup"><span data-stu-id="5b694-183">Get Azure subscription and tenant IDs</span></span>
<span data-ttu-id="5b694-184">If you do not have latest version of PowerShell installed on your machine, follow instructions in [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article to install it.</span><span class="sxs-lookup"><span data-stu-id="5b694-184">If you do not have latest version of PowerShell installed on your machine, follow instructions in [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article to install it.</span></span>

1. <span data-ttu-id="5b694-185">Start Azure PowerShell and run the following command</span><span class="sxs-lookup"><span data-stu-id="5b694-185">Start Azure PowerShell and run the following command</span></span>
2. <span data-ttu-id="5b694-186">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5b694-186">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="5b694-187">If you have only one Azure subscription associated with this account, you do not need to perform the next two steps.</span><span class="sxs-lookup"><span data-stu-id="5b694-187">If you have only one Azure subscription associated with this account, you do not need to perform the next two steps.</span></span>
3. <span data-ttu-id="5b694-188">Run the following command to view all the subscriptions for this account.</span><span class="sxs-lookup"><span data-stu-id="5b694-188">Run the following command to view all the subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="5b694-189">Run the following command to select the subscription that you want to work with.</span><span class="sxs-lookup"><span data-stu-id="5b694-189">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="5b694-190">Replace **NameOfAzureSubscription** with the name of your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="5b694-190">Replace **NameOfAzureSubscription** with the name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName NameOfAzureSubscription | Set-AzureRmContext
    ```PowerShell

Note down the **SubscriptionId** and **TenantId** values.
