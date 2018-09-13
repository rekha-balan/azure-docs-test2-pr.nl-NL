---
title: Using Remote Desktop with Azure Roles | Microsoft Docs
description: Using Remote Desktop with Azure Roles
services: visual-studio-online
documentationcenter: na
author: TomArcher
manager: douge
editor: ''
ms.assetid: f5727ebe-9f57-4d7d-aff1-58761e8de8c1
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/11/2016
ms.author: tarcher
ms.openlocfilehash: 2bf3d26b7fe5647a732137a6e02cff7ae085fc05
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550090"
---
# <a name="using-remote-desktop-with-azure-roles"></a><span data-ttu-id="b15f2-103">Using Remote Desktop with Azure Roles</span><span class="sxs-lookup"><span data-stu-id="b15f2-103">Using Remote Desktop with Azure Roles</span></span>
<span data-ttu-id="b15f2-104">By using the Azure SDK and Remote Desktop Services, you can access Azure roles and virtual machines that are hosted by Azure.</span><span class="sxs-lookup"><span data-stu-id="b15f2-104">By using the Azure SDK and Remote Desktop Services, you can access Azure roles and virtual machines that are hosted by Azure.</span></span> <span data-ttu-id="b15f2-105">In Visual Studio, you can configure Remote Desktop Services from an Azure project.</span><span class="sxs-lookup"><span data-stu-id="b15f2-105">In Visual Studio, you can configure Remote Desktop Services from an Azure project.</span></span> <span data-ttu-id="b15f2-106">To enable Remote Desktop Services, you must create a working project that contains one or more roles and then publish it to Azure.</span><span class="sxs-lookup"><span data-stu-id="b15f2-106">To enable Remote Desktop Services, you must create a working project that contains one or more roles and then publish it to Azure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b15f2-107">You should access an Azure role for troubleshooting or development only.</span><span class="sxs-lookup"><span data-stu-id="b15f2-107">You should access an Azure role for troubleshooting or development only.</span></span> <span data-ttu-id="b15f2-108">The purpose of each virtual machine is to run a specific role in your Azure application, not to run other client applications.</span><span class="sxs-lookup"><span data-stu-id="b15f2-108">The purpose of each virtual machine is to run a specific role in your Azure application, not to run other client applications.</span></span> <span data-ttu-id="b15f2-109">If you want to use Azure to host a virtual machine that you can use for any purpose, see Accessing Azure Virtual Machines from Server Explorer.</span><span class="sxs-lookup"><span data-stu-id="b15f2-109">If you want to use Azure to host a virtual machine that you can use for any purpose, see Accessing Azure Virtual Machines from Server Explorer.</span></span>
> 
> 

## <a name="to-enable-and-use-remote-desktop-for-an-azure-role"></a><span data-ttu-id="b15f2-110">To enable and use Remote Desktop for an Azure Role</span><span class="sxs-lookup"><span data-stu-id="b15f2-110">To enable and use Remote Desktop for an Azure Role</span></span>
1. <span data-ttu-id="b15f2-111">In Solution Explorer, open the shortcut menu for your project, and then choose **Publish**.</span><span class="sxs-lookup"><span data-stu-id="b15f2-111">In Solution Explorer, open the shortcut menu for your project, and then choose **Publish**.</span></span>
   
    <span data-ttu-id="b15f2-112">The **Publish Azure Application** wizard appears.</span><span class="sxs-lookup"><span data-stu-id="b15f2-112">The **Publish Azure Application** wizard appears.</span></span>
   
    ![Publish command for a Cloud Service project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-remote-desktop-roles/IC799161.png)
2. <span data-ttu-id="b15f2-114">At the bottom of **Microsoft Azure Publish Settings** page of the wizard, select the **Enable Remote Desktop** for all roles check box.</span><span class="sxs-lookup"><span data-stu-id="b15f2-114">At the bottom of **Microsoft Azure Publish Settings** page of the wizard, select the **Enable Remote Desktop** for all roles check box.</span></span> 
   
    <span data-ttu-id="b15f2-115">The **Remote Desktop Configuration** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="b15f2-115">The **Remote Desktop Configuration** dialog box appears.</span></span>
3. <span data-ttu-id="b15f2-116">At the bottom of the **Remote Desktop Configuration** dialog box, choose the **More Options** button.</span><span class="sxs-lookup"><span data-stu-id="b15f2-116">At the bottom of the **Remote Desktop Configuration** dialog box, choose the **More Options** button.</span></span> 
   
    <span data-ttu-id="b15f2-117">This displays a dropdown list box that lets you create or choose a certificate so that you can encrypt credentials information when connecting via remote desktop.</span><span class="sxs-lookup"><span data-stu-id="b15f2-117">This displays a dropdown list box that lets you create or choose a certificate so that you can encrypt credentials information when connecting via remote desktop.</span></span>
