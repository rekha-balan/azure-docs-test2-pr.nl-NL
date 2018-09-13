---
title: Import a SOAP API and convert to REST using the Azure portal | Microsoft Docs
description: Learn how to import a SOAP API and convert it to REST with API Management.
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
ms.openlocfilehash: 940756917c8f377e7d134818409e6287a4031e15
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870948"
---
# <a name="import-a-soap-api-and-convert-to-rest"></a><span data-ttu-id="2553f-103">Import a SOAP API and convert to REST</span><span class="sxs-lookup"><span data-stu-id="2553f-103">Import a SOAP API and convert to REST</span></span>

<span data-ttu-id="2553f-104">This article shows how to import a SOAP API and convert it to REST.</span><span class="sxs-lookup"><span data-stu-id="2553f-104">This article shows how to import a SOAP API and convert it to REST.</span></span> <span data-ttu-id="2553f-105">The article also shows how to test the APIM API.</span><span class="sxs-lookup"><span data-stu-id="2553f-105">The article also shows how to test the APIM API.</span></span>

<span data-ttu-id="2553f-106">In this article, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="2553f-106">In this article, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2553f-107">Import a SOAP API and convert to REST</span><span class="sxs-lookup"><span data-stu-id="2553f-107">Import a SOAP API and convert to REST</span></span>
> * <span data-ttu-id="2553f-108">Test the API in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="2553f-108">Test the API in the Azure portal</span></span>
> * <span data-ttu-id="2553f-109">Test the API in the Developer portal</span><span class="sxs-lookup"><span data-stu-id="2553f-109">Test the API in the Developer portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2553f-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2553f-110">Prerequisites</span></span>

<span data-ttu-id="2553f-111">Complete the following quickstart: [Create an Azure API Management instance](get-started-create-service-instance.md)</span><span class="sxs-lookup"><span data-stu-id="2553f-111">Complete the following quickstart: [Create an Azure API Management instance](get-started-create-service-instance.md)</span></span>

[!INCLUDE [api-management-navigate-to-instance.md](../../includes/api-management-navigate-to-instance.md)]

## <span data-ttu-id="2553f-112"><a name="create-api"> </a>Import and publish a back-end API</span><span class="sxs-lookup"><span data-stu-id="2553f-112"><a name="create-api"> </a>Import and publish a back-end API</span></span>

1. <span data-ttu-id="2553f-113">Select **APIs** from under **API MANAGEMENT**.</span><span class="sxs-lookup"><span data-stu-id="2553f-113">Select **APIs** from under **API MANAGEMENT**.</span></span>
2. <span data-ttu-id="2553f-114">Select **WSDL** from the **Add a new API** list.</span><span class="sxs-lookup"><span data-stu-id="2553f-114">Select **WSDL** from the **Add a new API** list.</span></span>

    ![SOAP API](./media/restify-soap-api/wsdl-api.png)
3. <span data-ttu-id="2553f-116">In the **WSDL specification**, enter the URL to where your SOAP API resides.</span><span class="sxs-lookup"><span data-stu-id="2553f-116">In the **WSDL specification**, enter the URL to where your SOAP API resides.</span></span>
4. <span data-ttu-id="2553f-117">Click **SOAP to REST** radio button.</span><span class="sxs-lookup"><span data-stu-id="2553f-117">Click **SOAP to REST** radio button.</span></span> <span data-ttu-id="2553f-118">When this option is clicked, APIM attempts to make an automatic transformation between XML and JSON.</span><span class="sxs-lookup"><span data-stu-id="2553f-118">When this option is clicked, APIM attempts to make an automatic transformation between XML and JSON.</span></span> <span data-ttu-id="2553f-119">In this case consumers should be calling the API as a restful API, which returns JSON.</span><span class="sxs-lookup"><span data-stu-id="2553f-119">In this case consumers should be calling the API as a restful API, which returns JSON.</span></span> <span data-ttu-id="2553f-120">APIM is converting each request into a SOAP call.</span><span class="sxs-lookup"><span data-stu-id="2553f-120">APIM is converting each request into a SOAP call.</span></span>

    ![SOAP to REST](./media/restify-soap-api/soap-to-rest.png)

