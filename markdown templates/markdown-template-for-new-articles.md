---
title: Page title that displays in the browser tab and search results | Microsoft Docs
description: Article description that will be displayed on landing pages and in most search results
services: service-name
documentationcenter: dev-center-name
author: GitHub-alias-of-only-one-author
manager: manager-alias
ms.service: required
ms.devlang: may be required
ms.topic: article
ms.tgt_pltfrm: may be required
ms.workload: required
ms.date: mm/dd/yyyy
ms.author: Your MSFT alias or your full email address;semicolon separates two or more aliases
ms.openlocfilehash: 2d8f80b91111aff216986a8a89c92760e7633aec
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555940"
---
# <a name="markdown-template-for-azure-on-microsoft-docs"></a><span data-ttu-id="5bfbd-103">Markdown template for Azure on Microsoft Docs</span><span class="sxs-lookup"><span data-stu-id="5bfbd-103">Markdown template for Azure on Microsoft Docs</span></span>

<span data-ttu-id="5bfbd-104">Your article should have only one H1 heading, which you create with a single # sign.</span><span class="sxs-lookup"><span data-stu-id="5bfbd-104">Your article should have only one H1 heading, which you create with a single # sign.</span></span> <span data-ttu-id="5bfbd-105">The the H1 heading should always be followed by a descriptive paragraph that helps the customer understand what the article is about.</span><span class="sxs-lookup"><span data-stu-id="5bfbd-105">The the H1 heading should always be followed by a descriptive paragraph that helps the customer understand what the article is about.</span></span> <span data-ttu-id="5bfbd-106">It should contain keywords you think customers would use to search for this piece of content.</span><span class="sxs-lookup"><span data-stu-id="5bfbd-106">It should contain keywords you think customers would use to search for this piece of content.</span></span> <span data-ttu-id="5bfbd-107">Do not start the article with a note or tip - always start with an introductory paragraph.</span><span class="sxs-lookup"><span data-stu-id="5bfbd-107">Do not start the article with a note or tip - always start with an introductory paragraph.</span></span>

## <a name="headings"></a><span data-ttu-id="5bfbd-108">Headings</span><span class="sxs-lookup"><span data-stu-id="5bfbd-108">Headings</span></span> 

<span data-ttu-id="5bfbd-109">Two ## signs create an H2 heading - if your article needs to be structured with headings below the H1, you need to have at least TWO H2 headings.</span><span class="sxs-lookup"><span data-stu-id="5bfbd-109">Two ## signs create an H2 heading - if your article needs to be structured with headings below the H1, you need to have at least TWO H2 headings.</span></span>

<span data-ttu-id="5bfbd-110">H2 headings are rendered on the page as an automatic on-page TOC.</span><span class="sxs-lookup"><span data-stu-id="5bfbd-110">H2 headings are rendered on the page as an automatic on-page TOC.</span></span> <span data-ttu-id="5bfbd-111">Do not hand-code article navigation in an article.</span><span class="sxs-lookup"><span data-stu-id="5bfbd-111">Do not hand-code article navigation in an article.</span></span> <span data-ttu-id="5bfbd-112">Use the H2 headings to do that.</span><span class="sxs-lookup"><span data-stu-id="5bfbd-112">Use the H2 headings to do that.</span></span>

<span data-ttu-id="5bfbd-113">Within an H2 section, you can use three ### signs to create H3 headings.</span><span class="sxs-lookup"><span data-stu-id="5bfbd-113">Within an H2 section, you can use three ### signs to create H3 headings.</span></span> <span data-ttu-id="5bfbd-114">In our content, try to avoid going deeper than 3 heading layers - the headings are often hard to distinguish on the rendered page.</span><span class="sxs-lookup"><span data-stu-id="5bfbd-114">In our content, try to avoid going deeper than 3 heading layers - the headings are often hard to distinguish on the rendered page.</span></span> 

