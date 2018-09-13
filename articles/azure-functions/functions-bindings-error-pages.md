---
title: Azure Functions error handling guidance | Microsoft Docs
description: Provides general guidance for handling errors that occur in when your functions execute, and links to binding-specific errors topics.
services: functions
cloud: ''
documentationcenter: ''
author: ggailey777
manager: jeconnoc
ms.assetid: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 02/01/2018
ms.author: glenga; cfowler
ms.openlocfilehash: 5a8dae73c164b319b4c291685deff402f9798364
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869943"
---
# <a name="azure-functions-error-handling"></a><span data-ttu-id="7f4bc-103">Azure Functions error handling</span><span class="sxs-lookup"><span data-stu-id="7f4bc-103">Azure Functions error handling</span></span>

<span data-ttu-id="7f4bc-104">This topic provides general guidance for handling errors that occur when your functions execute.</span><span class="sxs-lookup"><span data-stu-id="7f4bc-104">This topic provides general guidance for handling errors that occur when your functions execute.</span></span> <span data-ttu-id="7f4bc-105">It also provides links to the topics that describe binding-specific errors that may occur.</span><span class="sxs-lookup"><span data-stu-id="7f4bc-105">It also provides links to the topics that describe binding-specific errors that may occur.</span></span> 

## <a name="handing-errors-in-functions"></a><span data-ttu-id="7f4bc-106">Handing errors in functions</span><span class="sxs-lookup"><span data-stu-id="7f4bc-106">Handing errors in functions</span></span>
[!INCLUDE [bindings errors intro](../../includes/functions-bindings-errors-intro.md)]

 
## <a name="binding-error-codes"></a><span data-ttu-id="7f4bc-107">Binding error codes</span><span class="sxs-lookup"><span data-stu-id="7f4bc-107">Binding error codes</span></span>

<span data-ttu-id="7f4bc-108">When integrating with Azure services, you may have errors raised that originate from the APIs of the underlying services.</span><span class="sxs-lookup"><span data-stu-id="7f4bc-108">When integrating with Azure services, you may have errors raised that originate from the APIs of the underlying services.</span></span> <span data-ttu-id="7f4bc-109">Links to the error code documentation for these services can be found in the **Exceptions and return codes** section of the following trigger and binding reference topics:</span><span class="sxs-lookup"><span data-stu-id="7f4bc-109">Links to the error code documentation for these services can be found in the **Exceptions and return codes** section of the following trigger and binding reference topics:</span></span>

+ [<span data-ttu-id="7f4bc-110">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7f4bc-110">Azure Cosmos DB</span></span>](functions-bindings-cosmosdb.md#exceptions-and-return-codes)

+ [<span data-ttu-id="7f4bc-111">Blob storage</span><span class="sxs-lookup"><span data-stu-id="7f4bc-111">Blob storage</span></span>](functions-bindings-storage-blob.md#exceptions-and-return-codes)

+ [<span data-ttu-id="7f4bc-112">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="7f4bc-112">Event Hubs</span></span>](functions-bindings-event-hubs.md#exceptions-and-return-codes)

+ [<span data-ttu-id="7f4bc-113">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="7f4bc-113">Notification Hubs</span></span>](functions-bindings-notification-hubs.md#exceptions-and-return-codes)

+ [<span data-ttu-id="7f4bc-114">Queue storage</span><span class="sxs-lookup"><span data-stu-id="7f4bc-114">Queue storage</span></span>](functions-bindings-storage-queue.md#exceptions-and-return-codes)

+ [<span data-ttu-id="7f4bc-115">Service Bus</span><span class="sxs-lookup"><span data-stu-id="7f4bc-115">Service Bus</span></span>](functions-bindings-service-bus.md#exceptions-and-return-codes)

+ [<span data-ttu-id="7f4bc-116">Table storage</span><span class="sxs-lookup"><span data-stu-id="7f4bc-116">Table storage</span></span>](functions-bindings-storage-table.md#exceptions-and-return-codes)
