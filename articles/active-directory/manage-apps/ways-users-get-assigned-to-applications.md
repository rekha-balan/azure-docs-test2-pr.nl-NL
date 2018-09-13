---
title: How to Assign users to applications | Microsoft Docs
description: Understand how users get assigned to an application in your tenant
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
ms.topic: article
ms.date: 07/11/2017
ms.author: barbkess
ms.openlocfilehash: 2301c2eee2853617251053713b50f9915962027b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856384"
---
# <a name="how-to-assign-users-to-applications"></a><span data-ttu-id="32f68-103">How to assign users to applications</span><span class="sxs-lookup"><span data-stu-id="32f68-103">How to assign users to applications</span></span>

<span data-ttu-id="32f68-104">This article help you to understand how users get assigned to an application in your tenant.</span><span class="sxs-lookup"><span data-stu-id="32f68-104">This article help you to understand how users get assigned to an application in your tenant.</span></span>

## <a name="how-do-users-get-assigned-to-an-application-in-azure-ad"></a><span data-ttu-id="32f68-105">How do users get assigned to an application in Azure AD?</span><span class="sxs-lookup"><span data-stu-id="32f68-105">How do users get assigned to an application in Azure AD?</span></span>

<span data-ttu-id="32f68-106">For a user to access an application, they must first be assigned to it in some way.</span><span class="sxs-lookup"><span data-stu-id="32f68-106">For a user to access an application, they must first be assigned to it in some way.</span></span> <span data-ttu-id="32f68-107">Assignment can be performed by an administrator, a business delegate, or sometimes, the user themselves.</span><span class="sxs-lookup"><span data-stu-id="32f68-107">Assignment can be performed by an administrator, a business delegate, or sometimes, the user themselves.</span></span> <span data-ttu-id="32f68-108">Below describes the ways users can get assigned to applications:</span><span class="sxs-lookup"><span data-stu-id="32f68-108">Below describes the ways users can get assigned to applications:</span></span>

1.  <span data-ttu-id="32f68-109">An administrator [assigns a user](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) to the application directly</span><span class="sxs-lookup"><span data-stu-id="32f68-109">An administrator [assigns a user](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) to the application directly</span></span>

2.  <span data-ttu-id="32f68-110">An administrator [assigns a group](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) that the user is a member of to the application, including:</span><span class="sxs-lookup"><span data-stu-id="32f68-110">An administrator [assigns a group](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) that the user is a member of to the application, including:</span></span>

  * <span data-ttu-id="32f68-111">A group that was synchronized from on-premises</span><span class="sxs-lookup"><span data-stu-id="32f68-111">A group that was synchronized from on-premises</span></span>

  * <span data-ttu-id="32f68-112">A static security group created in the cloud</span><span class="sxs-lookup"><span data-stu-id="32f68-112">A static security group created in the cloud</span></span>

  * <span data-ttu-id="32f68-113">A [dynamic security group](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) created in the cloud</span><span class="sxs-lookup"><span data-stu-id="32f68-113">A [dynamic security group](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) created in the cloud</span></span>

  * <span data-ttu-id="32f68-114">An Office 365 group created in the cloud</span><span class="sxs-lookup"><span data-stu-id="32f68-114">An Office 365 group created in the cloud</span></span>

  * <span data-ttu-id="32f68-115">The [All Users](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) group</span><span class="sxs-lookup"><span data-stu-id="32f68-115">The [All Users](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) group</span></span>

3.  <span data-ttu-id="32f68-116">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to allow a user to add an application using the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature **without business approval**</span><span class="sxs-lookup"><span data-stu-id="32f68-116">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to allow a user to add an application using the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature **without business approval**</span></span>

4.  <span data-ttu-id="32f68-117">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to allow a user to add an application using the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature, but only w**ith prior approval from a selected set of business approvers**</span><span class="sxs-lookup"><span data-stu-id="32f68-117">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to allow a user to add an application using the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature, but only w**ith prior approval from a selected set of business approvers**</span></span>

5.  <span data-ttu-id="32f68-118">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) to allow a user to join a group that an application is assigned to **without business approval**</span><span class="sxs-lookup"><span data-stu-id="32f68-118">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) to allow a user to join a group that an application is assigned to **without business approval**</span></span>

6.  <span data-ttu-id="32f68-119">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) to allow a user to join a group that an application is assigned to, but only **with prior approval from a selected set of business approvers**</span><span class="sxs-lookup"><span data-stu-id="32f68-119">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) to allow a user to join a group that an application is assigned to, but only **with prior approval from a selected set of business approvers**</span></span>

7.  <span data-ttu-id="32f68-120">An administrator assigns a license to a user directly for a first party application, like [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="32f68-120">An administrator assigns a license to a user directly for a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

8.  <span data-ttu-id="32f68-121">An administrator assigns a license to a group that the user is a member of to a first party application, like [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="32f68-121">An administrator assigns a license to a group that the user is a member of to a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

9.  <span data-ttu-id="32f68-122">An [administrator consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) to be used by all users and then a user signs in to the application</span><span class="sxs-lookup"><span data-stu-id="32f68-122">An [administrator consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) to be used by all users and then a user signs in to the application</span></span>

10. <span data-ttu-id="32f68-123">A user [consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) themselves by signing in to the application</span><span class="sxs-lookup"><span data-stu-id="32f68-123">A user [consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) themselves by signing in to the application</span></span>

## <a name="next-steps"></a><span data-ttu-id="32f68-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="32f68-124">Next steps</span></span>
[<span data-ttu-id="32f68-125">Managing Applications with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="32f68-125">Managing Applications with Azure Active Directory</span></span>](what-is-application-management.md)
