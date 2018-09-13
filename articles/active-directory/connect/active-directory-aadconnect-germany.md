---
title: Azure AD Connect in Microsoft Cloud Germany
description: Azure AD Connect will integrate your on-premises directories with Azure Active Directory. This allows you to provide a common identity for Office 365, Azure, and SaaS applications integrated with Azure AD.
keywords: introduction to Azure AD Connect, Azure AD Connect overview, what is Azure AD Connect, install active directory, Germany, Black Forest
services: active-directory
documentationcenter: ''
author: billmath
manager: femila
editor: ''
ms.assetid: 2bcb0caf-5d97-46cb-8c32-bda66cc22dad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/07/2017
ms.author: billmath
ms.openlocfilehash: 36ed7347fb2baa01e1c6c2083344b78c6ee803fa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556531"
---
# <a name="azure-ad-connect-in-microsoft-cloud-germany---public-preview"></a><span data-ttu-id="5f608-105">Azure AD Connect in Microsoft Cloud Germany - Public Preview</span><span class="sxs-lookup"><span data-stu-id="5f608-105">Azure AD Connect in Microsoft Cloud Germany - Public Preview</span></span>
## <a name="introduction"></a><span data-ttu-id="5f608-106">Introduction</span><span class="sxs-lookup"><span data-stu-id="5f608-106">Introduction</span></span>
<span data-ttu-id="5f608-107">Azure AD Connect provides synchronization between your on-premises Active Directory and Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5f608-107">Azure AD Connect provides synchronization between your on-premises Active Directory and Azure Active Directory.</span></span>
<span data-ttu-id="5f608-108">Currently, many of the scenarios in [Microsoft Cloud Germany](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) must be done by the operator.</span><span class="sxs-lookup"><span data-stu-id="5f608-108">Currently, many of the scenarios in [Microsoft Cloud Germany](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) must be done by the operator.</span></span> <span data-ttu-id="5f608-109">When using Microsoft Cloud Germany, you must be aware of the following:</span><span class="sxs-lookup"><span data-stu-id="5f608-109">When using Microsoft Cloud Germany, you must be aware of the following:</span></span>

* <span data-ttu-id="5f608-110">The following URLs must be opened on a proxy server for synchronization to occur successfully:</span><span class="sxs-lookup"><span data-stu-id="5f608-110">The following URLs must be opened on a proxy server for synchronization to occur successfully:</span></span>
  
  * <span data-ttu-id="5f608-111">\*.microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="5f608-111">\*.microsoftonline.de</span></span>
  * <span data-ttu-id="5f608-112">\*.windows.net</span><span class="sxs-lookup"><span data-stu-id="5f608-112">\*.windows.net</span></span>
  * * <span data-ttu-id="5f608-113">Certificate Revocation Lists</span><span class="sxs-lookup"><span data-stu-id="5f608-113">Certificate Revocation Lists</span></span>
* <span data-ttu-id="5f608-114">When you sign in to your Azure AD directory, you must use an account in the onmicrosoft.de domain.</span><span class="sxs-lookup"><span data-stu-id="5f608-114">When you sign in to your Azure AD directory, you must use an account in the onmicrosoft.de domain.</span></span>
* <span data-ttu-id="5f608-115">The following features are not available:</span><span class="sxs-lookup"><span data-stu-id="5f608-115">The following features are not available:</span></span>
  * <span data-ttu-id="5f608-116">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="5f608-116">Azure AD Connect Health</span></span>
  * <span data-ttu-id="5f608-117">Automatic updates</span><span class="sxs-lookup"><span data-stu-id="5f608-117">Automatic updates</span></span>
  * <span data-ttu-id="5f608-118">Password writeback</span><span class="sxs-lookup"><span data-stu-id="5f608-118">Password writeback</span></span>

## <a name="download"></a><span data-ttu-id="5f608-119">Download</span><span class="sxs-lookup"><span data-stu-id="5f608-119">Download</span></span>
<span data-ttu-id="5f608-120">You can download Azure AD Connect from the Azure AD Connect blade within the portal.</span><span class="sxs-lookup"><span data-stu-id="5f608-120">You can download Azure AD Connect from the Azure AD Connect blade within the portal.</span></span>  <span data-ttu-id="5f608-121">Use the instructions below to locate the Azure AD Connect blade.</span><span class="sxs-lookup"><span data-stu-id="5f608-121">Use the instructions below to locate the Azure AD Connect blade.</span></span>

