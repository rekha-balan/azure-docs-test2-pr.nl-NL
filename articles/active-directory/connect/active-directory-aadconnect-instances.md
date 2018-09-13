---
title: 'Azure AD Connect: Sync service instances | Microsoft Docs'
description: This page documents special considerations for Azure AD instances.
services: active-directory
documentationcenter: ''
author: andkjell
manager: femila
editor: ''
ms.assetid: f340ea11-8ff5-4ae6-b09d-e939c76355a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/07/2017
ms.author: billmath
ms.openlocfilehash: db2d69c2a7e4db624bc73eae04d29fbccce99de4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662240"
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a><span data-ttu-id="a4bc9-103">Azure AD Connect: Special considerations for instances</span><span class="sxs-lookup"><span data-stu-id="a4bc9-103">Azure AD Connect: Special considerations for instances</span></span>
<span data-ttu-id="a4bc9-104">Azure AD Connect is most commonly used with the world-wide instance of Azure AD and Office 365.</span><span class="sxs-lookup"><span data-stu-id="a4bc9-104">Azure AD Connect is most commonly used with the world-wide instance of Azure AD and Office 365.</span></span> <span data-ttu-id="a4bc9-105">But there are also other instances and these have different requirements for URLs and other special considerations.</span><span class="sxs-lookup"><span data-stu-id="a4bc9-105">But there are also other instances and these have different requirements for URLs and other special considerations.</span></span>

## <a name="microsoft-cloud-germany"></a><span data-ttu-id="a4bc9-106">Microsoft Cloud Germany</span><span class="sxs-lookup"><span data-stu-id="a4bc9-106">Microsoft Cloud Germany</span></span>
<span data-ttu-id="a4bc9-107">The [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) is a sovereign cloud operated by a German data trustee.</span><span class="sxs-lookup"><span data-stu-id="a4bc9-107">The [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) is a sovereign cloud operated by a German data trustee.</span></span>

| <span data-ttu-id="a4bc9-108">URLs to open in proxy server</span><span class="sxs-lookup"><span data-stu-id="a4bc9-108">URLs to open in proxy server</span></span> |
| --- |
| <span data-ttu-id="a4bc9-109">\*.microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="a4bc9-109">\*.microsoftonline.de</span></span> |
| <span data-ttu-id="a4bc9-110">\*.windows.net</span><span class="sxs-lookup"><span data-stu-id="a4bc9-110">\*.windows.net</span></span> |
| <span data-ttu-id="a4bc9-111">+Certificate Revocation Lists</span><span class="sxs-lookup"><span data-stu-id="a4bc9-111">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="a4bc9-112">When you sign in to your Azure AD tenant, you must use an account in the onmicrosoft.de domain.</span><span class="sxs-lookup"><span data-stu-id="a4bc9-112">When you sign in to your Azure AD tenant, you must use an account in the onmicrosoft.de domain.</span></span>

<span data-ttu-id="a4bc9-113">Features currently not present in the Microsoft Cloud Germany:</span><span class="sxs-lookup"><span data-stu-id="a4bc9-113">Features currently not present in the Microsoft Cloud Germany:</span></span>

* <span data-ttu-id="a4bc9-114">**Azure AD Connect Health** is not available.</span><span class="sxs-lookup"><span data-stu-id="a4bc9-114">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="a4bc9-115">**Automatic updates** is not available.</span><span class="sxs-lookup"><span data-stu-id="a4bc9-115">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="a4bc9-116">**Password writeback** is not available.</span><span class="sxs-lookup"><span data-stu-id="a4bc9-116">**Password writeback** is not available.</span></span>
* <span data-ttu-id="a4bc9-117">Other Azure AD Premium services are not available.</span><span class="sxs-lookup"><span data-stu-id="a4bc9-117">Other Azure AD Premium services are not available.</span></span>

