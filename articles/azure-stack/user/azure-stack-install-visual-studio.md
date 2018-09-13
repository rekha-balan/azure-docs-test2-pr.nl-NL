---
title: Install Visual Studio and connect to Azure Stack | Microsoft Docs
description: Learn the steps required to install Visual Studio and connect to Azure Stack
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.service: azure-stack
ms.custom: vs-azure
ms.workload: azure-vs
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2018
ms.author: sethm
ms.reviewer: unknown
ms.openlocfilehash: 2afbea68c017805e9bd7db43b03face0705608b7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868838"
---
# <a name="install-visual-studio-and-connect-to-azure-stack"></a><span data-ttu-id="197b4-103">Install Visual Studio and connect to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="197b4-103">Install Visual Studio and connect to Azure Stack</span></span>

<span data-ttu-id="197b4-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="197b4-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="197b4-105">You can use Visual Studio to write and deploy Azure Resource Manager [templates](azure-stack-arm-templates.md) to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="197b4-105">You can use Visual Studio to write and deploy Azure Resource Manager [templates](azure-stack-arm-templates.md) to Azure Stack.</span></span> <span data-ttu-id="197b4-106">The steps in this article walk you through installing Visual Studio on the [Azure Stack](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or on an external computer if you plan to Azure Stack through the [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).</span><span class="sxs-lookup"><span data-stu-id="197b4-106">The steps in this article walk you through installing Visual Studio on the [Azure Stack](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or on an external computer if you plan to Azure Stack through the [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).</span></span>

## <a name="install-visual-studio"></a><span data-ttu-id="197b4-107">Install Visual Studio</span><span class="sxs-lookup"><span data-stu-id="197b4-107">Install Visual Studio</span></span>

1. <span data-ttu-id="197b4-108">Download and run the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="197b4-108">Download and run the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span>  

2. <span data-ttu-id="197b4-109">Open the **Microsoft Web Platform Installer**.</span><span class="sxs-lookup"><span data-stu-id="197b4-109">Open the **Microsoft Web Platform Installer**.</span></span>

3. <span data-ttu-id="197b4-110">Search for **Visual Studio Community 2015 with Microsoft Azure SDK - 2.9.6**.</span><span class="sxs-lookup"><span data-stu-id="197b4-110">Search for **Visual Studio Community 2015 with Microsoft Azure SDK - 2.9.6**.</span></span> <span data-ttu-id="197b4-111">Click **Add**, and **Install**.</span><span class="sxs-lookup"><span data-stu-id="197b4-111">Click **Add**, and **Install**.</span></span>

4. <span data-ttu-id="197b4-112">Uninstall the **Microsoft Azure PowerShell** that is installed as part of the Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="197b4-112">Uninstall the **Microsoft Azure PowerShell** that is installed as part of the Azure SDK.</span></span>

    ![Screenshot of WebPI install steps](./media/azure-stack-install-visual-studio/image1.png) 

5. [<span data-ttu-id="197b4-114">Install PowerShell for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="197b4-114">Install PowerShell for Azure Stack</span></span>](azure-stack-powershell-install.md)

6. <span data-ttu-id="197b4-115">Restart the operating system after the installation completes.</span><span class="sxs-lookup"><span data-stu-id="197b4-115">Restart the operating system after the installation completes.</span></span>

## <a name="connect-to-azure-stack-with-azure-ad"></a><span data-ttu-id="197b4-116">Connect to Azure Stack with Azure AD</span><span class="sxs-lookup"><span data-stu-id="197b4-116">Connect to Azure Stack with Azure AD</span></span>

1. <span data-ttu-id="197b4-117">Launch Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="197b4-117">Launch Visual Studio.</span></span>

2. <span data-ttu-id="197b4-118">From the **View** menu, select **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="197b4-118">From the **View** menu, select **Cloud Explorer**.</span></span>

3. <span data-ttu-id="197b4-119">In the new pane, select **Add Account** and sign in with your Azure Active Directory (Azure AD) credentials.</span><span class="sxs-lookup"><span data-stu-id="197b4-119">In the new pane, select **Add Account** and sign in with your Azure Active Directory (Azure AD) credentials.</span></span>  

    ![Screenshot of Cloud Explorer once logged in and connected to Azure Stack](./media/azure-stack-install-visual-studio/image2.png)

<span data-ttu-id="197b4-121">Once logged in, you can [deploy templates](azure-stack-deploy-template-visual-studio.md) or browse available resource types and resource groups to create your own templates.</span><span class="sxs-lookup"><span data-stu-id="197b4-121">Once logged in, you can [deploy templates](azure-stack-deploy-template-visual-studio.md) or browse available resource types and resource groups to create your own templates.</span></span>  

## <a name="connect-to-azure-stack-with-ad-fs"></a><span data-ttu-id="197b4-122">Connect to Azure Stack with AD FS</span><span class="sxs-lookup"><span data-stu-id="197b4-122">Connect to Azure Stack with AD FS</span></span>

1. <span data-ttu-id="197b4-123">Launch Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="197b4-123">Launch Visual Studio.</span></span>

2. <span data-ttu-id="197b4-124">From **Tools**, select **Options**.</span><span class="sxs-lookup"><span data-stu-id="197b4-124">From **Tools**, select **Options**.</span></span>

3. <span data-ttu-id="197b4-125">Expand **Environment** in the **Navigation Pane** and select **Accounts**.</span><span class="sxs-lookup"><span data-stu-id="197b4-125">Expand **Environment** in the **Navigation Pane** and select **Accounts**.</span></span>

4. <span data-ttu-id="197b4-126">Select **Add**, and enter the User Azure Resource Manger endpoint.</span><span class="sxs-lookup"><span data-stu-id="197b4-126">Select **Add**, and enter the User Azure Resource Manger endpoint.</span></span>  
  <span data-ttu-id="197b4-127">For the Azure Stack Development kit, the URL is: `https://management.local.azurestack/external`.</span><span class="sxs-lookup"><span data-stu-id="197b4-127">For the Azure Stack Development kit, the URL is: `https://management.local.azurestack/external`.</span></span>  
  <span data-ttu-id="197b4-128">For Azure Stack integrated systems the URL is: `https://management.[Region}.[External FQDN]`.</span><span class="sxs-lookup"><span data-stu-id="197b4-128">For Azure Stack integrated systems the URL is: `https://management.[Region}.[External FQDN]`.</span></span>

    ![X](./media/azure-stack-install-visual-studio/image5.png)

5. <span data-ttu-id="197b4-130">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="197b4-130">Select **Add**.</span></span>  

    <span data-ttu-id="197b4-131">Visual Studio calls the Azure Resource Manger and discovers the endpoints including the authentication endpoint for Azure Directory Federated Services (AD FS).</span><span class="sxs-lookup"><span data-stu-id="197b4-131">Visual Studio calls the Azure Resource Manger and discovers the endpoints including the authentication endpoint for Azure Directory Federated Services (AD FS).</span></span>

    ![Screenshot of Cloud Explorer once logged in and connected to Azure Stack](./media/azure-stack-install-visual-studio/image6.png)

6. <span data-ttu-id="197b4-133">Select **Cloud Explorer** from the **View** menu.</span><span class="sxs-lookup"><span data-stu-id="197b4-133">Select **Cloud Explorer** from the **View** menu.</span></span>
7. <span data-ttu-id="197b4-134">Select **Add Account** and sign in with your AD FS credentials.</span><span class="sxs-lookup"><span data-stu-id="197b4-134">Select **Add Account** and sign in with your AD FS credentials.</span></span>  

    ![X](./media/azure-stack-install-visual-studio/image7.png)

    <span data-ttu-id="197b4-136">Cloud Explorer queries the available subscriptions.</span><span class="sxs-lookup"><span data-stu-id="197b4-136">Cloud Explorer queries the available subscriptions.</span></span> <span data-ttu-id="197b4-137">You can select one an available subscription to manage.</span><span class="sxs-lookup"><span data-stu-id="197b4-137">You can select one an available subscription to manage.</span></span>

    ![X](./media/azure-stack-install-visual-studio/image8.png)

8. <span data-ttu-id="197b4-139">Browsing your existing resources, resource groups, or deploy templates.</span><span class="sxs-lookup"><span data-stu-id="197b4-139">Browsing your existing resources, resource groups, or deploy templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="197b4-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="197b4-140">Next steps</span></span>

 - <span data-ttu-id="197b4-141">Read more about [coexistence](https://msdn.microsoft.com/library/ms246609.aspx) with other Visual Studio versions.</span><span class="sxs-lookup"><span data-stu-id="197b4-141">Read more about [coexistence](https://msdn.microsoft.com/library/ms246609.aspx) with other Visual Studio versions.</span></span>
 - [<span data-ttu-id="197b4-142">Develop templates for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="197b4-142">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)