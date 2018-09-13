---
title: Import an Azure Function App as an API in Azure API Management | Microsoft Docs
description: This tutorial shows you how to import an Azure Function App into Azure API Management as an API.
services: api-management
documentationcenter: ''
author: mikebudzynski
manager: cfowler
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 08/28/2018
ms.author: apimpm
ms.openlocfilehash: ea6078088417099045006f81dcaf1f769bbd64d7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857401"
---
# <a name="import-an-azure-function-app-as-an-api-in-azure-api-management"></a><span data-ttu-id="7089b-103">Import an Azure Function App as an API in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="7089b-103">Import an Azure Function App as an API in Azure API Management</span></span>

<span data-ttu-id="7089b-104">Azure API Management supports importing Azure Function Apps as new APIs or appending them to existing APIs.</span><span class="sxs-lookup"><span data-stu-id="7089b-104">Azure API Management supports importing Azure Function Apps as new APIs or appending them to existing APIs.</span></span> <span data-ttu-id="7089b-105">The process automatically generates a host key in the Azure Function App, which is then assigned to a named value in Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="7089b-105">The process automatically generates a host key in the Azure Function App, which is then assigned to a named value in Azure API Management.</span></span>

<span data-ttu-id="7089b-106">This article walks through importing an Azure Function App as an API in Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="7089b-106">This article walks through importing an Azure Function App as an API in Azure API Management.</span></span> <span data-ttu-id="7089b-107">It also describes the testing process.</span><span class="sxs-lookup"><span data-stu-id="7089b-107">It also describes the testing process.</span></span>

<span data-ttu-id="7089b-108">You will learn how to:</span><span class="sxs-lookup"><span data-stu-id="7089b-108">You will learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7089b-109">Import an Azure Function App as an API</span><span class="sxs-lookup"><span data-stu-id="7089b-109">Import an Azure Function App as an API</span></span>
> * <span data-ttu-id="7089b-110">Append an Azure Function App to an API</span><span class="sxs-lookup"><span data-stu-id="7089b-110">Append an Azure Function App to an API</span></span>
> * <span data-ttu-id="7089b-111">View the new Azure Function App host key and Azure API Management named value</span><span class="sxs-lookup"><span data-stu-id="7089b-111">View the new Azure Function App host key and Azure API Management named value</span></span>
> * <span data-ttu-id="7089b-112">Test the API in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="7089b-112">Test the API in the Azure portal</span></span>
> * <span data-ttu-id="7089b-113">Test the API in the developer portal</span><span class="sxs-lookup"><span data-stu-id="7089b-113">Test the API in the developer portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7089b-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7089b-114">Prerequisites</span></span>

