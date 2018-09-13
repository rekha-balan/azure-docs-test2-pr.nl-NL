---
title: Manage and connect to your Azure China 21Vianet subscription | Microsoft Docs
description: Azure China 21Vianet has unique URLs and endpoints for managing your environment. After connecting to the Azure environment, operations for managing a service work if the component has been deployed correctly. Learn why it's important to use the right connections to manage your environment.
services: china
cloud: na
documentationcenter: na
author: v-wimarc
manager: edprice
ms.assetid: na
ms.service: china
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/29/2017
ms.author: v-wimarc
ms.openlocfilehash: 661837912c9b2dbdd4b27fe6c25c2ebe95aa96f7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856382"
---
# <a name="manage-and-connect-to-your-subscription"></a><span data-ttu-id="24558-105">Manage and connect to your subscription</span><span class="sxs-lookup"><span data-stu-id="24558-105">Manage and connect to your subscription</span></span>
<span data-ttu-id="24558-106">Microsoft Azure operated by 21Vianet (Azure China 21Vianet) has unique URLs and endpoints for managing your environment.</span><span class="sxs-lookup"><span data-stu-id="24558-106">Microsoft Azure operated by 21Vianet (Azure China 21Vianet) has unique URLs and endpoints for managing your environment.</span></span> <span data-ttu-id="24558-107">It's important to use the right connections to manage your environment.</span><span class="sxs-lookup"><span data-stu-id="24558-107">It's important to use the right connections to manage your environment.</span></span> <span data-ttu-id="24558-108">After you connect to the Azure environment, the normal operations for managing a service work if the component has been deployed.</span><span class="sxs-lookup"><span data-stu-id="24558-108">After you connect to the Azure environment, the normal operations for managing a service work if the component has been deployed.</span></span>

