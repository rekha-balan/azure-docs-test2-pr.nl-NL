---
title: Scheduler Limits and Defaults
description: Scheduler Limits and Defaults
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: ''
ms.assetid: 88f4a3e9-6dbd-4943-8543-f0649d423061
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: db6b1c196cb468f41c7a7ce34758de346b522abb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563057"
---
# <a name="scheduler-limits-and-defaults"></a>Scheduler Limits and Defaults
## <a name="scheduler-quotas-limits-defaults-and-throttles"></a>Scheduler Quotas, Limits, Defaults, and Throttles
[!INCLUDE [scheduler-limits-table](../../includes/scheduler-limits-table.md)]

## <a name="the-x-ms-request-id-header"></a>The x-ms-request-id Header
Every request made against the Scheduler service returns a response header named**x-ms-request-id**. This header contains an opaque value that uniquely identifies the request.

If a request is consistently failing and you have verified that the request is properly formulated, you may use this value to report the error to Microsoft. In your report, include the value of x-ms-request-id, the approximate time that the request was made, the identifier of the subscription, job collection, and/or job, and the type of operation that the request attempted.

## <a name="see-also"></a>See Also
 [What is Scheduler?](scheduler-intro.md)

 [Azure Scheduler concepts, terminology, and entity hierarchy](scheduler-concepts-terms.md)

 [Get started using Scheduler in the Azure portal](scheduler-get-started-portal.md)

 [Plans and billing in Azure Scheduler](scheduler-plans-billing.md)

 [Azure Scheduler REST API reference](https://msdn.microsoft.com/library/mt629143)

 [Azure Scheduler PowerShell cmdlets reference](scheduler-powershell-reference.md)

 [Azure Scheduler high-availability and reliability](scheduler-high-availability-reliability.md)

 [Azure Scheduler outbound authentication](scheduler-outbound-authentication.md)

