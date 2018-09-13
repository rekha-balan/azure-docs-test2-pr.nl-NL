---
title: How to Assign users to applications | Microsoft Docs
description: Understand how users get assigned to an application in your tenant
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
ms.openlocfilehash: 43ed4b0e96c583d8fd9da57eec40ddd2e96fee2f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553732"
---
# <a name="how-to-assign-users-to-applications"></a><span data-ttu-id="4bf99-103">How to assign users to applications</span><span class="sxs-lookup"><span data-stu-id="4bf99-103">How to assign users to applications</span></span>

<span data-ttu-id="4bf99-104">This article help you to understand how users get assigned to an application in your tenant.</span><span class="sxs-lookup"><span data-stu-id="4bf99-104">This article help you to understand how users get assigned to an application in your tenant.</span></span>

## <a name="how-do-users-get-assigned-to-an-application-in-azure-ad"></a><span data-ttu-id="4bf99-105">How do users get assigned to an application in Azure AD?</span><span class="sxs-lookup"><span data-stu-id="4bf99-105">How do users get assigned to an application in Azure AD?</span></span>

<span data-ttu-id="4bf99-106">For a user to access an application, they must first be assigned to it in some way.</span><span class="sxs-lookup"><span data-stu-id="4bf99-106">For a user to access an application, they must first be assigned to it in some way.</span></span> <span data-ttu-id="4bf99-107">Assignment can be performed by an administrator, a business delegate, or sometimes, the user themselves.</span><span class="sxs-lookup"><span data-stu-id="4bf99-107">Assignment can be performed by an administrator, a business delegate, or sometimes, the user themselves.</span></span> <span data-ttu-id="4bf99-108">Below describes the ways users can get assigned to applications:</span><span class="sxs-lookup"><span data-stu-id="4bf99-108">Below describes the ways users can get assigned to applications:</span></span>

1.  <span data-ttu-id="4bf99-109">An administrator [assigns a user](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) to the application directly</span><span class="sxs-lookup"><span data-stu-id="4bf99-109">An administrator [assigns a user](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) to the application directly</span></span>

2.  <span data-ttu-id="4bf99-110">An administrator [assigns a group](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) that the user is a member of to the application, including:</span><span class="sxs-lookup"><span data-stu-id="4bf99-110">An administrator [assigns a group](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) that the user is a member of to the application, including:</span></span>

  * <span data-ttu-id="4bf99-111">A group that was synchronized from on-premises</span><span class="sxs-lookup"><span data-stu-id="4bf99-111">A group that was synchronized from on-premises</span></span>

  * <span data-ttu-id="4bf99-112">A static security group created in the cloud</span><span class="sxs-lookup"><span data-stu-id="4bf99-112">A static security group created in the cloud</span></span>

  * <span data-ttu-id="4bf99-113">A [dynamic security group](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) created in the cloud</span><span class="sxs-lookup"><span data-stu-id="4bf99-113">A [dynamic security group](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) created in the cloud</span></span>

  * <span data-ttu-id="4bf99-114">An Office 365 group created in the cloud</span><span class="sxs-lookup"><span data-stu-id="4bf99-114">An Office 365 group created in the cloud</span></span>

  * <span data-ttu-id="4bf99-115">The [All Users](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) group</span><span class="sxs-lookup"><span data-stu-id="4bf99-115">The [All Users](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) group</span></span>

3.  <span data-ttu-id="4bf99-116">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to allow a user to add an application using the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature **without business approval**</span><span class="sxs-lookup"><span data-stu-id="4bf99-116">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to allow a user to add an application using the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature **without business approval**</span></span>

4.  <span data-ttu-id="4bf99-117">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to allow a user to add an application using the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature, but only w**ith prior approval from a selected set of business approvers**</span><span class="sxs-lookup"><span data-stu-id="4bf99-117">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to allow a user to add an application using the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature, but only w**ith prior approval from a selected set of business approvers**</span></span>

5.  <span data-ttu-id="4bf99-118">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) to allow a user to join a group that an application is assigned to **without business approval**</span><span class="sxs-lookup"><span data-stu-id="4bf99-118">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) to allow a user to join a group that an application is assigned to **without business approval**</span></span>

6.  <span data-ttu-id="4bf99-119">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) to allow a user to join a group that an application is assigned to, but only **with prior approval from a selected set of business approvers**</span><span class="sxs-lookup"><span data-stu-id="4bf99-119">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) to allow a user to join a group that an application is assigned to, but only **with prior approval from a selected set of business approvers**</span></span>

7.  <span data-ttu-id="4bf99-120">An administrator assigns a license to a user directly for a first party application, like [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="4bf99-120">An administrator assigns a license to a user directly for a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

8.  <span data-ttu-id="4bf99-121">An administrator assigns a license to a group that the user is a member of to a first party application, like [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="4bf99-121">An administrator assigns a license to a group that the user is a member of to a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

9.  <span data-ttu-id="4bf99-122">An [administrator consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) to be used by all users and then a user signs in to the application</span><span class="sxs-lookup"><span data-stu-id="4bf99-122">An [administrator consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) to be used by all users and then a user signs in to the application</span></span>

10. <span data-ttu-id="4bf99-123">A user [consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) themselves by signing in to the application</span><span class="sxs-lookup"><span data-stu-id="4bf99-123">A user [consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) themselves by signing in to the application</span></span>

## <a name="next-steps"></a><span data-ttu-id="4bf99-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="4bf99-124">Next steps</span></span>
[<span data-ttu-id="4bf99-125">Managing Applications with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4bf99-125">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
