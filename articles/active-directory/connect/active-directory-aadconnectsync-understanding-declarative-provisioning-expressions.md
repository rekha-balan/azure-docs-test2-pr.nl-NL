---
title: 'Azure AD Connect: Declarative Provisioning Expressions | Microsoft Docs'
description: Explains the declarative provisioning expressions.
services: active-directory
documentationcenter: ''
author: andkjell
manager: femila
editor: ''
ms.assetid: e3ea53c8-3801-4acf-a297-0fb9bb1bf11d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: markvi;andkjell
ms.openlocfilehash: 58908d65fdebd651e5cfab2b668574bdf7ab6085
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662435"
---
# <a name="azure-ad-connect-sync-understanding-declarative-provisioning-expressions"></a><span data-ttu-id="e4ef1-103">Azure AD Connect sync: Understanding Declarative Provisioning Expressions</span><span class="sxs-lookup"><span data-stu-id="e4ef1-103">Azure AD Connect sync: Understanding Declarative Provisioning Expressions</span></span>
<span data-ttu-id="e4ef1-104">Azure AD Connect sync builds on declarative provisioning first introduced in Forefront Identity Manager 2010.</span><span class="sxs-lookup"><span data-stu-id="e4ef1-104">Azure AD Connect sync builds on declarative provisioning first introduced in Forefront Identity Manager 2010.</span></span> <span data-ttu-id="e4ef1-105">It allows you to implement your complete identity integration business logic without the need to write compiled code.</span><span class="sxs-lookup"><span data-stu-id="e4ef1-105">It allows you to implement your complete identity integration business logic without the need to write compiled code.</span></span>

<span data-ttu-id="e4ef1-106">An essential part of declarative provisioning is the expression language used in attribute flows.</span><span class="sxs-lookup"><span data-stu-id="e4ef1-106">An essential part of declarative provisioning is the expression language used in attribute flows.</span></span> <span data-ttu-id="e4ef1-107">The language used is a subset of Microsoft® Visual Basic® for Applications (VBA).</span><span class="sxs-lookup"><span data-stu-id="e4ef1-107">The language used is a subset of Microsoft® Visual Basic® for Applications (VBA).</span></span> <span data-ttu-id="e4ef1-108">This language is used in Microsoft Office and users with experience of VBScript will also recognize it.</span><span class="sxs-lookup"><span data-stu-id="e4ef1-108">This language is used in Microsoft Office and users with experience of VBScript will also recognize it.</span></span> <span data-ttu-id="e4ef1-109">The Declarative Provisioning Expression Language is only using functions and is not a structured language.</span><span class="sxs-lookup"><span data-stu-id="e4ef1-109">The Declarative Provisioning Expression Language is only using functions and is not a structured language.</span></span> <span data-ttu-id="e4ef1-110">There are no methods or statements.</span><span class="sxs-lookup"><span data-stu-id="e4ef1-110">There are no methods or statements.</span></span> <span data-ttu-id="e4ef1-111">Functions are instead nested to express program flow.</span><span class="sxs-lookup"><span data-stu-id="e4ef1-111">Functions are instead nested to express program flow.</span></span>

