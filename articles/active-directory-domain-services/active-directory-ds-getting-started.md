---
title: 'Azure Active Directory Domain Services: Getting Started | Microsoft Docs'
description: Enable Azure Active Directory Domain Services using the Azure portal
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: mtillman
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory
ms.component: domain-services
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/23/2018
ms.author: maheshu
ms.openlocfilehash: b6651c038a2b3abd15b8b0587e6a0e95832401b1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856573"
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal"></a><span data-ttu-id="4a843-103">Enable Azure Active Directory Domain Services using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="4a843-103">Enable Azure Active Directory Domain Services using the Azure portal</span></span>
<span data-ttu-id="4a843-104">This article shows how to enable Azure Active Directory Domain Services (Azure AD DS) using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4a843-104">This article shows how to enable Azure Active Directory Domain Services (Azure AD DS) using the Azure portal.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="4a843-105">Before you begin</span><span class="sxs-lookup"><span data-stu-id="4a843-105">Before you begin</span></span>
<span data-ttu-id="4a843-106">To complete the tasks listed in this article, you need:</span><span class="sxs-lookup"><span data-stu-id="4a843-106">To complete the tasks listed in this article, you need:</span></span>

* <span data-ttu-id="4a843-107">A valid **Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="4a843-107">A valid **Azure subscription**.</span></span>
* <span data-ttu-id="4a843-108">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span><span class="sxs-lookup"><span data-stu-id="4a843-108">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
* <span data-ttu-id="4a843-109">The **Azure subscription must be associated with the Azure AD directory**.</span><span class="sxs-lookup"><span data-stu-id="4a843-109">The **Azure subscription must be associated with the Azure AD directory**.</span></span>
* <span data-ttu-id="4a843-110">You need **global administrator** privileges in your Azure AD directory to enable Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="4a843-110">You need **global administrator** privileges in your Azure AD directory to enable Azure AD Domain Services.</span></span>


## <a name="enable-azure-ad-domain-services"></a><span data-ttu-id="4a843-111">Enable Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="4a843-111">Enable Azure AD Domain Services</span></span>

<span data-ttu-id="4a843-112">To launch the **Enable Azure AD Domain Services** wizard, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="4a843-112">To launch the **Enable Azure AD Domain Services** wizard, complete the following steps:</span></span>

1. <span data-ttu-id="4a843-113">Go to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4a843-113">Go to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4a843-114">In the left pane, click **Create a resource**.</span><span class="sxs-lookup"><span data-stu-id="4a843-114">In the left pane, click **Create a resource**.</span></span>
3. <span data-ttu-id="4a843-115">In the **New** page, type **Domain Services** into the search bar.</span><span class="sxs-lookup"><span data-stu-id="4a843-115">In the **New** page, type **Domain Services** into the search bar.</span></span>

    ![Search for domain services](./media/getting-started/search-domain-services.png)

4. <span data-ttu-id="4a843-117">Click to select **Azure AD Domain Services** from the list of search suggestions.</span><span class="sxs-lookup"><span data-stu-id="4a843-117">Click to select **Azure AD Domain Services** from the list of search suggestions.</span></span> <span data-ttu-id="4a843-118">On the **Azure AD Domain Services** page, click the **Create** button.</span><span class="sxs-lookup"><span data-stu-id="4a843-118">On the **Azure AD Domain Services** page, click the **Create** button.</span></span>

    ![Domain services view](./media/getting-started/domain-services-blade.png)

5. <span data-ttu-id="4a843-120">The **Enable Azure AD Domain Services** wizard is launched.</span><span class="sxs-lookup"><span data-stu-id="4a843-120">The **Enable Azure AD Domain Services** wizard is launched.</span></span>


## <a name="task-1-configure-basic-settings"></a><span data-ttu-id="4a843-121">Task 1: configure basic settings</span><span class="sxs-lookup"><span data-stu-id="4a843-121">Task 1: configure basic settings</span></span>
<span data-ttu-id="4a843-122">In the **Basics** page of the wizard, specify the DNS domain name for the managed domain.</span><span class="sxs-lookup"><span data-stu-id="4a843-122">In the **Basics** page of the wizard, specify the DNS domain name for the managed domain.</span></span> <span data-ttu-id="4a843-123">You can also choose the resource group and Azure location to which the managed domain should be deployed.</span><span class="sxs-lookup"><span data-stu-id="4a843-123">You can also choose the resource group and Azure location to which the managed domain should be deployed.</span></span>

![Configure basics](./media/getting-started/domain-services-blade-basics.png)

