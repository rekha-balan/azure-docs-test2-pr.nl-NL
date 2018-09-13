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
ms.openlocfilehash: c167f40e09ac877d00d348285383106fc5ba41bc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868412"
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal"></a><span data-ttu-id="c8616-103">Enable Azure Active Directory Domain Services using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="c8616-103">Enable Azure Active Directory Domain Services using the Azure portal</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="c8616-104">Before you begin</span><span class="sxs-lookup"><span data-stu-id="c8616-104">Before you begin</span></span>
<span data-ttu-id="c8616-105">Refer to [Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="c8616-105">Refer to [Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>


## <a name="task-2-configure-network-settings"></a><span data-ttu-id="c8616-106">Task 2: configure network settings</span><span class="sxs-lookup"><span data-stu-id="c8616-106">Task 2: configure network settings</span></span>
<span data-ttu-id="c8616-107">The next configuration task is to create an Azure virtual network and a dedicated subnet within it.</span><span class="sxs-lookup"><span data-stu-id="c8616-107">The next configuration task is to create an Azure virtual network and a dedicated subnet within it.</span></span> <span data-ttu-id="c8616-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span><span class="sxs-lookup"><span data-stu-id="c8616-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="c8616-109">You may also pick an existing virtual network and create the dedicated subnet within it.</span><span class="sxs-lookup"><span data-stu-id="c8616-109">You may also pick an existing virtual network and create the dedicated subnet within it.</span></span>

1. <span data-ttu-id="c8616-110">Click **Virtual network** to select a virtual network.</span><span class="sxs-lookup"><span data-stu-id="c8616-110">Click **Virtual network** to select a virtual network.</span></span>
    > [!NOTE]
    > <span data-ttu-id="c8616-111">**Classic virtual networks are not supported for new deployments.**</span><span class="sxs-lookup"><span data-stu-id="c8616-111">**Classic virtual networks are not supported for new deployments.**</span></span> <span data-ttu-id="c8616-112">Classic virtual networks are not supported for new deployments.</span><span class="sxs-lookup"><span data-stu-id="c8616-112">Classic virtual networks are not supported for new deployments.</span></span> <span data-ttu-id="c8616-113">Existing managed domains deployed in classic virtual networks continue to be supported.</span><span class="sxs-lookup"><span data-stu-id="c8616-113">Existing managed domains deployed in classic virtual networks continue to be supported.</span></span> <span data-ttu-id="c8616-114">Microsoft will enable you to migrate an existing managed domain from a classic virtual network to a Resource Manager virtual network in the near future.</span><span class="sxs-lookup"><span data-stu-id="c8616-114">Microsoft will enable you to migrate an existing managed domain from a classic virtual network to a Resource Manager virtual network in the near future.</span></span>
    >

2. <span data-ttu-id="c8616-115">On the **Choose virtual network** page, you see all existing virtual networks.</span><span class="sxs-lookup"><span data-stu-id="c8616-115">On the **Choose virtual network** page, you see all existing virtual networks.</span></span> <span data-ttu-id="c8616-116">You see only the virtual networks that belong to the resource group and Azure location you have selected on the **Basics** wizard page.</span><span class="sxs-lookup"><span data-stu-id="c8616-116">You see only the virtual networks that belong to the resource group and Azure location you have selected on the **Basics** wizard page.</span></span>
3. <span data-ttu-id="c8616-117">Choose the virtual network in which Azure AD Domain Services should be enabled.</span><span class="sxs-lookup"><span data-stu-id="c8616-117">Choose the virtual network in which Azure AD Domain Services should be enabled.</span></span> <span data-ttu-id="c8616-118">You can either pick an existing virtual network or create a new one.</span><span class="sxs-lookup"><span data-stu-id="c8616-118">You can either pick an existing virtual network or create a new one.</span></span>

  > [!TIP]
  > <span data-ttu-id="c8616-119">**You cannot move your managed domain to a different virtual network after you enable Azure AD Domain Services.**</span><span class="sxs-lookup"><span data-stu-id="c8616-119">**You cannot move your managed domain to a different virtual network after you enable Azure AD Domain Services.**</span></span> <span data-ttu-id="c8616-120">Pick the right virtual network to enable your managed domain.</span><span class="sxs-lookup"><span data-stu-id="c8616-120">Pick the right virtual network to enable your managed domain.</span></span> <span data-ttu-id="c8616-121">After you create a managed domain, you cannot move it to a different virtual network, without deleting the managed domain.</span><span class="sxs-lookup"><span data-stu-id="c8616-121">After you create a managed domain, you cannot move it to a different virtual network, without deleting the managed domain.</span></span> <span data-ttu-id="c8616-122">We recommend reviewing the [networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md) before you proceed.</span><span class="sxs-lookup"><span data-stu-id="c8616-122">We recommend reviewing the [networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md) before you proceed.</span></span>  
  >

4. <span data-ttu-id="c8616-123">**Create virtual network:** Click **Create new** to create a new virtual network.</span><span class="sxs-lookup"><span data-stu-id="c8616-123">**Create virtual network:** Click **Create new** to create a new virtual network.</span></span> <span data-ttu-id="c8616-124">Use a dedicated subnet for Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="c8616-124">Use a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="c8616-125">For example, create a subnet with the name 'DomainServices', making it easy for other administrators to understand what is deployed within the subnet.</span><span class="sxs-lookup"><span data-stu-id="c8616-125">For example, create a subnet with the name 'DomainServices', making it easy for other administrators to understand what is deployed within the subnet.</span></span> <span data-ttu-id="c8616-126">Click **OK** when you're done.</span><span class="sxs-lookup"><span data-stu-id="c8616-126">Click **OK** when you're done.</span></span>

    ![Pick virtual network](./media/getting-started/domain-services-blade-network-pick-vnet.png)

  > [!WARNING]
  > <span data-ttu-id="c8616-128">Make sure to pick an address space that is within the private IP address space.</span><span class="sxs-lookup"><span data-stu-id="c8616-128">Make sure to pick an address space that is within the private IP address space.</span></span> <span data-ttu-id="c8616-129">IP Addresses that you do not own that are in the public address space cause errors within Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="c8616-129">IP Addresses that you do not own that are in the public address space cause errors within Azure AD Domain Services.</span></span>

5. <span data-ttu-id="c8616-130">**Existing virtual network:** If you plan to pick an existing virtual network, [create a dedicated subnet using the virtual networks extension](../virtual-network/virtual-network-manage-subnet.md#add-a-subnet), and then pick that subnet.</span><span class="sxs-lookup"><span data-stu-id="c8616-130">**Existing virtual network:** If you plan to pick an existing virtual network, [create a dedicated subnet using the virtual networks extension](../virtual-network/virtual-network-manage-subnet.md#add-a-subnet), and then pick that subnet.</span></span> <span data-ttu-id="c8616-131">Click **Virtual Network** to select the existing virtual network.</span><span class="sxs-lookup"><span data-stu-id="c8616-131">Click **Virtual Network** to select the existing virtual network.</span></span> <span data-ttu-id="c8616-132">Click **Subnet** to pick the dedicated subnet in your existing virtual network, within which to enable your new managed domain.</span><span class="sxs-lookup"><span data-stu-id="c8616-132">Click **Subnet** to pick the dedicated subnet in your existing virtual network, within which to enable your new managed domain.</span></span> <span data-ttu-id="c8616-133">Click **OK** when you're done.</span><span class="sxs-lookup"><span data-stu-id="c8616-133">Click **OK** when you're done.</span></span>

    ![Pick subnet within the virtual network](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > <span data-ttu-id="c8616-135">**Guidelines for selecting a subnet**</span><span class="sxs-lookup"><span data-stu-id="c8616-135">**Guidelines for selecting a subnet**</span></span>
  > 1. <span data-ttu-id="c8616-136">Use a dedicated subnet for Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="c8616-136">Use a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="c8616-137">Do not deploy any other virtual machines to this subnet.</span><span class="sxs-lookup"><span data-stu-id="c8616-137">Do not deploy any other virtual machines to this subnet.</span></span> <span data-ttu-id="c8616-138">This configuration enables you to configure network security groups (NSGs) for your workloads/virtual machines without disrupting your managed domain.</span><span class="sxs-lookup"><span data-stu-id="c8616-138">This configuration enables you to configure network security groups (NSGs) for your workloads/virtual machines without disrupting your managed domain.</span></span> <span data-ttu-id="c8616-139">For details, see [networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="c8616-139">For details, see [networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>
  2. <span data-ttu-id="c8616-140">Do not select the Gateway subnet for deploying Azure AD Domain Services, because it is not a supported configuration.</span><span class="sxs-lookup"><span data-stu-id="c8616-140">Do not select the Gateway subnet for deploying Azure AD Domain Services, because it is not a supported configuration.</span></span>
  3. <span data-ttu-id="c8616-141">The subnet you've selected must have at least 3-5 available IP addresses in its address space.</span><span class="sxs-lookup"><span data-stu-id="c8616-141">The subnet you've selected must have at least 3-5 available IP addresses in its address space.</span></span>
  >

6. <span data-ttu-id="c8616-142">When you are done, click **OK** to proceed to the **Administrator group** page of the wizard.</span><span class="sxs-lookup"><span data-stu-id="c8616-142">When you are done, click **OK** to proceed to the **Administrator group** page of the wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="c8616-143">Next step</span><span class="sxs-lookup"><span data-stu-id="c8616-143">Next step</span></span>
[<span data-ttu-id="c8616-144">Task 3: configure administrative group and enable Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="c8616-144">Task 3: configure administrative group and enable Azure AD Domain Services</span></span>](active-directory-ds-getting-started-admingroup.md)
