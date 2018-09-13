---
title: include file
description: include file
services: functions
author: tdykstra
manager: cfowler
ms.service: functions
ms.topic: include
ms.date: 05/23/2018
ms.author: tdykstra
ms.custom: include file
ms.openlocfilehash: a7ed3be6f3161b2152f88956b3eafe92232043aa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865559"
---
<span data-ttu-id="d0a00-103">The following table lists the trigger and binding attributes that are available in an Azure Functions class library project.</span><span class="sxs-lookup"><span data-stu-id="d0a00-103">The following table lists the trigger and binding attributes that are available in an Azure Functions class library project.</span></span> <span data-ttu-id="d0a00-104">All attributes are in the namespace `Microsoft.Azure.WebJobs`.</span><span class="sxs-lookup"><span data-stu-id="d0a00-104">All attributes are in the namespace `Microsoft.Azure.WebJobs`.</span></span>

| <span data-ttu-id="d0a00-105">Trigger</span><span class="sxs-lookup"><span data-stu-id="d0a00-105">Trigger</span></span> | <span data-ttu-id="d0a00-106">Input</span><span class="sxs-lookup"><span data-stu-id="d0a00-106">Input</span></span> | <span data-ttu-id="d0a00-107">Output</span><span class="sxs-lookup"><span data-stu-id="d0a00-107">Output</span></span>|
|------   | ------    | ------  |
| [<span data-ttu-id="d0a00-108">BlobTrigger</span><span class="sxs-lookup"><span data-stu-id="d0a00-108">BlobTrigger</span></span>](../articles/azure-functions/functions-bindings-storage-blob.md#trigger---attributes)| [<span data-ttu-id="d0a00-109">Blob</span><span class="sxs-lookup"><span data-stu-id="d0a00-109">Blob</span></span>](../articles/azure-functions/functions-bindings-storage-blob.md#input---attributes)| [<span data-ttu-id="d0a00-110">Blob</span><span class="sxs-lookup"><span data-stu-id="d0a00-110">Blob</span></span>](../articles/azure-functions/functions-bindings-storage-blob.md#output---attributes)|
| [<span data-ttu-id="d0a00-111">CosmosDBTrigger</span><span class="sxs-lookup"><span data-stu-id="d0a00-111">CosmosDBTrigger</span></span>](../articles/azure-functions/functions-bindings-cosmosdb.md#trigger---attributes)| [<span data-ttu-id="d0a00-112">DocumentDB</span><span class="sxs-lookup"><span data-stu-id="d0a00-112">DocumentDB</span></span>](../articles/azure-functions/functions-bindings-cosmosdb.md#input---attributes)| [<span data-ttu-id="d0a00-113">DocumentDB</span><span class="sxs-lookup"><span data-stu-id="d0a00-113">DocumentDB</span></span>](../articles/azure-functions/functions-bindings-cosmosdb.md#output---attributes) |
| [<span data-ttu-id="d0a00-114">EventHubTrigger</span><span class="sxs-lookup"><span data-stu-id="d0a00-114">EventHubTrigger</span></span>](../articles/azure-functions/functions-bindings-event-hubs.md#trigger---attributes)|| [<span data-ttu-id="d0a00-115">EventHub</span><span class="sxs-lookup"><span data-stu-id="d0a00-115">EventHub</span></span>](../articles/azure-functions/functions-bindings-event-hubs.md#output---attributes) |
| [<span data-ttu-id="d0a00-116">HTTPTrigger</span><span class="sxs-lookup"><span data-stu-id="d0a00-116">HTTPTrigger</span></span>](../articles/azure-functions/functions-bindings-http-webhook.md#trigger---attributes)|||
| [<span data-ttu-id="d0a00-117">QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="d0a00-117">QueueTrigger</span></span>](../articles/azure-functions/functions-bindings-storage-queue.md#trigger---attributes)|| [<span data-ttu-id="d0a00-118">Queue</span><span class="sxs-lookup"><span data-stu-id="d0a00-118">Queue</span></span>](../articles/azure-functions/functions-bindings-storage-queue.md#output---attributes) |
| [<span data-ttu-id="d0a00-119">ServiceBusTrigger</span><span class="sxs-lookup"><span data-stu-id="d0a00-119">ServiceBusTrigger</span></span>](../articles/azure-functions/functions-bindings-service-bus.md#trigger---attributes)|| [<span data-ttu-id="d0a00-120">ServiceBus</span><span class="sxs-lookup"><span data-stu-id="d0a00-120">ServiceBus</span></span>](../articles/azure-functions/functions-bindings-service-bus.md#output---attributes) |
| [<span data-ttu-id="d0a00-121">TimerTrigger</span><span class="sxs-lookup"><span data-stu-id="d0a00-121">TimerTrigger</span></span>](../articles/azure-functions/functions-bindings-timer.md#attributes) | ||
| |[<span data-ttu-id="d0a00-122">ApiHubFile</span><span class="sxs-lookup"><span data-stu-id="d0a00-122">ApiHubFile</span></span>](../articles/azure-functions/functions-bindings-external-file.md)| [<span data-ttu-id="d0a00-123">ApiHubFile</span><span class="sxs-lookup"><span data-stu-id="d0a00-123">ApiHubFile</span></span>](../articles/azure-functions/functions-bindings-external-file.md)|
| |[<span data-ttu-id="d0a00-124">MobileTable</span><span class="sxs-lookup"><span data-stu-id="d0a00-124">MobileTable</span></span>](../articles/azure-functions/functions-bindings-mobile-apps.md#input---attributes)| [<span data-ttu-id="d0a00-125">MobileTable</span><span class="sxs-lookup"><span data-stu-id="d0a00-125">MobileTable</span></span>](../articles/azure-functions/functions-bindings-mobile-apps.md#output---attributes) | 
| |[<span data-ttu-id="d0a00-126">Table</span><span class="sxs-lookup"><span data-stu-id="d0a00-126">Table</span></span>](../articles/azure-functions/functions-bindings-storage-table.md#input---attributes)| [<span data-ttu-id="d0a00-127">Table</span><span class="sxs-lookup"><span data-stu-id="d0a00-127">Table</span></span>](../articles/azure-functions/functions-bindings-storage-table.md#output---attributes)  | 
| ||[<span data-ttu-id="d0a00-128">NotificationHub</span><span class="sxs-lookup"><span data-stu-id="d0a00-128">NotificationHub</span></span>](../articles/azure-functions/functions-bindings-notification-hubs.md#attributes) |
| ||[<span data-ttu-id="d0a00-129">SendGrid</span><span class="sxs-lookup"><span data-stu-id="d0a00-129">SendGrid</span></span>](../articles/azure-functions/functions-bindings-sendgrid.md#attributes) |
| ||[<span data-ttu-id="d0a00-130">Twilio</span><span class="sxs-lookup"><span data-stu-id="d0a00-130">Twilio</span></span>](../articles/azure-functions/functions-bindings-twilio.md#attributes)| 