---
title: User provisioning to an Azure AD Gallery application is taking hours or more | Microsoft Docs
description: How to find out why provisioning to your application may be taking longer than you expected
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 07/11/2017
ms.author: barbkess
ms.reviewer: asteen
ms.openlocfilehash: 2b46fecc44803130e4f79667d0e083314c4419c2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857230"
---
# <a name="user-provisioning-to-an-azure-ad-gallery-application-is-taking-hours-or-more"></a><span data-ttu-id="8a1f3-103">User provisioning to an Azure AD Gallery application is taking hours or more</span><span class="sxs-lookup"><span data-stu-id="8a1f3-103">User provisioning to an Azure AD Gallery application is taking hours or more</span></span>

<span data-ttu-id="8a1f3-104">When first enabling automatic provisioning for an application, the initial sync can take anywhere from 20 minutes to several hours, depending on the size of the Azure AD directory and the number of users in scope for provisioning.</span><span class="sxs-lookup"><span data-stu-id="8a1f3-104">When first enabling automatic provisioning for an application, the initial sync can take anywhere from 20 minutes to several hours, depending on the size of the Azure AD directory and the number of users in scope for provisioning.</span></span> 

<span data-ttu-id="8a1f3-105">Subsequent syncs after the initial sync be faster, as the provisioning service stores watermarks that represent the state of both systems after the initial sync, improving performance of subsequent syncs.</span><span class="sxs-lookup"><span data-stu-id="8a1f3-105">Subsequent syncs after the initial sync be faster, as the provisioning service stores watermarks that represent the state of both systems after the initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-to-improve-provisioning-performance"></a><span data-ttu-id="8a1f3-106">How to improve provisioning performance</span><span class="sxs-lookup"><span data-stu-id="8a1f3-106">How to improve provisioning performance</span></span>

<span data-ttu-id="8a1f3-107">If the initial sync is taking more than a few hours, there is one thing you can do to improve performance:</span><span class="sxs-lookup"><span data-stu-id="8a1f3-107">If the initial sync is taking more than a few hours, there is one thing you can do to improve performance:</span></span>

-   <span data-ttu-id="8a1f3-108">**User scoping filters.**</span><span class="sxs-lookup"><span data-stu-id="8a1f3-108">**User scoping filters.**</span></span> <span data-ttu-id="8a1f3-109">Scoping filters allow you to fine tune the data that the provisioning service extracts from Azure AD by filtering out users based on specific attribute values.</span><span class="sxs-lookup"><span data-stu-id="8a1f3-109">Scoping filters allow you to fine tune the data that the provisioning service extracts from Azure AD by filtering out users based on specific attribute values.</span></span> <span data-ttu-id="8a1f3-110">For more information on scoping filters, see [Attribute-based application provisioning with scoping filters](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span><span class="sxs-lookup"><span data-stu-id="8a1f3-110">For more information on scoping filters, see [Attribute-based application provisioning with scoping filters](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a1f3-111">Next steps</span><span class="sxs-lookup"><span data-stu-id="8a1f3-111">Next steps</span></span>
[<span data-ttu-id="8a1f3-112">Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8a1f3-112">Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory</span></span>](user-provisioning.md)