<span data-ttu-id="e4ef1-112">For more details, see [Welcome to the Visual Basic for Applications language reference for Office 2013](https://msdn.microsoft.com/library/gg264383.aspx).</span><span class="sxs-lookup"><span data-stu-id="e4ef1-112">For more details, see [Welcome to the Visual Basic for Applications language reference for Office 2013](https://msdn.microsoft.com/library/gg264383.aspx).</span></span>

<span data-ttu-id="e4ef1-113">The attributes are strongly typed.</span><span class="sxs-lookup"><span data-stu-id="e4ef1-113">The attributes are strongly typed.</span></span> <span data-ttu-id="e4ef1-114">A function only accepts attributes of the correct type.</span><span class="sxs-lookup"><span data-stu-id="e4ef1-114">A function only accepts attributes of the correct type.</span></span> <span data-ttu-id="e4ef1-115">It is also case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="e4ef1-115">It is also case-sensitive.</span></span> <span data-ttu-id="e4ef1-116">Both function names and attribute names must have proper casing or an error is thrown.</span><span class="sxs-lookup"><span data-stu-id="e4ef1-116">Both function names and attribute names must have proper casing or an error is thrown.</span></span>

## <a name="language-definitions-and-identifiers"></a><span data-ttu-id="e4ef1-117">Language definitions and Identifiers</span><span class="sxs-lookup"><span data-stu-id="e4ef1-117">Language definitions and Identifiers</span></span>
* <span data-ttu-id="e4ef1-118">Functions have a name followed by arguments in brackets: FunctionName(argument 1, argument N).</span><span class="sxs-lookup"><span data-stu-id="e4ef1-118">Functions have a name followed by arguments in brackets: FunctionName(argument 1, argument N).</span></span>
* <span data-ttu-id="e4ef1-119">Attributes are identified by square brackets: [attributeName]</span><span class="sxs-lookup"><span data-stu-id="e4ef1-119">Attributes are identified by square brackets: [attributeName]</span></span>
* <span data-ttu-id="e4ef1-120">Parameters are identified by percent signs: %ParameterName%</span><span class="sxs-lookup"><span data-stu-id="e4ef1-120">Parameters are identified by percent signs: %ParameterName%</span></span>
* <span data-ttu-id="e4ef1-121">String constants are surrounded by quotes: For example, "Contoso" (Note: must use straight quotes "" and not smart quotes “”)</span><span class="sxs-lookup"><span data-stu-id="e4ef1-121">String constants are surrounded by quotes: For example, "Contoso" (Note: must use straight quotes "" and not smart quotes “”)</span></span>
* <span data-ttu-id="e4ef1-122">Numeric values are expressed without quotes and expected to be decimal.</span><span class="sxs-lookup"><span data-stu-id="e4ef1-122">Numeric values are expressed without quotes and expected to be decimal.</span></span> <span data-ttu-id="e4ef1-123">Hexadecimal values are prefixed with &H.</span><span class="sxs-lookup"><span data-stu-id="e4ef1-123">Hexadecimal values are prefixed with &H.</span></span> <span data-ttu-id="e4ef1-124">For example, 98052, &HFF</span><span class="sxs-lookup"><span data-stu-id="e4ef1-124">For example, 98052, &HFF</span></span>
* <span data-ttu-id="e4ef1-125">Boolean values are expressed with constants: True, False.</span><span class="sxs-lookup"><span data-stu-id="e4ef1-125">Boolean values are expressed with constants: True, False.</span></span>
* <span data-ttu-id="e4ef1-126">Built-in constants and literals are expressed with only their name: NULL, CRLF, IgnoreThisFlow</span><span class="sxs-lookup"><span data-stu-id="e4ef1-126">Built-in constants and literals are expressed with only their name: NULL, CRLF, IgnoreThisFlow</span></span>

### <a name="functions"></a><span data-ttu-id="e4ef1-127">Functions</span><span class="sxs-lookup"><span data-stu-id="e4ef1-127">Functions</span></span>
<span data-ttu-id="e4ef1-128">Declarative provisioning uses many functions to enable the possibility to transform attribute values.</span><span class="sxs-lookup"><span data-stu-id="e4ef1-128">Declarative provisioning uses many functions to enable the possibility to transform attribute values.</span></span> <span data-ttu-id="e4ef1-129">These functions can be nested so the result from one function is passed in to another function.</span><span class="sxs-lookup"><span data-stu-id="e4ef1-129">These functions can be nested so the result from one function is passed in to another function.</span></span>

`Function1(Function2(Function3()))`

<span data-ttu-id="e4ef1-130">The complete list of functions can be found in the [function reference](active-directory-aadconnectsync-functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="e4ef1-130">The complete list of functions can be found in the [function reference](active-directory-aadconnectsync-functions-reference.md).</span></span>

### <a name="parameters"></a><span data-ttu-id="e4ef1-131">Parameters</span><span class="sxs-lookup"><span data-stu-id="e4ef1-131">Parameters</span></span>
<span data-ttu-id="e4ef1-132">A parameter is defined either by a Connector or by an administrator using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e4ef1-132">A parameter is defined either by a Connector or by an administrator using PowerShell.</span></span> <span data-ttu-id="e4ef1-133">Parameters usually contain values that are different from system to system, for example the name of the domain the user is located in.</span><span class="sxs-lookup"><span data-stu-id="e4ef1-133">Parameters usually contain values that are different from system to system, for example the name of the domain the user is located in.</span></span> <span data-ttu-id="e4ef1-134">These parameters can be used in attribute flows.</span><span class="sxs-lookup"><span data-stu-id="e4ef1-134">These parameters can be used in attribute flows.</span></span>

<span data-ttu-id="e4ef1-135">The Active Directory Connector provided the following parameters for inbound Synchronization Rules:</span><span class="sxs-lookup"><span data-stu-id="e4ef1-135">The Active Directory Connector provided the following parameters for inbound Synchronization Rules:</span></span>

| <span data-ttu-id="e4ef1-136">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="e4ef1-136">Parameter Name</span></span> | <span data-ttu-id="e4ef1-137">Comment</span><span class="sxs-lookup"><span data-stu-id="e4ef1-137">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="e4ef1-138">Domain.Netbios</span><span class="sxs-lookup"><span data-stu-id="e4ef1-138">Domain.Netbios</span></span> |<span data-ttu-id="e4ef1-139">Netbios format of the domain currently being imported, for example FABRIKAMSALES</span><span class="sxs-lookup"><span data-stu-id="e4ef1-139">Netbios format of the domain currently being imported, for example FABRIKAMSALES</span></span> |
| <span data-ttu-id="e4ef1-140">Domain.FQDN</span><span class="sxs-lookup"><span data-stu-id="e4ef1-140">Domain.FQDN</span></span> |<span data-ttu-id="e4ef1-141">FQDN format of the domain currently being imported, for example sales.fabrikam.com</span><span class="sxs-lookup"><span data-stu-id="e4ef1-141">FQDN format of the domain currently being imported, for example sales.fabrikam.com</span></span> |
| <span data-ttu-id="e4ef1-142">Domain.LDAP</span><span class="sxs-lookup"><span data-stu-id="e4ef1-142">Domain.LDAP</span></span> |<span data-ttu-id="e4ef1-143">LDAP format of the domain currently being imported, for example DC=sales,DC=fabrikam,DC=com</span><span class="sxs-lookup"><span data-stu-id="e4ef1-143">LDAP format of the domain currently being imported, for example DC=sales,DC=fabrikam,DC=com</span></span> |
| <span data-ttu-id="e4ef1-144">Forest.Netbios</span><span class="sxs-lookup"><span data-stu-id="e4ef1-144">Forest.Netbios</span></span> |<span data-ttu-id="e4ef1-145">Netbios format of the forest name currently being imported, for example FABRIKAMCORP</span><span class="sxs-lookup"><span data-stu-id="e4ef1-145">Netbios format of the forest name currently being imported, for example FABRIKAMCORP</span></span> |
| <span data-ttu-id="e4ef1-146">Forest.FQDN</span><span class="sxs-lookup"><span data-stu-id="e4ef1-146">Forest.FQDN</span></span> |<span data-ttu-id="e4ef1-147">FQDN format of the forest name currently being imported, for example fabrikam.com</span><span class="sxs-lookup"><span data-stu-id="e4ef1-147">FQDN format of the forest name currently being imported, for example fabrikam.com</span></span> |
| <span data-ttu-id="e4ef1-148">Forest.LDAP</span><span class="sxs-lookup"><span data-stu-id="e4ef1-148">Forest.LDAP</span></span> |<span data-ttu-id="e4ef1-149">LDAP format of the forest name currently being imported, for example DC=fabrikam,DC=com</span><span class="sxs-lookup"><span data-stu-id="e4ef1-149">LDAP format of the forest name currently being imported, for example DC=fabrikam,DC=com</span></span> |

<span data-ttu-id="e4ef1-150">The system provides the following parameter, which is used to get the identifier of the Connector currently running:</span><span class="sxs-lookup"><span data-stu-id="e4ef1-150">The system provides the following parameter, which is used to get the identifier of the Connector currently running:</span></span>  
`Connector.ID`

<span data-ttu-id="e4ef1-151">Here is an example that populates the metaverse attribute domain with the netbios name of the domain where the user is located:</span><span class="sxs-lookup"><span data-stu-id="e4ef1-151">Here is an example that populates the metaverse attribute domain with the netbios name of the domain where the user is located:</span></span>  
`domain` <- `%Domain.Netbios%`

### <a name="operators"></a><span data-ttu-id="e4ef1-152">Operators</span><span class="sxs-lookup"><span data-stu-id="e4ef1-152">Operators</span></span>
<span data-ttu-id="e4ef1-153">The following operators can be used:</span><span class="sxs-lookup"><span data-stu-id="e4ef1-153">The following operators can be used:</span></span>

* <span data-ttu-id="e4ef1-154">**Comparison**: <, <=, <>, =, >, >=</span><span class="sxs-lookup"><span data-stu-id="e4ef1-154">**Comparison**: <, <=, <>, =, >, >=</span></span>
* <span data-ttu-id="e4ef1-155">**Mathematics**: +, -, \*, -</span><span class="sxs-lookup"><span data-stu-id="e4ef1-155">**Mathematics**: +, -, \*, -</span></span>
* <span data-ttu-id="e4ef1-156">**String**: & (concatenate)</span><span class="sxs-lookup"><span data-stu-id="e4ef1-156">**String**: & (concatenate)</span></span>
* <span data-ttu-id="e4ef1-157">**Logical**: && (and), || (or)</span><span class="sxs-lookup"><span data-stu-id="e4ef1-157">**Logical**: && (and), || (or)</span></span>
* <span data-ttu-id="e4ef1-158">**Evaluation order**: ( )</span><span class="sxs-lookup"><span data-stu-id="e4ef1-158">**Evaluation order**: ( )</span></span>

<span data-ttu-id="e4ef1-159">Operators are evaluated left to right and have the same evaluation priority.</span><span class="sxs-lookup"><span data-stu-id="e4ef1-159">Operators are evaluated left to right and have the same evaluation priority.</span></span> <span data-ttu-id="e4ef1-160">That is, the \* (multiplier) is not evaluated before - (subtraction).</span><span class="sxs-lookup"><span data-stu-id="e4ef1-160">That is, the \* (multiplier) is not evaluated before - (subtraction).</span></span> <span data-ttu-id="e4ef1-161">2\*(5+3) is not the same as 2\*5+3.</span><span class="sxs-lookup"><span data-stu-id="e4ef1-161">2\*(5+3) is not the same as 2\*5+3.</span></span> <span data-ttu-id="e4ef1-162">The brackets ( ) are used to change the evaluation order when left to right evaluation order isn't appropriate.</span><span class="sxs-lookup"><span data-stu-id="e4ef1-162">The brackets ( ) are used to change the evaluation order when left to right evaluation order isn't appropriate.</span></span>

## <a name="multi-valued-attributes"></a><span data-ttu-id="e4ef1-163">Multi-valued attributes</span><span class="sxs-lookup"><span data-stu-id="e4ef1-163">Multi-valued attributes</span></span>
<span data-ttu-id="e4ef1-164">The functions can operate on both single-valued and multi-valued attributes.</span><span class="sxs-lookup"><span data-stu-id="e4ef1-164">The functions can operate on both single-valued and multi-valued attributes.</span></span> <span data-ttu-id="e4ef1-165">For multi-valued attributes, the function operates over every value and applies the same function to every value.</span><span class="sxs-lookup"><span data-stu-id="e4ef1-165">For multi-valued attributes, the function operates over every value and applies the same function to every value.</span></span>

<span data-ttu-id="e4ef1-166">For example:</span><span class="sxs-lookup"><span data-stu-id="e4ef1-166">For example:</span></span>  
<span data-ttu-id="e4ef1-167">`Trim([proxyAddresses])` Do a Trim of every value in the proxyAddress attribute.</span><span class="sxs-lookup"><span data-stu-id="e4ef1-167">`Trim([proxyAddresses])` Do a Trim of every value in the proxyAddress attribute.</span></span>  
<span data-ttu-id="e4ef1-168">`Word([proxyAddresses],1,"@") & "@contoso.com"` For every value with an @-sign, replace the domain with @contoso.com.</span><span class="sxs-lookup"><span data-stu-id="e4ef1-168">`Word([proxyAddresses],1,"@") & "@contoso.com"` For every value with an @-sign, replace the domain with @contoso.com.</span></span>  
<span data-ttu-id="e4ef1-169">`IIF(InStr([proxyAddresses],"SIP:")=1,NULL,[proxyAddresses])` Look for the SIP-address and remove it from the values.</span><span class="sxs-lookup"><span data-stu-id="e4ef1-169">`IIF(InStr([proxyAddresses],"SIP:")=1,NULL,[proxyAddresses])` Look for the SIP-address and remove it from the values.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4ef1-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="e4ef1-170">Next steps</span></span>
* <span data-ttu-id="e4ef1-171">Read more about the configuration model in [Understanding Declarative Provisioning](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="e4ef1-171">Read more about the configuration model in [Understanding Declarative Provisioning](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span></span>
* <span data-ttu-id="e4ef1-172">See how declarative provisioning is used out-of-box in [Understanding the default configuration](active-directory-aadconnectsync-understanding-default-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="e4ef1-172">See how declarative provisioning is used out-of-box in [Understanding the default configuration](active-directory-aadconnectsync-understanding-default-configuration.md).</span></span>
* <span data-ttu-id="e4ef1-173">See how to make a practical change using declarative provisioning in [How to make a change to the default configuration](active-directory-aadconnectsync-change-the-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="e4ef1-173">See how to make a practical change using declarative provisioning in [How to make a change to the default configuration](active-directory-aadconnectsync-change-the-configuration.md).</span></span>

<span data-ttu-id="e4ef1-174">**Overview topics**</span><span class="sxs-lookup"><span data-stu-id="e4ef1-174">**Overview topics**</span></span>

* [<span data-ttu-id="e4ef1-175">Azure AD Connect sync: Understand and customize synchronization</span><span class="sxs-lookup"><span data-stu-id="e4ef1-175">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="e4ef1-176">Integrating your on-premises identities with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e4ef1-176">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

<span data-ttu-id="e4ef1-177">**Reference topics**</span><span class="sxs-lookup"><span data-stu-id="e4ef1-177">**Reference topics**</span></span>

* [<span data-ttu-id="e4ef1-178">Azure AD Connect sync: Functions Reference</span><span class="sxs-lookup"><span data-stu-id="e4ef1-178">Azure AD Connect sync: Functions Reference</span></span>](active-directory-aadconnectsync-functions-reference.md)

