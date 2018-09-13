---
title: Bind using Secure LDAP (LDAPS) to an Azure AD Domain Services managed domain | Microsoft Docs
description: Bind to an Azure AD Domain Services managed domain using secure LDAP (LDAPS)
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: mtillman
editor: curtand
ms.assetid: 6871374a-0300-4275-9a45-a39a52c65ae4
ms.service: active-directory
ms.component: domain-services
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 08/01/2018
ms.author: maheshu
ms.openlocfilehash: 9728d42710ce44226363ea4954d83fcc3efbfb75
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865182"
---
# <a name="bind-to-an-azure-ad-domain-services-managed-domain-using-secure-ldap-ldaps"></a><span data-ttu-id="c9011-103">Bind to an Azure AD Domain Services managed domain using secure LDAP (LDAPS)</span><span class="sxs-lookup"><span data-stu-id="c9011-103">Bind to an Azure AD Domain Services managed domain using secure LDAP (LDAPS)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c9011-104">Before you begin</span><span class="sxs-lookup"><span data-stu-id="c9011-104">Before you begin</span></span>
<span data-ttu-id="c9011-105">Complete [Task 4 - configure DNS to access the managed domain from the internet](active-directory-ds-ldaps-configure-dns.md).</span><span class="sxs-lookup"><span data-stu-id="c9011-105">Complete [Task 4 - configure DNS to access the managed domain from the internet](active-directory-ds-ldaps-configure-dns.md).</span></span>


## <a name="task-5-bind-to-the-managed-domain-over-ldap-using-ldpexe"></a><span data-ttu-id="c9011-106">Task 5: Bind to the managed domain over LDAP using LDP.exe</span><span class="sxs-lookup"><span data-stu-id="c9011-106">Task 5: Bind to the managed domain over LDAP using LDP.exe</span></span>
<span data-ttu-id="c9011-107">You can use the LDP.exe tool, which is included in the Remote Server Administration tools package to bind and search over LDAP.</span><span class="sxs-lookup"><span data-stu-id="c9011-107">You can use the LDP.exe tool, which is included in the Remote Server Administration tools package to bind and search over LDAP.</span></span>

<span data-ttu-id="c9011-108">First, open LDP and connect to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="c9011-108">First, open LDP and connect to the managed domain.</span></span> <span data-ttu-id="c9011-109">Click **Connection** and click **Connect...** in the menu.</span><span class="sxs-lookup"><span data-stu-id="c9011-109">Click **Connection** and click **Connect...** in the menu.</span></span> <span data-ttu-id="c9011-110">Specify the DNS domain name of the managed domain.</span><span class="sxs-lookup"><span data-stu-id="c9011-110">Specify the DNS domain name of the managed domain.</span></span> <span data-ttu-id="c9011-111">Specify the port to use for connections.</span><span class="sxs-lookup"><span data-stu-id="c9011-111">Specify the port to use for connections.</span></span> <span data-ttu-id="c9011-112">For LDAP connections, use port 389.</span><span class="sxs-lookup"><span data-stu-id="c9011-112">For LDAP connections, use port 389.</span></span> <span data-ttu-id="c9011-113">For LDAPS connections, use port 636.</span><span class="sxs-lookup"><span data-stu-id="c9011-113">For LDAPS connections, use port 636.</span></span> <span data-ttu-id="c9011-114">Click **OK** button to connect to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="c9011-114">Click **OK** button to connect to the managed domain.</span></span>

<span data-ttu-id="c9011-115">Next, bind to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="c9011-115">Next, bind to the managed domain.</span></span> <span data-ttu-id="c9011-116">Click **Connection** and click **Bind...** in the menu.</span><span class="sxs-lookup"><span data-stu-id="c9011-116">Click **Connection** and click **Bind...** in the menu.</span></span> <span data-ttu-id="c9011-117">Provide the credentials of a user account belonging to the 'AAD DC Administrators' group.</span><span class="sxs-lookup"><span data-stu-id="c9011-117">Provide the credentials of a user account belonging to the 'AAD DC Administrators' group.</span></span>

<span data-ttu-id="c9011-118">Select **View**, and then select **Tree** in the menu.</span><span class="sxs-lookup"><span data-stu-id="c9011-118">Select **View**, and then select **Tree** in the menu.</span></span> <span data-ttu-id="c9011-119">Leave the Base DN field blank, and click OK.</span><span class="sxs-lookup"><span data-stu-id="c9011-119">Leave the Base DN field blank, and click OK.</span></span> <span data-ttu-id="c9011-120">Navigate to the container that you want to search, right-click the container, and select Search.</span><span class="sxs-lookup"><span data-stu-id="c9011-120">Navigate to the container that you want to search, right-click the container, and select Search.</span></span>

> [!TIP]
> - <span data-ttu-id="c9011-121">Users and groups synchronized from Azure AD are stored in the **AADDC Users** container.</span><span class="sxs-lookup"><span data-stu-id="c9011-121">Users and groups synchronized from Azure AD are stored in the **AADDC Users** container.</span></span> <span data-ttu-id="c9011-122">The search path for this container looks like ```CN=AADDC\ Users,DC=CONTOSO100,DC=COM```.</span><span class="sxs-lookup"><span data-stu-id="c9011-122">The search path for this container looks like ```CN=AADDC\ Users,DC=CONTOSO100,DC=COM```.</span></span>
> - <span data-ttu-id="c9011-123">Computer accounts for computers joined to the managed domain are stored in the **AADDC Computers** container.</span><span class="sxs-lookup"><span data-stu-id="c9011-123">Computer accounts for computers joined to the managed domain are stored in the **AADDC Computers** container.</span></span> <span data-ttu-id="c9011-124">The search path for this container looks like ```CN=AADDC\ Computers,DC=CONTOSO100,DC=COM```.</span><span class="sxs-lookup"><span data-stu-id="c9011-124">The search path for this container looks like ```CN=AADDC\ Computers,DC=CONTOSO100,DC=COM```.</span></span>
>
>