## <a name="microsoft-azure-government-cloud"></a><span data-ttu-id="a4bc9-118">Microsoft Azure Government cloud</span><span class="sxs-lookup"><span data-stu-id="a4bc9-118">Microsoft Azure Government cloud</span></span>
<span data-ttu-id="a4bc9-119">The [Microsoft Azure Government cloud](https://azure.microsoft.com/features/gov/) is a cloud for US government.</span><span class="sxs-lookup"><span data-stu-id="a4bc9-119">The [Microsoft Azure Government cloud](https://azure.microsoft.com/features/gov/) is a cloud for US government.</span></span>

<span data-ttu-id="a4bc9-120">This cloud has been supported by earlier releases of DirSync.</span><span class="sxs-lookup"><span data-stu-id="a4bc9-120">This cloud has been supported by earlier releases of DirSync.</span></span> <span data-ttu-id="a4bc9-121">From build 1.1.180 of Azure AD Connect, the next generation of the cloud is supported.</span><span class="sxs-lookup"><span data-stu-id="a4bc9-121">From build 1.1.180 of Azure AD Connect, the next generation of the cloud is supported.</span></span> <span data-ttu-id="a4bc9-122">This generation is using US-only based endpoints and have a different list of URLs to open in your proxy server.</span><span class="sxs-lookup"><span data-stu-id="a4bc9-122">This generation is using US-only based endpoints and have a different list of URLs to open in your proxy server.</span></span>

| <span data-ttu-id="a4bc9-123">URLs to open in proxy server</span><span class="sxs-lookup"><span data-stu-id="a4bc9-123">URLs to open in proxy server</span></span> |
| --- |
| <span data-ttu-id="a4bc9-124">\*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="a4bc9-124">\*.microsoftonline.com</span></span> |
| <span data-ttu-id="a4bc9-125">\*.gov.us.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="a4bc9-125">\*.gov.us.microsoftonline.com</span></span> |
| <span data-ttu-id="a4bc9-126">+Certificate Revocation Lists</span><span class="sxs-lookup"><span data-stu-id="a4bc9-126">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="a4bc9-127">Azure AD Connect is not able to automatically detect that your Azure AD tenant is located in the Government cloud.</span><span class="sxs-lookup"><span data-stu-id="a4bc9-127">Azure AD Connect is not able to automatically detect that your Azure AD tenant is located in the Government cloud.</span></span> <span data-ttu-id="a4bc9-128">Instead you need to take the following actions when you install Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="a4bc9-128">Instead you need to take the following actions when you install Azure AD Connect.</span></span>

1. <span data-ttu-id="a4bc9-129">Start the Azure AD Connect installation.</span><span class="sxs-lookup"><span data-stu-id="a4bc9-129">Start the Azure AD Connect installation.</span></span>
2. <span data-ttu-id="a4bc9-130">When you see the first page where you are supposed to accept the EULA, do not continue but leave the installation wizard running.</span><span class="sxs-lookup"><span data-stu-id="a4bc9-130">When you see the first page where you are supposed to accept the EULA, do not continue but leave the installation wizard running.</span></span>
3. <span data-ttu-id="a4bc9-131">Start regedit and change the registry key `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` to the value `2`.</span><span class="sxs-lookup"><span data-stu-id="a4bc9-131">Start regedit and change the registry key `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` to the value `2`.</span></span>
4. <span data-ttu-id="a4bc9-132">Go back to the Azure AD Connect installation wizard, accept the EULA, and continue.</span><span class="sxs-lookup"><span data-stu-id="a4bc9-132">Go back to the Azure AD Connect installation wizard, accept the EULA, and continue.</span></span> <span data-ttu-id="a4bc9-133">During installation, make sure to use the **custom configuration** installation path (and not Express installation).</span><span class="sxs-lookup"><span data-stu-id="a4bc9-133">During installation, make sure to use the **custom configuration** installation path (and not Express installation).</span></span> <span data-ttu-id="a4bc9-134">Then continue the installation as usual.</span><span class="sxs-lookup"><span data-stu-id="a4bc9-134">Then continue the installation as usual.</span></span>

<span data-ttu-id="a4bc9-135">Features currently not present in the Microsoft Azure Government cloud:</span><span class="sxs-lookup"><span data-stu-id="a4bc9-135">Features currently not present in the Microsoft Azure Government cloud:</span></span>

* <span data-ttu-id="a4bc9-136">**Azure AD Connect Health** is not available.</span><span class="sxs-lookup"><span data-stu-id="a4bc9-136">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="a4bc9-137">**Automatic updates** is not available.</span><span class="sxs-lookup"><span data-stu-id="a4bc9-137">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="a4bc9-138">**Password writeback** is not available.</span><span class="sxs-lookup"><span data-stu-id="a4bc9-138">**Password writeback** is not available.</span></span>
* <span data-ttu-id="a4bc9-139">Other Azure AD Premium services are not available.</span><span class="sxs-lookup"><span data-stu-id="a4bc9-139">Other Azure AD Premium services are not available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4bc9-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="a4bc9-140">Next steps</span></span>
<span data-ttu-id="a4bc9-141">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="a4bc9-141">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
