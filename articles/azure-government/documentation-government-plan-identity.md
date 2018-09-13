---
title: Azure Government Identity | Microsoft Docs
description: Provides Planning Guidance for Identity in Azure Government
services: azure-government
cloud: gov
documentationcenter: ''
author: bernie-msft
manager: zakramer
ms.assetid: 1f222624-872b-4fe7-9c65-796deae03306
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 10/20/2017
ms.author: beellis
ms.openlocfilehash: 68f6db6a5d96d41a0c1eed61a79e308d43e07c6b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869900"
---
# <a name="planning-identity-for-azure-government-applications"></a><span data-ttu-id="c8ce2-103">Planning identity for Azure Government applications</span><span class="sxs-lookup"><span data-stu-id="c8ce2-103">Planning identity for Azure Government applications</span></span>

<span data-ttu-id="c8ce2-104">Microsoft Azure Government provides the same ways to build applications and manage identities as Azure Public.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-104">Microsoft Azure Government provides the same ways to build applications and manage identities as Azure Public.</span></span> <span data-ttu-id="c8ce2-105">Azure Government customers may already have an Azure Active Directory (Azure AD) Public tenant or may create a tenant in Azure AD Government.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-105">Azure Government customers may already have an Azure Active Directory (Azure AD) Public tenant or may create a tenant in Azure AD Government.</span></span> <span data-ttu-id="c8ce2-106">This article provides guidance on identity decisions based on the application and location of your identity.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-106">This article provides guidance on identity decisions based on the application and location of your identity.</span></span>

## <a name="identity-models"></a><span data-ttu-id="c8ce2-107">Identity models</span><span class="sxs-lookup"><span data-stu-id="c8ce2-107">Identity models</span></span>
<span data-ttu-id="c8ce2-108">Before determining the identity approach for your application, you need to know what identity types are available to you.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-108">Before determining the identity approach for your application, you need to know what identity types are available to you.</span></span> <span data-ttu-id="c8ce2-109">There are three types: On-Premises Identity, Cloud Identity, and Hybrid Identity.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-109">There are three types: On-Premises Identity, Cloud Identity, and Hybrid Identity.</span></span>


|<span data-ttu-id="c8ce2-110">On-Premises Identity</span><span class="sxs-lookup"><span data-stu-id="c8ce2-110">On-Premises Identity</span></span>|<span data-ttu-id="c8ce2-111">Cloud Identity</span><span class="sxs-lookup"><span data-stu-id="c8ce2-111">Cloud Identity</span></span>|<span data-ttu-id="c8ce2-112">Hybrid Identity</span><span class="sxs-lookup"><span data-stu-id="c8ce2-112">Hybrid Identity</span></span>
|---|---|---|
|<span data-ttu-id="c8ce2-113">On-Premises Identities belong to on-premises Active Directory environments that most customers use today.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-113">On-Premises Identities belong to on-premises Active Directory environments that most customers use today.</span></span>|<span data-ttu-id="c8ce2-114">Cloud identities originate, only exist, and are managed in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-114">Cloud identities originate, only exist, and are managed in Azure AD.</span></span>|<span data-ttu-id="c8ce2-115">Hybrid identities originate as on-premises identities, but become hybrid through directory synchronization to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-115">Hybrid identities originate as on-premises identities, but become hybrid through directory synchronization to Azure AD.</span></span> <span data-ttu-id="c8ce2-116">After directory synchronization they exist both on-premises and in the cloud, hence hybrid.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-116">After directory synchronization they exist both on-premises and in the cloud, hence hybrid.</span></span>|

>[!NOTE]
><span data-ttu-id="c8ce2-117">Hybrid comes with deployment options (Synchronized Identity, Federated Identity, etc.) that all rely on directory synchronization and mostly define how identities are authenticated as discussed in [Choose a Hybrid Identity Solution](..\active-directory\choose-hybrid-identity-solution.md).</span><span class="sxs-lookup"><span data-stu-id="c8ce2-117">Hybrid comes with deployment options (Synchronized Identity, Federated Identity, etc.) that all rely on directory synchronization and mostly define how identities are authenticated as discussed in [Choose a Hybrid Identity Solution](..\active-directory\choose-hybrid-identity-solution.md).</span></span>
>