<span data-ttu-id="c9011-125">More information - [LDAP query basics](https://technet.microsoft.com/library/aa996205.aspx)</span><span class="sxs-lookup"><span data-stu-id="c9011-125">More information - [LDAP query basics](https://technet.microsoft.com/library/aa996205.aspx)</span></span>


## <a name="task-6-lock-down-secure-ldap-access-to-your-managed-domain-over-the-internet"></a><span data-ttu-id="c9011-126">Task 6: Lock down secure LDAP access to your managed domain over the internet</span><span class="sxs-lookup"><span data-stu-id="c9011-126">Task 6: Lock down secure LDAP access to your managed domain over the internet</span></span>
> [!NOTE]
> <span data-ttu-id="c9011-127">If you have not enabled LDAPS access to the managed domain over the internet, skip this configuration task.</span><span class="sxs-lookup"><span data-stu-id="c9011-127">If you have not enabled LDAPS access to the managed domain over the internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="c9011-128">Before you begin this task, complete the steps outlined in [Task 3](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md).</span><span class="sxs-lookup"><span data-stu-id="c9011-128">Before you begin this task, complete the steps outlined in [Task 3](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md).</span></span>

<span data-ttu-id="c9011-129">When you enable LDAPS access over the internet to your managed domain, it creates a security threat.</span><span class="sxs-lookup"><span data-stu-id="c9011-129">When you enable LDAPS access over the internet to your managed domain, it creates a security threat.</span></span> <span data-ttu-id="c9011-130">The managed domain is reachable from the internet at the port used for secure LDAP (that is, port 636).</span><span class="sxs-lookup"><span data-stu-id="c9011-130">The managed domain is reachable from the internet at the port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="c9011-131">You can choose to restrict access to the managed domain to specific known IP addresses.</span><span class="sxs-lookup"><span data-stu-id="c9011-131">You can choose to restrict access to the managed domain to specific known IP addresses.</span></span> <span data-ttu-id="c9011-132">Create a network security group (NSG) and associate it with the subnet where you have enabled Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="c9011-132">Create a network security group (NSG) and associate it with the subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="c9011-133">The sample NSG in the following table locks down secure LDAP access over the internet.</span><span class="sxs-lookup"><span data-stu-id="c9011-133">The sample NSG in the following table locks down secure LDAP access over the internet.</span></span> <span data-ttu-id="c9011-134">The rules in the NSG allow inbound secure LDAP access over TCP port 636 only from a specified set of IP addresses.</span><span class="sxs-lookup"><span data-stu-id="c9011-134">The rules in the NSG allow inbound secure LDAP access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="c9011-135">The default 'DenyAll' rule applies to all other inbound traffic from the internet.</span><span class="sxs-lookup"><span data-stu-id="c9011-135">The default 'DenyAll' rule applies to all other inbound traffic from the internet.</span></span> <span data-ttu-id="c9011-136">The NSG rule to allow LDAPS access over the internet from specified IP addresses has a higher priority than the DenyAll NSG rule.</span><span class="sxs-lookup"><span data-stu-id="c9011-136">The NSG rule to allow LDAPS access over the internet from specified IP addresses has a higher priority than the DenyAll NSG rule.</span></span>

![Sample NSG to secure LDAPS access over the internet](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="c9011-138">**More information** - [Network security groups](../virtual-network/security-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c9011-138">**More information** - [Network security groups](../virtual-network/security-overview.md).</span></span>


## <a name="related-content"></a><span data-ttu-id="c9011-139">Related content</span><span class="sxs-lookup"><span data-stu-id="c9011-139">Related content</span></span>
* [<span data-ttu-id="c9011-140">Azure AD Domain Services - Getting Started guide</span><span class="sxs-lookup"><span data-stu-id="c9011-140">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="c9011-141">Administer an Azure AD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="c9011-141">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="c9011-142">LDAP query basics</span><span class="sxs-lookup"><span data-stu-id="c9011-142">LDAP query basics</span></span>](https://technet.microsoft.com/library/aa996205.aspx)
* [<span data-ttu-id="c9011-143">Administer Group Policy on an Azure AD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="c9011-143">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="c9011-144">Network security groups</span><span class="sxs-lookup"><span data-stu-id="c9011-144">Network security groups</span></span>](../virtual-network/security-overview.md)
* [<span data-ttu-id="c9011-145">Create a Network Security Group</span><span class="sxs-lookup"><span data-stu-id="c9011-145">Create a Network Security Group</span></span>](../virtual-network/tutorial-filter-network-traffic.md)


## <a name="next-step"></a><span data-ttu-id="c9011-146">Next step</span><span class="sxs-lookup"><span data-stu-id="c9011-146">Next step</span></span>
[<span data-ttu-id="c9011-147">Troubleshoot secure LDAP on a managed domain</span><span class="sxs-lookup"><span data-stu-id="c9011-147">Troubleshoot secure LDAP on a managed domain</span></span>](active-directory-ds-ldaps-troubleshoot.md)
