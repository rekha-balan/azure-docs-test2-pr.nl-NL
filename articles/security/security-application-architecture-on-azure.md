---
title: Integrate security into your Azure architectural designs | Microsoft Docs
description: " This article will help you understand the application and services architecture on Azure to make it easier to integrate security into design and implementation. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 4f2d9386-bda3-4ec8-8b1a-cd0c11242ffc
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 91e46d690d3e7c298bc3b4020cc383ca99c43c4f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550514"
---
# <a name="application-architecture-on-azure"></a><span data-ttu-id="d4298-103">Application architecture on Azure</span><span class="sxs-lookup"><span data-stu-id="d4298-103">Application architecture on Azure</span></span>
<span data-ttu-id="d4298-104">To help secure your cloud-based solutions on Microsoft Azure, a strong architectural foundation is critical.</span><span class="sxs-lookup"><span data-stu-id="d4298-104">To help secure your cloud-based solutions on Microsoft Azure, a strong architectural foundation is critical.</span></span> <span data-ttu-id="d4298-105">Architects, designers, and implementers all benefit from a strong knowledge of application and services architecture.</span><span class="sxs-lookup"><span data-stu-id="d4298-105">Architects, designers, and implementers all benefit from a strong knowledge of application and services architecture.</span></span> <span data-ttu-id="d4298-106">This foundational knowledge helps you understand all the components of your cloud-based solutions and make it easier to integrate security into all aspects of your design and implementation.</span><span class="sxs-lookup"><span data-stu-id="d4298-106">This foundational knowledge helps you understand all the components of your cloud-based solutions and make it easier to integrate security into all aspects of your design and implementation.</span></span>

<span data-ttu-id="d4298-107">We have the following to help you with your architectural investigations and designs:</span><span class="sxs-lookup"><span data-stu-id="d4298-107">We have the following to help you with your architectural investigations and designs:</span></span>

* <span data-ttu-id="d4298-108">Architectural infographics</span><span class="sxs-lookup"><span data-stu-id="d4298-108">Architectural infographics</span></span>
* <span data-ttu-id="d4298-109">Architectural blueprints</span><span class="sxs-lookup"><span data-stu-id="d4298-109">Architectural blueprints</span></span>
* <span data-ttu-id="d4298-110">Cloud and enterprise symbol set</span><span class="sxs-lookup"><span data-stu-id="d4298-110">Cloud and enterprise symbol set</span></span>
* <span data-ttu-id="d4298-111">3D blueprint Visio template</span><span class="sxs-lookup"><span data-stu-id="d4298-111">3D blueprint Visio template</span></span>

## <a name="architectural-infographics"></a><span data-ttu-id="d4298-112">Architectural infographics</span><span class="sxs-lookup"><span data-stu-id="d4298-112">Architectural infographics</span></span>
<span data-ttu-id="d4298-113">Microsoft publishes several architectural related posters/infographics.</span><span class="sxs-lookup"><span data-stu-id="d4298-113">Microsoft publishes several architectural related posters/infographics.</span></span> <span data-ttu-id="d4298-114">They include:</span><span class="sxs-lookup"><span data-stu-id="d4298-114">They include:</span></span>

