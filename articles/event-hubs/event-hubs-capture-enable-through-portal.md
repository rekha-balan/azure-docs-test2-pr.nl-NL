---
title: Azure Event Hubs Capture enable through portal | Microsoft Docs
description: Enable the Event Hubs Capture feature using the Azure portal.
services: event-hubs
documentationcenter: ''
author: ShubhaVijayasarathy
manager: timlt
editor: ''
ms.assetid: ''
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/16/2018
ms.author: shvija
ms.openlocfilehash: ff80bc2452c9826a5c51c146a957fddc72d2dbc2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869173"
---
# <a name="enable-event-hubs-capture-using-the-azure-portal"></a><span data-ttu-id="3ea3e-103">Enable Event Hubs Capture using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="3ea3e-103">Enable Event Hubs Capture using the Azure portal</span></span>

<span data-ttu-id="3ea3e-104">Azure [Event Hubs Capture][capture-overview] enables you to automatically deliver the streaming data in Event Hubs to an [Azure Blob storage](https://azure.microsoft.com/services/storage/blobs/) or [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account of your choice.</span><span class="sxs-lookup"><span data-stu-id="3ea3e-104">Azure [Event Hubs Capture][capture-overview] enables you to automatically deliver the streaming data in Event Hubs to an [Azure Blob storage](https://azure.microsoft.com/services/storage/blobs/) or [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account of your choice.</span></span>

<span data-ttu-id="3ea3e-105">You can configure Capture at the event hub creation time using the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3ea3e-105">You can configure Capture at the event hub creation time using the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="3ea3e-106">You can either capture the data to an Azure [Blob storage](https://azure.microsoft.com/services/storage/blobs/) container, or to an [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account.</span><span class="sxs-lookup"><span data-stu-id="3ea3e-106">You can either capture the data to an Azure [Blob storage](https://azure.microsoft.com/services/storage/blobs/) container, or to an [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account.</span></span>

<span data-ttu-id="3ea3e-107">For more information, see the [Event Hubs Capture overview][capture-overview].</span><span class="sxs-lookup"><span data-stu-id="3ea3e-107">For more information, see the [Event Hubs Capture overview][capture-overview].</span></span>

## <a name="capture-data-to-an-azure-storage-account"></a><span data-ttu-id="3ea3e-108">Capture data to an Azure Storage account</span><span class="sxs-lookup"><span data-stu-id="3ea3e-108">Capture data to an Azure Storage account</span></span>  

<span data-ttu-id="3ea3e-109">When you create an event hub, you can enable Capture by clicking the **On** button in the **Create Event Hub** portal screen.</span><span class="sxs-lookup"><span data-stu-id="3ea3e-109">When you create an event hub, you can enable Capture by clicking the **On** button in the **Create Event Hub** portal screen.</span></span> <span data-ttu-id="3ea3e-110">You then specify a Storage Account and container by clicking **Azure Storage** in the **Capture Provider** box.</span><span class="sxs-lookup"><span data-stu-id="3ea3e-110">You then specify a Storage Account and container by clicking **Azure Storage** in the **Capture Provider** box.</span></span> <span data-ttu-id="3ea3e-111">Because Event Hubs Capture uses service-to-service authentication with storage, you do not need to specify a storage connection string.</span><span class="sxs-lookup"><span data-stu-id="3ea3e-111">Because Event Hubs Capture uses service-to-service authentication with storage, you do not need to specify a storage connection string.</span></span> <span data-ttu-id="3ea3e-112">The resource picker selects the resource URI for your storage account automatically.</span><span class="sxs-lookup"><span data-stu-id="3ea3e-112">The resource picker selects the resource URI for your storage account automatically.</span></span> <span data-ttu-id="3ea3e-113">If you use Azure Resource Manager, you must supply this URI explicitly as a string.</span><span class="sxs-lookup"><span data-stu-id="3ea3e-113">If you use Azure Resource Manager, you must supply this URI explicitly as a string.</span></span>

<span data-ttu-id="3ea3e-114">The default time window is 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="3ea3e-114">The default time window is 5 minutes.</span></span> <span data-ttu-id="3ea3e-115">The minimum value is 1, the maximum 15.</span><span class="sxs-lookup"><span data-stu-id="3ea3e-115">The minimum value is 1, the maximum 15.</span></span> <span data-ttu-id="3ea3e-116">The **Size** window has a range of 10-500 MB.</span><span class="sxs-lookup"><span data-stu-id="3ea3e-116">The **Size** window has a range of 10-500 MB.</span></span>

![][1]

## <a name="capture-data-to-an-azure-data-lake-store-account"></a><span data-ttu-id="3ea3e-117">Capture data to an Azure Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="3ea3e-117">Capture data to an Azure Data Lake Store account</span></span>

<span data-ttu-id="3ea3e-118">To capture data to Azure Data Lake Store, you create a Data Lake Store account, and an event hub:</span><span class="sxs-lookup"><span data-stu-id="3ea3e-118">To capture data to Azure Data Lake Store, you create a Data Lake Store account, and an event hub:</span></span>

### <a name="create-an-azure-data-lake-store-account-and-folders"></a><span data-ttu-id="3ea3e-119">Create an Azure Data Lake Store account and folders</span><span class="sxs-lookup"><span data-stu-id="3ea3e-119">Create an Azure Data Lake Store account and folders</span></span>

1. <span data-ttu-id="3ea3e-120">Create a Data Lake Store account, following the instructions in [Get started with Azure Data Lake Store using the Azure portal](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3ea3e-120">Create a Data Lake Store account, following the instructions in [Get started with Azure Data Lake Store using the Azure portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>
2. <span data-ttu-id="3ea3e-121">Follow the instructions in the [Assign permissions to Event Hubs](../data-lake-store/data-lake-store-archive-eventhub-capture.md#assign-permissions-to-event-hubs) section to create a folder within the Data Lake Store account in which you want to capture the data from Event Hubs, and assign permissions to Event Hubs so that it can write data into your Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="3ea3e-121">Follow the instructions in the [Assign permissions to Event Hubs](../data-lake-store/data-lake-store-archive-eventhub-capture.md#assign-permissions-to-event-hubs) section to create a folder within the Data Lake Store account in which you want to capture the data from Event Hubs, and assign permissions to Event Hubs so that it can write data into your Data Lake Store account.</span></span>  

### <a name="create-an-event-hub"></a><span data-ttu-id="3ea3e-122">Create an event hub</span><span class="sxs-lookup"><span data-stu-id="3ea3e-122">Create an event hub</span></span>

1. <span data-ttu-id="3ea3e-123">Note that the event hub must be in the same Azure subscription as the Azure Data Lake Store you just created.</span><span class="sxs-lookup"><span data-stu-id="3ea3e-123">Note that the event hub must be in the same Azure subscription as the Azure Data Lake Store you just created.</span></span> <span data-ttu-id="3ea3e-124">Create the event hub, clicking the **On** button under **Capture** in the **Create Event Hub** portal page.</span><span class="sxs-lookup"><span data-stu-id="3ea3e-124">Create the event hub, clicking the **On** button under **Capture** in the **Create Event Hub** portal page.</span></span> 
2. <span data-ttu-id="3ea3e-125">In the **Create Event Hub** portal page, select **Azure Data Lake Store** from the **Capture Provider** box.</span><span class="sxs-lookup"><span data-stu-id="3ea3e-125">In the **Create Event Hub** portal page, select **Azure Data Lake Store** from the **Capture Provider** box.</span></span>
3. <span data-ttu-id="3ea3e-126">In **Select Data Lake Store**, specify the Data Lake Store account you created previously, and in the **Data Lake Path** field, enter the path to the data folder you created.</span><span class="sxs-lookup"><span data-stu-id="3ea3e-126">In **Select Data Lake Store**, specify the Data Lake Store account you created previously, and in the **Data Lake Path** field, enter the path to the data folder you created.</span></span>

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a><span data-ttu-id="3ea3e-127">Add or configure Capture on an existing event hub</span><span class="sxs-lookup"><span data-stu-id="3ea3e-127">Add or configure Capture on an existing event hub</span></span>

<span data-ttu-id="3ea3e-128">You can configure Capture on existing event hubs that are in Event Hubs namespaces.</span><span class="sxs-lookup"><span data-stu-id="3ea3e-128">You can configure Capture on existing event hubs that are in Event Hubs namespaces.</span></span> <span data-ttu-id="3ea3e-129">To enable Capture on an existing event hub, or to change your Capture settings, click the namespace to load the overview screen, then click the event hub for which you want to enable or change the Capture setting.</span><span class="sxs-lookup"><span data-stu-id="3ea3e-129">To enable Capture on an existing event hub, or to change your Capture settings, click the namespace to load the overview screen, then click the event hub for which you want to enable or change the Capture setting.</span></span> <span data-ttu-id="3ea3e-130">Finally, click the **Capture** option on the left side of the open page and then edit the settings, as shown in the following figures:</span><span class="sxs-lookup"><span data-stu-id="3ea3e-130">Finally, click the **Capture** option on the left side of the open page and then edit the settings, as shown in the following figures:</span></span>

### <a name="azure-blob-storage"></a><span data-ttu-id="3ea3e-131">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="3ea3e-131">Azure Blob Storage</span></span>

![][2]

### <a name="azure-data-lake-store"></a><span data-ttu-id="3ea3e-132">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="3ea3e-132">Azure Data Lake Store</span></span>

![][4]

[1]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture1.png
[2]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture2.png
[3]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture3.png
[4]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture4.png

## <a name="next-steps"></a><span data-ttu-id="3ea3e-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="3ea3e-133">Next steps</span></span>

- <span data-ttu-id="3ea3e-134">Learn more about Event Hubs capture by reading the [Event Hubs Capture overview][capture-overview].</span><span class="sxs-lookup"><span data-stu-id="3ea3e-134">Learn more about Event Hubs capture by reading the [Event Hubs Capture overview][capture-overview].</span></span>
- <span data-ttu-id="3ea3e-135">You can also configure Event Hubs Capture using Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="3ea3e-135">You can also configure Event Hubs Capture using Azure Resource Manager templates.</span></span> <span data-ttu-id="3ea3e-136">For more information, see [Enable Capture using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span><span class="sxs-lookup"><span data-stu-id="3ea3e-136">For more information, see [Enable Capture using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span></span>
- [<span data-ttu-id="3ea3e-137">Get started with Azure Data Lake Store using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="3ea3e-137">Get started with Azure Data Lake Store using the Azure portal</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)

[capture-overview]: event-hubs-capture-overview.md