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
# <a name="scheduler-limits-and-defaults"></a><span data-ttu-id="d2b87-103">Scheduler Limits and Defaults</span><span class="sxs-lookup"><span data-stu-id="d2b87-103">Scheduler Limits and Defaults</span></span>
## <a name="scheduler-quotas-limits-defaults-and-throttles"></a><span data-ttu-id="d2b87-104">Scheduler Quotas, Limits, Defaults, and Throttles</span><span class="sxs-lookup"><span data-stu-id="d2b87-104">Scheduler Quotas, Limits, Defaults, and Throttles</span></span>
[!INCLUDE [scheduler-limits-table](../../includes/scheduler-limits-table.md)]

## <a name="the-x-ms-request-id-header"></a><span data-ttu-id="d2b87-105">The x-ms-request-id Header</span><span class="sxs-lookup"><span data-stu-id="d2b87-105">The x-ms-request-id Header</span></span>
<span data-ttu-id="d2b87-106">Every request made against the Scheduler service returns a response header named**x-ms-request-id**. This header contains an opaque value that uniquely identifies the request.</span><span class="sxs-lookup"><span data-stu-id="d2b87-106">Every request made against the Scheduler service returns a response header named**x-ms-request-id**. This header contains an opaque value that uniquely identifies the request.</span></span>

<span data-ttu-id="d2b87-107">If a request is consistently failing and you have verified that the request is properly formulated, you may use this value to report the error to Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d2b87-107">If a request is consistently failing and you have verified that the request is properly formulated, you may use this value to report the error to Microsoft.</span></span> <span data-ttu-id="d2b87-108">In your report, include the value of x-ms-request-id, the approximate time that the request was made, the identifier of the subscription, job collection, and/or job, and the type of operation that the request attempted.</span><span class="sxs-lookup"><span data-stu-id="d2b87-108">In your report, include the value of x-ms-request-id, the approximate time that the request was made, the identifier of the subscription, job collection, and/or job, and the type of operation that the request attempted.</span></span>

## <a name="see-also"></a><span data-ttu-id="d2b87-109">See Also</span><span class="sxs-lookup"><span data-stu-id="d2b87-109">See Also</span></span>
 [<span data-ttu-id="d2b87-110">What is Scheduler?</span><span class="sxs-lookup"><span data-stu-id="d2b87-110">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="d2b87-111">Azure Scheduler concepts, terminology, and entity hierarchy</span><span class="sxs-lookup"><span data-stu-id="d2b87-111">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="d2b87-112">Get started using Scheduler in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d2b87-112">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="d2b87-113">Plans and billing in Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="d2b87-113">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="d2b87-114">Azure Scheduler REST API reference</span><span class="sxs-lookup"><span data-stu-id="d2b87-114">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="d2b87-115">Azure Scheduler PowerShell cmdlets reference</span><span class="sxs-lookup"><span data-stu-id="d2b87-115">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="d2b87-116">Azure Scheduler high-availability and reliability</span><span class="sxs-lookup"><span data-stu-id="d2b87-116">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="d2b87-117">Azure Scheduler outbound authentication</span><span class="sxs-lookup"><span data-stu-id="d2b87-117">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

