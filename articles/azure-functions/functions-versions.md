---
title: Azure Functions runtime versions overview
description: Azure Functions supports multiple versions of the runtime. Learn the differences between them and how to choose the one that's right for you.
services: functions
documentationcenter: ''
author: ggailey777
manager: jeconnoc
ms.service: azure-functions
ms.topic: conceptual
ms.date: 07/29/2018
ms.author: glenga
ms.openlocfilehash: 716f2b537a47c6e721c7393cba340a583c7ed064
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867754"
---
# <a name="azure-functions-runtime-versions-overview"></a><span data-ttu-id="c855f-104">Azure Functions runtime versions overview</span><span class="sxs-lookup"><span data-stu-id="c855f-104">Azure Functions runtime versions overview</span></span>

 <span data-ttu-id="c855f-105">There are two major versions of the Azure Functions runtime: 1.x and 2.x.</span><span class="sxs-lookup"><span data-stu-id="c855f-105">There are two major versions of the Azure Functions runtime: 1.x and 2.x.</span></span> <span data-ttu-id="c855f-106">Only 1.x is approved for production use.</span><span class="sxs-lookup"><span data-stu-id="c855f-106">Only 1.x is approved for production use.</span></span> <span data-ttu-id="c855f-107">This article explains what's new in 2.x, which is in preview.</span><span class="sxs-lookup"><span data-stu-id="c855f-107">This article explains what's new in 2.x, which is in preview.</span></span>

| <span data-ttu-id="c855f-108">Runtime</span><span class="sxs-lookup"><span data-stu-id="c855f-108">Runtime</span></span> | <span data-ttu-id="c855f-109">Status</span><span class="sxs-lookup"><span data-stu-id="c855f-109">Status</span></span> |
|---------|---------|
|<span data-ttu-id="c855f-110">1.x</span><span class="sxs-lookup"><span data-stu-id="c855f-110">1.x</span></span>|<span data-ttu-id="c855f-111">Generally Available (GA)</span><span class="sxs-lookup"><span data-stu-id="c855f-111">Generally Available (GA)</span></span>|
|<span data-ttu-id="c855f-112">2.x</span><span class="sxs-lookup"><span data-stu-id="c855f-112">2.x</span></span>|<span data-ttu-id="c855f-113">Preview<sup>\*</sup></span><span class="sxs-lookup"><span data-stu-id="c855f-113">Preview<sup>\*</sup></span></span>|

