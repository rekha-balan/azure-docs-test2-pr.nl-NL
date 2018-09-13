---
title: Connect to Azure Germany by using Visual Studio | Microsoft Docs
description: Information on managing your subscription in Azure Germany by using Visual Studio
services: germany
cloud: na
documentationcenter: na
author: gitralf
manager: rainerst
ms.assetid: na
ms.service: germany
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/13/2017
ms.author: ralfwi
ms.openlocfilehash: 07b15fa7211d1af4042d7b412dfc56d1cc7a0025
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855592"
---
# <a name="connect-to-azure-germany-by-using-visual-studio"></a><span data-ttu-id="26406-103">Connect to Azure Germany by using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="26406-103">Connect to Azure Germany by using Visual Studio</span></span>
<span data-ttu-id="26406-104">Developers use Visual Studio to easily manage their Azure subscriptions while building solutions.</span><span class="sxs-lookup"><span data-stu-id="26406-104">Developers use Visual Studio to easily manage their Azure subscriptions while building solutions.</span></span> <span data-ttu-id="26406-105">Currently, you can't configure a connection to Azure Germany in the Visual Studio user interface.</span><span class="sxs-lookup"><span data-stu-id="26406-105">Currently, you can't configure a connection to Azure Germany in the Visual Studio user interface.</span></span>  

## <a name="visual-studio-2017"></a><span data-ttu-id="26406-106">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="26406-106">Visual Studio 2017</span></span>
<span data-ttu-id="26406-107">Visual Studio 2017 requires a configuration file for Visual Studio to connect to Azure Germany.</span><span class="sxs-lookup"><span data-stu-id="26406-107">Visual Studio 2017 requires a configuration file for Visual Studio to connect to Azure Germany.</span></span> <span data-ttu-id="26406-108">With this file in place, Visual Studio connects to Azure Germany instead of global Azure.</span><span class="sxs-lookup"><span data-stu-id="26406-108">With this file in place, Visual Studio connects to Azure Germany instead of global Azure.</span></span>

### <a name="create-a-configuration-file-for-azure-germany"></a><span data-ttu-id="26406-109">Create a configuration file for Azure Germany</span><span class="sxs-lookup"><span data-stu-id="26406-109">Create a configuration file for Azure Germany</span></span>
<span data-ttu-id="26406-110">Create a file named **AadProvider.Configuration.json** with the following content:</span><span class="sxs-lookup"><span data-stu-id="26406-110">Create a file named **AadProvider.Configuration.json** with the following content:</span></span>

        {
          "AuthenticationQueryParameters":null,
          "AsmEndPoint":"https://management.microsoftazure.de/",
          "Authority":"https://login.microsoftonline.de/",
          "AzureResourceManagementEndpoint":"https://management.microsoftazure.de/",
          "AzureResourceManagementAudienceEndpoints":["https://management.core.cloudapi.de/"],
          "ClientIdentifier":"872cd9fa-d31f-45e0-9eab-6e460a02d1f1",
          "EnvironmentName":"BlackForest",
          "GraphEndpoint":"https://graph.cloudapi.de",
          "MsaHomeTenantId":"f577cd82-810c-43f9-a1f6-0cc532871050",
          "NativeClientRedirect":"urn:ietf:wg:oauth:2.0:oob",
          "PortalEndpoint":"https://portal.core.cloudapi.de/",
          "ResourceEndpoint":"https://management.microsoftazure.de/",
          "ValidateAuthority":true,
          "VisualStudioOnlineEndpoint":"https://app.vssps.visualstudio.com/",
          "VisualStudioOnlineAudience":"499b84ac-1321-427f-aa17-267ca6975798"
        }

### <a name="update-visual-studio-for-azure-germany"></a><span data-ttu-id="26406-111">Update Visual Studio for Azure Germany</span><span class="sxs-lookup"><span data-stu-id="26406-111">Update Visual Studio for Azure Germany</span></span>

1.  <span data-ttu-id="26406-112">Close Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="26406-112">Close Visual Studio.</span></span>
2.  <span data-ttu-id="26406-113">Place **AadProvider.Configuration.json** in **%localappdata%\\.IdentityService\AadConfigurations**.</span><span class="sxs-lookup"><span data-stu-id="26406-113">Place **AadProvider.Configuration.json** in **%localappdata%\\.IdentityService\AadConfigurations**.</span></span> <span data-ttu-id="26406-114">Create this folder if it isn't present.</span><span class="sxs-lookup"><span data-stu-id="26406-114">Create this folder if it isn't present.</span></span>
3.  <span data-ttu-id="26406-115">Start Visual Studio and begin using your Azure Germany account.</span><span class="sxs-lookup"><span data-stu-id="26406-115">Start Visual Studio and begin using your Azure Germany account.</span></span>

