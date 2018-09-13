---
title: Permissions in Azure Security Center | Microsoft Docs
description: This article explains how Azure Security Center uses role-based access control to assign permissions to users and identifies the allowed actions for each role.
services: security-center
cloud: na
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
ms.assetid: ''
ms.service: security-center
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2016
ms.author: terrylan
ms.openlocfilehash: d1c8a39bbcda7d22fdce08d122098e994ca87451
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554071"
---
# <a name="permissions-in-azure-security-center"></a><span data-ttu-id="6c443-103">Permissions in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="6c443-103">Permissions in Azure Security Center</span></span>

<span data-ttu-id="6c443-104">Azure Security Center uses [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md), which provides [built-in roles](../active-directory/role-based-access-built-in-roles.md) that can be assigned to users, groups, and services in Azure.</span><span class="sxs-lookup"><span data-stu-id="6c443-104">Azure Security Center uses [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md), which provides [built-in roles](../active-directory/role-based-access-built-in-roles.md) that can be assigned to users, groups, and services in Azure.</span></span>

<span data-ttu-id="6c443-105">Security Center assesses the configuration of your resources to identify security issues and vulnerabilities.</span><span class="sxs-lookup"><span data-stu-id="6c443-105">Security Center assesses the configuration of your resources to identify security issues and vulnerabilities.</span></span> <span data-ttu-id="6c443-106">In Security Center, you only see information related to a resource when you are assigned the role of Owner, Contributor, or Reader for the subscription or resource group that a resource belongs to.</span><span class="sxs-lookup"><span data-stu-id="6c443-106">In Security Center, you only see information related to a resource when you are assigned the role of Owner, Contributor, or Reader for the subscription or resource group that a resource belongs to.</span></span>

## <a name="roles-and-allowed-actions"></a><span data-ttu-id="6c443-107">Roles and allowed actions</span><span class="sxs-lookup"><span data-stu-id="6c443-107">Roles and allowed actions</span></span>

<span data-ttu-id="6c443-108">The following table displays roles and allowed actions in Security Center.</span><span class="sxs-lookup"><span data-stu-id="6c443-108">The following table displays roles and allowed actions in Security Center.</span></span> <span data-ttu-id="6c443-109">An X indicates that the action is allowed for that role.</span><span class="sxs-lookup"><span data-stu-id="6c443-109">An X indicates that the action is allowed for that role.</span></span>

| <span data-ttu-id="6c443-110">Role</span><span class="sxs-lookup"><span data-stu-id="6c443-110">Role</span></span> | <span data-ttu-id="6c443-111">Edit security policy</span><span class="sxs-lookup"><span data-stu-id="6c443-111">Edit security policy</span></span> | <span data-ttu-id="6c443-112">Apply security recommendations for a resource</span><span class="sxs-lookup"><span data-stu-id="6c443-112">Apply security recommendations for a resource</span></span> | <span data-ttu-id="6c443-113">Remediate or Dismiss alerts</span><span class="sxs-lookup"><span data-stu-id="6c443-113">Remediate or Dismiss alerts</span></span> | <span data-ttu-id="6c443-114">View alerts across a subscription</span><span class="sxs-lookup"><span data-stu-id="6c443-114">View alerts across a subscription</span></span> | <span data-ttu-id="6c443-115">View alerts for a specific resource</span><span class="sxs-lookup"><span data-stu-id="6c443-115">View alerts for a specific resource</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="6c443-116">Subscription Owner</span><span class="sxs-lookup"><span data-stu-id="6c443-116">Subscription Owner</span></span> | <span data-ttu-id="6c443-117">X</span><span class="sxs-lookup"><span data-stu-id="6c443-117">X</span></span> | <span data-ttu-id="6c443-118">X</span><span class="sxs-lookup"><span data-stu-id="6c443-118">X</span></span> | <span data-ttu-id="6c443-119">X</span><span class="sxs-lookup"><span data-stu-id="6c443-119">X</span></span> | <span data-ttu-id="6c443-120">X</span><span class="sxs-lookup"><span data-stu-id="6c443-120">X</span></span> | <span data-ttu-id="6c443-121">X</span><span class="sxs-lookup"><span data-stu-id="6c443-121">X</span></span> |
| <span data-ttu-id="6c443-122">Subscription Contributor</span><span class="sxs-lookup"><span data-stu-id="6c443-122">Subscription Contributor</span></span> | <span data-ttu-id="6c443-123">X</span><span class="sxs-lookup"><span data-stu-id="6c443-123">X</span></span> | <span data-ttu-id="6c443-124">X</span><span class="sxs-lookup"><span data-stu-id="6c443-124">X</span></span> | <span data-ttu-id="6c443-125">X</span><span class="sxs-lookup"><span data-stu-id="6c443-125">X</span></span> | <span data-ttu-id="6c443-126">X</span><span class="sxs-lookup"><span data-stu-id="6c443-126">X</span></span> | <span data-ttu-id="6c443-127">X</span><span class="sxs-lookup"><span data-stu-id="6c443-127">X</span></span> |
| <span data-ttu-id="6c443-128">Resource Group Owner</span><span class="sxs-lookup"><span data-stu-id="6c443-128">Resource Group Owner</span></span> | -- | <span data-ttu-id="6c443-129">X</span><span class="sxs-lookup"><span data-stu-id="6c443-129">X</span></span> | -- | -- | <span data-ttu-id="6c443-130">X</span><span class="sxs-lookup"><span data-stu-id="6c443-130">X</span></span> |
| <span data-ttu-id="6c443-131">Resource Group Contributor</span><span class="sxs-lookup"><span data-stu-id="6c443-131">Resource Group Contributor</span></span> | -- | <span data-ttu-id="6c443-132">X</span><span class="sxs-lookup"><span data-stu-id="6c443-132">X</span></span> | -- | -- | <span data-ttu-id="6c443-133">X</span><span class="sxs-lookup"><span data-stu-id="6c443-133">X</span></span> |
| <span data-ttu-id="6c443-134">Reader</span><span class="sxs-lookup"><span data-stu-id="6c443-134">Reader</span></span> | -- | -- | -- | <span data-ttu-id="6c443-135">X</span><span class="sxs-lookup"><span data-stu-id="6c443-135">X</span></span> | <span data-ttu-id="6c443-136">X</span><span class="sxs-lookup"><span data-stu-id="6c443-136">X</span></span> |

