---
title: Microsoft Azure StorSimple Data Manager UI | Microsoft Docs
description: Describes how to use StorSimple Data Manager serivce UI (private preview)
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
ms.openlocfilehash: 264f2345a34bf42232286b1e584b0c14738af2ec
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554151"
---
# <a name="manage-using-the-storsimple-data-manager-service-ui-private-preview"></a><span data-ttu-id="a22bc-103">Manage using the StorSimple Data Manager service UI (Private Preview)</span><span class="sxs-lookup"><span data-stu-id="a22bc-103">Manage using the StorSimple Data Manager service UI (Private Preview)</span></span>

<span data-ttu-id="a22bc-104">This article explains how you can use the StorSimple Data Manager UI to perform data transformation on data residing on the StorSimple 8000 series devices.</span><span class="sxs-lookup"><span data-stu-id="a22bc-104">This article explains how you can use the StorSimple Data Manager UI to perform data transformation on data residing on the StorSimple 8000 series devices.</span></span> <span data-ttu-id="a22bc-105">The transformed data can then be consumed by other Azure services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search.</span><span class="sxs-lookup"><span data-stu-id="a22bc-105">The transformed data can then be consumed by other Azure services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search.</span></span> 


## <a name="use-storsimple-data-transformation"></a><span data-ttu-id="a22bc-106">Use StorSimple Data Transformation</span><span class="sxs-lookup"><span data-stu-id="a22bc-106">Use StorSimple Data Transformation</span></span>

<span data-ttu-id="a22bc-107">The StorSimple Data Manager is the resource within which Data Transformation can be instantiated.</span><span class="sxs-lookup"><span data-stu-id="a22bc-107">The StorSimple Data Manager is the resource within which Data Transformation can be instantiated.</span></span> <span data-ttu-id="a22bc-108">The Data Transformation service lets you move data from your StorSimple on-premises device to blobs in Azure storage.</span><span class="sxs-lookup"><span data-stu-id="a22bc-108">The Data Transformation service lets you move data from your StorSimple on-premises device to blobs in Azure storage.</span></span> <span data-ttu-id="a22bc-109">Hence, in workflow you need to specify the details about your StorSimple device and the data of interest that you want to move to the storage account.</span><span class="sxs-lookup"><span data-stu-id="a22bc-109">Hence, in workflow you need to specify the details about your StorSimple device and the data of interest that you want to move to the storage account.</span></span>

### <a name="create-a-storsimple-data-manager-service"></a><span data-ttu-id="a22bc-110">Create a StorSimple Data Manager service</span><span class="sxs-lookup"><span data-stu-id="a22bc-110">Create a StorSimple Data Manager service</span></span>

<span data-ttu-id="a22bc-111">Perform the following steps to create a StorSimple Data Manager service.</span><span class="sxs-lookup"><span data-stu-id="a22bc-111">Perform the following steps to create a StorSimple Data Manager service.</span></span>

1. <span data-ttu-id="a22bc-112">To create a StorSimple Data Manager service, go to [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)</span><span class="sxs-lookup"><span data-stu-id="a22bc-112">To create a StorSimple Data Manager service, go to [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)</span></span>

2. <span data-ttu-id="a22bc-113">Click the **+** icon and search for StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="a22bc-113">Click the **+** icon and search for StorSimple Data Manager.</span></span> <span data-ttu-id="a22bc-114">Click your StorSimple Data Manager service and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a22bc-114">Click your StorSimple Data Manager service and then click **Create**.</span></span>

3. <span data-ttu-id="a22bc-115">If your subscription is enabled for creating this service, you see the following blade.</span><span class="sxs-lookup"><span data-stu-id="a22bc-115">If your subscription is enabled for creating this service, you see the following blade.</span></span>

    ![Create a StorSimple Data Managers resource](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-data-manager-ui/create-new-data-manager-service.png)

4. <span data-ttu-id="a22bc-117">Enter the inputs and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a22bc-117">Enter the inputs and click **Create**.</span></span> <span data-ttu-id="a22bc-118">The specified location should be the one that houses your storage accounts and your StorSimple Manager service.</span><span class="sxs-lookup"><span data-stu-id="a22bc-118">The specified location should be the one that houses your storage accounts and your StorSimple Manager service.</span></span> <span data-ttu-id="a22bc-119">Currently, only West US and West Europe regions are supported.</span><span class="sxs-lookup"><span data-stu-id="a22bc-119">Currently, only West US and West Europe regions are supported.</span></span> <span data-ttu-id="a22bc-120">Hence, your StorSimple Manager service, Data Manager service, and the associated storage account should all be in the preceding supported regions.</span><span class="sxs-lookup"><span data-stu-id="a22bc-120">Hence, your StorSimple Manager service, Data Manager service, and the associated storage account should all be in the preceding supported regions.</span></span> <span data-ttu-id="a22bc-121">It takes about a minute to create the service.</span><span class="sxs-lookup"><span data-stu-id="a22bc-121">It takes about a minute to create the service.</span></span>

