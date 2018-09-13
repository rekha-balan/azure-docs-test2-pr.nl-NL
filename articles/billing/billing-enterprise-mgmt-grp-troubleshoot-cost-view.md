---
title: Troubleshoot Azure enterprise cost views | Microsoft Docs
description: Learn how to resolve any issues you might have with organizational cost views within the Azure portal.
author: rthorn17
manager: rithorn
editor: ''
ms.assetid: ''
ms.service: billing
ms.devlang: na
ms.topic: troubleshooting
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 2/22/2017
ms.author: rithorn
ms.openlocfilehash: 2a9639103b494e3af54a6a21ed769cf4f7bd6259
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869716"
---
# <a name="troubleshoot-enterprise-cost-views"></a><span data-ttu-id="dc6fd-103">Troubleshoot enterprise cost views</span><span class="sxs-lookup"><span data-stu-id="dc6fd-103">Troubleshoot enterprise cost views</span></span> 

<span data-ttu-id="dc6fd-104">Within enterprise enrollments, there are multiple settings that could cause users within the enrollment to not be able to view costs.</span><span class="sxs-lookup"><span data-stu-id="dc6fd-104">Within enterprise enrollments, there are multiple settings that could cause users within the enrollment to not be able to view costs.</span></span>  <span data-ttu-id="dc6fd-105">These settings are managed by the enrollment administrator, or by the partner if the enrollment is not purchased directly with Microsoft.</span><span class="sxs-lookup"><span data-stu-id="dc6fd-105">These settings are managed by the enrollment administrator, or by the partner if the enrollment is not purchased directly with Microsoft.</span></span>  <span data-ttu-id="dc6fd-106">This article helps you understand what the settings are and how they impact the enrollment.</span><span class="sxs-lookup"><span data-stu-id="dc6fd-106">This article helps you understand what the settings are and how they impact the enrollment.</span></span> <span data-ttu-id="dc6fd-107">These settings are independent of the [Azure RBAC Roles](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal).</span><span class="sxs-lookup"><span data-stu-id="dc6fd-107">These settings are independent of the [Azure RBAC Roles](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal).</span></span> 


## <a name="enabling-access-to-costs"></a><span data-ttu-id="dc6fd-108">Enabling access to costs</span><span class="sxs-lookup"><span data-stu-id="dc6fd-108">Enabling access to costs</span></span>

<span data-ttu-id="dc6fd-109">Are you seeing a message Unauthorized, or *"Cost views are disabled in your enrollment."*</span><span class="sxs-lookup"><span data-stu-id="dc6fd-109">Are you seeing a message Unauthorized, or *"Cost views are disabled in your enrollment."*</span></span> <span data-ttu-id="dc6fd-110">when looking for cost information? ![unauthorized](media/billing-enterprise-mgmt-groups/unauthorized.png)</span><span class="sxs-lookup"><span data-stu-id="dc6fd-110">when looking for cost information? ![unauthorized](media/billing-enterprise-mgmt-groups/unauthorized.png)</span></span>

<span data-ttu-id="dc6fd-111">It might be due to one of the following reasons:</span><span class="sxs-lookup"><span data-stu-id="dc6fd-111">It might be due to one of the following reasons:</span></span>

1. <span data-ttu-id="dc6fd-112">You’ve purchased Azure through an enterprise partner, and the partner hasn’t released pricing yet.</span><span class="sxs-lookup"><span data-stu-id="dc6fd-112">You’ve purchased Azure through an enterprise partner, and the partner hasn’t released pricing yet.</span></span> <span data-ttu-id="dc6fd-113">To release pricing, contact your partner to do update the setting within the [Enterprise portal](https://ea.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dc6fd-113">To release pricing, contact your partner to do update the setting within the [Enterprise portal](https://ea.azure.com).</span></span>
2. <span data-ttu-id="dc6fd-114">Alternatively, if you’re an EA Direct customer, there are a couple of possibilities:</span><span class="sxs-lookup"><span data-stu-id="dc6fd-114">Alternatively, if you’re an EA Direct customer, there are a couple of possibilities:</span></span>
    * <span data-ttu-id="dc6fd-115">You are an Account Owner and your Enrollment Administrator has disabled the "AO view charges" setting.</span><span class="sxs-lookup"><span data-stu-id="dc6fd-115">You are an Account Owner and your Enrollment Administrator has disabled the "AO view charges" setting.</span></span>  
    * <span data-ttu-id="dc6fd-116">You are a Department Administrator and your Enrollment Administrator has disabled the "DA view charges" setting.</span><span class="sxs-lookup"><span data-stu-id="dc6fd-116">You are a Department Administrator and your Enrollment Administrator has disabled the "DA view charges" setting.</span></span>
    * <span data-ttu-id="dc6fd-117">Contact your Enrollment Administrator to get access.</span><span class="sxs-lookup"><span data-stu-id="dc6fd-117">Contact your Enrollment Administrator to get access.</span></span> <span data-ttu-id="dc6fd-118">The Enrollment Admin can visit the [Enterprise portal](https://ea.azure.com/manage/enrollment) and update the setting as seen here:</span><span class="sxs-lookup"><span data-stu-id="dc6fd-118">The Enrollment Admin can visit the [Enterprise portal](https://ea.azure.com/manage/enrollment) and update the setting as seen here:</span></span>

![Enterprise Portal Settings](media/billing-enterprise-mgmt-groups/ea-portal-settings.png)


## <a name="asset-is-unavailable"></a><span data-ttu-id="dc6fd-120">Asset is unavailable?</span><span class="sxs-lookup"><span data-stu-id="dc6fd-120">Asset is unavailable?</span></span> 
<span data-ttu-id="dc6fd-121">If you are receiving an error message "This asset is unavailable" when trying to access a subscription or management group, then you do not have the correct role to view this item.</span><span class="sxs-lookup"><span data-stu-id="dc6fd-121">If you are receiving an error message "This asset is unavailable" when trying to access a subscription or management group, then you do not have the correct role to view this item.</span></span>  

![asset-not-found](media/billing-enterprise-mgmt-groups/asset-not-found.png)

<span data-ttu-id="dc6fd-123">Contact the administer of the subscription or management groups to be given access.</span><span class="sxs-lookup"><span data-stu-id="dc6fd-123">Contact the administer of the subscription or management groups to be given access.</span></span>  
* <span data-ttu-id="dc6fd-124">For subscriptions, reference [Azure Role-Based Access Control (RBAC)](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal) document for help on which role is needed.</span><span class="sxs-lookup"><span data-stu-id="dc6fd-124">For subscriptions, reference [Azure Role-Based Access Control (RBAC)](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal) document for help on which role is needed.</span></span>
