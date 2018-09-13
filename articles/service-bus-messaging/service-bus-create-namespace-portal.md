---
title: Create a Service Bus namespace in the Azure portal | Microsoft Docs
description: How to create a Service Bus namespace using the Azure portal.
services: service-bus-messaging
documentationcenter: .net
author: jtaubensee
manager: timlt
editor: ''
ms.assetid: fbb10e62-b133-4851-9d27-40bd844db3ba
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 03/23/2017
ms.author: jotaub
ms.openlocfilehash: 5de92033eb7eb4fef8d27a215b3284ab80594065
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563621"
---
# <a name="create-a-service-bus-namespace-using-the-azure-portal"></a><span data-ttu-id="4a7a6-103">Create a Service Bus namespace using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="4a7a6-103">Create a Service Bus namespace using the Azure portal</span></span>
<span data-ttu-id="4a7a6-104">A namespace is a common container for all messaging components.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-104">A namespace is a common container for all messaging components.</span></span> <span data-ttu-id="4a7a6-105">Multiple queues and topics can reside within a single namespace, and namespaces often serve as application containers.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-105">Multiple queues and topics can reside within a single namespace, and namespaces often serve as application containers.</span></span> <span data-ttu-id="4a7a6-106">There are two different ways to create a Service Bus namespace:</span><span class="sxs-lookup"><span data-stu-id="4a7a6-106">There are two different ways to create a Service Bus namespace:</span></span>

1. <span data-ttu-id="4a7a6-107">Azure portal (this article)</span><span class="sxs-lookup"><span data-stu-id="4a7a6-107">Azure portal (this article)</span></span>
2. <span data-ttu-id="4a7a6-108">[Resource Manager templates][create-namespace-using-arm]</span><span class="sxs-lookup"><span data-stu-id="4a7a6-108">[Resource Manager templates][create-namespace-using-arm]</span></span>

## <a name="create-a-namespace-in-the-azure-portal"></a><span data-ttu-id="4a7a6-109">Create a namespace in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="4a7a6-109">Create a namespace in the Azure portal</span></span>
[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

<span data-ttu-id="4a7a6-110">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="4a7a6-110">Congratulations!</span></span> <span data-ttu-id="4a7a6-111">You have now created a Service Bus Messaging namespace.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-111">You have now created a Service Bus Messaging namespace.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a7a6-112">Next steps</span><span class="sxs-lookup"><span data-stu-id="4a7a6-112">Next steps</span></span>
<span data-ttu-id="4a7a6-113">Check out our [GitHub samples][github-samples] which show some of the more advanced features of Azure Service Bus Messaging.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-113">Check out our [GitHub samples][github-samples] which show some of the more advanced features of Azure Service Bus Messaging.</span></span>

[create-namespace-using-arm]: service-bus-resource-manager-overview.md
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
