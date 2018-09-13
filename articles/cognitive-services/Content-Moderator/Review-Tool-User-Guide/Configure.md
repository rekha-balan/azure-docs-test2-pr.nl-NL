---
title: Configure the Review Tool | Microsoft Docs
description: Configure or get your team, tags, connectors, workflows, and credentials.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.technology: content-moderator
ms.topic: article
ms.date: 02/03/2017
ms.author: sajagtap
ms.openlocfilehash: c8f8eed308e7b3ef618d9289d3ac0b3f1a424ff9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549441"
---
# <a name="configure-or-get-review-tool-settings"></a><span data-ttu-id="26768-103">Configure or Get Review Tool Settings</span><span class="sxs-lookup"><span data-stu-id="26768-103">Configure or Get Review Tool Settings</span></span> #

## <a name="team"></a><span data-ttu-id="26768-104">Team</span><span class="sxs-lookup"><span data-stu-id="26768-104">Team</span></span> ##

<span data-ttu-id="26768-105">After you have sent out invites, you can monitor them, change permissions for team members, and invite additional users on the screens shown below.</span><span class="sxs-lookup"><span data-stu-id="26768-105">After you have sent out invites, you can monitor them, change permissions for team members, and invite additional users on the screens shown below.</span></span> <span data-ttu-id="26768-106">You can also create subteams and assign existing members.</span><span class="sxs-lookup"><span data-stu-id="26768-106">You can also create subteams and assign existing members.</span></span> <span data-ttu-id="26768-107">The users can be either administrators or reviewers.</span><span class="sxs-lookup"><span data-stu-id="26768-107">The users can be either administrators or reviewers.</span></span> <span data-ttu-id="26768-108">The difference between the two roles is that administrators can invite other users, while reviewers cannot.</span><span class="sxs-lookup"><span data-stu-id="26768-108">The difference between the two roles is that administrators can invite other users, while reviewers cannot.</span></span>

![Teams](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Content-Moderator/Review-Tool-User-Guide/images/7-Settings-Team.PNG)

## <a name="tags"></a><span data-ttu-id="26768-110">Tags</span><span class="sxs-lookup"><span data-stu-id="26768-110">Tags</span></span> ##

<span data-ttu-id="26768-111">This is where you can define your custom tags by entering the short code, name, and description for your tags and using the **Add** button.</span><span class="sxs-lookup"><span data-stu-id="26768-111">This is where you can define your custom tags by entering the short code, name, and description for your tags and using the **Add** button.</span></span> <span data-ttu-id="26768-112">You will see your new tag on the screen.</span><span class="sxs-lookup"><span data-stu-id="26768-112">You will see your new tag on the screen.</span></span> <span data-ttu-id="26768-113">Click the **Save** button to save your new tag and make it available during reviews.</span><span class="sxs-lookup"><span data-stu-id="26768-113">Click the **Save** button to save your new tag and make it available during reviews.</span></span>

![Tags](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Content-Moderator/Review-Tool-User-Guide/images/7-Settings-Tags-Combined.PNG)

## <a name="connectors"></a><span data-ttu-id="26768-115">Connectors</span><span class="sxs-lookup"><span data-stu-id="26768-115">Connectors</span></span> ##

<span data-ttu-id="26768-116">The Content Moderator review tool calls the Content Moderator APIs with the **default** workflow to moderate content.</span><span class="sxs-lookup"><span data-stu-id="26768-116">The Content Moderator review tool calls the Content Moderator APIs with the **default** workflow to moderate content.</span></span> <span data-ttu-id="26768-117">It will auto-provision the Moderator API credentials for you when you sign up for the review tool.</span><span class="sxs-lookup"><span data-stu-id="26768-117">It will auto-provision the Moderator API credentials for you when you sign up for the review tool.</span></span>

<span data-ttu-id="26768-118">It also supports integrating other APIs as long as a connector is available.</span><span class="sxs-lookup"><span data-stu-id="26768-118">It also supports integrating other APIs as long as a connector is available.</span></span> <span data-ttu-id="26768-119">We have made a few connectors available out of the box.</span><span class="sxs-lookup"><span data-stu-id="26768-119">We have made a few connectors available out of the box.</span></span> <span data-ttu-id="26768-120">You can enter your credentials for these APIs by using the **Connect** button.</span><span class="sxs-lookup"><span data-stu-id="26768-120">You can enter your credentials for these APIs by using the **Connect** button.</span></span> <span data-ttu-id="26768-121">You can then use these connectors in your custom workflows, as shown in the next section.</span><span class="sxs-lookup"><span data-stu-id="26768-121">You can then use these connectors in your custom workflows, as shown in the next section.</span></span>

![Connectors](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Content-Moderator/Review-Tool-User-Guide/images/7-Settings-Connectors.PNG)

## <a name="workflows"></a><span data-ttu-id="26768-123">Workflows</span><span class="sxs-lookup"><span data-stu-id="26768-123">Workflows</span></span> ##

<span data-ttu-id="26768-124">This is where you can see the **default** workflow.</span><span class="sxs-lookup"><span data-stu-id="26768-124">This is where you can see the **default** workflow.</span></span> <span data-ttu-id="26768-125">You can also define custom workflows for image and text by using the API Connectors available under the Connectors section.</span><span class="sxs-lookup"><span data-stu-id="26768-125">You can also define custom workflows for image and text by using the API Connectors available under the Connectors section.</span></span> <span data-ttu-id="26768-126">For a detailed example of how to define custom workflows, please see the **[Workflows](workflows.md)** section.</span><span class="sxs-lookup"><span data-stu-id="26768-126">For a detailed example of how to define custom workflows, please see the **[Workflows](workflows.md)** section.</span></span>

![Workflows](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Content-Moderator/Review-Tool-User-Guide/images/7-Settings-Workflows.PNG)

## <a name="credentials"></a><span data-ttu-id="26768-128">Credentials</span><span class="sxs-lookup"><span data-stu-id="26768-128">Credentials</span></span> ##

<span data-ttu-id="26768-129">In this section, you can access your Content Moderator subscription key to use with the APIs (Image, Text, List, Workflow, and Review APIs) included with Content Moderator.</span><span class="sxs-lookup"><span data-stu-id="26768-129">In this section, you can access your Content Moderator subscription key to use with the APIs (Image, Text, List, Workflow, and Review APIs) included with Content Moderator.</span></span> <span data-ttu-id="26768-130">You will use these APIs to integrate your content with the various Content Moderator capabilities, whether for scanning or for both scanning and enabling human review workflows.</span><span class="sxs-lookup"><span data-stu-id="26768-130">You will use these APIs to integrate your content with the various Content Moderator capabilities, whether for scanning or for both scanning and enabling human review workflows.</span></span>

![Credentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Content-Moderator/Review-Tool-User-Guide/images/7-Settings-Credentials3.PNG)





