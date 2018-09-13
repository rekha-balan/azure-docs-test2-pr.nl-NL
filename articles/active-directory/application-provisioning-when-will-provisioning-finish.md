---
title: User provisioning to an Azure AD Gallery application is taking hours or more | Microsoft Docs
description: How to find out why provisioning to your application may be taking longer than you expected
services: active-directory
documentationcenter: ''
author: ajamess
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: asteen
ms.openlocfilehash: 0bb8d24b99fedd6722c9e6e78aaa9c0eee09ad54
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553741"
---
# <a name="user-provisioning-to-an-azure-ad-gallery-application-is-taking-hours-or-more"></a><span data-ttu-id="bf708-103">User provisioning to an Azure AD Gallery application is taking hours or more</span><span class="sxs-lookup"><span data-stu-id="bf708-103">User provisioning to an Azure AD Gallery application is taking hours or more</span></span>

<span data-ttu-id="bf708-104">When first enabling automatic provisioning for an application, the initial sync can take anywhere from 20 minutes to several hours, depending on the size of the Azure AD directory and the number of users in scope for provisioning.</span><span class="sxs-lookup"><span data-stu-id="bf708-104">When first enabling automatic provisioning for an application, the initial sync can take anywhere from 20 minutes to several hours, depending on the size of the Azure AD directory and the number of users in scope for provisioning.</span></span> 

<span data-ttu-id="bf708-105">Subsequent syncs after the initial sync be faster, as the provisioning service stores watermarks that represent the state of both systems after the initial sync, improving performance of subsequent syncs.</span><span class="sxs-lookup"><span data-stu-id="bf708-105">Subsequent syncs after the initial sync be faster, as the provisioning service stores watermarks that represent the state of both systems after the initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-to-improve-provisioning-performance"></a><span data-ttu-id="bf708-106">How to improve provisioning performance</span><span class="sxs-lookup"><span data-stu-id="bf708-106">How to improve provisioning performance</span></span>

<span data-ttu-id="bf708-107">If the initial sync is taking more than a few hours, there is one thing you can do to improve performance:</span><span class="sxs-lookup"><span data-stu-id="bf708-107">If the initial sync is taking more than a few hours, there is one thing you can do to improve performance:</span></span>

-   <span data-ttu-id="bf708-108">**User scoping filters.**</span><span class="sxs-lookup"><span data-stu-id="bf708-108">**User scoping filters.**</span></span> <span data-ttu-id="bf708-109">Scoping filters allow you to fine tune the data that the provisioning service extracts from Azure AD by filtering out users based on specific attribute values.</span><span class="sxs-lookup"><span data-stu-id="bf708-109">Scoping filters allow you to fine tune the data that the provisioning service extracts from Azure AD by filtering out users based on specific attribute values.</span></span> <span data-ttu-id="bf708-110">For more information on scoping filters, see [Attribute-based application provisioning with scoping filters](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span><span class="sxs-lookup"><span data-stu-id="bf708-110">For more information on scoping filters, see [Attribute-based application provisioning with scoping filters](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf708-111">Next steps</span><span class="sxs-lookup"><span data-stu-id="bf708-111">Next steps</span></span>
[<span data-ttu-id="bf708-112">Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bf708-112">Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory</span></span>](active-directory-saas-app-provisioning.md)

