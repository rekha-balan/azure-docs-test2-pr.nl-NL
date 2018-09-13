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
# <a name="create-a-service-bus-namespace-using-the-azure-portal"></a>Create a Service Bus namespace using the Azure portal
A namespace is a common container for all messaging components. Multiple queues and topics can reside within a single namespace, and namespaces often serve as application containers. There are two different ways to create a Service Bus namespace:

1. Azure portal (this article)
2. [Resource Manager templates][create-namespace-using-arm]

## <a name="create-a-namespace-in-the-azure-portal"></a>Create a namespace in the Azure portal
[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

Congratulations! You have now created a Service Bus Messaging namespace.

## <a name="next-steps"></a>Next steps
Check out our [GitHub samples][github-samples] which show some of the more advanced features of Azure Service Bus Messaging.

[create-namespace-using-arm]: service-bus-resource-manager-overview.md
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