### <a name="create-a-data-transformation-job-definition"></a><span data-ttu-id="a22bc-122">Create a data transformation job definition</span><span class="sxs-lookup"><span data-stu-id="a22bc-122">Create a data transformation job definition</span></span>

<span data-ttu-id="a22bc-123">Within a StorSimple Data Manager service, you need to create a data transformation job definition.</span><span class="sxs-lookup"><span data-stu-id="a22bc-123">Within a StorSimple Data Manager service, you need to create a data transformation job definition.</span></span> <span data-ttu-id="a22bc-124">A job definition specifies details of the data that you are interested in moving into a storage account in the native format.</span><span class="sxs-lookup"><span data-stu-id="a22bc-124">A job definition specifies details of the data that you are interested in moving into a storage account in the native format.</span></span> 

<span data-ttu-id="a22bc-125">Perform the following steps to create a new data transformation job definition.</span><span class="sxs-lookup"><span data-stu-id="a22bc-125">Perform the following steps to create a new data transformation job definition.</span></span>

1.  <span data-ttu-id="a22bc-126">Navigate to the service that you created.</span><span class="sxs-lookup"><span data-stu-id="a22bc-126">Navigate to the service that you created.</span></span> <span data-ttu-id="a22bc-127">Click **+ Job Definition**.</span><span class="sxs-lookup"><span data-stu-id="a22bc-127">Click **+ Job Definition**.</span></span>

    ![Click +Job Definition](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-data-manager-ui/click-add-job-definition.png)

2. <span data-ttu-id="a22bc-129">The new job definition blade opens up.</span><span class="sxs-lookup"><span data-stu-id="a22bc-129">The new job definition blade opens up.</span></span> <span data-ttu-id="a22bc-130">Give your job definition a name and click **Source**.</span><span class="sxs-lookup"><span data-stu-id="a22bc-130">Give your job definition a name and click **Source**.</span></span> <span data-ttu-id="a22bc-131">In the **Configure data source** blade, specify the details of your StorSimple device and the data of interest.</span><span class="sxs-lookup"><span data-stu-id="a22bc-131">In the **Configure data source** blade, specify the details of your StorSimple device and the data of interest.</span></span>

    ![Create job definition](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-data-manager-ui/create-new-job-deifnition.png)

3. <span data-ttu-id="a22bc-133">Since this is a new Data Manager service, no data repositories are configured.</span><span class="sxs-lookup"><span data-stu-id="a22bc-133">Since this is a new Data Manager service, no data repositories are configured.</span></span> <span data-ttu-id="a22bc-134">To add your StorSimple Manager as a data repository, click **Add new** in the data repository dropdown and then click **Add Data Repository**.</span><span class="sxs-lookup"><span data-stu-id="a22bc-134">To add your StorSimple Manager as a data repository, click **Add new** in the data repository dropdown and then click **Add Data Repository**.</span></span>

4. <span data-ttu-id="a22bc-135">Choose **StorSimple 8000 series Manager** as the repository type and enter the properties of your **StorSimple Manager**.</span><span class="sxs-lookup"><span data-stu-id="a22bc-135">Choose **StorSimple 8000 series Manager** as the repository type and enter the properties of your **StorSimple Manager**.</span></span> <span data-ttu-id="a22bc-136">For the **Resource Id** field, you need to enter the number before the **:** in the registration key of your StorSimple manager.</span><span class="sxs-lookup"><span data-stu-id="a22bc-136">For the **Resource Id** field, you need to enter the number before the **:** in the registration key of your StorSimple manager.</span></span>

    ![Create data source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-data-manager-ui/create-new-data-source.png)

5.  <span data-ttu-id="a22bc-138">Click **OK** when done.</span><span class="sxs-lookup"><span data-stu-id="a22bc-138">Click **OK** when done.</span></span> <span data-ttu-id="a22bc-139">This saves your data repository and this StorSimple Manager can be reused in other job definitions without entering these parameters again.</span><span class="sxs-lookup"><span data-stu-id="a22bc-139">This saves your data repository and this StorSimple Manager can be reused in other job definitions without entering these parameters again.</span></span> <span data-ttu-id="a22bc-140">It takes a few seconds after you click **OK** for the StorSimple Manager to show up in the dropdown.</span><span class="sxs-lookup"><span data-stu-id="a22bc-140">It takes a few seconds after you click **OK** for the StorSimple Manager to show up in the dropdown.</span></span>

