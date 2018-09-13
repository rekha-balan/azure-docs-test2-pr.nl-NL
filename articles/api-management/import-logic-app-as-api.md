---
title: Import a Logic App as an API with the Azure portal  | Microsoft Docs
description: This tutorial shows you how to use API Management (APIM) to import Logic App as an API.
services: api-management
documentationcenter: ''
author: vladvino
manager: cfowler
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 11/22/2017
ms.author: apimpm
ms.openlocfilehash: 4b5f884fe6e1f1fdc12d7993418f7a10614a4cbe
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857615"
---
# <a name="import-a-logic-app-as-an-api"></a><span data-ttu-id="0c19c-103">Import a Logic App as an API</span><span class="sxs-lookup"><span data-stu-id="0c19c-103">Import a Logic App as an API</span></span>

<span data-ttu-id="0c19c-104">This article shows how to import a Logic App as an API.</span><span class="sxs-lookup"><span data-stu-id="0c19c-104">This article shows how to import a Logic App as an API.</span></span> <span data-ttu-id="0c19c-105">The article also shows how to test the APIM API.</span><span class="sxs-lookup"><span data-stu-id="0c19c-105">The article also shows how to test the APIM API.</span></span>

<span data-ttu-id="0c19c-106">In this article, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="0c19c-106">In this article, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0c19c-107">Import a Logic App as an API</span><span class="sxs-lookup"><span data-stu-id="0c19c-107">Import a Logic App as an API</span></span>
> * <span data-ttu-id="0c19c-108">Test the API in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="0c19c-108">Test the API in the Azure portal</span></span>
> * <span data-ttu-id="0c19c-109">Test the API in the Developer portal</span><span class="sxs-lookup"><span data-stu-id="0c19c-109">Test the API in the Developer portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c19c-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0c19c-110">Prerequisites</span></span>

