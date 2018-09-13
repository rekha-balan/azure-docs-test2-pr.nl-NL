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
# <a name="create-an-event-hubs-namespace-and-an-event-hub-using-the-azure-portal"></a>Create an Event Hubs namespace and an event hub using the Azure portal

## <a name="create-an-event-hubs-namespace"></a>Create an Event Hubs namespace
1. Log on to the [Azure portal][Azure portal], and click **New** at the top left of the screen.
1. Click **Internet of Things**, and then click **Event Hubs**.
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-create/create-event-hub9.png)
1. In the **Create namespace** blade, enter a namespace name. The system immediately checks to see if the name is available.
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-create/create-event-hub1.png)
1. After making sure the namespace name is available, choose the pricing tier (Basic or Standard). Also, choose an Azure subscription, resource group, and location in which to create the resource. 
1. Click **Create** to create the namespace.
1. In the Event Hubs namespace list, click the newly-created namespace.      
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-create/create-event-hub2.png)
1. In the namespace blade, click **Event Hubs**.
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-create/create-event-hub3.png)

## <a name="create-an-event-hub"></a>Create an event hub

1. At the top of the blade, click **Add Event Hub**.
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-create/create-event-hub4.png)
1. Type a name for your event hub, then click **Create**.
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-create/create-event-hub5.png)
1. In the list of event hubs, click the newly created event hub name. 
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-create/create-event-hub6.png)
1. Back in the namespace blade (not the specific event hub blade), click **Shared access policies**, and then click **RootManageSharedAccessKey**.
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-create/create-event-hub7.png)
1. Click the copy button to copy the **RootManageSharedAccessKey** connection string to the clipboard. Save this connection string to use later in the tutorial.
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-create/create-event-hub8.png)

Your event hub is now created, and you have the connection strings you need to send and receive events.

## <a name="next-steps"></a>Next steps
To learn more about Event Hubs, visit these links:

* [Event Hubs overview](event-hubs-overview.md)
* [Event Hubs API overview](event-hubs-api-overview.md)

[Azure portal]: https://portal.azure.com/