4. <span data-ttu-id="b15f2-118">In the dropdown list, choose **&lt;Create>**, or choose an existing one from the list.</span><span class="sxs-lookup"><span data-stu-id="b15f2-118">In the dropdown list, choose **&lt;Create>**, or choose an existing one from the list.</span></span> 
   
    <span data-ttu-id="b15f2-119">If you choose an existing certificate, skip the following steps.</span><span class="sxs-lookup"><span data-stu-id="b15f2-119">If you choose an existing certificate, skip the following steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b15f2-120">The certificates that you need for a remote desktop connection are different from the certificates that you use for other Azure operations.</span><span class="sxs-lookup"><span data-stu-id="b15f2-120">The certificates that you need for a remote desktop connection are different from the certificates that you use for other Azure operations.</span></span> <span data-ttu-id="b15f2-121">The remote access certificate must have a private key.</span><span class="sxs-lookup"><span data-stu-id="b15f2-121">The remote access certificate must have a private key.</span></span>
   > 
   > 
   
    <span data-ttu-id="b15f2-122">The **Create Certificate** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="b15f2-122">The **Create Certificate** dialog box appears.</span></span>
   
   1. <span data-ttu-id="b15f2-123">Provide a friendly name for the new certificate, and then choose the **OK** button.</span><span class="sxs-lookup"><span data-stu-id="b15f2-123">Provide a friendly name for the new certificate, and then choose the **OK** button.</span></span> <span data-ttu-id="b15f2-124">The new certificate appears in the dropdown list box.</span><span class="sxs-lookup"><span data-stu-id="b15f2-124">The new certificate appears in the dropdown list box.</span></span>
   2. <span data-ttu-id="b15f2-125">In the **Remote Desktop Configuration** dialog box, provide a user name and a password.</span><span class="sxs-lookup"><span data-stu-id="b15f2-125">In the **Remote Desktop Configuration** dialog box, provide a user name and a password.</span></span>
      
       <span data-ttu-id="b15f2-126">You can’t use an existing account.</span><span class="sxs-lookup"><span data-stu-id="b15f2-126">You can’t use an existing account.</span></span> <span data-ttu-id="b15f2-127">Don’t specify Administrator as the user name for the new account.</span><span class="sxs-lookup"><span data-stu-id="b15f2-127">Don’t specify Administrator as the user name for the new account.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="b15f2-128">If the password doesn’t meet the complexity requirements, a red icon appears next to the password text box.</span><span class="sxs-lookup"><span data-stu-id="b15f2-128">If the password doesn’t meet the complexity requirements, a red icon appears next to the password text box.</span></span> <span data-ttu-id="b15f2-129">The password must include capital letters, lowercase letters, and numbers or symbols.</span><span class="sxs-lookup"><span data-stu-id="b15f2-129">The password must include capital letters, lowercase letters, and numbers or symbols.</span></span>
      > 
      > 
   3. <span data-ttu-id="b15f2-130">Choose a date on which the account will expire and after which remote desktop connections will be blocked.</span><span class="sxs-lookup"><span data-stu-id="b15f2-130">Choose a date on which the account will expire and after which remote desktop connections will be blocked.</span></span>
   4. <span data-ttu-id="b15f2-131">After you've provided all the required information, choose the **OK** button.</span><span class="sxs-lookup"><span data-stu-id="b15f2-131">After you've provided all the required information, choose the **OK** button.</span></span>
      
       <span data-ttu-id="b15f2-132">Several settings that enable Remote Access Services are added to the .cscfg and .csdef files.</span><span class="sxs-lookup"><span data-stu-id="b15f2-132">Several settings that enable Remote Access Services are added to the .cscfg and .csdef files.</span></span>
5. <span data-ttu-id="b15f2-133">In the **Microsoft Azure Publish Settings** wizard, choose the **OK** button when you’re ready to publish your cloud service.</span><span class="sxs-lookup"><span data-stu-id="b15f2-133">In the **Microsoft Azure Publish Settings** wizard, choose the **OK** button when you’re ready to publish your cloud service.</span></span>
   
    <span data-ttu-id="b15f2-134">If you're not ready to publish, choose the **Cancel** button.</span><span class="sxs-lookup"><span data-stu-id="b15f2-134">If you're not ready to publish, choose the **Cancel** button.</span></span> <span data-ttu-id="b15f2-135">The configuration settings are saved, and you can publish your cloud service later.</span><span class="sxs-lookup"><span data-stu-id="b15f2-135">The configuration settings are saved, and you can publish your cloud service later.</span></span>

## <a name="connect-to-an-azure-role-by-using-remote-desktop"></a><span data-ttu-id="b15f2-136">Connect to an Azure Role by using Remote Desktop</span><span class="sxs-lookup"><span data-stu-id="b15f2-136">Connect to an Azure Role by using Remote Desktop</span></span>
<span data-ttu-id="b15f2-137">After you publish your cloud service on Azure, you can use Server Explorer to log into the virtual machines that Azure hosts.</span><span class="sxs-lookup"><span data-stu-id="b15f2-137">After you publish your cloud service on Azure, you can use Server Explorer to log into the virtual machines that Azure hosts.</span></span> 

1. <span data-ttu-id="b15f2-138">In Server Explorer, expand the **Azure** node, and then expand the node for a cloud service and one of its roles to display a list of instances.</span><span class="sxs-lookup"><span data-stu-id="b15f2-138">In Server Explorer, expand the **Azure** node, and then expand the node for a cloud service and one of its roles to display a list of instances.</span></span>
2. <span data-ttu-id="b15f2-139">Open the shortcut menu for an instance node, and then choose **Connect Using Remote Desktop**.</span><span class="sxs-lookup"><span data-stu-id="b15f2-139">Open the shortcut menu for an instance node, and then choose **Connect Using Remote Desktop**.</span></span>
   
    ![Connecting via remote desktop](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-remote-desktop-roles/IC799162.png)
3. <span data-ttu-id="b15f2-141">Enter the user name and password that you created previously.</span><span class="sxs-lookup"><span data-stu-id="b15f2-141">Enter the user name and password that you created previously.</span></span> <span data-ttu-id="b15f2-142">You are now logged into your remote session.</span><span class="sxs-lookup"><span data-stu-id="b15f2-142">You are now logged into your remote session.</span></span>



