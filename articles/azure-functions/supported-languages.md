---
title: Supported languages in Azure Functions
description: Learn which languages are supported (GA) and which are experimental or in preview.
services: functions
documentationcenter: na
author: ggailey777
manager: jeconnoc
ms.service: azure-functions
ms.devlang: dotnet
ms.topic: reference
ms.date: 08/02/2018
ms.author: glenga
ms.openlocfilehash: b735f93b2d7ad093ef752fd5f26be729a1157b37
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868960"
---
# <a name="supported-languages-in-azure-functions"></a><span data-ttu-id="f6142-103">Supported languages in Azure Functions</span><span class="sxs-lookup"><span data-stu-id="f6142-103">Supported languages in Azure Functions</span></span>

<span data-ttu-id="f6142-104">This article explains the levels of support offered for languages that you can use with Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="f6142-104">This article explains the levels of support offered for languages that you can use with Azure Functions.</span></span>

## <a name="levels-of-support"></a><span data-ttu-id="f6142-105">Levels of support</span><span class="sxs-lookup"><span data-stu-id="f6142-105">Levels of support</span></span>

<span data-ttu-id="f6142-106">There are three levels of support:</span><span class="sxs-lookup"><span data-stu-id="f6142-106">There are three levels of support:</span></span>

* <span data-ttu-id="f6142-107">**Generally available (GA)** - Fully supported and approved for production use.</span><span class="sxs-lookup"><span data-stu-id="f6142-107">**Generally available (GA)** - Fully supported and approved for production use.</span></span>
* <span data-ttu-id="f6142-108">**Preview** - Not yet supported but is expected to reach GA status in the future.</span><span class="sxs-lookup"><span data-stu-id="f6142-108">**Preview** - Not yet supported but is expected to reach GA status in the future.</span></span>
* <span data-ttu-id="f6142-109">**Experimental** - Not supported and might be abandoned in the future; no guarantee of eventual preview or GA status.</span><span class="sxs-lookup"><span data-stu-id="f6142-109">**Experimental** - Not supported and might be abandoned in the future; no guarantee of eventual preview or GA status.</span></span>

## <a name="languages-in-runtime-1x-and-2x"></a><span data-ttu-id="f6142-110">Languages in runtime 1.x and 2.x</span><span class="sxs-lookup"><span data-stu-id="f6142-110">Languages in runtime 1.x and 2.x</span></span>

<span data-ttu-id="f6142-111">[Two versions of the Azure Functions runtime](functions-versions.md) are available.</span><span class="sxs-lookup"><span data-stu-id="f6142-111">[Two versions of the Azure Functions runtime](functions-versions.md) are available.</span></span> <span data-ttu-id="f6142-112">The 1.x runtime is GA.</span><span class="sxs-lookup"><span data-stu-id="f6142-112">The 1.x runtime is GA.</span></span> <span data-ttu-id="f6142-113">It's the only runtime that is approved for production applications.</span><span class="sxs-lookup"><span data-stu-id="f6142-113">It's the only runtime that is approved for production applications.</span></span> <span data-ttu-id="f6142-114">The 2.x runtime is currently in preview, so the languages it supports are in preview.</span><span class="sxs-lookup"><span data-stu-id="f6142-114">The 2.x runtime is currently in preview, so the languages it supports are in preview.</span></span> <span data-ttu-id="f6142-115">The following table shows which languages are supported in each runtime version.</span><span class="sxs-lookup"><span data-stu-id="f6142-115">The following table shows which languages are supported in each runtime version.</span></span>

[!INCLUDE [functions-supported-languages](../../includes/functions-supported-languages.md)]

### <a name="experimental-languages"></a><span data-ttu-id="f6142-116">Experimental languages</span><span class="sxs-lookup"><span data-stu-id="f6142-116">Experimental languages</span></span>

<span data-ttu-id="f6142-117">The experimental languages in version 1.x don't scale well and don't support all bindings.</span><span class="sxs-lookup"><span data-stu-id="f6142-117">The experimental languages in version 1.x don't scale well and don't support all bindings.</span></span> <span data-ttu-id="f6142-118">For example, Python is slow because the Functions runtime runs *python.exe* with each function invocation.</span><span class="sxs-lookup"><span data-stu-id="f6142-118">For example, Python is slow because the Functions runtime runs *python.exe* with each function invocation.</span></span> <span data-ttu-id="f6142-119">And while Python supports HTTP bindings, it can't access the request object.</span><span class="sxs-lookup"><span data-stu-id="f6142-119">And while Python supports HTTP bindings, it can't access the request object.</span></span>