1. <span data-ttu-id="4a843-125">Choose the **DNS domain name** for your managed domain.</span><span class="sxs-lookup"><span data-stu-id="4a843-125">Choose the **DNS domain name** for your managed domain.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4a843-126">**Guidelines for selecting a DNS domain name**</span><span class="sxs-lookup"><span data-stu-id="4a843-126">**Guidelines for selecting a DNS domain name**</span></span>
   > * <span data-ttu-id="4a843-127">**Built-in domain name:** By default, the wizard specifies the default/built-in domain name of the directory (with a **.onmicrosoft.com** suffix) for you.</span><span class="sxs-lookup"><span data-stu-id="4a843-127">**Built-in domain name:** By default, the wizard specifies the default/built-in domain name of the directory (with a **.onmicrosoft.com** suffix) for you.</span></span> <span data-ttu-id="4a843-128">If you choose to enable secure LDAP access to the managed domain over the internet, expect issues creating a public DNS record or obtaining a secure LDAP certificate from a public CA for this domain name.</span><span class="sxs-lookup"><span data-stu-id="4a843-128">If you choose to enable secure LDAP access to the managed domain over the internet, expect issues creating a public DNS record or obtaining a secure LDAP certificate from a public CA for this domain name.</span></span> <span data-ttu-id="4a843-129">Microsoft owns the *.onmicrosoft.com* domain and CAs will not issue certificates vouching for this domain.</span><span class="sxs-lookup"><span data-stu-id="4a843-129">Microsoft owns the *.onmicrosoft.com* domain and CAs will not issue certificates vouching for this domain.</span></span>
   * <span data-ttu-id="4a843-130">**Custom domain names:** You can also type in a custom domain name.</span><span class="sxs-lookup"><span data-stu-id="4a843-130">**Custom domain names:** You can also type in a custom domain name.</span></span> <span data-ttu-id="4a843-131">In this example, the custom domain name is *contoso100.com*.</span><span class="sxs-lookup"><span data-stu-id="4a843-131">In this example, the custom domain name is *contoso100.com*.</span></span>
   * <span data-ttu-id="4a843-132">**Non-routable domain suffixes:** We generally recommend avoiding a non-routable domain name suffix.</span><span class="sxs-lookup"><span data-stu-id="4a843-132">**Non-routable domain suffixes:** We generally recommend avoiding a non-routable domain name suffix.</span></span> <span data-ttu-id="4a843-133">For instance, it is better to avoid creating a domain with the DNS domain name 'contoso.local'.</span><span class="sxs-lookup"><span data-stu-id="4a843-133">For instance, it is better to avoid creating a domain with the DNS domain name 'contoso.local'.</span></span> <span data-ttu-id="4a843-134">The '.local' DNS suffix is not routable and can cause issues with DNS resolution.</span><span class="sxs-lookup"><span data-stu-id="4a843-134">The '.local' DNS suffix is not routable and can cause issues with DNS resolution.</span></span>
   * <span data-ttu-id="4a843-135">**Domain prefix restrictions:** The prefix of your specified domain name (for example, *contoso100* in the *contoso100.com* domain name) must contain 15 or fewer characters.</span><span class="sxs-lookup"><span data-stu-id="4a843-135">**Domain prefix restrictions:** The prefix of your specified domain name (for example, *contoso100* in the *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="4a843-136">You cannot create a managed domain with a prefix longer than 15 characters.</span><span class="sxs-lookup"><span data-stu-id="4a843-136">You cannot create a managed domain with a prefix longer than 15 characters.</span></span>
   * <span data-ttu-id="4a843-137">**Network name conflicts:** Ensure that the DNS domain name you have chosen for the managed domain does not already exist in the virtual network.</span><span class="sxs-lookup"><span data-stu-id="4a843-137">**Network name conflicts:** Ensure that the DNS domain name you have chosen for the managed domain does not already exist in the virtual network.</span></span> <span data-ttu-id="4a843-138">Specifically, check whether:</span><span class="sxs-lookup"><span data-stu-id="4a843-138">Specifically, check whether:</span></span>
       * <span data-ttu-id="4a843-139">You already have an Active Directory domain with the same DNS domain name on the virtual network.</span><span class="sxs-lookup"><span data-stu-id="4a843-139">You already have an Active Directory domain with the same DNS domain name on the virtual network.</span></span>
       * <span data-ttu-id="4a843-140">The virtual network where you plan to enable the managed domain has a VPN connection with your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="4a843-140">The virtual network where you plan to enable the managed domain has a VPN connection with your on-premises network.</span></span> <span data-ttu-id="4a843-141">In this scenario, ensure you don't have a domain with the same DNS domain name on your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="4a843-141">In this scenario, ensure you don't have a domain with the same DNS domain name on your on-premises network.</span></span>
       * <span data-ttu-id="4a843-142">You have an existing cloud service with that name on the virtual network.</span><span class="sxs-lookup"><span data-stu-id="4a843-142">You have an existing cloud service with that name on the virtual network.</span></span>
    >

2. <span data-ttu-id="4a843-143">Select the Azure **Subscription** in which you would like to create the managed domain.</span><span class="sxs-lookup"><span data-stu-id="4a843-143">Select the Azure **Subscription** in which you would like to create the managed domain.</span></span>

3. <span data-ttu-id="4a843-144">Select the **Resource group** to which the managed domain should belong.</span><span class="sxs-lookup"><span data-stu-id="4a843-144">Select the **Resource group** to which the managed domain should belong.</span></span> <span data-ttu-id="4a843-145">Choose either the **Create new** or **Use existing** options to select the resource group.</span><span class="sxs-lookup"><span data-stu-id="4a843-145">Choose either the **Create new** or **Use existing** options to select the resource group.</span></span>

4. <span data-ttu-id="4a843-146">Choose the Azure **Location** in which the managed domain should be created.</span><span class="sxs-lookup"><span data-stu-id="4a843-146">Choose the Azure **Location** in which the managed domain should be created.</span></span> <span data-ttu-id="4a843-147">On the **Network** page of the wizard, you see only virtual networks that belong to the location you have selected.</span><span class="sxs-lookup"><span data-stu-id="4a843-147">On the **Network** page of the wizard, you see only virtual networks that belong to the location you have selected.</span></span>

5. <span data-ttu-id="4a843-148">Click **OK** to move on to the **Network** page of the wizard.</span><span class="sxs-lookup"><span data-stu-id="4a843-148">Click **OK** to move on to the **Network** page of the wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="4a843-149">Next step</span><span class="sxs-lookup"><span data-stu-id="4a843-149">Next step</span></span>
[<span data-ttu-id="4a843-150">Task 2: configure network settings</span><span class="sxs-lookup"><span data-stu-id="4a843-150">Task 2: configure network settings</span></span>](active-directory-ds-getting-started-network.md)
