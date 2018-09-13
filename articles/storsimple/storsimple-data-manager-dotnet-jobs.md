---
title: Use .NET SDK for Microsoft Azure StorSimple Data Manager jobs | Microsoft Docs
description: Learn how to use .NET SDK to launch StorSimple Data Manager jobs (private preview)
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: ''
ms.assetid: ''
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: 60cde851a466a5b4b0752908f11272eedb246b0a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552678"
---
# <a name="use-the-net-sdk-to-initiate-data-transformation-private-preview"></a><span data-ttu-id="1e4e5-103">Use the .Net SDK to initiate data transformation (Private Preview)</span><span class="sxs-lookup"><span data-stu-id="1e4e5-103">Use the .Net SDK to initiate data transformation (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="1e4e5-104">Overview</span><span class="sxs-lookup"><span data-stu-id="1e4e5-104">Overview</span></span>

<span data-ttu-id="1e4e5-105">This article explains how you can use the data transformation feature within the StorSimple Data Manager service to transform StorSimple device data.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-105">This article explains how you can use the data transformation feature within the StorSimple Data Manager service to transform StorSimple device data.</span></span> <span data-ttu-id="1e4e5-106">The transformed data is then consumed by other Azure services in the cloud.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-106">The transformed data is then consumed by other Azure services in the cloud.</span></span> <span data-ttu-id="1e4e5-107">The article also has a walkthrough to help create a sample .NET console application to initiate a data transformation job and then track it for completion.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-107">The article also has a walkthrough to help create a sample .NET console application to initiate a data transformation job and then track it for completion.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e4e5-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1e4e5-108">Prerequisites</span></span>

<span data-ttu-id="1e4e5-109">Before you begin, ensure that you have:</span><span class="sxs-lookup"><span data-stu-id="1e4e5-109">Before you begin, ensure that you have:</span></span>
*   <span data-ttu-id="1e4e5-110">A system with Visual Studio 2012, 2013, or 2015 installed.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-110">A system with Visual Studio 2012, 2013, or 2015 installed.</span></span>
*   <span data-ttu-id="1e4e5-111">Azure Powershell installed.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-111">Azure Powershell installed.</span></span> <span data-ttu-id="1e4e5-112">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="1e4e5-112">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="1e4e5-113">Configuration settings to initialize the Data Transformation job (instructions to obtain these settings are included here).</span><span class="sxs-lookup"><span data-stu-id="1e4e5-113">Configuration settings to initialize the Data Transformation job (instructions to obtain these settings are included here).</span></span>
*   <span data-ttu-id="1e4e5-114">A job definition that has been correctly configured in a Hybrid Data Resource within a Resource Group.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-114">A job definition that has been correctly configured in a Hybrid Data Resource within a Resource Group.</span></span>
*   <span data-ttu-id="1e4e5-115">All the required dlls.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-115">All the required dlls.</span></span> <span data-ttu-id="1e4e5-116">Download these dlls from the [GitHub repository](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).</span><span class="sxs-lookup"><span data-stu-id="1e4e5-116">Download these dlls from the [GitHub repository](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).</span></span>
*   <span data-ttu-id="1e4e5-117">`Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) from the github repository.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-117">`Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) from the github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="1e4e5-118">Step-by-step</span><span class="sxs-lookup"><span data-stu-id="1e4e5-118">Step-by-step</span></span>

<span data-ttu-id="1e4e5-119">Perform the following steps to use .NET to launch a data transformation job.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-119">Perform the following steps to use .NET to launch a data transformation job.</span></span>

1. <span data-ttu-id="1e4e5-120">To retrieve the configuration parameters, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="1e4e5-120">To retrieve the configuration parameters, do the following steps:</span></span>
    1. <span data-ttu-id="1e4e5-121">Download the `Get-ConfigurationParams.ps1` from the github repository script in `C:\DataTransformation` location.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-121">Download the `Get-ConfigurationParams.ps1` from the github repository script in `C:\DataTransformation` location.</span></span>
    1. <span data-ttu-id="1e4e5-122">Run the `Get-ConfigurationParams.ps1` script from the github repository.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-122">Run the `Get-ConfigurationParams.ps1` script from the github repository.</span></span> <span data-ttu-id="1e4e5-123">Type the following command:</span><span class="sxs-lookup"><span data-stu-id="1e4e5-123">Type the following command:</span></span>

        ```
        C:\DataTransformation\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```
        <span data-ttu-id="1e4e5-124">You can pass in any values for the ActiveDirectoryKey and AppName.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-124">You can pass in any values for the ActiveDirectoryKey and AppName.</span></span>


