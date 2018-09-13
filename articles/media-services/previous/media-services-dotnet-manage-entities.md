---
title: Managing Assets and Related Entities with Media Services .NET SDK
description: Learn how to manage assets and related entities with the Media Services SDK for .NET.
author: juliako
manager: cfowler
editor: ''
services: media-services
documentationcenter: ''
ms.assetid: 1bd8fd42-7306-463d-bfe5-f642802f1906
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: af5baf3444196e5a0e8412d9ab4f019fdccb033e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856832"
---
# <a name="managing-assets-and-related-entities-with-media-services-net-sdk"></a><span data-ttu-id="afdad-103">Managing Assets and Related Entities with Media Services .NET SDK</span><span class="sxs-lookup"><span data-stu-id="afdad-103">Managing Assets and Related Entities with Media Services .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-manage-entities.md)
> * [REST](media-services-rest-manage-entities.md)
> 
> 

<span data-ttu-id="afdad-106">This topic shows how to manage Azure Media Services entities with .NET.</span><span class="sxs-lookup"><span data-stu-id="afdad-106">This topic shows how to manage Azure Media Services entities with .NET.</span></span> 

>[!NOTE]
> Starting April 1, 2017, any Job record in your account older than 90 days will be automatically deleted, along with its associated Task records, even if the total number of records is below the maximum quota. For example, on April 1, 2017, any Job record in your account older than December 31, 2016, will be automatically deleted. If you need to archive the job/task information, you can use the code described in this topic.

## <a name="prerequisites"></a><span data-ttu-id="afdad-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="afdad-110">Prerequisites</span></span>

<span data-ttu-id="afdad-111">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="afdad-111">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="get-an-asset-reference"></a><span data-ttu-id="afdad-112">Get an Asset Reference</span><span class="sxs-lookup"><span data-stu-id="afdad-112">Get an Asset Reference</span></span>
<span data-ttu-id="afdad-113">A frequent task is to get a reference to an existing asset in Media Services.</span><span class="sxs-lookup"><span data-stu-id="afdad-113">A frequent task is to get a reference to an existing asset in Media Services.</span></span> <span data-ttu-id="afdad-114">The following code example shows how you can get an asset reference from the Assets collection on the server context object, based on an asset Id. The following code example uses a Linq query to get a reference to an existing IAsset object.</span><span class="sxs-lookup"><span data-stu-id="afdad-114">The following code example shows how you can get an asset reference from the Assets collection on the server context object, based on an asset Id. The following code example uses a Linq query to get a reference to an existing IAsset object.</span></span>

```csharp
    static IAsset GetAsset(string assetId)
    {
        // Use a LINQ Select query to get an asset.
        var assetInstance =
            from a in _context.Assets
            where a.Id == assetId
            select a;
        // Reference the asset as an IAsset.
        IAsset asset = assetInstance.FirstOrDefault();

        return asset;
    }
```

## <a name="list-all-assets"></a><span data-ttu-id="afdad-115">List All Assets</span><span class="sxs-lookup"><span data-stu-id="afdad-115">List All Assets</span></span>
<span data-ttu-id="afdad-116">As the number of assets you have in storage grows, it is helpful to list your assets.</span><span class="sxs-lookup"><span data-stu-id="afdad-116">As the number of assets you have in storage grows, it is helpful to list your assets.</span></span> <span data-ttu-id="afdad-117">The following code example shows how to iterate through the Assets collection on the server context object.</span><span class="sxs-lookup"><span data-stu-id="afdad-117">The following code example shows how to iterate through the Assets collection on the server context object.</span></span> <span data-ttu-id="afdad-118">With each asset, the code example also writes some of its property values to the console.</span><span class="sxs-lookup"><span data-stu-id="afdad-118">With each asset, the code example also writes some of its property values to the console.</span></span> <span data-ttu-id="afdad-119">For example, each asset can contain many media files.</span><span class="sxs-lookup"><span data-stu-id="afdad-119">For example, each asset can contain many media files.</span></span> <span data-ttu-id="afdad-120">The code example writes out all files associated with each asset.</span><span class="sxs-lookup"><span data-stu-id="afdad-120">The code example writes out all files associated with each asset.</span></span>

