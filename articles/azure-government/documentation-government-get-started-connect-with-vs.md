---
title: Connect to Azure Government with Visual Studio | Microsoft Docs
description: Information on managing your subscription in Azure Government by connecting with Visual Studio
services: azure-government
cloud: gov
documentationcenter: ''
author: zakramer
manager: liki
ms.assetid: faf269aa-e879-4b0e-a5ba-d4110684616a
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 02/13/2017
ms.author: zakramer
ms.openlocfilehash: ffb3fd6183a1d84fa0fcab1c7a14c64db786a441
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554556"
---
# <a name="connecting-via-visual-studio"></a><span data-ttu-id="233ea-103">Connecting via Visual Studio</span><span class="sxs-lookup"><span data-stu-id="233ea-103">Connecting via Visual Studio</span></span>
<span data-ttu-id="233ea-104">Visual Studio is used by developers to easily manage their Azure subscriptions while building solutions.</span><span class="sxs-lookup"><span data-stu-id="233ea-104">Visual Studio is used by developers to easily manage their Azure subscriptions while building solutions.</span></span>  <span data-ttu-id="233ea-105">Visual Studio does not currently allow you to configure a connection to Azure Government in the user interface.</span><span class="sxs-lookup"><span data-stu-id="233ea-105">Visual Studio does not currently allow you to configure a connection to Azure Government in the user interface.</span></span>  

## <a name="visual-studio-2017"></a><span data-ttu-id="233ea-106">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="233ea-106">Visual Studio 2017</span></span>
<span data-ttu-id="233ea-107">Visual Studio 2017 requires a configuration file for Visual Studio to connect to Azure Government.</span><span class="sxs-lookup"><span data-stu-id="233ea-107">Visual Studio 2017 requires a configuration file for Visual Studio to connect to Azure Government.</span></span>  <span data-ttu-id="233ea-108">With this file inplace Visual Studio connects to Azure Government instead of Azure Public.</span><span class="sxs-lookup"><span data-stu-id="233ea-108">With this file inplace Visual Studio connects to Azure Government instead of Azure Public.</span></span>

### <a name="create-a-configuration-file-for-azure-government"></a><span data-ttu-id="233ea-109">Create a configuration file for Azure Government</span><span class="sxs-lookup"><span data-stu-id="233ea-109">Create a configuration file for Azure Government</span></span>
<span data-ttu-id="233ea-110">Create a file named **AadProvider.Configuration.json** with the following content:</span><span class="sxs-lookup"><span data-stu-id="233ea-110">Create a file named **AadProvider.Configuration.json** with the following content:</span></span>

        {
          "AuthenticationQueryParameters": null,
          "AsmEndPoint": "https://management.core.usgovcloudapi.net/",
          "Authority": "https://login.microsoftonline.us/",
          "AzureResourceManagementEndpoint": "https://management.usgovcloudapi.net",
          "AzureResourceManagementAudienceEndpoints": [ "https://management.core.usgovcloudapi.net" ],
          "ClientIdentifier": "872cd9fa-d31f-45e0-9eab-6e460a02d1f1",
          "EnvironmentName": "AzureUSGovernment",
          "GraphEndpoint": "https://graph.windows.net",
          "MsaHomeTenantId": "f8cdef31-a31e-4b4a-93e4-5f571e91255a",
          "NativeClientRedirect": "urn:ietf:wg:oauth:2.0:oob",
          "PortalEndpoint": "https://portal.azure.us/",
          "ResourceEndpoint": "https://management.core.usgovcloudapi.net",
          "ValidateAuthority": true,
          "VisualStudioOnlineEndpoint": "https://app.vssps.visualstudio.com/",
          "VisualStudioOnlineAudience": "499b84ac-1321-427f-aa17-267ca6975798"
        }

### <a name="updating-visual-studio-for-azure-government"></a><span data-ttu-id="233ea-111">Updating Visual Studio for Azure Government</span><span class="sxs-lookup"><span data-stu-id="233ea-111">Updating Visual Studio for Azure Government</span></span>

1.  <span data-ttu-id="233ea-112">Close Visual Studio</span><span class="sxs-lookup"><span data-stu-id="233ea-112">Close Visual Studio</span></span>
2.  <span data-ttu-id="233ea-113">Place **AadProvider.Configuration.json** created in the previous step into **%localappdata%\\.IdentityService\AadConfigurations**.</span><span class="sxs-lookup"><span data-stu-id="233ea-113">Place **AadProvider.Configuration.json** created in the previous step into **%localappdata%\\.IdentityService\AadConfigurations**.</span></span>  <span data-ttu-id="233ea-114">Create this folder if not present.</span><span class="sxs-lookup"><span data-stu-id="233ea-114">Create this folder if not present.</span></span>
3.  <span data-ttu-id="233ea-115">Launch Visual Studio and begin using your Azure Government account.</span><span class="sxs-lookup"><span data-stu-id="233ea-115">Launch Visual Studio and begin using your Azure Government account.</span></span>