2. <span data-ttu-id="1e4e5-125">This script outputs the following values:      - Client ID      - Tenant ID      - Active Directory key (same as the one entered above)      - Subscription ID</span><span class="sxs-lookup"><span data-stu-id="1e4e5-125">This script outputs the following values:      - Client ID      - Tenant ID      - Active Directory key (same as the one entered above)      - Subscription ID</span></span>

3. <span data-ttu-id="1e4e5-126">Using Visual Studio 2012, 2013 or 2015, create a C# .NET console application.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-126">Using Visual Studio 2012, 2013 or 2015, create a C# .NET console application.</span></span>

    1. <span data-ttu-id="1e4e5-127">Launch **Visual Studio 2012/2013/2015**.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-127">Launch **Visual Studio 2012/2013/2015**.</span></span>
    1. <span data-ttu-id="1e4e5-128">Click **File**, point to **New**, and click **Project**.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-128">Click **File**, point to **New**, and click **Project**.</span></span>
    2. <span data-ttu-id="1e4e5-129">Expand **Templates**, and select **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-129">Expand **Templates**, and select **Visual C#**.</span></span>
    3. <span data-ttu-id="1e4e5-130">Select **Console Application** from the list of project types on the right.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-130">Select **Console Application** from the list of project types on the right.</span></span>
    4. <span data-ttu-id="1e4e5-131">Enter **DataTransformationApp** for the **Name**.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-131">Enter **DataTransformationApp** for the **Name**.</span></span>
    5. <span data-ttu-id="1e4e5-132">Select **C:\DataTransformation** for the **Location**.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-132">Select **C:\DataTransformation** for the **Location**.</span></span>
    6. <span data-ttu-id="1e4e5-133">Click **OK** to create the project.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-133">Click **OK** to create the project.</span></span>

4.  <span data-ttu-id="1e4e5-134">Now, add all DLLs present in the [dlls](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) folder as **References** in the project that you created.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-134">Now, add all DLLs present in the [dlls](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) folder as **References** in the project that you created.</span></span> <span data-ttu-id="1e4e5-135">To download the dll files, do the following:</span><span class="sxs-lookup"><span data-stu-id="1e4e5-135">To download the dll files, do the following:</span></span>

    1. <span data-ttu-id="1e4e5-136">In Visual Studio, go to **View > Solution Explorer**.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-136">In Visual Studio, go to **View > Solution Explorer**.</span></span>
    1. <span data-ttu-id="1e4e5-137">Click the arrow to the left of Data Transformation App project.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-137">Click the arrow to the left of Data Transformation App project.</span></span> <span data-ttu-id="1e4e5-138">Click **References** and then right-click to **Add Reference**.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-138">Click **References** and then right-click to **Add Reference**.</span></span>
    2. <span data-ttu-id="1e4e5-139">Browse to the location of the packages folder, select all the DLLs and click **Add**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-139">Browse to the location of the packages folder, select all the DLLs and click **Add**, and then click **OK**.</span></span>

5. <span data-ttu-id="1e4e5-140">Add the following **using** statements to the source file (Program.cs) in the project.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-140">Add the following **using** statements to the source file (Program.cs) in the project.</span></span>

    ```
    using System;
    using System.Collections.Generic;
    using System.Threading;
    using Microsoft.Azure.Management.HybridData.Models;
    using Microsoft.Internal.Dms.DmsWebJob;
    using Microsoft.Internal.Dms.DmsWebJob.Contracts;
    ```


6. <span data-ttu-id="1e4e5-141">The following code initializes the data transformation job instance.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-141">The following code initializes the data transformation job instance.</span></span> <span data-ttu-id="1e4e5-142">Add this in the **Main method**.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-142">Add this in the **Main method**.</span></span> <span data-ttu-id="1e4e5-143">Replace the values of configuration parameters as obtained earlier.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-143">Replace the values of configuration parameters as obtained earlier.</span></span> <span data-ttu-id="1e4e5-144">Plug in the values of **Resource Group Name** and **Hybrid Data Resource name**.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-144">Plug in the values of **Resource Group Name** and **Hybrid Data Resource name**.</span></span> <span data-ttu-id="1e4e5-145">The **Resource Group Name** is the one that hosts the Hybrid Data Resource on which the job definition was configured.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-145">The **Resource Group Name** is the one that hosts the Hybrid Data Resource on which the job definition was configured.</span></span>

    ```
    // Setup the configuration parameters.
    var configParams = new ConfigurationParams
    {
        ClientId = "client-id",
        TenantId = "tenant-id",
        ActiveDirectoryKey = "active-directory-key",
        SubscriptionId = "subscription-id",
        ResourceGroupName = "resource-group-name",
        ResourceName = "resource-name"
    };

    // Initialize the Data Transformation Job instance.
    DataTransformationJob dataTransformationJob = new DataTransformationJob(configParams);

    ```