* [<span data-ttu-id="d4298-115">Building Real-World Cloud Applications</span><span class="sxs-lookup"><span data-stu-id="d4298-115">Building Real-World Cloud Applications</span></span>](https://azure.microsoft.com/documentation/infographics/building-real-world-cloud-apps/)
* [<span data-ttu-id="d4298-116">Scaling with Cloud Services</span><span class="sxs-lookup"><span data-stu-id="d4298-116">Scaling with Cloud Services</span></span>](https://azure.microsoft.com/documentation/infographics/cloud-services/)

## <a name="architectural-blueprints"></a><span data-ttu-id="d4298-117">Architectural blueprints</span><span class="sxs-lookup"><span data-stu-id="d4298-117">Architectural blueprints</span></span>
<span data-ttu-id="d4298-118">Microsoft publishes a set of high-level [architectural blueprints](http://aka.ms/azblueprints) showing how to build specific types of systems using Microsoft products.</span><span class="sxs-lookup"><span data-stu-id="d4298-118">Microsoft publishes a set of high-level [architectural blueprints](http://aka.ms/azblueprints) showing how to build specific types of systems using Microsoft products.</span></span>
<span data-ttu-id="d4298-119">Each blueprint includes a:</span><span class="sxs-lookup"><span data-stu-id="d4298-119">Each blueprint includes a:</span></span>

* <span data-ttu-id="d4298-120">Flat 2D Visio 2003-based file that you can download and modify</span><span class="sxs-lookup"><span data-stu-id="d4298-120">Flat 2D Visio 2003-based file that you can download and modify</span></span>
* <span data-ttu-id="d4298-121">Colorful 3D perspective PDF file to introduce the blueprint to less technical audiences</span><span class="sxs-lookup"><span data-stu-id="d4298-121">Colorful 3D perspective PDF file to introduce the blueprint to less technical audiences</span></span>
* <span data-ttu-id="d4298-122">Video that walks through the 3D version</span><span class="sxs-lookup"><span data-stu-id="d4298-122">Video that walks through the 3D version</span></span>

## <a name="cloud-and-enterprise-symbol-set"></a><span data-ttu-id="d4298-123">Cloud and enterprise symbol set</span><span class="sxs-lookup"><span data-stu-id="d4298-123">Cloud and enterprise symbol set</span></span>
<span data-ttu-id="d4298-124">[View the Visio and symbols training video](http://aka.ms/CnESymbolsVideo) and then [download the Cloud and Enterprise Symbol set](http://aka.ms/CnESymbols) to help create technical materials that describe Azure, Windows Server, SQL Server and more.</span><span class="sxs-lookup"><span data-stu-id="d4298-124">[View the Visio and symbols training video](http://aka.ms/CnESymbolsVideo) and then [download the Cloud and Enterprise Symbol set](http://aka.ms/CnESymbols) to help create technical materials that describe Azure, Windows Server, SQL Server and more.</span></span> <span data-ttu-id="d4298-125">You can use the symbols in architecture diagrams, training materials, presentations, datasheets, infographics, whitepapers, and even third party books if the book trains people to use Microsoft products.</span><span class="sxs-lookup"><span data-stu-id="d4298-125">You can use the symbols in architecture diagrams, training materials, presentations, datasheets, infographics, whitepapers, and even third party books if the book trains people to use Microsoft products.</span></span> <span data-ttu-id="d4298-126">However, they are not meant for use in user interfaces.</span><span class="sxs-lookup"><span data-stu-id="d4298-126">However, they are not meant for use in user interfaces.</span></span>

## <a name="3d-blueprint-visio-template"></a><span data-ttu-id="d4298-127">3D blueprint Visio template</span><span class="sxs-lookup"><span data-stu-id="d4298-127">3D blueprint Visio template</span></span>
<span data-ttu-id="d4298-128">The 3D versions of the [Microsoft Architecture Blueprints](http://aka.ms/azblueprints) were initially created in a non-Microsoft tool.</span><span class="sxs-lookup"><span data-stu-id="d4298-128">The 3D versions of the [Microsoft Architecture Blueprints](http://aka.ms/azblueprints) were initially created in a non-Microsoft tool.</span></span> <span data-ttu-id="d4298-129">A new Visio 2013 (and later) template shipped on August 5, 2015 as part of a [Microsoft Architecture certification course distributed on EDX.ORG](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course).</span><span class="sxs-lookup"><span data-stu-id="d4298-129">A new Visio 2013 (and later) template shipped on August 5, 2015 as part of a [Microsoft Architecture certification course distributed on EDX.ORG](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course).</span></span>

<span data-ttu-id="d4298-130">The template is also available outside the course.</span><span class="sxs-lookup"><span data-stu-id="d4298-130">The template is also available outside the course.</span></span>

* <span data-ttu-id="d4298-131">[View the training video](http://aka.ms/3dBlueprintTemplateVideo) first so you know what it can do</span><span class="sxs-lookup"><span data-stu-id="d4298-131">[View the training video](http://aka.ms/3dBlueprintTemplateVideo) first so you know what it can do</span></span>
* <span data-ttu-id="d4298-132">Download the [Microsoft 3d Blueprint Visio Template](http://aka.ms/3DBlueprintTemplate)</span><span class="sxs-lookup"><span data-stu-id="d4298-132">Download the [Microsoft 3d Blueprint Visio Template](http://aka.ms/3DBlueprintTemplate)</span></span>
* <span data-ttu-id="d4298-133">Download the [Cloud and Enterprise Symbols](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) to use with the 3D template</span><span class="sxs-lookup"><span data-stu-id="d4298-133">Download the [Cloud and Enterprise Symbols](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) to use with the 3D template</span></span>
