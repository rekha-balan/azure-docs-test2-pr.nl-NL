---
title: Capture data from Event Hubs into Azure Data Lake Storage Gen1 | Microsoft Docs
description: Use Azure Data Lake Storage Gen1 to capture data from Event Hubs
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: conceptual
ms.date: 05/29/2018
ms.author: nitinme
ms.openlocfilehash: 0bb870b54099fce9f7f6cfd1666be1b6393c5d07
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870233"
---
# <a name="use-azure-data-lake-storage-gen1-to-capture-data-from-event-hubs"></a><span data-ttu-id="948c8-103">Use Azure Data Lake Storage Gen1 to capture data from Event Hubs</span><span class="sxs-lookup"><span data-stu-id="948c8-103">Use Azure Data Lake Storage Gen1 to capture data from Event Hubs</span></span>

<span data-ttu-id="948c8-104">Learn how to use Azure Data Lake Storage Gen1 to capture data received by Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="948c8-104">Learn how to use Azure Data Lake Storage Gen1 to capture data received by Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="948c8-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="948c8-105">Prerequisites</span></span>

* <span data-ttu-id="948c8-106">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="948c8-106">**An Azure subscription**.</span></span> <span data-ttu-id="948c8-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="948c8-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="948c8-108">**An Azure Data Lake Storage Gen1 account**.</span><span class="sxs-lookup"><span data-stu-id="948c8-108">**An Azure Data Lake Storage Gen1 account**.</span></span> <span data-ttu-id="948c8-109">For instructions on how to create one, see [Get started with Azure Data Lake Storage Gen1](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="948c8-109">For instructions on how to create one, see [Get started with Azure Data Lake Storage Gen1](data-lake-store-get-started-portal.md).</span></span>

*  <span data-ttu-id="948c8-110">**An Event Hubs namespace**.</span><span class="sxs-lookup"><span data-stu-id="948c8-110">**An Event Hubs namespace**.</span></span> <span data-ttu-id="948c8-111">For instructions, see [Create an Event Hubs namespace](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span><span class="sxs-lookup"><span data-stu-id="948c8-111">For instructions, see [Create an Event Hubs namespace](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span></span> <span data-ttu-id="948c8-112">Make sure the Data Lake Storage Gen1 account and the Event Hubs namespace are in the same Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="948c8-112">Make sure the Data Lake Storage Gen1 account and the Event Hubs namespace are in the same Azure subscription.</span></span>


## <a name="assign-permissions-to-event-hubs"></a><span data-ttu-id="948c8-113">Assign permissions to Event Hubs</span><span class="sxs-lookup"><span data-stu-id="948c8-113">Assign permissions to Event Hubs</span></span>

<span data-ttu-id="948c8-114">In this section, you create a folder within the account where you want to capture the data from Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="948c8-114">In this section, you create a folder within the account where you want to capture the data from Event Hubs.</span></span> <span data-ttu-id="948c8-115">You also assign permissions to Event Hubs so that it can write data into a Data Lake Storage Gen1 account.</span><span class="sxs-lookup"><span data-stu-id="948c8-115">You also assign permissions to Event Hubs so that it can write data into a Data Lake Storage Gen1 account.</span></span> 

1. <span data-ttu-id="948c8-116">Open the Data Lake Storage Gen1 account where you want to capture data from Event Hubs and then click on **Data Explorer**.</span><span class="sxs-lookup"><span data-stu-id="948c8-116">Open the Data Lake Storage Gen1 account where you want to capture data from Event Hubs and then click on **Data Explorer**.</span></span>

    <span data-ttu-id="948c8-117">![Data Lake Storage Gen1 data explorer](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data Lake Storage Gen1 data explorer")</span><span class="sxs-lookup"><span data-stu-id="948c8-117">![Data Lake Storage Gen1 data explorer](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data Lake Storage Gen1 data explorer")</span></span>

1.  <span data-ttu-id="948c8-118">Click **New Folder** and then enter a name for folder where you want to capture the data.</span><span class="sxs-lookup"><span data-stu-id="948c8-118">Click **New Folder** and then enter a name for folder where you want to capture the data.</span></span>

    <span data-ttu-id="948c8-119">![Create a new folder in Data Lake Storage Gen1](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Create a new folder in Data Lake Storage Gen1")</span><span class="sxs-lookup"><span data-stu-id="948c8-119">![Create a new folder in Data Lake Storage Gen1](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Create a new folder in Data Lake Storage Gen1")</span></span>

1. <span data-ttu-id="948c8-120">Assign permissions at the root of Data Lake Storage Gen1.</span><span class="sxs-lookup"><span data-stu-id="948c8-120">Assign permissions at the root of Data Lake Storage Gen1.</span></span> 

    <span data-ttu-id="948c8-121">a.</span><span class="sxs-lookup"><span data-stu-id="948c8-121">a.</span></span> <span data-ttu-id="948c8-122">Click **Data Explorer**, select the root of the Data Lake Storage Gen1 account, and then click **Access**.</span><span class="sxs-lookup"><span data-stu-id="948c8-122">Click **Data Explorer**, select the root of the Data Lake Storage Gen1 account, and then click **Access**.</span></span>

    <span data-ttu-id="948c8-123">![Assign permissions for the Data Lake Storage Gen1 root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Assign permissions for the Data Lake Storage Gen1 root")</span><span class="sxs-lookup"><span data-stu-id="948c8-123">![Assign permissions for the Data Lake Storage Gen1 root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Assign permissions for the Data Lake Storage Gen1 root")</span></span>

    <span data-ttu-id="948c8-124">b.</span><span class="sxs-lookup"><span data-stu-id="948c8-124">b.</span></span> <span data-ttu-id="948c8-125">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="948c8-125">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="948c8-126">![Assign permissions for the Data Lake Storage Gen1 root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for the Data Lake Storage Gen1 root")</span><span class="sxs-lookup"><span data-stu-id="948c8-126">![Assign permissions for the Data Lake Storage Gen1 root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for the Data Lake Storage Gen1 root")</span></span>
    
    <span data-ttu-id="948c8-127">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="948c8-127">Click **Select**.</span></span>

    <span data-ttu-id="948c8-128">c.</span><span class="sxs-lookup"><span data-stu-id="948c8-128">c.</span></span> <span data-ttu-id="948c8-129">Under **Assign Permissions**, click **Select Permissions**.</span><span class="sxs-lookup"><span data-stu-id="948c8-129">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="948c8-130">Set **Permissions** to **Execute**.</span><span class="sxs-lookup"><span data-stu-id="948c8-130">Set **Permissions** to **Execute**.</span></span> <span data-ttu-id="948c8-131">Set **Add to** to **This folder and all children**.</span><span class="sxs-lookup"><span data-stu-id="948c8-131">Set **Add to** to **This folder and all children**.</span></span> <span data-ttu-id="948c8-132">Set **Add as** to **An access permission entry and a default permission entry**.</span><span class="sxs-lookup"><span data-stu-id="948c8-132">Set **Add as** to **An access permission entry and a default permission entry**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="948c8-133">When creating a new folder heirarchy for capturing data received by Azure Event Hubs, this is an easy way to ensure access to the destination folder.</span><span class="sxs-lookup"><span data-stu-id="948c8-133">When creating a new folder heirarchy for capturing data received by Azure Event Hubs, this is an easy way to ensure access to the destination folder.</span></span>  <span data-ttu-id="948c8-134">However, adding permissions to all children of a top level folder with many child files and folders may take a long time.</span><span class="sxs-lookup"><span data-stu-id="948c8-134">However, adding permissions to all children of a top level folder with many child files and folders may take a long time.</span></span>  <span data-ttu-id="948c8-135">If your root folder contains a large number of files and folders, it may be faster to add **Execute** permissions for `Microsoft.EventHubs` individually to each folder in the path to your final destination folder.</span><span class="sxs-lookup"><span data-stu-id="948c8-135">If your root folder contains a large number of files and folders, it may be faster to add **Execute** permissions for `Microsoft.EventHubs` individually to each folder in the path to your final destination folder.</span></span> 

    <span data-ttu-id="948c8-136">![Assign permissions for the Data Lake Storage Gen1 root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Assign permissions for the Data Lake Storage Gen1 root")</span><span class="sxs-lookup"><span data-stu-id="948c8-136">![Assign permissions for the Data Lake Storage Gen1 root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Assign permissions for the Data Lake Storage Gen1 root")</span></span>

    <span data-ttu-id="948c8-137">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="948c8-137">Click **OK**.</span></span>

1. <span data-ttu-id="948c8-138">Assign permissions for the folder under the Data Lake Storage Gen1 account where you want to capture data.</span><span class="sxs-lookup"><span data-stu-id="948c8-138">Assign permissions for the folder under the Data Lake Storage Gen1 account where you want to capture data.</span></span>

    <span data-ttu-id="948c8-139">a.</span><span class="sxs-lookup"><span data-stu-id="948c8-139">a.</span></span> <span data-ttu-id="948c8-140">Click **Data Explorer**, select the folder in the Data Lake Storage Gen1 account, and then click **Access**.</span><span class="sxs-lookup"><span data-stu-id="948c8-140">Click **Data Explorer**, select the folder in the Data Lake Storage Gen1 account, and then click **Access**.</span></span>

    <span data-ttu-id="948c8-141">![Assign permissions for the Data Lake Storage Gen1 folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Assign permissions for the Data Lake Storage Gen1 folder")</span><span class="sxs-lookup"><span data-stu-id="948c8-141">![Assign permissions for the Data Lake Storage Gen1 folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Assign permissions for the Data Lake Storage Gen1 folder")</span></span>

    <span data-ttu-id="948c8-142">b.</span><span class="sxs-lookup"><span data-stu-id="948c8-142">b.</span></span> <span data-ttu-id="948c8-143">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="948c8-143">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="948c8-144">![Assign permissions for the Data Lake Storage Gen1 folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for the Data Lake Storage Gen1 folder")</span><span class="sxs-lookup"><span data-stu-id="948c8-144">![Assign permissions for the Data Lake Storage Gen1 folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for the Data Lake Storage Gen1 folder")</span></span>
    
    <span data-ttu-id="948c8-145">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="948c8-145">Click **Select**.</span></span>

    <span data-ttu-id="948c8-146">c.</span><span class="sxs-lookup"><span data-stu-id="948c8-146">c.</span></span> <span data-ttu-id="948c8-147">Under **Assign Permissions**, click **Select Permissions**.</span><span class="sxs-lookup"><span data-stu-id="948c8-147">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="948c8-148">Set **Permissions** to **Read, Write,** and **Execute**.</span><span class="sxs-lookup"><span data-stu-id="948c8-148">Set **Permissions** to **Read, Write,** and **Execute**.</span></span> <span data-ttu-id="948c8-149">Set **Add to** to **This folder and all children**.</span><span class="sxs-lookup"><span data-stu-id="948c8-149">Set **Add to** to **This folder and all children**.</span></span> <span data-ttu-id="948c8-150">Finally, set **Add as** to **An access permission entry and a default permission entry**.</span><span class="sxs-lookup"><span data-stu-id="948c8-150">Finally, set **Add as** to **An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="948c8-151">![Assign permissions for the Data Lake Storage Gen1 folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Assign permissions for the Data Lake Storage Gen1 folder")</span><span class="sxs-lookup"><span data-stu-id="948c8-151">![Assign permissions for the Data Lake Storage Gen1 folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Assign permissions for the Data Lake Storage Gen1 folder")</span></span>
    
    <span data-ttu-id="948c8-152">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="948c8-152">Click **OK**.</span></span> 

## <a name="configure-event-hubs-to-capture-data-to-data-lake-storage-gen1"></a><span data-ttu-id="948c8-153">Configure Event Hubs to capture data to Data Lake Storage Gen1</span><span class="sxs-lookup"><span data-stu-id="948c8-153">Configure Event Hubs to capture data to Data Lake Storage Gen1</span></span>

<span data-ttu-id="948c8-154">In this section, you create an Event Hub within an Event Hubs namespace.</span><span class="sxs-lookup"><span data-stu-id="948c8-154">In this section, you create an Event Hub within an Event Hubs namespace.</span></span> <span data-ttu-id="948c8-155">You also configure the Event Hub to capture data to an Azure Data Lake Storage Gen1 account.</span><span class="sxs-lookup"><span data-stu-id="948c8-155">You also configure the Event Hub to capture data to an Azure Data Lake Storage Gen1 account.</span></span> <span data-ttu-id="948c8-156">This section assumes that you have already created an Event Hubs namespace.</span><span class="sxs-lookup"><span data-stu-id="948c8-156">This section assumes that you have already created an Event Hubs namespace.</span></span>

1. <span data-ttu-id="948c8-157">From the **Overview** pane of the Event Hubs namespace, click **+ Event Hub**.</span><span class="sxs-lookup"><span data-stu-id="948c8-157">From the **Overview** pane of the Event Hubs namespace, click **+ Event Hub**.</span></span>

    <span data-ttu-id="948c8-158">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Create Event Hub")</span><span class="sxs-lookup"><span data-stu-id="948c8-158">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Create Event Hub")</span></span>

1. <span data-ttu-id="948c8-159">Provide the following values to configure Event Hubs to capture data to Data Lake Storage Gen1.</span><span class="sxs-lookup"><span data-stu-id="948c8-159">Provide the following values to configure Event Hubs to capture data to Data Lake Storage Gen1.</span></span>

    <span data-ttu-id="948c8-160">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Create Event Hub")</span><span class="sxs-lookup"><span data-stu-id="948c8-160">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Create Event Hub")</span></span>

    <span data-ttu-id="948c8-161">a.</span><span class="sxs-lookup"><span data-stu-id="948c8-161">a.</span></span> <span data-ttu-id="948c8-162">Provide a name for the Event Hub.</span><span class="sxs-lookup"><span data-stu-id="948c8-162">Provide a name for the Event Hub.</span></span>
    
    <span data-ttu-id="948c8-163">b.</span><span class="sxs-lookup"><span data-stu-id="948c8-163">b.</span></span> <span data-ttu-id="948c8-164">For this tutorial, set **Partition Count** and **Message Retention** to the default values.</span><span class="sxs-lookup"><span data-stu-id="948c8-164">For this tutorial, set **Partition Count** and **Message Retention** to the default values.</span></span>
    
    <span data-ttu-id="948c8-165">c.</span><span class="sxs-lookup"><span data-stu-id="948c8-165">c.</span></span> <span data-ttu-id="948c8-166">Set **Capture** to **On**.</span><span class="sxs-lookup"><span data-stu-id="948c8-166">Set **Capture** to **On**.</span></span> <span data-ttu-id="948c8-167">Set the **Time Window** (how frequently to capture) and **Size Window** (data size to capture).</span><span class="sxs-lookup"><span data-stu-id="948c8-167">Set the **Time Window** (how frequently to capture) and **Size Window** (data size to capture).</span></span> 
    
    <span data-ttu-id="948c8-168">d.</span><span class="sxs-lookup"><span data-stu-id="948c8-168">d.</span></span> <span data-ttu-id="948c8-169">For **Capture Provider**, select **Azure Data Lake Store** and then select the Data Lake Storage Gen1 account you created earlier.</span><span class="sxs-lookup"><span data-stu-id="948c8-169">For **Capture Provider**, select **Azure Data Lake Store** and then select the Data Lake Storage Gen1 account you created earlier.</span></span> <span data-ttu-id="948c8-170">For **Data Lake Path**, enter the name of the folder you created in the Data Lake Storage Gen1 account.</span><span class="sxs-lookup"><span data-stu-id="948c8-170">For **Data Lake Path**, enter the name of the folder you created in the Data Lake Storage Gen1 account.</span></span> <span data-ttu-id="948c8-171">You only need to provide the relative path to the folder.</span><span class="sxs-lookup"><span data-stu-id="948c8-171">You only need to provide the relative path to the folder.</span></span>

    <span data-ttu-id="948c8-172">e.</span><span class="sxs-lookup"><span data-stu-id="948c8-172">e.</span></span> <span data-ttu-id="948c8-173">Leave the **Sample capture file name formats** to the default value.</span><span class="sxs-lookup"><span data-stu-id="948c8-173">Leave the **Sample capture file name formats** to the default value.</span></span> <span data-ttu-id="948c8-174">This option governs the folder structure that is created under the capture folder.</span><span class="sxs-lookup"><span data-stu-id="948c8-174">This option governs the folder structure that is created under the capture folder.</span></span>

    <span data-ttu-id="948c8-175">f.</span><span class="sxs-lookup"><span data-stu-id="948c8-175">f.</span></span> <span data-ttu-id="948c8-176">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="948c8-176">Click **Create**.</span></span>

## <a name="test-the-setup"></a><span data-ttu-id="948c8-177">Test the setup</span><span class="sxs-lookup"><span data-stu-id="948c8-177">Test the setup</span></span>

<span data-ttu-id="948c8-178">You can now test the solution by sending data to the Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="948c8-178">You can now test the solution by sending data to the Azure Event Hub.</span></span> <span data-ttu-id="948c8-179">Follow the instructions at [Send events to Azure Event Hubs](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span><span class="sxs-lookup"><span data-stu-id="948c8-179">Follow the instructions at [Send events to Azure Event Hubs](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span></span> <span data-ttu-id="948c8-180">Once you start sending the data, you see the data reflected in Data Lake Storage Gen1 using the folder structure you specified.</span><span class="sxs-lookup"><span data-stu-id="948c8-180">Once you start sending the data, you see the data reflected in Data Lake Storage Gen1 using the folder structure you specified.</span></span> <span data-ttu-id="948c8-181">For example, you see a folder structure, as shown in the following screenshot, in your Data Lake Storage Gen1 account.</span><span class="sxs-lookup"><span data-stu-id="948c8-181">For example, you see a folder structure, as shown in the following screenshot, in your Data Lake Storage Gen1 account.</span></span>

<span data-ttu-id="948c8-182">![Sample EventHub data in Data Lake Storage Gen1](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Sample EventHub data in Data Lake Storage Gen1")</span><span class="sxs-lookup"><span data-stu-id="948c8-182">![Sample EventHub data in Data Lake Storage Gen1](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Sample EventHub data in Data Lake Storage Gen1")</span></span>

> [!NOTE]
> <span data-ttu-id="948c8-183">Even if you do not have messages coming into Event Hubs, Event Hubs writes empty files with just the headers into the Data Lake Storage Gen1 account.</span><span class="sxs-lookup"><span data-stu-id="948c8-183">Even if you do not have messages coming into Event Hubs, Event Hubs writes empty files with just the headers into the Data Lake Storage Gen1 account.</span></span> <span data-ttu-id="948c8-184">The files are written at the same time interval that you provided while creating the Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="948c8-184">The files are written at the same time interval that you provided while creating the Event Hubs.</span></span>
> 
>

## <a name="analyze-data-in-data-lake-storage-gen1"></a><span data-ttu-id="948c8-185">Analyze data in Data Lake Storage Gen1</span><span class="sxs-lookup"><span data-stu-id="948c8-185">Analyze data in Data Lake Storage Gen1</span></span>

<span data-ttu-id="948c8-186">Once the data is in Data Lake Storage Gen1, you can run analytical jobs to process and crunch the data.</span><span class="sxs-lookup"><span data-stu-id="948c8-186">Once the data is in Data Lake Storage Gen1, you can run analytical jobs to process and crunch the data.</span></span> <span data-ttu-id="948c8-187">See [USQL Avro Example](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) on how to do this using Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="948c8-187">See [USQL Avro Example](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) on how to do this using Azure Data Lake Analytics.</span></span>
  

## <a name="see-also"></a><span data-ttu-id="948c8-188">See also</span><span class="sxs-lookup"><span data-stu-id="948c8-188">See also</span></span>
* [<span data-ttu-id="948c8-189">Secure data in Data Lake Storage Gen1</span><span class="sxs-lookup"><span data-stu-id="948c8-189">Secure data in Data Lake Storage Gen1</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="948c8-190">Copy data from Azure Storage Blobs to Data Lake Storage Gen1</span><span class="sxs-lookup"><span data-stu-id="948c8-190">Copy data from Azure Storage Blobs to Data Lake Storage Gen1</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
