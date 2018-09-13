---
title: Characteristics of Azure Active Directory directories | Microsoft Docs
description: Manage your Azure Active Directory directories by understanding your directories as fully independent resources
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: 2b862b75-14df-45f2-a8ab-2a3ff1e2eb08
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5ec00d5e8380f121dd9302cf08a0708c530aab9b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564104"
---
# <a name="understand-how-multiple-azure-active-directory-directories-interact"></a><span data-ttu-id="2a060-103">Understand how multiple Azure Active Directory directories interact</span><span class="sxs-lookup"><span data-stu-id="2a060-103">Understand how multiple Azure Active Directory directories interact</span></span>
<span data-ttu-id="2a060-104">In Azure Active Directory (Azure AD), each directory is a fully independent resource: a peer, fully-featured, and logically independent of other directories that you manage.</span><span class="sxs-lookup"><span data-stu-id="2a060-104">In Azure Active Directory (Azure AD), each directory is a fully independent resource: a peer, fully-featured, and logically independent of other directories that you manage.</span></span> <span data-ttu-id="2a060-105">There is no parent-child relationship between directories.</span><span class="sxs-lookup"><span data-stu-id="2a060-105">There is no parent-child relationship between directories.</span></span> <span data-ttu-id="2a060-106">This independence between directories includes resource independence, administrative independence, and synchronization independence.</span><span class="sxs-lookup"><span data-stu-id="2a060-106">This independence between directories includes resource independence, administrative independence, and synchronization independence.</span></span>

## <a name="resource-independence"></a><span data-ttu-id="2a060-107">Resource independence</span><span class="sxs-lookup"><span data-stu-id="2a060-107">Resource independence</span></span>
<span data-ttu-id="2a060-108">If you create or delete a resource in one directory, it has no impact on any resource in another directory, with the partial exception of external users, described below.</span><span class="sxs-lookup"><span data-stu-id="2a060-108">If you create or delete a resource in one directory, it has no impact on any resource in another directory, with the partial exception of external users, described below.</span></span> <span data-ttu-id="2a060-109">If you use a custom domain 'contoso.com' with one directory, it cannot be used with any other directory.</span><span class="sxs-lookup"><span data-stu-id="2a060-109">If you use a custom domain 'contoso.com' with one directory, it cannot be used with any other directory.</span></span>

## <a name="administrative-independence"></a><span data-ttu-id="2a060-110">Administrative independence</span><span class="sxs-lookup"><span data-stu-id="2a060-110">Administrative independence</span></span>
<span data-ttu-id="2a060-111">If a non-administrative user of directory 'Contoso' creates a test directory 'Test' then:</span><span class="sxs-lookup"><span data-stu-id="2a060-111">If a non-administrative user of directory 'Contoso' creates a test directory 'Test' then:</span></span>

* <span data-ttu-id="2a060-112">By default, the user who creates a directory is added as an external user in that new directory, and assigned the global administrator role in that directory.</span><span class="sxs-lookup"><span data-stu-id="2a060-112">By default, the user who creates a directory is added as an external user in that new directory, and assigned the global administrator role in that directory.</span></span>
* <span data-ttu-id="2a060-113">The administrators of directory 'Contoso' have no direct administrative privileges to directory 'Test' unless an administrator of 'Test' specifically grants them these privileges.</span><span class="sxs-lookup"><span data-stu-id="2a060-113">The administrators of directory 'Contoso' have no direct administrative privileges to directory 'Test' unless an administrator of 'Test' specifically grants them these privileges.</span></span> <span data-ttu-id="2a060-114">Administrators of 'Contoso' can control access to directory 'Test' if they control the user account which created 'Test.'</span><span class="sxs-lookup"><span data-stu-id="2a060-114">Administrators of 'Contoso' can control access to directory 'Test' if they control the user account which created 'Test.'</span></span>
* <span data-ttu-id="2a060-115">If you change (add or remove) an administrator role for a user in one directory, the change does not affect any administrator role that the user might have in another directory.</span><span class="sxs-lookup"><span data-stu-id="2a060-115">If you change (add or remove) an administrator role for a user in one directory, the change does not affect any administrator role that the user might have in another directory.</span></span>

## <a name="synchronization-independence"></a><span data-ttu-id="2a060-116">Synchronization independence</span><span class="sxs-lookup"><span data-stu-id="2a060-116">Synchronization independence</span></span>
<span data-ttu-id="2a060-117">You can configure each Azure AD directory independently to get data synchronized from a single instance of either:</span><span class="sxs-lookup"><span data-stu-id="2a060-117">You can configure each Azure AD directory independently to get data synchronized from a single instance of either:</span></span>

* <span data-ttu-id="2a060-118">The Directory Synchronization (DirSync) tool, to synchronize data with a single AD forest.</span><span class="sxs-lookup"><span data-stu-id="2a060-118">The Directory Synchronization (DirSync) tool, to synchronize data with a single AD forest.</span></span>
* <span data-ttu-id="2a060-119">The Azure Active Directory Connector for Forefront Identity Manager, to synchronize data with one or more on-premises forests, and/or non-Azure AD data sources.</span><span class="sxs-lookup"><span data-stu-id="2a060-119">The Azure Active Directory Connector for Forefront Identity Manager, to synchronize data with one or more on-premises forests, and/or non-Azure AD data sources.</span></span>

## <a name="add-an-azure-ad-directory"></a><span data-ttu-id="2a060-120">Add an Azure AD directory</span><span class="sxs-lookup"><span data-stu-id="2a060-120">Add an Azure AD directory</span></span>
<span data-ttu-id="2a060-121">To add an Azure AD directory in the Azure classic portal, select the Azure Active Directory extension on the left and tap **Add**.</span><span class="sxs-lookup"><span data-stu-id="2a060-121">To add an Azure AD directory in the Azure classic portal, select the Azure Active Directory extension on the left and tap **Add**.</span></span>

> [!NOTE]
> <span data-ttu-id="2a060-122">Unlike other Azure resources, your directories are not child resources of an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="2a060-122">Unlike other Azure resources, your directories are not child resources of an Azure subscription.</span></span> <span data-ttu-id="2a060-123">If you cancel or allow your Azure subscription to expire, you can still access your directory data using Azure PowerShell, the Azure Graph API, or other interfaces such as the Office 365 Admin Center.</span><span class="sxs-lookup"><span data-stu-id="2a060-123">If you cancel or allow your Azure subscription to expire, you can still access your directory data using Azure PowerShell, the Azure Graph API, or other interfaces such as the Office 365 Admin Center.</span></span> <span data-ttu-id="2a060-124">You can also associate another subscription with the directory.</span><span class="sxs-lookup"><span data-stu-id="2a060-124">You can also associate another subscription with the directory.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="2a060-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="2a060-125">Next steps</span></span>
<span data-ttu-id="2a060-126">For a broad overview of Azure AD licensing issues and best practices, see [What is Azure Active Directory licensing?](active-directory-licensing-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="2a060-126">For a broad overview of Azure AD licensing issues and best practices, see [What is Azure Active Directory licensing?](active-directory-licensing-what-is.md).</span></span>
