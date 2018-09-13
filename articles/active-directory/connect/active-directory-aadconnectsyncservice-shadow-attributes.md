---
title: Azure AD Connect sync service shadow attributes | Microsoft Docs
description: Describes how shadow attributes work in Azure AD Connect sync service.
services: active-directory
documentationcenter: ''
author: andkjell
manager: femila
editor: ''
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: billmath
ms.openlocfilehash: 86e8a7e4a1f457fe6a24360853494c178c4d66f9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550656"
---
# <a name="azure-ad-connect-sync-service-shadow-attributes"></a><span data-ttu-id="24825-103">Azure AD Connect sync service shadow attributes</span><span class="sxs-lookup"><span data-stu-id="24825-103">Azure AD Connect sync service shadow attributes</span></span>
<span data-ttu-id="24825-104">Most attributes are represented the same way in Azure AD as they are in your on-premises Active Directory.</span><span class="sxs-lookup"><span data-stu-id="24825-104">Most attributes are represented the same way in Azure AD as they are in your on-premises Active Directory.</span></span> <span data-ttu-id="24825-105">But some attributes have some special handling and the attribute value in Azure AD might be different than what Azure AD Connect synchronizes.</span><span class="sxs-lookup"><span data-stu-id="24825-105">But some attributes have some special handling and the attribute value in Azure AD might be different than what Azure AD Connect synchronizes.</span></span>

## <a name="introducing-shadow-attributes"></a><span data-ttu-id="24825-106">Introducing shadow attributes</span><span class="sxs-lookup"><span data-stu-id="24825-106">Introducing shadow attributes</span></span>
<span data-ttu-id="24825-107">Some attributes have two representations in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="24825-107">Some attributes have two representations in Azure AD.</span></span> <span data-ttu-id="24825-108">Both the on-premises value and a calculated value are stored.</span><span class="sxs-lookup"><span data-stu-id="24825-108">Both the on-premises value and a calculated value are stored.</span></span> <span data-ttu-id="24825-109">These extra attributes are called shadow attributes.</span><span class="sxs-lookup"><span data-stu-id="24825-109">These extra attributes are called shadow attributes.</span></span> <span data-ttu-id="24825-110">The two most common attributes where you see this behavior are **userPrincipalName** and **proxyAddress**.</span><span class="sxs-lookup"><span data-stu-id="24825-110">The two most common attributes where you see this behavior are **userPrincipalName** and **proxyAddress**.</span></span> <span data-ttu-id="24825-111">The change in attribute values happens when there are values in these attributes representing non-verified domains.</span><span class="sxs-lookup"><span data-stu-id="24825-111">The change in attribute values happens when there are values in these attributes representing non-verified domains.</span></span> <span data-ttu-id="24825-112">But the sync engine in Connect reads the value in the shadow attribute so from its perspective, the attribute has been confirmed by Azure AD.</span><span class="sxs-lookup"><span data-stu-id="24825-112">But the sync engine in Connect reads the value in the shadow attribute so from its perspective, the attribute has been confirmed by Azure AD.</span></span>

<span data-ttu-id="24825-113">You cannot see the shadow attributes using the Azure portal or with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="24825-113">You cannot see the shadow attributes using the Azure portal or with PowerShell.</span></span> <span data-ttu-id="24825-114">But understanding the concept helps you to troubleshoot certain scenarios where the attribute has different values on-premises and in the cloud.</span><span class="sxs-lookup"><span data-stu-id="24825-114">But understanding the concept helps you to troubleshoot certain scenarios where the attribute has different values on-premises and in the cloud.</span></span>

<span data-ttu-id="24825-115">To better understand the behavior, look at this example from Fabrikam:</span><span class="sxs-lookup"><span data-stu-id="24825-115">To better understand the behavior, look at this example from Fabrikam:</span></span>  
![Domains](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsyncservice-shadow-attributes/domains.png)  
<span data-ttu-id="24825-117">They have multiple UPN suffixes in their on-premises Active Directory, but they have only verified one.</span><span class="sxs-lookup"><span data-stu-id="24825-117">They have multiple UPN suffixes in their on-premises Active Directory, but they have only verified one.</span></span>

