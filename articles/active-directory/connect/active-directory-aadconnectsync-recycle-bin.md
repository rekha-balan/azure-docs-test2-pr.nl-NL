---
title: 'Azure AD Connect sync: Enable AD recycle bin | Microsoft Docs'
description: This topic recommends the use of AD Recycle Bin feature with Azure AD Connect.
services: active-directory
keywords: AD Recycle Bin, accidental deletion, source anchor
documentationcenter: ''
author: cychua
manager: femila
editor: ''
ms.assetid: afec4207-74f7-4cdd-b13a-574af5223a90
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: billmath
ms.openlocfilehash: 9778db69e94e9f1d033cc8c16fdb9554df3eddcc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661826"
---
# <a name="azure-ad-connect-sync-enable-ad-recycle-bin"></a><span data-ttu-id="90fcc-104">Azure AD Connect sync: Enable AD recycle bin</span><span class="sxs-lookup"><span data-stu-id="90fcc-104">Azure AD Connect sync: Enable AD recycle bin</span></span>
<span data-ttu-id="90fcc-105">It is recommended that you enable the AD Recycle Bin feature for your on-premises Active Directories, which are synchronized to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="90fcc-105">It is recommended that you enable the AD Recycle Bin feature for your on-premises Active Directories, which are synchronized to Azure AD.</span></span> 

<span data-ttu-id="90fcc-106">If you accidentally deleted an on-premises AD user object and restore it using the feature, Azure AD restores the corresponding Azure AD user object.</span><span class="sxs-lookup"><span data-stu-id="90fcc-106">If you accidentally deleted an on-premises AD user object and restore it using the feature, Azure AD restores the corresponding Azure AD user object.</span></span>  <span data-ttu-id="90fcc-107">For information about the AD Recycle Bin feature, refer to article [Scenario Overview for Restoring Deleted Active Directory Objects](https://technet.microsoft.com/library/dd379542.aspx).</span><span class="sxs-lookup"><span data-stu-id="90fcc-107">For information about the AD Recycle Bin feature, refer to article [Scenario Overview for Restoring Deleted Active Directory Objects](https://technet.microsoft.com/library/dd379542.aspx).</span></span>

## <a name="benefits-of-enabling-the-ad-recycle-bin"></a><span data-ttu-id="90fcc-108">Benefits of enabling the AD recycle bin</span><span class="sxs-lookup"><span data-stu-id="90fcc-108">Benefits of enabling the AD recycle bin</span></span>
<span data-ttu-id="90fcc-109">This feature helps with restoring Azure AD user objects by doing the following:</span><span class="sxs-lookup"><span data-stu-id="90fcc-109">This feature helps with restoring Azure AD user objects by doing the following:</span></span>

* <span data-ttu-id="90fcc-110">If you accidentally deleted an on-premises AD user object, the corresponding Azure AD user object will be deleted in the next sync cycle.</span><span class="sxs-lookup"><span data-stu-id="90fcc-110">If you accidentally deleted an on-premises AD user object, the corresponding Azure AD user object will be deleted in the next sync cycle.</span></span> <span data-ttu-id="90fcc-111">By default, Azure AD keeps the deleted Azure AD user object in soft-deleted state for 30 days.</span><span class="sxs-lookup"><span data-stu-id="90fcc-111">By default, Azure AD keeps the deleted Azure AD user object in soft-deleted state for 30 days.</span></span>

* <span data-ttu-id="90fcc-112">If you have on-premises AD Recycle Bin feature enabled, you can restore the deleted on-premises AD user object without changing its Source Anchor value.</span><span class="sxs-lookup"><span data-stu-id="90fcc-112">If you have on-premises AD Recycle Bin feature enabled, you can restore the deleted on-premises AD user object without changing its Source Anchor value.</span></span> <span data-ttu-id="90fcc-113">When the recovered on-premises AD user object is synchronized to Azure AD, Azure AD will restore the corresponding soft-deleted Azure AD user object.</span><span class="sxs-lookup"><span data-stu-id="90fcc-113">When the recovered on-premises AD user object is synchronized to Azure AD, Azure AD will restore the corresponding soft-deleted Azure AD user object.</span></span> <span data-ttu-id="90fcc-114">For information about Source Anchor attribute, refer to article [Azure AD Connect: Design concepts](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span><span class="sxs-lookup"><span data-stu-id="90fcc-114">For information about Source Anchor attribute, refer to article [Azure AD Connect: Design concepts](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span></span>

* <span data-ttu-id="90fcc-115">If you do not have on-premises AD Recycle Bin feature enabled, you may be required to create an AD user object to replace the deleted object.</span><span class="sxs-lookup"><span data-stu-id="90fcc-115">If you do not have on-premises AD Recycle Bin feature enabled, you may be required to create an AD user object to replace the deleted object.</span></span> <span data-ttu-id="90fcc-116">If Azure AD Connect Synchronization Service is configured to use system-generated AD attribute (such as ObjectGuid) for the Source Anchor attribute, the newly created AD user object will not have the same Source Anchor value as the deleted AD user object.</span><span class="sxs-lookup"><span data-stu-id="90fcc-116">If Azure AD Connect Synchronization Service is configured to use system-generated AD attribute (such as ObjectGuid) for the Source Anchor attribute, the newly created AD user object will not have the same Source Anchor value as the deleted AD user object.</span></span> <span data-ttu-id="90fcc-117">When the newly created AD user object is synchronized to Azure AD, Azure AD creates a new Azure AD user object instead of restoring the soft-deleted Azure AD user object.</span><span class="sxs-lookup"><span data-stu-id="90fcc-117">When the newly created AD user object is synchronized to Azure AD, Azure AD creates a new Azure AD user object instead of restoring the soft-deleted Azure AD user object.</span></span>

> [!NOTE]
> <span data-ttu-id="90fcc-118">By default, Azure AD keeps deleted Azure AD user objects in soft-deleted state for 30 days before they are permanently deleted.</span><span class="sxs-lookup"><span data-stu-id="90fcc-118">By default, Azure AD keeps deleted Azure AD user objects in soft-deleted state for 30 days before they are permanently deleted.</span></span> <span data-ttu-id="90fcc-119">However, administrators can accelerate the deletion of such objects.</span><span class="sxs-lookup"><span data-stu-id="90fcc-119">However, administrators can accelerate the deletion of such objects.</span></span> <span data-ttu-id="90fcc-120">Once the objects are permanently deleted, they can no longer be recovered, even if on-premises AD Recycle Bin feature is enabled.</span><span class="sxs-lookup"><span data-stu-id="90fcc-120">Once the objects are permanently deleted, they can no longer be recovered, even if on-premises AD Recycle Bin feature is enabled.</span></span>



## <a name="next-steps"></a><span data-ttu-id="90fcc-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="90fcc-121">Next steps</span></span>
<span data-ttu-id="90fcc-122">**Overview topics**</span><span class="sxs-lookup"><span data-stu-id="90fcc-122">**Overview topics**</span></span>

* [<span data-ttu-id="90fcc-123">Azure AD Connect sync: Understand and customize synchronization</span><span class="sxs-lookup"><span data-stu-id="90fcc-123">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="90fcc-124">Integrating your on-premises identities with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="90fcc-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)