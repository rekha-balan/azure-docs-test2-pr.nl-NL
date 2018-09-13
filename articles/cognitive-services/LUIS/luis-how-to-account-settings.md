---
title: Manage your account settings in LUIS | Microsoft Docs
description: Use LUIS website to manage your account settings.
titleSuffix: Azure
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 07/08/2018
ms.author: diberry
ms.openlocfilehash: 73e90e5ae86db2c2c4625762b285f8c86f0e241b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868851"
---
# <a name="manage-account-and-authoring-key"></a><span data-ttu-id="f6097-103">Manage account and authoring key</span><span class="sxs-lookup"><span data-stu-id="f6097-103">Manage account and authoring key</span></span>
<span data-ttu-id="f6097-104">The two key pieces of information for a LUIS account are the user account and the authoring key.</span><span class="sxs-lookup"><span data-stu-id="f6097-104">The two key pieces of information for a LUIS account are the user account and the authoring key.</span></span> <span data-ttu-id="f6097-105">Your login information is managed at [account.microsoft.com](https://account.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="f6097-105">Your login information is managed at [account.microsoft.com](https://account.microsoft.com).</span></span> <span data-ttu-id="f6097-106">Your authoring key is managed from the [LUIS](luis-reference-regions.md) website **Settings** page.</span><span class="sxs-lookup"><span data-stu-id="f6097-106">Your authoring key is managed from the [LUIS](luis-reference-regions.md) website **Settings** page.</span></span> 

## <a name="authoring-key"></a><span data-ttu-id="f6097-107">Authoring key</span><span class="sxs-lookup"><span data-stu-id="f6097-107">Authoring key</span></span>

<span data-ttu-id="f6097-108">This single, region-specific authoring key, on the **Settings** page, allows you to author all your apps from the [LUIS](luis-reference-regions.md) website as well as the [authoring APIs](https://aka.ms/luis-authoring-api).</span><span class="sxs-lookup"><span data-stu-id="f6097-108">This single, region-specific authoring key, on the **Settings** page, allows you to author all your apps from the [LUIS](luis-reference-regions.md) website as well as the [authoring APIs](https://aka.ms/luis-authoring-api).</span></span> <span data-ttu-id="f6097-109">As a convenience, the authoring key is allowed to make a [limited](luis-boundaries.md) number of endpoint queries each month.</span><span class="sxs-lookup"><span data-stu-id="f6097-109">As a convenience, the authoring key is allowed to make a [limited](luis-boundaries.md) number of endpoint queries each month.</span></span> 

![LUIS Settings page](./media/luis-how-to-account-settings/account-settings.png)

<span data-ttu-id="f6097-111">The authoring key is used for any apps you own as well as any apps you are listed as a collaborator.</span><span class="sxs-lookup"><span data-stu-id="f6097-111">The authoring key is used for any apps you own as well as any apps you are listed as a collaborator.</span></span>

## <a name="authoring-key-regions"></a><span data-ttu-id="f6097-112">Authoring key regions</span><span class="sxs-lookup"><span data-stu-id="f6097-112">Authoring key regions</span></span>
<span data-ttu-id="f6097-113">The authoring key is specific to the [authoring region](luis-reference-regions.md#publishing-regions).</span><span class="sxs-lookup"><span data-stu-id="f6097-113">The authoring key is specific to the [authoring region](luis-reference-regions.md#publishing-regions).</span></span> <span data-ttu-id="f6097-114">The key does not work in a different region.</span><span class="sxs-lookup"><span data-stu-id="f6097-114">The key does not work in a different region.</span></span> 

## <a name="reset-authoring-key"></a><span data-ttu-id="f6097-115">Reset authoring key</span><span class="sxs-lookup"><span data-stu-id="f6097-115">Reset authoring key</span></span>
<span data-ttu-id="f6097-116">If your authoring key is compromised, reset the key.</span><span class="sxs-lookup"><span data-stu-id="f6097-116">If your authoring key is compromised, reset the key.</span></span> <span data-ttu-id="f6097-117">The key is reset on all your apps in the [LUIS](luis-reference-regions.md) website.</span><span class="sxs-lookup"><span data-stu-id="f6097-117">The key is reset on all your apps in the [LUIS](luis-reference-regions.md) website.</span></span> <span data-ttu-id="f6097-118">If you author your apps via the authoring APIs, you need to change the value of `Ocp-Apim-Subscription-Key` to the new key.</span><span class="sxs-lookup"><span data-stu-id="f6097-118">If you author your apps via the authoring APIs, you need to change the value of `Ocp-Apim-Subscription-Key` to the new key.</span></span> 

## <a name="delete-account"></a><span data-ttu-id="f6097-119">Delete account</span><span class="sxs-lookup"><span data-stu-id="f6097-119">Delete account</span></span>
<span data-ttu-id="f6097-120">See [Data storage and removal](luis-concept-data-storage.md#accounts) for information about what data is deleted when you delete your account.</span><span class="sxs-lookup"><span data-stu-id="f6097-120">See [Data storage and removal](luis-concept-data-storage.md#accounts) for information about what data is deleted when you delete your account.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f6097-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="f6097-121">Next steps</span></span>

<span data-ttu-id="f6097-122">Learn more about your [authoring key](luis-concept-keys.md#authoring-key).</span><span class="sxs-lookup"><span data-stu-id="f6097-122">Learn more about your [authoring key](luis-concept-keys.md#authoring-key).</span></span> 

