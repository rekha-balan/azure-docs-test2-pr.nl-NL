---
title: Conversation Learner default configuration - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: Learn about the default Conversation Learner configuration.
services: cognitive-services
author: v-jaswel
manager: nolachar
ms.service: cognitive-services
ms.component: conversation-learner
ms.topic: article
ms.date: 04/30/2018
ms.author: v-jaswel
ms.openlocfilehash: c0ad9f71665e503fe794c68200b90a8474750823
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865058"
---
# <a name="default-values-and-boundaries"></a><span data-ttu-id="89e9a-103">Default values and boundaries</span><span class="sxs-lookup"><span data-stu-id="89e9a-103">Default values and boundaries</span></span>

<span data-ttu-id="89e9a-104">This document describes the default configuration of Conversation Learner, and key service boundaries.</span><span class="sxs-lookup"><span data-stu-id="89e9a-104">This document describes the default configuration of Conversation Learner, and key service boundaries.</span></span>

## <a name="default-configuration"></a><span data-ttu-id="89e9a-105">Default configuration</span><span class="sxs-lookup"><span data-stu-id="89e9a-105">Default configuration</span></span>

<span data-ttu-id="89e9a-106">Parameter</span><span class="sxs-lookup"><span data-stu-id="89e9a-106">Parameter</span></span> | <span data-ttu-id="89e9a-107">Default value</span><span class="sxs-lookup"><span data-stu-id="89e9a-107">Default value</span></span>
--- | --- 
<span data-ttu-id="89e9a-108">Default session timeout</span><span class="sxs-lookup"><span data-stu-id="89e9a-108">Default session timeout</span></span> | <span data-ttu-id="89e9a-109">30 minutes</span><span class="sxs-lookup"><span data-stu-id="89e9a-109">30 minutes</span></span>

## <a name="boundaries"></a><span data-ttu-id="89e9a-110">Boundaries</span><span class="sxs-lookup"><span data-stu-id="89e9a-110">Boundaries</span></span>

