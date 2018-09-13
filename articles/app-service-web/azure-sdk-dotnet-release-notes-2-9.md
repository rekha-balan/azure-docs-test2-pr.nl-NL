---
title: Azure SDK for .NET 2.9 Release Notes
description: Azure SDK for .NET 2.9 Release Notes
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
ms.date: 02/24/2017
ms.author: juliako;mikhegn
ms.openlocfilehash: 3c3fb275a7c980f71a3a30e6875b9515321bad99
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661894"
---
# <a name="azure-sdk-for-net-29-release-notes"></a><span data-ttu-id="c04b6-103">Azure SDK for .NET 2.9 release notes</span><span class="sxs-lookup"><span data-stu-id="c04b6-103">Azure SDK for .NET 2.9 release notes</span></span>

<span data-ttu-id="c04b6-104">This topic includes release notes for versions 2.9 and 2.9.6 of Azure SDK for .NET.</span><span class="sxs-lookup"><span data-stu-id="c04b6-104">This topic includes release notes for versions 2.9 and 2.9.6 of Azure SDK for .NET.</span></span>

##<a name="azure-sdk-for-net-296-release-summary"></a><span data-ttu-id="c04b6-105">Azure SDK for .NET 2.9.6 release summary</span><span class="sxs-lookup"><span data-stu-id="c04b6-105">Azure SDK for .NET 2.9.6 release summary</span></span>

<span data-ttu-id="c04b6-106">Release date: 11/16/2016</span><span class="sxs-lookup"><span data-stu-id="c04b6-106">Release date: 11/16/2016</span></span>
 
<span data-ttu-id="c04b6-107">No breaking changes to the Azure SDK 2.9 have been introduced in this release.</span><span class="sxs-lookup"><span data-stu-id="c04b6-107">No breaking changes to the Azure SDK 2.9 have been introduced in this release.</span></span> <span data-ttu-id="c04b6-108">There is also no upgrade process needed to leverage this SDK with existing Cloud Service projects.</span><span class="sxs-lookup"><span data-stu-id="c04b6-108">There is also no upgrade process needed to leverage this SDK with existing Cloud Service projects.</span></span>

### <a name="visual-studio-2017-release-candidate"></a><span data-ttu-id="c04b6-109">Visual Studio 2017 Release Candidate</span><span class="sxs-lookup"><span data-stu-id="c04b6-109">Visual Studio 2017 Release Candidate</span></span>

- <span data-ttu-id="c04b6-110">In Visual Studio 2017 RC, this release of the Azure SDK for .NET is built in in the Azure Workload.</span><span class="sxs-lookup"><span data-stu-id="c04b6-110">In Visual Studio 2017 RC, this release of the Azure SDK for .NET is built in in the Azure Workload.</span></span> <span data-ttu-id="c04b6-111">All the tools you need to do Azure development will be part of Visual Studio 2017 RC going forward.</span><span class="sxs-lookup"><span data-stu-id="c04b6-111">All the tools you need to do Azure development will be part of Visual Studio 2017 RC going forward.</span></span> <span data-ttu-id="c04b6-112">For Visual Studio 2015 and Visual Studio 2013, the SDK will still be available through WebPI.</span><span class="sxs-lookup"><span data-stu-id="c04b6-112">For Visual Studio 2015 and Visual Studio 2013, the SDK will still be available through WebPI.</span></span> <span data-ttu-id="c04b6-113">We will be discontinuing Azure SDK for .NET releases for Visual Studio 2013, when Visual Studio 2017 releases as a final product.</span><span class="sxs-lookup"><span data-stu-id="c04b6-113">We will be discontinuing Azure SDK for .NET releases for Visual Studio 2013, when Visual Studio 2017 releases as a final product.</span></span> <span data-ttu-id="c04b6-114">Follow this link to download Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span><span class="sxs-lookup"><span data-stu-id="c04b6-114">Follow this link to download Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="c04b6-115">Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="c04b6-115">Azure Diagnostics</span></span>

- <span data-ttu-id="c04b6-116">Changed the behavior to only store a partial connection string with the key replaced by a token for Cloud Services diagnostics storage connection string.</span><span class="sxs-lookup"><span data-stu-id="c04b6-116">Changed the behavior to only store a partial connection string with the key replaced by a token for Cloud Services diagnostics storage connection string.</span></span> <span data-ttu-id="c04b6-117">The actual storage key is now stored in the user profile folder so its access can be controlled.</span><span class="sxs-lookup"><span data-stu-id="c04b6-117">The actual storage key is now stored in the user profile folder so its access can be controlled.</span></span> <span data-ttu-id="c04b6-118">Visual Studio will read the storage key from user profile folder for local debugging and publishing process.</span><span class="sxs-lookup"><span data-stu-id="c04b6-118">Visual Studio will read the storage key from user profile folder for local debugging and publishing process.</span></span> 
- <span data-ttu-id="c04b6-119">In response to the change described above, Visual Studio Online team enhanced the Azure Cloud Services deployment task template so users could specify the storage key for setting diagnostics extension when publishing to Azure in Continuous Integration and Deployment.</span><span class="sxs-lookup"><span data-stu-id="c04b6-119">In response to the change described above, Visual Studio Online team enhanced the Azure Cloud Services deployment task template so users could specify the storage key for setting diagnostics extension when publishing to Azure in Continuous Integration and Deployment.</span></span>
- <span data-ttu-id="c04b6-120">We’ve made it possible to store secure connection string and tokenization for Azure Diagnostics (WAD), to help you solve problems with configuration across environements.</span><span class="sxs-lookup"><span data-stu-id="c04b6-120">We’ve made it possible to store secure connection string and tokenization for Azure Diagnostics (WAD), to help you solve problems with configuration across environements.</span></span>
 