5. <span data-ttu-id="2553f-122">Press tab.</span><span class="sxs-lookup"><span data-stu-id="2553f-122">Press tab.</span></span>

    <span data-ttu-id="2553f-123">The following fields get filled up with the info from the SOAP API: Display name, Name, Description.</span><span class="sxs-lookup"><span data-stu-id="2553f-123">The following fields get filled up with the info from the SOAP API: Display name, Name, Description.</span></span>
6. <span data-ttu-id="2553f-124">Add an API URL suffix.</span><span class="sxs-lookup"><span data-stu-id="2553f-124">Add an API URL suffix.</span></span> <span data-ttu-id="2553f-125">The suffix is a name that identifies this specific API in this APIM instance.</span><span class="sxs-lookup"><span data-stu-id="2553f-125">The suffix is a name that identifies this specific API in this APIM instance.</span></span> <span data-ttu-id="2553f-126">It has to be unique in this APIM instance.</span><span class="sxs-lookup"><span data-stu-id="2553f-126">It has to be unique in this APIM instance.</span></span>
9. <span data-ttu-id="2553f-127">Publish the API by associating the API with a product.</span><span class="sxs-lookup"><span data-stu-id="2553f-127">Publish the API by associating the API with a product.</span></span> <span data-ttu-id="2553f-128">In this case, the "*Unlimited*" product is used.</span><span class="sxs-lookup"><span data-stu-id="2553f-128">In this case, the "*Unlimited*" product is used.</span></span>  <span data-ttu-id="2553f-129">If you want for the API to be published and be available to developers, add it to a product.</span><span class="sxs-lookup"><span data-stu-id="2553f-129">If you want for the API to be published and be available to developers, add it to a product.</span></span> <span data-ttu-id="2553f-130">You can do it during API creation or set it later.</span><span class="sxs-lookup"><span data-stu-id="2553f-130">You can do it during API creation or set it later.</span></span>

    <span data-ttu-id="2553f-131">Products are associations of one or more APIs.</span><span class="sxs-lookup"><span data-stu-id="2553f-131">Products are associations of one or more APIs.</span></span> <span data-ttu-id="2553f-132">You can include a number of APIs and offer them to developers through the developer portal.</span><span class="sxs-lookup"><span data-stu-id="2553f-132">You can include a number of APIs and offer them to developers through the developer portal.</span></span> <span data-ttu-id="2553f-133">Developers must first subscribe to a product to get access to the API.</span><span class="sxs-lookup"><span data-stu-id="2553f-133">Developers must first subscribe to a product to get access to the API.</span></span> <span data-ttu-id="2553f-134">When they subscribe, they get a subscription key that is good for any API in that product.</span><span class="sxs-lookup"><span data-stu-id="2553f-134">When they subscribe, they get a subscription key that is good for any API in that product.</span></span> <span data-ttu-id="2553f-135">If you created the APIM instance, you are an administrator already, so you are subscribed to every product by default.</span><span class="sxs-lookup"><span data-stu-id="2553f-135">If you created the APIM instance, you are an administrator already, so you are subscribed to every product by default.</span></span>

    <span data-ttu-id="2553f-136">By default, each API Management instance comes with two sample products:</span><span class="sxs-lookup"><span data-stu-id="2553f-136">By default, each API Management instance comes with two sample products:</span></span>

    * <span data-ttu-id="2553f-137">**Starter**</span><span class="sxs-lookup"><span data-stu-id="2553f-137">**Starter**</span></span>
    * <span data-ttu-id="2553f-138">**Unlimited**</span><span class="sxs-lookup"><span data-stu-id="2553f-138">**Unlimited**</span></span>   
10. <span data-ttu-id="2553f-139">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="2553f-139">Select **Create**.</span></span>

## <a name="test-the-new-apim-api-in-the-azure-portal"></a><span data-ttu-id="2553f-140">Test the new APIM API in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="2553f-140">Test the new APIM API in the Azure portal</span></span>

<span data-ttu-id="2553f-141">Operations can be called directly from the Azure portal, which provides a convenient way to view and test the operations of an API.</span><span class="sxs-lookup"><span data-stu-id="2553f-141">Operations can be called directly from the Azure portal, which provides a convenient way to view and test the operations of an API.</span></span>  