<span data-ttu-id="89e9a-111">Parameter</span><span class="sxs-lookup"><span data-stu-id="89e9a-111">Parameter</span></span> | <span data-ttu-id="89e9a-112">Limit</span><span class="sxs-lookup"><span data-stu-id="89e9a-112">Limit</span></span>
--- | --- 
<span data-ttu-id="89e9a-113">Authoring API, max HTTP calls per month</span><span class="sxs-lookup"><span data-stu-id="89e9a-113">Authoring API, max HTTP calls per month</span></span> | <span data-ttu-id="89e9a-114">5M</span><span class="sxs-lookup"><span data-stu-id="89e9a-114">5M</span></span>
<span data-ttu-id="89e9a-115">Authoring API, max HTTP calls per second</span><span class="sxs-lookup"><span data-stu-id="89e9a-115">Authoring API, max HTTP calls per second</span></span> | <span data-ttu-id="89e9a-116">25</span><span class="sxs-lookup"><span data-stu-id="89e9a-116">25</span></span>
<span data-ttu-id="89e9a-117">Session API, max HTTP calls per month</span><span class="sxs-lookup"><span data-stu-id="89e9a-117">Session API, max HTTP calls per month</span></span> | <span data-ttu-id="89e9a-118">500K</span><span class="sxs-lookup"><span data-stu-id="89e9a-118">500K</span></span>
<span data-ttu-id="89e9a-119">Session API, max HTTP calls per second</span><span class="sxs-lookup"><span data-stu-id="89e9a-119">Session API, max HTTP calls per second</span></span> | <span data-ttu-id="89e9a-120">10</span><span class="sxs-lookup"><span data-stu-id="89e9a-120">10</span></span>
<span data-ttu-id="89e9a-121">Max number of custom (non-programmatic) entities per model</span><span class="sxs-lookup"><span data-stu-id="89e9a-121">Max number of custom (non-programmatic) entities per model</span></span> | <span data-ttu-id="89e9a-122">See [LUIS boundaries doc](https://docs.microsoft.com/en-us/azure/cognitive-services/luis/luis-boundaries); in practice, actual number may be slightly smaller</span><span class="sxs-lookup"><span data-stu-id="89e9a-122">See [LUIS boundaries doc](https://docs.microsoft.com/en-us/azure/cognitive-services/luis/luis-boundaries); in practice, actual number may be slightly smaller</span></span>
<span data-ttu-id="89e9a-123">Max number of pre-built entities per model</span><span class="sxs-lookup"><span data-stu-id="89e9a-123">Max number of pre-built entities per model</span></span> | <span data-ttu-id="89e9a-124">See [LUIS boundaries doc](https://docs.microsoft.com/en-us/azure/cognitive-services/luis/luis-boundaries)</span><span class="sxs-lookup"><span data-stu-id="89e9a-124">See [LUIS boundaries doc](https://docs.microsoft.com/en-us/azure/cognitive-services/luis/luis-boundaries)</span></span>
<span data-ttu-id="89e9a-125">Max number of entities (in total) per model</span><span class="sxs-lookup"><span data-stu-id="89e9a-125">Max number of entities (in total) per model</span></span> | <span data-ttu-id="89e9a-126">100</span><span class="sxs-lookup"><span data-stu-id="89e9a-126">100</span></span>
<span data-ttu-id="89e9a-127">Max number of actions per model</span><span class="sxs-lookup"><span data-stu-id="89e9a-127">Max number of actions per model</span></span> | <span data-ttu-id="89e9a-128">32</span><span class="sxs-lookup"><span data-stu-id="89e9a-128">32</span></span>
<span data-ttu-id="89e9a-129">Max number of train dialogs per model</span><span class="sxs-lookup"><span data-stu-id="89e9a-129">Max number of train dialogs per model</span></span> | <span data-ttu-id="89e9a-130">1000</span><span class="sxs-lookup"><span data-stu-id="89e9a-130">1000</span></span>
<span data-ttu-id="89e9a-131">Max number of user turns per train dialog</span><span class="sxs-lookup"><span data-stu-id="89e9a-131">Max number of user turns per train dialog</span></span> | <span data-ttu-id="89e9a-132">100</span><span class="sxs-lookup"><span data-stu-id="89e9a-132">100</span></span>
<span data-ttu-id="89e9a-133">Max number of log dialogs per model</span><span class="sxs-lookup"><span data-stu-id="89e9a-133">Max number of log dialogs per model</span></span> | <span data-ttu-id="89e9a-134">No pre-set limit, but log dialogs are only retained for a fixed period before being discarded.</span><span class="sxs-lookup"><span data-stu-id="89e9a-134">No pre-set limit, but log dialogs are only retained for a fixed period before being discarded.</span></span>  <span data-ttu-id="89e9a-135">Also, the Conversation Learner UI will show 100 log dialogs at a time.</span><span class="sxs-lookup"><span data-stu-id="89e9a-135">Also, the Conversation Learner UI will show 100 log dialogs at a time.</span></span> 
<span data-ttu-id="89e9a-136">Max number of models per user</span><span class="sxs-lookup"><span data-stu-id="89e9a-136">Max number of models per user</span></span> | <span data-ttu-id="89e9a-137">No pre-set limit</span><span class="sxs-lookup"><span data-stu-id="89e9a-137">No pre-set limit</span></span>
<span data-ttu-id="89e9a-138">Max number of sequential non-wait actions</span><span class="sxs-lookup"><span data-stu-id="89e9a-138">Max number of sequential non-wait actions</span></span> | <span data-ttu-id="89e9a-139">5 (\*)</span><span class="sxs-lookup"><span data-stu-id="89e9a-139">5 (\*)</span></span>

<span data-ttu-id="89e9a-140">(\*) After 5 sequential non-wait actions, all non-wait actions are masked, and Conversation Learner will choose amongst available wait actions.</span><span class="sxs-lookup"><span data-stu-id="89e9a-140">(\*) After 5 sequential non-wait actions, all non-wait actions are masked, and Conversation Learner will choose amongst available wait actions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89e9a-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="89e9a-141">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="89e9a-142">Get started with Conversation Learner</span><span class="sxs-lookup"><span data-stu-id="89e9a-142">Get started with Conversation Learner</span></span>](./quickstart.md)
