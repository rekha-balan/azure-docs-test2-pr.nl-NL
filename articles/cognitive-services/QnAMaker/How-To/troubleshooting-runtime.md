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
# <a name="qnamaker-troubleshooting"></a><span data-ttu-id="38db0-103">QnAMaker Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="38db0-103">QnAMaker Troubleshooting</span></span>
<span data-ttu-id="38db0-104">QnAMaker comprises of components hosted in the user's Azure account.</span><span class="sxs-lookup"><span data-stu-id="38db0-104">QnAMaker comprises of components hosted in the user's Azure account.</span></span> <span data-ttu-id="38db0-105">Debugging may require users to manipulate their QnAMaker Azure resources or provide QnAMaker support team with additional information about their setup.</span><span class="sxs-lookup"><span data-stu-id="38db0-105">Debugging may require users to manipulate their QnAMaker Azure resources or provide QnAMaker support team with additional information about their setup.</span></span>

## <a name="how-to-get-latest-qnamaker-runtime-updates"></a><span data-ttu-id="38db0-106">How to get latest QnAMaker runtime updates</span><span class="sxs-lookup"><span data-stu-id="38db0-106">How to get latest QnAMaker runtime updates</span></span>
<span data-ttu-id="38db0-107">QnAMaker runtime is part of the Azure App Service deployed when you [create a QnAMaker service](./set-up-qnamaker-service-azure.md) in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="38db0-107">QnAMaker runtime is part of the Azure App Service deployed when you [create a QnAMaker service](./set-up-qnamaker-service-azure.md) in Azure portal.</span></span> <span data-ttu-id="38db0-108">Updates are made periodically to the runtime.</span><span class="sxs-lookup"><span data-stu-id="38db0-108">Updates are made periodically to the runtime.</span></span> <span data-ttu-id="38db0-109">To apply the latest updates to apply to your QnAMaker setup, you must restart the App Service.</span><span class="sxs-lookup"><span data-stu-id="38db0-109">To apply the latest updates to apply to your QnAMaker setup, you must restart the App Service.</span></span>
1. <span data-ttu-id="38db0-110">Go to your QnAMaker service (resource group) in the [Azure portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="38db0-110">Go to your QnAMaker service (resource group) in the [Azure portal](https://portal.azure.com)</span></span>

    ![QnAMaker Azure resource group](../media/qnamaker-how-to-troubleshoot/qnamaker-azure-resourcegroup.png)

2. <span data-ttu-id="38db0-112">Click on the App Service and open the Overview section</span><span class="sxs-lookup"><span data-stu-id="38db0-112">Click on the App Service and open the Overview section</span></span>

     ![QnAMaker App Service](../media/qnamaker-how-to-troubleshoot/qnamaker-azure-appservice.png)

3. <span data-ttu-id="38db0-114">Restart the App service.</span><span class="sxs-lookup"><span data-stu-id="38db0-114">Restart the App service.</span></span> <span data-ttu-id="38db0-115">It should complete within a couple of seconds.</span><span class="sxs-lookup"><span data-stu-id="38db0-115">It should complete within a couple of seconds.</span></span> <span data-ttu-id="38db0-116">Note that your downstream applications/bots build on this QnAMaker service will be unavailable to end-users during this restart period.</span><span class="sxs-lookup"><span data-stu-id="38db0-116">Note that your downstream applications/bots build on this QnAMaker service will be unavailable to end-users during this restart period.</span></span>

    ![QnAMaker appservice restart](../media/qnamaker-how-to-upgrade-qnamaker/qnamaker-appservice-restart.png)

## <a name="how-to-get-the-qnamaker-service-hostname"></a><span data-ttu-id="38db0-118">How to get the QnAMaker service hostname</span><span class="sxs-lookup"><span data-stu-id="38db0-118">How to get the QnAMaker service hostname</span></span>
<span data-ttu-id="38db0-119">QnAMaker service hostname is useful for debugging purposes when you contact QnAMaker Support or UserVoice.</span><span class="sxs-lookup"><span data-stu-id="38db0-119">QnAMaker service hostname is useful for debugging purposes when you contact QnAMaker Support or UserVoice.</span></span> <span data-ttu-id="38db0-120">The hostname is a URL of this form: https://*{hostname}*.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="38db0-120">The hostname is a URL of this form: https://*{hostname}*.azurewebsites.net.</span></span>
    
1. <span data-ttu-id="38db0-121">Go to your QnAMaker service (resource group) in the [Azure portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="38db0-121">Go to your QnAMaker service (resource group) in the [Azure portal](https://portal.azure.com)</span></span>

    ![QnAMaker Azure resource group](../media/qnamaker-how-to-troubleshoot/qnamaker-azure-resourcegroup.png)

2. <span data-ttu-id="38db0-123">Click on the App Service</span><span class="sxs-lookup"><span data-stu-id="38db0-123">Click on the App Service</span></span>

     ![QnAMaker App Service](../media/qnamaker-how-to-troubleshoot/qnamaker-azure-appservice.png)

3. <span data-ttu-id="38db0-125">The hostname URL is available in the Overview section</span><span class="sxs-lookup"><span data-stu-id="38db0-125">The hostname URL is available in the Overview section</span></span>

    ![QnAMaker hostname](../media/qnamaker-how-to-troubleshoot/qnamaker-azure-gethostname.png)
    

## <a name="next-steps"></a><span data-ttu-id="38db0-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="38db0-127">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="38db0-128">Use QnAMaker API</span><span class="sxs-lookup"><span data-stu-id="38db0-128">Use QnAMaker API</span></span>](./upgrade-qnamaker-service.md)
