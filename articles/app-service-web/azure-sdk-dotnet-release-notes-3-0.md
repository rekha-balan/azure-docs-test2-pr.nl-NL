---
title: Azure SDK for .NET 3.0 Release Notes | Microsoft Docs
description: Azure SDK for .NET 3.0 Release Notes
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: ''
ms.assetid: c83d815b-fc19-4260-821e-7d2a7206dffc
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 03/07/2017
ms.author: juliako;mikhegn
ms.openlocfilehash: dea4a174aaf3727d66e9d69d32d433ff24e0d06d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553726"
---
# <a name="azure-sdk-for-net-30-release-notes"></a><span data-ttu-id="009f0-103">Azure SDK for .NET 3.0 release notes</span><span class="sxs-lookup"><span data-stu-id="009f0-103">Azure SDK for .NET 3.0 release notes</span></span>

<span data-ttu-id="009f0-104">This topic includes release notes for version 3.0 of the Azure SDK for .NET.</span><span class="sxs-lookup"><span data-stu-id="009f0-104">This topic includes release notes for version 3.0 of the Azure SDK for .NET.</span></span>

##<a name="azure-sdk-for-net-30-release-summary"></a><span data-ttu-id="009f0-105">Azure SDK for .NET 3.0 release summary</span><span class="sxs-lookup"><span data-stu-id="009f0-105">Azure SDK for .NET 3.0 release summary</span></span>

<span data-ttu-id="009f0-106">Release date: 03/07/2017</span><span class="sxs-lookup"><span data-stu-id="009f0-106">Release date: 03/07/2017</span></span>
 
<span data-ttu-id="009f0-107">No breaking changes to the Azure SDK 3.0 have been introduced in this release.</span><span class="sxs-lookup"><span data-stu-id="009f0-107">No breaking changes to the Azure SDK 3.0 have been introduced in this release.</span></span> <span data-ttu-id="009f0-108">There is also no upgrade process needed to leverage this SDK with existing Cloud Service projects.</span><span class="sxs-lookup"><span data-stu-id="009f0-108">There is also no upgrade process needed to leverage this SDK with existing Cloud Service projects.</span></span> <span data-ttu-id="009f0-109">To allow use of the Azure SDK 3.0 without requiring an upgrade process, Azure SDK 3.0 installs to the same directories as Azure SDK 2.9.</span><span class="sxs-lookup"><span data-stu-id="009f0-109">To allow use of the Azure SDK 3.0 without requiring an upgrade process, Azure SDK 3.0 installs to the same directories as Azure SDK 2.9.</span></span> <span data-ttu-id="009f0-110">Most the components did not change the major version from 2.9 but instead just updated the build number.</span><span class="sxs-lookup"><span data-stu-id="009f0-110">Most the components did not change the major version from 2.9 but instead just updated the build number.</span></span>

## <a name="visual-studio-2017-rtw"></a><span data-ttu-id="009f0-111">Visual Studio 2017 RTW</span><span class="sxs-lookup"><span data-stu-id="009f0-111">Visual Studio 2017 RTW</span></span>

- <span data-ttu-id="009f0-112">In Visual Studio 2017, this release of the Azure SDK for .NET is built in to the Azure Workload.</span><span class="sxs-lookup"><span data-stu-id="009f0-112">In Visual Studio 2017, this release of the Azure SDK for .NET is built in to the Azure Workload.</span></span> <span data-ttu-id="009f0-113">All the tools you need to do Azure development will be part of Visual Studio 2017 going forward.</span><span class="sxs-lookup"><span data-stu-id="009f0-113">All the tools you need to do Azure development will be part of Visual Studio 2017 going forward.</span></span> <span data-ttu-id="009f0-114">For Visual Studio 2015 the SDK will still be available through WebPI.</span><span class="sxs-lookup"><span data-stu-id="009f0-114">For Visual Studio 2015 the SDK will still be available through WebPI.</span></span> <span data-ttu-id="009f0-115">We have discontinued Azure SDK for .NET releases for Visual Studio 2013 now that Visual Studio 2017 has been released.</span><span class="sxs-lookup"><span data-stu-id="009f0-115">We have discontinued Azure SDK for .NET releases for Visual Studio 2013 now that Visual Studio 2017 has been released.</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="009f0-116">Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="009f0-116">Azure Diagnostics</span></span>