```csharp
    static void ListAssets()
    {
        string waitMessage = "Building the list. This may take a few "
            + "seconds to a few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder to store the list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IAsset asset in _context.Assets)
        {
            // Display the collection of assets.
            builder.AppendLine("");
            builder.AppendLine("******ASSET******");
            builder.AppendLine("Asset ID: " + asset.Id);
            builder.AppendLine("Name: " + asset.Name);
            builder.AppendLine("==============");
            builder.AppendLine("******ASSET FILES******");

            // Display the files associated with each asset. 
            foreach (IAssetFile fileItem in asset.AssetFiles)
            {
                builder.AppendLine("Name: " + fileItem.Name);
                builder.AppendLine("Size: " + fileItem.ContentFileSize);
                builder.AppendLine("==============");
            }
        }

        // Display output in console.
        Console.Write(builder.ToString());
    }
```

## <a name="get-a-job-reference"></a><span data-ttu-id="afdad-121">Get a Job Reference</span><span class="sxs-lookup"><span data-stu-id="afdad-121">Get a Job Reference</span></span>

<span data-ttu-id="afdad-122">When you work with processing tasks in Media Services code, you often need to get a reference to an existing job based on an Id. The following code example shows how to get a reference to an IJob object from the Jobs collection.</span><span class="sxs-lookup"><span data-stu-id="afdad-122">When you work with processing tasks in Media Services code, you often need to get a reference to an existing job based on an Id. The following code example shows how to get a reference to an IJob object from the Jobs collection.</span></span>

<span data-ttu-id="afdad-123">You may need to get a job reference when starting a long-running encoding job, and need to check the job status on a thread.</span><span class="sxs-lookup"><span data-stu-id="afdad-123">You may need to get a job reference when starting a long-running encoding job, and need to check the job status on a thread.</span></span> <span data-ttu-id="afdad-124">In cases like this, when the method returns from a thread, you need to retrieve a refreshed reference to a job.</span><span class="sxs-lookup"><span data-stu-id="afdad-124">In cases like this, when the method returns from a thread, you need to retrieve a refreshed reference to a job.</span></span>

```csharp
    static IJob GetJob(string jobId)
    {
        // Use a Linq select query to get an updated 
        // reference by Id. 
        var jobInstance =
            from j in _context.Jobs
            where j.Id == jobId
            select j;
        // Return the job reference as an Ijob. 
        IJob job = jobInstance.FirstOrDefault();

        return job;
    }
```

## <a name="list-jobs-and-assets"></a><span data-ttu-id="afdad-125">List Jobs and Assets</span><span class="sxs-lookup"><span data-stu-id="afdad-125">List Jobs and Assets</span></span>
<span data-ttu-id="afdad-126">An important related task is to list assets with their associated job in Media Services.</span><span class="sxs-lookup"><span data-stu-id="afdad-126">An important related task is to list assets with their associated job in Media Services.</span></span> <span data-ttu-id="afdad-127">The following code example shows you how to list each IJob object, and then for each job, it displays properties about the job, all related tasks, all input assets, and all output assets.</span><span class="sxs-lookup"><span data-stu-id="afdad-127">The following code example shows you how to list each IJob object, and then for each job, it displays properties about the job, all related tasks, all input assets, and all output assets.</span></span> <span data-ttu-id="afdad-128">The code in this example can be useful for numerous other tasks.</span><span class="sxs-lookup"><span data-stu-id="afdad-128">The code in this example can be useful for numerous other tasks.</span></span> <span data-ttu-id="afdad-129">For example, if you want to list the output assets from one or more encoding jobs that you ran previously, this code shows how to access the output assets.</span><span class="sxs-lookup"><span data-stu-id="afdad-129">For example, if you want to list the output assets from one or more encoding jobs that you ran previously, this code shows how to access the output assets.</span></span> <span data-ttu-id="afdad-130">When you have a reference to an output asset, you can then deliver the content to other users or applications by downloading it, or providing URLs.</span><span class="sxs-lookup"><span data-stu-id="afdad-130">When you have a reference to an output asset, you can then deliver the content to other users or applications by downloading it, or providing URLs.</span></span> 

