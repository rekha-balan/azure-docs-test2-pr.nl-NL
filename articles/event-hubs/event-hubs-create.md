---
title: Create an Azure event hub | Microsoft Docs
description: Create an Azure Event Hubs namespace and an event hub using the Azure portal
services: event-hubs
documentationcenter: na
author: jtaubensee
manager: timlt
editor: ''
ms.assetid: ff99e327-c8db-4354-9040-9c60c51a2191
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/25/2017
ms.author: jotaub
ms.openlocfilehash: 6c439fc58c361473d25dddcdd0ef05a473b2ef11
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540636"
---
# <a name="create-an-event-hubs-namespace-and-an-event-hub-using-the-azure-portal"></a><span data-ttu-id="156f3-103">Create an Event Hubs namespace and an event hub using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="156f3-103">Create an Event Hubs namespace and an event hub using the Azure portal</span></span>

## <a name="create-an-event-hubs-namespace"></a><span data-ttu-id="156f3-104">Create an Event Hubs namespace</span><span class="sxs-lookup"><span data-stu-id="156f3-104">Create an Event Hubs namespace</span></span>
1. <span data-ttu-id="156f3-105">Log on to the [Azure portal][Azure portal], and click **New** at the top left of the screen.</span><span class="sxs-lookup"><span data-stu-id="156f3-105">Log on to the [Azure portal][Azure portal], and click **New** at the top left of the screen.</span></span>
1. <span data-ttu-id="156f3-106">Click **Internet of Things**, and then click **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="156f3-106">Click **Internet of Things**, and then click **Event Hubs**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-create/create-event-hub9.png)
1. <span data-ttu-id="156f3-107">In the **Create namespace** blade, enter a namespace name.</span><span class="sxs-lookup"><span data-stu-id="156f3-107">In the **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="156f3-108">The system immediately checks to see if the name is available.</span><span class="sxs-lookup"><span data-stu-id="156f3-108">The system immediately checks to see if the name is available.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-create/create-event-hub1.png)
1. <span data-ttu-id="156f3-109">After making sure the namespace name is available, choose the pricing tier (Basic or Standard).</span><span class="sxs-lookup"><span data-stu-id="156f3-109">After making sure the namespace name is available, choose the pricing tier (Basic or Standard).</span></span> <span data-ttu-id="156f3-110">Also, choose an Azure subscription, resource group, and location in which to create the resource.</span><span class="sxs-lookup"><span data-stu-id="156f3-110">Also, choose an Azure subscription, resource group, and location in which to create the resource.</span></span> 
1. <span data-ttu-id="156f3-111">Click **Create** to create the namespace.</span><span class="sxs-lookup"><span data-stu-id="156f3-111">Click **Create** to create the namespace.</span></span>
1. <span data-ttu-id="156f3-112">In the Event Hubs namespace list, click the newly-created namespace.</span><span class="sxs-lookup"><span data-stu-id="156f3-112">In the Event Hubs namespace list, click the newly-created namespace.</span></span>      
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-create/create-event-hub2.png)
1. <span data-ttu-id="156f3-113">In the namespace blade, click **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="156f3-113">In the namespace blade, click **Event Hubs**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-create/create-event-hub3.png)

## <a name="create-an-event-hub"></a><span data-ttu-id="156f3-114">Create an event hub</span><span class="sxs-lookup"><span data-stu-id="156f3-114">Create an event hub</span></span>

1. <span data-ttu-id="156f3-115">At the top of the blade, click **Add Event Hub**.</span><span class="sxs-lookup"><span data-stu-id="156f3-115">At the top of the blade, click **Add Event Hub**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-create/create-event-hub4.png)
1. <span data-ttu-id="156f3-116">Type a name for your event hub, then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="156f3-116">Type a name for your event hub, then click **Create**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-create/create-event-hub5.png)
1. <span data-ttu-id="156f3-117">In the list of event hubs, click the newly created event hub name.</span><span class="sxs-lookup"><span data-stu-id="156f3-117">In the list of event hubs, click the newly created event hub name.</span></span> 
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-create/create-event-hub6.png)
1. <span data-ttu-id="156f3-118">Back in the namespace blade (not the specific event hub blade), click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="156f3-118">Back in the namespace blade (not the specific event hub blade), click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-create/create-event-hub7.png)
1. <span data-ttu-id="156f3-119">Click the copy button to copy the **RootManageSharedAccessKey** connection string to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="156f3-119">Click the copy button to copy the **RootManageSharedAccessKey** connection string to the clipboard.</span></span> <span data-ttu-id="156f3-120">Save this connection string to use later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="156f3-120">Save this connection string to use later in the tutorial.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-create/create-event-hub8.png)

<span data-ttu-id="156f3-121">Your event hub is now created, and you have the connection strings you need to send and receive events.</span><span class="sxs-lookup"><span data-stu-id="156f3-121">Your event hub is now created, and you have the connection strings you need to send and receive events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="156f3-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="156f3-122">Next steps</span></span>
<span data-ttu-id="156f3-123">To learn more about Event Hubs, visit these links:</span><span class="sxs-lookup"><span data-stu-id="156f3-123">To learn more about Event Hubs, visit these links:</span></span>

* [<span data-ttu-id="156f3-124">Event Hubs overview</span><span class="sxs-lookup"><span data-stu-id="156f3-124">Event Hubs overview</span></span>](event-hubs-overview.md)
* [<span data-ttu-id="156f3-125">Event Hubs API overview</span><span class="sxs-lookup"><span data-stu-id="156f3-125">Event Hubs API overview</span></span>](event-hubs-api-overview.md)

[Azure portal]: https://portal.azure.com/








