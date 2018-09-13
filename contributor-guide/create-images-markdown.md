---
title: Create images in markdown
description: Explains how to create images in markdown according to guidelines set for the Azure repositories.
services: ''
solutions: ''
documentationcenter: ''
author: kenhoff
manager: ilanas
editor: tysonn
ms.service: contributor-guide
ms.devlang: ''
ms.topic: article
ms.tgt_pltfrm: ''
ms.workload: ''
ms.date: 06/25/2015
ms.author: kenhoff
ms.openlocfilehash: dce588150f0a20a91a320869eb5f27b30427624c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554267"
---
# <a name="create-images-in-markdown"></a><span data-ttu-id="dfd3a-103">Create images in markdown</span><span class="sxs-lookup"><span data-stu-id="dfd3a-103">Create images in markdown</span></span>
## <a name="image-folder-creation-and-link-syntax"></a><span data-ttu-id="dfd3a-104">Image folder creation and link syntax</span><span class="sxs-lookup"><span data-stu-id="dfd3a-104">Image folder creation and link syntax</span></span>
<span data-ttu-id="dfd3a-105">For a new article, you'll need to create a folder in the following location:</span><span class="sxs-lookup"><span data-stu-id="dfd3a-105">For a new article, you'll need to create a folder in the following location:</span></span>

    /articles/<service-directory>/media/<article-name>/

<span data-ttu-id="dfd3a-106">For example:</span><span class="sxs-lookup"><span data-stu-id="dfd3a-106">For example:</span></span>

    /articles/app-service/media/app-service-enterprise-multichannel-apps/

<span data-ttu-id="dfd3a-107">After you create the folder and added images to it, use the following syntax to create images in your article:</span><span class="sxs-lookup"><span data-stu-id="dfd3a-107">After you create the folder and added images to it, use the following syntax to create images in your article:</span></span>

```
![Alt image text](./media/article-name/your-image-filename.png)
```
<span data-ttu-id="dfd3a-108">Example:</span><span class="sxs-lookup"><span data-stu-id="dfd3a-108">Example:</span></span>

<span data-ttu-id="dfd3a-109">See [the markdown template](../markdown%20templates/markdown-template-for-new-articles.md) for an example.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-109">See [the markdown template](../markdown%20templates/markdown-template-for-new-articles.md) for an example.</span></span>  <span data-ttu-id="dfd3a-110">The image reference links in this markdown template are designed to be at the bottom of the template.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-110">The image reference links in this markdown template are designed to be at the bottom of the template.</span></span>

## <a name="image-guidelines-specific-to-azure-technical-content"></a><span data-ttu-id="dfd3a-111">Image guidelines specific to azure technical content</span><span class="sxs-lookup"><span data-stu-id="dfd3a-111">Image guidelines specific to azure technical content</span></span>
<span data-ttu-id="dfd3a-112">Screenshots are currently encouraged if it's not possible to include repro steps.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-112">Screenshots are currently encouraged if it's not possible to include repro steps.</span></span> <span data-ttu-id="dfd3a-113">Do write your content so that the content can stand without the screenshots if necessary.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-113">Do write your content so that the content can stand without the screenshots if necessary.</span></span>

<span data-ttu-id="dfd3a-114">Use the following guidelines when creating and including art files:</span><span class="sxs-lookup"><span data-stu-id="dfd3a-114">Use the following guidelines when creating and including art files:</span></span>

* <span data-ttu-id="dfd3a-115">Do not share art files across documents.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-115">Do not share art files across documents.</span></span> <span data-ttu-id="dfd3a-116">Copy the file you need and add it to the media folder for your specific topic.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-116">Copy the file you need and add it to the media folder for your specific topic.</span></span> <span data-ttu-id="dfd3a-117">Sharing between files is discouraged because  it is easier to remove deprecated content and images which keeps the repo clean.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-117">Sharing between files is discouraged because  it is easier to remove deprecated content and images which keeps the repo clean.</span></span>
* <span data-ttu-id="dfd3a-118">File formats: Use .png files - they are higher quality and maintain their quality during the localization process.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-118">File formats: Use .png files - they are higher quality and maintain their quality during the localization process.</span></span> <span data-ttu-id="dfd3a-119">Other file formats do not maintain their quality as well.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-119">Other file formats do not maintain their quality as well.</span></span> <span data-ttu-id="dfd3a-120">The .jpeg format is permitted, but not preferred.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-120">The .jpeg format is permitted, but not preferred.</span></span>  <span data-ttu-id="dfd3a-121">No animated GIF files.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-121">No animated GIF files.</span></span>
* <span data-ttu-id="dfd3a-122">Use red squares of the default width provided in Paint (5 px) to call attention to particular elements in screenshots.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-122">Use red squares of the default width provided in Paint (5 px) to call attention to particular elements in screenshots.</span></span>  
  
    <span data-ttu-id="dfd3a-123">Example:</span><span class="sxs-lookup"><span data-stu-id="dfd3a-123">Example:</span></span>
  
    ![This is an example of a red square used as a callout.](./media/create-images-markdown/gs13noauth.png)
