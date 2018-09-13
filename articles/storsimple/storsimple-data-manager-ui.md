---
title: Microsoft Azure StorSimple Data Manager UI | Microsoft Docs
description: Describes how to use StorSimple Data Manager serivce UI
services: storsimple
documentationcenter: NA
author: alkohli
manager: jeconnoc
editor: ''
ms.assetid: ''
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 01/16/2018
ms.author: alkohli
ms.openlocfilehash: d704cf8e6840c6a7b0a637c404d421f9f1497c46
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44814579"
---
# <a name="manage-the-storsimple-data-manager-service-in-azure-portal"></a><span data-ttu-id="979b5-103">Manage the StorSimple Data Manager service in Azure portal</span><span class="sxs-lookup"><span data-stu-id="979b5-103">Manage the StorSimple Data Manager service in Azure portal</span></span>

<span data-ttu-id="979b5-104">This article explains how you can use the StorSimple Data Manager UI to transform the data residing on the StorSimple 8000 series devices.</span><span class="sxs-lookup"><span data-stu-id="979b5-104">This article explains how you can use the StorSimple Data Manager UI to transform the data residing on the StorSimple 8000 series devices.</span></span> <span data-ttu-id="979b5-105">The transformed data can then be consumed by other Azure services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search.</span><span class="sxs-lookup"><span data-stu-id="979b5-105">The transformed data can then be consumed by other Azure services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search.</span></span>


## <a name="use-storsimple-data-transformation"></a><span data-ttu-id="979b5-106">Use StorSimple Data Transformation</span><span class="sxs-lookup"><span data-stu-id="979b5-106">Use StorSimple Data Transformation</span></span>

<span data-ttu-id="979b5-107">The StorSimple Data Manager is the resource within which data transformation is instantiated.</span><span class="sxs-lookup"><span data-stu-id="979b5-107">The StorSimple Data Manager is the resource within which data transformation is instantiated.</span></span> <span data-ttu-id="979b5-108">The Data Transformation service lets you transform data from the StorSimple format to native format in blobs or Azure Files.</span><span class="sxs-lookup"><span data-stu-id="979b5-108">The Data Transformation service lets you transform data from the StorSimple format to native format in blobs or Azure Files.</span></span> <span data-ttu-id="979b5-109">To transform the StorSimple native format data, you need to specify the details about your StorSimple 8000 series device and the data of interest that you want to transform.</span><span class="sxs-lookup"><span data-stu-id="979b5-109">To transform the StorSimple native format data, you need to specify the details about your StorSimple 8000 series device and the data of interest that you want to transform.</span></span>

### <a name="create-a-storsimple-data-manager-service"></a><span data-ttu-id="979b5-110">Create a StorSimple Data Manager service</span><span class="sxs-lookup"><span data-stu-id="979b5-110">Create a StorSimple Data Manager service</span></span>

<span data-ttu-id="979b5-111">Perform the following steps to create a StorSimple Data Manager service.</span><span class="sxs-lookup"><span data-stu-id="979b5-111">Perform the following steps to create a StorSimple Data Manager service.</span></span>