<span data-ttu-id="afdad-131">For more information on options for delivering assets, see [Deliver Assets with the Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="afdad-131">For more information on options for delivering assets, see [Deliver Assets with the Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span></span>

```csharp
    // List all jobs on the server, and for each job, also list 
    // all tasks, all input assets, all output assets.

    static void ListJobsAndAssets()
    {
        string waitMessage = "Building the list. This may take a few "
            + "seconds to a few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder to store the list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IJob job in _context.Jobs)
        {
            // Display the collection of jobs on the server.
            builder.AppendLine("");
            builder.AppendLine("******JOB*******");
            builder.AppendLine("Job ID: " + job.Id);
            builder.AppendLine("Name: " + job.Name);
            builder.AppendLine("State: " + job.State);
            builder.AppendLine("Order: " + job.Priority);
            builder.AppendLine("==============");


            // For each job, display the associated tasks (a job  
            // has one or more tasks). 
            builder.AppendLine("******TASKS*******");
            foreach (ITask task in job.Tasks)
            {
                builder.AppendLine("Task Id: " + task.Id);
                builder.AppendLine("Name: " + task.Name);
                builder.AppendLine("Progress: " + task.Progress);
                builder.AppendLine("Configuration: " + task.Configuration);
                if (task.ErrorDetails != null)
                {
                    builder.AppendLine("Error: " + task.ErrorDetails);
                }
                builder.AppendLine("==============");
            }

            // For each job, display the list of input media assets.
            builder.AppendLine("******JOB INPUT MEDIA ASSETS*******");
            foreach (IAsset inputAsset in job.InputMediaAssets)
            {

                if (inputAsset != null)
                {
                    builder.AppendLine("Input Asset Id: " + inputAsset.Id);
                    builder.AppendLine("Name: " + inputAsset.Name);
                    builder.AppendLine("==============");
                }
            }

            // For each job, display the list of output media assets.
            builder.AppendLine("******JOB OUTPUT MEDIA ASSETS*******");
            foreach (IAsset theAsset in job.OutputMediaAssets)
            {
                if (theAsset != null)
                {
                    builder.AppendLine("Output Asset Id: " + theAsset.Id);
                    builder.AppendLine("Name: " + theAsset.Name);
                    builder.AppendLine("==============");
                }
            }

        }

        // Display output in console.
        Console.Write(builder.ToString());
    }
```

## <a name="list-all-access-policies"></a><span data-ttu-id="afdad-132">List all Access Policies</span><span class="sxs-lookup"><span data-stu-id="afdad-132">List all Access Policies</span></span>
<span data-ttu-id="afdad-133">In Media Services, you can define an access policy on an asset or its files.</span><span class="sxs-lookup"><span data-stu-id="afdad-133">In Media Services, you can define an access policy on an asset or its files.</span></span> <span data-ttu-id="afdad-134">An access policy defines the permissions for a file or an asset (what type of access, and the duration).</span><span class="sxs-lookup"><span data-stu-id="afdad-134">An access policy defines the permissions for a file or an asset (what type of access, and the duration).</span></span> <span data-ttu-id="afdad-135">In your Media Services code, you typically define an access policy by creating an IAccessPolicy object and then associating it with an existing asset.</span><span class="sxs-lookup"><span data-stu-id="afdad-135">In your Media Services code, you typically define an access policy by creating an IAccessPolicy object and then associating it with an existing asset.</span></span> <span data-ttu-id="afdad-136">Then you create a ILocator object, which lets you provide direct access to assets in Media Services.</span><span class="sxs-lookup"><span data-stu-id="afdad-136">Then you create a ILocator object, which lets you provide direct access to assets in Media Services.</span></span> <span data-ttu-id="afdad-137">The Visual Studio project that accompanies this documentation series contains several code examples that show how to create and assign access policies and locators to assets.</span><span class="sxs-lookup"><span data-stu-id="afdad-137">The Visual Studio project that accompanies this documentation series contains several code examples that show how to create and assign access policies and locators to assets.</span></span>

<span data-ttu-id="afdad-138">The following code example shows how to list all access policies on the server, and shows the type of permissions associated with each.</span><span class="sxs-lookup"><span data-stu-id="afdad-138">The following code example shows how to list all access policies on the server, and shows the type of permissions associated with each.</span></span> <span data-ttu-id="afdad-139">Another useful way to view access policies is to list all ILocator objects on the server, and then for each locator, you can list its associated access policy by using its AccessPolicy property.</span><span class="sxs-lookup"><span data-stu-id="afdad-139">Another useful way to view access policies is to list all ILocator objects on the server, and then for each locator, you can list its associated access policy by using its AccessPolicy property.</span></span>

```csharp
    static void ListAllPolicies()
    {
        foreach (IAccessPolicy policy in _context.AccessPolicies)
        {
            Console.WriteLine("");
            Console.WriteLine("Name:  " + policy.Name);
            Console.WriteLine("ID:  " + policy.Id);
            Console.WriteLine("Permissions: " + policy.Permissions);
            Console.WriteLine("==============");

        }
    }
```
    
## <a name="limit-access-policies"></a><span data-ttu-id="afdad-140">Limit Access Policies</span><span class="sxs-lookup"><span data-stu-id="afdad-140">Limit Access Policies</span></span> 

>[!NOTE]
> There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy). You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies). 