6.  <span data-ttu-id="a22bc-141">In the **Configure data source** blade, enter the device name and the volume name that has your data of interest.</span><span class="sxs-lookup"><span data-stu-id="a22bc-141">In the **Configure data source** blade, enter the device name and the volume name that has your data of interest.</span></span>

7.  <span data-ttu-id="a22bc-142">In the **Filter** subsection, enter the root directory that contains your data of interest (this field should start with a `\`).</span><span class="sxs-lookup"><span data-stu-id="a22bc-142">In the **Filter** subsection, enter the root directory that contains your data of interest (this field should start with a `\`).</span></span> <span data-ttu-id="a22bc-143">You can also add any file filters here.</span><span class="sxs-lookup"><span data-stu-id="a22bc-143">You can also add any file filters here.</span></span>

8.  <span data-ttu-id="a22bc-144">The data transformation service works on the data that is pushed up to the Azure via snapshots.</span><span class="sxs-lookup"><span data-stu-id="a22bc-144">The data transformation service works on the data that is pushed up to the Azure via snapshots.</span></span> <span data-ttu-id="a22bc-145">When running this job, you can choose to take a backup every time this job is run (to work on latest data) or to use the last existing backup in the cloud (if you are working on some archived data).</span><span class="sxs-lookup"><span data-stu-id="a22bc-145">When running this job, you can choose to take a backup every time this job is run (to work on latest data) or to use the last existing backup in the cloud (if you are working on some archived data).</span></span>

    ![New data source details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-data-manager-ui/new-data-source-details.png)

9. <span data-ttu-id="a22bc-147">Next, the Target settings need to be configured.</span><span class="sxs-lookup"><span data-stu-id="a22bc-147">Next, the Target settings need to be configured.</span></span> <span data-ttu-id="a22bc-148">There are 2 types of supported targets – Azure Storage accounts and Azure Media Services accounts.</span><span class="sxs-lookup"><span data-stu-id="a22bc-148">There are 2 types of supported targets – Azure Storage accounts and Azure Media Services accounts.</span></span> <span data-ttu-id="a22bc-149">Choose storage accounts to put files into blobs in that account.</span><span class="sxs-lookup"><span data-stu-id="a22bc-149">Choose storage accounts to put files into blobs in that account.</span></span> <span data-ttu-id="a22bc-150">Choose media services account to put files into assets in that account.</span><span class="sxs-lookup"><span data-stu-id="a22bc-150">Choose media services account to put files into assets in that account.</span></span> <span data-ttu-id="a22bc-151">Again, we need to add a repository.</span><span class="sxs-lookup"><span data-stu-id="a22bc-151">Again, we need to add a repository.</span></span> <span data-ttu-id="a22bc-152">In the dropdown, select **Add new** and then **Configure settings**.</span><span class="sxs-lookup"><span data-stu-id="a22bc-152">In the dropdown, select **Add new** and then **Configure settings**.</span></span>

    ![Create data sink](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-data-manager-ui/create-new-data-sink.png)

10. <span data-ttu-id="a22bc-154">Here, you can select the type of repository you want to add and the other parameters associated with the repository.</span><span class="sxs-lookup"><span data-stu-id="a22bc-154">Here, you can select the type of repository you want to add and the other parameters associated with the repository.</span></span> <span data-ttu-id="a22bc-155">In both cases, a storage queue is created when the job runs.</span><span class="sxs-lookup"><span data-stu-id="a22bc-155">In both cases, a storage queue is created when the job runs.</span></span> <span data-ttu-id="a22bc-156">This queue is populated with messages about transformed blobs as they are ready.</span><span class="sxs-lookup"><span data-stu-id="a22bc-156">This queue is populated with messages about transformed blobs as they are ready.</span></span> <span data-ttu-id="a22bc-157">The name of this queue is the same as the name of the job definition.</span><span class="sxs-lookup"><span data-stu-id="a22bc-157">The name of this queue is the same as the name of the job definition.</span></span> <span data-ttu-id="a22bc-158">If you select **Media Services** as the repo type, then you can also enter storage account credentials where the queue is created.</span><span class="sxs-lookup"><span data-stu-id="a22bc-158">If you select **Media Services** as the repo type, then you can also enter storage account credentials where the queue is created.</span></span>

    ![New data sink details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-data-manager-ui/new-data-sink-details.png)

11. <span data-ttu-id="a22bc-160">After adding the data repository (which takes a few seconds), you will find the repo in the dropdown in the **Target account name**.</span><span class="sxs-lookup"><span data-stu-id="a22bc-160">After adding the data repository (which takes a few seconds), you will find the repo in the dropdown in the **Target account name**.</span></span>  <span data-ttu-id="a22bc-161">Choose the target that you need.</span><span class="sxs-lookup"><span data-stu-id="a22bc-161">Choose the target that you need.</span></span>

12. <span data-ttu-id="a22bc-162">Click **OK** to create the job definition.</span><span class="sxs-lookup"><span data-stu-id="a22bc-162">Click **OK** to create the job definition.</span></span> <span data-ttu-id="a22bc-163">Your job definition is now set up.</span><span class="sxs-lookup"><span data-stu-id="a22bc-163">Your job definition is now set up.</span></span> <span data-ttu-id="a22bc-164">You can use this job definition multiple times via the UI.</span><span class="sxs-lookup"><span data-stu-id="a22bc-164">You can use this job definition multiple times via the UI.</span></span>

    ![Add new job definition](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-data-manager-ui/add-new-job-definition.png)

### <a name="run-the-job-definition"></a><span data-ttu-id="a22bc-166">Run the job definition</span><span class="sxs-lookup"><span data-stu-id="a22bc-166">Run the job definition</span></span>

<span data-ttu-id="a22bc-167">Whenever you need to move data from StorSimple to the storage account that you have specified in the job definition, you will need to invoke it.</span><span class="sxs-lookup"><span data-stu-id="a22bc-167">Whenever you need to move data from StorSimple to the storage account that you have specified in the job definition, you will need to invoke it.</span></span> <span data-ttu-id="a22bc-168">There is some flexibility in changing the parameters every time you invoke the job.</span><span class="sxs-lookup"><span data-stu-id="a22bc-168">There is some flexibility in changing the parameters every time you invoke the job.</span></span> <span data-ttu-id="a22bc-169">The steps are as follows:</span><span class="sxs-lookup"><span data-stu-id="a22bc-169">The steps are as follows:</span></span>

1. <span data-ttu-id="a22bc-170">Select your StorSimple Data Manager service and go to **Monitoring**.</span><span class="sxs-lookup"><span data-stu-id="a22bc-170">Select your StorSimple Data Manager service and go to **Monitoring**.</span></span> <span data-ttu-id="a22bc-171">Click **Run Now**.</span><span class="sxs-lookup"><span data-stu-id="a22bc-171">Click **Run Now**.</span></span>

    ![Trigger job definition](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-data-manager-ui/run-now.png)

2. <span data-ttu-id="a22bc-173">Choose the job definition that you want to run.</span><span class="sxs-lookup"><span data-stu-id="a22bc-173">Choose the job definition that you want to run.</span></span> <span data-ttu-id="a22bc-174">Click **Run settings** to modify any settings that you might want to change for this job run.</span><span class="sxs-lookup"><span data-stu-id="a22bc-174">Click **Run settings** to modify any settings that you might want to change for this job run.</span></span>

    ![Run job settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-data-manager-ui/run-settings.png)

3. <span data-ttu-id="a22bc-176">Click **OK** and then click **Run** to launch your job.</span><span class="sxs-lookup"><span data-stu-id="a22bc-176">Click **OK** and then click **Run** to launch your job.</span></span> <span data-ttu-id="a22bc-177">To monitor this job, go to the **Jobs** page in your StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="a22bc-177">To monitor this job, go to the **Jobs** page in your StorSimple Data Manager.</span></span>

    ![Jobs list and status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-data-manager-ui/jobs-list-and-status.png)

4. <span data-ttu-id="a22bc-179">In addition to monitoring in the **Jobs** blade, you can also listen on the storage queue where a message is added every time a file is moved from StorSimple to the storage account.</span><span class="sxs-lookup"><span data-stu-id="a22bc-179">In addition to monitoring in the **Jobs** blade, you can also listen on the storage queue where a message is added every time a file is moved from StorSimple to the storage account.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a22bc-180">Next steps</span><span class="sxs-lookup"><span data-stu-id="a22bc-180">Next steps</span></span>

<span data-ttu-id="a22bc-181">[Use .NET SDK to launch StorSimple Data Manager jobs](storsimple-data-manager-dotnet-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="a22bc-181">[Use .NET SDK to launch StorSimple Data Manager jobs](storsimple-data-manager-dotnet-jobs.md).</span></span>










