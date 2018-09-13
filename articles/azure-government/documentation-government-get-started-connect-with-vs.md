---
title: Connect to Azure Government with Visual Studio | Microsoft Docs
description: Information on managing your subscription in Azure Government by connecting with Visual Studio
services: azure-government
cloud: gov
documentationcenter: ''
author: zakramer
manager: liki
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 08/10/2018
ms.author: yujhong
ms.openlocfilehash: a0282aa25c5bdf04d9684a1e79feeb16fa8747d2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44810276"
---
# <a name="develop-with-visual-studio"></a><span data-ttu-id="15cb1-103">Develop with Visual Studio</span><span class="sxs-lookup"><span data-stu-id="15cb1-103">Develop with Visual Studio</span></span>

<span data-ttu-id="15cb1-104">Visual Studio is used by developers to easily manage their Azure subscriptions while building solutions.</span><span class="sxs-lookup"><span data-stu-id="15cb1-104">Visual Studio is used by developers to easily manage their Azure subscriptions while building solutions.</span></span> <span data-ttu-id="15cb1-105">Visual Studio does not currently allow you to configure a connection to Azure Government in the user interface.</span><span class="sxs-lookup"><span data-stu-id="15cb1-105">Visual Studio does not currently allow you to configure a connection to Azure Government in the user interface.</span></span> 

<span data-ttu-id="15cb1-106">The following video demonstrates how to use the VS 2017 extension that enables you to switch between different Azure environments.</span><span class="sxs-lookup"><span data-stu-id="15cb1-106">The following video demonstrates how to use the VS 2017 extension that enables you to switch between different Azure environments.</span></span> <span data-ttu-id="15cb1-107">It walks you through installation and showing how easy it is to connect to Azure Government.</span><span class="sxs-lookup"><span data-stu-id="15cb1-107">It walks you through installation and showing how easy it is to connect to Azure Government.</span></span> <span data-ttu-id="15cb1-108">The same steps are described in this article.</span><span class="sxs-lookup"><span data-stu-id="15cb1-108">The same steps are described in this article.</span></span> <span data-ttu-id="15cb1-109">The topic also shows how you can achieve the same configuration manually.</span><span class="sxs-lookup"><span data-stu-id="15cb1-109">The topic also shows how you can achieve the same configuration manually.</span></span> 