## <a name="selecting-identity-for-an-azure-government-application"></a><span data-ttu-id="c8ce2-118">Selecting identity for an Azure Government application</span><span class="sxs-lookup"><span data-stu-id="c8ce2-118">Selecting identity for an Azure Government application</span></span>
<span data-ttu-id="c8ce2-119">When building any Azure application, a developer must first decide on the authentication technology:</span><span class="sxs-lookup"><span data-stu-id="c8ce2-119">When building any Azure application, a developer must first decide on the authentication technology:</span></span>

- <span data-ttu-id="c8ce2-120">**Applications using modern authentication** – Applications using OAuth, OpenID Connect, and/or other modern authentication protocols supported by Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-120">**Applications using modern authentication** – Applications using OAuth, OpenID Connect, and/or other modern authentication protocols supported by Azure Active Directory.</span></span>  <span data-ttu-id="c8ce2-121">An example is a newly developed application built using PaaS technologies (**for example**, Web Sites, Cloud Database as a Service, etc.)</span><span class="sxs-lookup"><span data-stu-id="c8ce2-121">An example is a newly developed application built using PaaS technologies (**for example**, Web Sites, Cloud Database as a Service, etc.)</span></span>
- <span data-ttu-id="c8ce2-122">**Apps using legacy authentication protocols (Kerberos/NTLM)** – Applications typically migrated from on-premises (**for example**, Lift-n-Shift).</span><span class="sxs-lookup"><span data-stu-id="c8ce2-122">**Apps using legacy authentication protocols (Kerberos/NTLM)** – Applications typically migrated from on-premises (**for example**, Lift-n-Shift).</span></span>

<span data-ttu-id="c8ce2-123">Based on this decision there are different considerations when building in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-123">Based on this decision there are different considerations when building in Azure Government.</span></span>

### <a name="applications-using-modern-authentication-in-azure-government"></a><span data-ttu-id="c8ce2-124">Applications using modern authentication in Azure Government</span><span class="sxs-lookup"><span data-stu-id="c8ce2-124">Applications using modern authentication in Azure Government</span></span>
<span data-ttu-id="c8ce2-125">[Integrating Applications with Azure Active Directory](../active-directory/develop/quickstart-v1-integrate-apps-with-azure-ad.md) shows how you can use Azure AD to provide secure sign-in and authorization to your applications.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-125">[Integrating Applications with Azure Active Directory](../active-directory/develop/quickstart-v1-integrate-apps-with-azure-ad.md) shows how you can use Azure AD to provide secure sign-in and authorization to your applications.</span></span>  <span data-ttu-id="c8ce2-126">This process is the same for Azure Public and Azure Government once you choose your identity authority.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-126">This process is the same for Azure Public and Azure Government once you choose your identity authority.</span></span>

#### <a name="choosing-your-identity-authority"></a><span data-ttu-id="c8ce2-127">Choosing your identity authority</span><span class="sxs-lookup"><span data-stu-id="c8ce2-127">Choosing your identity authority</span></span>
<span data-ttu-id="c8ce2-128">Azure Government applications can use Azure AD Government identities, but can you use Azure AD Public identities to authenticate to an application hosted in Azure Government?</span><span class="sxs-lookup"><span data-stu-id="c8ce2-128">Azure Government applications can use Azure AD Government identities, but can you use Azure AD Public identities to authenticate to an application hosted in Azure Government?</span></span>  <span data-ttu-id="c8ce2-129">Yes!</span><span class="sxs-lookup"><span data-stu-id="c8ce2-129">Yes!</span></span>  <span data-ttu-id="c8ce2-130">Since you can use either identity authority, you need to choose which to use:</span><span class="sxs-lookup"><span data-stu-id="c8ce2-130">Since you can use either identity authority, you need to choose which to use:</span></span>

-   <span data-ttu-id="c8ce2-131">**Azure AD Public** – Commonly used if your organization already has an Azure AD Public tenant to support Office 365 (Public or GCC) or another application.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-131">**Azure AD Public** – Commonly used if your organization already has an Azure AD Public tenant to support Office 365 (Public or GCC) or another application.</span></span>
-   <span data-ttu-id="c8ce2-132">**Azure AD Government** - Commonly used if your organization already has an Azure AD Government tenant to support Office 365 (GCC High or DoD) or are creating a new tenant in Azure AD Government.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-132">**Azure AD Government** - Commonly used if your organization already has an Azure AD Government tenant to support Office 365 (GCC High or DoD) or are creating a new tenant in Azure AD Government.</span></span>

