---
title: Credentials in Azure Content Moderator | Microsoft Docs
description: Manage Content Moderator credentials to use with the APIs.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 06/25/2017
ms.author: sajagtap
ms.openlocfilehash: 6477879953dc2bb2c7503eb0b2d4b5effa7b6a11
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865031"
---
# <a name="manage-credentials"></a><span data-ttu-id="1de9a-103">Manage credentials</span><span class="sxs-lookup"><span data-stu-id="1de9a-103">Manage credentials</span></span>

<span data-ttu-id="1de9a-104">Your Content Moderator credentials are created in the following locations:</span><span class="sxs-lookup"><span data-stu-id="1de9a-104">Your Content Moderator credentials are created in the following locations:</span></span>

- [<span data-ttu-id="1de9a-105">The Azure portal</span><span class="sxs-lookup"><span data-stu-id="1de9a-105">The Azure portal</span></span>](https://ms.portal.azure.com/#create/Microsoft.CognitiveServicesContentModerator)
- [<span data-ttu-id="1de9a-106">The Content Moderator review tool</span><span class="sxs-lookup"><span data-stu-id="1de9a-106">The Content Moderator review tool</span></span>](http://contentmoderator.cognitive.microsoft.com/)

<span data-ttu-id="1de9a-107">This article explains where to find them and how they relate to each other.</span><span class="sxs-lookup"><span data-stu-id="1de9a-107">This article explains where to find them and how they relate to each other.</span></span>

## <a name="the-azure-portal"></a><span data-ttu-id="1de9a-108">The Azure portal</span><span class="sxs-lookup"><span data-stu-id="1de9a-108">The Azure portal</span></span>

<span data-ttu-id="1de9a-109">On the Azure portal dashboard, select your Content Moderator account.</span><span class="sxs-lookup"><span data-stu-id="1de9a-109">On the Azure portal dashboard, select your Content Moderator account.</span></span> <span data-ttu-id="1de9a-110">Under **Resource Management**, select **Keys**.</span><span class="sxs-lookup"><span data-stu-id="1de9a-110">Under **Resource Management**, select **Keys**.</span></span> <span data-ttu-id="1de9a-111">To copy the key, select the icon to the right of the key.</span><span class="sxs-lookup"><span data-stu-id="1de9a-111">To copy the key, select the icon to the right of the key.</span></span>

![Content Moderator keys in the Azure portal](images/credentials-azure-portal-keys.PNG)

### <a name="use-the-azure-account-with-the-review-tool-and-review-api"></a><span data-ttu-id="1de9a-113">Use the Azure account with the review tool and review API</span><span class="sxs-lookup"><span data-stu-id="1de9a-113">Use the Azure account with the review tool and review API</span></span>
<span data-ttu-id="1de9a-114">To use your Azure key with the review APIs, copy the Resource ID listed on the **Properties** screen in the following screenshot, and enter it on the review tool's credentials screen in the **Whitelisted Resource Id(s)** fields as shown in the following **Resource ID** section.</span><span class="sxs-lookup"><span data-stu-id="1de9a-114">To use your Azure key with the review APIs, copy the Resource ID listed on the **Properties** screen in the following screenshot, and enter it on the review tool's credentials screen in the **Whitelisted Resource Id(s)** fields as shown in the following **Resource ID** section.</span></span> 

> [!NOTE]
> <span data-ttu-id="1de9a-115">Your Content Moderator subscription's region should match the review team's region for it to recognize your team and access the team data.</span><span class="sxs-lookup"><span data-stu-id="1de9a-115">Your Content Moderator subscription's region should match the review team's region for it to recognize your team and access the team data.</span></span> <span data-ttu-id="1de9a-116">For example, in the images on this page, The **West US** region **(4)** contains the Content Moderator Azure subscription and your review team.</span><span class="sxs-lookup"><span data-stu-id="1de9a-116">For example, in the images on this page, The **West US** region **(4)** contains the Content Moderator Azure subscription and your review team.</span></span>
>
> <span data-ttu-id="1de9a-117">Once you replace the two places in the review tool with the key and the Resource ID from your Azure subscription, your **Trial Ocp-Apim-Subscription-Key** displayed on the Credentials screen is no longer used, but is always available.</span><span class="sxs-lookup"><span data-stu-id="1de9a-117">Once you replace the two places in the review tool with the key and the Resource ID from your Azure subscription, your **Trial Ocp-Apim-Subscription-Key** displayed on the Credentials screen is no longer used, but is always available.</span></span>
> <span data-ttu-id="1de9a-118">The trial key limits you to maximum 5,000 transactions per month at 1 request per second (RPS).</span><span class="sxs-lookup"><span data-stu-id="1de9a-118">The trial key limits you to maximum 5,000 transactions per month at 1 request per second (RPS).</span></span>

![Content Moderator Resource ID in the Azure portal](images/credentials-azure-portal-resourceid.PNG)

### <a name="use-the-azure-account-with-the-workflows-in-the-review-tool"></a><span data-ttu-id="1de9a-120">Use the Azure account with the workflows in the review tool</span><span class="sxs-lookup"><span data-stu-id="1de9a-120">Use the Azure account with the workflows in the review tool</span></span>

<span data-ttu-id="1de9a-121">To use your Azure key for the workflows available within Content Moderator, enter it in the **Ocp-Apim-Subscription-Key** field in the **Workflow Settings** section as shown in the following **Workflows** section.</span><span class="sxs-lookup"><span data-stu-id="1de9a-121">To use your Azure key for the workflows available within Content Moderator, enter it in the **Ocp-Apim-Subscription-Key** field in the **Workflow Settings** section as shown in the following **Workflows** section.</span></span> <span data-ttu-id="1de9a-122">Hit the **'+'** to save your resource ID.</span><span class="sxs-lookup"><span data-stu-id="1de9a-122">Hit the **'+'** to save your resource ID.</span></span>

![Content Moderator workflow credentials in the review tool](images/credentials-workflow.PNG)

## <a name="the-review-tool"></a><span data-ttu-id="1de9a-124">The Review tool</span><span class="sxs-lookup"><span data-stu-id="1de9a-124">The Review tool</span></span>

<span data-ttu-id="1de9a-125">On the Review tool Dashboard, on the **Settings** tab, select **Credentials**.</span><span class="sxs-lookup"><span data-stu-id="1de9a-125">On the Review tool Dashboard, on the **Settings** tab, select **Credentials**.</span></span>

![Content Moderator credentials in the review tool](images/credentials-trial-resource-workflow.PNG)

<span data-ttu-id="1de9a-127">The following section examines the preceding image in more detail:</span><span class="sxs-lookup"><span data-stu-id="1de9a-127">The following section examines the preceding image in more detail:</span></span>

### <a name="api"></a><span data-ttu-id="1de9a-128">API</span><span class="sxs-lookup"><span data-stu-id="1de9a-128">API</span></span>

<span data-ttu-id="1de9a-129">The first part lists your **review API endpoint**, **team ID**, and the **Ocp-Apim-Subscription-Key (Content Moderator trial key)** generated as part of your review team creation.</span><span class="sxs-lookup"><span data-stu-id="1de9a-129">The first part lists your **review API endpoint**, **team ID**, and the **Ocp-Apim-Subscription-Key (Content Moderator trial key)** generated as part of your review team creation.</span></span> <span data-ttu-id="1de9a-130">Use them to call all Content Moderator APIs, including the review API.</span><span class="sxs-lookup"><span data-stu-id="1de9a-130">Use them to call all Content Moderator APIs, including the review API.</span></span>

<span data-ttu-id="1de9a-131">Also note your region identifier for your API endpoint.</span><span class="sxs-lookup"><span data-stu-id="1de9a-131">Also note your region identifier for your API endpoint.</span></span> <span data-ttu-id="1de9a-132">For example, **westus** is the region in "https://westus.api.cognitive.microsoft.com/contentmoderator/review/v1.0"</span><span class="sxs-lookup"><span data-stu-id="1de9a-132">For example, **westus** is the region in "https://westus.api.cognitive.microsoft.com/contentmoderator/review/v1.0"</span></span>

![Content Moderator key in the review tool](images/credentials-trialkey.PNG)

### <a name="resource-id"></a><span data-ttu-id="1de9a-134">Resource ID</span><span class="sxs-lookup"><span data-stu-id="1de9a-134">Resource ID</span></span>

<span data-ttu-id="1de9a-135">We covered this section in the [using your Azure account with the review tool and API](credentials.md#how-to-use-your-azure-account-with-the-review-tool) section.</span><span class="sxs-lookup"><span data-stu-id="1de9a-135">We covered this section in the [using your Azure account with the review tool and API](credentials.md#how-to-use-your-azure-account-with-the-review-tool) section.</span></span> <span data-ttu-id="1de9a-136">This field is usually blank unless you add your Azure Resource Id to this field as explained in the previous section.</span><span class="sxs-lookup"><span data-stu-id="1de9a-136">This field is usually blank unless you add your Azure Resource Id to this field as explained in the previous section.</span></span>

### <a name="workflows"></a><span data-ttu-id="1de9a-137">Workflows</span><span class="sxs-lookup"><span data-stu-id="1de9a-137">Workflows</span></span>

<span data-ttu-id="1de9a-138">We covered this set of fields in the previous section on [using your Azure key to run the workflows](credentials.md#use-the-azure-account-with-the-workflows-in-the-review-tool).</span><span class="sxs-lookup"><span data-stu-id="1de9a-138">We covered this set of fields in the previous section on [using your Azure key to run the workflows](credentials.md#use-the-azure-account-with-the-workflows-in-the-review-tool).</span></span> <span data-ttu-id="1de9a-139">By default, the review tool uses its auto-generated trial key for running the workflows, and that's what shows up to begin with.</span><span class="sxs-lookup"><span data-stu-id="1de9a-139">By default, the review tool uses its auto-generated trial key for running the workflows, and that's what shows up to begin with.</span></span> <span data-ttu-id="1de9a-140">The other two fields allow using term and image lists in the Screen Text and Evaluate Image operations respectively.</span><span class="sxs-lookup"><span data-stu-id="1de9a-140">The other two fields allow using term and image lists in the Screen Text and Evaluate Image operations respectively.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1de9a-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="1de9a-141">Next steps</span></span>

* <span data-ttu-id="1de9a-142">Learn how to use the Content Moderator credentials in your [workflows](workflows.md).</span><span class="sxs-lookup"><span data-stu-id="1de9a-142">Learn how to use the Content Moderator credentials in your [workflows](workflows.md).</span></span>