## <a name="connect-by-using-the-portal"></a><span data-ttu-id="24558-109">Connect by using the portal</span><span class="sxs-lookup"><span data-stu-id="24558-109">Connect by using the portal</span></span>
<span data-ttu-id="24558-110">Access to applications and services on Microsoft Azure China 21Vianet is through the [Azure portal](https://portal.azure.cn/), an [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) platform.</span><span class="sxs-lookup"><span data-stu-id="24558-110">Access to applications and services on Microsoft Azure China 21Vianet is through the [Azure portal](https://portal.azure.cn/), an [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) platform.</span></span>

![Azure portal](media/china-get-started-service-manage-and-connect/azureportal.png)

## <a name="work-with-administrator-roles"></a><span data-ttu-id="24558-112">Work with administrator roles</span><span class="sxs-lookup"><span data-stu-id="24558-112">Work with administrator roles</span></span>
<span data-ttu-id="24558-113">One account administrator role is created per Azure account, typically the person who signed up for or bought the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="24558-113">One account administrator role is created per Azure account, typically the person who signed up for or bought the Azure subscription.</span></span> <span data-ttu-id="24558-114">This role is authorized to use the [Account Center](https://account.windowsazure.cn/) to perform management tasks.</span><span class="sxs-lookup"><span data-stu-id="24558-114">This role is authorized to use the [Account Center](https://account.windowsazure.cn/) to perform management tasks.</span></span>

<span data-ttu-id="24558-115">To sign in, the account administrator uses the organization ID (OrgID) created when the subscription was purchased.</span><span class="sxs-lookup"><span data-stu-id="24558-115">To sign in, the account administrator uses the organization ID (OrgID) created when the subscription was purchased.</span></span> 

### <a name="create-a-service-administrator-to-manage-the-service-deployment"></a><span data-ttu-id="24558-116">Create a service administrator to manage the service deployment</span><span class="sxs-lookup"><span data-stu-id="24558-116">Create a service administrator to manage the service deployment</span></span> 
<span data-ttu-id="24558-117">One service administrator role is created per Azure account and is authorized to manage services in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="24558-117">One service administrator role is created per Azure account and is authorized to manage services in Azure portal.</span></span> <span data-ttu-id="24558-118">With a new subscription, the account administrator is also the service administrator.</span><span class="sxs-lookup"><span data-stu-id="24558-118">With a new subscription, the account administrator is also the service administrator.</span></span>

<span data-ttu-id="24558-119">To create a service administrator:</span><span class="sxs-lookup"><span data-stu-id="24558-119">To create a service administrator:</span></span>
1.  <span data-ttu-id="24558-120">Log on to the Azure portal and click **Active Directory** from the left navigation menu.</span><span class="sxs-lookup"><span data-stu-id="24558-120">Log on to the Azure portal and click **Active Directory** from the left navigation menu.</span></span>
2.  <span data-ttu-id="24558-121">Under **Name**, click **Add a user**.</span><span class="sxs-lookup"><span data-stu-id="24558-121">Under **Name**, click **Add a user**.</span></span> <span data-ttu-id="24558-122">Enter a user name, profile, and a temporary password for the new user.</span><span class="sxs-lookup"><span data-stu-id="24558-122">Enter a user name, profile, and a temporary password for the new user.</span></span>
3.  <span data-ttu-id="24558-123">Click **View my bill**, select the subscription, and then click **Edit subscription details**.</span><span class="sxs-lookup"><span data-stu-id="24558-123">Click **View my bill**, select the subscription, and then click **Edit subscription details**.</span></span>
4.  <span data-ttu-id="24558-124">Change Service Administrator to the newly-created user.</span><span class="sxs-lookup"><span data-stu-id="24558-124">Change Service Administrator to the newly-created user.</span></span>

### <a name="create-a-co-administrator"></a><span data-ttu-id="24558-125">Create a co-administrator</span><span class="sxs-lookup"><span data-stu-id="24558-125">Create a co-administrator</span></span>
<span data-ttu-id="24558-126">Account administrators can create up to 199 co-administrator roles per subscription.</span><span class="sxs-lookup"><span data-stu-id="24558-126">Account administrators can create up to 199 co-administrator roles per subscription.</span></span> <span data-ttu-id="24558-127">This role has the same access privileges as the service administrator, but cannot change the association of subscriptions to Azure directories.</span><span class="sxs-lookup"><span data-stu-id="24558-127">This role has the same access privileges as the service administrator, but cannot change the association of subscriptions to Azure directories.</span></span>
1.  <span data-ttu-id="24558-128">Log on to Azure portal and click **Active Directory** on the left navigation menu.</span><span class="sxs-lookup"><span data-stu-id="24558-128">Log on to Azure portal and click **Active Directory** on the left navigation menu.</span></span>
2.  <span data-ttu-id="24558-129">Under **Name**, click **Add a user**.</span><span class="sxs-lookup"><span data-stu-id="24558-129">Under **Name**, click **Add a user**.</span></span> <span data-ttu-id="24558-130">Enter a user name, profile, and a temporary password for the new user.</span><span class="sxs-lookup"><span data-stu-id="24558-130">Enter a user name, profile, and a temporary password for the new user.</span></span>
3.  <span data-ttu-id="24558-131">On the main menu bar, click **Setting**, then click **Administrators**.</span><span class="sxs-lookup"><span data-stu-id="24558-131">On the main menu bar, click **Setting**, then click **Administrators**.</span></span>
4.  <span data-ttu-id="24558-132">Click **Add**, then enter the user address from the earlier step.</span><span class="sxs-lookup"><span data-stu-id="24558-132">Click **Add**, then enter the user address from the earlier step.</span></span> <span data-ttu-id="24558-133">Use the original account domain.</span><span class="sxs-lookup"><span data-stu-id="24558-133">Use the original account domain.</span></span> <span data-ttu-id="24558-134">Select the subscription to which the co-administrator has access.</span><span class="sxs-lookup"><span data-stu-id="24558-134">Select the subscription to which the co-administrator has access.</span></span>
5.  <span data-ttu-id="24558-135">Verify the change on the **Setting** page.</span><span class="sxs-lookup"><span data-stu-id="24558-135">Verify the change on the **Setting** page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="24558-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="24558-136">Next steps</span></span>
- [<span data-ttu-id="24558-137">Azure portal</span><span class="sxs-lookup"><span data-stu-id="24558-137">Azure portal</span></span>](https://portal.azure.cn/)
- [<span data-ttu-id="24558-138">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="24558-138">Azure Resource Manager</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)
- [<span data-ttu-id="24558-139">Account Center</span><span class="sxs-lookup"><span data-stu-id="24558-139">Account Center</span></span>](https://account.windowsazure.cn/)