<span data-ttu-id="c8ce2-133">Once decided, the special consideration is where you perform your app registration.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-133">Once decided, the special consideration is where you perform your app registration.</span></span> <span data-ttu-id="c8ce2-134">If you choose Azure AD Public identities for your Azure Government application, you must register the application in your Azure AD Public tenant.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-134">If you choose Azure AD Public identities for your Azure Government application, you must register the application in your Azure AD Public tenant.</span></span> <span data-ttu-id="c8ce2-135">Otherwise, if you perform the app registration in the directory the subscription trusts (Azure Government) the intended set of users cannot authenticate.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-135">Otherwise, if you perform the app registration in the directory the subscription trusts (Azure Government) the intended set of users cannot authenticate.</span></span>

>[!NOTE]
> <span data-ttu-id="c8ce2-136">Applications registered with Azure AD only allow sign-in from users in the Azure AD tenant the application was registered in.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-136">Applications registered with Azure AD only allow sign-in from users in the Azure AD tenant the application was registered in.</span></span> <span data-ttu-id="c8ce2-137">If you have multiple Azure AD Public tenants, it’s important to know which is intended to allow sign-ins from.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-137">If you have multiple Azure AD Public tenants, it’s important to know which is intended to allow sign-ins from.</span></span> <span data-ttu-id="c8ce2-138">If you intend to allow users to authenticate to the application from multiple Azure AD tenants the application must be registered in each tenant.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-138">If you intend to allow users to authenticate to the application from multiple Azure AD tenants the application must be registered in each tenant.</span></span>
>

<span data-ttu-id="c8ce2-139">The other consideration is the identity authority URL.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-139">The other consideration is the identity authority URL.</span></span>  <span data-ttu-id="c8ce2-140">You need the correct URL based on your chosen authority:</span><span class="sxs-lookup"><span data-stu-id="c8ce2-140">You need the correct URL based on your chosen authority:</span></span>

-   <span data-ttu-id="c8ce2-141">**Azure AD Public** = login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="c8ce2-141">**Azure AD Public** = login.microsoftonline.com</span></span>
-   <span data-ttu-id="c8ce2-142">**Azure AD Government** = login.microsoftonline.us</span><span class="sxs-lookup"><span data-stu-id="c8ce2-142">**Azure AD Government** = login.microsoftonline.us</span></span>

### <a name="applications-using-legacy-authentication-protocols-kerberosntlm"></a><span data-ttu-id="c8ce2-143">Applications using legacy authentication protocols (Kerberos/NTLM)</span><span class="sxs-lookup"><span data-stu-id="c8ce2-143">Applications using legacy authentication protocols (Kerberos/NTLM)</span></span>
<span data-ttu-id="c8ce2-144">Supporting IaaS cloud-based applications dependent on NTLM/Kerberos authentication requires On-Premises Identity.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-144">Supporting IaaS cloud-based applications dependent on NTLM/Kerberos authentication requires On-Premises Identity.</span></span> <span data-ttu-id="c8ce2-145">The aim is to support logins for line-of-business application and other apps that require Windows Integrated authentication.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-145">The aim is to support logins for line-of-business application and other apps that require Windows Integrated authentication.</span></span> <span data-ttu-id="c8ce2-146">Adding Active Directory domain controllers as virtual machines in Azure IaaS is the typical method to support these types of apps, shown in the following figure:</span><span class="sxs-lookup"><span data-stu-id="c8ce2-146">Adding Active Directory domain controllers as virtual machines in Azure IaaS is the typical method to support these types of apps, shown in the following figure:</span></span> 

<div id="imagecontainer">
<div></div>
<div align="center">

<span data-ttu-id="c8ce2-147">![alt text](./media/documentation-government-plan-identity-extending-ad-to-azure-iaas.png "Extending On-Premises Active Directory Footprint to Azure IaaS")</span><span class="sxs-lookup"><span data-stu-id="c8ce2-147">![alt text](./media/documentation-government-plan-identity-extending-ad-to-azure-iaas.png "Extending On-Premises Active Directory Footprint to Azure IaaS")</span></span>

</div>
<div></div>
</div>

>[!NOTE]
><span data-ttu-id="c8ce2-148">The preceding figure is a simple connectivity example, using site-to-site VPN.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-148">The preceding figure is a simple connectivity example, using site-to-site VPN.</span></span> <span data-ttu-id="c8ce2-149">Azure ExpressRoute is another and more preferred connectivity option.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-149">Azure ExpressRoute is another and more preferred connectivity option.</span></span>
>

