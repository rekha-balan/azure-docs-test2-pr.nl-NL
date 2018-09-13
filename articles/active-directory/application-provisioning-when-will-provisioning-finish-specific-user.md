---
title: Find out when a specific user will be able to access an application | Microsoft Docs
description: How to find out when a critically important user be able to access an application you have configured for user provisioning with Azure AD
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
ms.openlocfilehash: fe99a817f69465238ab71e71e049375fd8547a1f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564328"
---
# <a name="find-out-when-a-specific-user-will-be-able-to-access-an-application"></a><span data-ttu-id="3fd26-103">Find out when a specific user will be able to access an application</span><span class="sxs-lookup"><span data-stu-id="3fd26-103">Find out when a specific user will be able to access an application</span></span>
<span data-ttu-id="3fd26-104">When using automatic user provisioning with an application, Azure AD automatically provision and update user accounts in an app based on things like [user and group assignment](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) at a regularly scheduled time interval, typically every 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="3fd26-104">When using automatic user provisioning with an application, Azure AD automatically provision and update user accounts in an app based on things like [user and group assignment](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) at a regularly scheduled time interval, typically every 10 minutes.</span></span>

## <a name="how-long-does-it-take"></a><span data-ttu-id="3fd26-105">How long does it take?</span><span class="sxs-lookup"><span data-stu-id="3fd26-105">How long does it take?</span></span>

<span data-ttu-id="3fd26-106">The time it takes for a given user to be provisioned depends mainly on whether or not an initial “full” sync has already occurred.</span><span class="sxs-lookup"><span data-stu-id="3fd26-106">The time it takes for a given user to be provisioned depends mainly on whether or not an initial “full” sync has already occurred.</span></span>

<span data-ttu-id="3fd26-107">The first sync between Azure AD and an app can take anywhere from 20 minutes to several hours, depending on the size of the Azure AD directory and the number of users in scope for provisioning.</span><span class="sxs-lookup"><span data-stu-id="3fd26-107">The first sync between Azure AD and an app can take anywhere from 20 minutes to several hours, depending on the size of the Azure AD directory and the number of users in scope for provisioning.</span></span> 

<span data-ttu-id="3fd26-108">Subsequent syncs after the initial sync be faster (e.g. within 10 minutes), as the provisioning service stores watermarks that represent the state of both systems after the initial sync, improving performance of subsequent syncs.</span><span class="sxs-lookup"><span data-stu-id="3fd26-108">Subsequent syncs after the initial sync be faster (e.g. within 10 minutes), as the provisioning service stores watermarks that represent the state of both systems after the initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-to-check-the-status-of-a-user"></a><span data-ttu-id="3fd26-109">How to check the status of a user</span><span class="sxs-lookup"><span data-stu-id="3fd26-109">How to check the status of a user</span></span>

<span data-ttu-id="3fd26-110">To see the provisioning status for a selected user, consult the Audit logs in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3fd26-110">To see the provisioning status for a selected user, consult the Audit logs in Azure AD.</span></span>

<span data-ttu-id="3fd26-111">The provisioning audit logs can be accessed in the Azure portal, in the **Azure Active Directory &gt; Enterprise Apps &gt; \[Application Name\] &gt; Audit Logs** tab. Filter the logs on the **Account Provisioning** category to only see the provisioning events for that app.</span><span class="sxs-lookup"><span data-stu-id="3fd26-111">The provisioning audit logs can be accessed in the Azure portal, in the **Azure Active Directory &gt; Enterprise Apps &gt; \[Application Name\] &gt; Audit Logs** tab. Filter the logs on the **Account Provisioning** category to only see the provisioning events for that app.</span></span> <span data-ttu-id="3fd26-112">You can search for users based on the “matching ID” that was configured for them in the attribute mappings.</span><span class="sxs-lookup"><span data-stu-id="3fd26-112">You can search for users based on the “matching ID” that was configured for them in the attribute mappings.</span></span> 

<span data-ttu-id="3fd26-113">For example, if you configured the “user principal name” or “email address” as the matching attribute on the Azure AD side, and the user not being provisioning has a value of “audrey@contoso.com”, then search the audit logs for “audrey@contoso.com” and review then entries returned.</span><span class="sxs-lookup"><span data-stu-id="3fd26-113">For example, if you configured the “user principal name” or “email address” as the matching attribute on the Azure AD side, and the user not being provisioning has a value of “audrey@contoso.com”, then search the audit logs for “audrey@contoso.com” and review then entries returned.</span></span>

<span data-ttu-id="3fd26-114">The provisioning audit logs record all the operations performed by the provisioning service, including:</span><span class="sxs-lookup"><span data-stu-id="3fd26-114">The provisioning audit logs record all the operations performed by the provisioning service, including:</span></span>

* <span data-ttu-id="3fd26-115">Querying Azure AD for assigned users that are in scope for provisioning</span><span class="sxs-lookup"><span data-stu-id="3fd26-115">Querying Azure AD for assigned users that are in scope for provisioning</span></span>
* <span data-ttu-id="3fd26-116">Querying the target app for the existence of those users</span><span class="sxs-lookup"><span data-stu-id="3fd26-116">Querying the target app for the existence of those users</span></span>
* <span data-ttu-id="3fd26-117">Comparing the user objects between the system</span><span class="sxs-lookup"><span data-stu-id="3fd26-117">Comparing the user objects between the system</span></span>
* <span data-ttu-id="3fd26-118">Adding, updating, or disabling the user account in the target system based on the comparison</span><span class="sxs-lookup"><span data-stu-id="3fd26-118">Adding, updating, or disabling the user account in the target system based on the comparison</span></span>

## <a name="next-steps"></a><span data-ttu-id="3fd26-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="3fd26-119">Next steps</span></span>
<span data-ttu-id="3fd26-120">[Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''</span><span class="sxs-lookup"><span data-stu-id="3fd26-120">[Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''</span></span>
