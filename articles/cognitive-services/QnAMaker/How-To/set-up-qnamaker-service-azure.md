---
title: How to setup a QnA Maker service - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: How to setup a QnA Maker service
services: cognitive-services
author: nstulasi
manager: sangitap
ms.service: cognitive-services
ms.component: QnAMaker
ms.topic: article
ms.date: 04/21/2018
ms.author: saneppal
ms.openlocfilehash: ce452dd686529e017b4eae4717eadb044b389409
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864852"
---
# <a name="create-a-qna-maker-service"></a><span data-ttu-id="1c64d-103">Create a QnA Maker service</span><span class="sxs-lookup"><span data-stu-id="1c64d-103">Create a QnA Maker service</span></span>

<span data-ttu-id="1c64d-104">Before you can create any QnA Maker knowledge bases, you must first set up a QnA Maker service in Azure.</span><span class="sxs-lookup"><span data-stu-id="1c64d-104">Before you can create any QnA Maker knowledge bases, you must first set up a QnA Maker service in Azure.</span></span> <span data-ttu-id="1c64d-105">Anyone with authorization to create new resources in a subscription can set up a QnA Maker service.</span><span class="sxs-lookup"><span data-stu-id="1c64d-105">Anyone with authorization to create new resources in a subscription can set up a QnA Maker service.</span></span>

<span data-ttu-id="1c64d-106">This setup deploys a few Azure resources.</span><span class="sxs-lookup"><span data-stu-id="1c64d-106">This setup deploys a few Azure resources.</span></span> <span data-ttu-id="1c64d-107">Together, these resources manage the knowledge base content and provide question-answering capabilities though an endpoint.</span><span class="sxs-lookup"><span data-stu-id="1c64d-107">Together, these resources manage the knowledge base content and provide question-answering capabilities though an endpoint.</span></span>