<span data-ttu-id="c855f-114"><sup>\*</sup>To receive important updates on version 2.x, including breaking changes announcements, watch the [Azure App Service announcements](https://github.com/Azure/app-service-announcements/issues) repository.</span><span class="sxs-lookup"><span data-stu-id="c855f-114"><sup>\*</sup>To receive important updates on version 2.x, including breaking changes announcements, watch the [Azure App Service announcements](https://github.com/Azure/app-service-announcements/issues) repository.</span></span>

> [!NOTE] 
> <span data-ttu-id="c855f-115">This article refers to the cloud service Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="c855f-115">This article refers to the cloud service Azure Functions.</span></span> <span data-ttu-id="c855f-116">For information about the product that lets you run Azure Functions on-premises, see the [Azure Functions Runtime Overview](functions-runtime-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c855f-116">For information about the product that lets you run Azure Functions on-premises, see the [Azure Functions Runtime Overview](functions-runtime-overview.md).</span></span>

## <a name="cross-platform-development"></a><span data-ttu-id="c855f-117">Cross-platform development</span><span class="sxs-lookup"><span data-stu-id="c855f-117">Cross-platform development</span></span>

<span data-ttu-id="c855f-118">Runtime 1.x supports development and hosting only in the portal or on Windows.</span><span class="sxs-lookup"><span data-stu-id="c855f-118">Runtime 1.x supports development and hosting only in the portal or on Windows.</span></span> <span data-ttu-id="c855f-119">Runtime 2.x runs on .NET Core, which means it can run on all platforms supported by .NET Core, including macOS and Linux.</span><span class="sxs-lookup"><span data-stu-id="c855f-119">Runtime 2.x runs on .NET Core, which means it can run on all platforms supported by .NET Core, including macOS and Linux.</span></span> <span data-ttu-id="c855f-120">This enables cross-platform development and hosting scenarios that aren't possible with 1.x.</span><span class="sxs-lookup"><span data-stu-id="c855f-120">This enables cross-platform development and hosting scenarios that aren't possible with 1.x.</span></span>

## <a name="languages"></a><span data-ttu-id="c855f-121">Languages</span><span class="sxs-lookup"><span data-stu-id="c855f-121">Languages</span></span>

<span data-ttu-id="c855f-122">Runtime 2.x uses a new language extensibility model.</span><span class="sxs-lookup"><span data-stu-id="c855f-122">Runtime 2.x uses a new language extensibility model.</span></span> <span data-ttu-id="c855f-123">Initially, JavaScript and Java are taking advantage of this new model.</span><span class="sxs-lookup"><span data-stu-id="c855f-123">Initially, JavaScript and Java are taking advantage of this new model.</span></span> <span data-ttu-id="c855f-124">Azure Functions 1.x experimental languages haven't been updated to use the new model, so they are not supported in 2.x.</span><span class="sxs-lookup"><span data-stu-id="c855f-124">Azure Functions 1.x experimental languages haven't been updated to use the new model, so they are not supported in 2.x.</span></span> <span data-ttu-id="c855f-125">The following table indicates which programming languages are supported in each runtime version.</span><span class="sxs-lookup"><span data-stu-id="c855f-125">The following table indicates which programming languages are supported in each runtime version.</span></span>

[!INCLUDE [functions-supported-languages](../../includes/functions-supported-languages.md)]

<span data-ttu-id="c855f-126">For more information, see [Supported languages](supported-languages.md).</span><span class="sxs-lookup"><span data-stu-id="c855f-126">For more information, see [Supported languages](supported-languages.md).</span></span>

## <a name="bindings"></a><span data-ttu-id="c855f-127">Bindings</span><span class="sxs-lookup"><span data-stu-id="c855f-127">Bindings</span></span> 

<span data-ttu-id="c855f-128">Runtime 2.x uses a new [binding extensibility model](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview) that offers these advantages:</span><span class="sxs-lookup"><span data-stu-id="c855f-128">Runtime 2.x uses a new [binding extensibility model](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview) that offers these advantages:</span></span>

* <span data-ttu-id="c855f-129">Support for third-party binding extensions.</span><span class="sxs-lookup"><span data-stu-id="c855f-129">Support for third-party binding extensions.</span></span>
* <span data-ttu-id="c855f-130">Decoupling of runtime and bindings.</span><span class="sxs-lookup"><span data-stu-id="c855f-130">Decoupling of runtime and bindings.</span></span> <span data-ttu-id="c855f-131">This allows binding extensions to be versioned and released independently.</span><span class="sxs-lookup"><span data-stu-id="c855f-131">This allows binding extensions to be versioned and released independently.</span></span> <span data-ttu-id="c855f-132">You can, for example, opt to upgrade to a version of an extension that relies on a newer version of an underlying SDK.</span><span class="sxs-lookup"><span data-stu-id="c855f-132">You can, for example, opt to upgrade to a version of an extension that relies on a newer version of an underlying SDK.</span></span>
* <span data-ttu-id="c855f-133">A lighter execution environment, where only the bindings in use are known and loaded by the runtime.</span><span class="sxs-lookup"><span data-stu-id="c855f-133">A lighter execution environment, where only the bindings in use are known and loaded by the runtime.</span></span>

<span data-ttu-id="c855f-134">All built-in Azure Functions bindings have adopted this model and are no longer included by default, except for the Timer trigger and the HTTP trigger.</span><span class="sxs-lookup"><span data-stu-id="c855f-134">All built-in Azure Functions bindings have adopted this model and are no longer included by default, except for the Timer trigger and the HTTP trigger.</span></span> <span data-ttu-id="c855f-135">Those extensions are automatically installed when you create functions through tools like Visual Studio or through the portal.</span><span class="sxs-lookup"><span data-stu-id="c855f-135">Those extensions are automatically installed when you create functions through tools like Visual Studio or through the portal.</span></span>

<span data-ttu-id="c855f-136">The following table indicates which bindings are supported in each runtime version.</span><span class="sxs-lookup"><span data-stu-id="c855f-136">The following table indicates which bindings are supported in each runtime version.</span></span>

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

## <a name="known-issues-in-2x"></a><span data-ttu-id="c855f-137">Known issues in 2.x</span><span class="sxs-lookup"><span data-stu-id="c855f-137">Known issues in 2.x</span></span>

<span data-ttu-id="c855f-138">For more information about bindings support and other functional gaps in 2.x, see [Runtime 2.0 known issues](https://github.com/Azure/azure-webjobs-sdk-script/wiki/Azure-Functions-runtime-2.0-known-issues).</span><span class="sxs-lookup"><span data-stu-id="c855f-138">For more information about bindings support and other functional gaps in 2.x, see [Runtime 2.0 known issues](https://github.com/Azure/azure-webjobs-sdk-script/wiki/Azure-Functions-runtime-2.0-known-issues).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c855f-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="c855f-139">Next steps</span></span>

<span data-ttu-id="c855f-140">For more information, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="c855f-140">For more information, see the following resources:</span></span>

* [<span data-ttu-id="c855f-141">Code and test Azure Functions locally</span><span class="sxs-lookup"><span data-stu-id="c855f-141">Code and test Azure Functions locally</span></span>](functions-run-local.md)
* [<span data-ttu-id="c855f-142">How to target Azure Functions runtime versions</span><span class="sxs-lookup"><span data-stu-id="c855f-142">How to target Azure Functions runtime versions</span></span>](set-runtime-version.md)
* [<span data-ttu-id="c855f-143">Release notes</span><span class="sxs-lookup"><span data-stu-id="c855f-143">Release notes</span></span>](https://github.com/Azure/azure-functions-host/releases)