<span data-ttu-id="c8ce2-150">The type of domain controller to place in Azure is also a consideration based on application requirements for directory access.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-150">The type of domain controller to place in Azure is also a consideration based on application requirements for directory access.</span></span> <span data-ttu-id="c8ce2-151">If applications require directory write access, deploy a standard domain controller with a writable copy of the Active Directory database.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-151">If applications require directory write access, deploy a standard domain controller with a writable copy of the Active Directory database.</span></span> <span data-ttu-id="c8ce2-152">If applications only require directory read access, we recommend deploying a RODC (Read-Only Domain Controller) to Azure instead.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-152">If applications only require directory read access, we recommend deploying a RODC (Read-Only Domain Controller) to Azure instead.</span></span> <span data-ttu-id="c8ce2-153">Specifically, for RODCs we recommend following the guidance available at [Deployment Decisions and Factors for Read-Only DCs](https://msdn.microsoft.com/library/azure/jj156090.aspx#BKMK_RODC).</span><span class="sxs-lookup"><span data-stu-id="c8ce2-153">Specifically, for RODCs we recommend following the guidance available at [Deployment Decisions and Factors for Read-Only DCs](https://msdn.microsoft.com/library/azure/jj156090.aspx#BKMK_RODC).</span></span>

<span data-ttu-id="c8ce2-154">We have documentation covering the guidelines for deploying AD Domain Controllers and ADFS (AD Federation Services) at these links:</span><span class="sxs-lookup"><span data-stu-id="c8ce2-154">We have documentation covering the guidelines for deploying AD Domain Controllers and ADFS (AD Federation Services) at these links:</span></span>

 - [<span data-ttu-id="c8ce2-155">Guidelines for Deploying Windows Server Active Directory on Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="c8ce2-155">Guidelines for Deploying Windows Server Active Directory on Azure Virtual Machines</span></span>](https://msdn.microsoft.com/library/azure/jj156090.aspx) 
   -  <span data-ttu-id="c8ce2-156">Answers questions such as:</span><span class="sxs-lookup"><span data-stu-id="c8ce2-156">Answers questions such as:</span></span>
    -   <span data-ttu-id="c8ce2-157">Is it safe to virtualize Windows Server Active Directory Domain Controllers?</span><span class="sxs-lookup"><span data-stu-id="c8ce2-157">Is it safe to virtualize Windows Server Active Directory Domain Controllers?</span></span>
    -   <span data-ttu-id="c8ce2-158">Why deploy AD to Azure Virtual Machines?</span><span class="sxs-lookup"><span data-stu-id="c8ce2-158">Why deploy AD to Azure Virtual Machines?</span></span>
    -   <span data-ttu-id="c8ce2-159">Can you deploy ADFS to Azure Virtual Machines?</span><span class="sxs-lookup"><span data-stu-id="c8ce2-159">Can you deploy ADFS to Azure Virtual Machines?</span></span>
 - [<span data-ttu-id="c8ce2-160">Deploying Active Directory Federation Services in Azure</span><span class="sxs-lookup"><span data-stu-id="c8ce2-160">Deploying Active Directory Federation Services in Azure</span></span>](..\active-directory\connect\active-directory-aadconnect-azure-adfs.md)
   -   <span data-ttu-id="c8ce2-161">Provides guidance on how to deploy ADFS in Azure.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-161">Provides guidance on how to deploy ADFS in Azure.</span></span>

## <a name="identity-scenarios-for-subscription-administration-in-azure-government"></a><span data-ttu-id="c8ce2-162">Identity scenarios for subscription administration in Azure Government</span><span class="sxs-lookup"><span data-stu-id="c8ce2-162">Identity scenarios for subscription administration in Azure Government</span></span>
<span data-ttu-id="c8ce2-163">First, see [Managing and connecting to your subscription in Azure Government](.\documentation-government-manage-subscriptions.md), for instructions on accessing Azure Government management portals.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-163">First, see [Managing and connecting to your subscription in Azure Government](.\documentation-government-manage-subscriptions.md), for instructions on accessing Azure Government management portals.</span></span>

<span data-ttu-id="c8ce2-164">There are a few important points that set the foundation of this section:</span><span class="sxs-lookup"><span data-stu-id="c8ce2-164">There are a few important points that set the foundation of this section:</span></span>

 -  <span data-ttu-id="c8ce2-165">Azure subscriptions only trust one directory, therefore subscription administration must be performed by an identity from that directory.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-165">Azure subscriptions only trust one directory, therefore subscription administration must be performed by an identity from that directory.</span></span>
 -  <span data-ttu-id="c8ce2-166">Azure Public subscriptions trust directories in Azure AD Public and Azure Government subscriptions trust directories in Azure AD Government.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-166">Azure Public subscriptions trust directories in Azure AD Public and Azure Government subscriptions trust directories in Azure AD Government.</span></span>
 -  <span data-ttu-id="c8ce2-167">If you have both Azure Public and Azure Government subscriptions, separate identities for both are required.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-167">If you have both Azure Public and Azure Government subscriptions, separate identities for both are required.</span></span>

<span data-ttu-id="c8ce2-168">The currently supported identity scenarios to simultaneously manage Azure Public and Azure Government subscriptions are:</span><span class="sxs-lookup"><span data-stu-id="c8ce2-168">The currently supported identity scenarios to simultaneously manage Azure Public and Azure Government subscriptions are:</span></span>

- <span data-ttu-id="c8ce2-169">Cloud identities - Cloud identities are used to manage both subscriptions</span><span class="sxs-lookup"><span data-stu-id="c8ce2-169">Cloud identities - Cloud identities are used to manage both subscriptions</span></span>
- <span data-ttu-id="c8ce2-170">Hybrid and cloud identities - Hybrid identity for one subscription, cloud identity for the other</span><span class="sxs-lookup"><span data-stu-id="c8ce2-170">Hybrid and cloud identities - Hybrid identity for one subscription, cloud identity for the other</span></span>
- <span data-ttu-id="c8ce2-171">Hybrid identities - Hybrid identities are used to manage both subscriptions.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-171">Hybrid identities - Hybrid identities are used to manage both subscriptions.</span></span>

<span data-ttu-id="c8ce2-172">A common scenario, having both Office 365 and Azure subscriptions, is conveyed in each of the following scenarios.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-172">A common scenario, having both Office 365 and Azure subscriptions, is conveyed in each of the following scenarios.</span></span>

### <a name="using-cloud-identities-for-multi-cloud-subscription-administration"></a><span data-ttu-id="c8ce2-173">Using cloud identities for multi-cloud subscription administration</span><span class="sxs-lookup"><span data-stu-id="c8ce2-173">Using cloud identities for multi-cloud subscription administration</span></span>

<span data-ttu-id="c8ce2-174">The following diagram is the simplest of the scenarios to implement.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-174">The following diagram is the simplest of the scenarios to implement.</span></span>

<div id="imagecontainer">
<div></div>
<div align="center">

<span data-ttu-id="c8ce2-175">![alt text](./media/documentation-government-plan-identity-cloud-identities-for-subscription-administration.png "Using Cloud Identities for Multi-Cloud Subscription Administration")</span><span class="sxs-lookup"><span data-stu-id="c8ce2-175">![alt text](./media/documentation-government-plan-identity-cloud-identities-for-subscription-administration.png "Using Cloud Identities for Multi-Cloud Subscription Administration")</span></span>

</div>
<div></div>
</div>

<span data-ttu-id="c8ce2-176">While using cloud identities is the simplest approach, it is also the least secure because passwords are used as an authentication factor.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-176">While using cloud identities is the simplest approach, it is also the least secure because passwords are used as an authentication factor.</span></span> <span data-ttu-id="c8ce2-177">We recommend [Azure Multi-Factor Authentication](../active-directory/authentication/multi-factor-authentication.md), Microsoft's two-step verification solution, to add a critical second layer of security to secure access to Azure subscriptions when using cloud identities.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-177">We recommend [Azure Multi-Factor Authentication](../active-directory/authentication/multi-factor-authentication.md), Microsoft's two-step verification solution, to add a critical second layer of security to secure access to Azure subscriptions when using cloud identities.</span></span>

<span data-ttu-id="c8ce2-178">See [How Azure Multi-Factor Authentication works](../active-directory/authentication/concept-mfa-howitworks.md) to learn more about the available methods for two-step verification.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-178">See [How Azure Multi-Factor Authentication works](../active-directory/authentication/concept-mfa-howitworks.md) to learn more about the available methods for two-step verification.</span></span>

### <a name="using-hybrid-and-cloud-identities-for-multi-cloud-subscription-administration"></a><span data-ttu-id="c8ce2-179">Using hybrid and cloud identities for multi-cloud subscription administration</span><span class="sxs-lookup"><span data-stu-id="c8ce2-179">Using hybrid and cloud identities for multi-cloud subscription administration</span></span>

<span data-ttu-id="c8ce2-180">In this scenario, we include administrator identities through directory synchronization to the Public tenant while cloud identities are still used in the government tenant:</span><span class="sxs-lookup"><span data-stu-id="c8ce2-180">In this scenario, we include administrator identities through directory synchronization to the Public tenant while cloud identities are still used in the government tenant:</span></span>

<div id="imagecontainer">
<div></div>
<div align="center">

<span data-ttu-id="c8ce2-181">![alt text](./media/documentation-government-plan-identity-hybrid-and-cloud-identities-for-subscription-administration.png "Using Hybrid and Cloud Identities for Multi-Cloud Subscription Administration")</span><span class="sxs-lookup"><span data-stu-id="c8ce2-181">![alt text](./media/documentation-government-plan-identity-hybrid-and-cloud-identities-for-subscription-administration.png "Using Hybrid and Cloud Identities for Multi-Cloud Subscription Administration")</span></span>

</div>
<div></div>
</div>

<span data-ttu-id="c8ce2-182">Using hybrid identities for administrative accounts allows the use of smartcards (physical or virtual).</span><span class="sxs-lookup"><span data-stu-id="c8ce2-182">Using hybrid identities for administrative accounts allows the use of smartcards (physical or virtual).</span></span> <span data-ttu-id="c8ce2-183">Government agencies using Common Access Cards (CACs) or Personal Identity Verification (PIV) cards benefit from this approach.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-183">Government agencies using Common Access Cards (CACs) or Personal Identity Verification (PIV) cards benefit from this approach.</span></span> <span data-ttu-id="c8ce2-184">In this scenario ADFS serves as the identity provider and implements the two-step verification (**for example**, smart card + PIN).</span><span class="sxs-lookup"><span data-stu-id="c8ce2-184">In this scenario ADFS serves as the identity provider and implements the two-step verification (**for example**, smart card + PIN).</span></span>

### <a name="using-hybrid-identities-for-multi-cloud-subscription-administration"></a><span data-ttu-id="c8ce2-185">Using hybrid identities for multi-cloud subscription administration</span><span class="sxs-lookup"><span data-stu-id="c8ce2-185">Using hybrid identities for multi-cloud subscription administration</span></span>

<span data-ttu-id="c8ce2-186">In this scenario, hybrid identities are used to administrator subscriptions in both clouds:</span><span class="sxs-lookup"><span data-stu-id="c8ce2-186">In this scenario, hybrid identities are used to administrator subscriptions in both clouds:</span></span>

<div id="imagecontainer">
<div></div>
<div align="center">

<span data-ttu-id="c8ce2-187">![alt text](./media/documentation-government-plan-identity-hybrid-identities-for-subscription-administration.png "Using Hybrid Identities for Multi-Cloud Subscription Administration")</span><span class="sxs-lookup"><span data-stu-id="c8ce2-187">![alt text](./media/documentation-government-plan-identity-hybrid-identities-for-subscription-administration.png "Using Hybrid Identities for Multi-Cloud Subscription Administration")</span></span>

</div>
<div></div>
</div>

## <a name="frequently-asked-questions"></a><span data-ttu-id="c8ce2-188">Frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="c8ce2-188">Frequently asked questions</span></span>

<span data-ttu-id="c8ce2-189">**Why does Office 365 GCC use Azure AD Public?**</span><span class="sxs-lookup"><span data-stu-id="c8ce2-189">**Why does Office 365 GCC use Azure AD Public?**</span></span>

<span data-ttu-id="c8ce2-190">The first Office 365 US Government environment, Government Community Cloud (GCC), was created when Microsoft had a single cloud directory.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-190">The first Office 365 US Government environment, Government Community Cloud (GCC), was created when Microsoft had a single cloud directory.</span></span> <span data-ttu-id="c8ce2-191">The Office 365 GCC environment was designed to use Azure AD Public while still adhering to controls and requirements outlined in FedRAMP Moderate, CJIS (Criminal Justice Information Services), IRS 1075, and National Institute of Standards and Technology (NIST) publication 800-171.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-191">The Office 365 GCC environment was designed to use Azure AD Public while still adhering to controls and requirements outlined in FedRAMP Moderate, CJIS (Criminal Justice Information Services), IRS 1075, and National Institute of Standards and Technology (NIST) publication 800-171.</span></span> <span data-ttu-id="c8ce2-192">Azure Government, with its Azure AD infrastructure was created later.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-192">Azure Government, with its Azure AD infrastructure was created later.</span></span> <span data-ttu-id="c8ce2-193">By that time, GCC had already secured the necessary compliance certifications (for example, FedRAMP Moderate and CJIS) to meet Federal, State, and Local government requirements while serving hundreds of thousands of customers.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-193">By that time, GCC had already secured the necessary compliance certifications (for example, FedRAMP Moderate and CJIS) to meet Federal, State, and Local government requirements while serving hundreds of thousands of customers.</span></span> <span data-ttu-id="c8ce2-194">Now, many Office 365 GCC customers have two Azure AD tenants: one from the Azure AD subscription that supports Office 365 GCC and the other from their Azure Government subscription with identities in both.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-194">Now, many Office 365 GCC customers have two Azure AD tenants: one from the Azure AD subscription that supports Office 365 GCC and the other from their Azure Government subscription with identities in both.</span></span>


<span data-ttu-id="c8ce2-195">**How do I identify an Azure Government tenant?**</span><span class="sxs-lookup"><span data-stu-id="c8ce2-195">**How do I identify an Azure Government tenant?**</span></span>  
<span data-ttu-id="c8ce2-196">Here’s a way to find out using your browser of choice:</span><span class="sxs-lookup"><span data-stu-id="c8ce2-196">Here’s a way to find out using your browser of choice:</span></span>

   - <span data-ttu-id="c8ce2-197">Obtain your tenant name (**for example**, contoso.onmicrosoft.com) or a domain name registered to your Azure AD tenant (**for example**, contoso.gov).</span><span class="sxs-lookup"><span data-stu-id="c8ce2-197">Obtain your tenant name (**for example**, contoso.onmicrosoft.com) or a domain name registered to your Azure AD tenant (**for example**, contoso.gov).</span></span>  
   - <span data-ttu-id="c8ce2-198">Navigate to https://login.microsoftonline.com/\<domainname\>/.well-known/openid-configuration</span><span class="sxs-lookup"><span data-stu-id="c8ce2-198">Navigate to https://login.microsoftonline.com/\<domainname\>/.well-known/openid-configuration</span></span>  
     - <span data-ttu-id="c8ce2-199">\<domainname\> can either be the tenant name or domain name you gathered in step 1.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-199">\<domainname\> can either be the tenant name or domain name you gathered in step 1.</span></span>
     - <span data-ttu-id="c8ce2-200">**An example URL**: https://login.microsoftonline.com/contoso.onmicrosoft.com/.well-known/openid-configuration</span><span class="sxs-lookup"><span data-stu-id="c8ce2-200">**An example URL**: https://login.microsoftonline.com/contoso.onmicrosoft.com/.well-known/openid-configuration</span></span>
   - <span data-ttu-id="c8ce2-201">The result posts back to the page in attribute/value pairs using Java Script Object Notation (JSON) format that resembles:</span><span class="sxs-lookup"><span data-stu-id="c8ce2-201">The result posts back to the page in attribute/value pairs using Java Script Object Notation (JSON) format that resembles:</span></span>

     ```json
     {
       "authorization_endpoint":"https://login.microsoftonline.com/b552ff1c-edad-4b6f-b301-5963a979bc4d/oauth2/authorize",
       "tenant_region_scope":"USG"
     }
     ```
     
   - <span data-ttu-id="c8ce2-202">If the **tenant_region_scope** attribute’s value is **USG** as shown, you have yourself an Azure Government tenant.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-202">If the **tenant_region_scope** attribute’s value is **USG** as shown, you have yourself an Azure Government tenant.</span></span>
     - <span data-ttu-id="c8ce2-203">The result is a JSON file that’s natively rendered by more modern browsers such as Microsoft Edge, Mozilla Firefox, and Google Chrome.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-203">The result is a JSON file that’s natively rendered by more modern browsers such as Microsoft Edge, Mozilla Firefox, and Google Chrome.</span></span> <span data-ttu-id="c8ce2-204">Internet Explorer doesn’t natively render the JSON format so instead prompts you to open or save the file.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-204">Internet Explorer doesn’t natively render the JSON format so instead prompts you to open or save the file.</span></span> <span data-ttu-id="c8ce2-205">If you must use Internet Explorer, choose the save option and open it with another browser or plain text reader.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-205">If you must use Internet Explorer, choose the save option and open it with another browser or plain text reader.</span></span>
     - <span data-ttu-id="c8ce2-206">The tenant_region_scope property is exactly how it sounds, regional.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-206">The tenant_region_scope property is exactly how it sounds, regional.</span></span> <span data-ttu-id="c8ce2-207">If you have a tenant in Azure Public in North America, the value would be **NA**.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-207">If you have a tenant in Azure Public in North America, the value would be **NA**.</span></span>

<span data-ttu-id="c8ce2-208">**If I’m an Office 365 GCC customer and want to build solutions in Azure Government do I need to have two tenants?**</span><span class="sxs-lookup"><span data-stu-id="c8ce2-208">**If I’m an Office 365 GCC customer and want to build solutions in Azure Government do I need to have two tenants?**</span></span>  
<span data-ttu-id="c8ce2-209">Yes, the Azure AD Government tenant is required for your Azure Government Subscription administration.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-209">Yes, the Azure AD Government tenant is required for your Azure Government Subscription administration.</span></span>

<span data-ttu-id="c8ce2-210">**If I’m an Office 365 GCC customer that has built workloads in Azure Government, where should I authenticate from, Public or Government?**</span><span class="sxs-lookup"><span data-stu-id="c8ce2-210">**If I’m an Office 365 GCC customer that has built workloads in Azure Government, where should I authenticate from, Public or Government?**</span></span>  
<span data-ttu-id="c8ce2-211">See “Choosing your Identity Authority” earlier in this article.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-211">See “Choosing your Identity Authority” earlier in this article.</span></span>

<span data-ttu-id="c8ce2-212">**I’m an Office 365 customer and have chosen hybrid identity as my identity model. I also have several Azure subscriptions. Is it possible to use the same Azure AD tenant to handle sign-in for Office 365, applications built in my Azure subscriptions, and/or applications reconfigured to use Azure AD for sign-in?**</span><span class="sxs-lookup"><span data-stu-id="c8ce2-212">**I’m an Office 365 customer and have chosen hybrid identity as my identity model. I also have several Azure subscriptions. Is it possible to use the same Azure AD tenant to handle sign-in for Office 365, applications built in my Azure subscriptions, and/or applications reconfigured to use Azure AD for sign-in?**</span></span>

<span data-ttu-id="c8ce2-213">Yes, see [How Azure subscriptions are associated with Azure Active Directory](../active-directory/fundamentals/active-directory-how-subscriptions-associated-directory.md) to learn more about the relationship between Azure subscriptions and Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-213">Yes, see [How Azure subscriptions are associated with Azure Active Directory](../active-directory/fundamentals/active-directory-how-subscriptions-associated-directory.md) to learn more about the relationship between Azure subscriptions and Azure AD.</span></span> <span data-ttu-id="c8ce2-214">It also contains instructions on how to associate subscriptions to the common directory of your choosing.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-214">It also contains instructions on how to associate subscriptions to the common directory of your choosing.</span></span>

<span data-ttu-id="c8ce2-215">**Can an Azure Government subscription be associated with a directory in Azure AD Public?**</span><span class="sxs-lookup"><span data-stu-id="c8ce2-215">**Can an Azure Government subscription be associated with a directory in Azure AD Public?**</span></span>

<span data-ttu-id="c8ce2-216">No, the ability to manage Azure Government subscriptions requires identities sourced from a directory in Azure AD Government.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-216">No, the ability to manage Azure Government subscriptions requires identities sourced from a directory in Azure AD Government.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8ce2-217">Next steps</span><span class="sxs-lookup"><span data-stu-id="c8ce2-217">Next steps</span></span>

- <span data-ttu-id="c8ce2-218">Check out the [Azure Government developer guide](..\azure-government\documentation-government-developer-guide.md) and build your first application!</span><span class="sxs-lookup"><span data-stu-id="c8ce2-218">Check out the [Azure Government developer guide](..\azure-government\documentation-government-developer-guide.md) and build your first application!</span></span>
- <span data-ttu-id="c8ce2-219">For supplemental information and updates, subscribe to the [Microsoft Azure Government blog.](https://blogs.msdn.microsoft.com/azuregov/)</span><span class="sxs-lookup"><span data-stu-id="c8ce2-219">For supplemental information and updates, subscribe to the [Microsoft Azure Government blog.](https://blogs.msdn.microsoft.com/azuregov/)</span></span>