<span data-ttu-id="afdad-143">For example, you can create a generic set of policies with the following code that would only run one time in your application.</span><span class="sxs-lookup"><span data-stu-id="afdad-143">For example, you can create a generic set of policies with the following code that would only run one time in your application.</span></span> <span data-ttu-id="afdad-144">You can log IDs to a log file for later use:</span><span class="sxs-lookup"><span data-stu-id="afdad-144">You can log IDs to a log file for later use:</span></span>

```csharp
    double year = 365.25;
    double week = 7;
    IAccessPolicy policyYear = _context.AccessPolicies.Create("One Year", TimeSpan.FromDays(year), AccessPermissions.Read);
    IAccessPolicy policy100Year = _context.AccessPolicies.Create("Hundred Years", TimeSpan.FromDays(year * 100), AccessPermissions.Read);
    IAccessPolicy policyWeek = _context.AccessPolicies.Create("One Week", TimeSpan.FromDays(week), AccessPermissions.Read);

    Console.WriteLine("One year policy ID is: " + policyYear.Id);
    Console.WriteLine("100 year policy ID is: " + policy100Year.Id);
    Console.WriteLine("One week policy ID is: " + policyWeek.Id);
```

<span data-ttu-id="afdad-145">Then, you can use the existing IDs in your code like this:</span><span class="sxs-lookup"><span data-stu-id="afdad-145">Then, you can use the existing IDs in your code like this:</span></span>

```csharp
    const string policy1YearId = "nb:pid:UUID:2a4f0104-51a9-4078-ae26-c730f88d35cf";


    // Get the standard policy for 1 year read only
    var tempPolicyId = from b in _context.AccessPolicies
                       where b.Id == policy1YearId
                       select b;
    IAccessPolicy policy1Year = tempPolicyId.FirstOrDefault();

    // Get the existing asset
    var tempAsset = from a in _context.Assets
                where a.Id == assetID
                select a;
    IAsset asset = tempAsset.SingleOrDefault();

    ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
        policy1Year,
        DateTime.UtcNow.AddMinutes(-5));
    Console.WriteLine("The locator base path is " + originLocator.BaseUri.ToString());
```

## <a name="list-all-locators"></a><span data-ttu-id="afdad-146">List All Locators</span><span class="sxs-lookup"><span data-stu-id="afdad-146">List All Locators</span></span>
<span data-ttu-id="afdad-147">A locator is a URL that provides a direct path to access an asset, along with permissions to the asset as defined by the locator's associated access policy.</span><span class="sxs-lookup"><span data-stu-id="afdad-147">A locator is a URL that provides a direct path to access an asset, along with permissions to the asset as defined by the locator's associated access policy.</span></span> <span data-ttu-id="afdad-148">Each asset can have a collection of ILocator objects associated with it on its Locators property.</span><span class="sxs-lookup"><span data-stu-id="afdad-148">Each asset can have a collection of ILocator objects associated with it on its Locators property.</span></span> <span data-ttu-id="afdad-149">The server context also has a Locators collection that contains all locators.</span><span class="sxs-lookup"><span data-stu-id="afdad-149">The server context also has a Locators collection that contains all locators.</span></span>