- <span data-ttu-id="009f0-117">Changed the behavior to only store a partial connection string with the key replaced by a token for Cloud Services diagnostics storage connection string.</span><span class="sxs-lookup"><span data-stu-id="009f0-117">Changed the behavior to only store a partial connection string with the key replaced by a token for Cloud Services diagnostics storage connection string.</span></span> <span data-ttu-id="009f0-118">The actual storage key is now stored in the user profile folder so its access can be controlled.</span><span class="sxs-lookup"><span data-stu-id="009f0-118">The actual storage key is now stored in the user profile folder so its access can be controlled.</span></span> <span data-ttu-id="009f0-119">Visual Studio will read the storage key from user profile folder for local debugging and publishing process.</span><span class="sxs-lookup"><span data-stu-id="009f0-119">Visual Studio will read the storage key from user profile folder for local debugging and publishing process.</span></span> 
- <span data-ttu-id="009f0-120">In response to the change described above, Visual Studio Online team enhanced the Azure Cloud Services deployment task template so users could specify the storage key for setting diagnostics extension when publishing to Azure in Continuous Integration and Deployment.</span><span class="sxs-lookup"><span data-stu-id="009f0-120">In response to the change described above, Visual Studio Online team enhanced the Azure Cloud Services deployment task template so users could specify the storage key for setting diagnostics extension when publishing to Azure in Continuous Integration and Deployment.</span></span>
- <span data-ttu-id="009f0-121">We’ve made it possible to store secure connection string and tokenization for Azure Diagnostics (WAD), to help you solve problems with configuration across environements.</span><span class="sxs-lookup"><span data-stu-id="009f0-121">We’ve made it possible to store secure connection string and tokenization for Azure Diagnostics (WAD), to help you solve problems with configuration across environements.</span></span>
 
### <a name="windows-server-2016-virtual-machines"></a><span data-ttu-id="009f0-122">Windows Server 2016 virtual machines</span><span class="sxs-lookup"><span data-stu-id="009f0-122">Windows Server 2016 virtual machines</span></span>

- <span data-ttu-id="009f0-123">Visual Studio now supports deploying Cloud Services to OS Family 5 (Windows Server 2016) virtual machines.</span><span class="sxs-lookup"><span data-stu-id="009f0-123">Visual Studio now supports deploying Cloud Services to OS Family 5 (Windows Server 2016) virtual machines.</span></span> <span data-ttu-id="009f0-124">For existing cloud services, you can change your settings to target the new OS Family.</span><span class="sxs-lookup"><span data-stu-id="009f0-124">For existing cloud services, you can change your settings to target the new OS Family.</span></span> <span data-ttu-id="009f0-125">When creating new cloud services, if you choose to create the service using .net 4.6 or higher, it will default the service to use OS Family 5.</span><span class="sxs-lookup"><span data-stu-id="009f0-125">When creating new cloud services, if you choose to create the service using .net 4.6 or higher, it will default the service to use OS Family 5.</span></span>  <span data-ttu-id="009f0-126">For more information, you can review the [Guest OS Family support table](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="009f0-126">For more information, you can review the [Guest OS Family support table](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span>

### <a name="known-issues"></a><span data-ttu-id="009f0-127">Known issues</span><span class="sxs-lookup"><span data-stu-id="009f0-127">Known issues</span></span>

- <span data-ttu-id="009f0-128">Azure .NET SDK 3.0 introduced an issue when removing Visual Studio 2017 in a side by side configuration with Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="009f0-128">Azure .NET SDK 3.0 introduced an issue when removing Visual Studio 2017 in a side by side configuration with Visual Studio 2015.</span></span>  <span data-ttu-id="009f0-129">If you have the Azure SDK installed for Visual Studio 2015, the Microsoft Azure Storage Emulator and Microsoft Azure Compute Emulator will be removed if you uninstall Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="009f0-129">If you have the Azure SDK installed for Visual Studio 2015, the Microsoft Azure Storage Emulator and Microsoft Azure Compute Emulator will be removed if you uninstall Visual Studio 2017.</span></span>  <span data-ttu-id="009f0-130">This will produce an error when creating and debugging new Cloud services projects in Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="009f0-130">This will produce an error when creating and debugging new Cloud services projects in Visual Studio 2015.</span></span> <span data-ttu-id="009f0-131">In order to fix this issue,  reinstall the Azure SDK from the Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="009f0-131">In order to fix this issue,  reinstall the Azure SDK from the Web Platform Installer.</span></span>  <span data-ttu-id="009f0-132">The issue will be resolved in a future Visual Studio 2017 update.</span><span class="sxs-lookup"><span data-stu-id="009f0-132">The issue will be resolved in a future Visual Studio 2017 update.</span></span>  <span data-ttu-id="009f0-133">.</span><span class="sxs-lookup"><span data-stu-id="009f0-133">.</span></span>

 
### <a name="azure-in-role-cache"></a><span data-ttu-id="009f0-134">Azure In-Role Cache</span><span class="sxs-lookup"><span data-stu-id="009f0-134">Azure In-Role Cache</span></span> 

- <span data-ttu-id="009f0-135">Support for Azure In-Role Cache ended on November 30, 2016.</span><span class="sxs-lookup"><span data-stu-id="009f0-135">Support for Azure In-Role Cache ended on November 30, 2016.</span></span> <span data-ttu-id="009f0-136">For more details, click [here](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span><span class="sxs-lookup"><span data-stu-id="009f0-136">For more details, click [here](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span></span>




