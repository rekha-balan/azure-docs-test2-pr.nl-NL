---
title: QnAMaker troubleshooting | Microsoft Docs
titleSuffix: Azure
description: How to troubleshoot your QnAMaker runtime
services: cognitive-services
author: nstulasi
manager: sangitap
ms.service: cognitive-services
ms.component: QnAMaker
ms.topic: article
ms.date: 06/04/2018
ms.author: saneppal
ms.openlocfilehash: 23847c81a39ea392b6e64575406c9dc338b852de
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865859"
---
# <a name="qnamaker-troubleshooting"></a>QnAMaker Troubleshooting
QnAMaker comprises of components hosted in the user's Azure account. Debugging may require users to manipulate their QnAMaker Azure resources or provide QnAMaker support team with additional information about their setup.

## <a name="how-to-get-latest-qnamaker-runtime-updates"></a>How to get latest QnAMaker runtime updates
QnAMaker runtime is part of the Azure App Service deployed when you [create a QnAMaker service](./set-up-qnamaker-service-azure.md) in Azure portal. Updates are made periodically to the runtime. To apply the latest updates to apply to your QnAMaker setup, you must restart the App Service.
1. Go to your QnAMaker service (resource group) in the [Azure portal](https://portal.azure.com)

    ![QnAMaker Azure resource group](../media/qnamaker-how-to-troubleshoot/qnamaker-azure-resourcegroup.png)

2. Click on the App Service and open the Overview section

     ![QnAMaker App Service](../media/qnamaker-how-to-troubleshoot/qnamaker-azure-appservice.png)

3. Restart the App service. It should complete within a couple of seconds. Note that your downstream applications/bots build on this QnAMaker service will be unavailable to end-users during this restart period.

    ![QnAMaker appservice restart](../media/qnamaker-how-to-upgrade-qnamaker/qnamaker-appservice-restart.png)

## <a name="how-to-get-the-qnamaker-service-hostname"></a>How to get the QnAMaker service hostname
QnAMaker service hostname is useful for debugging purposes when you contact QnAMaker Support or UserVoice. The hostname is a URL of this form: https://*{hostname}*.azurewebsites.net.
    
1. Go to your QnAMaker service (resource group) in the [Azure portal](https://portal.azure.com)

    ![QnAMaker Azure resource group](../media/qnamaker-how-to-troubleshoot/qnamaker-azure-resourcegroup.png)

2. Click on the App Service

     ![QnAMaker App Service](../media/qnamaker-how-to-troubleshoot/qnamaker-azure-appservice.png)

3. The hostname URL is available in the Overview section

    ![QnAMaker hostname](../media/qnamaker-how-to-troubleshoot/qnamaker-azure-gethostname.png)
    

## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"]
> [Use QnAMaker API](./upgrade-qnamaker-service.md)