> [!NOTE]
> <span data-ttu-id="26406-116">With the configuration file, only Azure Germany subscriptions are accessible.</span><span class="sxs-lookup"><span data-stu-id="26406-116">With the configuration file, only Azure Germany subscriptions are accessible.</span></span> <span data-ttu-id="26406-117">You still see subscriptions that you configured previously, but they don't work because Visual Studio is now connected to Azure Germany instead of global Azure.</span><span class="sxs-lookup"><span data-stu-id="26406-117">You still see subscriptions that you configured previously, but they don't work because Visual Studio is now connected to Azure Germany instead of global Azure.</span></span> <span data-ttu-id="26406-118">To connect to global Azure, remove the file.</span><span class="sxs-lookup"><span data-stu-id="26406-118">To connect to global Azure, remove the file.</span></span>
> 
> 

### <a name="revert-a-visual-studio-connection-to-azure-germany"></a><span data-ttu-id="26406-119">Revert a Visual Studio connection to Azure Germany</span><span class="sxs-lookup"><span data-stu-id="26406-119">Revert a Visual Studio connection to Azure Germany</span></span>
<span data-ttu-id="26406-120">To enable Visual Studio to connect to global Azure, you need to remove the configuration file that enables the connection to Azure Germany.</span><span class="sxs-lookup"><span data-stu-id="26406-120">To enable Visual Studio to connect to global Azure, you need to remove the configuration file that enables the connection to Azure Germany.</span></span>

1.  <span data-ttu-id="26406-121">Close Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="26406-121">Close Visual Studio.</span></span>
2.  <span data-ttu-id="26406-122">Delete or rename the **%localappdata%\.IdentityService\AadConfigurations** folder.</span><span class="sxs-lookup"><span data-stu-id="26406-122">Delete or rename the **%localappdata%\.IdentityService\AadConfigurations** folder.</span></span>
3.  <span data-ttu-id="26406-123">Restart Visual Studio and begin using your global Azure account.</span><span class="sxs-lookup"><span data-stu-id="26406-123">Restart Visual Studio and begin using your global Azure account.</span></span>

> [!NOTE]
> <span data-ttu-id="26406-124">After this configuration is reverted, your Azure Germany subscriptions are no longer accessible.</span><span class="sxs-lookup"><span data-stu-id="26406-124">After this configuration is reverted, your Azure Germany subscriptions are no longer accessible.</span></span>
> 
>

## <a name="visual-studio-2015"></a><span data-ttu-id="26406-125">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="26406-125">Visual Studio 2015</span></span>
<span data-ttu-id="26406-126">Visual Studio 2015 requires a registry change for Visual Studio to connect to Azure Germany.</span><span class="sxs-lookup"><span data-stu-id="26406-126">Visual Studio 2015 requires a registry change for Visual Studio to connect to Azure Germany.</span></span> <span data-ttu-id="26406-127">After this registry key is set, Visual Studio connects to Azure Germany instead of global Azure.</span><span class="sxs-lookup"><span data-stu-id="26406-127">After this registry key is set, Visual Studio connects to Azure Germany instead of global Azure.</span></span>

### <a name="update-visual-studio-for-azure-germany"></a><span data-ttu-id="26406-128">Update Visual Studio for Azure Germany</span><span class="sxs-lookup"><span data-stu-id="26406-128">Update Visual Studio for Azure Germany</span></span>
<span data-ttu-id="26406-129">To enable Visual Studio to connect to Azure Germany, you need to update the registry.</span><span class="sxs-lookup"><span data-stu-id="26406-129">To enable Visual Studio to connect to Azure Germany, you need to update the registry.</span></span>

1. <span data-ttu-id="26406-130">Close Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="26406-130">Close Visual Studio.</span></span>
2. <span data-ttu-id="26406-131">Create a text file named **VisualStudioForAzureGermany.reg**.</span><span class="sxs-lookup"><span data-stu-id="26406-131">Create a text file named **VisualStudioForAzureGermany.reg**.</span></span>
3. <span data-ttu-id="26406-132">Copy and paste the following text into **VisualStudioForAzureGermany.reg**:</span><span class="sxs-lookup"><span data-stu-id="26406-132">Copy and paste the following text into **VisualStudioForAzureGermany.reg**:</span></span>
   
        Windows Registry Editor Version 5.00
 
        [HKEY_CURRENT_USER\Software\Microsoft\VSCommon\ConnectedUser]
        "AadInstance"="https://login.microsoftonline.de/"
        "adaluri"="https://management.microsoftazure.de"
        "AzureRMEndpoint"="https://management.microsoftazure.de"
        "AzureRMAudienceEndpoint"="https://management.core.cloudapi.de"
        "EnableAzureRMIdentity"="true"
        "GraphUrl"="graph.cloudapi.de"
        "AadApplicationTenant"="f577cd82-810c-43f9-a1f6-0cc532871050"

