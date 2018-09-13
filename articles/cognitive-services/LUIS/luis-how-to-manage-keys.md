---
title: Manage your endpoint keys in LUIS | Microsoft Docs
description: Use Language Understanding (LUIS) to manage your programmatic API, endpoint, and external keys.
titleSuffix: Azure
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 03/21/2018
ms.author: diberry
ms.openlocfilehash: 127c09a022f5efb95ab6a5ec2db0de633b437a54
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869694"
---
# <a name="manage-your-luis-endpoint-keys"></a><span data-ttu-id="75045-103">Manage your LUIS endpoint keys</span><span class="sxs-lookup"><span data-stu-id="75045-103">Manage your LUIS endpoint keys</span></span>
<span data-ttu-id="75045-104">A key allows you to author and publish your LUIS app, or query your endpoint.</span><span class="sxs-lookup"><span data-stu-id="75045-104">A key allows you to author and publish your LUIS app, or query your endpoint.</span></span> 

<a name="programmatic-key" ></a>
<a name="authoring-key" ></a>
<a name="endpoint-key" ></a>
<a name="use-endpoint-key-in-query" ></a>
<a name="api-usage-of-ocp-apim-subscription-key" ></a>
<a name="key-limits" ></a>
<a name="key-limit-errors" ></a>
## <a name="key-concepts"></a><span data-ttu-id="75045-105">Key concepts</span><span class="sxs-lookup"><span data-stu-id="75045-105">Key concepts</span></span>
<span data-ttu-id="75045-106">See [Keys in LUIS](luis-concept-keys.md) to understand LUIS authoring and endpoint key concepts.</span><span class="sxs-lookup"><span data-stu-id="75045-106">See [Keys in LUIS](luis-concept-keys.md) to understand LUIS authoring and endpoint key concepts.</span></span>

<a name="create-and-use-an-endpoint-key"></a>
## <a name="assign-endpoint-key"></a><span data-ttu-id="75045-107">Assign endpoint key</span><span class="sxs-lookup"><span data-stu-id="75045-107">Assign endpoint key</span></span>
<span data-ttu-id="75045-108">On the **Publish app** page, there is already a key in the **Resources and Keys** table.</span><span class="sxs-lookup"><span data-stu-id="75045-108">On the **Publish app** page, there is already a key in the **Resources and Keys** table.</span></span> <span data-ttu-id="75045-109">This is the authoring (starter) key.</span><span class="sxs-lookup"><span data-stu-id="75045-109">This is the authoring (starter) key.</span></span> 