### <a name="userprincipalname"></a><span data-ttu-id="24825-118">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="24825-118">userPrincipalName</span></span>
<span data-ttu-id="24825-119">A user has the following attribute values in a non-verified domain:</span><span class="sxs-lookup"><span data-stu-id="24825-119">A user has the following attribute values in a non-verified domain:</span></span>

| <span data-ttu-id="24825-120">Attribute</span><span class="sxs-lookup"><span data-stu-id="24825-120">Attribute</span></span> | <span data-ttu-id="24825-121">Value</span><span class="sxs-lookup"><span data-stu-id="24825-121">Value</span></span> |
| --- | --- |
| <span data-ttu-id="24825-122">on-premises userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="24825-122">on-premises userPrincipalName</span></span> | lee.sperry@fabrikam.com |
| <span data-ttu-id="24825-123">Azure AD shadowUserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="24825-123">Azure AD shadowUserPrincipalName</span></span> | lee.sperry@fabrikam.com |
| <span data-ttu-id="24825-124">Azure AD userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="24825-124">Azure AD userPrincipalName</span></span> | lee.sperry@fabrikam.onmicrosoft.com |

<span data-ttu-id="24825-125">The userPrincipalName attribute is the value you see when using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="24825-125">The userPrincipalName attribute is the value you see when using PowerShell.</span></span>

<span data-ttu-id="24825-126">Since the real on-premises attribute value is stored in Azure AD, when you verify the fabrikam.com domain, Azure AD updates the userPrincipalName attribute with the value from the shadowUserPrincipalName.</span><span class="sxs-lookup"><span data-stu-id="24825-126">Since the real on-premises attribute value is stored in Azure AD, when you verify the fabrikam.com domain, Azure AD updates the userPrincipalName attribute with the value from the shadowUserPrincipalName.</span></span> <span data-ttu-id="24825-127">You do not have to synchronize any changes from Azure AD Connect for these values to be updated.</span><span class="sxs-lookup"><span data-stu-id="24825-127">You do not have to synchronize any changes from Azure AD Connect for these values to be updated.</span></span>

### <a name="proxyaddresses"></a><span data-ttu-id="24825-128">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="24825-128">proxyAddresses</span></span>
<span data-ttu-id="24825-129">The same process for only including verified domains also occurs for proxyAddresses, but with some additional logic.</span><span class="sxs-lookup"><span data-stu-id="24825-129">The same process for only including verified domains also occurs for proxyAddresses, but with some additional logic.</span></span> <span data-ttu-id="24825-130">The check for verified domains only happens for mailbox users.</span><span class="sxs-lookup"><span data-stu-id="24825-130">The check for verified domains only happens for mailbox users.</span></span> <span data-ttu-id="24825-131">A mail-enabled user or contact represent a user in another Exchange organization and you can add any values in proxyAddresses to these objects.</span><span class="sxs-lookup"><span data-stu-id="24825-131">A mail-enabled user or contact represent a user in another Exchange organization and you can add any values in proxyAddresses to these objects.</span></span>

<span data-ttu-id="24825-132">For a mailbox user, either on-premises or in Exchange Online, only values for verified domains appear.</span><span class="sxs-lookup"><span data-stu-id="24825-132">For a mailbox user, either on-premises or in Exchange Online, only values for verified domains appear.</span></span> <span data-ttu-id="24825-133">It could look like this:</span><span class="sxs-lookup"><span data-stu-id="24825-133">It could look like this:</span></span>

| <span data-ttu-id="24825-134">Attribute</span><span class="sxs-lookup"><span data-stu-id="24825-134">Attribute</span></span> | <span data-ttu-id="24825-135">Value</span><span class="sxs-lookup"><span data-stu-id="24825-135">Value</span></span> |
| --- | --- |
| <span data-ttu-id="24825-136">on-premises proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="24825-136">on-premises proxyAddresses</span></span> | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie.spencer@fabrikam.com</br>smtp:abbie@fabrikamonline.com |
| <span data-ttu-id="24825-137">Exchange Online proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="24825-137">Exchange Online proxyAddresses</span></span> | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie@fabrikamonline.com</br>SIP:abbie.spencer@fabrikamonline.com |