1. <span data-ttu-id="1c64d-108">Log in to the [Azure portal](<https://portal.azure.com>).</span><span class="sxs-lookup"><span data-stu-id="1c64d-108">Log in to the [Azure portal](<https://portal.azure.com>).</span></span>

2.  <span data-ttu-id="1c64d-109">Click on **Add new resource**, and type "qna maker" in search, and select the QnA Maker resource</span><span class="sxs-lookup"><span data-stu-id="1c64d-109">Click on **Add new resource**, and type "qna maker" in search, and select the QnA Maker resource</span></span>

    ![Create a new QnA Maker service](../media/qnamaker-how-to-setup-service/create-new-resource.png)

3.  <span data-ttu-id="1c64d-111">Click on **Create** after reading the terms and conditions.</span><span class="sxs-lookup"><span data-stu-id="1c64d-111">Click on **Create** after reading the terms and conditions.</span></span>

    ![Create a new QnA Maker service](../media/qnamaker-how-to-setup-service/create-new-resource-button.png)

4. <span data-ttu-id="1c64d-113">In **QnA Maker**, select the appropriate tiers and regions.</span><span class="sxs-lookup"><span data-stu-id="1c64d-113">In **QnA Maker**, select the appropriate tiers and regions.</span></span>

    ![Create a new QnA Maker service](../media/qnamaker-how-to-setup-service/enter-qnamaker-info.png)

    * <span data-ttu-id="1c64d-115">Fill the **Name** with a unique name to identify this QnA Maker service.</span><span class="sxs-lookup"><span data-stu-id="1c64d-115">Fill the **Name** with a unique name to identify this QnA Maker service.</span></span> <span data-ttu-id="1c64d-116">This name also identifies the QnA Maker endpoint to which your knowledge bases will be associated.</span><span class="sxs-lookup"><span data-stu-id="1c64d-116">This name also identifies the QnA Maker endpoint to which your knowledge bases will be associated.</span></span>
    * <span data-ttu-id="1c64d-117">Choose the **Subscription** in which the QnA Maker resource will be deployed.</span><span class="sxs-lookup"><span data-stu-id="1c64d-117">Choose the **Subscription** in which the QnA Maker resource will be deployed.</span></span>
    * <span data-ttu-id="1c64d-118">Select the **Management pricing tier** for the QnA Maker management services (portal and management APIs).</span><span class="sxs-lookup"><span data-stu-id="1c64d-118">Select the **Management pricing tier** for the QnA Maker management services (portal and management APIs).</span></span> <span data-ttu-id="1c64d-119">See [here](https://aka.ms/qnamaker-pricing) for details on the pricing of the SKUs.</span><span class="sxs-lookup"><span data-stu-id="1c64d-119">See [here](https://aka.ms/qnamaker-pricing) for details on the pricing of the SKUs.</span></span>
    * <span data-ttu-id="1c64d-120">Create a new **Resource Group** (recommended) or use an existing one in which to deploy this QnA Maker resource.</span><span class="sxs-lookup"><span data-stu-id="1c64d-120">Create a new **Resource Group** (recommended) or use an existing one in which to deploy this QnA Maker resource.</span></span>
    * <span data-ttu-id="1c64d-121">Choose the **Search pricing tier** of the Azure Search service.</span><span class="sxs-lookup"><span data-stu-id="1c64d-121">Choose the **Search pricing tier** of the Azure Search service.</span></span> <span data-ttu-id="1c64d-122">If you see the Free tier option greyed out, it means you already have a Free Azure Search tier deployed in your subscription.</span><span class="sxs-lookup"><span data-stu-id="1c64d-122">If you see the Free tier option greyed out, it means you already have a Free Azure Search tier deployed in your subscription.</span></span> <span data-ttu-id="1c64d-123">In that case, you will need to start with the Basic Azure Search tier.</span><span class="sxs-lookup"><span data-stu-id="1c64d-123">In that case, you will need to start with the Basic Azure Search tier.</span></span> <span data-ttu-id="1c64d-124">See details of Azure search pricing [here](https://azure.microsoft.com/en-us/pricing/details/search/).</span><span class="sxs-lookup"><span data-stu-id="1c64d-124">See details of Azure search pricing [here](https://azure.microsoft.com/en-us/pricing/details/search/).</span></span>
    * <span data-ttu-id="1c64d-125">Choose the **Search Location** where you want Azure Search data to be deployed.</span><span class="sxs-lookup"><span data-stu-id="1c64d-125">Choose the **Search Location** where you want Azure Search data to be deployed.</span></span> <span data-ttu-id="1c64d-126">Restrictions in where customer data must be stored will inform the location you choose for Azure Search.</span><span class="sxs-lookup"><span data-stu-id="1c64d-126">Restrictions in where customer data must be stored will inform the location you choose for Azure Search.</span></span>
    * <span data-ttu-id="1c64d-127">Give a name to your App service in **App name**.</span><span class="sxs-lookup"><span data-stu-id="1c64d-127">Give a name to your App service in **App name**.</span></span>
    * <span data-ttu-id="1c64d-128">By default the App service defaults to the standard (S1) tier.</span><span class="sxs-lookup"><span data-stu-id="1c64d-128">By default the App service defaults to the standard (S1) tier.</span></span> <span data-ttu-id="1c64d-129">You can change the plan after creation.</span><span class="sxs-lookup"><span data-stu-id="1c64d-129">You can change the plan after creation.</span></span> <span data-ttu-id="1c64d-130">See more details of App service pricing [here](https://azure.microsoft.com/en-in/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="1c64d-130">See more details of App service pricing [here](https://azure.microsoft.com/en-in/pricing/details/app-service/).</span></span>
    * <span data-ttu-id="1c64d-131">Choose the **Website location** where the App Service will be deployed.</span><span class="sxs-lookup"><span data-stu-id="1c64d-131">Choose the **Website location** where the App Service will be deployed.</span></span>

        > [!NOTE]
        > <span data-ttu-id="1c64d-132">The Search Location can be different from the Website Location.</span><span class="sxs-lookup"><span data-stu-id="1c64d-132">The Search Location can be different from the Website Location.</span></span>

    * <span data-ttu-id="1c64d-133">Choose whether you want to enable **Application Insights** or not.</span><span class="sxs-lookup"><span data-stu-id="1c64d-133">Choose whether you want to enable **Application Insights** or not.</span></span> <span data-ttu-id="1c64d-134">If **Application Insights** is enabled, QnA Maker collects telemetry on traffic, chat logs, and errors.</span><span class="sxs-lookup"><span data-stu-id="1c64d-134">If **Application Insights** is enabled, QnA Maker collects telemetry on traffic, chat logs, and errors.</span></span>
    * <span data-ttu-id="1c64d-135">Choose the **App insights location** where Application Insights resource will be deployed.</span><span class="sxs-lookup"><span data-stu-id="1c64d-135">Choose the **App insights location** where Application Insights resource will be deployed.</span></span>

5. <span data-ttu-id="1c64d-136">Once all the fields are validated, you can click on **Create** to start deployment of these services in your subscription.</span><span class="sxs-lookup"><span data-stu-id="1c64d-136">Once all the fields are validated, you can click on **Create** to start deployment of these services in your subscription.</span></span> <span data-ttu-id="1c64d-137">It will take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="1c64d-137">It will take a few minutes to complete.</span></span>

6.  <span data-ttu-id="1c64d-138">Once the deployment is done, you will see the following resources created in your subscription.</span><span class="sxs-lookup"><span data-stu-id="1c64d-138">Once the deployment is done, you will see the following resources created in your subscription.</span></span>

    ![Create a new QnA Maker service](../media/qnamaker-how-to-setup-service/resources-created.png)

## <a name="next-steps"></a><span data-ttu-id="1c64d-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="1c64d-140">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1c64d-141">Create and publish a knowledge base</span><span class="sxs-lookup"><span data-stu-id="1c64d-141">Create and publish a knowledge base</span></span>](../Quickstarts/create-publish-knowledge-base.md)