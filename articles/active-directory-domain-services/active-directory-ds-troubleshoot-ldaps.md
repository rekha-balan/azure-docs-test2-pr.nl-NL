---
title: 'Azure Active Directory Domain Services: Troubleshooting Secure LDAP configuration | Microsoft Docs'
description: Troubleshooting Secure LDAP for Azure AD Domain Services
services: active-directory-ds
documentationcenter: ''
author: eringreenlee
manager: ''
editor: ''
ms.assetid: 81208c0b-8d41-4f65-be15-42119b1b5957
ms.service: active-directory
ms.component: domain-services
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 02/21/2018
ms.author: ergreenl
ms.openlocfilehash: e3a31749407f9ec0494e8452b602ed9966c5ab83
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968270"
---
# <a name="azure-ad-domain-services---troubleshooting-secure-ldap-configuration"></a><span data-ttu-id="e388a-103">Azure AD Domain Services - Troubleshooting Secure LDAP configuration</span><span class="sxs-lookup"><span data-stu-id="e388a-103">Azure AD Domain Services - Troubleshooting Secure LDAP configuration</span></span>

<span data-ttu-id="e388a-104">This article provides resolutions for common issues when [configuring secure LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md) for Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="e388a-104">This article provides resolutions for common issues when [configuring secure LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md) for Azure AD Domain Services.</span></span>

## <a name="aadds101-secure-ldap-network-security-group-configuration"></a><span data-ttu-id="e388a-105">AADDS101: Secure LDAP Network Security Group configuration</span><span class="sxs-lookup"><span data-stu-id="e388a-105">AADDS101: Secure LDAP Network Security Group configuration</span></span>

<span data-ttu-id="e388a-106">**Alert message:**</span><span class="sxs-lookup"><span data-stu-id="e388a-106">**Alert message:**</span></span>

<span data-ttu-id="e388a-107">*Secure LDAP over the internet is enabled for the managed domain. However, access to port 636 is not locked down using a network security group. This may expose user accounts on the managed domain to password brute-force attacks.*</span><span class="sxs-lookup"><span data-stu-id="e388a-107">*Secure LDAP over the internet is enabled for the managed domain. However, access to port 636 is not locked down using a network security group. This may expose user accounts on the managed domain to password brute-force attacks.*</span></span>

### <a name="secure-ldap-port"></a><span data-ttu-id="e388a-108">Secure LDAP port</span><span class="sxs-lookup"><span data-stu-id="e388a-108">Secure LDAP port</span></span>

<span data-ttu-id="e388a-109">When secure LDAP is enabled, we recommend creating additional rules to allow inbound LDAPS access only from certain IP addresses.</span><span class="sxs-lookup"><span data-stu-id="e388a-109">When secure LDAP is enabled, we recommend creating additional rules to allow inbound LDAPS access only from certain IP addresses.</span></span> <span data-ttu-id="e388a-110">These rules protect your domain from brute force attacks that could pose a security threat.</span><span class="sxs-lookup"><span data-stu-id="e388a-110">These rules protect your domain from brute force attacks that could pose a security threat.</span></span> <span data-ttu-id="e388a-111">Port 636 allows access to your managed domain.</span><span class="sxs-lookup"><span data-stu-id="e388a-111">Port 636 allows access to your managed domain.</span></span> <span data-ttu-id="e388a-112">Here is how to update your NSG to allow access for Secure LDAP:</span><span class="sxs-lookup"><span data-stu-id="e388a-112">Here is how to update your NSG to allow access for Secure LDAP:</span></span>