1. <span data-ttu-id="979b5-112">Use your Microsoft account credentials to log on to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="979b5-112">Use your Microsoft account credentials to log on to the [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="979b5-113">Click **+ Create a resource** and search for StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="979b5-113">Click **+ Create a resource** and search for StorSimple Data Manager.</span></span>

    ![Create a StorSimple Data Manager service 1](./media/storsimple-data-manager-ui/create-service-1.png)

3. <span data-ttu-id="979b5-115">Click StorSimple Data Manager and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="979b5-115">Click StorSimple Data Manager and then click **Create**.</span></span>
    
    ![Create a StorSimple Data Manager service 2](./media/storsimple-data-manager-ui/create-service-3.png)

3. <span data-ttu-id="979b5-117">For the new service, specify the following:</span><span class="sxs-lookup"><span data-stu-id="979b5-117">For the new service, specify the following:</span></span>

    1. <span data-ttu-id="979b5-118">Provide a unique **Service name** for your StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="979b5-118">Provide a unique **Service name** for your StorSimple Data Manager.</span></span> <span data-ttu-id="979b5-119">This is a friendly name that can be used to identify the service.</span><span class="sxs-lookup"><span data-stu-id="979b5-119">This is a friendly name that can be used to identify the service.</span></span> <span data-ttu-id="979b5-120">The name can have between 3 and 24 characters that can be letters, numbers, and hyphens.</span><span class="sxs-lookup"><span data-stu-id="979b5-120">The name can have between 3 and 24 characters that can be letters, numbers, and hyphens.</span></span> <span data-ttu-id="979b5-121">The name must start and end with a letter or a number.</span><span class="sxs-lookup"><span data-stu-id="979b5-121">The name must start and end with a letter or a number.</span></span>

    2. <span data-ttu-id="979b5-122">Choose a **Subscription** from the dropdown list.</span><span class="sxs-lookup"><span data-stu-id="979b5-122">Choose a **Subscription** from the dropdown list.</span></span> <span data-ttu-id="979b5-123">The subscription is linked to your billing account.</span><span class="sxs-lookup"><span data-stu-id="979b5-123">The subscription is linked to your billing account.</span></span> <span data-ttu-id="979b5-124">This field is automatically populated (and not selectable) if you have only one subscription.</span><span class="sxs-lookup"><span data-stu-id="979b5-124">This field is automatically populated (and not selectable) if you have only one subscription.</span></span>

    3. <span data-ttu-id="979b5-125">Select an existing resource group or create a new group.</span><span class="sxs-lookup"><span data-stu-id="979b5-125">Select an existing resource group or create a new group.</span></span> <span data-ttu-id="979b5-126">For more information, see [Azure resource groups](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-infrastructure-resource-groups-guidelines/).</span><span class="sxs-lookup"><span data-stu-id="979b5-126">For more information, see [Azure resource groups](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-infrastructure-resource-groups-guidelines/).</span></span>

    4. <span data-ttu-id="979b5-127">Specify the **Location** for your service that houses your storage accounts and your StorSimple Data Manager service.</span><span class="sxs-lookup"><span data-stu-id="979b5-127">Specify the **Location** for your service that houses your storage accounts and your StorSimple Data Manager service.</span></span> <span data-ttu-id="979b5-128">Your StorSimple Device Manager service, Data Manager service, and the associated storage account should all be in the supported regions.</span><span class="sxs-lookup"><span data-stu-id="979b5-128">Your StorSimple Device Manager service, Data Manager service, and the associated storage account should all be in the supported regions.</span></span>
    
    5. <span data-ttu-id="979b5-129">To get a link to this service on your dashboard, select **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="979b5-129">To get a link to this service on your dashboard, select **Pin to dashboard**.</span></span>
    
    6. <span data-ttu-id="979b5-130">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="979b5-130">Click **Create**.</span></span>

    ![Create a StorSimple Data Manager service 3](./media/storsimple-data-manager-ui/create-service-4.png)

<span data-ttu-id="979b5-132">The service creation takes a few minutes.</span><span class="sxs-lookup"><span data-stu-id="979b5-132">The service creation takes a few minutes.</span></span> <span data-ttu-id="979b5-133">You see a notification after the service is successfully created and the new service is displayed.</span><span class="sxs-lookup"><span data-stu-id="979b5-133">You see a notification after the service is successfully created and the new service is displayed.</span></span>

### <a name="create-a-data-transformation-job-definition"></a><span data-ttu-id="979b5-134">Create a data transformation job definition</span><span class="sxs-lookup"><span data-stu-id="979b5-134">Create a data transformation job definition</span></span>

<span data-ttu-id="979b5-135">Within a StorSimple Data Manager service, you need to create a data transformation job definition.</span><span class="sxs-lookup"><span data-stu-id="979b5-135">Within a StorSimple Data Manager service, you need to create a data transformation job definition.</span></span> <span data-ttu-id="979b5-136">A job definition specifies details of the StorSimple data that you are interested in moving into a storage account in the native format.</span><span class="sxs-lookup"><span data-stu-id="979b5-136">A job definition specifies details of the StorSimple data that you are interested in moving into a storage account in the native format.</span></span> <span data-ttu-id="979b5-137">Once you create a job definition, then you can run this job again with different runtime settings.</span><span class="sxs-lookup"><span data-stu-id="979b5-137">Once you create a job definition, then you can run this job again with different runtime settings.</span></span>

<span data-ttu-id="979b5-138">Perform the following steps to create a job definition.</span><span class="sxs-lookup"><span data-stu-id="979b5-138">Perform the following steps to create a job definition.</span></span>

1. <span data-ttu-id="979b5-139">Navigate to the service that you created.</span><span class="sxs-lookup"><span data-stu-id="979b5-139">Navigate to the service that you created.</span></span> <span data-ttu-id="979b5-140">Go to **Management > Job definitions**.</span><span class="sxs-lookup"><span data-stu-id="979b5-140">Go to **Management > Job definitions**.</span></span>

2. <span data-ttu-id="979b5-141">Click **+ Job definition**.</span><span class="sxs-lookup"><span data-stu-id="979b5-141">Click **+ Job definition**.</span></span>

    ![Click +Job Definition](./media/storsimple-data-manager-ui/create-job-definition-1.png)

3. <span data-ttu-id="979b5-143">Provide a name for your job definition.</span><span class="sxs-lookup"><span data-stu-id="979b5-143">Provide a name for your job definition.</span></span> <span data-ttu-id="979b5-144">The name can be between 3 and 63 characters.</span><span class="sxs-lookup"><span data-stu-id="979b5-144">The name can be between 3 and 63 characters.</span></span> <span data-ttu-id="979b5-145">The name can contain uppercase and lowercase letters, numbers, and hyphens.</span><span class="sxs-lookup"><span data-stu-id="979b5-145">The name can contain uppercase and lowercase letters, numbers, and hyphens.</span></span>

4. <span data-ttu-id="979b5-146">Specify a location where your job runs.</span><span class="sxs-lookup"><span data-stu-id="979b5-146">Specify a location where your job runs.</span></span> <span data-ttu-id="979b5-147">This location can be different than the location where the service is deployed.</span><span class="sxs-lookup"><span data-stu-id="979b5-147">This location can be different than the location where the service is deployed.</span></span>

5. <span data-ttu-id="979b5-148">Click **Source** to specify the source data repository.</span><span class="sxs-lookup"><span data-stu-id="979b5-148">Click **Source** to specify the source data repository.</span></span>

    ![Configure source data repo](./media/storsimple-data-manager-ui/create-job-definition-2.png)

6. <span data-ttu-id="979b5-150">Since this is a new Data Manager service, no data repositories are configured.</span><span class="sxs-lookup"><span data-stu-id="979b5-150">Since this is a new Data Manager service, no data repositories are configured.</span></span> <span data-ttu-id="979b5-151">In **Configure data source**, specify the details of your StorSimple 8000 series device and the data of interest.</span><span class="sxs-lookup"><span data-stu-id="979b5-151">In **Configure data source**, specify the details of your StorSimple 8000 series device and the data of interest.</span></span>

   <span data-ttu-id="979b5-152">To add your StorSimple Device Manager as a data repository, click **Add new** in the data repository dropdown and then click **Add Data Repository**.</span><span class="sxs-lookup"><span data-stu-id="979b5-152">To add your StorSimple Device Manager as a data repository, click **Add new** in the data repository dropdown and then click **Add Data Repository**.</span></span>

    ![Add new data repo](./media/storsimple-data-manager-ui/create-job-definition-3.png)
  
    1. <span data-ttu-id="979b5-154">Choose **StorSimple 8000 series Manager** as the data repository type.</span><span class="sxs-lookup"><span data-stu-id="979b5-154">Choose **StorSimple 8000 series Manager** as the data repository type.</span></span>
    
    2. <span data-ttu-id="979b5-155">Enter a friendly name for your source data repository.</span><span class="sxs-lookup"><span data-stu-id="979b5-155">Enter a friendly name for your source data repository.</span></span>
    
    3. <span data-ttu-id="979b5-156">From the dropdown list, choose a subscription associated with your StorSimple Device Manager service.</span><span class="sxs-lookup"><span data-stu-id="979b5-156">From the dropdown list, choose a subscription associated with your StorSimple Device Manager service.</span></span>
    
    4. <span data-ttu-id="979b5-157">Provide the name of the StorSimple Device Manager for the **Resource**.</span><span class="sxs-lookup"><span data-stu-id="979b5-157">Provide the name of the StorSimple Device Manager for the **Resource**.</span></span>

    5. <span data-ttu-id="979b5-158">Enter the **Service data encryption** key for the StorSimple Device Manager service.</span><span class="sxs-lookup"><span data-stu-id="979b5-158">Enter the **Service data encryption** key for the StorSimple Device Manager service.</span></span> 

    ![Configure source data repo 1](./media/storsimple-data-manager-ui/create-job-definition-4.png)

    <span data-ttu-id="979b5-160">Click **OK** when done.</span><span class="sxs-lookup"><span data-stu-id="979b5-160">Click **OK** when done.</span></span> <span data-ttu-id="979b5-161">This saves your data repository.</span><span class="sxs-lookup"><span data-stu-id="979b5-161">This saves your data repository.</span></span> <span data-ttu-id="979b5-162">Reuse this StorSimple Device Manager in other job definitions without entering these parameters again.</span><span class="sxs-lookup"><span data-stu-id="979b5-162">Reuse this StorSimple Device Manager in other job definitions without entering these parameters again.</span></span> <span data-ttu-id="979b5-163">It takes a few seconds after you click **OK** for the newly created source data repository to show up in the dropdown.</span><span class="sxs-lookup"><span data-stu-id="979b5-163">It takes a few seconds after you click **OK** for the newly created source data repository to show up in the dropdown.</span></span>

7. <span data-ttu-id="979b5-164">From the dropdown list for **Data repository**, select the data repository you created.</span><span class="sxs-lookup"><span data-stu-id="979b5-164">From the dropdown list for **Data repository**, select the data repository you created.</span></span> 

    1. <span data-ttu-id="979b5-165">Enter the name of the StorSimple 8000 series device that contains the data of interest.</span><span class="sxs-lookup"><span data-stu-id="979b5-165">Enter the name of the StorSimple 8000 series device that contains the data of interest.</span></span>

    2. <span data-ttu-id="979b5-166">Specify the name of the volume residing on the StorSimple device that has your data of interest.</span><span class="sxs-lookup"><span data-stu-id="979b5-166">Specify the name of the volume residing on the StorSimple device that has your data of interest.</span></span>

    3. <span data-ttu-id="979b5-167">In the **Filter** subsection, enter the root directory that contains your data of interest in _\MyRootDirectory\Data_ format.</span><span class="sxs-lookup"><span data-stu-id="979b5-167">In the **Filter** subsection, enter the root directory that contains your data of interest in _\MyRootDirectory\Data_ format.</span></span> <span data-ttu-id="979b5-168">Drive letters such _\C:\Data_ are not supported.</span><span class="sxs-lookup"><span data-stu-id="979b5-168">Drive letters such _\C:\Data_ are not supported.</span></span> <span data-ttu-id="979b5-169">You can also add any file filters here.</span><span class="sxs-lookup"><span data-stu-id="979b5-169">You can also add any file filters here.</span></span>

    4. <span data-ttu-id="979b5-170">The data transformation service works on the data that is pushed up to the Azure via snapshots.</span><span class="sxs-lookup"><span data-stu-id="979b5-170">The data transformation service works on the data that is pushed up to the Azure via snapshots.</span></span> <span data-ttu-id="979b5-171">When you run this job, you can choose to take a backup every time this job is run (to work on latest data) or use the last existing backup in the cloud (if you are working on some archived data).</span><span class="sxs-lookup"><span data-stu-id="979b5-171">When you run this job, you can choose to take a backup every time this job is run (to work on latest data) or use the last existing backup in the cloud (if you are working on some archived data).</span></span>

    5. <span data-ttu-id="979b5-172">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="979b5-172">Click **OK**.</span></span>

    ![Configure source data repo 2](./media/storsimple-data-manager-ui/create-job-definition-8.png)

8. <span data-ttu-id="979b5-174">Next, the target data repository needs to be configured.</span><span class="sxs-lookup"><span data-stu-id="979b5-174">Next, the target data repository needs to be configured.</span></span> <span data-ttu-id="979b5-175">Choose storage accounts to put files into blobs in that account.</span><span class="sxs-lookup"><span data-stu-id="979b5-175">Choose storage accounts to put files into blobs in that account.</span></span> <span data-ttu-id="979b5-176">In the dropdown, select **Add new** and then **Configure settings**.</span><span class="sxs-lookup"><span data-stu-id="979b5-176">In the dropdown, select **Add new** and then **Configure settings**.</span></span>

9. <span data-ttu-id="979b5-177">Select the type of target repository you want to add and the other parameters associated with the repository.</span><span class="sxs-lookup"><span data-stu-id="979b5-177">Select the type of target repository you want to add and the other parameters associated with the repository.</span></span>

    <span data-ttu-id="979b5-178">If you select a Storage account type target, you can specify a friendly name, subscription (choose the same as that of the service or other), and a storage account.</span><span class="sxs-lookup"><span data-stu-id="979b5-178">If you select a Storage account type target, you can specify a friendly name, subscription (choose the same as that of the service or other), and a storage account.</span></span>
        <span data-ttu-id="979b5-179">![Configure target data repo 1](./media/storsimple-data-manager-ui/create-job-definition-10.png)</span><span class="sxs-lookup"><span data-stu-id="979b5-179">![Configure target data repo 1](./media/storsimple-data-manager-ui/create-job-definition-10.png)</span></span>

    <span data-ttu-id="979b5-180">A storage queue is created when the job runs.</span><span class="sxs-lookup"><span data-stu-id="979b5-180">A storage queue is created when the job runs.</span></span> <span data-ttu-id="979b5-181">This queue is populated with messages about transformed blobs as they are ready.</span><span class="sxs-lookup"><span data-stu-id="979b5-181">This queue is populated with messages about transformed blobs as they are ready.</span></span> <span data-ttu-id="979b5-182">The name of this queue is the same as the name of the job definition.</span><span class="sxs-lookup"><span data-stu-id="979b5-182">The name of this queue is the same as the name of the job definition.</span></span>
    
10. <span data-ttu-id="979b5-183">After you add the data repository, wait a couple minutes.</span><span class="sxs-lookup"><span data-stu-id="979b5-183">After you add the data repository, wait a couple minutes.</span></span>
    
    1. <span data-ttu-id="979b5-184">Select the repository you created as the target from the dropdown list in the **Target account name**.</span><span class="sxs-lookup"><span data-stu-id="979b5-184">Select the repository you created as the target from the dropdown list in the **Target account name**.</span></span>

    2. <span data-ttu-id="979b5-185">Choose the storage type as blobs or files.</span><span class="sxs-lookup"><span data-stu-id="979b5-185">Choose the storage type as blobs or files.</span></span> <span data-ttu-id="979b5-186">Specify the name of the storage container where the transformed data resides.</span><span class="sxs-lookup"><span data-stu-id="979b5-186">Specify the name of the storage container where the transformed data resides.</span></span> <span data-ttu-id="979b5-187">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="979b5-187">Click **OK**.</span></span>

        ![Configure target data repo storage account](./media/storsimple-data-manager-ui/create-job-definition-16.png)

11. <span data-ttu-id="979b5-189">You can also check the option to present an estimate of job duration before you run the job.</span><span class="sxs-lookup"><span data-stu-id="979b5-189">You can also check the option to present an estimate of job duration before you run the job.</span></span> <span data-ttu-id="979b5-190">Click **OK** to create the job definition.</span><span class="sxs-lookup"><span data-stu-id="979b5-190">Click **OK** to create the job definition.</span></span> <span data-ttu-id="979b5-191">Your job definition is now complete.</span><span class="sxs-lookup"><span data-stu-id="979b5-191">Your job definition is now complete.</span></span> <span data-ttu-id="979b5-192">You can use this job definition multiple times via the UI with different runtime settings.</span><span class="sxs-lookup"><span data-stu-id="979b5-192">You can use this job definition multiple times via the UI with different runtime settings.</span></span>

    ![Complete job definition](./media/storsimple-data-manager-ui/create-job-definition-13.png)

    <span data-ttu-id="979b5-194">The newly created job definition is added to the list of job definitions for this service.</span><span class="sxs-lookup"><span data-stu-id="979b5-194">The newly created job definition is added to the list of job definitions for this service.</span></span>

### <a name="run-the-job-definition"></a><span data-ttu-id="979b5-195">Run the job definition</span><span class="sxs-lookup"><span data-stu-id="979b5-195">Run the job definition</span></span>

<span data-ttu-id="979b5-196">Whenever you need to move data from StorSimple to the storage account that you have specified in the job definition, you need to run it.</span><span class="sxs-lookup"><span data-stu-id="979b5-196">Whenever you need to move data from StorSimple to the storage account that you have specified in the job definition, you need to run it.</span></span> <span data-ttu-id="979b5-197">At runtime, some parameters can be specified differently.</span><span class="sxs-lookup"><span data-stu-id="979b5-197">At runtime, some parameters can be specified differently.</span></span> <span data-ttu-id="979b5-198">The steps are as follows:</span><span class="sxs-lookup"><span data-stu-id="979b5-198">The steps are as follows:</span></span>

1. <span data-ttu-id="979b5-199">Select your StorSimple Data Manager service and go to **Management > Job definitions**.</span><span class="sxs-lookup"><span data-stu-id="979b5-199">Select your StorSimple Data Manager service and go to **Management > Job definitions**.</span></span> <span data-ttu-id="979b5-200">Select and click the job definition that you want to run.</span><span class="sxs-lookup"><span data-stu-id="979b5-200">Select and click the job definition that you want to run.</span></span>
     
     ![Start job run 1](./media/storsimple-data-manager-ui/start-job-run1.png)

2. <span data-ttu-id="979b5-202">Click **Run Now**.</span><span class="sxs-lookup"><span data-stu-id="979b5-202">Click **Run Now**.</span></span>
     
     ![Start job run 2](./media/storsimple-data-manager-ui/start-job-run2.png)

3. <span data-ttu-id="979b5-204">Click **Run settings** to modify any settings that you might want to change for this job run.</span><span class="sxs-lookup"><span data-stu-id="979b5-204">Click **Run settings** to modify any settings that you might want to change for this job run.</span></span> <span data-ttu-id="979b5-205">Click **OK** and then click **Run** to launch your job.</span><span class="sxs-lookup"><span data-stu-id="979b5-205">Click **OK** and then click **Run** to launch your job.</span></span>

    ![Start job run 3](./media/storsimple-data-manager-ui/start-job-run3.png)

4. <span data-ttu-id="979b5-207">To monitor this job, go to **Jobs** in your StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="979b5-207">To monitor this job, go to **Jobs** in your StorSimple Data Manager.</span></span> <span data-ttu-id="979b5-208">In addition to monitoring in the **Jobs** blade, you can also listen on the storage queue where a message is added every time a file is moved from StorSimple to the storage account.</span><span class="sxs-lookup"><span data-stu-id="979b5-208">In addition to monitoring in the **Jobs** blade, you can also listen on the storage queue where a message is added every time a file is moved from StorSimple to the storage account.</span></span>

    ![Start job run 4](./media/storsimple-data-manager-ui/start-job-run4.png)


## <a name="next-steps"></a><span data-ttu-id="979b5-210">Next steps</span><span class="sxs-lookup"><span data-stu-id="979b5-210">Next steps</span></span>

<span data-ttu-id="979b5-211">[Use .NET SDK to launch StorSimple Data Manager jobs](storsimple-data-manager-dotnet-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="979b5-211">[Use .NET SDK to launch StorSimple Data Manager jobs](storsimple-data-manager-dotnet-jobs.md).</span></span>