### <a name="the-azure-ad-connect-blade"></a><span data-ttu-id="5f608-122">The Azure AD Connect Blade</span><span class="sxs-lookup"><span data-stu-id="5f608-122">The Azure AD Connect Blade</span></span>
<span data-ttu-id="5f608-123">Once you have signed in to the Azure portal, do the following:</span><span class="sxs-lookup"><span data-stu-id="5f608-123">Once you have signed in to the Azure portal, do the following:</span></span>

1. <span data-ttu-id="5f608-124">Go to Browse</span><span class="sxs-lookup"><span data-stu-id="5f608-124">Go to Browse</span></span>
2. <span data-ttu-id="5f608-125">Select Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5f608-125">Select Azure Active Directory</span></span>
3. <span data-ttu-id="5f608-126">Then select Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="5f608-126">Then select Azure AD Connect</span></span>

<span data-ttu-id="5f608-127">You should see the following:</span><span class="sxs-lookup"><span data-stu-id="5f608-127">You should see the following:</span></span>

![Azure AD Connect Blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-germany/germany1.png)

<span data-ttu-id="5f608-129">The following table describes the features shown in the blade.</span><span class="sxs-lookup"><span data-stu-id="5f608-129">The following table describes the features shown in the blade.</span></span>

| <span data-ttu-id="5f608-130">Title</span><span class="sxs-lookup"><span data-stu-id="5f608-130">Title</span></span> | <span data-ttu-id="5f608-131">Description</span><span class="sxs-lookup"><span data-stu-id="5f608-131">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5f608-132">SYNC STATUS</span><span class="sxs-lookup"><span data-stu-id="5f608-132">SYNC STATUS</span></span> |<span data-ttu-id="5f608-133">Let's you know whether synchronization is enabled or disabled.</span><span class="sxs-lookup"><span data-stu-id="5f608-133">Let's you know whether synchronization is enabled or disabled.</span></span> |
| <span data-ttu-id="5f608-134">LAST SYNC</span><span class="sxs-lookup"><span data-stu-id="5f608-134">LAST SYNC</span></span> |<span data-ttu-id="5f608-135">The last time a successful sync completed.</span><span class="sxs-lookup"><span data-stu-id="5f608-135">The last time a successful sync completed.</span></span> |
| <span data-ttu-id="5f608-136">FEDERATED DOMAINS</span><span class="sxs-lookup"><span data-stu-id="5f608-136">FEDERATED DOMAINS</span></span> |<span data-ttu-id="5f608-137">Shows the number of federated domains currently configured.</span><span class="sxs-lookup"><span data-stu-id="5f608-137">Shows the number of federated domains currently configured.</span></span> |

## <a name="installation"></a><span data-ttu-id="5f608-138">Installation</span><span class="sxs-lookup"><span data-stu-id="5f608-138">Installation</span></span>
<span data-ttu-id="5f608-139">To install Azure AD Connect, you can use the documentation [here](active-directory-aadconnect.md#install-azure-ad-connect).</span><span class="sxs-lookup"><span data-stu-id="5f608-139">To install Azure AD Connect, you can use the documentation [here](active-directory-aadconnect.md#install-azure-ad-connect).</span></span>

## <a name="advanced-features-and-additional-information"></a><span data-ttu-id="5f608-140">Advanced features and Additional Information</span><span class="sxs-lookup"><span data-stu-id="5f608-140">Advanced features and Additional Information</span></span>
<span data-ttu-id="5f608-141">For additional information and guidance on custom settings or advanced configurations, start with [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="5f608-141">For additional information and guidance on custom settings or advanced configurations, start with [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>  <span data-ttu-id="5f608-142">This page provides information and links to additional guidance.</span><span class="sxs-lookup"><span data-stu-id="5f608-142">This page provides information and links to additional guidance.</span></span>


