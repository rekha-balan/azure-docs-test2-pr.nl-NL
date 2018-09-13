---
title: Import SOAP API using the Azure portal | Microsoft Docs
description: Learn how to import SOAP API with API Management.
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
ms.openlocfilehash: 108758751b7c8ef5906cb55495a2604f918b2714
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864923"
---
# <a name="import-soap-api"></a><span data-ttu-id="40db2-103">Import SOAP API</span><span class="sxs-lookup"><span data-stu-id="40db2-103">Import SOAP API</span></span>

<span data-ttu-id="40db2-104">This article shows how to import a standard XML representation of a SOAP API.</span><span class="sxs-lookup"><span data-stu-id="40db2-104">This article shows how to import a standard XML representation of a SOAP API.</span></span> <span data-ttu-id="40db2-105">The article also shows how to test the APIM API.</span><span class="sxs-lookup"><span data-stu-id="40db2-105">The article also shows how to test the APIM API.</span></span>

<span data-ttu-id="40db2-106">In this article, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="40db2-106">In this article, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="40db2-107">Import SOAP API</span><span class="sxs-lookup"><span data-stu-id="40db2-107">Import SOAP API</span></span>
> * <span data-ttu-id="40db2-108">Test the API in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="40db2-108">Test the API in the Azure portal</span></span>
> * <span data-ttu-id="40db2-109">Test the API in the Developer portal</span><span class="sxs-lookup"><span data-stu-id="40db2-109">Test the API in the Developer portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40db2-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="40db2-110">Prerequisites</span></span>

<span data-ttu-id="40db2-111">Complete the following quickstart: [Create an Azure API Management instance](get-started-create-service-instance.md)</span><span class="sxs-lookup"><span data-stu-id="40db2-111">Complete the following quickstart: [Create an Azure API Management instance](get-started-create-service-instance.md)</span></span>

[!INCLUDE [api-management-navigate-to-instance.md](../../includes/api-management-navigate-to-instance.md)]

## <span data-ttu-id="40db2-112"><a name="create-api"> </a>Import and publish a back-end API</span><span class="sxs-lookup"><span data-stu-id="40db2-112"><a name="create-api"> </a>Import and publish a back-end API</span></span>

1. <span data-ttu-id="40db2-113">Select **APIs** from under **API MANAGEMENT**.</span><span class="sxs-lookup"><span data-stu-id="40db2-113">Select **APIs** from under **API MANAGEMENT**.</span></span>
2. <span data-ttu-id="40db2-114">Select **WSDL** from the **Add a new API** list.</span><span class="sxs-lookup"><span data-stu-id="40db2-114">Select **WSDL** from the **Add a new API** list.</span></span>

    ![Soap api](./media/import-soap-api/wsdl-api.png)
3. <span data-ttu-id="40db2-116">In the **WSDL specification**, enter the URL to where your SOAP API resides.</span><span class="sxs-lookup"><span data-stu-id="40db2-116">In the **WSDL specification**, enter the URL to where your SOAP API resides.</span></span>
4. <span data-ttu-id="40db2-117">The **SOAP pass-through** radio button is selected by default.</span><span class="sxs-lookup"><span data-stu-id="40db2-117">The **SOAP pass-through** radio button is selected by default.</span></span> <span data-ttu-id="40db2-118">With this selection, the API is going to be exposed as SOAP.</span><span class="sxs-lookup"><span data-stu-id="40db2-118">With this selection, the API is going to be exposed as SOAP.</span></span> <span data-ttu-id="40db2-119">Consumer has to use SOAP rules.</span><span class="sxs-lookup"><span data-stu-id="40db2-119">Consumer has to use SOAP rules.</span></span> <span data-ttu-id="40db2-120">If you want to "restify" the API, follow the steps in [Import a SOAP API and convert it to REST](restify-soap-api.md).</span><span class="sxs-lookup"><span data-stu-id="40db2-120">If you want to "restify" the API, follow the steps in [Import a SOAP API and convert it to REST](restify-soap-api.md).</span></span>

    ![Pass-through](./media/import-soap-api/pass-through.png)