## <a name="images"></a><span data-ttu-id="5bfbd-115">Images</span><span class="sxs-lookup"><span data-stu-id="5bfbd-115">Images</span></span>
<span data-ttu-id="5bfbd-116">You can use images throughout a technical article.</span><span class="sxs-lookup"><span data-stu-id="5bfbd-116">You can use images throughout a technical article.</span></span> <span data-ttu-id="5bfbd-117">Make sure you include alt text for all your images.</span><span class="sxs-lookup"><span data-stu-id="5bfbd-117">Make sure you include alt text for all your images.</span></span> <span data-ttu-id="5bfbd-118">This helps accessibility and discoverability.</span><span class="sxs-lookup"><span data-stu-id="5bfbd-118">This helps accessibility and discoverability.</span></span>

<span data-ttu-id="5bfbd-119">This image of the GitHub Octocats uses in-line image references:</span><span class="sxs-lookup"><span data-stu-id="5bfbd-119">This image of the GitHub Octocats uses in-line image references:</span></span>

 ![GitHub Octocats using inline link](./media/markdown-template-for-new-articles/octocats.png)

<span data-ttu-id="5bfbd-121">The sample markdown looks like this:</span><span class="sxs-lookup"><span data-stu-id="5bfbd-121">The sample markdown looks like this:</span></span>
```
![GitHub Octocats using inline link](./media/markdown-template-for-new-articles/octocats.png)
```

<span data-ttu-id="5bfbd-122">This second image of the octocats uses reference style syntax, where you define the target as "5" and at the bottom of the article, and you list the path to image 5 in a reference section.</span><span class="sxs-lookup"><span data-stu-id="5bfbd-122">This second image of the octocats uses reference style syntax, where you define the target as "5" and at the bottom of the article, and you list the path to image 5 in a reference section.</span></span>

 ![GitHub Octocats using ref style link][5]

 <span data-ttu-id="5bfbd-124">The sample markdown looks like this:</span><span class="sxs-lookup"><span data-stu-id="5bfbd-124">The sample markdown looks like this:</span></span>
 ```
  ![GitHub Octocats image][5]

  <!--Image references-->
  [5]: ./media/markdown-template-for-new-articles/octocats.png
 ``` 