> [!NOTE]
> <span data-ttu-id="233ea-116">With the configuration file, only Azure Government subscriptions are accessible.</span><span class="sxs-lookup"><span data-stu-id="233ea-116">With the configuration file, only Azure Government subscriptions are accessible.</span></span>  <span data-ttu-id="233ea-117">You still see subscriptions that you configured previously but they do not work because Visual Studio is now connected to Azure Government instead of Azure Public.</span><span class="sxs-lookup"><span data-stu-id="233ea-117">You still see subscriptions that you configured previously but they do not work because Visual Studio is now connected to Azure Government instead of Azure Public.</span></span>  <span data-ttu-id="233ea-118">Remove the file to connect to Azure Commercial.</span><span class="sxs-lookup"><span data-stu-id="233ea-118">Remove the file to connect to Azure Commercial.</span></span>
> 
> 

### <a name="reverting-visual-studio-connection-to-azure-government"></a><span data-ttu-id="233ea-119">Reverting Visual Studio Connection to Azure Government</span><span class="sxs-lookup"><span data-stu-id="233ea-119">Reverting Visual Studio Connection to Azure Government</span></span>
<span data-ttu-id="233ea-120">To enable Visual Studio to connect to Azure Public, you need to remove the configuration file settings that enables connection to Azure Government.</span><span class="sxs-lookup"><span data-stu-id="233ea-120">To enable Visual Studio to connect to Azure Public, you need to remove the configuration file settings that enables connection to Azure Government.</span></span>

1.  <span data-ttu-id="233ea-121">Close Visual Studio</span><span class="sxs-lookup"><span data-stu-id="233ea-121">Close Visual Studio</span></span>
2.  <span data-ttu-id="233ea-122">Delete this folder: **%localappdata%\.IdentityService\AadConfigurations**</span><span class="sxs-lookup"><span data-stu-id="233ea-122">Delete this folder: **%localappdata%\.IdentityService\AadConfigurations**</span></span>
3.  <span data-ttu-id="233ea-123">Restart Visual Studio and begin using your Azure Public account.</span><span class="sxs-lookup"><span data-stu-id="233ea-123">Restart Visual Studio and begin using your Azure Public account.</span></span>

> [!NOTE]
> <span data-ttu-id="233ea-124">Once this configuration has been reverted, your Azure Government subscriptions no longer accessible.</span><span class="sxs-lookup"><span data-stu-id="233ea-124">Once this configuration has been reverted, your Azure Government subscriptions no longer accessible.</span></span>
> 
>

## <a name="visual-studio-2015"></a><span data-ttu-id="233ea-125">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="233ea-125">Visual Studio 2015</span></span>
<span data-ttu-id="233ea-126">Visual Studio 2015 requires a registry change for Visual Studio to connect to Azure Government.</span><span class="sxs-lookup"><span data-stu-id="233ea-126">Visual Studio 2015 requires a registry change for Visual Studio to connect to Azure Government.</span></span>  <span data-ttu-id="233ea-127">Once this registry key is set Visual Studio connects to Azure Government instead of Azure Public.</span><span class="sxs-lookup"><span data-stu-id="233ea-127">Once this registry key is set Visual Studio connects to Azure Government instead of Azure Public.</span></span>

### <a name="updating-visual-studio-for-azure-government"></a><span data-ttu-id="233ea-128">Updating Visual Studio for Azure Government</span><span class="sxs-lookup"><span data-stu-id="233ea-128">Updating Visual Studio for Azure Government</span></span>
<span data-ttu-id="233ea-129">To enable Visual Studio to connect to Azure Government, you need to update the registry.</span><span class="sxs-lookup"><span data-stu-id="233ea-129">To enable Visual Studio to connect to Azure Government, you need to update the registry.</span></span>

1. <span data-ttu-id="233ea-130">Close Visual Studio</span><span class="sxs-lookup"><span data-stu-id="233ea-130">Close Visual Studio</span></span>
2. <span data-ttu-id="233ea-131">Create a text file named **VisualStudioForAzureGov.reg**</span><span class="sxs-lookup"><span data-stu-id="233ea-131">Create a text file named **VisualStudioForAzureGov.reg**</span></span>
3. <span data-ttu-id="233ea-132">Copy and paste the following text into **VisualStudioForAzureGov.reg**:</span><span class="sxs-lookup"><span data-stu-id="233ea-132">Copy and paste the following text into **VisualStudioForAzureGov.reg**:</span></span>
   
        Windows Registry Editor Version 5.00
   
        [HKEY_CURRENT_USER\Software\Microsoft\VSCommon\ConnectedUser]
        "AadInstance"="https://login.microsoftonline.us/"
        "adaluri"="https://management.core.usgovcloudapi.net"
        "AzureRMEndpoint"="https://management.usgovcloudapi.net"
        "AzureRMAudienceEndpoint"="https://management.core.usgovcloudapi.net"
        "EnableAzureRMIdentity"="true"
        "GraphUrl"="graph.windows.net"