5. <span data-ttu-id="40db2-122">Press tab.</span><span class="sxs-lookup"><span data-stu-id="40db2-122">Press tab.</span></span>

    <span data-ttu-id="40db2-123">The following fields get filled up with the info from the SOAP API: Display name, Name, Description.</span><span class="sxs-lookup"><span data-stu-id="40db2-123">The following fields get filled up with the info from the SOAP API: Display name, Name, Description.</span></span>
6. <span data-ttu-id="40db2-124">Add an API URL suffix.</span><span class="sxs-lookup"><span data-stu-id="40db2-124">Add an API URL suffix.</span></span> <span data-ttu-id="40db2-125">The suffix is a name that identifies this specific API in this APIM instance.</span><span class="sxs-lookup"><span data-stu-id="40db2-125">The suffix is a name that identifies this specific API in this APIM instance.</span></span> <span data-ttu-id="40db2-126">It has to be unique in this APIM instance.</span><span class="sxs-lookup"><span data-stu-id="40db2-126">It has to be unique in this APIM instance.</span></span>
9. <span data-ttu-id="40db2-127">Publish the API by associating the API with a product.</span><span class="sxs-lookup"><span data-stu-id="40db2-127">Publish the API by associating the API with a product.</span></span> <span data-ttu-id="40db2-128">In this case, the "*Unlimited*" product is used.</span><span class="sxs-lookup"><span data-stu-id="40db2-128">In this case, the "*Unlimited*" product is used.</span></span>  <span data-ttu-id="40db2-129">If you want for the API to be published and be available to developers, add it to a product.</span><span class="sxs-lookup"><span data-stu-id="40db2-129">If you want for the API to be published and be available to developers, add it to a product.</span></span> <span data-ttu-id="40db2-130">You can do it during API creation or set it later.</span><span class="sxs-lookup"><span data-stu-id="40db2-130">You can do it during API creation or set it later.</span></span>

    <span data-ttu-id="40db2-131">Products are associations of one or more APIs.</span><span class="sxs-lookup"><span data-stu-id="40db2-131">Products are associations of one or more APIs.</span></span> <span data-ttu-id="40db2-132">You can include a number of APIs and offer them to developers through the developer portal.</span><span class="sxs-lookup"><span data-stu-id="40db2-132">You can include a number of APIs and offer them to developers through the developer portal.</span></span> <span data-ttu-id="40db2-133">Developers must first subscribe to a product to get access to the API.</span><span class="sxs-lookup"><span data-stu-id="40db2-133">Developers must first subscribe to a product to get access to the API.</span></span> <span data-ttu-id="40db2-134">When they subscribe, they get a subscription key that is good for any API in that product.</span><span class="sxs-lookup"><span data-stu-id="40db2-134">When they subscribe, they get a subscription key that is good for any API in that product.</span></span> <span data-ttu-id="40db2-135">If you created the APIM instance, you are an administrator already, so you are subscribed to every product by default.</span><span class="sxs-lookup"><span data-stu-id="40db2-135">If you created the APIM instance, you are an administrator already, so you are subscribed to every product by default.</span></span>

    <span data-ttu-id="40db2-136">By default, each API Management instance comes with two sample products:</span><span class="sxs-lookup"><span data-stu-id="40db2-136">By default, each API Management instance comes with two sample products:</span></span>

    * <span data-ttu-id="40db2-137">**Starter**</span><span class="sxs-lookup"><span data-stu-id="40db2-137">**Starter**</span></span>
    * <span data-ttu-id="40db2-138">**Unlimited**</span><span class="sxs-lookup"><span data-stu-id="40db2-138">**Unlimited**</span></span>   
10. <span data-ttu-id="40db2-139">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="40db2-139">Select **Create**.</span></span>

### <a name="test-the-new-apim-api-in-the-administrative-portal"></a><span data-ttu-id="40db2-140">Test the new APIM API in the administrative portal</span><span class="sxs-lookup"><span data-stu-id="40db2-140">Test the new APIM API in the administrative portal</span></span>

<span data-ttu-id="40db2-141">Operations can be called directly from the administrative portal, which provides a convenient way to view and test the operations of an API.</span><span class="sxs-lookup"><span data-stu-id="40db2-141">Operations can be called directly from the administrative portal, which provides a convenient way to view and test the operations of an API.</span></span>  

