---
title: Install Visual Studio and connect to Azure Stack | Microsoft Docs
description: Learn the steps required to install Visual Studio and connect to Azure Stack
services: azure-stack
documentationcenter: ''
author: heathl17
manager: byronr
editor: ''
ms.assetid: 2022dbe5-47fd-457d-9af3-6c01688171d7
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2016
ms.author: sngun
ms.openlocfilehash: 785cfcac1220a258905bae6ece58a0dda9f1be7c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550184"
---
# <a name="install-visual-studio-and-connect-to-azure-stack"></a><span data-ttu-id="d3133-103">Install Visual Studio and connect to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d3133-103">Install Visual Studio and connect to Azure Stack</span></span>

<span data-ttu-id="d3133-104">Use Visual Studio to author and deploy Azure Resource Manager [templates](azure-stack-arm-templates.md) in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="d3133-104">Use Visual Studio to author and deploy Azure Resource Manager [templates](azure-stack-arm-templates.md) in Azure Stack.</span></span> <span data-ttu-id="d3133-105">You can use the steps described in this article to install Visual Studio either on [MAS-CON01](azure-stack-connect-azure-stack.md#connect-with-remote-desktop) computer, Azure Stack host computer or on a Windows-based external client if you are connected through [VPN](azure-stack-connect-azure-stack.md#connect-with-vpn).</span><span class="sxs-lookup"><span data-stu-id="d3133-105">You can use the steps described in this article to install Visual Studio either on [MAS-CON01](azure-stack-connect-azure-stack.md#connect-with-remote-desktop) computer, Azure Stack host computer or on a Windows-based external client if you are connected through [VPN](azure-stack-connect-azure-stack.md#connect-with-vpn).</span></span> <span data-ttu-id="d3133-106">These steps perform a new installation of Visual Studio 2015 Community Edition.</span><span class="sxs-lookup"><span data-stu-id="d3133-106">These steps perform a new installation of Visual Studio 2015 Community Edition.</span></span> <span data-ttu-id="d3133-107">Read more about [coexistence](https://msdn.microsoft.com/library/ms246609.aspx) between other Visual Studio versions.</span><span class="sxs-lookup"><span data-stu-id="d3133-107">Read more about [coexistence](https://msdn.microsoft.com/library/ms246609.aspx) between other Visual Studio versions.</span></span>

## <a name="install-visual-studio"></a><span data-ttu-id="d3133-108">Install Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d3133-108">Install Visual Studio</span></span>
1. <span data-ttu-id="d3133-109">Download and run the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3133-109">Download and run the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span>             
2. <span data-ttu-id="d3133-110">Search for **Visual Studio Community 2015 with Microsoft Azure SDK - 2.9.6**, click **Add**, and **Install**.</span><span class="sxs-lookup"><span data-stu-id="d3133-110">Search for **Visual Studio Community 2015 with Microsoft Azure SDK - 2.9.6**, click **Add**, and **Install**.</span></span>

    ![Screenshot of WebPI install steps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-install-visual-studio/image1.png) 

3. <span data-ttu-id="d3133-112">Uninstall the **Microsoft Azure PowerShell** that is installed as part of the Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="d3133-112">Uninstall the **Microsoft Azure PowerShell** that is installed as part of the Azure SDK.</span></span>

    ![Screenshot of add/remove programs interface for Azure PowerShell](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-install-visual-studio/image2.png) 

4. [<span data-ttu-id="d3133-114">Install PowerShell for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d3133-114">Install PowerShell for Azure Stack</span></span>](azure-stack-powershell-install.md)

5. <span data-ttu-id="d3133-115">Restart the operating system after the installation completes.</span><span class="sxs-lookup"><span data-stu-id="d3133-115">Restart the operating system after the installation completes.</span></span>

## <a name="connect-to-azure-stack"></a><span data-ttu-id="d3133-116">Connect to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d3133-116">Connect to Azure Stack</span></span>

1. <span data-ttu-id="d3133-117">Launch Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3133-117">Launch Visual Studio.</span></span>

2. <span data-ttu-id="d3133-118">From the **View** menu, select **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="d3133-118">From the **View** menu, select **Cloud Explorer**.</span></span>

3. <span data-ttu-id="d3133-119">In the new pane, select **Add Account** and sign in with your Azure Active Directory credentials.</span><span class="sxs-lookup"><span data-stu-id="d3133-119">In the new pane, select **Add Account** and sign in with your Azure Active Directory credentials.</span></span>  
    <span data-ttu-id="d3133-120">![Screenshot of Cloud Explorer once logged in and connected to Azure Stack](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-install-visual-studio/image6.png)</span><span class="sxs-lookup"><span data-stu-id="d3133-120">![Screenshot of Cloud Explorer once logged in and connected to Azure Stack](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-install-visual-studio/image6.png)</span></span>

<span data-ttu-id="d3133-121">Once logged in, you can [deploy templates](azure-stack-deploy-template-visual-studio.md) or browse available resource types and resource groups to create your own templates.</span><span class="sxs-lookup"><span data-stu-id="d3133-121">Once logged in, you can [deploy templates](azure-stack-deploy-template-visual-studio.md) or browse available resource types and resource groups to create your own templates.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="d3133-122">Next Steps</span><span class="sxs-lookup"><span data-stu-id="d3133-122">Next Steps</span></span>

 - [<span data-ttu-id="d3133-123">Develop templates for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d3133-123">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)



