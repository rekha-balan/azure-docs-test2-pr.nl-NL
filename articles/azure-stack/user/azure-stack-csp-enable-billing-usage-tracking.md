---
title: Enable a Cloud Service Provider to manage your Azure Stack subscription | Microsoft Docs
description: Enable the service provider to access a subscription in Azure Stack.
services: azure-stack
documentationcenter: ''
author: brenduns
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2018
ms.author: brenduns
ms.reviewer: alfredop
ms.openlocfilehash: f309b86578f340040927735c067656158f3198fc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865466"
---
# <a name="enable-a-cloud-service-provider-to-manage-your-azure-stack-subscription"></a><span data-ttu-id="e1db2-103">Enable a Cloud Service Provider to manage your Azure Stack subscription</span><span class="sxs-lookup"><span data-stu-id="e1db2-103">Enable a Cloud Service Provider to manage your Azure Stack subscription</span></span>

<span data-ttu-id="e1db2-104">*Applies to: Azure Stack integrated systems*</span><span class="sxs-lookup"><span data-stu-id="e1db2-104">*Applies to: Azure Stack integrated systems*</span></span>

<span data-ttu-id="e1db2-105">If you're using Azure Stack with a Cloud Service Provider (CSP), you might choose to manage your own subscription to access resources in Azure and in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="e1db2-105">If you're using Azure Stack with a Cloud Service Provider (CSP), you might choose to manage your own subscription to access resources in Azure and in Azure Stack.</span></span> <span data-ttu-id="e1db2-106">You can also let the provider manage your subscription for you.</span><span class="sxs-lookup"><span data-stu-id="e1db2-106">You can also let the provider manage your subscription for you.</span></span> <span data-ttu-id="e1db2-107">This article shows you how to:</span><span class="sxs-lookup"><span data-stu-id="e1db2-107">This article shows you how to:</span></span>

 * <span data-ttu-id="e1db2-108">Give your service provider access your subscription.</span><span class="sxs-lookup"><span data-stu-id="e1db2-108">Give your service provider access your subscription.</span></span>
 * <span data-ttu-id="e1db2-109">Make sure the service provider can manage your service.</span><span class="sxs-lookup"><span data-stu-id="e1db2-109">Make sure the service provider can manage your service.</span></span>

> [!Note]
>  <span data-ttu-id="e1db2-110">If the CSP isn't managing your account, and you skip the following steps, the CSP can't manage your Azure Stack subscription for you.</span><span class="sxs-lookup"><span data-stu-id="e1db2-110">If the CSP isn't managing your account, and you skip the following steps, the CSP can't manage your Azure Stack subscription for you.</span></span>

## <a name="manage-your-subscription-with-a-cloud-service-provider"></a><span data-ttu-id="e1db2-111">Manage your subscription with a Cloud Service Provider</span><span class="sxs-lookup"><span data-stu-id="e1db2-111">Manage your subscription with a Cloud Service Provider</span></span>

<span data-ttu-id="e1db2-112">Add the CSP as **user** to your subscription.</span><span class="sxs-lookup"><span data-stu-id="e1db2-112">Add the CSP as **user** to your subscription.</span></span>

1. <span data-ttu-id="e1db2-113">Add your CSP as guest user with the user role to your tenant directory.</span><span class="sxs-lookup"><span data-stu-id="e1db2-113">Add your CSP as guest user with the user role to your tenant directory.</span></span>  <span data-ttu-id="e1db2-114">For steps on adding a user, see [Add new users to Azure Active Directory](https://docs.microsoft.com/azure/active-directory/add-users-azure-active-directory)</span><span class="sxs-lookup"><span data-stu-id="e1db2-114">For steps on adding a user, see [Add new users to Azure Active Directory](https://docs.microsoft.com/azure/active-directory/add-users-azure-active-directory)</span></span>
2. <span data-ttu-id="e1db2-115">The CSP creates the local Azure Stack subscription for you.</span><span class="sxs-lookup"><span data-stu-id="e1db2-115">The CSP creates the local Azure Stack subscription for you.</span></span>
3. <span data-ttu-id="e1db2-116">You are ready to start using Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="e1db2-116">You are ready to start using Azure Stack.</span></span>
4. <span data-ttu-id="e1db2-117">Your CSP should create a resource in your subscription to verify that they can also manage your resources.</span><span class="sxs-lookup"><span data-stu-id="e1db2-117">Your CSP should create a resource in your subscription to verify that they can also manage your resources.</span></span> <span data-ttu-id="e1db2-118">For example, they can [Create a Windows virtual machine with the Azure Stack portal](azure-stack-quick-windows-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e1db2-118">For example, they can [Create a Windows virtual machine with the Azure Stack portal](azure-stack-quick-windows-portal.md).</span></span>

## <a name="enable-the-cloud-service-provider-to-manage-your-subscription-using-rbac-rights"></a><span data-ttu-id="e1db2-119">Enable the Cloud Service Provider to manage your subscription using RBAC rights</span><span class="sxs-lookup"><span data-stu-id="e1db2-119">Enable the Cloud Service Provider to manage your subscription using RBAC rights</span></span>

<span data-ttu-id="e1db2-120">Add the CSP as **owner** to your subscription.</span><span class="sxs-lookup"><span data-stu-id="e1db2-120">Add the CSP as **owner** to your subscription.</span></span>

1. <span data-ttu-id="e1db2-121">Add your CSP as guest user to your tenant directory.</span><span class="sxs-lookup"><span data-stu-id="e1db2-121">Add your CSP as guest user to your tenant directory.</span></span>  <span data-ttu-id="e1db2-122">For steps on adding a user, see [Add new users to Azure Active Directory](https://docs.microsoft.com/azure/active-directory/add-users-azure-active-directory)</span><span class="sxs-lookup"><span data-stu-id="e1db2-122">For steps on adding a user, see [Add new users to Azure Active Directory](https://docs.microsoft.com/azure/active-directory/add-users-azure-active-directory)</span></span>
2. <span data-ttu-id="e1db2-123">Add the Owner role to the CSP guest user.</span><span class="sxs-lookup"><span data-stu-id="e1db2-123">Add the Owner role to the CSP guest user.</span></span> <span data-ttu-id="e1db2-124">For steps on adding the CSP user to your subscription, see [Use Role-Based Access Control to manage access to your Azure subscription resources](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal)</span><span class="sxs-lookup"><span data-stu-id="e1db2-124">For steps on adding the CSP user to your subscription, see [Use Role-Based Access Control to manage access to your Azure subscription resources](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal)</span></span>
3. <span data-ttu-id="e1db2-125">The CSP creates the local Azure Stack subscription for you.</span><span class="sxs-lookup"><span data-stu-id="e1db2-125">The CSP creates the local Azure Stack subscription for you.</span></span>
4. <span data-ttu-id="e1db2-126">You are ready to start using Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="e1db2-126">You are ready to start using Azure Stack.</span></span>
5. <span data-ttu-id="e1db2-127">Your CSP should create a resource in your subscription to verify that they can manage your resources.</span><span class="sxs-lookup"><span data-stu-id="e1db2-127">Your CSP should create a resource in your subscription to verify that they can manage your resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1db2-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="e1db2-128">Next steps</span></span>

<span data-ttu-id="e1db2-129">To learn more about how to retrieve resource usage information from Azure Stack, see [Usage and billing in Azure Stack](../azure-stack-billing-and-chargeback.md).</span><span class="sxs-lookup"><span data-stu-id="e1db2-129">To learn more about how to retrieve resource usage information from Azure Stack, see [Usage and billing in Azure Stack](../azure-stack-billing-and-chargeback.md).</span></span>
