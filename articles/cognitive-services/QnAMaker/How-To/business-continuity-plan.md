---
title: Create a business continuty plan for your QnA Maker service - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: How to create a business continuity plan for your QnA Maker service
services: cognitive-services
author: nstulasi
manager: sangitap
ms.service: cognitive-services
ms.component: QnAMaker
ms.topic: article
ms.date: 05/07/2018
ms.author: saneppal
ms.openlocfilehash: ca6e54b8a8ca8b38e8ef6b1a148f8b2c54bd43da
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867258"
---
# <a name="create-a-business-continuity-plan-for-your-qna-maker-service"></a><span data-ttu-id="5fb2d-103">Create a business continuity plan for your QnA Maker service</span><span class="sxs-lookup"><span data-stu-id="5fb2d-103">Create a business continuity plan for your QnA Maker service</span></span>

<span data-ttu-id="5fb2d-104">The primary objective of the business continuity plan is to create a resilient knowledge base endpoint, which would ensure no down time for the Bot or the application consuming it.</span><span class="sxs-lookup"><span data-stu-id="5fb2d-104">The primary objective of the business continuity plan is to create a resilient knowledge base endpoint, which would ensure no down time for the Bot or the application consuming it.</span></span>

![QnA Maker bcp plan](../media/qnamaker-how-to-bcp-plan/qnamaker-bcp-plan.png)

<span data-ttu-id="5fb2d-106">The high-level idea as represented above is as follows:</span><span class="sxs-lookup"><span data-stu-id="5fb2d-106">The high-level idea as represented above is as follows:</span></span>

1. <span data-ttu-id="5fb2d-107">Set up two parallel [QnA Maker services](../How-To/set-up-qnamaker-service-azure.md) in [Azure paired regions](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions).</span><span class="sxs-lookup"><span data-stu-id="5fb2d-107">Set up two parallel [QnA Maker services](../How-To/set-up-qnamaker-service-azure.md) in [Azure paired regions](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions).</span></span>

2. <span data-ttu-id="5fb2d-108">Keep the primary and secondary Azure search indexes in sync. Use the github sample [here](https://github.com/pchoudhari/QnAMakerBackupRestore) to see how to backup-restore Azure indexes.</span><span class="sxs-lookup"><span data-stu-id="5fb2d-108">Keep the primary and secondary Azure search indexes in sync. Use the github sample [here](https://github.com/pchoudhari/QnAMakerBackupRestore) to see how to backup-restore Azure indexes.</span></span>

3. <span data-ttu-id="5fb2d-109">Back up the Application Insights using [continuous export](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-export-telemetry).</span><span class="sxs-lookup"><span data-stu-id="5fb2d-109">Back up the Application Insights using [continuous export](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-export-telemetry).</span></span>

4. <span data-ttu-id="5fb2d-110">Once the primary and secondary stacks have been set up, use [traffic manager](https://docs.microsoft.com/en-us/azure/traffic-manager/) to configure the two endpoints and set up a routing method.</span><span class="sxs-lookup"><span data-stu-id="5fb2d-110">Once the primary and secondary stacks have been set up, use [traffic manager](https://docs.microsoft.com/en-us/azure/traffic-manager/) to configure the two endpoints and set up a routing method.</span></span>

5. <span data-ttu-id="5fb2d-111">You would need to create an SSL certificate for your traffic manager endpoint.</span><span class="sxs-lookup"><span data-stu-id="5fb2d-111">You would need to create an SSL certificate for your traffic manager endpoint.</span></span> <span data-ttu-id="5fb2d-112">[Bind the SSL certificate](https://docs.microsoft.com/en-us/azure/app-service/app-service-web-tutorial-custom-ssl) in your App services.</span><span class="sxs-lookup"><span data-stu-id="5fb2d-112">[Bind the SSL certificate](https://docs.microsoft.com/en-us/azure/app-service/app-service-web-tutorial-custom-ssl) in your App services.</span></span>

6. <span data-ttu-id="5fb2d-113">Finally, use the traffic manager endpoint in your Bot or App.</span><span class="sxs-lookup"><span data-stu-id="5fb2d-113">Finally, use the traffic manager endpoint in your Bot or App.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5fb2d-114">Next steps</span><span class="sxs-lookup"><span data-stu-id="5fb2d-114">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5fb2d-115">Choose capacity for your QnA Maker deployment</span><span class="sxs-lookup"><span data-stu-id="5fb2d-115">Choose capacity for your QnA Maker deployment</span></span>](../Tutorials/choosing-capacity-qnamaker-deployment.md)