1. <span data-ttu-id="40db2-142">Select the API you created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="40db2-142">Select the API you created in the previous step.</span></span>
2. <span data-ttu-id="40db2-143">Press the **Test** tab.</span><span class="sxs-lookup"><span data-stu-id="40db2-143">Press the **Test** tab.</span></span>
3. <span data-ttu-id="40db2-144">Select some operation.</span><span class="sxs-lookup"><span data-stu-id="40db2-144">Select some operation.</span></span>

    <span data-ttu-id="40db2-145">The page displays fields for query parameters and fields for the headers.</span><span class="sxs-lookup"><span data-stu-id="40db2-145">The page displays fields for query parameters and fields for the headers.</span></span> <span data-ttu-id="40db2-146">One of the headers is "Ocp-Apim-Subscription-Key", for the subscription key of the product that is associated with this API.</span><span class="sxs-lookup"><span data-stu-id="40db2-146">One of the headers is "Ocp-Apim-Subscription-Key", for the subscription key of the product that is associated with this API.</span></span> <span data-ttu-id="40db2-147">If you created the APIM instance, you are an administrator already, so the key is filled in automatically.</span><span class="sxs-lookup"><span data-stu-id="40db2-147">If you created the APIM instance, you are an administrator already, so the key is filled in automatically.</span></span> 
1. <span data-ttu-id="40db2-148">Press **Send**.</span><span class="sxs-lookup"><span data-stu-id="40db2-148">Press **Send**.</span></span>

    <span data-ttu-id="40db2-149">Backend responds with **200 OK** and some data.</span><span class="sxs-lookup"><span data-stu-id="40db2-149">Backend responds with **200 OK** and some data.</span></span>

### <span data-ttu-id="40db2-150"><a name="call-operation"> </a>Call an operation from the developer portal</span><span class="sxs-lookup"><span data-stu-id="40db2-150"><a name="call-operation"> </a>Call an operation from the developer portal</span></span>

<span data-ttu-id="40db2-151">Operations can also be called **Developer portal** to test APIs.</span><span class="sxs-lookup"><span data-stu-id="40db2-151">Operations can also be called **Developer portal** to test APIs.</span></span> 

1. <span data-ttu-id="40db2-152">Select the API you created in the "Import and publish a back-end API" step.</span><span class="sxs-lookup"><span data-stu-id="40db2-152">Select the API you created in the "Import and publish a back-end API" step.</span></span>
2. <span data-ttu-id="40db2-153">Press **Developer portal**.</span><span class="sxs-lookup"><span data-stu-id="40db2-153">Press **Developer portal**.</span></span>

    <span data-ttu-id="40db2-154">The "Developer portal" site opens up.</span><span class="sxs-lookup"><span data-stu-id="40db2-154">The "Developer portal" site opens up.</span></span>
3. <span data-ttu-id="40db2-155">Select the **API** that you created.</span><span class="sxs-lookup"><span data-stu-id="40db2-155">Select the **API** that you created.</span></span>
4. <span data-ttu-id="40db2-156">Click the operation you want to test.</span><span class="sxs-lookup"><span data-stu-id="40db2-156">Click the operation you want to test.</span></span>
5. <span data-ttu-id="40db2-157">Press **Try it**.</span><span class="sxs-lookup"><span data-stu-id="40db2-157">Press **Try it**.</span></span>
6. <span data-ttu-id="40db2-158">Press **Send**.</span><span class="sxs-lookup"><span data-stu-id="40db2-158">Press **Send**.</span></span>
    
    <span data-ttu-id="40db2-159">After an operation is invoked, the developer portal displays the **Response status**, the **Response headers**, and any **Response content**.</span><span class="sxs-lookup"><span data-stu-id="40db2-159">After an operation is invoked, the developer portal displays the **Response status**, the **Response headers**, and any **Response content**.</span></span>

[!INCLUDE [api-management-navigate-to-instance.md](../../includes/api-management-append-apis.md)]

[!INCLUDE [api-management-define-api-topics.md](../../includes/api-management-define-api-topics.md)]

## <a name="next-steps"></a><span data-ttu-id="40db2-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="40db2-160">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="40db2-161">Transform and protect a published API</span><span class="sxs-lookup"><span data-stu-id="40db2-161">Transform and protect a published API</span></span>](transform-api.md)