* <span data-ttu-id="dfd3a-125">When it makes sense, feel free to crop images so the UI elements will be displayed in full size.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-125">When it makes sense, feel free to crop images so the UI elements will be displayed in full size.</span></span> <span data-ttu-id="dfd3a-126">Make sure that the context is clear to users, though.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-126">Make sure that the context is clear to users, though.</span></span>
* <span data-ttu-id="dfd3a-127">Avoid whitespace on edges of screenshots.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-127">Avoid whitespace on edges of screenshots.</span></span> <span data-ttu-id="dfd3a-128">If you crop a screenshot in a way that leaves white background at the edges, add a single pixel gray border around the image.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-128">If you crop a screenshot in a way that leaves white background at the edges, add a single pixel gray border around the image.</span></span>  <span data-ttu-id="dfd3a-129">If using Paint, use the lighter gray in the default color pallete (0xC3C3C3).</span><span class="sxs-lookup"><span data-stu-id="dfd3a-129">If using Paint, use the lighter gray in the default color pallete (0xC3C3C3).</span></span> <span data-ttu-id="dfd3a-130">If using some other graphic app, the RGB color is R195, G195, 195.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-130">If using some other graphic app, the RGB color is R195, G195, 195.</span></span> <span data-ttu-id="dfd3a-131">You can easily add a gray border around an image in Visio--to do this, select the image, select Line, and ensure the the correct color is set, and then change the line weight to 1 1/2 pt.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-131">You can easily add a gray border around an image in Visio--to do this, select the image, select Line, and ensure the the correct color is set, and then change the line weight to 1 1/2 pt.</span></span>  <span data-ttu-id="dfd3a-132">Screenshots should have a 1-pixel-wide gray border so that white areas of the screenshot do not blur into the web page.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-132">Screenshots should have a 1-pixel-wide gray border so that white areas of the screenshot do not blur into the web page.</span></span>
  
    <span data-ttu-id="dfd3a-133">Example:</span><span class="sxs-lookup"><span data-stu-id="dfd3a-133">Example:</span></span>
  
    ![This is an example of a gray border around whitespace.](./media/create-images-markdown/agent.png)
  
    <span data-ttu-id="dfd3a-135">For a tool to help automate the process of adding the required border to images, see [AddACOMBorder tool - How to automate the process of adding the required 1 pixel grey border to ACOM images](https://github.com/Azure/Azure-CSI-Content-Tools/tree/master/Tools/AddACOMImageBorder).</span><span class="sxs-lookup"><span data-stu-id="dfd3a-135">For a tool to help automate the process of adding the required border to images, see [AddACOMBorder tool - How to automate the process of adding the required 1 pixel grey border to ACOM images](https://github.com/Azure/Azure-CSI-Content-Tools/tree/master/Tools/AddACOMImageBorder).</span></span>
* <span data-ttu-id="dfd3a-136">Conceptual images with whitespace do not need a gray border.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-136">Conceptual images with whitespace do not need a gray border.</span></span>  
  
    <span data-ttu-id="dfd3a-137">Example:</span><span class="sxs-lookup"><span data-stu-id="dfd3a-137">Example:</span></span>
  
    ![This is an example of a conceptual image with whitespace and no gray border.](./media/create-images-markdown/ic727360.png)
* <span data-ttu-id="dfd3a-139">Try not to make an image too wide.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-139">Try not to make an image too wide.</span></span>  <span data-ttu-id="dfd3a-140">Images will be automatically resized if they are too wide.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-140">Images will be automatically resized if they are too wide.</span></span> <span data-ttu-id="dfd3a-141">However, the resizing sometimes causes fuzziness, so we recommend that you limit the width of your images to 780 px, and manually resize images before submission if necessary.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-141">However, the resizing sometimes causes fuzziness, so we recommend that you limit the width of your images to 780 px, and manually resize images before submission if necessary.</span></span>
* <span data-ttu-id="dfd3a-142">Show command outputs in screenshots.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-142">Show command outputs in screenshots.</span></span>  <span data-ttu-id="dfd3a-143">If your article includes steps where the user is working within a shell, it's useful to show command output in screenshots.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-143">If your article includes steps where the user is working within a shell, it's useful to show command output in screenshots.</span></span> <span data-ttu-id="dfd3a-144">In this case, restricting your shell width to about 72 characters generally ensures that your image will remain within the 780 px width guideline.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-144">In this case, restricting your shell width to about 72 characters generally ensures that your image will remain within the 780 px width guideline.</span></span> <span data-ttu-id="dfd3a-145">Before taking a screenshot of output, resize the window so that just the relevant command and output is shown (optionally with a blank line on either side).</span><span class="sxs-lookup"><span data-stu-id="dfd3a-145">Before taking a screenshot of output, resize the window so that just the relevant command and output is shown (optionally with a blank line on either side).</span></span>
* <span data-ttu-id="dfd3a-146">Take whole screenshots of windows when possible.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-146">Take whole screenshots of windows when possible.</span></span> <span data-ttu-id="dfd3a-147">When taking a screenshot of a browser window, resize your browser window to 780 px wide or less, and keep the height of the browser window as short as possible such that your application fits within the window.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-147">When taking a screenshot of a browser window, resize your browser window to 780 px wide or less, and keep the height of the browser window as short as possible such that your application fits within the window.</span></span>
  
    <span data-ttu-id="dfd3a-148">Example:</span><span class="sxs-lookup"><span data-stu-id="dfd3a-148">Example:</span></span>
  
    ![This is an example of a browser window screenshot.](./media/create-images-markdown/helloworldlocal.png)
* <span data-ttu-id="dfd3a-150">Use caution with what information is revealed in screenshots.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-150">Use caution with what information is revealed in screenshots.</span></span>  <span data-ttu-id="dfd3a-151">Do not reveal internal company information or personal information.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-151">Do not reveal internal company information or personal information.</span></span>
* <span data-ttu-id="dfd3a-152">In conceptual art or diagrams, use the official icons in the Cloud and Enterprise symbol and icon set.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-152">In conceptual art or diagrams, use the official icons in the Cloud and Enterprise symbol and icon set.</span></span> <span data-ttu-id="dfd3a-153">A public set is available at http://aka.ms/CnESymbols.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-153">A public set is available at http://aka.ms/CnESymbols.</span></span>
* <span data-ttu-id="dfd3a-154">Replace personal or private information in screenshots with placeholder text enclosed in angle brackets.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-154">Replace personal or private information in screenshots with placeholder text enclosed in angle brackets.</span></span> <span data-ttu-id="dfd3a-155">This includes user names, subscription IDs, and other related info.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-155">This includes user names, subscription IDs, and other related info.</span></span> <span data-ttu-id="dfd3a-156">Personal names can be replaced with an [approved fictious name](https://aka.ms/ficticiousnames)(Employee-only link).</span><span class="sxs-lookup"><span data-stu-id="dfd3a-156">Personal names can be replaced with an [approved fictious name](https://aka.ms/ficticiousnames)(Employee-only link).</span></span> <span data-ttu-id="dfd3a-157">Do not use the crayon or marker tip in Paint to obscure or blur personal or private information.</span><span class="sxs-lookup"><span data-stu-id="dfd3a-157">Do not use the crayon or marker tip in Paint to obscure or blur personal or private information.</span></span>
  
  <span data-ttu-id="dfd3a-158">The following image has been correctly updated to replace the actual **subscription ID** with placeholder information:</span><span class="sxs-lookup"><span data-stu-id="dfd3a-158">The following image has been correctly updated to replace the actual **subscription ID** with placeholder information:</span></span>
  
  ![Private information replaced with placeholder](./media/create-images-markdown/placeholder-in-screenshot-correct.png)

### <a name="contributors-guide-links"></a><span data-ttu-id="dfd3a-160">Contributors' Guide Links</span><span class="sxs-lookup"><span data-stu-id="dfd3a-160">Contributors' Guide Links</span></span>
* [<span data-ttu-id="dfd3a-161">Overview article</span><span class="sxs-lookup"><span data-stu-id="dfd3a-161">Overview article</span></span>](../README.md)
* [<span data-ttu-id="dfd3a-162">Index of guidance articles</span><span class="sxs-lookup"><span data-stu-id="dfd3a-162">Index of guidance articles</span></span>](contributor-guide-index.md)