7. <span data-ttu-id="1e4e5-146">Specify the parameters with which the job definition needs to be run</span><span class="sxs-lookup"><span data-stu-id="1e4e5-146">Specify the parameters with which the job definition needs to be run</span></span>

    ```
    string jobDefinitionName = "job-definition-name";

    DataTransformationInput dataTransformationInput = dataTransformationJob.GetJobDefinitionParameters(jobDefinitionName);

    ```

    <span data-ttu-id="1e4e5-147">(OR)</span><span class="sxs-lookup"><span data-stu-id="1e4e5-147">(OR)</span></span>

    <span data-ttu-id="1e4e5-148">If you want to change the job definition parameters during run time, then add the following code:</span><span class="sxs-lookup"><span data-stu-id="1e4e5-148">If you want to change the job definition parameters during run time, then add the following code:</span></span>

    ```
    string jobDefinitionName = "job-definition-name";
    // Must start with a '\'
    var rootDirectories = new List<string> {@"\root"};

    // Name of the volume on the StorSimple device.
    var volumeNames = new List<string> {"volume-name"};

    var dataTransformationInput = new DataTransformationInput
    {
        // If you require the latest existing backup to be picked else use TakeNow to trigger a new backup.
        BackupChoice = BackupChoice.UseExistingLatest.ToString(),
        // Name of the StorSimple device.
        DeviceName = "device-name",
        // Name of the container in Azure storage where the files will be placed after execution.
        ContainerName = "container-name",
        // File name filter (search pattern) to be applied on files under the root directory. * - Match all files.
        FileNameFilter = "*",
        // List of root directories.
        RootDirectories = rootDirectories,
        // Name of the volume on StorSimple device on which the relevant data is present. 
        VolumeNames = volumeNames
    };
    
    ```

8. <span data-ttu-id="1e4e5-149">After the initialization, add the following code to trigger a data transformation job on the job definition.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-149">After the initialization, add the following code to trigger a data transformation job on the job definition.</span></span> <span data-ttu-id="1e4e5-150">Plug in the appropriate **Job Definition Name**.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-150">Plug in the appropriate **Job Definition Name**.</span></span>

    ```
    // Trigger a job, retrieve the jobId and the retry interval for polling.
    int retryAfter;
    string jobId = dataTransformationJob.RunJobAsync(jobDefinitionName, 
    dataTransformationInput, out retryAfter);

    ```

9. <span data-ttu-id="1e4e5-151">This job uploads the matched files present under the root directory on the StorSimple volume to the specified container.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-151">This job uploads the matched files present under the root directory on the StorSimple volume to the specified container.</span></span> <span data-ttu-id="1e4e5-152">When a file is uploaded, a message is dropped in the queue (in the same storage account as the container) with the same name as the job definition.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-152">When a file is uploaded, a message is dropped in the queue (in the same storage account as the container) with the same name as the job definition.</span></span> <span data-ttu-id="1e4e5-153">This message can be used as a trigger to initiate any further processing of the file.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-153">This message can be used as a trigger to initiate any further processing of the file.</span></span>

10. <span data-ttu-id="1e4e5-154">Once the job has been triggered, add the following code to track the job for completion.</span><span class="sxs-lookup"><span data-stu-id="1e4e5-154">Once the job has been triggered, add the following code to track the job for completion.</span></span>

    ```
    Job jobDetails = null;

    // Poll the job.
    do
    {
        jobDetails = dataTransformationJob.GetJob(jobDefinitionName, jobId);

        // Wait before polling for the status again.
        Thread.Sleep(TimeSpan.FromSeconds(retryAfter));

    } while (jobDetails.Status == JobStatus.InProgress);

    // Completion status of the job.
    Console.WriteLine("JobStatus: {0}", jobDetails.Status);
    
    // To hold the console before exiting.
    Console.Read();

    ```


## <a name="next-steps"></a><span data-ttu-id="1e4e5-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="1e4e5-155">Next steps</span></span>

<span data-ttu-id="1e4e5-156">[Use StorSimple Data Manager UI to transform your data](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="1e4e5-156">[Use StorSimple Data Manager UI to transform your data](storsimple-data-manager-ui.md).</span></span>
