---
title: Administrative units management in Azure Active Directory
description: Using administrative units for more granular delegation of permissions in Azure Active Directory
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: 8464cd6b-1d1a-470d-a4fb-ee29b8eab4c4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/13/2017
ms.author: curtand
ms.openlocfilehash: 5d4e7cb2f54eec76f8d3b8d0329c07ae389bf9fb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662174"
---
# <a name="administrative-units-management-in-azure-ad---public-preview"></a><span data-ttu-id="3cdda-103">Administrative units management in Azure AD - Public Preview</span><span class="sxs-lookup"><span data-stu-id="3cdda-103">Administrative units management in Azure AD - Public Preview</span></span>
<span data-ttu-id="3cdda-104">This article describes administrative units – a new Azure Active Directory container of resources that can be used for delegating administrative permissions over subsets of users and applying policies to a subset of users.</span><span class="sxs-lookup"><span data-stu-id="3cdda-104">This article describes administrative units – a new Azure Active Directory container of resources that can be used for delegating administrative permissions over subsets of users and applying policies to a subset of users.</span></span> <span data-ttu-id="3cdda-105">In Azure Active Directory, administrative units enable central administrators to delegate permissions to regional administrators or to set policy at a granular level.</span><span class="sxs-lookup"><span data-stu-id="3cdda-105">In Azure Active Directory, administrative units enable central administrators to delegate permissions to regional administrators or to set policy at a granular level.</span></span>

<span data-ttu-id="3cdda-106">This is useful in organizations with independent divisions, for example, a large university that is made up of many autonomous schools (Business school, Engineering school, and so on) which are independent from each other.</span><span class="sxs-lookup"><span data-stu-id="3cdda-106">This is useful in organizations with independent divisions, for example, a large university that is made up of many autonomous schools (Business school, Engineering school, and so on) which are independent from each other.</span></span> <span data-ttu-id="3cdda-107">Such divisions have their own IT administrators who control access, manage users, and set policies specifically for their division.</span><span class="sxs-lookup"><span data-stu-id="3cdda-107">Such divisions have their own IT administrators who control access, manage users, and set policies specifically for their division.</span></span> <span data-ttu-id="3cdda-108">Central administrators want to be able grant these divisional administrators permissions over the users in their particular divisions.</span><span class="sxs-lookup"><span data-stu-id="3cdda-108">Central administrators want to be able grant these divisional administrators permissions over the users in their particular divisions.</span></span> <span data-ttu-id="3cdda-109">More specifically, using this example, a central administrator can, for instance, create an administrative unit for a particular school (Business school) and populate it with only the Business school users.</span><span class="sxs-lookup"><span data-stu-id="3cdda-109">More specifically, using this example, a central administrator can, for instance, create an administrative unit for a particular school (Business school) and populate it with only the Business school users.</span></span> <span data-ttu-id="3cdda-110">Then a central administrator can add the Business school IT staff to a scoped role, in other words, grant the IT staff of Business school administrative permissions only over the Business school administrative unit.</span><span class="sxs-lookup"><span data-stu-id="3cdda-110">Then a central administrator can add the Business school IT staff to a scoped role, in other words, grant the IT staff of Business school administrative permissions only over the Business school administrative unit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3cdda-111">You can create and use administrative units only if you enable Azure Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="3cdda-111">You can create and use administrative units only if you enable Azure Active Directory Premium.</span></span> <span data-ttu-id="3cdda-112">For more information, see [Getting started with Azure AD Premium](active-directory-get-started-premium.md).</span><span class="sxs-lookup"><span data-stu-id="3cdda-112">For more information, see [Getting started with Azure AD Premium](active-directory-get-started-premium.md).</span></span>
>
>

<span data-ttu-id="3cdda-113">From the central administrator’s point of view, an administrative unit is a directory object that can be created and populated with resources.</span><span class="sxs-lookup"><span data-stu-id="3cdda-113">From the central administrator’s point of view, an administrative unit is a directory object that can be created and populated with resources.</span></span> <span data-ttu-id="3cdda-114">**In this release, these resources can be only users.**</span><span class="sxs-lookup"><span data-stu-id="3cdda-114">**In this release, these resources can be only users.**</span></span> <span data-ttu-id="3cdda-115">Once created and populated, the administrative unit can be used as a scope to restrict the granted permission only over resources contained in the administrative unit.</span><span class="sxs-lookup"><span data-stu-id="3cdda-115">Once created and populated, the administrative unit can be used as a scope to restrict the granted permission only over resources contained in the administrative unit.</span></span>

## <a name="managing-administrative-units"></a><span data-ttu-id="3cdda-116">Managing administrative units</span><span class="sxs-lookup"><span data-stu-id="3cdda-116">Managing administrative units</span></span>
<span data-ttu-id="3cdda-117">In this preview release, you can create and manage administrative units using the Azure Active Directory Module for Windows PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="3cdda-117">In this preview release, you can create and manage administrative units using the Azure Active Directory Module for Windows PowerShell cmdlets.</span></span>

<span data-ttu-id="3cdda-118">For more information on software requirements and installing the Azure AD module, and for information on the Azure AD Module cmdlets for managing administrative units, including syntax, parameter descriptions, and examples, see [Manage Azure AD using Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx).</span><span class="sxs-lookup"><span data-stu-id="3cdda-118">For more information on software requirements and installing the Azure AD module, and for information on the Azure AD Module cmdlets for managing administrative units, including syntax, parameter descriptions, and examples, see [Manage Azure AD using Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3cdda-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="3cdda-119">Next steps</span></span>
[<span data-ttu-id="3cdda-120">Azure Active Directory editions</span><span class="sxs-lookup"><span data-stu-id="3cdda-120">Azure Active Directory editions</span></span>](active-directory-editions.md)