<span data-ttu-id="f6142-120">Experimental support for PowerShell is limited to version 5.1, because that is what's installed by default on the VMs on which function apps run.</span><span class="sxs-lookup"><span data-stu-id="f6142-120">Experimental support for PowerShell is limited to version 5.1, because that is what's installed by default on the VMs on which function apps run.</span></span> <span data-ttu-id="f6142-121">If you want to run PowerShell scripts, consider [Azure Automation](https://azure.microsoft.com/services/automation/).</span><span class="sxs-lookup"><span data-stu-id="f6142-121">If you want to run PowerShell scripts, consider [Azure Automation](https://azure.microsoft.com/services/automation/).</span></span>

<span data-ttu-id="f6142-122">If you want to use one of the languages that are only available in 1.x, stay on the 1.x runtime.</span><span class="sxs-lookup"><span data-stu-id="f6142-122">If you want to use one of the languages that are only available in 1.x, stay on the 1.x runtime.</span></span> <span data-ttu-id="f6142-123">But don't use experimental languages for anything that you rely on, as there is no official support for them.</span><span class="sxs-lookup"><span data-stu-id="f6142-123">But don't use experimental languages for anything that you rely on, as there is no official support for them.</span></span> <span data-ttu-id="f6142-124">You can request help by [creating GitHub issues](https://github.com/Azure/azure-webjobs-sdk-script/issues), but support cases should not be opened for problems with experimental languages.</span><span class="sxs-lookup"><span data-stu-id="f6142-124">You can request help by [creating GitHub issues](https://github.com/Azure/azure-webjobs-sdk-script/issues), but support cases should not be opened for problems with experimental languages.</span></span> 

<span data-ttu-id="f6142-125">The version 2.x runtime doesn't support experimental languages.</span><span class="sxs-lookup"><span data-stu-id="f6142-125">The version 2.x runtime doesn't support experimental languages.</span></span> <span data-ttu-id="f6142-126">Support for new languages is added only when the language can be supported in production.</span><span class="sxs-lookup"><span data-stu-id="f6142-126">Support for new languages is added only when the language can be supported in production.</span></span> 

### <a name="language-extensibility"></a><span data-ttu-id="f6142-127">Language extensibility</span><span class="sxs-lookup"><span data-stu-id="f6142-127">Language extensibility</span></span>

<span data-ttu-id="f6142-128">The 2.x runtime is designed to offer [language extensibility](https://github.com/Azure/azure-webjobs-sdk-script/wiki/Language-Extensibility).</span><span class="sxs-lookup"><span data-stu-id="f6142-128">The 2.x runtime is designed to offer [language extensibility](https://github.com/Azure/azure-webjobs-sdk-script/wiki/Language-Extensibility).</span></span> <span data-ttu-id="f6142-129">Among the first languages to be based on this extensibility model is Java, which is in preview in 2.x.</span><span class="sxs-lookup"><span data-stu-id="f6142-129">Among the first languages to be based on this extensibility model is Java, which is in preview in 2.x.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6142-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="f6142-130">Next steps</span></span>

<span data-ttu-id="f6142-131">To learn more about how to use one of the GA or preview languages in Azure Functions, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="f6142-131">To learn more about how to use one of the GA or preview languages in Azure Functions, see the following resources:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f6142-132">C#</span><span class="sxs-lookup"><span data-stu-id="f6142-132">C#</span></span>](functions-reference-csharp.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="f6142-133">F#</span><span class="sxs-lookup"><span data-stu-id="f6142-133">F#</span></span>](functions-reference-fsharp.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="f6142-134">JavaScript</span><span class="sxs-lookup"><span data-stu-id="f6142-134">JavaScript</span></span>](functions-reference-node.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="f6142-135">Java</span><span class="sxs-lookup"><span data-stu-id="f6142-135">Java</span></span>](functions-reference-java.md)
