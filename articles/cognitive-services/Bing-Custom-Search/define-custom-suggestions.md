---
title: 'Bing Custom Search: Define Custom Autosuggest suggestions | Microsoft Docs'
description: Describes how to configure Custom Autosuggest with custom suggestions
services: cognitive-services
author: brapel
manager: ehansen
ms.service: cognitive-services
ms.technology: bing-custom-search
ms.topic: article
ms.date: 09/28/2017
ms.author: v-brapel
ms.openlocfilehash: e7a62a79bdc2e486fb6bfca34eb4addeba2bde0e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966121"
---
# <a name="configure-your-custom-autosuggest-experience"></a><span data-ttu-id="1779f-103">Configure your custom autosuggest experience</span><span class="sxs-lookup"><span data-stu-id="1779f-103">Configure your custom autosuggest experience</span></span>
<span data-ttu-id="1779f-104">If you subscribed to Custom Search at the appropriate level (see the [pricing pages](https://azure.microsoft.com/pricing/details/cognitive-services/bing-custom-search/)), you can customize the search suggestions made in your Custom Search experience.</span><span class="sxs-lookup"><span data-stu-id="1779f-104">If you subscribed to Custom Search at the appropriate level (see the [pricing pages](https://azure.microsoft.com/pricing/details/cognitive-services/bing-custom-search/)), you can customize the search suggestions made in your Custom Search experience.</span></span> <span data-ttu-id="1779f-105">Custom Autosuggest returns a list of suggested queries based on a partial query string that the user provides.</span><span class="sxs-lookup"><span data-stu-id="1779f-105">Custom Autosuggest returns a list of suggested queries based on a partial query string that the user provides.</span></span> <span data-ttu-id="1779f-106">With Custom Autosuggest, you provide custom search suggestions relevant to your search experience.</span><span class="sxs-lookup"><span data-stu-id="1779f-106">With Custom Autosuggest, you provide custom search suggestions relevant to your search experience.</span></span> <span data-ttu-id="1779f-107">You specify whether to return only custom suggestions or to also include Bing suggestions.</span><span class="sxs-lookup"><span data-stu-id="1779f-107">You specify whether to return only custom suggestions or to also include Bing suggestions.</span></span> <span data-ttu-id="1779f-108">If you include Bing suggestions, custom suggestions appear before the Bing suggestions.</span><span class="sxs-lookup"><span data-stu-id="1779f-108">If you include Bing suggestions, custom suggestions appear before the Bing suggestions.</span></span> <span data-ttu-id="1779f-109">Bing suggestions are restricted to the context of your Custom Search instance.</span><span class="sxs-lookup"><span data-stu-id="1779f-109">Bing suggestions are restricted to the context of your Custom Search instance.</span></span>

## <a name="configure-custom-autosuggest"></a><span data-ttu-id="1779f-110">Configure Custom Autosuggest</span><span class="sxs-lookup"><span data-stu-id="1779f-110">Configure Custom Autosuggest</span></span>
<span data-ttu-id="1779f-111">Use the following instructions to configure Custom Autosuggest for your Custom Search instance.</span><span class="sxs-lookup"><span data-stu-id="1779f-111">Use the following instructions to configure Custom Autosuggest for your Custom Search instance.</span></span>

1.  <span data-ttu-id="1779f-112">Sign in to [Custom Search](https://customsearch.ai).</span><span class="sxs-lookup"><span data-stu-id="1779f-112">Sign in to [Custom Search](https://customsearch.ai).</span></span>
2.  <span data-ttu-id="1779f-113">Click a Custom Search instance.</span><span class="sxs-lookup"><span data-stu-id="1779f-113">Click a Custom Search instance.</span></span> <span data-ttu-id="1779f-114">To create an instance, see [Create your first Bing Custom Search instance](quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="1779f-114">To create an instance, see [Create your first Bing Custom Search instance](quick-start.md).</span></span>
3.  <span data-ttu-id="1779f-115">Click the **Autosuggest** tab.</span><span class="sxs-lookup"><span data-stu-id="1779f-115">Click the **Autosuggest** tab.</span></span>

## <a name="enable-bing-suggestions"></a><span data-ttu-id="1779f-116">Enable Bing suggestions</span><span class="sxs-lookup"><span data-stu-id="1779f-116">Enable Bing suggestions</span></span>
<span data-ttu-id="1779f-117">To enable Bing suggestions, toggle the **Automatic Bing suggestions** slider to the on position.</span><span class="sxs-lookup"><span data-stu-id="1779f-117">To enable Bing suggestions, toggle the **Automatic Bing suggestions** slider to the on position.</span></span> <span data-ttu-id="1779f-118">The slider becomes blue.</span><span class="sxs-lookup"><span data-stu-id="1779f-118">The slider becomes blue.</span></span>

## <a name="add-suggestions"></a><span data-ttu-id="1779f-119">Add suggestions</span><span class="sxs-lookup"><span data-stu-id="1779f-119">Add suggestions</span></span>
<span data-ttu-id="1779f-120">To add a suggestion, enter it into the text box.</span><span class="sxs-lookup"><span data-stu-id="1779f-120">To add a suggestion, enter it into the text box.</span></span> <span data-ttu-id="1779f-121">Press the enter key or click the **+** icon.</span><span class="sxs-lookup"><span data-stu-id="1779f-121">Press the enter key or click the **+** icon.</span></span> <span data-ttu-id="1779f-122">Custom suggestions can be in any language and will appear before Bing suggestions.</span><span class="sxs-lookup"><span data-stu-id="1779f-122">Custom suggestions can be in any language and will appear before Bing suggestions.</span></span>

## <a name="upload-suggestions"></a><span data-ttu-id="1779f-123">Upload suggestions</span><span class="sxs-lookup"><span data-stu-id="1779f-123">Upload suggestions</span></span>
<span data-ttu-id="1779f-124">You can upload a list of suggestions from a file.</span><span class="sxs-lookup"><span data-stu-id="1779f-124">You can upload a list of suggestions from a file.</span></span> <span data-ttu-id="1779f-125">Place each suggestion on a separate line.</span><span class="sxs-lookup"><span data-stu-id="1779f-125">Place each suggestion on a separate line.</span></span> <span data-ttu-id="1779f-126">Click the upload icon and select your file.</span><span class="sxs-lookup"><span data-stu-id="1779f-126">Click the upload icon and select your file.</span></span>

## <a name="remove-suggestions"></a><span data-ttu-id="1779f-127">Remove suggestions</span><span class="sxs-lookup"><span data-stu-id="1779f-127">Remove suggestions</span></span>
<span data-ttu-id="1779f-128">To remove a suggestion, click the remove icon next to the suggestion you want to remove.</span><span class="sxs-lookup"><span data-stu-id="1779f-128">To remove a suggestion, click the remove icon next to the suggestion you want to remove.</span></span>

[!INCLUDE [publish or revert](./includes/publish-revert.md)]

  >[!NOTE]  
  ><span data-ttu-id="1779f-129">It may take up to 24 hours for Custom Autosuggest configuration changes to take effect.</span><span class="sxs-lookup"><span data-stu-id="1779f-129">It may take up to 24 hours for Custom Autosuggest configuration changes to take effect.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1779f-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="1779f-130">Next steps</span></span>

- [<span data-ttu-id="1779f-131">Get custom suggestions</span><span class="sxs-lookup"><span data-stu-id="1779f-131">Get custom suggestions</span></span>](./get-custom-suggestions.md)
- [<span data-ttu-id="1779f-132">Search your custom instance</span><span class="sxs-lookup"><span data-stu-id="1779f-132">Search your custom instance</span></span>](./search-your-custom-view.md)
- [<span data-ttu-id="1779f-133">Configure and consume custom hosted UI</span><span class="sxs-lookup"><span data-stu-id="1779f-133">Configure and consume custom hosted UI</span></span>](./hosted-ui.md)