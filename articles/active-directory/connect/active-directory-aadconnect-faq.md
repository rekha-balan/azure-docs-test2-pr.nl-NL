---
title: 'Azure Active Directory Connect: FAQ - | Microsoft Docs'
description: This page has frequently asked questions about Azure AD Connect.
services: active-directory
documentationcenter: ''
author: billmath
manager: femila
ms.assetid: 4e47a087-ebcd-4b63-9574-0c31907a39a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: billmath
ms.openlocfilehash: 27cc51d3f9220756fc1188f978dc158f17037bc3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552710"
---
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a><span data-ttu-id="83530-103">Frequently asked questions for Azure Active Directory Connect</span><span class="sxs-lookup"><span data-stu-id="83530-103">Frequently asked questions for Azure Active Directory Connect</span></span>

## <a name="general-installation"></a><span data-ttu-id="83530-104">General installation</span><span class="sxs-lookup"><span data-stu-id="83530-104">General installation</span></span>
<span data-ttu-id="83530-105">**Q: Will installation work if the Azure AD Global Admin has 2FA enabled?**</span><span class="sxs-lookup"><span data-stu-id="83530-105">**Q: Will installation work if the Azure AD Global Admin has 2FA enabled?**</span></span>  
<span data-ttu-id="83530-106">With the builds from February 2016, this is supported.</span><span class="sxs-lookup"><span data-stu-id="83530-106">With the builds from February 2016, this is supported.</span></span>

<span data-ttu-id="83530-107">**Q: Is there a way to install Azure AD Connect unattended?**</span><span class="sxs-lookup"><span data-stu-id="83530-107">**Q: Is there a way to install Azure AD Connect unattended?**</span></span>  
<span data-ttu-id="83530-108">It is only supported to install Azure AD Connect using the installation wizard.</span><span class="sxs-lookup"><span data-stu-id="83530-108">It is only supported to install Azure AD Connect using the installation wizard.</span></span> <span data-ttu-id="83530-109">An unattended and silent installation is not supported.</span><span class="sxs-lookup"><span data-stu-id="83530-109">An unattended and silent installation is not supported.</span></span>

<span data-ttu-id="83530-110">**Q: I have a forest where one domain cannot be contacted. How do I install Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="83530-110">**Q: I have a forest where one domain cannot be contacted. How do I install Azure AD Connect?**</span></span>  
<span data-ttu-id="83530-111">With the builds from February 2016, this is supported.</span><span class="sxs-lookup"><span data-stu-id="83530-111">With the builds from February 2016, this is supported.</span></span>

<span data-ttu-id="83530-112">**Q: Does the AD DS health agent work on server core?**</span><span class="sxs-lookup"><span data-stu-id="83530-112">**Q: Does the AD DS health agent work on server core?**</span></span>  
<span data-ttu-id="83530-113">Yes.</span><span class="sxs-lookup"><span data-stu-id="83530-113">Yes.</span></span> <span data-ttu-id="83530-114">After installing the agent, you can complete the registration process using the following PowerShell commandlet:</span><span class="sxs-lookup"><span data-stu-id="83530-114">After installing the agent, you can complete the registration process using the following PowerShell commandlet:</span></span> 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a><span data-ttu-id="83530-115">Network</span><span class="sxs-lookup"><span data-stu-id="83530-115">Network</span></span>
<span data-ttu-id="83530-116">**Q: I have a firewall, network device, or something else that limits the maximum time connections can stay open on my network. How long should my client side timeout threshold be when using Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="83530-116">**Q: I have a firewall, network device, or something else that limits the maximum time connections can stay open on my network. How long should my client side timeout threshold be when using Azure AD Connect?**</span></span>  
<span data-ttu-id="83530-117">All networking software, physical devices, or anything else that limits the maximum time connections can remain open should use a threshold of at least 5 minutes (300 seconds) for connectivity between the server where the Azure AD Connect client is installed and Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="83530-117">All networking software, physical devices, or anything else that limits the maximum time connections can remain open should use a threshold of at least 5 minutes (300 seconds) for connectivity between the server where the Azure AD Connect client is installed and Azure Active Directory.</span></span> <span data-ttu-id="83530-118">This also applies to all previously released Microsoft Identity synchronization tools.</span><span class="sxs-lookup"><span data-stu-id="83530-118">This also applies to all previously released Microsoft Identity synchronization tools.</span></span>