<span data-ttu-id="afdad-150">The following code example lists all locators on the server.</span><span class="sxs-lookup"><span data-stu-id="afdad-150">The following code example lists all locators on the server.</span></span> <span data-ttu-id="afdad-151">For each locator, it shows the Id for the related asset and access policy.</span><span class="sxs-lookup"><span data-stu-id="afdad-151">For each locator, it shows the Id for the related asset and access policy.</span></span> <span data-ttu-id="afdad-152">It also displays the type of permissions, the expiration date, and the full path to the asset.</span><span class="sxs-lookup"><span data-stu-id="afdad-152">It also displays the type of permissions, the expiration date, and the full path to the asset.</span></span>

<span data-ttu-id="afdad-153">Note that a locator path to an asset is only a base URL to the asset.</span><span class="sxs-lookup"><span data-stu-id="afdad-153">Note that a locator path to an asset is only a base URL to the asset.</span></span> <span data-ttu-id="afdad-154">To create a direct path to individual files that a user or application could browse to, your code must add the specific file path to the locator path.</span><span class="sxs-lookup"><span data-stu-id="afdad-154">To create a direct path to individual files that a user or application could browse to, your code must add the specific file path to the locator path.</span></span> <span data-ttu-id="afdad-155">For more information on how to do this, see the topic [Deliver Assets with the Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="afdad-155">For more information on how to do this, see the topic [Deliver Assets with the Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span></span>

```csharp
    static void ListAllLocators()
    {
        foreach (ILocator locator in _context.Locators)
        {
            Console.WriteLine("***********");
            Console.WriteLine("Locator Id: " + locator.Id);
            Console.WriteLine("Locator asset Id: " + locator.AssetId);
            Console.WriteLine("Locator access policy Id: " + locator.AccessPolicyId);
            Console.WriteLine("Access policy permissions: " + locator.AccessPolicy.Permissions);
            Console.WriteLine("Locator expiration: " + locator.ExpirationDateTime);
            // The locator path is the base or parent path (with included permissions) to access  
            // the media content of an asset. To create a full URL to a specific media file, take 
            // the locator path and then append a file name and info as needed.  
            Console.WriteLine("Locator base path: " + locator.Path);
            Console.WriteLine("");
        }
    }
```

## <a name="enumerating-through-large-collections-of-entities"></a><span data-ttu-id="afdad-156">Enumerating through large collections of entities</span><span class="sxs-lookup"><span data-stu-id="afdad-156">Enumerating through large collections of entities</span></span>
<span data-ttu-id="afdad-157">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results to 1000 results.</span><span class="sxs-lookup"><span data-stu-id="afdad-157">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results to 1000 results.</span></span> <span data-ttu-id="afdad-158">You need to use Skip and Take when enumerating through large collections of entities.</span><span class="sxs-lookup"><span data-stu-id="afdad-158">You need to use Skip and Take when enumerating through large collections of entities.</span></span> 

<span data-ttu-id="afdad-159">The following function loops through all the jobs in the provided Media Services Account.</span><span class="sxs-lookup"><span data-stu-id="afdad-159">The following function loops through all the jobs in the provided Media Services Account.</span></span> <span data-ttu-id="afdad-160">Media Services returns 1000 jobs in Jobs Collection.</span><span class="sxs-lookup"><span data-stu-id="afdad-160">Media Services returns 1000 jobs in Jobs Collection.</span></span> <span data-ttu-id="afdad-161">The function makes use of Skip and Take to make sure that all jobs are enumerated (in case you have more than 1000 jobs in your account).</span><span class="sxs-lookup"><span data-stu-id="afdad-161">The function makes use of Skip and Take to make sure that all jobs are enumerated (in case you have more than 1000 jobs in your account).</span></span>

```csharp
    static void ProcessJobs()
    {
        try
        {

            int skipSize = 0;
            int batchSize = 1000;
            int currentBatch = 0;

            while (true)
            {
                // Loop through all Jobs (1000 at a time) in the Media Services account
                IQueryable _jobsCollectionQuery = _context.Jobs.Skip(skipSize).Take(batchSize);
                foreach (IJob job in _jobsCollectionQuery)
                {
                    currentBatch++;
                    Console.WriteLine("Processing Job Id:" + job.Id);
                }

                if (currentBatch == batchSize)
                {
                    skipSize += batchSize;
                    currentBatch = 0;
                }
                else
                {
                    break;
                }
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }
    }
```

## <a name="delete-an-asset"></a><span data-ttu-id="afdad-162">Delete an Asset</span><span class="sxs-lookup"><span data-stu-id="afdad-162">Delete an Asset</span></span>
<span data-ttu-id="afdad-163">The following example deletes an asset.</span><span class="sxs-lookup"><span data-stu-id="afdad-163">The following example deletes an asset.</span></span>

```csharp
    static void DeleteAsset( IAsset asset)
    {
        // delete the asset
        asset.Delete();

        // Verify asset deletion
        if (GetAsset(asset.Id) == null)
            Console.WriteLine("Deleted the Asset");

    }
```

## <a name="delete-a-job"></a><span data-ttu-id="afdad-164">Delete a Job</span><span class="sxs-lookup"><span data-stu-id="afdad-164">Delete a Job</span></span>
<span data-ttu-id="afdad-165">To delete a job, you must check the state of the job as indicated in the State property.</span><span class="sxs-lookup"><span data-stu-id="afdad-165">To delete a job, you must check the state of the job as indicated in the State property.</span></span> <span data-ttu-id="afdad-166">Jobs that are finished or canceled can be deleted, while jobs that are in certain other states, such as queued, scheduled, or processing, must be canceled first, and then they can be deleted.</span><span class="sxs-lookup"><span data-stu-id="afdad-166">Jobs that are finished or canceled can be deleted, while jobs that are in certain other states, such as queued, scheduled, or processing, must be canceled first, and then they can be deleted.</span></span>

<span data-ttu-id="afdad-167">The following code example shows a method for deleting a job by checking job states and then deleting when the state is finished or canceled.</span><span class="sxs-lookup"><span data-stu-id="afdad-167">The following code example shows a method for deleting a job by checking job states and then deleting when the state is finished or canceled.</span></span> <span data-ttu-id="afdad-168">This code depends on the previous section in this topic for getting a reference to a job: Get a job reference.</span><span class="sxs-lookup"><span data-stu-id="afdad-168">This code depends on the previous section in this topic for getting a reference to a job: Get a job reference.</span></span>

```csharp
    static void DeleteJob(string jobId)
    {
        bool jobDeleted = false;

        while (!jobDeleted)
        {
            // Get an updated job reference.  
            IJob job = GetJob(jobId);

            // Check and handle various possible job states. You can 
            // only delete a job whose state is Finished, Error, or Canceled.   
            // You can cancel jobs that are Queued, Scheduled, or Processing,  
            // and then delete after they are canceled.
            switch (job.State)
            {
                case JobState.Finished:
                case JobState.Canceled:
                case JobState.Error:
                    // Job errors should already be logged by polling or event 
                    // handling methods such as CheckJobProgress or StateChanged.
                    // You can also call job.DeleteAsync to do async deletes.
                    job.Delete();
                    Console.WriteLine("Job has been deleted.");
                    jobDeleted = true;
                    break;
                case JobState.Canceling:
                    Console.WriteLine("Job is cancelling and will be deleted "
                        + "when finished.");
                    Console.WriteLine("Wait while job finishes canceling...");
                    Thread.Sleep(5000);
                    break;
                case JobState.Queued:
                case JobState.Scheduled:
                case JobState.Processing:
                    job.Cancel();
                    Console.WriteLine("Job is scheduled or processing and will "
                        + "be deleted.");
                    break;
                default:
                    break;
            }

        }
    }
```


## <a name="delete-an-access-policy"></a><span data-ttu-id="afdad-169">Delete an Access Policy</span><span class="sxs-lookup"><span data-stu-id="afdad-169">Delete an Access Policy</span></span>
<span data-ttu-id="afdad-170">The following code example shows how to get a reference to an access policy based on a policy Id, and then to delete the policy.</span><span class="sxs-lookup"><span data-stu-id="afdad-170">The following code example shows how to get a reference to an access policy based on a policy Id, and then to delete the policy.</span></span>

```csharp
    static void DeleteAccessPolicy(string existingPolicyId)
    {
        // To delete a specific access policy, get a reference to the policy.  
        // based on the policy Id passed to the method.
        var policyInstance =
                from p in _context.AccessPolicies
                where p.Id == existingPolicyId
                select p;
        IAccessPolicy policy = policyInstance.FirstOrDefault();

        policy.Delete();

    }
```


## <a name="media-services-learning-paths"></a><span data-ttu-id="afdad-171">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="afdad-171">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="afdad-172">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="afdad-172">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

