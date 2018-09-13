---
title: Before you deploy App Services on Azure Stack | Microsoft Docs
description: Steps to complete before deploying App Service on Azure Stack
services: azure-stack
documentationcenter: ''
author: apwestgarth
manager: stefsch
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/6/2017
ms.author: anwestg
ms.openlocfilehash: 8ada7e7d733cfeddcaf742ea5d296607c7392e7a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564530"
---
# <a name="before-you-get-started-with-app-service-on-azure-stack"></a><span data-ttu-id="d54e6-103">Before you get started with App Service on Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d54e6-103">Before you get started with App Service on Azure Stack</span></span>

<span data-ttu-id="d54e6-104">You need a few items to install App Service on Azure Stack:</span><span class="sxs-lookup"><span data-stu-id="d54e6-104">You need a few items to install App Service on Azure Stack:</span></span>

- <span data-ttu-id="d54e6-105">A completed deployment of [Azure Stack Technical Preview 3](azure-stack-run-powershell-script.md)</span><span class="sxs-lookup"><span data-stu-id="d54e6-105">A completed deployment of [Azure Stack Technical Preview 3](azure-stack-run-powershell-script.md)</span></span>
- <span data-ttu-id="d54e6-106">Enough space in your Azure Stack system for a small deployment of App Service on Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="d54e6-106">Enough space in your Azure Stack system for a small deployment of App Service on Azure Stack.</span></span>  <span data-ttu-id="d54e6-107">The required space is roughly 20 GB of disk space.</span><span class="sxs-lookup"><span data-stu-id="d54e6-107">The required space is roughly 20 GB of disk space.</span></span>
- <span data-ttu-id="d54e6-108">A Windows Server VM Image for use when creating Virtual Machines for App Service on Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d54e6-108">A Windows Server VM Image for use when creating Virtual Machines for App Service on Azure Stack</span></span>
- <span data-ttu-id="d54e6-109">[A server that's running SQL Server](#SQL-Server).</span><span class="sxs-lookup"><span data-stu-id="d54e6-109">[A server that's running SQL Server](#SQL-Server).</span></span>

>[!NOTE] 
> <span data-ttu-id="d54e6-110">The following steps ALL take place on the MAS-CON01 VM.</span><span class="sxs-lookup"><span data-stu-id="d54e6-110">The following steps ALL take place on the MAS-CON01 VM.</span></span>

## <a name="before-you-deploy-app-service-on-azure-stack"></a><span data-ttu-id="d54e6-111">Before you deploy App Service on Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d54e6-111">Before you deploy App Service on Azure Stack</span></span>

<span data-ttu-id="d54e6-112">To deploy a resource provider, you must run the PowerShell Integrated Scripting Environment(ISE) as an administrator.</span><span class="sxs-lookup"><span data-stu-id="d54e6-112">To deploy a resource provider, you must run the PowerShell Integrated Scripting Environment(ISE) as an administrator.</span></span> <span data-ttu-id="d54e6-113">For this reason, you need to allow cookies and JavaScript in the Internet Explorer profile that you use to sign in to Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d54e6-113">For this reason, you need to allow cookies and JavaScript in the Internet Explorer profile that you use to sign in to Azure Active Directory.</span></span>

## <a name="turn-off-internet-explorer-enhanced-security"></a><span data-ttu-id="d54e6-114">Turn off Internet Explorer enhanced security</span><span class="sxs-lookup"><span data-stu-id="d54e6-114">Turn off Internet Explorer enhanced security</span></span>

1.  <span data-ttu-id="d54e6-115">Sign in to the Azure Stack proof-of-concept (POC) computer as **AzureStack/administrator**, and then open **Server Manager**.</span><span class="sxs-lookup"><span data-stu-id="d54e6-115">Sign in to the Azure Stack proof-of-concept (POC) computer as **AzureStack/administrator**, and then open **Server Manager**.</span></span>
2.  <span data-ttu-id="d54e6-116">Turn off **Internet Explorer Enhanced Security Configuration** for both admins and users.</span><span class="sxs-lookup"><span data-stu-id="d54e6-116">Turn off **Internet Explorer Enhanced Security Configuration** for both admins and users.</span></span>
3.  <span data-ttu-id="d54e6-117">Sign in to the MAS-CON01.AzureStack.local virtual machine as an administrator, and then open **Server Manager**.</span><span class="sxs-lookup"><span data-stu-id="d54e6-117">Sign in to the MAS-CON01.AzureStack.local virtual machine as an administrator, and then open **Server Manager**.</span></span>
4.  <span data-ttu-id="d54e6-118">Turn off **Internet Explorer Enhanced Security Configuration** for both admins and users.</span><span class="sxs-lookup"><span data-stu-id="d54e6-118">Turn off **Internet Explorer Enhanced Security Configuration** for both admins and users.</span></span>

## <a name="enable-cookies"></a><span data-ttu-id="d54e6-119">Enable cookies</span><span class="sxs-lookup"><span data-stu-id="d54e6-119">Enable cookies</span></span>

1.  <span data-ttu-id="d54e6-120">Select **Start**, > **All apps**, > **Windows accessories**.</span><span class="sxs-lookup"><span data-stu-id="d54e6-120">Select **Start**, > **All apps**, > **Windows accessories**.</span></span> <span data-ttu-id="d54e6-121">Right-click **Internet Explorer** > **More** > **Run as an administrator**.</span><span class="sxs-lookup"><span data-stu-id="d54e6-121">Right-click **Internet Explorer** > **More** > **Run as an administrator**.</span></span>
2.  <span data-ttu-id="d54e6-122">If you are prompted, select **Use recommended security**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="d54e6-122">If you are prompted, select **Use recommended security**, and then select **OK**.</span></span>
3.  <span data-ttu-id="d54e6-123">In Internet Explorer, select **Tools** (the gear icon), > **Internet Options** > **Privacy** > **Advanced**.</span><span class="sxs-lookup"><span data-stu-id="d54e6-123">In Internet Explorer, select **Tools** (the gear icon), > **Internet Options** > **Privacy** > **Advanced**.</span></span>
4.  <span data-ttu-id="d54e6-124">Select **Advanced**.</span><span class="sxs-lookup"><span data-stu-id="d54e6-124">Select **Advanced**.</span></span> <span data-ttu-id="d54e6-125">Make sure that both of the **Accept** check boxes are selected, and then select **OK** and **OK** again.</span><span class="sxs-lookup"><span data-stu-id="d54e6-125">Make sure that both of the **Accept** check boxes are selected, and then select **OK** and **OK** again.</span></span>
5.  <span data-ttu-id="d54e6-126">Close Internet Explorer, and restart PowerShell ISE as an administrator.</span><span class="sxs-lookup"><span data-stu-id="d54e6-126">Close Internet Explorer, and restart PowerShell ISE as an administrator.</span></span>

## <a name="install-powershell-for-azure-stack"></a><span data-ttu-id="d54e6-127">Install PowerShell for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d54e6-127">Install PowerShell for Azure Stack</span></span>

<span data-ttu-id="d54e6-128">Follow the steps in this article [Install PowerShell](azure-stack-powershell-install.md)</span><span class="sxs-lookup"><span data-stu-id="d54e6-128">Follow the steps in this article [Install PowerShell](azure-stack-powershell-install.md)</span></span>

## <a name="using-visual-studio-with-azure-stack"></a><span data-ttu-id="d54e6-129">Using Visual Studio with Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d54e6-129">Using Visual Studio with Azure Stack</span></span>

<span data-ttu-id="d54e6-130">Follow the steps in this article - [Install Visual Studio](azure-stack-install-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="d54e6-130">Follow the steps in this article - [Install Visual Studio](azure-stack-install-visual-studio.md)</span></span>

## <a name="add-a-windows-server-2016-vm-image-to-azure-stack"></a><span data-ttu-id="d54e6-131">Add a Windows Server 2016 VM image to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d54e6-131">Add a Windows Server 2016 VM image to Azure Stack</span></span>

<span data-ttu-id="d54e6-132">App Service deploys a number of virtual machines and as such requires a Windows Server 2016 VM Image be available within Azure Stack - [Add a default virtual machine image](azure-stack-add-default-image.md)</span><span class="sxs-lookup"><span data-stu-id="d54e6-132">App Service deploys a number of virtual machines and as such requires a Windows Server 2016 VM Image be available within Azure Stack - [Add a default virtual machine image](azure-stack-add-default-image.md)</span></span>

## <a name="SQL-Server"></a><span data-ttu-id="d54e6-133">SQL Server</span><span class="sxs-lookup"><span data-stu-id="d54e6-133">SQL Server</span></span>

<span data-ttu-id="d54e6-134">By default, the App Service on Azure Stack installer is set to use the SQL Server that is installed along with the Azure Stack SQL Resource Provider.</span><span class="sxs-lookup"><span data-stu-id="d54e6-134">By default, the App Service on Azure Stack installer is set to use the SQL Server that is installed along with the Azure Stack SQL Resource Provider.</span></span> <span data-ttu-id="d54e6-135">When you install the SQL Server Resource Provider (SQL RP), ensure you take note of the database administrator username and password.</span><span class="sxs-lookup"><span data-stu-id="d54e6-135">When you install the SQL Server Resource Provider (SQL RP), ensure you take note of the database administrator username and password.</span></span> <span data-ttu-id="d54e6-136">You need both when you install App Service on Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="d54e6-136">You need both when you install App Service on Azure Stack.</span></span>
>[!NOTE]
> <span data-ttu-id="d54e6-137">You can deploy and use another server to run SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d54e6-137">You can deploy and use another server to run SQL Server.</span></span> <span data-ttu-id="d54e6-138">You can choose the SQL Server instance to use when you complete the options in the App Service on Azure Stack installer.</span><span class="sxs-lookup"><span data-stu-id="d54e6-138">You can choose the SQL Server instance to use when you complete the options in the App Service on Azure Stack installer.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d54e6-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="d54e6-139">Next steps</span></span>

- [<span data-ttu-id="d54e6-140">Install the App Service Resource Provider</span><span class="sxs-lookup"><span data-stu-id="d54e6-140">Install the App Service Resource Provider</span></span>](azure-stack-app-service-deploy.md)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-before-you-get-started/PSGallery.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-before-you-get-started/WebPI_InstalledProducts.png