4. <span data-ttu-id="233ea-133">Save and then run the file by double-clicking it.</span><span class="sxs-lookup"><span data-stu-id="233ea-133">Save and then run the file by double-clicking it.</span></span>  <span data-ttu-id="233ea-134">You are prompted to merge the file into your registry.</span><span class="sxs-lookup"><span data-stu-id="233ea-134">You are prompted to merge the file into your registry.</span></span>
5. <span data-ttu-id="233ea-135">Launch Visual Studio and begin using [Cloud Explorer](../vs-azure-tools-resources-managing-with-cloud-explorer.md) with your Azure Government account.</span><span class="sxs-lookup"><span data-stu-id="233ea-135">Launch Visual Studio and begin using [Cloud Explorer](../vs-azure-tools-resources-managing-with-cloud-explorer.md) with your Azure Government account.</span></span>

> [!NOTE]
> <span data-ttu-id="233ea-136">Once this registry key is set, only Azure Government subscriptions are accessible.</span><span class="sxs-lookup"><span data-stu-id="233ea-136">Once this registry key is set, only Azure Government subscriptions are accessible.</span></span>  <span data-ttu-id="233ea-137">You still see subscriptions that you configured previously but they do not work because Visual Studio is now connected to Azure Government instead of Azure Public.</span><span class="sxs-lookup"><span data-stu-id="233ea-137">You still see subscriptions that you configured previously but they do not work because Visual Studio is now connected to Azure Government instead of Azure Public.</span></span>  <span data-ttu-id="233ea-138">See the following section for steps to revert the changes.</span><span class="sxs-lookup"><span data-stu-id="233ea-138">See the following section for steps to revert the changes.</span></span>
> 
> 

### <a name="reverting-visual-studio-connection-to-azure-government"></a><span data-ttu-id="233ea-139">Reverting Visual Studio Connection to Azure Government</span><span class="sxs-lookup"><span data-stu-id="233ea-139">Reverting Visual Studio Connection to Azure Government</span></span>
<span data-ttu-id="233ea-140">To enable Visual Studio to connect to Azure Public, you need to remove the registry settings that enable connection to Azure Government.</span><span class="sxs-lookup"><span data-stu-id="233ea-140">To enable Visual Studio to connect to Azure Public, you need to remove the registry settings that enable connection to Azure Government.</span></span>

1. <span data-ttu-id="233ea-141">Close Visual Studio</span><span class="sxs-lookup"><span data-stu-id="233ea-141">Close Visual Studio</span></span>
2. <span data-ttu-id="233ea-142">Create a text file named **VisualStudioForAzureGov_Remove.reg**</span><span class="sxs-lookup"><span data-stu-id="233ea-142">Create a text file named **VisualStudioForAzureGov_Remove.reg**</span></span>
3. <span data-ttu-id="233ea-143">Copy and paste the following text into **VisualStudioForAzureGov_Remove.reg**:</span><span class="sxs-lookup"><span data-stu-id="233ea-143">Copy and paste the following text into **VisualStudioForAzureGov_Remove.reg**:</span></span>
   
        Windows Registry Editor Version 5.00
   
        [HKEY_CURRENT_USER\Software\Microsoft\VSCommon\ConnectedUser]
        "AadInstance"=-
        "adaluri"=-
        "AzureRMEndpoint"=-
        "AzureRMAudienceEndpoint"=-
        "EnableAzureRMIdentity"=-
        "GraphUrl"=-
4. <span data-ttu-id="233ea-144">Save and then run the file by double-clicking it.</span><span class="sxs-lookup"><span data-stu-id="233ea-144">Save and then run the file by double-clicking it.</span></span>  <span data-ttu-id="233ea-145">You are prompted to merge the file into your registry.</span><span class="sxs-lookup"><span data-stu-id="233ea-145">You are prompted to merge the file into your registry.</span></span>
5. <span data-ttu-id="233ea-146">Launch Visual Studio</span><span class="sxs-lookup"><span data-stu-id="233ea-146">Launch Visual Studio</span></span>

> [!NOTE]
> <span data-ttu-id="233ea-147">Once this registry key has been reverted, your Azure Government subscriptions show but are not accessible.</span><span class="sxs-lookup"><span data-stu-id="233ea-147">Once this registry key has been reverted, your Azure Government subscriptions show but are not accessible.</span></span>  <span data-ttu-id="233ea-148">They can safely be removed.</span><span class="sxs-lookup"><span data-stu-id="233ea-148">They can safely be removed.</span></span>
> 
> 
