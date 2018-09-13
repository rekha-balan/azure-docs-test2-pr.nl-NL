---
title: Azure AD + Active Directory requirements for Azure RemoteApp | Microsoft Docs
description: Learn how to set up Active Directory to work with Azure RemoteApp.
services: remoteapp
documentationcenter: ''
author: msmbaldwin
manager: mbaldwin
ms.assetid: 66366b25-6012-45fa-a4f6-da0ddfe0b486
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 232901ab919c63ea70e52afb845240b41a517c51
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553016"
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a><span data-ttu-id="17814-103">Azure AD + Active Directory requirements for Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="17814-103">Azure AD + Active Directory requirements for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="17814-104">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="17814-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="17814-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="17814-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="17814-106">For your Azure RemoteApp hybrid collection or for a cloud collection that you want to federate using AD Connect, you need to do the following.</span><span class="sxs-lookup"><span data-stu-id="17814-106">For your Azure RemoteApp hybrid collection or for a cloud collection that you want to federate using AD Connect, you need to do the following.</span></span>

### <a name="connect-azure-ad-and-active-directory"></a><span data-ttu-id="17814-107">Connect Azure AD and Active Directory</span><span class="sxs-lookup"><span data-stu-id="17814-107">Connect Azure AD and Active Directory</span></span>
<span data-ttu-id="17814-108">If you want to connect your Azure AD tenant and your on-premises Active Directory environments, use AD Connect.</span><span class="sxs-lookup"><span data-stu-id="17814-108">If you want to connect your Azure AD tenant and your on-premises Active Directory environments, use AD Connect.</span></span> <span data-ttu-id="17814-109">It will take you only [4 clicks](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) to connect the two directories.</span><span class="sxs-lookup"><span data-stu-id="17814-109">It will take you only [4 clicks](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) to connect the two directories.</span></span>

<span data-ttu-id="17814-110">Note - Directory synchronization is required for hybrid collections.</span><span class="sxs-lookup"><span data-stu-id="17814-110">Note - Directory synchronization is required for hybrid collections.</span></span>

### <a name="make-sure-your-domaincom-match"></a><span data-ttu-id="17814-111">Make sure your "@domain.com" match</span><span class="sxs-lookup"><span data-stu-id="17814-111">Make sure your "@domain.com" match</span></span>
<span data-ttu-id="17814-112">Before you get started, make sure that the UPN for your on-premises forest matches the suffix of your Azure AD domain.</span><span class="sxs-lookup"><span data-stu-id="17814-112">Before you get started, make sure that the UPN for your on-premises forest matches the suffix of your Azure AD domain.</span></span> 

<span data-ttu-id="17814-113">After you set up the UPN domain suffix in Azure AD, all users logging into Azure RemoteApp will log in as "user@<the suffix you set up>."</span><span class="sxs-lookup"><span data-stu-id="17814-113">After you set up the UPN domain suffix in Azure AD, all users logging into Azure RemoteApp will log in as "user@<the suffix you set up>."</span></span> <span data-ttu-id="17814-114">Make sure that users can also log in with the same user@suffix into the on-premises domain.</span><span class="sxs-lookup"><span data-stu-id="17814-114">Make sure that users can also log in with the same user@suffix into the on-premises domain.</span></span> <span data-ttu-id="17814-115">In certain cases you can set up one domain name in Azure AD while specifying a different domain suffix for the user on-prem.</span><span class="sxs-lookup"><span data-stu-id="17814-115">In certain cases you can set up one domain name in Azure AD while specifying a different domain suffix for the user on-prem.</span></span> <span data-ttu-id="17814-116">In this case, your users won't be able to connect to any domain-joined computers or resources through Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="17814-116">In this case, your users won't be able to connect to any domain-joined computers or resources through Azure RemoteApp.</span></span>

<span data-ttu-id="17814-117">For example, if you set up your UPN domain suffix in AAD as contoso.com, but some users on premises/AD are configured to log in with @contoso.uk, then those users will not be able to correctly log into the ARA collection.</span><span class="sxs-lookup"><span data-stu-id="17814-117">For example, if you set up your UPN domain suffix in AAD as contoso.com, but some users on premises/AD are configured to log in with @contoso.uk, then those users will not be able to correctly log into the ARA collection.</span></span> <span data-ttu-id="17814-118">Users UPN in AAD and AD must be the same for the login to be possible”</span><span class="sxs-lookup"><span data-stu-id="17814-118">Users UPN in AAD and AD must be the same for the login to be possible”</span></span>

### <a name="create-objects-for-azure-remoteapp"></a><span data-ttu-id="17814-119">Create objects for Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="17814-119">Create objects for Azure RemoteApp</span></span>
<span data-ttu-id="17814-120">You also need to create the following on-premises Active Directory objects:</span><span class="sxs-lookup"><span data-stu-id="17814-120">You also need to create the following on-premises Active Directory objects:</span></span>

* <span data-ttu-id="17814-121">A service account to provide access to domain resources for RemoteApp programs by joining RDSH end points to the on-premises domain.</span><span class="sxs-lookup"><span data-stu-id="17814-121">A service account to provide access to domain resources for RemoteApp programs by joining RDSH end points to the on-premises domain.</span></span>
* <span data-ttu-id="17814-122">An Organizational Unit (OU) to contain RemoteApp machine objects.</span><span class="sxs-lookup"><span data-stu-id="17814-122">An Organizational Unit (OU) to contain RemoteApp machine objects.</span></span> <span data-ttu-id="17814-123">Use of the OU is recommended (but not required) to isolate the accounts and policies you will use with RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="17814-123">Use of the OU is recommended (but not required) to isolate the accounts and policies you will use with RemoteApp.</span></span>

<span data-ttu-id="17814-124">You need both of these objects when you create your RemoteApp collection, so be sure to do these steps first.</span><span class="sxs-lookup"><span data-stu-id="17814-124">You need both of these objects when you create your RemoteApp collection, so be sure to do these steps first.</span></span>