> [!NOTE]
> <span data-ttu-id="6c443-137">We recommend that you assign the least permissive role needed for users to complete their tasks.</span><span class="sxs-lookup"><span data-stu-id="6c443-137">We recommend that you assign the least permissive role needed for users to complete their tasks.</span></span> <span data-ttu-id="6c443-138">For example, assign the Reader role to users who only need to view information about the security health of a resource but not take action, such as applying recommendations or editing policies.</span><span class="sxs-lookup"><span data-stu-id="6c443-138">For example, assign the Reader role to users who only need to view information about the security health of a resource but not take action, such as applying recommendations or editing policies.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="6c443-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="6c443-139">Next steps</span></span>
<span data-ttu-id="6c443-140">This article explained how Security Center uses RBAC to assign permissions to users and identified the allowed actions for each role.</span><span class="sxs-lookup"><span data-stu-id="6c443-140">This article explained how Security Center uses RBAC to assign permissions to users and identified the allowed actions for each role.</span></span> <span data-ttu-id="6c443-141">Now that you're familiar with the role assignments needed to monitor the security state of your subscription, edit security policies, and apply recommendations, learn how to:</span><span class="sxs-lookup"><span data-stu-id="6c443-141">Now that you're familiar with the role assignments needed to monitor the security state of your subscription, edit security policies, and apply recommendations, learn how to:</span></span>

- [<span data-ttu-id="6c443-142">Set security policies in Security Center</span><span class="sxs-lookup"><span data-stu-id="6c443-142">Set security policies in Security Center</span></span>](security-center-policies.md)
- [<span data-ttu-id="6c443-143">Manage security recommendations in Security Center</span><span class="sxs-lookup"><span data-stu-id="6c443-143">Manage security recommendations in Security Center</span></span>](security-center-recommendations.md)
- [<span data-ttu-id="6c443-144">Monitor the security health of your Azure resources</span><span class="sxs-lookup"><span data-stu-id="6c443-144">Monitor the security health of your Azure resources</span></span>](security-center-monitoring.md)
- [<span data-ttu-id="6c443-145">Manage and respond to security alerts in Security Center</span><span class="sxs-lookup"><span data-stu-id="6c443-145">Manage and respond to security alerts in Security Center</span></span>](security-center-managing-and-responding-alerts.md)
- [<span data-ttu-id="6c443-146">Monitor partner security solutions</span><span class="sxs-lookup"><span data-stu-id="6c443-146">Monitor partner security solutions</span></span>](security-center-partner-solutions.md)