<span data-ttu-id="83530-119">**Q: Are SLDs (Single Label Domains) supported?**</span><span class="sxs-lookup"><span data-stu-id="83530-119">**Q: Are SLDs (Single Label Domains) supported?**</span></span>  
<span data-ttu-id="83530-120">No, Azure AD Connect does not support on-premises forests/domains using SLDs.</span><span class="sxs-lookup"><span data-stu-id="83530-120">No, Azure AD Connect does not support on-premises forests/domains using SLDs.</span></span>

<span data-ttu-id="83530-121">**Q: Are "dotted" NetBios named supported?**</span><span class="sxs-lookup"><span data-stu-id="83530-121">**Q: Are "dotted" NetBios named supported?**</span></span>  
<span data-ttu-id="83530-122">No, Azure AD Connect does not support on-premises forests/domains where the NetBios name contains a period "." in the name.</span><span class="sxs-lookup"><span data-stu-id="83530-122">No, Azure AD Connect does not support on-premises forests/domains where the NetBios name contains a period "." in the name.</span></span>

## <a name="federation"></a><span data-ttu-id="83530-123">Federation</span><span class="sxs-lookup"><span data-stu-id="83530-123">Federation</span></span>
<span data-ttu-id="83530-124">**Q: What do I do if I receive an email that asking me to renew my Office 365 certificate**</span><span class="sxs-lookup"><span data-stu-id="83530-124">**Q: What do I do if I receive an email that asking me to renew my Office 365 certificate**</span></span>  
<span data-ttu-id="83530-125">Use the guidance that is outlined in the [renew certificates](active-directory-aadconnect-o365-certs.md) topic on how to renew the certificate.</span><span class="sxs-lookup"><span data-stu-id="83530-125">Use the guidance that is outlined in the [renew certificates](active-directory-aadconnect-o365-certs.md) topic on how to renew the certificate.</span></span>

<span data-ttu-id="83530-126">**Q: I have "Automatically update relying party" set for O365 relying party. Do I have to take any action when my token signing certificate automatically rolls over?**</span><span class="sxs-lookup"><span data-stu-id="83530-126">**Q: I have "Automatically update relying party" set for O365 relying party. Do I have to take any action when my token signing certificate automatically rolls over?**</span></span>  
<span data-ttu-id="83530-127">Use the guidance that is outlined in the article [renew certificates](active-directory-aadconnect-o365-certs.md).</span><span class="sxs-lookup"><span data-stu-id="83530-127">Use the guidance that is outlined in the article [renew certificates](active-directory-aadconnect-o365-certs.md).</span></span>

## <a name="environment"></a><span data-ttu-id="83530-128">Environment</span><span class="sxs-lookup"><span data-stu-id="83530-128">Environment</span></span>
<span data-ttu-id="83530-129">**Q: Is it supported to rename the server after Azure AD Connect has been installed?**</span><span class="sxs-lookup"><span data-stu-id="83530-129">**Q: Is it supported to rename the server after Azure AD Connect has been installed?**</span></span>  
<span data-ttu-id="83530-130">No.</span><span class="sxs-lookup"><span data-stu-id="83530-130">No.</span></span> <span data-ttu-id="83530-131">Changing the server name will cause the sync engine to not be able to connect to the SQL database and the service will not be able to start.</span><span class="sxs-lookup"><span data-stu-id="83530-131">Changing the server name will cause the sync engine to not be able to connect to the SQL database and the service will not be able to start.</span></span>

## <a name="identity-data"></a><span data-ttu-id="83530-132">Identity data</span><span class="sxs-lookup"><span data-stu-id="83530-132">Identity data</span></span>
<span data-ttu-id="83530-133">**Q: The UPN (userPrincipalName) attribute in Azure AD does not match the on-prem UPN - why?**</span><span class="sxs-lookup"><span data-stu-id="83530-133">**Q: The UPN (userPrincipalName) attribute in Azure AD does not match the on-prem UPN - why?**</span></span>  
<span data-ttu-id="83530-134">See these articles:</span><span class="sxs-lookup"><span data-stu-id="83530-134">See these articles:</span></span>