* <span data-ttu-id="7089b-115">Complete the quickstart [Create an Azure API Management instance](get-started-create-service-instance.md).</span><span class="sxs-lookup"><span data-stu-id="7089b-115">Complete the quickstart [Create an Azure API Management instance](get-started-create-service-instance.md).</span></span>
* <span data-ttu-id="7089b-116">Make sure you have an Azure Functions app in your subscription.</span><span class="sxs-lookup"><span data-stu-id="7089b-116">Make sure you have an Azure Functions app in your subscription.</span></span> <span data-ttu-id="7089b-117">For more information, see [Create an Azure Function App](../azure-functions/functions-create-first-azure-function.md#create-a-function-app).</span><span class="sxs-lookup"><span data-stu-id="7089b-117">For more information, see [Create an Azure Function App](../azure-functions/functions-create-first-azure-function.md#create-a-function-app).</span></span> <span data-ttu-id="7089b-118">It has to contain Functions with HTTP trigger and authorization level setting set to *Anonymous* or *Function*.</span><span class="sxs-lookup"><span data-stu-id="7089b-118">It has to contain Functions with HTTP trigger and authorization level setting set to *Anonymous* or *Function*.</span></span>

[!INCLUDE [api-management-navigate-to-instance.md](../../includes/api-management-navigate-to-instance.md)]

## <a name="add-new-api-from-azure-function-app"></a> <span data-ttu-id="7089b-119">Import an Azure Function App as a new API</span><span class="sxs-lookup"><span data-stu-id="7089b-119">Import an Azure Function App as a new API</span></span>

<span data-ttu-id="7089b-120">Follow the steps below to create a new API from an Azure Function App.</span><span class="sxs-lookup"><span data-stu-id="7089b-120">Follow the steps below to create a new API from an Azure Function App.</span></span>

1. <span data-ttu-id="7089b-121">In your **Azure API Management** service instance, select **APIs** from the menu on the left.</span><span class="sxs-lookup"><span data-stu-id="7089b-121">In your **Azure API Management** service instance, select **APIs** from the menu on the left.</span></span>

2. <span data-ttu-id="7089b-122">In the **Add a new API** list, select **Function App**.</span><span class="sxs-lookup"><span data-stu-id="7089b-122">In the **Add a new API** list, select **Function App**.</span></span>

    ![Add from Function App](./media/import-function-app-as-api/add-01.png)

3. <span data-ttu-id="7089b-124">Click **Browse** to select Functions for import.</span><span class="sxs-lookup"><span data-stu-id="7089b-124">Click **Browse** to select Functions for import.</span></span>

    ![Add from Function App](./media/import-function-app-as-api/add-02.png)

4. <span data-ttu-id="7089b-126">Click on the **Function App** section to choose from the list of available Function Apps.</span><span class="sxs-lookup"><span data-stu-id="7089b-126">Click on the **Function App** section to choose from the list of available Function Apps.</span></span>

    ![Add from Function App](./media/import-function-app-as-api/add-03.png)

5. <span data-ttu-id="7089b-128">Find the Function App you want to import Functions from, click on it and press **Select**.</span><span class="sxs-lookup"><span data-stu-id="7089b-128">Find the Function App you want to import Functions from, click on it and press **Select**.</span></span>

    ![Add from Function App](./media/import-function-app-as-api/add-04.png)

6. <span data-ttu-id="7089b-130">Select the Functions you would like to import and click **Select**.</span><span class="sxs-lookup"><span data-stu-id="7089b-130">Select the Functions you would like to import and click **Select**.</span></span>

    ![Add from Function App](./media/import-function-app-as-api/add-05.png)

    > [!NOTE]
    > <span data-ttu-id="7089b-132">You can import only Functions that are based off HTTP trigger and have the authorization level setting set to *Anonymous* or *Function*.</span><span class="sxs-lookup"><span data-stu-id="7089b-132">You can import only Functions that are based off HTTP trigger and have the authorization level setting set to *Anonymous* or *Function*.</span></span>

7. <span data-ttu-id="7089b-133">Edit the pre-populated fields if needed.</span><span class="sxs-lookup"><span data-stu-id="7089b-133">Edit the pre-populated fields if needed.</span></span> <span data-ttu-id="7089b-134">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="7089b-134">Click **Create**.</span></span>

    ![Add from Function App](./media/import-function-app-as-api/add-06.png)

## <a name="append-azure-function-app-to-api"></a> <span data-ttu-id="7089b-136">Append Azure Function App to an existing API</span><span class="sxs-lookup"><span data-stu-id="7089b-136">Append Azure Function App to an existing API</span></span>

<span data-ttu-id="7089b-137">Follow the steps below to append Azure Function App to an existing API.</span><span class="sxs-lookup"><span data-stu-id="7089b-137">Follow the steps below to append Azure Function App to an existing API.</span></span>

1. <span data-ttu-id="7089b-138">In your **Azure API Management** service instance, select **APIs** from the menu on the left.</span><span class="sxs-lookup"><span data-stu-id="7089b-138">In your **Azure API Management** service instance, select **APIs** from the menu on the left.</span></span>

2. <span data-ttu-id="7089b-139">Choose an API you want to import an Azure Function App to.</span><span class="sxs-lookup"><span data-stu-id="7089b-139">Choose an API you want to import an Azure Function App to.</span></span> <span data-ttu-id="7089b-140">Click **...** and select **Import** from the context menu.</span><span class="sxs-lookup"><span data-stu-id="7089b-140">Click **...** and select **Import** from the context menu.</span></span>

    ![Append from Function App](./media/import-function-app-as-api/append-01.png)

3. <span data-ttu-id="7089b-142">Click on the **Function App** tile.</span><span class="sxs-lookup"><span data-stu-id="7089b-142">Click on the **Function App** tile.</span></span>

    ![Append from Function App](./media/import-function-app-as-api/append-02.png)

4. <span data-ttu-id="7089b-144">In the pop-up window, click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="7089b-144">In the pop-up window, click **Browse**.</span></span>

    ![Append from Function App](./media/import-function-app-as-api/append-03.png)

5. <span data-ttu-id="7089b-146">Click on the **Function App** section to choose from the list of available Function Apps.</span><span class="sxs-lookup"><span data-stu-id="7089b-146">Click on the **Function App** section to choose from the list of available Function Apps.</span></span>

    ![Add from Function App](./media/import-function-app-as-api/add-03.png)

6. <span data-ttu-id="7089b-148">Find the Function App you want to import Functions from, click on it and press **Select**.</span><span class="sxs-lookup"><span data-stu-id="7089b-148">Find the Function App you want to import Functions from, click on it and press **Select**.</span></span>

    ![Add from Function App](./media/import-function-app-as-api/add-04.png)

7. <span data-ttu-id="7089b-150">Select the Functions you would like to import and click **Select**.</span><span class="sxs-lookup"><span data-stu-id="7089b-150">Select the Functions you would like to import and click **Select**.</span></span>

    ![Add from Function App](./media/import-function-app-as-api/add-05.png)

8. <span data-ttu-id="7089b-152">Click **Import**.</span><span class="sxs-lookup"><span data-stu-id="7089b-152">Click **Import**.</span></span>

    ![Append from Function App](./media/import-function-app-as-api/append-04.png)

## <a name="function-app-import-keys"></a> <span data-ttu-id="7089b-154">Generated Azure Function App host key</span><span class="sxs-lookup"><span data-stu-id="7089b-154">Generated Azure Function App host key</span></span>

<span data-ttu-id="7089b-155">Import of an Azure Function App automatically generates:</span><span class="sxs-lookup"><span data-stu-id="7089b-155">Import of an Azure Function App automatically generates:</span></span>
* <span data-ttu-id="7089b-156">host key inside the Function App with the name apim-{*your Azure API Management service instance name*},</span><span class="sxs-lookup"><span data-stu-id="7089b-156">host key inside the Function App with the name apim-{*your Azure API Management service instance name*},</span></span>
* <span data-ttu-id="7089b-157">named value inside the Azure API Management instance with the name {*your Azure Function App instance name*}-key, which contains the created host key.</span><span class="sxs-lookup"><span data-stu-id="7089b-157">named value inside the Azure API Management instance with the name {*your Azure Function App instance name*}-key, which contains the created host key.</span></span>

> [!WARNING]
> <span data-ttu-id="7089b-158">Removing or changing value of either the Azure Function App host key or Azure API Management named value will break the communication between the services.</span><span class="sxs-lookup"><span data-stu-id="7089b-158">Removing or changing value of either the Azure Function App host key or Azure API Management named value will break the communication between the services.</span></span> <span data-ttu-id="7089b-159">The values do not sync automatically.</span><span class="sxs-lookup"><span data-stu-id="7089b-159">The values do not sync automatically.</span></span>
>
> <span data-ttu-id="7089b-160">If you need to rotate the host key, make sure the named value in Azure API Management is also modified.</span><span class="sxs-lookup"><span data-stu-id="7089b-160">If you need to rotate the host key, make sure the named value in Azure API Management is also modified.</span></span>

### <a name="access-azure-function-app-host-key"></a><span data-ttu-id="7089b-161">Access Azure Function App host key</span><span class="sxs-lookup"><span data-stu-id="7089b-161">Access Azure Function App host key</span></span>

1. <span data-ttu-id="7089b-162">Navigate to your Azure Function App instance.</span><span class="sxs-lookup"><span data-stu-id="7089b-162">Navigate to your Azure Function App instance.</span></span>

2. <span data-ttu-id="7089b-163">Select **Function App settings** from the overview.</span><span class="sxs-lookup"><span data-stu-id="7089b-163">Select **Function App settings** from the overview.</span></span>

    ![Add from Function App](./media/import-function-app-as-api/keys-02-a.png)

3. <span data-ttu-id="7089b-165">The key is located in the **Host Keys** section.</span><span class="sxs-lookup"><span data-stu-id="7089b-165">The key is located in the **Host Keys** section.</span></span>

    ![Add from Function App](./media/import-function-app-as-api/keys-02-b.png)

### <a name="access-the-named-value-in-azure-api-management"></a><span data-ttu-id="7089b-167">Access the named value in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="7089b-167">Access the named value in Azure API Management</span></span>

<span data-ttu-id="7089b-168">Navigate to your Azure API Management instance and select **Named values** from the menu on the left.</span><span class="sxs-lookup"><span data-stu-id="7089b-168">Navigate to your Azure API Management instance and select **Named values** from the menu on the left.</span></span> <span data-ttu-id="7089b-169">The Azure Function App key is stored there.</span><span class="sxs-lookup"><span data-stu-id="7089b-169">The Azure Function App key is stored there.</span></span>

![Add from Function App](./media/import-function-app-as-api/keys-01.png)

## <a name="test-in-azure-portal"></a> <span data-ttu-id="7089b-171">Test the new API Management API in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="7089b-171">Test the new API Management API in the Azure portal</span></span>

<span data-ttu-id="7089b-172">You can call operations directly from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7089b-172">You can call operations directly from the Azure portal.</span></span> <span data-ttu-id="7089b-173">Using the Azure portal is a convenient way to view and test the operations of an API.</span><span class="sxs-lookup"><span data-stu-id="7089b-173">Using the Azure portal is a convenient way to view and test the operations of an API.</span></span>  

1. <span data-ttu-id="7089b-174">Select the API that you created in the preceding section.</span><span class="sxs-lookup"><span data-stu-id="7089b-174">Select the API that you created in the preceding section.</span></span>

2. <span data-ttu-id="7089b-175">Select the **Test** tab.</span><span class="sxs-lookup"><span data-stu-id="7089b-175">Select the **Test** tab.</span></span>

3. <span data-ttu-id="7089b-176">Select an operation.</span><span class="sxs-lookup"><span data-stu-id="7089b-176">Select an operation.</span></span>

    <span data-ttu-id="7089b-177">The page displays fields for query parameters and fields for the headers.</span><span class="sxs-lookup"><span data-stu-id="7089b-177">The page displays fields for query parameters and fields for the headers.</span></span> <span data-ttu-id="7089b-178">One of the headers is **Ocp-Apim-Subscription-Key**, for the subscription key of the product that is associated with this API.</span><span class="sxs-lookup"><span data-stu-id="7089b-178">One of the headers is **Ocp-Apim-Subscription-Key**, for the subscription key of the product that is associated with this API.</span></span> <span data-ttu-id="7089b-179">If you created the API Management instance, you are an administrator already, so the key is filled in automatically.</span><span class="sxs-lookup"><span data-stu-id="7089b-179">If you created the API Management instance, you are an administrator already, so the key is filled in automatically.</span></span> 

4. <span data-ttu-id="7089b-180">Select **Send**.</span><span class="sxs-lookup"><span data-stu-id="7089b-180">Select **Send**.</span></span>

    <span data-ttu-id="7089b-181">The back end responds with **200 OK** and some data.</span><span class="sxs-lookup"><span data-stu-id="7089b-181">The back end responds with **200 OK** and some data.</span></span>

## <a name="test-in-developer-portal"></a> <span data-ttu-id="7089b-182">Call an operation from the developer portal</span><span class="sxs-lookup"><span data-stu-id="7089b-182">Call an operation from the developer portal</span></span>

<span data-ttu-id="7089b-183">You can also call operations from the developer portal to test APIs.</span><span class="sxs-lookup"><span data-stu-id="7089b-183">You can also call operations from the developer portal to test APIs.</span></span> 

1. <span data-ttu-id="7089b-184">Select the API that you created in [Import and publish a back-end API](#create-api).</span><span class="sxs-lookup"><span data-stu-id="7089b-184">Select the API that you created in [Import and publish a back-end API](#create-api).</span></span>

2. <span data-ttu-id="7089b-185">Select **Developer portal**.</span><span class="sxs-lookup"><span data-stu-id="7089b-185">Select **Developer portal**.</span></span>

    <span data-ttu-id="7089b-186">The developer portal site opens.</span><span class="sxs-lookup"><span data-stu-id="7089b-186">The developer portal site opens.</span></span>

3. <span data-ttu-id="7089b-187">Select the **API** that you created.</span><span class="sxs-lookup"><span data-stu-id="7089b-187">Select the **API** that you created.</span></span>

4. <span data-ttu-id="7089b-188">Select the operation you want to test.</span><span class="sxs-lookup"><span data-stu-id="7089b-188">Select the operation you want to test.</span></span>

5. <span data-ttu-id="7089b-189">Select **Try it**.</span><span class="sxs-lookup"><span data-stu-id="7089b-189">Select **Try it**.</span></span>

6. <span data-ttu-id="7089b-190">Select **Send**.</span><span class="sxs-lookup"><span data-stu-id="7089b-190">Select **Send**.</span></span>
    
    <span data-ttu-id="7089b-191">After an operation is invoked, the developer portal displays the **Response status**, the **Response headers**, and any **Response content**.</span><span class="sxs-lookup"><span data-stu-id="7089b-191">After an operation is invoked, the developer portal displays the **Response status**, the **Response headers**, and any **Response content**.</span></span>

[!INCLUDE [api-management-define-api-topics.md](../../includes/api-management-define-api-topics.md)]

## <a name="next-steps"></a><span data-ttu-id="7089b-192">Next steps</span><span class="sxs-lookup"><span data-stu-id="7089b-192">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7089b-193">Transform and protect a published API</span><span class="sxs-lookup"><span data-stu-id="7089b-193">Transform and protect a published API</span></span>](transform-api.md)