4. <span data-ttu-id="26406-133">Save and then run the file by double-clicking it.</span><span class="sxs-lookup"><span data-stu-id="26406-133">Save and then run the file by double-clicking it.</span></span> <span data-ttu-id="26406-134">You are prompted to merge the file into your registry.</span><span class="sxs-lookup"><span data-stu-id="26406-134">You are prompted to merge the file into your registry.</span></span>
5. <span data-ttu-id="26406-135">Start Visual Studio and begin using [Cloud Explorer](../vs-azure-tools-resources-managing-with-cloud-explorer.md) with your Azure Germany account.</span><span class="sxs-lookup"><span data-stu-id="26406-135">Start Visual Studio and begin using [Cloud Explorer](../vs-azure-tools-resources-managing-with-cloud-explorer.md) with your Azure Germany account.</span></span>

> [!NOTE]
> <span data-ttu-id="26406-136">After this registry key is set, only Azure Germany subscriptions are accessible.</span><span class="sxs-lookup"><span data-stu-id="26406-136">After this registry key is set, only Azure Germany subscriptions are accessible.</span></span> <span data-ttu-id="26406-137">You still see subscriptions that you configured previously, but they don't work because Visual Studio is now connected to Azure Germany instead of global Azure.</span><span class="sxs-lookup"><span data-stu-id="26406-137">You still see subscriptions that you configured previously, but they don't work because Visual Studio is now connected to Azure Germany instead of global Azure.</span></span> <span data-ttu-id="26406-138">To connect to global Azure, revert the changes.</span><span class="sxs-lookup"><span data-stu-id="26406-138">To connect to global Azure, revert the changes.</span></span>
> 
> 

### <a name="revert-a-visual-studio-connection-to-azure-germany"></a><span data-ttu-id="26406-139">Revert a Visual Studio connection to Azure Germany</span><span class="sxs-lookup"><span data-stu-id="26406-139">Revert a Visual Studio connection to Azure Germany</span></span>
<span data-ttu-id="26406-140">To enable Visual Studio to connect to global Azure, you need to remove the registry settings that enable the connection to Azure Germany.</span><span class="sxs-lookup"><span data-stu-id="26406-140">To enable Visual Studio to connect to global Azure, you need to remove the registry settings that enable the connection to Azure Germany.</span></span>

1. <span data-ttu-id="26406-141">Close Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="26406-141">Close Visual Studio.</span></span>
2. <span data-ttu-id="26406-142">Create a text file named **VisualStudioForAzureGermany_Remove.reg**.</span><span class="sxs-lookup"><span data-stu-id="26406-142">Create a text file named **VisualStudioForAzureGermany_Remove.reg**.</span></span>
3. <span data-ttu-id="26406-143">Copy and paste the following text into **VisualStudioForAzureGermany_Remove.reg**:</span><span class="sxs-lookup"><span data-stu-id="26406-143">Copy and paste the following text into **VisualStudioForAzureGermany_Remove.reg**:</span></span>
   
        Windows Registry Editor Version 5.00
   
        [HKEY_CURRENT_USER\Software\Microsoft\VSCommon\ConnectedUser]
        "AadInstance"=-
        "adaluri"=-
        "AzureRMEndpoint"=-
        "AzureRMAudienceEndpoint"=-
        "EnableAzureRMIdentity"=-
        "GraphUrl"=-
        
4. <span data-ttu-id="26406-144">Save and then run the file by double-clicking it.</span><span class="sxs-lookup"><span data-stu-id="26406-144">Save and then run the file by double-clicking it.</span></span> <span data-ttu-id="26406-145">You are prompted to merge the file into your registry.</span><span class="sxs-lookup"><span data-stu-id="26406-145">You are prompted to merge the file into your registry.</span></span>
5. <span data-ttu-id="26406-146">Start Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="26406-146">Start Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="26406-147">After this registry key is reverted, your Azure Germany subscriptions appear but are not accessible.</span><span class="sxs-lookup"><span data-stu-id="26406-147">After this registry key is reverted, your Azure Germany subscriptions appear but are not accessible.</span></span> <span data-ttu-id="26406-148">You can safely remove them.</span><span class="sxs-lookup"><span data-stu-id="26406-148">You can safely remove them.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="26406-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="26406-149">Next steps</span></span>
<span data-ttu-id="26406-150">For more information about connecting to Azure Germany, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="26406-150">For more information about connecting to Azure Germany, see the following resources:</span></span>

* [<span data-ttu-id="26406-151">Connect to Azure Germany by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="26406-151">Connect to Azure Germany by using PowerShell</span></span>](./germany-get-started-connect-with-ps.md)
* [<span data-ttu-id="26406-152">Connect to Azure Germany by using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="26406-152">Connect to Azure Germany by using Azure CLI</span></span>](./germany-get-started-connect-with-cli.md)
* [<span data-ttu-id="26406-153">Connect to Azure Germany by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="26406-153">Connect to Azure Germany by using the Azure portal</span></span>](./germany-get-started-connect-with-portal.md)