* [<span data-ttu-id="83530-135">User names in Office 365, Azure, or Intune don't match the on-premises UPN or alternate login ID</span><span class="sxs-lookup"><span data-stu-id="83530-135">User names in Office 365, Azure, or Intune don't match the on-premises UPN or alternate login ID</span></span>](https://support.microsoft.com/en-us/kb/2523192)
* [<span data-ttu-id="83530-136">Changes aren't synced by the Azure Active Directory Sync tool after you change the UPN of a user account to use a different federated domain</span><span class="sxs-lookup"><span data-stu-id="83530-136">Changes aren't synced by the Azure Active Directory Sync tool after you change the UPN of a user account to use a different federated domain</span></span>](https://support.microsoft.com/en-us/kb/2669550)

<span data-ttu-id="83530-137">You can also configure Azure AD to allow the sync engine to update the userPrincipalName as described in [Azure AD Connect sync service features](active-directory-aadconnectsyncservice-features.md).</span><span class="sxs-lookup"><span data-stu-id="83530-137">You can also configure Azure AD to allow the sync engine to update the userPrincipalName as described in [Azure AD Connect sync service features](active-directory-aadconnectsyncservice-features.md).</span></span>

<span data-ttu-id="83530-138">**Q: Is it supported to soft match on-premises AD Group/Contact objects with existing Azure AD Group/Contact objects?**</span><span class="sxs-lookup"><span data-stu-id="83530-138">**Q: Is it supported to soft match on-premises AD Group/Contact objects with existing Azure AD Group/Contact objects?**</span></span>  
<span data-ttu-id="83530-139">No, this is currently not supported.</span><span class="sxs-lookup"><span data-stu-id="83530-139">No, this is currently not supported.</span></span>

<span data-ttu-id="83530-140">**Q: Is it supported to manually set ImmutableId attribute on existing Azure AD Group/Contact objects to hard match it to on-premises AD Group/Contact objects?**</span><span class="sxs-lookup"><span data-stu-id="83530-140">**Q: Is it supported to manually set ImmutableId attribute on existing Azure AD Group/Contact objects to hard match it to on-premises AD Group/Contact objects?**</span></span>  
<span data-ttu-id="83530-141">No, this is currently not supported.</span><span class="sxs-lookup"><span data-stu-id="83530-141">No, this is currently not supported.</span></span>



## <a name="custom-configuration"></a><span data-ttu-id="83530-142">Custom configuration</span><span class="sxs-lookup"><span data-stu-id="83530-142">Custom configuration</span></span>
<span data-ttu-id="83530-143">**Q: Where are the PowerShell cmdlets for Azure AD Connect documented?**</span><span class="sxs-lookup"><span data-stu-id="83530-143">**Q: Where are the PowerShell cmdlets for Azure AD Connect documented?**</span></span>  
<span data-ttu-id="83530-144">With the exception of the cmdlets documented on this site, other PowerShell cmdlets found in Azure AD Connect are not supported for customer use.</span><span class="sxs-lookup"><span data-stu-id="83530-144">With the exception of the cmdlets documented on this site, other PowerShell cmdlets found in Azure AD Connect are not supported for customer use.</span></span>

<span data-ttu-id="83530-145">**Q: Can I use "Server export/server import" found in *Synchronization Service Manager* to move configuration between servers?**</span><span class="sxs-lookup"><span data-stu-id="83530-145">**Q: Can I use "Server export/server import" found in *Synchronization Service Manager* to move configuration between servers?**</span></span>  
<span data-ttu-id="83530-146">No.</span><span class="sxs-lookup"><span data-stu-id="83530-146">No.</span></span> <span data-ttu-id="83530-147">This option will not retrieve all configuration settings and should not be used.</span><span class="sxs-lookup"><span data-stu-id="83530-147">This option will not retrieve all configuration settings and should not be used.</span></span> <span data-ttu-id="83530-148">You should instead use the wizard to create the base configuration on the second server and use the sync rule editor to generate PowerShell scripts to move any custom rule between servers.</span><span class="sxs-lookup"><span data-stu-id="83530-148">You should instead use the wizard to create the base configuration on the second server and use the sync rule editor to generate PowerShell scripts to move any custom rule between servers.</span></span> <span data-ttu-id="83530-149">See [Swing migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="83530-149">See [Swing migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span>

<span data-ttu-id="83530-150">**Q: Can passwords be cached for the Azure sign-in page and can this be prevented since it contains a password input element with the autocomplete = "false" attribute?**</span><span class="sxs-lookup"><span data-stu-id="83530-150">**Q: Can passwords be cached for the Azure sign-in page and can this be prevented since it contains a password input element with the autocomplete = "false" attribute?**</span></span></br>
<span data-ttu-id="83530-151">We currently do not support modifying the HTML attributes of the Password input field, including the autocomplete tag.</span><span class="sxs-lookup"><span data-stu-id="83530-151">We currently do not support modifying the HTML attributes of the Password input field, including the autocomplete tag.</span></span> <span data-ttu-id="83530-152">We are currently working on a feature that will allow for custom Javascript which will allow you to add any attribute to the password field.</span><span class="sxs-lookup"><span data-stu-id="83530-152">We are currently working on a feature that will allow for custom Javascript which will allow you to add any attribute to the password field.</span></span> <span data-ttu-id="83530-153">This should be available later part of 2017.</span><span class="sxs-lookup"><span data-stu-id="83530-153">This should be available later part of 2017.</span></span>

<span data-ttu-id="83530-154">**Q: On the Azure sign-in page, usernames for users who have previously signed in successfully are shown.  Can this behavior be turned off?**</span><span class="sxs-lookup"><span data-stu-id="83530-154">**Q: On the Azure sign-in page, usernames for users who have previously signed in successfully are shown.  Can this behavior be turned off?**</span></span></br>
<span data-ttu-id="83530-155">We currently do not support modifying the HTML attributes of the sign-in page.</span><span class="sxs-lookup"><span data-stu-id="83530-155">We currently do not support modifying the HTML attributes of the sign-in page.</span></span> <span data-ttu-id="83530-156">We are currently working on a feature that will allow for custom Javascript which will allow you to add any attribute to the password field.</span><span class="sxs-lookup"><span data-stu-id="83530-156">We are currently working on a feature that will allow for custom Javascript which will allow you to add any attribute to the password field.</span></span> <span data-ttu-id="83530-157">This should be available later part of 2017.</span><span class="sxs-lookup"><span data-stu-id="83530-157">This should be available later part of 2017.</span></span>

<span data-ttu-id="83530-158">**Q: Is there a way to prevent concurrent sessions?**</span><span class="sxs-lookup"><span data-stu-id="83530-158">**Q: Is there a way to prevent concurrent sessions?**</span></span></br>
<span data-ttu-id="83530-159">No.</span><span class="sxs-lookup"><span data-stu-id="83530-159">No.</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="83530-160">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="83530-160">Troubleshooting</span></span>
<span data-ttu-id="83530-161">**Q: How can I get help with Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="83530-161">**Q: How can I get help with Azure AD Connect?**</span></span>

[<span data-ttu-id="83530-162">Search the Microsoft Knowledge Base (KB)</span><span class="sxs-lookup"><span data-stu-id="83530-162">Search the Microsoft Knowledge Base (KB)</span></span>](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* <span data-ttu-id="83530-163">Search the Microsoft Knowledge Base (KB) for technical solutions to common break-fix issues about Support for Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="83530-163">Search the Microsoft Knowledge Base (KB) for technical solutions to common break-fix issues about Support for Azure AD Connect.</span></span>

[<span data-ttu-id="83530-164">Microsoft Azure Active Directory Forums</span><span class="sxs-lookup"><span data-stu-id="83530-164">Microsoft Azure Active Directory Forums</span></span>](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* <span data-ttu-id="83530-165">You can search and browse for technical questions and answers from the community or ask your own question by clicking [here](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span><span class="sxs-lookup"><span data-stu-id="83530-165">You can search and browse for technical questions and answers from the community or ask your own question by clicking [here](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span></span>

[<span data-ttu-id="83530-166">Azure AD Connect customer support</span><span class="sxs-lookup"><span data-stu-id="83530-166">Azure AD Connect customer support</span></span>](https://manage.windowsazure.com/?getsupport=true)

* <span data-ttu-id="83530-167">Use this link to get support through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="83530-167">Use this link to get support through the Azure portal.</span></span>

