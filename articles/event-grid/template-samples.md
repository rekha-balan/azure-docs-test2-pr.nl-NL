---
title: Azure Resource Manager template samples - Event Grid | Microsoft Docs
description: Azure Resource Manager template samples for Event Grid
services: event-grid
author: tfitzmac
manager: timlt
ms.service: event-grid
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.date: 03/27/2018
ms.author: tomfitz
ms.openlocfilehash: f4d6a663b4e0d2c2166028051e713668534b20bc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967985"
---
# <a name="azure-resource-manager-templates-for-event-grid"></a><span data-ttu-id="0cea5-103">Azure Resource Manager templates for Event Grid</span><span class="sxs-lookup"><span data-stu-id="0cea5-103">Azure Resource Manager templates for Event Grid</span></span>

<span data-ttu-id="0cea5-104">The following table includes links to Azure Resource Manager templates for Event Grid.</span><span class="sxs-lookup"><span data-stu-id="0cea5-104">The following table includes links to Azure Resource Manager templates for Event Grid.</span></span>

| | |
|-|-|
|<span data-ttu-id="0cea5-105">**Event Grid subscriptions**</span><span class="sxs-lookup"><span data-stu-id="0cea5-105">**Event Grid subscriptions**</span></span>||
| [<span data-ttu-id="0cea5-106">Custom topic and subscription with WebHook endpoint</span><span class="sxs-lookup"><span data-stu-id="0cea5-106">Custom topic and subscription with WebHook endpoint</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-event-grid)| <span data-ttu-id="0cea5-107">Deploys an Event Grid custom topic.</span><span class="sxs-lookup"><span data-stu-id="0cea5-107">Deploys an Event Grid custom topic.</span></span> <span data-ttu-id="0cea5-108">Creates a subscription to that custom topic that uses a WebHook endpoint.</span><span class="sxs-lookup"><span data-stu-id="0cea5-108">Creates a subscription to that custom topic that uses a WebHook endpoint.</span></span> |
| [<span data-ttu-id="0cea5-109">Custom topic subscription with EventHub endpoint</span><span class="sxs-lookup"><span data-stu-id="0cea5-109">Custom topic subscription with EventHub endpoint</span></span>](https://github.com/Azure/azure-docs-json-samples/blob/master/event-grid/subscribeCustomTopicToEventHub.json)| <span data-ttu-id="0cea5-110">Creates an Event Grid subscription to a custom topic that already exists.</span><span class="sxs-lookup"><span data-stu-id="0cea5-110">Creates an Event Grid subscription to a custom topic that already exists.</span></span> <span data-ttu-id="0cea5-111">The subscription uses an Event Hub for the endpoint.</span><span class="sxs-lookup"><span data-stu-id="0cea5-111">The subscription uses an Event Hub for the endpoint.</span></span> |
| [<span data-ttu-id="0cea5-112">Resource group subscription</span><span class="sxs-lookup"><span data-stu-id="0cea5-112">Resource group subscription</span></span>](https://github.com/Azure/azure-docs-json-samples/blob/master/event-grid/subscribeResourceGroupToWebHook.json)| <span data-ttu-id="0cea5-113">Subscribes to events for a resource group.</span><span class="sxs-lookup"><span data-stu-id="0cea5-113">Subscribes to events for a resource group.</span></span> <span data-ttu-id="0cea5-114">The resource group you specify as the target during deployment is the source of events.</span><span class="sxs-lookup"><span data-stu-id="0cea5-114">The resource group you specify as the target during deployment is the source of events.</span></span> <span data-ttu-id="0cea5-115">The subscription uses an Event Hub for the endpoint.</span><span class="sxs-lookup"><span data-stu-id="0cea5-115">The subscription uses an Event Hub for the endpoint.</span></span> |
| [<span data-ttu-id="0cea5-116">Blob storage account and subscription</span><span class="sxs-lookup"><span data-stu-id="0cea5-116">Blob storage account and subscription</span></span>](https://github.com/Azure/azure-docs-json-samples/blob/master/event-grid/createBlobAndSubscribe.json)| <span data-ttu-id="0cea5-117">Deploys an Azure Blob storage account and subscribes to events for that storage account.</span><span class="sxs-lookup"><span data-stu-id="0cea5-117">Deploys an Azure Blob storage account and subscribes to events for that storage account.</span></span> |
| | |
