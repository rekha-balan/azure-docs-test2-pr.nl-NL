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
# <a name="create-a-business-continuity-plan-for-your-qna-maker-service"></a>Create a business continuity plan for your QnA Maker service

The primary objective of the business continuity plan is to create a resilient knowledge base endpoint, which would ensure no down time for the Bot or the application consuming it.

![QnA Maker bcp plan](../media/qnamaker-how-to-bcp-plan/qnamaker-bcp-plan.png)

The high-level idea as represented above is as follows:

1. Set up two parallel [QnA Maker services](../How-To/set-up-qnamaker-service-azure.md) in [Azure paired regions](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions).

2. Keep the primary and secondary Azure search indexes in sync. Use the github sample [here](https://github.com/pchoudhari/QnAMakerBackupRestore) to see how to backup-restore Azure indexes.

3. Back up the Application Insights using [continuous export](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-export-telemetry).

4. Once the primary and secondary stacks have been set up, use [traffic manager](https://docs.microsoft.com/en-us/azure/traffic-manager/) to configure the two endpoints and set up a routing method.

5. You would need to create an SSL certificate for your traffic manager endpoint. [Bind the SSL certificate](https://docs.microsoft.com/en-us/azure/app-service/app-service-web-tutorial-custom-ssl) in your App services.

6. Finally, use the traffic manager endpoint in your Bot or App.

## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"]
> [Choose capacity for your QnA Maker deployment](../Tutorials/choosing-capacity-qnamaker-deployment.md)