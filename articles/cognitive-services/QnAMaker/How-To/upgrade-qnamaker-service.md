---
title: Upgrade your QnA Maker service - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: How to upgrade your QnA Maker service
services: cognitive-services
author: nstulasi
manager: sangitap
ms.service: cognitive-services
ms.component: QnAMaker
ms.topic: article
ms.date: 05/07/2018
ms.author: saneppal
ms.openlocfilehash: e8d3713d6729c4e30da9a64a382e9d5a647dfefd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968141"
---
# <a name="upgrade-your-qna-maker-service"></a><span data-ttu-id="f4edd-103">Upgrade your QnA Maker service</span><span class="sxs-lookup"><span data-stu-id="f4edd-103">Upgrade your QnA Maker service</span></span>
<span data-ttu-id="f4edd-104">You can choose to upgrade individual components of the QnA Maker stack after the initial creation.</span><span class="sxs-lookup"><span data-stu-id="f4edd-104">You can choose to upgrade individual components of the QnA Maker stack after the initial creation.</span></span> <span data-ttu-id="f4edd-105">See the details of the dependent components and SKU selection [here](https://aka.ms/qnamaker-docs-capacity).</span><span class="sxs-lookup"><span data-stu-id="f4edd-105">See the details of the dependent components and SKU selection [here](https://aka.ms/qnamaker-docs-capacity).</span></span>

## <a name="upgrade-qna-maker-management-sku"></a><span data-ttu-id="f4edd-106">Upgrade QnA Maker Management SKU</span><span class="sxs-lookup"><span data-stu-id="f4edd-106">Upgrade QnA Maker Management SKU</span></span>
<span data-ttu-id="f4edd-107">To upgrade the QnA Maker management SKU:</span><span class="sxs-lookup"><span data-stu-id="f4edd-107">To upgrade the QnA Maker management SKU:</span></span>
1. <span data-ttu-id="f4edd-108">Go to your QnA Maker resource in the Azure portal, and select **Pricing tier**.</span><span class="sxs-lookup"><span data-stu-id="f4edd-108">Go to your QnA Maker resource in the Azure portal, and select **Pricing tier**.</span></span>

    ![QnA Maker resource](../media/qnamaker-how-to-upgrade-qnamaker/qnamaker-resource.png)

2. <span data-ttu-id="f4edd-110">Choose the appropriate SKU and press **Select**.</span><span class="sxs-lookup"><span data-stu-id="f4edd-110">Choose the appropriate SKU and press **Select**.</span></span>

    ![QnA Maker pricing](../media/qnamaker-how-to-upgrade-qnamaker/qnamaker-pricing-page.png)

## <a name="upgrade-app-service"></a><span data-ttu-id="f4edd-112">Upgrade App service</span><span class="sxs-lookup"><span data-stu-id="f4edd-112">Upgrade App service</span></span>
<span data-ttu-id="f4edd-113">You can [scale up](https://docs.microsoft.com/azure/app-service/web-sites-scale) or scale down the App service.</span><span class="sxs-lookup"><span data-stu-id="f4edd-113">You can [scale up](https://docs.microsoft.com/azure/app-service/web-sites-scale) or scale down the App service.</span></span>

1. <span data-ttu-id="f4edd-114">Go to the App service resource in the Azure portal, and select **scale up** or **scale down** options as required.</span><span class="sxs-lookup"><span data-stu-id="f4edd-114">Go to the App service resource in the Azure portal, and select **scale up** or **scale down** options as required.</span></span>

    ![QnA Maker app service scale](../media/qnamaker-how-to-upgrade-qnamaker/qnamaker-appservice-scale.png)

## <a name="upgrade-azure-search-service"></a><span data-ttu-id="f4edd-116">Upgrade Azure Search service</span><span class="sxs-lookup"><span data-stu-id="f4edd-116">Upgrade Azure Search service</span></span>
<span data-ttu-id="f4edd-117">Currently it is not possible to perform an in place upgrade of the Azure search SKU.</span><span class="sxs-lookup"><span data-stu-id="f4edd-117">Currently it is not possible to perform an in place upgrade of the Azure search SKU.</span></span> <span data-ttu-id="f4edd-118">However, you can create a new Azure search resource with the desired SKU, restore the data to the new resource, and then link it to the QnA Maker stack.</span><span class="sxs-lookup"><span data-stu-id="f4edd-118">However, you can create a new Azure search resource with the desired SKU, restore the data to the new resource, and then link it to the QnA Maker stack.</span></span>

1. <span data-ttu-id="f4edd-119">Create a new Azure search resource in the Azure portal, and choose the desired SKU.</span><span class="sxs-lookup"><span data-stu-id="f4edd-119">Create a new Azure search resource in the Azure portal, and choose the desired SKU.</span></span>

    ![QnA Maker Azure search resource](../media/qnamaker-how-to-upgrade-qnamaker/qnamaker-azuresearch-new.png)

2. <span data-ttu-id="f4edd-121">Restore the indexes from your original Azure search resource to the new one.</span><span class="sxs-lookup"><span data-stu-id="f4edd-121">Restore the indexes from your original Azure search resource to the new one.</span></span> <span data-ttu-id="f4edd-122">See the backup restore sample code [here](https://github.com/pchoudhari/QnAMakerBackupRestore).</span><span class="sxs-lookup"><span data-stu-id="f4edd-122">See the backup restore sample code [here](https://github.com/pchoudhari/QnAMakerBackupRestore).</span></span>

3. <span data-ttu-id="f4edd-123">Once the data is restored, go to your new Azure search resource, select **Keys**, and note down the **Name** and the **Admin key**.</span><span class="sxs-lookup"><span data-stu-id="f4edd-123">Once the data is restored, go to your new Azure search resource, select **Keys**, and note down the **Name** and the **Admin key**.</span></span>

    ![QnA Maker Azure search keys](../media/qnamaker-how-to-upgrade-qnamaker/qnamaker-azuresearch-keys.png)

4. <span data-ttu-id="f4edd-125">To link the new Azure search resource to the QnA Maker stack, go to the QnA Maker App service.</span><span class="sxs-lookup"><span data-stu-id="f4edd-125">To link the new Azure search resource to the QnA Maker stack, go to the QnA Maker App service.</span></span>

    ![QnA Maker appservice](../media/qnamaker-how-to-upgrade-qnamaker/qnamaker-resource-list-appservice.png)

5. <span data-ttu-id="f4edd-127">Select **Application settings** and replace the **AzureSearchName** and **AzureSearchAdminKey** fields from step 3.</span><span class="sxs-lookup"><span data-stu-id="f4edd-127">Select **Application settings** and replace the **AzureSearchName** and **AzureSearchAdminKey** fields from step 3.</span></span>

    ![QnA Maker appservice setting](../media/qnamaker-how-to-upgrade-qnamaker/qnamaker-appservice-settings.png)

6. <span data-ttu-id="f4edd-129">Restart the App service.</span><span class="sxs-lookup"><span data-stu-id="f4edd-129">Restart the App service.</span></span>

    ![QnA Maker appservice restart](../media/qnamaker-how-to-upgrade-qnamaker/qnamaker-appservice-restart.png)

## <a name="next-steps"></a><span data-ttu-id="f4edd-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="f4edd-131">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f4edd-132">Use QnA Maker API</span><span class="sxs-lookup"><span data-stu-id="f4edd-132">Use QnA Maker API</span></span>](../Quickstarts/csharp.md)