> [!VIDEO https://channel9.msdn.com/blogs/Azure-Government/Azure-Environment-Selector-Visual-Studio-Extension/player]

<span data-ttu-id="15cb1-110">If you don't have an Azure Government subscription, create a [free account](https://azure.microsoft.com/global-infrastructure/government/request/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="15cb1-110">If you don't have an Azure Government subscription, create a [free account](https://azure.microsoft.com/global-infrastructure/government/request/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15cb1-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="15cb1-111">Prerequisites</span></span>

* <span data-ttu-id="15cb1-112">Review [Guidance for developers](documentation-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="15cb1-112">Review [Guidance for developers](documentation-government-developer-guide.md).</span></span><br/> <span data-ttu-id="15cb1-113">This article discusses Azure Government's unique URLs and endpoints for managing your environment.</span><span class="sxs-lookup"><span data-stu-id="15cb1-113">This article discusses Azure Government's unique URLs and endpoints for managing your environment.</span></span> <span data-ttu-id="15cb1-114">You must know about these endpoints in order to connect to Azure Government.</span><span class="sxs-lookup"><span data-stu-id="15cb1-114">You must know about these endpoints in order to connect to Azure Government.</span></span> 
* <span data-ttu-id="15cb1-115">Review [Compare Azure Government and global Azure](compare-azure-government-global-azure.md) and click on a service of interest to see variations between Azure Government and global Azure.</span><span class="sxs-lookup"><span data-stu-id="15cb1-115">Review [Compare Azure Government and global Azure](compare-azure-government-global-azure.md) and click on a service of interest to see variations between Azure Government and global Azure.</span></span>

## <a name="visual-studio-2017"></a><span data-ttu-id="15cb1-116">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="15cb1-116">Visual Studio 2017</span></span>

### <a name="automatically-configuring-your-target-using-a-visual-studio-extension"></a><span data-ttu-id="15cb1-117">Automatically configuring your target using a Visual Studio Extension</span><span class="sxs-lookup"><span data-stu-id="15cb1-117">Automatically configuring your target using a Visual Studio Extension</span></span> 

>[!NOTE] 
><span data-ttu-id="15cb1-118">This is the recommended way to connect to Azure Government through Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="15cb1-118">This is the recommended way to connect to Azure Government through Visual Studio.</span></span> 
>

<span data-ttu-id="15cb1-119">The Visual Studio extension allows for quickly and easily switching between Azure environments.</span><span class="sxs-lookup"><span data-stu-id="15cb1-119">The Visual Studio extension allows for quickly and easily switching between Azure environments.</span></span> <span data-ttu-id="15cb1-120">This can be installed like any other extension in Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="15cb1-120">This can be installed like any other extension in Visual Studio:</span></span> 

1. <span data-ttu-id="15cb1-121">In the **Tools** menu, open **Extension and Updates**</span><span class="sxs-lookup"><span data-stu-id="15cb1-121">In the **Tools** menu, open **Extension and Updates**</span></span>
2. <span data-ttu-id="15cb1-122">Click the **Online** tab on the left and **Search "*azure environment selector*"**.</span><span class="sxs-lookup"><span data-stu-id="15cb1-122">Click the **Online** tab on the left and **Search "*azure environment selector*"**.</span></span>
3. <span data-ttu-id="15cb1-123">**Download** the package, as shown in the screenshot below.</span><span class="sxs-lookup"><span data-stu-id="15cb1-123">**Download** the package, as shown in the screenshot below.</span></span>

      ![Download the extension](./media/documentation-government-get-started-connect-with-vs-extension1.png)   

4. <span data-ttu-id="15cb1-125">**Restart Visual Studio** to complete the installation of the extension.</span><span class="sxs-lookup"><span data-stu-id="15cb1-125">**Restart Visual Studio** to complete the installation of the extension.</span></span>
5. <span data-ttu-id="15cb1-126">Once Visual Studio restarts, in the **Tools** menu, open the newly available **Azure Environment Selector**:</span><span class="sxs-lookup"><span data-stu-id="15cb1-126">Once Visual Studio restarts, in the **Tools** menu, open the newly available **Azure Environment Selector**:</span></span>

      ![Azure Environment Selector](./media/documentation-government-get-started-connect-with-vs-extension2.png)

6. <span data-ttu-id="15cb1-128">In the Azure Environment Selector dialog, select **Azure Government** from the dropdown:</span><span class="sxs-lookup"><span data-stu-id="15cb1-128">In the Azure Environment Selector dialog, select **Azure Government** from the dropdown:</span></span>

      ![Azure Government](./media/documentation-government-get-started-connect-with-vs-extension4.png)

<span data-ttu-id="15cb1-130">From here, you can restart Visual Studio and the change will take effect.</span><span class="sxs-lookup"><span data-stu-id="15cb1-130">From here, you can restart Visual Studio and the change will take effect.</span></span> <span data-ttu-id="15cb1-131">Once Visual Studio restarts, you will now be able to connect to other environments with VS tools such as the Cloud Explorer (shown below connected to Azure Government), Server Explorer, the main Visual Studio login, and the Visual Studio Solution Explorer.</span><span class="sxs-lookup"><span data-stu-id="15cb1-131">Once Visual Studio restarts, you will now be able to connect to other environments with VS tools such as the Cloud Explorer (shown below connected to Azure Government), Server Explorer, the main Visual Studio login, and the Visual Studio Solution Explorer.</span></span>

![Azure Government](./media/documentation-government-get-started-connect-with-vs-extension5.png)

 
### <a name="manually-configuring-your-target"></a><span data-ttu-id="15cb1-133">Manually configuring your target</span><span class="sxs-lookup"><span data-stu-id="15cb1-133">Manually configuring your target</span></span> 

>[!NOTE] 
><span data-ttu-id="15cb1-134">If you have successfully completed the extension installation above, you do not need to complete this section.</span><span class="sxs-lookup"><span data-stu-id="15cb1-134">If you have successfully completed the extension installation above, you do not need to complete this section.</span></span>
>

#### <a name="manually-creating-a-configuration-file-for-azure-government"></a><span data-ttu-id="15cb1-135">Manually creating a configuration file for Azure Government</span><span class="sxs-lookup"><span data-stu-id="15cb1-135">Manually creating a configuration file for Azure Government</span></span> 
<span data-ttu-id="15cb1-136">Create a file named **AadProvider.Configuration.json** with the following content:</span><span class="sxs-lookup"><span data-stu-id="15cb1-136">Create a file named **AadProvider.Configuration.json** with the following content:</span></span>

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

#### <a name="manually-updating-visual-studio-for-azure-government"></a><span data-ttu-id="15cb1-137">Manually updating Visual Studio for Azure Government</span><span class="sxs-lookup"><span data-stu-id="15cb1-137">Manually updating Visual Studio for Azure Government</span></span>

1.  <span data-ttu-id="15cb1-138">Close Visual Studio</span><span class="sxs-lookup"><span data-stu-id="15cb1-138">Close Visual Studio</span></span>
2.  <span data-ttu-id="15cb1-139">Place **AadProvider.Configuration.json** created in the previous step into **%localappdata%\\.IdentityService\AadConfigurations**.</span><span class="sxs-lookup"><span data-stu-id="15cb1-139">Place **AadProvider.Configuration.json** created in the previous step into **%localappdata%\\.IdentityService\AadConfigurations**.</span></span>  <span data-ttu-id="15cb1-140">Create this folder if not present.</span><span class="sxs-lookup"><span data-stu-id="15cb1-140">Create this folder if not present.</span></span>
3.  <span data-ttu-id="15cb1-141">Launch Visual Studio and begin using your Azure Government account.</span><span class="sxs-lookup"><span data-stu-id="15cb1-141">Launch Visual Studio and begin using your Azure Government account.</span></span>

> [!NOTE]
> <span data-ttu-id="15cb1-142">With the configuration file, only Azure Government subscriptions are accessible.</span><span class="sxs-lookup"><span data-stu-id="15cb1-142">With the configuration file, only Azure Government subscriptions are accessible.</span></span>  <span data-ttu-id="15cb1-143">You still see subscriptions that you configured previously but they do not work because Visual Studio is now connected to Azure Government instead of global Azure.</span><span class="sxs-lookup"><span data-stu-id="15cb1-143">You still see subscriptions that you configured previously but they do not work because Visual Studio is now connected to Azure Government instead of global Azure.</span></span>  <span data-ttu-id="15cb1-144">Remove the file to connect to Azure Commercial.</span><span class="sxs-lookup"><span data-stu-id="15cb1-144">Remove the file to connect to Azure Commercial.</span></span>
> 
> 

#### <a name="manually-reverting-visual-studio-connection-to-azure-government"></a><span data-ttu-id="15cb1-145">Manually reverting Visual Studio Connection to Azure Government</span><span class="sxs-lookup"><span data-stu-id="15cb1-145">Manually reverting Visual Studio Connection to Azure Government</span></span>
<span data-ttu-id="15cb1-146">To enable Visual Studio to connect to global Azure, you need to remove the configuration file setting that enables connection to Azure Government.</span><span class="sxs-lookup"><span data-stu-id="15cb1-146">To enable Visual Studio to connect to global Azure, you need to remove the configuration file setting that enables connection to Azure Government.</span></span>

1.  <span data-ttu-id="15cb1-147">Close Visual Studio</span><span class="sxs-lookup"><span data-stu-id="15cb1-147">Close Visual Studio</span></span>
2.  <span data-ttu-id="15cb1-148">Delete this folder: **%localappdata%\.IdentityService\AadConfigurations**</span><span class="sxs-lookup"><span data-stu-id="15cb1-148">Delete this folder: **%localappdata%\.IdentityService\AadConfigurations**</span></span>
3.  <span data-ttu-id="15cb1-149">Restart Visual Studio and begin using your global Azure account.</span><span class="sxs-lookup"><span data-stu-id="15cb1-149">Restart Visual Studio and begin using your global Azure account.</span></span>

> [!NOTE]
> <span data-ttu-id="15cb1-150">Once this configuration has been reverted, your Azure Government subscriptions no longer accessible.</span><span class="sxs-lookup"><span data-stu-id="15cb1-150">Once this configuration has been reverted, your Azure Government subscriptions no longer accessible.</span></span>
> 
>

## <a name="visual-studio-2015"></a><span data-ttu-id="15cb1-151">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="15cb1-151">Visual Studio 2015</span></span>

<span data-ttu-id="15cb1-152">Visual Studio 2015 requires a registry change for Visual Studio to connect to Azure Government.</span><span class="sxs-lookup"><span data-stu-id="15cb1-152">Visual Studio 2015 requires a registry change for Visual Studio to connect to Azure Government.</span></span> <span data-ttu-id="15cb1-153">Once this registry key is set, Visual Studio connects to Azure Government instead of global Azure.</span><span class="sxs-lookup"><span data-stu-id="15cb1-153">Once this registry key is set, Visual Studio connects to Azure Government instead of global Azure.</span></span>

### <a name="updating-visual-studio-for-azure-government"></a><span data-ttu-id="15cb1-154">Updating Visual Studio for Azure Government</span><span class="sxs-lookup"><span data-stu-id="15cb1-154">Updating Visual Studio for Azure Government</span></span>
<span data-ttu-id="15cb1-155">To enable Visual Studio to connect to Azure Government, you need to update the registry.</span><span class="sxs-lookup"><span data-stu-id="15cb1-155">To enable Visual Studio to connect to Azure Government, you need to update the registry.</span></span>

1. <span data-ttu-id="15cb1-156">Close Visual Studio</span><span class="sxs-lookup"><span data-stu-id="15cb1-156">Close Visual Studio</span></span>
2. <span data-ttu-id="15cb1-157">Create a text file named **VisualStudioForAzureGov.reg**</span><span class="sxs-lookup"><span data-stu-id="15cb1-157">Create a text file named **VisualStudioForAzureGov.reg**</span></span>
3. <span data-ttu-id="15cb1-158">Copy and paste the following text into **VisualStudioForAzureGov.reg**:</span><span class="sxs-lookup"><span data-stu-id="15cb1-158">Copy and paste the following text into **VisualStudioForAzureGov.reg**:</span></span>
   
        Windows Registry Editor Version 5.00
   
        [HKEY_CURRENT_USER\Software\Microsoft\VSCommon\ConnectedUser]
        "AadInstance"="https://login.microsoftonline.us/"
        "adaluri"="https://management.core.usgovcloudapi.net"
        "AzureRMEndpoint"="https://management.usgovcloudapi.net"
        "AzureRMAudienceEndpoint"="https://management.core.usgovcloudapi.net"
        "EnableAzureRMIdentity"="true"
        "GraphUrl"="graph.windows.net"
4. <span data-ttu-id="15cb1-159">Save and then run the file by double-clicking it.</span><span class="sxs-lookup"><span data-stu-id="15cb1-159">Save and then run the file by double-clicking it.</span></span>  <span data-ttu-id="15cb1-160">You are prompted to merge the file into your registry.</span><span class="sxs-lookup"><span data-stu-id="15cb1-160">You are prompted to merge the file into your registry.</span></span>
5. <span data-ttu-id="15cb1-161">Launch Visual Studio and begin using [Cloud Explorer](../vs-azure-tools-resources-managing-with-cloud-explorer.md) with your Azure Government account.</span><span class="sxs-lookup"><span data-stu-id="15cb1-161">Launch Visual Studio and begin using [Cloud Explorer](../vs-azure-tools-resources-managing-with-cloud-explorer.md) with your Azure Government account.</span></span>

> [!NOTE]
> <span data-ttu-id="15cb1-162">Once this registry key is set, only Azure Government subscriptions are accessible.</span><span class="sxs-lookup"><span data-stu-id="15cb1-162">Once this registry key is set, only Azure Government subscriptions are accessible.</span></span>  <span data-ttu-id="15cb1-163">You still see subscriptions that you configured previously but they do not work because Visual Studio is now connected to Azure Government instead of global Azure.</span><span class="sxs-lookup"><span data-stu-id="15cb1-163">You still see subscriptions that you configured previously but they do not work because Visual Studio is now connected to Azure Government instead of global Azure.</span></span>  <span data-ttu-id="15cb1-164">See the following section for steps to revert the changes.</span><span class="sxs-lookup"><span data-stu-id="15cb1-164">See the following section for steps to revert the changes.</span></span>
> 
> 

### <a name="reverting-visual-studio-connection-to-azure-government"></a><span data-ttu-id="15cb1-165">Reverting Visual Studio Connection to Azure Government</span><span class="sxs-lookup"><span data-stu-id="15cb1-165">Reverting Visual Studio Connection to Azure Government</span></span>
<span data-ttu-id="15cb1-166">To enable Visual Studio to connect to global Azure, you need to remove the registry settings that enable connection to Azure Government.</span><span class="sxs-lookup"><span data-stu-id="15cb1-166">To enable Visual Studio to connect to global Azure, you need to remove the registry settings that enable connection to Azure Government.</span></span>

1. <span data-ttu-id="15cb1-167">Close Visual Studio</span><span class="sxs-lookup"><span data-stu-id="15cb1-167">Close Visual Studio</span></span>
2. <span data-ttu-id="15cb1-168">Create a text file named **VisualStudioForAzureGov_Remove.reg**</span><span class="sxs-lookup"><span data-stu-id="15cb1-168">Create a text file named **VisualStudioForAzureGov_Remove.reg**</span></span>
3. <span data-ttu-id="15cb1-169">Copy and paste the following text into **VisualStudioForAzureGov_Remove.reg**:</span><span class="sxs-lookup"><span data-stu-id="15cb1-169">Copy and paste the following text into **VisualStudioForAzureGov_Remove.reg**:</span></span>
   
        Windows Registry Editor Version 5.00
   
        [HKEY_CURRENT_USER\Software\Microsoft\VSCommon\ConnectedUser]
        "AadInstance"=-
        "adaluri"=-
        "AzureRMEndpoint"=-
        "AzureRMAudienceEndpoint"=-
        "EnableAzureRMIdentity"=-
        "GraphUrl"=-
4. <span data-ttu-id="15cb1-170">Save and then run the file by double-clicking it.</span><span class="sxs-lookup"><span data-stu-id="15cb1-170">Save and then run the file by double-clicking it.</span></span>  <span data-ttu-id="15cb1-171">You are prompted to merge the file into your registry.</span><span class="sxs-lookup"><span data-stu-id="15cb1-171">You are prompted to merge the file into your registry.</span></span>
5. <span data-ttu-id="15cb1-172">Launch Visual Studio</span><span class="sxs-lookup"><span data-stu-id="15cb1-172">Launch Visual Studio</span></span>

> [!NOTE]
> <span data-ttu-id="15cb1-173">Once this registry key has been reverted, your Azure Government subscriptions show but are not accessible.</span><span class="sxs-lookup"><span data-stu-id="15cb1-173">Once this registry key has been reverted, your Azure Government subscriptions show but are not accessible.</span></span>  <span data-ttu-id="15cb1-174">They can safely be removed.</span><span class="sxs-lookup"><span data-stu-id="15cb1-174">They can safely be removed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="15cb1-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="15cb1-175">Next steps</span></span>

<span data-ttu-id="15cb1-176">[Develop with Azure DevOps Services](documentation-government-get-started-connect-with-vsts.md)
[Develop with SQL Server Management Studio](documentation-government-connect-ssms.md)</span><span class="sxs-lookup"><span data-stu-id="15cb1-176">[Develop with Azure DevOps Services](documentation-government-get-started-connect-with-vsts.md)
[Develop with SQL Server Management Studio](documentation-government-connect-ssms.md)</span></span>