1. <span data-ttu-id="75045-110">Create a LUIS key on the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="75045-110">Create a LUIS key on the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="75045-111">For further instructions, see [Creating an endpoint key using Azure](luis-how-to-azure-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="75045-111">For further instructions, see [Creating an endpoint key using Azure](luis-how-to-azure-subscription.md).</span></span>
 
2. <span data-ttu-id="75045-112">In order to add the LUIS key created in the previous step, click the **Add Key** button to open the **Assign a key to your app** dialog.</span><span class="sxs-lookup"><span data-stu-id="75045-112">In order to add the LUIS key created in the previous step, click the **Add Key** button to open the **Assign a key to your app** dialog.</span></span> 

    ![Assign a key to your app](./media/luis-manage-keys/assign-key.png)
3. <span data-ttu-id="75045-114">Select a Tenant in the dialog.</span><span class="sxs-lookup"><span data-stu-id="75045-114">Select a Tenant in the dialog.</span></span> 
 
    > [!Note]
    > <span data-ttu-id="75045-115">In Azure, a tenant represents the Azure Active Directory ID of the client or organization associated with a service.</span><span class="sxs-lookup"><span data-stu-id="75045-115">In Azure, a tenant represents the Azure Active Directory ID of the client or organization associated with a service.</span></span> <span data-ttu-id="75045-116">If you previously signed up for an Azure subscription with your individual Microsoft Account, you already have a tenant!</span><span class="sxs-lookup"><span data-stu-id="75045-116">If you previously signed up for an Azure subscription with your individual Microsoft Account, you already have a tenant!</span></span> <span data-ttu-id="75045-117">When you log in to the Azure portal, you are automatically logged in to [your default tenant](https://docs.microsoft.com/azure/active-directory/develop/active-directory-howto-tenant).</span><span class="sxs-lookup"><span data-stu-id="75045-117">When you log in to the Azure portal, you are automatically logged in to [your default tenant](https://docs.microsoft.com/azure/active-directory/develop/active-directory-howto-tenant).</span></span> <span data-ttu-id="75045-118">You are free to use this tenant but you may want to create an Organizational administrator account.</span><span class="sxs-lookup"><span data-stu-id="75045-118">You are free to use this tenant but you may want to create an Organizational administrator account.</span></span>

4. <span data-ttu-id="75045-119">Choose the Azure subscription associated with the Azure LUIS key you want to add.</span><span class="sxs-lookup"><span data-stu-id="75045-119">Choose the Azure subscription associated with the Azure LUIS key you want to add.</span></span>

5. <span data-ttu-id="75045-120">Select the Azure LUIS account.</span><span class="sxs-lookup"><span data-stu-id="75045-120">Select the Azure LUIS account.</span></span> <span data-ttu-id="75045-121">The region of the account is displayed in parentheses.</span><span class="sxs-lookup"><span data-stu-id="75045-121">The region of the account is displayed in parentheses.</span></span> 

    ![Choose the key](./media/luis-manage-keys/assign-key-filled-out.png)

6. <span data-ttu-id="75045-123">After you assign this endpoint key, use it in all endpoint queries.</span><span class="sxs-lookup"><span data-stu-id="75045-123">After you assign this endpoint key, use it in all endpoint queries.</span></span> 

<!-- content moved to luis-reference-regions.md, need replacement links-->
<a name="regions-and-keys"></a>
<a name="publishing-to-europe"></a>
<a name="publishing-to-australia"></a>

## <a name="publishing-regions"></a><span data-ttu-id="75045-124">Publishing regions</span><span class="sxs-lookup"><span data-stu-id="75045-124">Publishing regions</span></span>
<span data-ttu-id="75045-125">Learn more about publishing [regions](luis-reference-regions.md) including publishing in [Europe](luis-reference-regions.md#publishing-to-europe), and [Australia](luis-reference-regions.md#publishing-to-australia).</span><span class="sxs-lookup"><span data-stu-id="75045-125">Learn more about publishing [regions](luis-reference-regions.md) including publishing in [Europe](luis-reference-regions.md#publishing-to-europe), and [Australia](luis-reference-regions.md#publishing-to-australia).</span></span> <span data-ttu-id="75045-126">Publishing regions are different from authoring regions.</span><span class="sxs-lookup"><span data-stu-id="75045-126">Publishing regions are different from authoring regions.</span></span> <span data-ttu-id="75045-127">Make sure you create an app in the authoring region corresponding to the publishing region you want.</span><span class="sxs-lookup"><span data-stu-id="75045-127">Make sure you create an app in the authoring region corresponding to the publishing region you want.</span></span>

## <a name="unassign-key"></a><span data-ttu-id="75045-128">Unassign key</span><span class="sxs-lookup"><span data-stu-id="75045-128">Unassign key</span></span>

* <span data-ttu-id="75045-129">In the **Resources and Keys list**, click the trash bin icon next to the entity you want to unassign.</span><span class="sxs-lookup"><span data-stu-id="75045-129">In the **Resources and Keys list**, click the trash bin icon next to the entity you want to unassign.</span></span> <span data-ttu-id="75045-130">Then, click **OK** in the confirmation message to confirm deletion.</span><span class="sxs-lookup"><span data-stu-id="75045-130">Then, click **OK** in the confirmation message to confirm deletion.</span></span>
 
    ![Unassign Entity](./media/luis-manage-keys/unassign-key.png)

> [!NOTE]
> <span data-ttu-id="75045-132">Unassigning the LUIS key does not delete it from your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="75045-132">Unassigning the LUIS key does not delete it from your Azure subscription.</span></span>

## <a name="next-steps"></a><span data-ttu-id="75045-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="75045-133">Next steps</span></span>

<span data-ttu-id="75045-134">Use your key to publish your app in the **Publish app** page.</span><span class="sxs-lookup"><span data-stu-id="75045-134">Use your key to publish your app in the **Publish app** page.</span></span> <span data-ttu-id="75045-135">For instructions on publishing, see [Publish app](luis-how-to-publish-app.md).</span><span class="sxs-lookup"><span data-stu-id="75045-135">For instructions on publishing, see [Publish app](luis-how-to-publish-app.md).</span></span>