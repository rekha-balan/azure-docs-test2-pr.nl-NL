---
title: Azure Batch render manager support
description: Using Azure for rendering using Azure Batch render manager integration
services: batch
author: mscurrell
ms.author: markscu
ms.date: 08/02/2018
ms.topic: conceptual
ms.openlocfilehash: 798b2b457016856662f392af25d987788f73c242
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866898"
---
# <a name="using-azure-batch-with-render-farm-managers"></a><span data-ttu-id="65751-103">Using Azure Batch with render farm managers</span><span class="sxs-lookup"><span data-stu-id="65751-103">Using Azure Batch with render farm managers</span></span>

<span data-ttu-id="65751-104">If you're using an existing on-premises render farm, then it's highly likely that a render manager controls the render farm capacity and render jobs.</span><span class="sxs-lookup"><span data-stu-id="65751-104">If you're using an existing on-premises render farm, then it's highly likely that a render manager controls the render farm capacity and render jobs.</span></span>

<span data-ttu-id="65751-105">Azure provides either built-in support or add-ons for popular render managers.</span><span class="sxs-lookup"><span data-stu-id="65751-105">Azure provides either built-in support or add-ons for popular render managers.</span></span> <span data-ttu-id="65751-106">You can then add and remove Azure VMs, including VMs with the pay-for-use application licensing and low-priority VMs.</span><span class="sxs-lookup"><span data-stu-id="65751-106">You can then add and remove Azure VMs, including VMs with the pay-for-use application licensing and low-priority VMs.</span></span>

<span data-ttu-id="65751-107">The following render managers are supported:</span><span class="sxs-lookup"><span data-stu-id="65751-107">The following render managers are supported:</span></span>

* [<span data-ttu-id="65751-108">PipelineFX Qube!</span><span class="sxs-lookup"><span data-stu-id="65751-108">PipelineFX Qube!</span></span>](https://www.pipelinefx.com/)
* [<span data-ttu-id="65751-109">Royal Render</span><span class="sxs-lookup"><span data-stu-id="65751-109">Royal Render</span></span>](http://www.royalrender.de/)
* [<span data-ttu-id="65751-110">Thinkbox Deadline</span><span class="sxs-lookup"><span data-stu-id="65751-110">Thinkbox Deadline</span></span>](https://deadline.thinkboxsoftware.com/)

## <a name="using-azure-with-pipelinefx-qube"></a><span data-ttu-id="65751-111">Using Azure with PipelineFX Qube</span><span class="sxs-lookup"><span data-stu-id="65751-111">Using Azure with PipelineFX Qube</span></span>

<span data-ttu-id="65751-112">Scripts and instructions to enable Azure Batch pool VMs to be used as Qube workers are in [the GitHub repository](https://github.com/Azure/azure-qube).</span><span class="sxs-lookup"><span data-stu-id="65751-112">Scripts and instructions to enable Azure Batch pool VMs to be used as Qube workers are in [the GitHub repository](https://github.com/Azure/azure-qube).</span></span>

## <a name="using-azure-with-royal-render"></a><span data-ttu-id="65751-113">Using Azure with Royal Render</span><span class="sxs-lookup"><span data-stu-id="65751-113">Using Azure with Royal Render</span></span>

<span data-ttu-id="65751-114">Royal Render has Azure and Azure Batch integration built-in, allowing you to extend a render farm with Azure-based VMs.</span><span class="sxs-lookup"><span data-stu-id="65751-114">Royal Render has Azure and Azure Batch integration built-in, allowing you to extend a render farm with Azure-based VMs.</span></span> <span data-ttu-id="65751-115">For a summary, see [the help files](http://www.royalrender.de/help8/index.html?Cloudrendering.html).</span><span class="sxs-lookup"><span data-stu-id="65751-115">For a summary, see [the help files](http://www.royalrender.de/help8/index.html?Cloudrendering.html).</span></span>

<span data-ttu-id="65751-116">For an example of a Royal Render customer using the Azure integration, see the [Jellyfish Pictures customer story](https://customers.microsoft.com/en-gb/story/jellyfishpictures).</span><span class="sxs-lookup"><span data-stu-id="65751-116">For an example of a Royal Render customer using the Azure integration, see the [Jellyfish Pictures customer story](https://customers.microsoft.com/en-gb/story/jellyfishpictures).</span></span>

## <a name="using-azure-with-thinkbox-deadline"></a><span data-ttu-id="65751-117">Using Azure with Thinkbox Deadline</span><span class="sxs-lookup"><span data-stu-id="65751-117">Using Azure with Thinkbox Deadline</span></span>

<span data-ttu-id="65751-118">Scripts and instructions to enable Azure Batch pool VMs to be used as Deadline slaves are in [the GitHub repository](https://github.com/Azure/azure-deadline).</span><span class="sxs-lookup"><span data-stu-id="65751-118">Scripts and instructions to enable Azure Batch pool VMs to be used as Deadline slaves are in [the GitHub repository](https://github.com/Azure/azure-deadline).</span></span>

## <a name="next-steps"></a><span data-ttu-id="65751-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="65751-119">Next steps</span></span>

<span data-ttu-id="65751-120">Try out the Azure Batch integration for your render manager, using the appropriate plug-in and instructions on GitHub, where applicable.</span><span class="sxs-lookup"><span data-stu-id="65751-120">Try out the Azure Batch integration for your render manager, using the appropriate plug-in and instructions on GitHub, where applicable.</span></span>