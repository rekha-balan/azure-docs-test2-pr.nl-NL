---
title: Azure reserved resource name errors | Microsoft Docs
description: Describes how to resolve errors when providing a resource name that includes a reserved word.
services: azure-resource-manager
documentationcenter: ''
author: tfitzmac
manager: timlt
editor: ''
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: troubleshooting
ms.date: 11/08/2017
ms.author: tomfitz
ms.openlocfilehash: b91a53d17d64afb0a56f745505f10e8cabbc22cc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869712"
---
# <a name="resolve-reserved-resource-name-errors"></a><span data-ttu-id="053af-103">Resolve reserved resource name errors</span><span class="sxs-lookup"><span data-stu-id="053af-103">Resolve reserved resource name errors</span></span>

<span data-ttu-id="053af-104">This article describes the error you encounter when deploying a resource that includes a reserved word in its name.</span><span class="sxs-lookup"><span data-stu-id="053af-104">This article describes the error you encounter when deploying a resource that includes a reserved word in its name.</span></span>

## <a name="symptom"></a><span data-ttu-id="053af-105">Symptom</span><span class="sxs-lookup"><span data-stu-id="053af-105">Symptom</span></span>

<span data-ttu-id="053af-106">When deploying a resource that is available through a public endpoint, you may receive the following error:</span><span class="sxs-lookup"><span data-stu-id="053af-106">When deploying a resource that is available through a public endpoint, you may receive the following error:</span></span>

```
Code=ReservedResourceName;
Message=The resource name <resource-name> or a part of the name is a trademarked or reserved word.
```

## <a name="cause"></a><span data-ttu-id="053af-107">Cause</span><span class="sxs-lookup"><span data-stu-id="053af-107">Cause</span></span>

<span data-ttu-id="053af-108">Resources that have a public endpoint cannot use reserved words or trademarks in the name.</span><span class="sxs-lookup"><span data-stu-id="053af-108">Resources that have a public endpoint cannot use reserved words or trademarks in the name.</span></span>

<span data-ttu-id="053af-109">The following words are reserved:</span><span class="sxs-lookup"><span data-stu-id="053af-109">The following words are reserved:</span></span>