1. <span data-ttu-id="e388a-113">Navigate to the [Network Security Groups tab](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.Network%2FNetworkSecurityGroups) in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e388a-113">Navigate to the [Network Security Groups tab](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.Network%2FNetworkSecurityGroups) in the Azure portal</span></span>
2. <span data-ttu-id="e388a-114">Choose the NSG associated with your domain from the table.</span><span class="sxs-lookup"><span data-stu-id="e388a-114">Choose the NSG associated with your domain from the table.</span></span>
3. <span data-ttu-id="e388a-115">Click on **Inbound security rules**</span><span class="sxs-lookup"><span data-stu-id="e388a-115">Click on **Inbound security rules**</span></span>
4. <span data-ttu-id="e388a-116">Create the port 636 rule</span><span class="sxs-lookup"><span data-stu-id="e388a-116">Create the port 636 rule</span></span>
   1. <span data-ttu-id="e388a-117">Click **Add** on the top navigation bar.</span><span class="sxs-lookup"><span data-stu-id="e388a-117">Click **Add** on the top navigation bar.</span></span>
   2. <span data-ttu-id="e388a-118">Choose **IP Addresses** for the source.</span><span class="sxs-lookup"><span data-stu-id="e388a-118">Choose **IP Addresses** for the source.</span></span>
   3. <span data-ttu-id="e388a-119">Specify the Source port ranges for this rule.</span><span class="sxs-lookup"><span data-stu-id="e388a-119">Specify the Source port ranges for this rule.</span></span>
   4. <span data-ttu-id="e388a-120">Input "636" for Destination port ranges.</span><span class="sxs-lookup"><span data-stu-id="e388a-120">Input "636" for Destination port ranges.</span></span>
   5. <span data-ttu-id="e388a-121">Protocol is **TCP**.</span><span class="sxs-lookup"><span data-stu-id="e388a-121">Protocol is **TCP**.</span></span>
   6. <span data-ttu-id="e388a-122">Give the rule an appropriate name, description, and priority.</span><span class="sxs-lookup"><span data-stu-id="e388a-122">Give the rule an appropriate name, description, and priority.</span></span> <span data-ttu-id="e388a-123">This rule's priority should be higher than your "Deny all" rule's priority, if you have one.</span><span class="sxs-lookup"><span data-stu-id="e388a-123">This rule's priority should be higher than your "Deny all" rule's priority, if you have one.</span></span>
   7. <span data-ttu-id="e388a-124">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="e388a-124">Click **OK**.</span></span>
5. <span data-ttu-id="e388a-125">Verify that your rule has been created.</span><span class="sxs-lookup"><span data-stu-id="e388a-125">Verify that your rule has been created.</span></span>
6. <span data-ttu-id="e388a-126">Check your domain's health in two hours to ensure that you have completed the steps correctly.</span><span class="sxs-lookup"><span data-stu-id="e388a-126">Check your domain's health in two hours to ensure that you have completed the steps correctly.</span></span>

> [!TIP]
> <span data-ttu-id="e388a-127">Port 636 is not the only rule needed for Azure AD Domain Services to run smoothly.</span><span class="sxs-lookup"><span data-stu-id="e388a-127">Port 636 is not the only rule needed for Azure AD Domain Services to run smoothly.</span></span> <span data-ttu-id="e388a-128">To learn more, visit the [Networking guidelines](active-directory-ds-networking.md) or [Troubleshoot NSG configuration](active-directory-ds-troubleshoot-nsg.md) articles.</span><span class="sxs-lookup"><span data-stu-id="e388a-128">To learn more, visit the [Networking guidelines](active-directory-ds-networking.md) or [Troubleshoot NSG configuration](active-directory-ds-troubleshoot-nsg.md) articles.</span></span>
>

## <a name="aadds502-secure-ldap-certificate-expiring"></a><span data-ttu-id="e388a-129">AADDS502: Secure LDAP certificate expiring</span><span class="sxs-lookup"><span data-stu-id="e388a-129">AADDS502: Secure LDAP certificate expiring</span></span>

<span data-ttu-id="e388a-130">**Alert message:**</span><span class="sxs-lookup"><span data-stu-id="e388a-130">**Alert message:**</span></span>

<span data-ttu-id="e388a-131">*The secure LDAP certificate for the managed domain will expire on [date]].*</span><span class="sxs-lookup"><span data-stu-id="e388a-131">*The secure LDAP certificate for the managed domain will expire on [date]].*</span></span>

<span data-ttu-id="e388a-132">**Resolution:**</span><span class="sxs-lookup"><span data-stu-id="e388a-132">**Resolution:**</span></span>

<span data-ttu-id="e388a-133">Create a new secure LDAP certificate by following the steps outlined in the [Configure secure LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md) article.</span><span class="sxs-lookup"><span data-stu-id="e388a-133">Create a new secure LDAP certificate by following the steps outlined in the [Configure secure LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md) article.</span></span>

## <a name="contact-us"></a><span data-ttu-id="e388a-134">Contact us</span><span class="sxs-lookup"><span data-stu-id="e388a-134">Contact us</span></span>
<span data-ttu-id="e388a-135">Contact the Azure Active Directory Domain Services product team to [share feedback or for support](active-directory-ds-contact-us.md).</span><span class="sxs-lookup"><span data-stu-id="e388a-135">Contact the Azure Active Directory Domain Services product team to [share feedback or for support](active-directory-ds-contact-us.md).</span></span>
