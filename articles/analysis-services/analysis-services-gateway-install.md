---
title: Install On-premises data gateway | Microsoft Docs
description: Learn how to install and configure an On-premises data gateway.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 09/10/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: 1ef5d51db34e0d0a947a4d6ba6c7e614b1ac3384
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868187"
---
# <a name="install-and-configure-an-on-premises-data-gateway"></a><span data-ttu-id="05eda-103">Install and configure an on-premises data gateway</span><span class="sxs-lookup"><span data-stu-id="05eda-103">Install and configure an on-premises data gateway</span></span>
<span data-ttu-id="05eda-104">An on-premises data gateway is required when one or more Azure Analysis Services servers in the same region connect to on-premises data sources.</span><span class="sxs-lookup"><span data-stu-id="05eda-104">An on-premises data gateway is required when one or more Azure Analysis Services servers in the same region connect to on-premises data sources.</span></span> <span data-ttu-id="05eda-105">To learn more about the gateway, see [On-premises data gateway](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="05eda-105">To learn more about the gateway, see [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05eda-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="05eda-106">Prerequisites</span></span>
<span data-ttu-id="05eda-107">**Minimum Requirements:**</span><span class="sxs-lookup"><span data-stu-id="05eda-107">**Minimum Requirements:**</span></span>

* <span data-ttu-id="05eda-108">.NET 4.5 Framework</span><span class="sxs-lookup"><span data-stu-id="05eda-108">.NET 4.5 Framework</span></span>
* <span data-ttu-id="05eda-109">64-bit version of Windows 7 / Windows Server 2008 R2 (or later)</span><span class="sxs-lookup"><span data-stu-id="05eda-109">64-bit version of Windows 7 / Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="05eda-110">**Recommended:**</span><span class="sxs-lookup"><span data-stu-id="05eda-110">**Recommended:**</span></span>

* <span data-ttu-id="05eda-111">8 Core CPU</span><span class="sxs-lookup"><span data-stu-id="05eda-111">8 Core CPU</span></span>
* <span data-ttu-id="05eda-112">8 GB Memory</span><span class="sxs-lookup"><span data-stu-id="05eda-112">8 GB Memory</span></span>
* <span data-ttu-id="05eda-113">64-bit version of Windows 2012 R2 (or later)</span><span class="sxs-lookup"><span data-stu-id="05eda-113">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="05eda-114">**Important considerations:**</span><span class="sxs-lookup"><span data-stu-id="05eda-114">**Important considerations:**</span></span>

* <span data-ttu-id="05eda-115">During setup, when registering your gateway with Azure, the default region for your subscription is selected.</span><span class="sxs-lookup"><span data-stu-id="05eda-115">During setup, when registering your gateway with Azure, the default region for your subscription is selected.</span></span> <span data-ttu-id="05eda-116">You can choose a different region.</span><span class="sxs-lookup"><span data-stu-id="05eda-116">You can choose a different region.</span></span> <span data-ttu-id="05eda-117">If you have servers in more than one region, you must install a gateway for each region.</span><span class="sxs-lookup"><span data-stu-id="05eda-117">If you have servers in more than one region, you must install a gateway for each region.</span></span> 
* <span data-ttu-id="05eda-118">The gateway cannot be installed on a domain controller.</span><span class="sxs-lookup"><span data-stu-id="05eda-118">The gateway cannot be installed on a domain controller.</span></span>
* <span data-ttu-id="05eda-119">Only one gateway can be installed on a single computer.</span><span class="sxs-lookup"><span data-stu-id="05eda-119">Only one gateway can be installed on a single computer.</span></span>
* <span data-ttu-id="05eda-120">Install the gateway on a computer that remains on and does not go to sleep.</span><span class="sxs-lookup"><span data-stu-id="05eda-120">Install the gateway on a computer that remains on and does not go to sleep.</span></span>
* <span data-ttu-id="05eda-121">Do not install the gateway on a computer wirelessly connected to your network.</span><span class="sxs-lookup"><span data-stu-id="05eda-121">Do not install the gateway on a computer wirelessly connected to your network.</span></span> <span data-ttu-id="05eda-122">Performance can be diminished.</span><span class="sxs-lookup"><span data-stu-id="05eda-122">Performance can be diminished.</span></span>
* <span data-ttu-id="05eda-123">When installing the gateway, the user account you're signed in to your computer with must have Log on as service privileges.</span><span class="sxs-lookup"><span data-stu-id="05eda-123">When installing the gateway, the user account you're signed in to your computer with must have Log on as service privileges.</span></span> <span data-ttu-id="05eda-124">When install is complete, the On-premises data gateway service uses the NT SERVICE\PBIEgwService account to log on as a service.</span><span class="sxs-lookup"><span data-stu-id="05eda-124">When install is complete, the On-premises data gateway service uses the NT SERVICE\PBIEgwService account to log on as a service.</span></span> <span data-ttu-id="05eda-125">A different account can be specified during setup or in Services after setup is complete.</span><span class="sxs-lookup"><span data-stu-id="05eda-125">A different account can be specified during setup or in Services after setup is complete.</span></span> <span data-ttu-id="05eda-126">Ensure Group Policy settings allow both the account you're signed in with when installing and the service account you choose have Log on as service privileges.</span><span class="sxs-lookup"><span data-stu-id="05eda-126">Ensure Group Policy settings allow both the account you're signed in with when installing and the service account you choose have Log on as service privileges.</span></span>
* <span data-ttu-id="05eda-127">Sign in to Azure with an account in Azure AD for the same [tenant](https://msdn.microsoft.com/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant) as the subscription you are registering the gateway in.</span><span class="sxs-lookup"><span data-stu-id="05eda-127">Sign in to Azure with an account in Azure AD for the same [tenant](https://msdn.microsoft.com/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant) as the subscription you are registering the gateway in.</span></span> <span data-ttu-id="05eda-128">Azure B2B (guest) accounts are not supported when installing and registering a gateway.</span><span class="sxs-lookup"><span data-stu-id="05eda-128">Azure B2B (guest) accounts are not supported when installing and registering a gateway.</span></span>
* <span data-ttu-id="05eda-129">If data sources are on an Azure Virtual Network (VNet), you must configure the [AlwaysUseGateway](analysis-services-vnet-gateway.md) server property.</span><span class="sxs-lookup"><span data-stu-id="05eda-129">If data sources are on an Azure Virtual Network (VNet), you must configure the [AlwaysUseGateway](analysis-services-vnet-gateway.md) server property.</span></span>
* <span data-ttu-id="05eda-130">The (unified) gateway described here is not supported in Azure Government, Azure Germany, and Azure China sovereign regions.</span><span class="sxs-lookup"><span data-stu-id="05eda-130">The (unified) gateway described here is not supported in Azure Government, Azure Germany, and Azure China sovereign regions.</span></span> <span data-ttu-id="05eda-131">Use **Dedicated On-premises gateway for Azure Analysis Services**, installed from your server's **Quick Start** in the portal.</span><span class="sxs-lookup"><span data-stu-id="05eda-131">Use **Dedicated On-premises gateway for Azure Analysis Services**, installed from your server's **Quick Start** in the portal.</span></span> 


## <a name="download"></a><span data-ttu-id="05eda-132">Download</span><span class="sxs-lookup"><span data-stu-id="05eda-132">Download</span></span>
 [<span data-ttu-id="05eda-133">Download the gateway</span><span class="sxs-lookup"><span data-stu-id="05eda-133">Download the gateway</span></span>](https://aka.ms/azureasgateway)

## <a name="install"></a><span data-ttu-id="05eda-134">Install</span><span class="sxs-lookup"><span data-stu-id="05eda-134">Install</span></span>

1. <span data-ttu-id="05eda-135">Run setup.</span><span class="sxs-lookup"><span data-stu-id="05eda-135">Run setup.</span></span>

2. <span data-ttu-id="05eda-136">Select a location, accept the terms, and then click **Install**.</span><span class="sxs-lookup"><span data-stu-id="05eda-136">Select a location, accept the terms, and then click **Install**.</span></span>

   ![Install location and license terms](media/analysis-services-gateway-install/aas-gateway-installer-accept.png)

3. <span data-ttu-id="05eda-138">Sign in to Azure.</span><span class="sxs-lookup"><span data-stu-id="05eda-138">Sign in to Azure.</span></span> <span data-ttu-id="05eda-139">The account must be in your tenant's Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="05eda-139">The account must be in your tenant's Azure Active Directory.</span></span> <span data-ttu-id="05eda-140">This account is used for the gateway administrator.</span><span class="sxs-lookup"><span data-stu-id="05eda-140">This account is used for the gateway administrator.</span></span> <span data-ttu-id="05eda-141">Azure B2B (guest) accounts are not supported when installing and registering the gateway.</span><span class="sxs-lookup"><span data-stu-id="05eda-141">Azure B2B (guest) accounts are not supported when installing and registering the gateway.</span></span>

   ![Sign in to Azure](media/analysis-services-gateway-install/aas-gateway-installer-account.png)

   > [!NOTE]
   > <span data-ttu-id="05eda-143">If you sign in with a domain account, it's mapped to your organizational account in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05eda-143">If you sign in with a domain account, it's mapped to your organizational account in Azure AD.</span></span> <span data-ttu-id="05eda-144">Your organizational account is used as the gateway administrator.</span><span class="sxs-lookup"><span data-stu-id="05eda-144">Your organizational account is used as the gateway administrator.</span></span>

## <a name="register"></a><span data-ttu-id="05eda-145">Register</span><span class="sxs-lookup"><span data-stu-id="05eda-145">Register</span></span>
<span data-ttu-id="05eda-146">In order to create a gateway resource in Azure, you must register the local instance you installed with the Gateway Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="05eda-146">In order to create a gateway resource in Azure, you must register the local instance you installed with the Gateway Cloud Service.</span></span> 

1.  <span data-ttu-id="05eda-147">Select **Register a new gateway on this computer**.</span><span class="sxs-lookup"><span data-stu-id="05eda-147">Select **Register a new gateway on this computer**.</span></span>

    ![Register](media/analysis-services-gateway-install/aas-gateway-register-new.png)

2. <span data-ttu-id="05eda-149">Type a name and recovery key for your gateway.</span><span class="sxs-lookup"><span data-stu-id="05eda-149">Type a name and recovery key for your gateway.</span></span> <span data-ttu-id="05eda-150">By default, the gateway uses your subscription's default region.</span><span class="sxs-lookup"><span data-stu-id="05eda-150">By default, the gateway uses your subscription's default region.</span></span> <span data-ttu-id="05eda-151">If you need to select a different region, select **Change Region**.</span><span class="sxs-lookup"><span data-stu-id="05eda-151">If you need to select a different region, select **Change Region**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="05eda-152">Save your recovery key in a safe place.</span><span class="sxs-lookup"><span data-stu-id="05eda-152">Save your recovery key in a safe place.</span></span> <span data-ttu-id="05eda-153">The recovery key is required in-order to takeover, migrate, or restore a gateway.</span><span class="sxs-lookup"><span data-stu-id="05eda-153">The recovery key is required in-order to takeover, migrate, or restore a gateway.</span></span> 

   ![Register](media/analysis-services-gateway-install/aas-gateway-register-name.png)


## <a name="create-resource"></a><span data-ttu-id="05eda-155">Create an Azure gateway resource</span><span class="sxs-lookup"><span data-stu-id="05eda-155">Create an Azure gateway resource</span></span>
<span data-ttu-id="05eda-156">After you've installed and registered your gateway, you need to create a gateway resource in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="05eda-156">After you've installed and registered your gateway, you need to create a gateway resource in your Azure subscription.</span></span> <span data-ttu-id="05eda-157">Sign in to Azure with the same account you used when registering the gateway.</span><span class="sxs-lookup"><span data-stu-id="05eda-157">Sign in to Azure with the same account you used when registering the gateway.</span></span>

1. <span data-ttu-id="05eda-158">In Azure portal, click **Create a resource** > **Integration** > **On-premises data gateway**.</span><span class="sxs-lookup"><span data-stu-id="05eda-158">In Azure portal, click **Create a resource** > **Integration** > **On-premises data gateway**.</span></span>

   ![Create a gateway resource](media/analysis-services-gateway-install/aas-gateway-new-azure-resource.png)

2. <span data-ttu-id="05eda-160">In **Create connection gateway**, enter these settings:</span><span class="sxs-lookup"><span data-stu-id="05eda-160">In **Create connection gateway**, enter these settings:</span></span>

    * <span data-ttu-id="05eda-161">**Name**: Enter a name for your gateway resource.</span><span class="sxs-lookup"><span data-stu-id="05eda-161">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="05eda-162">**Subscription**: Select the Azure subscription to associate with your gateway resource.</span><span class="sxs-lookup"><span data-stu-id="05eda-162">**Subscription**: Select the Azure subscription to associate with your gateway resource.</span></span> 
   
      <span data-ttu-id="05eda-163">The default subscription is based on the Azure account that you used to sign in.</span><span class="sxs-lookup"><span data-stu-id="05eda-163">The default subscription is based on the Azure account that you used to sign in.</span></span>

    * <span data-ttu-id="05eda-164">**Resource group**: Create a resource group or select an existing resource group.</span><span class="sxs-lookup"><span data-stu-id="05eda-164">**Resource group**: Create a resource group or select an existing resource group.</span></span>

    * <span data-ttu-id="05eda-165">**Location**: Select the region you registered your gateway in.</span><span class="sxs-lookup"><span data-stu-id="05eda-165">**Location**: Select the region you registered your gateway in.</span></span>

    * <span data-ttu-id="05eda-166">**Installation Name**: If your gateway installation isn't already selected, select the gateway registered.</span><span class="sxs-lookup"><span data-stu-id="05eda-166">**Installation Name**: If your gateway installation isn't already selected, select the gateway registered.</span></span> 

    <span data-ttu-id="05eda-167">When you're done, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="05eda-167">When you're done, click **Create**.</span></span>

## <a name="connect-servers"></a><span data-ttu-id="05eda-168">Connect servers to the gateway resource</span><span class="sxs-lookup"><span data-stu-id="05eda-168">Connect servers to the gateway resource</span></span>

1. <span data-ttu-id="05eda-169">In your Azure Analysis Services server overview, click **On-Premises Data Gateway**.</span><span class="sxs-lookup"><span data-stu-id="05eda-169">In your Azure Analysis Services server overview, click **On-Premises Data Gateway**.</span></span>

   ![Connect server to gateway](media/analysis-services-gateway-install/aas-gateway-connect-server.png)

2. <span data-ttu-id="05eda-171">In **Pick an On-Premises Data Gateway to connect**, select your gateway resource, and then click **Connect selected gateway**.</span><span class="sxs-lookup"><span data-stu-id="05eda-171">In **Pick an On-Premises Data Gateway to connect**, select your gateway resource, and then click **Connect selected gateway**.</span></span>

   ![Connect server to gateway resource](media/analysis-services-gateway-install/aas-gateway-connect-resource.png)

    > [!NOTE]
    > <span data-ttu-id="05eda-173">If your gateway does not appear in the list, your server is likely not in the same region as the region you specified when registering the gateway.</span><span class="sxs-lookup"><span data-stu-id="05eda-173">If your gateway does not appear in the list, your server is likely not in the same region as the region you specified when registering the gateway.</span></span> 

<span data-ttu-id="05eda-174">That's it.</span><span class="sxs-lookup"><span data-stu-id="05eda-174">That's it.</span></span> <span data-ttu-id="05eda-175">If you need to open ports or do any troubleshooting, be sure to check out [On-premises data gateway](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="05eda-175">If you need to open ports or do any troubleshooting, be sure to check out [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="05eda-176">Next steps</span><span class="sxs-lookup"><span data-stu-id="05eda-176">Next steps</span></span>
* [<span data-ttu-id="05eda-177">Manage Analysis Services</span><span class="sxs-lookup"><span data-stu-id="05eda-177">Manage Analysis Services</span></span>](analysis-services-manage.md)   
* [<span data-ttu-id="05eda-178">Get data from Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="05eda-178">Get data from Azure Analysis Services</span></span>](analysis-services-connect.md)   
* [<span data-ttu-id="05eda-179">Use gateway for data sources on an Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="05eda-179">Use gateway for data sources on an Azure Virtual Network</span></span>](analysis-services-vnet-gateway.md)