* <span data-ttu-id="053af-110">ACCESS</span><span class="sxs-lookup"><span data-stu-id="053af-110">ACCESS</span></span>
* <span data-ttu-id="053af-111">AZURE</span><span class="sxs-lookup"><span data-stu-id="053af-111">AZURE</span></span>
* <span data-ttu-id="053af-112">BING</span><span class="sxs-lookup"><span data-stu-id="053af-112">BING</span></span>
* <span data-ttu-id="053af-113">BIZSPARK</span><span class="sxs-lookup"><span data-stu-id="053af-113">BIZSPARK</span></span>
* <span data-ttu-id="053af-114">BIZTALK</span><span class="sxs-lookup"><span data-stu-id="053af-114">BIZTALK</span></span>
* <span data-ttu-id="053af-115">CORTANA</span><span class="sxs-lookup"><span data-stu-id="053af-115">CORTANA</span></span>
* <span data-ttu-id="053af-116">DIRECTX</span><span class="sxs-lookup"><span data-stu-id="053af-116">DIRECTX</span></span>
* <span data-ttu-id="053af-117">DOTNET</span><span class="sxs-lookup"><span data-stu-id="053af-117">DOTNET</span></span>
* <span data-ttu-id="053af-118">DYNAMICS</span><span class="sxs-lookup"><span data-stu-id="053af-118">DYNAMICS</span></span>
* <span data-ttu-id="053af-119">EXCEL</span><span class="sxs-lookup"><span data-stu-id="053af-119">EXCEL</span></span>
* <span data-ttu-id="053af-120">EXCHANGE</span><span class="sxs-lookup"><span data-stu-id="053af-120">EXCHANGE</span></span>
* <span data-ttu-id="053af-121">FOREFRONT</span><span class="sxs-lookup"><span data-stu-id="053af-121">FOREFRONT</span></span>
* <span data-ttu-id="053af-122">GROOVE</span><span class="sxs-lookup"><span data-stu-id="053af-122">GROOVE</span></span>
* <span data-ttu-id="053af-123">HOLOLENS</span><span class="sxs-lookup"><span data-stu-id="053af-123">HOLOLENS</span></span>
* <span data-ttu-id="053af-124">HYPERV</span><span class="sxs-lookup"><span data-stu-id="053af-124">HYPERV</span></span>
* <span data-ttu-id="053af-125">KINECT</span><span class="sxs-lookup"><span data-stu-id="053af-125">KINECT</span></span>
* <span data-ttu-id="053af-126">LYNC</span><span class="sxs-lookup"><span data-stu-id="053af-126">LYNC</span></span>
* <span data-ttu-id="053af-127">MSDN</span><span class="sxs-lookup"><span data-stu-id="053af-127">MSDN</span></span>
* <span data-ttu-id="053af-128">O365</span><span class="sxs-lookup"><span data-stu-id="053af-128">O365</span></span>
* <span data-ttu-id="053af-129">OFFICE</span><span class="sxs-lookup"><span data-stu-id="053af-129">OFFICE</span></span>
* <span data-ttu-id="053af-130">OFFICE365</span><span class="sxs-lookup"><span data-stu-id="053af-130">OFFICE365</span></span>
* <span data-ttu-id="053af-131">ONEDRIVE</span><span class="sxs-lookup"><span data-stu-id="053af-131">ONEDRIVE</span></span>
* <span data-ttu-id="053af-132">ONENOTE</span><span class="sxs-lookup"><span data-stu-id="053af-132">ONENOTE</span></span>
* <span data-ttu-id="053af-133">OUTLOOK</span><span class="sxs-lookup"><span data-stu-id="053af-133">OUTLOOK</span></span>
* <span data-ttu-id="053af-134">POWERPOINT</span><span class="sxs-lookup"><span data-stu-id="053af-134">POWERPOINT</span></span>
* <span data-ttu-id="053af-135">SHAREPOINT</span><span class="sxs-lookup"><span data-stu-id="053af-135">SHAREPOINT</span></span>
* <span data-ttu-id="053af-136">SKYPE</span><span class="sxs-lookup"><span data-stu-id="053af-136">SKYPE</span></span>
* <span data-ttu-id="053af-137">VISIO</span><span class="sxs-lookup"><span data-stu-id="053af-137">VISIO</span></span>
* <span data-ttu-id="053af-138">VISUALSTUDIO</span><span class="sxs-lookup"><span data-stu-id="053af-138">VISUALSTUDIO</span></span>

<span data-ttu-id="053af-139">The following words cannot be used as either a whole word or a substring in the name:</span><span class="sxs-lookup"><span data-stu-id="053af-139">The following words cannot be used as either a whole word or a substring in the name:</span></span>

* <span data-ttu-id="053af-140">LOGIN</span><span class="sxs-lookup"><span data-stu-id="053af-140">LOGIN</span></span>
* <span data-ttu-id="053af-141">MICROSOFT</span><span class="sxs-lookup"><span data-stu-id="053af-141">MICROSOFT</span></span>
* <span data-ttu-id="053af-142">WINDOWS</span><span class="sxs-lookup"><span data-stu-id="053af-142">WINDOWS</span></span>
* <span data-ttu-id="053af-143">XBOX</span><span class="sxs-lookup"><span data-stu-id="053af-143">XBOX</span></span>

## <a name="solution"></a><span data-ttu-id="053af-144">Solution</span><span class="sxs-lookup"><span data-stu-id="053af-144">Solution</span></span>

<span data-ttu-id="053af-145">Provide a name that does not use one of the reserved words.</span><span class="sxs-lookup"><span data-stu-id="053af-145">Provide a name that does not use one of the reserved words.</span></span>