+ <span data-ttu-id="0c19c-111">Complete the following quickstart: [Create an Azure API Management instance](get-started-create-service-instance.md)</span><span class="sxs-lookup"><span data-stu-id="0c19c-111">Complete the following quickstart: [Create an Azure API Management instance](get-started-create-service-instance.md)</span></span>
+ <span data-ttu-id="0c19c-112">Make sure there is a Logic App in your subscription.</span><span class="sxs-lookup"><span data-stu-id="0c19c-112">Make sure there is a Logic App in your subscription.</span></span> <span data-ttu-id="0c19c-113">For more information, [Create your first Logic App](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="0c19c-113">For more information, [Create your first Logic App](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span></span>

[!INCLUDE [api-management-navigate-to-instance.md](../../includes/api-management-navigate-to-instance.md)]

## <span data-ttu-id="0c19c-114"><a name="create-api"> </a>Import and publish a back-end API</span><span class="sxs-lookup"><span data-stu-id="0c19c-114"><a name="create-api"> </a>Import and publish a back-end API</span></span>

1. <span data-ttu-id="0c19c-115">Select **APIs** from under **API MANAGEMENT**.</span><span class="sxs-lookup"><span data-stu-id="0c19c-115">Select **APIs** from under **API MANAGEMENT**.</span></span>
2. <span data-ttu-id="0c19c-116">Select **Logic App** from the **Add a new API** list.</span><span class="sxs-lookup"><span data-stu-id="0c19c-116">Select **Logic App** from the **Add a new API** list.</span></span>

    ![Logic app](./media/import-logic-app-as-api/logic-app-api.png)
3. <span data-ttu-id="0c19c-118">Press **Browse** to see the list of Logic Apps in your subscription.</span><span class="sxs-lookup"><span data-stu-id="0c19c-118">Press **Browse** to see the list of Logic Apps in your subscription.</span></span>
4. <span data-ttu-id="0c19c-119">Select the app.</span><span class="sxs-lookup"><span data-stu-id="0c19c-119">Select the app.</span></span> <span data-ttu-id="0c19c-120">APIM finds the swagger associated with the selected app, fetches it, and imports it.</span><span class="sxs-lookup"><span data-stu-id="0c19c-120">APIM finds the swagger associated with the selected app, fetches it, and imports it.</span></span> 
5. <span data-ttu-id="0c19c-121">Add an API URL suffix.</span><span class="sxs-lookup"><span data-stu-id="0c19c-121">Add an API URL suffix.</span></span> <span data-ttu-id="0c19c-122">The suffix is a name that identifies this specific API in this APIM instance.</span><span class="sxs-lookup"><span data-stu-id="0c19c-122">The suffix is a name that identifies this specific API in this APIM instance.</span></span> <span data-ttu-id="0c19c-123">It has to be unique in this APIM instance.</span><span class="sxs-lookup"><span data-stu-id="0c19c-123">It has to be unique in this APIM instance.</span></span>
6. <span data-ttu-id="0c19c-124">Publish the API by associating the API with a product.</span><span class="sxs-lookup"><span data-stu-id="0c19c-124">Publish the API by associating the API with a product.</span></span> <span data-ttu-id="0c19c-125">In this case, the "*Unlimited*" product is used.</span><span class="sxs-lookup"><span data-stu-id="0c19c-125">In this case, the "*Unlimited*" product is used.</span></span>  <span data-ttu-id="0c19c-126">If you want for the API to be published and be available to developers, add it to a product.</span><span class="sxs-lookup"><span data-stu-id="0c19c-126">If you want for the API to be published and be available to developers, add it to a product.</span></span> <span data-ttu-id="0c19c-127">You can do it during API creation or set it later.</span><span class="sxs-lookup"><span data-stu-id="0c19c-127">You can do it during API creation or set it later.</span></span>

    <span data-ttu-id="0c19c-128">Products are associations of one or more APIs.</span><span class="sxs-lookup"><span data-stu-id="0c19c-128">Products are associations of one or more APIs.</span></span> <span data-ttu-id="0c19c-129">You can include a number of APIs and offer them to developers through the developer portal.</span><span class="sxs-lookup"><span data-stu-id="0c19c-129">You can include a number of APIs and offer them to developers through the developer portal.</span></span> <span data-ttu-id="0c19c-130">Developers must first subscribe to a product to get access to the API.</span><span class="sxs-lookup"><span data-stu-id="0c19c-130">Developers must first subscribe to a product to get access to the API.</span></span> <span data-ttu-id="0c19c-131">When they subscribe, they get a subscription key that is good for any API in that product.</span><span class="sxs-lookup"><span data-stu-id="0c19c-131">When they subscribe, they get a subscription key that is good for any API in that product.</span></span> <span data-ttu-id="0c19c-132">If you created the APIM instance, you are an administrator already, so you are subscribed to every product by default.</span><span class="sxs-lookup"><span data-stu-id="0c19c-132">If you created the APIM instance, you are an administrator already, so you are subscribed to every product by default.</span></span>

    <span data-ttu-id="0c19c-133">By default, each API Management instance comes with two sample products:</span><span class="sxs-lookup"><span data-stu-id="0c19c-133">By default, each API Management instance comes with two sample products:</span></span>

    * <span data-ttu-id="0c19c-134">**Starter**</span><span class="sxs-lookup"><span data-stu-id="0c19c-134">**Starter**</span></span>
    * <span data-ttu-id="0c19c-135">**Unlimited**</span><span class="sxs-lookup"><span data-stu-id="0c19c-135">**Unlimited**</span></span>   
7. <span data-ttu-id="0c19c-136">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="0c19c-136">Select **Create**.</span></span>

## <a name="test-the-new-apim-api-in-the-azure-portal"></a><span data-ttu-id="0c19c-137">Test the new APIM API in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="0c19c-137">Test the new APIM API in the Azure portal</span></span>

<span data-ttu-id="0c19c-138">Operations can be called directly from the Azure portal, which provides a convenient way to view and test the operations of an API.</span><span class="sxs-lookup"><span data-stu-id="0c19c-138">Operations can be called directly from the Azure portal, which provides a convenient way to view and test the operations of an API.</span></span>  

1. <span data-ttu-id="0c19c-139">Select the API you created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="0c19c-139">Select the API you created in the previous step.</span></span>
2. <span data-ttu-id="0c19c-140">Press the **Test** tab.</span><span class="sxs-lookup"><span data-stu-id="0c19c-140">Press the **Test** tab.</span></span>
3. <span data-ttu-id="0c19c-141">Select some operation.</span><span class="sxs-lookup"><span data-stu-id="0c19c-141">Select some operation.</span></span>

    <span data-ttu-id="0c19c-142">The page displays fields for query parameters and fields for the headers.</span><span class="sxs-lookup"><span data-stu-id="0c19c-142">The page displays fields for query parameters and fields for the headers.</span></span> <span data-ttu-id="0c19c-143">One of the headers is "Ocp-Apim-Subscription-Key", for the subscription key of the product that is associated with this API.</span><span class="sxs-lookup"><span data-stu-id="0c19c-143">One of the headers is "Ocp-Apim-Subscription-Key", for the subscription key of the product that is associated with this API.</span></span> <span data-ttu-id="0c19c-144">If you created the APIM instance, you are an administrator already, so the key is filled in automatically.</span><span class="sxs-lookup"><span data-stu-id="0c19c-144">If you created the APIM instance, you are an administrator already, so the key is filled in automatically.</span></span> 
1. <span data-ttu-id="0c19c-145">Press **Send**.</span><span class="sxs-lookup"><span data-stu-id="0c19c-145">Press **Send**.</span></span>

    <span data-ttu-id="0c19c-146">Backend responds with **200 OK** and some data.</span><span class="sxs-lookup"><span data-stu-id="0c19c-146">Backend responds with **200 OK** and some data.</span></span>

## <span data-ttu-id="0c19c-147"><a name="call-operation"> </a>Call an operation from the developer portal</span><span class="sxs-lookup"><span data-stu-id="0c19c-147"><a name="call-operation"> </a>Call an operation from the developer portal</span></span>

<span data-ttu-id="0c19c-148">Operations can also be called **Developer portal** to test APIs.</span><span class="sxs-lookup"><span data-stu-id="0c19c-148">Operations can also be called **Developer portal** to test APIs.</span></span> 

1. <span data-ttu-id="0c19c-149">Select the API you created in the "Import and publish a back-end API" step.</span><span class="sxs-lookup"><span data-stu-id="0c19c-149">Select the API you created in the "Import and publish a back-end API" step.</span></span>
2. <span data-ttu-id="0c19c-150">Press **Developer portal**.</span><span class="sxs-lookup"><span data-stu-id="0c19c-150">Press **Developer portal**.</span></span>

    <span data-ttu-id="0c19c-151">The "Developer portal" site opens up.</span><span class="sxs-lookup"><span data-stu-id="0c19c-151">The "Developer portal" site opens up.</span></span>
3. <span data-ttu-id="0c19c-152">Select the **API** that you created.</span><span class="sxs-lookup"><span data-stu-id="0c19c-152">Select the **API** that you created.</span></span>
4. <span data-ttu-id="0c19c-153">Click the operation you want to test.</span><span class="sxs-lookup"><span data-stu-id="0c19c-153">Click the operation you want to test.</span></span>
5. <span data-ttu-id="0c19c-154">Press **Try it**.</span><span class="sxs-lookup"><span data-stu-id="0c19c-154">Press **Try it**.</span></span>
6. <span data-ttu-id="0c19c-155">Press **Send**.</span><span class="sxs-lookup"><span data-stu-id="0c19c-155">Press **Send**.</span></span>
    
    <span data-ttu-id="0c19c-156">After an operation is invoked, the developer portal displays the **Response status**, the **Response headers**, and any **Response content**.</span><span class="sxs-lookup"><span data-stu-id="0c19c-156">After an operation is invoked, the developer portal displays the **Response status**, the **Response headers**, and any **Response content**.</span></span>

[!INCLUDE [api-management-navigate-to-instance.md](../../includes/api-management-append-apis.md)]

>[!NOTE]
> <span data-ttu-id="0c19c-157">Every Logic App has **manual-invoke** operation.</span><span class="sxs-lookup"><span data-stu-id="0c19c-157">Every Logic App has **manual-invoke** operation.</span></span> <span data-ttu-id="0c19c-158">If you want to comprise your API of multiple logic apps, in order not to have collision, you need to rename the function.</span><span class="sxs-lookup"><span data-stu-id="0c19c-158">If you want to comprise your API of multiple logic apps, in order not to have collision, you need to rename the function.</span></span>

[!INCLUDE [api-management-define-api-topics.md](../../includes/api-management-define-api-topics.md)]

## <a name="next-steps"></a><span data-ttu-id="0c19c-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="0c19c-159">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0c19c-160">Transform and protect a published API</span><span class="sxs-lookup"><span data-stu-id="0c19c-160">Transform and protect a published API</span></span>](transform-api.md)