<span data-ttu-id="24825-138">In this case **smtp:abbie.spencer@fabrikam.com** was removed since that domain has not been verified.</span><span class="sxs-lookup"><span data-stu-id="24825-138">In this case **smtp:abbie.spencer@fabrikam.com** was removed since that domain has not been verified.</span></span> <span data-ttu-id="24825-139">But Exchange also added **SIP:abbie.spencer@fabrikamonline.com**.</span><span class="sxs-lookup"><span data-stu-id="24825-139">But Exchange also added **SIP:abbie.spencer@fabrikamonline.com**.</span></span> <span data-ttu-id="24825-140">Fabrikam has not used Lync/Skype on-premises, but Azure AD and Exchange Online prepare for it.</span><span class="sxs-lookup"><span data-stu-id="24825-140">Fabrikam has not used Lync/Skype on-premises, but Azure AD and Exchange Online prepare for it.</span></span>

<span data-ttu-id="24825-141">This logic for proxyAddresses is referred to as **ProxyCalc**.</span><span class="sxs-lookup"><span data-stu-id="24825-141">This logic for proxyAddresses is referred to as **ProxyCalc**.</span></span> <span data-ttu-id="24825-142">ProxyCalc is invoked with every change on a user when:</span><span class="sxs-lookup"><span data-stu-id="24825-142">ProxyCalc is invoked with every change on a user when:</span></span>

- <span data-ttu-id="24825-143">The user has been assigned a service plan that includes Exchange Online even if the user was not licensed for Exchange.</span><span class="sxs-lookup"><span data-stu-id="24825-143">The user has been assigned a service plan that includes Exchange Online even if the user was not licensed for Exchange.</span></span> <span data-ttu-id="24825-144">For example, if the user is assigned the Office E3 SKU, but only was assigned SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="24825-144">For example, if the user is assigned the Office E3 SKU, but only was assigned SharePoint Online.</span></span> <span data-ttu-id="24825-145">This is true even if your mailbox is still on-premises.</span><span class="sxs-lookup"><span data-stu-id="24825-145">This is true even if your mailbox is still on-premises.</span></span>
- <span data-ttu-id="24825-146">The attribute msExchRecipientTypeDetails has a value.</span><span class="sxs-lookup"><span data-stu-id="24825-146">The attribute msExchRecipientTypeDetails has a value.</span></span>
- <span data-ttu-id="24825-147">You make a change to proxyAddresses or userPrincipalName.</span><span class="sxs-lookup"><span data-stu-id="24825-147">You make a change to proxyAddresses or userPrincipalName.</span></span>

<span data-ttu-id="24825-148">ProxyCalc might take some time to process a change on a user and is not synchronous with the Azure AD Connect export process.</span><span class="sxs-lookup"><span data-stu-id="24825-148">ProxyCalc might take some time to process a change on a user and is not synchronous with the Azure AD Connect export process.</span></span>

> [!NOTE]
> <span data-ttu-id="24825-149">The ProxyCalc logic has some additional behaviors for advanced scenarios not documented in this topic.</span><span class="sxs-lookup"><span data-stu-id="24825-149">The ProxyCalc logic has some additional behaviors for advanced scenarios not documented in this topic.</span></span> <span data-ttu-id="24825-150">This topic is provided for you to understand the behavior and not document all internal logic.</span><span class="sxs-lookup"><span data-stu-id="24825-150">This topic is provided for you to understand the behavior and not document all internal logic.</span></span>

### <a name="quarantined-attribute-values"></a><span data-ttu-id="24825-151">Quarantined attribute values</span><span class="sxs-lookup"><span data-stu-id="24825-151">Quarantined attribute values</span></span>
<span data-ttu-id="24825-152">Shadow attributes are also used when there are duplicate attribute values.</span><span class="sxs-lookup"><span data-stu-id="24825-152">Shadow attributes are also used when there are duplicate attribute values.</span></span> <span data-ttu-id="24825-153">For more information, see [duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span><span class="sxs-lookup"><span data-stu-id="24825-153">For more information, see [duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="24825-154">See also</span><span class="sxs-lookup"><span data-stu-id="24825-154">See also</span></span>
* [<span data-ttu-id="24825-155">Azure AD Connect sync</span><span class="sxs-lookup"><span data-stu-id="24825-155">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="24825-156">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="24825-156">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