### <a name="windows-server-2016-virtual-machines"></a><span data-ttu-id="c04b6-121">Windows Server 2016 virtual machines</span><span class="sxs-lookup"><span data-stu-id="c04b6-121">Windows Server 2016 virtual machines</span></span>

- <span data-ttu-id="c04b6-122">Visual Studio now supports deploying Cloud Services to OS Family 5 (Windows Server 2016) virtual machines.</span><span class="sxs-lookup"><span data-stu-id="c04b6-122">Visual Studio now supports deploying Cloud Services to OS Family 5 (Windows Server 2016) virtual machines.</span></span> <span data-ttu-id="c04b6-123">For existing cloud services, you can change your settings to target the new OS Family.</span><span class="sxs-lookup"><span data-stu-id="c04b6-123">For existing cloud services, you can change your settings to target the new OS Family.</span></span> <span data-ttu-id="c04b6-124">When creating new cloud services, if you choose to create the service using .net 4.6 or higher, it will default the service to use OS Family 5.</span><span class="sxs-lookup"><span data-stu-id="c04b6-124">When creating new cloud services, if you choose to create the service using .net 4.6 or higher, it will default the service to use OS Family 5.</span></span>  <span data-ttu-id="c04b6-125">For more information, you can review the [Guest OS Family support table](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span><span class="sxs-lookup"><span data-stu-id="c04b6-125">For more information, you can review the [Guest OS Family support table](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span></span>

#### <a name="known-issues"></a><span data-ttu-id="c04b6-126">Known issues</span><span class="sxs-lookup"><span data-stu-id="c04b6-126">Known issues</span></span>

- <span data-ttu-id="c04b6-127">Azure .NET SDK 2.9.6 introduced a restriction that blocks deployment of projects using unsupported .NET frameworks (such as .NET 4.6) to any OS Family < 5.</span><span class="sxs-lookup"><span data-stu-id="c04b6-127">Azure .NET SDK 2.9.6 introduced a restriction that blocks deployment of projects using unsupported .NET frameworks (such as .NET 4.6) to any OS Family < 5.</span></span> <span data-ttu-id="c04b6-128">A workaround is provided [here](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span><span class="sxs-lookup"><span data-stu-id="c04b6-128">A workaround is provided [here](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span></span>

 
### <a name="azure-in-role-cache"></a><span data-ttu-id="c04b6-129">Azure In-Role Cache</span><span class="sxs-lookup"><span data-stu-id="c04b6-129">Azure In-Role Cache</span></span> 

- <span data-ttu-id="c04b6-130">Support for Azure In-Role Cache ends on November 30, 2016.</span><span class="sxs-lookup"><span data-stu-id="c04b6-130">Support for Azure In-Role Cache ends on November 30, 2016.</span></span> <span data-ttu-id="c04b6-131">For more details, click [here](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span><span class="sxs-lookup"><span data-stu-id="c04b6-131">For more details, click [here](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span></span>

### <a name="azure-resource-manager-templates-for-azure-stack"></a><span data-ttu-id="c04b6-132">Azure Resource Manager Templates for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="c04b6-132">Azure Resource Manager Templates for Azure Stack</span></span>

- <span data-ttu-id="c04b6-133">We’ve introduced Azure Stack as a deployment target for your Azure Resource Manager Templates.</span><span class="sxs-lookup"><span data-stu-id="c04b6-133">We’ve introduced Azure Stack as a deployment target for your Azure Resource Manager Templates.</span></span>


## <a name="azure-sdk-for-net-29-summary"></a><span data-ttu-id="c04b6-134">Azure SDK for .NET 2.9 summary</span><span class="sxs-lookup"><span data-stu-id="c04b6-134">Azure SDK for .NET 2.9 summary</span></span>

## <a name="overview"></a><span data-ttu-id="c04b6-135">Overview</span><span class="sxs-lookup"><span data-stu-id="c04b6-135">Overview</span></span>
<span data-ttu-id="c04b6-136">This document contains the release notes for the Azure SDK for .NET 2.9 release.</span><span class="sxs-lookup"><span data-stu-id="c04b6-136">This document contains the release notes for the Azure SDK for .NET 2.9 release.</span></span> 

<span data-ttu-id="c04b6-137">For detailed information about updates in this release, see the [Azure SDK 2.9 announcement post](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span><span class="sxs-lookup"><span data-stu-id="c04b6-137">For detailed information about updates in this release, see the [Azure SDK 2.9 announcement post](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span></span>

## <a name="azure-sdk-29-for-visual-studio-2015-update-2-and-visual-studio-15-preview"></a><span data-ttu-id="c04b6-138">Azure SDK 2.9 for Visual Studio 2015 Update 2 and Visual Studio "15" Preview</span><span class="sxs-lookup"><span data-stu-id="c04b6-138">Azure SDK 2.9 for Visual Studio 2015 Update 2 and Visual Studio "15" Preview</span></span>
<span data-ttu-id="c04b6-139">This update includes the following bug fixes:</span><span class="sxs-lookup"><span data-stu-id="c04b6-139">This update includes the following bug fixes:</span></span>

* <span data-ttu-id="c04b6-140">Issue related to REST API Client Generation in in which the string "Unknown Type” would appear as the name of the code-gen folder and/or the name of the namespace dropped into the generated code.</span><span class="sxs-lookup"><span data-stu-id="c04b6-140">Issue related to REST API Client Generation in in which the string "Unknown Type” would appear as the name of the code-gen folder and/or the name of the namespace dropped into the generated code.</span></span>
* <span data-ttu-id="c04b6-141">Issue related to Scheduled WebJobs in which the authentication information was failing to be passed to the Scheduler provisioning process.</span><span class="sxs-lookup"><span data-stu-id="c04b6-141">Issue related to Scheduled WebJobs in which the authentication information was failing to be passed to the Scheduler provisioning process.</span></span>

<span data-ttu-id="c04b6-142">This update includes the following new feature:</span><span class="sxs-lookup"><span data-stu-id="c04b6-142">This update includes the following new feature:</span></span>

* <span data-ttu-id="c04b6-143">Support for secondary App Services in the "Services" tab of the App Service provisioning dialog.</span><span class="sxs-lookup"><span data-stu-id="c04b6-143">Support for secondary App Services in the "Services" tab of the App Service provisioning dialog.</span></span> 

## <a name="azure-data-lake-tools-for-visual-studio-2015-update-2"></a><span data-ttu-id="c04b6-144">Azure Data Lake Tools for Visual Studio 2015 Update 2</span><span class="sxs-lookup"><span data-stu-id="c04b6-144">Azure Data Lake Tools for Visual Studio 2015 Update 2</span></span>
<span data-ttu-id="c04b6-145">This updates includes the following:</span><span class="sxs-lookup"><span data-stu-id="c04b6-145">This updates includes the following:</span></span>

* <span data-ttu-id="c04b6-146">**Azure Data Lake Tools** for Visual Studio is now merged into the Azure SDK for .NET release.</span><span class="sxs-lookup"><span data-stu-id="c04b6-146">**Azure Data Lake Tools** for Visual Studio is now merged into the Azure SDK for .NET release.</span></span> <span data-ttu-id="c04b6-147">The tool is automatically installed when you install Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="c04b6-147">The tool is automatically installed when you install Azure SDK.</span></span> 
  
    <span data-ttu-id="c04b6-148">The tool is updated frequently, go [here](http://aka.ms/datalaketool) to get the updates.</span><span class="sxs-lookup"><span data-stu-id="c04b6-148">The tool is updated frequently, go [here](http://aka.ms/datalaketool) to get the updates.</span></span>
* <span data-ttu-id="c04b6-149">**Server Explorer** now enables you to view all and create some U-SQL metadata entities.</span><span class="sxs-lookup"><span data-stu-id="c04b6-149">**Server Explorer** now enables you to view all and create some U-SQL metadata entities.</span></span> <span data-ttu-id="c04b6-150">For more information, see [this](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blog.</span><span class="sxs-lookup"><span data-stu-id="c04b6-150">For more information, see [this](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blog.</span></span>

## <a name="hdinsight-tools"></a><span data-ttu-id="c04b6-151">HDInsight Tools</span><span class="sxs-lookup"><span data-stu-id="c04b6-151">HDInsight Tools</span></span>
<span data-ttu-id="c04b6-152">**HDInsight Tools** for Visual Studio now supports HDInsight version 3.3, including showing Tez graphs and other language fixes.</span><span class="sxs-lookup"><span data-stu-id="c04b6-152">**HDInsight Tools** for Visual Studio now supports HDInsight version 3.3, including showing Tez graphs and other language fixes.</span></span>

## <a name="azure-resource-manager"></a><span data-ttu-id="c04b6-153">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c04b6-153">Azure Resource Manager</span></span>
<span data-ttu-id="c04b6-154">This release adds [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) support for Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="c04b6-154">This release adds [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) support for Resource Manager templates.</span></span>

## <a name="see-also"></a><span data-ttu-id="c04b6-155">See also</span><span class="sxs-lookup"><span data-stu-id="c04b6-155">See also</span></span>
[<span data-ttu-id="c04b6-156">Azure SDK 2.9 announcement post</span><span class="sxs-lookup"><span data-stu-id="c04b6-156">Azure SDK 2.9 announcement post</span></span>](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)