1. <span data-ttu-id="2553f-142">Select the API you created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="2553f-142">Select the API you created in the previous step.</span></span>
2. <span data-ttu-id="2553f-143">Press the **Test** tab.</span><span class="sxs-lookup"><span data-stu-id="2553f-143">Press the **Test** tab.</span></span>
3. <span data-ttu-id="2553f-144">Select some operation.</span><span class="sxs-lookup"><span data-stu-id="2553f-144">Select some operation.</span></span>

    <span data-ttu-id="2553f-145">The page displays fields for query parameters and fields for the headers.</span><span class="sxs-lookup"><span data-stu-id="2553f-145">The page displays fields for query parameters and fields for the headers.</span></span> <span data-ttu-id="2553f-146">One of the headers is "Ocp-Apim-Subscription-Key", for the subscription key of the product that is associated with this API.</span><span class="sxs-lookup"><span data-stu-id="2553f-146">One of the headers is "Ocp-Apim-Subscription-Key", for the subscription key of the product that is associated with this API.</span></span> <span data-ttu-id="2553f-147">If you created the APIM instance, you are an administrator already, so the key is filled in automatically.</span><span class="sxs-lookup"><span data-stu-id="2553f-147">If you created the APIM instance, you are an administrator already, so the key is filled in automatically.</span></span> 
1. <span data-ttu-id="2553f-148">Press **Send**.</span><span class="sxs-lookup"><span data-stu-id="2553f-148">Press **Send**.</span></span>

    <span data-ttu-id="2553f-149">Backend responds with **200 OK** and some data.</span><span class="sxs-lookup"><span data-stu-id="2553f-149">Backend responds with **200 OK** and some data.</span></span>

## <span data-ttu-id="2553f-150"><a name="call-operation"> </a>Call an operation from the developer portal</span><span class="sxs-lookup"><span data-stu-id="2553f-150"><a name="call-operation"> </a>Call an operation from the developer portal</span></span>

<span data-ttu-id="2553f-151">Operations can also be called **Developer portal** to test APIs.</span><span class="sxs-lookup"><span data-stu-id="2553f-151">Operations can also be called **Developer portal** to test APIs.</span></span> 

1. <span data-ttu-id="2553f-152">Select the API you created in the "Import and publish a back-end API" step.</span><span class="sxs-lookup"><span data-stu-id="2553f-152">Select the API you created in the "Import and publish a back-end API" step.</span></span>
2. <span data-ttu-id="2553f-153">Press **Developer portal**.</span><span class="sxs-lookup"><span data-stu-id="2553f-153">Press **Developer portal**.</span></span>

    <span data-ttu-id="2553f-154">The "Developer portal" site opens up.</span><span class="sxs-lookup"><span data-stu-id="2553f-154">The "Developer portal" site opens up.</span></span>
3. <span data-ttu-id="2553f-155">Select the **API** that you created.</span><span class="sxs-lookup"><span data-stu-id="2553f-155">Select the **API** that you created.</span></span>
4. <span data-ttu-id="2553f-156">Click the operation you want to test.</span><span class="sxs-lookup"><span data-stu-id="2553f-156">Click the operation you want to test.</span></span>
5. <span data-ttu-id="2553f-157">Press **Try it**.</span><span class="sxs-lookup"><span data-stu-id="2553f-157">Press **Try it**.</span></span>
6. <span data-ttu-id="2553f-158">Press **Send**.</span><span class="sxs-lookup"><span data-stu-id="2553f-158">Press **Send**.</span></span>
    
    <span data-ttu-id="2553f-159">After an operation is invoked, the developer portal displays the **Response status**, the **Response headers**, and any **Response content**.</span><span class="sxs-lookup"><span data-stu-id="2553f-159">After an operation is invoked, the developer portal displays the **Response status**, the **Response headers**, and any **Response content**.</span></span>

[!INCLUDE [api-management-navigate-to-instance.md](../../includes/api-management-append-apis.md)]

[!INCLUDE [api-management-define-api-topics.md](../../includes/api-management-define-api-topics.md)]

## <a name="next-steps"></a><span data-ttu-id="2553f-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="2553f-160">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2553f-161">Transform and protect a published API</span><span class="sxs-lookup"><span data-stu-id="2553f-161">Transform and protect a published API</span></span>](transform-api.md)