## <a name="linking"></a><span data-ttu-id="5bfbd-125">Linking</span><span class="sxs-lookup"><span data-stu-id="5bfbd-125">Linking</span></span>
<span data-ttu-id="5bfbd-126">Your article will most likely contain links.</span><span class="sxs-lookup"><span data-stu-id="5bfbd-126">Your article will most likely contain links.</span></span> <span data-ttu-id="5bfbd-127">Here's sample markdown for a link to a target that is not on the docs.microsoft.com site:</span><span class="sxs-lookup"><span data-stu-id="5bfbd-127">Here's sample markdown for a link to a target that is not on the docs.microsoft.com site:</span></span>

    [link text](url)
    [Scott Guthrie's blog](http://weblogs.asp.net/scottgu)

<span data-ttu-id="5bfbd-128">Here's sample markdown for a link to another technical article in the azure-docs-pr repository:</span><span class="sxs-lookup"><span data-stu-id="5bfbd-128">Here's sample markdown for a link to another technical article in the azure-docs-pr repository:</span></span>

    [link text](../service-directory/article-name.md)
    [ExpressRoute circuits and routing domains](../expressroute/expressroute-circuit-peerings.md)

<span data-ttu-id="5bfbd-129">You can also use so-called reference style links where you define the links at the bottom of the article, and reference them like this:</span><span class="sxs-lookup"><span data-stu-id="5bfbd-129">You can also use so-called reference style links where you define the links at the bottom of the article, and reference them like this:</span></span>

    I get 10 times more traffic from [Google][gog] than from [Yahoo][yah] or [MSN][msn].

<span data-ttu-id="5bfbd-130">For more information about linking, see the [linking guidance](../contributor-guide/create-links-markdown.md)</span><span class="sxs-lookup"><span data-stu-id="5bfbd-130">For more information about linking, see the [linking guidance](../contributor-guide/create-links-markdown.md)</span></span>

## <a name="notes-and-tips"></a><span data-ttu-id="5bfbd-131">Notes and tips</span><span class="sxs-lookup"><span data-stu-id="5bfbd-131">Notes and tips</span></span>
<span data-ttu-id="5bfbd-132">You should use notes and tips judiciously.</span><span class="sxs-lookup"><span data-stu-id="5bfbd-132">You should use notes and tips judiciously.</span></span> <span data-ttu-id="5bfbd-133">A little bit goes a long way.</span><span class="sxs-lookup"><span data-stu-id="5bfbd-133">A little bit goes a long way.</span></span> <span data-ttu-id="5bfbd-134">Put the text of the note or tip on the line after the custom markdown extension.</span><span class="sxs-lookup"><span data-stu-id="5bfbd-134">Put the text of the note or tip on the line after the custom markdown extension.</span></span>

```
> [!NOTE]
> Note text.

> [!TIP]
> Tip text.

> [!IMPORTANT]
> Important text.
```

## <a name="lists"></a><span data-ttu-id="5bfbd-135">Lists</span><span class="sxs-lookup"><span data-stu-id="5bfbd-135">Lists</span></span>

<span data-ttu-id="5bfbd-136">A simple numbered list in markdown creates a numbered list on your published page.</span><span class="sxs-lookup"><span data-stu-id="5bfbd-136">A simple numbered list in markdown creates a numbered list on your published page.</span></span>

1. <span data-ttu-id="5bfbd-137">First step.</span><span class="sxs-lookup"><span data-stu-id="5bfbd-137">First step.</span></span>
2. <span data-ttu-id="5bfbd-138">Second step.</span><span class="sxs-lookup"><span data-stu-id="5bfbd-138">Second step.</span></span>
3. <span data-ttu-id="5bfbd-139">Third step.</span><span class="sxs-lookup"><span data-stu-id="5bfbd-139">Third step.</span></span>

<span data-ttu-id="5bfbd-140">Use hyphens to create unordered lists:</span><span class="sxs-lookup"><span data-stu-id="5bfbd-140">Use hyphens to create unordered lists:</span></span>

- <span data-ttu-id="5bfbd-141">Item</span><span class="sxs-lookup"><span data-stu-id="5bfbd-141">Item</span></span>
- <span data-ttu-id="5bfbd-142">Item</span><span class="sxs-lookup"><span data-stu-id="5bfbd-142">Item</span></span>
- <span data-ttu-id="5bfbd-143">Item</span><span class="sxs-lookup"><span data-stu-id="5bfbd-143">Item</span></span>


## <a name="next-steps"></a><span data-ttu-id="5bfbd-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="5bfbd-144">Next steps</span></span>
<span data-ttu-id="5bfbd-145">Every topic should end with 1 to 3 concrete, action oriented next steps and links to the next logical piece of content to keep the customer engaged.</span><span class="sxs-lookup"><span data-stu-id="5bfbd-145">Every topic should end with 1 to 3 concrete, action oriented next steps and links to the next logical piece of content to keep the customer engaged.</span></span> 

- <span data-ttu-id="5bfbd-146">See the [content quality guidelines](../contributor-guide/contributor-guide-pr-criteria.md#non-blocking-content-quality-items) for an example of what a good next steps section looks like.</span><span class="sxs-lookup"><span data-stu-id="5bfbd-146">See the [content quality guidelines](../contributor-guide/contributor-guide-pr-criteria.md#non-blocking-content-quality-items) for an example of what a good next steps section looks like.</span></span> 

- <span data-ttu-id="5bfbd-147">Review the [custom markdown extensions](../contributor-guide/custom-markdown-extensions.md) we use for videos, reusable content, selectors, and other content features.</span><span class="sxs-lookup"><span data-stu-id="5bfbd-147">Review the [custom markdown extensions](../contributor-guide/custom-markdown-extensions.md) we use for videos, reusable content, selectors, and other content features.</span></span>

- <span data-ttu-id="5bfbd-148">Make sure your articles meet [the content quality guidelines](../contributor-guide/contributor-guide-pr-criteria.md) before you sign-off on a PR.</span><span class="sxs-lookup"><span data-stu-id="5bfbd-148">Make sure your articles meet [the content quality guidelines](../contributor-guide/contributor-guide-pr-criteria.md) before you sign-off on a PR.</span></span> 


<!--Image references-->
[5]: ./media/markdown-template-for-new-articles/octocats.png

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[gog]: http://google.com/        
[yah]: http://search.yahoo.com/  
[msn]: http://search.msn.com/    
