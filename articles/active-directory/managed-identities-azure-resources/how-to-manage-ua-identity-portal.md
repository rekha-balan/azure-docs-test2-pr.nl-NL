---
title: How to manage a user-assigned managed identity using the Azure portal
description: Step by step instructions on how to create, list and delete a user-assigned managed identity.
services: active-directory
documentationcenter: ''
author: daveba
manager: mtillman
editor: ''
ms.service: active-directory
ms.component: msi
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/16/2018
ms.author: daveba
ms.openlocfilehash: 6729bee9bfebd8e80ae3b791dc2a8a480ac8b525
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867832"
---
# <a name="create-list-or-delete-a-user-assigned-managed-identity-using-the-azure-portal"></a><span data-ttu-id="670dd-103">Create, list or delete a user-assigned managed identity using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="670dd-103">Create, list or delete a user-assigned managed identity using the Azure portal</span></span>

[!INCLUDE [preview-notice](~/includes/active-directory-msi-preview-notice-ua.md)]

<span data-ttu-id="670dd-104">Managed identities for Azure resources provides Azure services with a managed identity in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="670dd-104">Managed identities for Azure resources provides Azure services with a managed identity in Azure Active Directory.</span></span> <span data-ttu-id="670dd-105">You can use this identity to authenticate to services that support Azure AD authentication, without needing credentials in your code.</span><span class="sxs-lookup"><span data-stu-id="670dd-105">You can use this identity to authenticate to services that support Azure AD authentication, without needing credentials in your code.</span></span> 

<span data-ttu-id="670dd-106">In this article, you learn how to create, list and delete a user-assigned managed identity using the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="670dd-106">In this article, you learn how to create, list and delete a user-assigned managed identity using the Azure Portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="670dd-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="670dd-107">Prerequisites</span></span>

- <span data-ttu-id="670dd-108">If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview.md).</span><span class="sxs-lookup"><span data-stu-id="670dd-108">If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview.md).</span></span> <span data-ttu-id="670dd-109">**Be sure to review the [difference between a system-assigned and user-assigned managed identity](overview.md#how-does-it-work)**.</span><span class="sxs-lookup"><span data-stu-id="670dd-109">**Be sure to review the [difference between a system-assigned and user-assigned managed identity](overview.md#how-does-it-work)**.</span></span>
- <span data-ttu-id="670dd-110">If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/free/) before continuing.</span><span class="sxs-lookup"><span data-stu-id="670dd-110">If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/free/) before continuing.</span></span>
- <span data-ttu-id="670dd-111">To perform the management operations in this article, your account needs the following role assignments:</span><span class="sxs-lookup"><span data-stu-id="670dd-111">To perform the management operations in this article, your account needs the following role assignments:</span></span>
    - <span data-ttu-id="670dd-112">[Managed Identity Contributor](/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role to create, read (list), update, and delete a user-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="670dd-112">[Managed Identity Contributor](/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role to create, read (list), update, and delete a user-assigned managed identity.</span></span>
    - <span data-ttu-id="670dd-113">[Managed Identity Operator](/azure/role-based-access-control/built-in-roles#managed-identity-operator) role to read (list) the properties of a user-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="670dd-113">[Managed Identity Operator](/azure/role-based-access-control/built-in-roles#managed-identity-operator) role to read (list) the properties of a user-assigned managed identity.</span></span>

## <a name="create-a-user-assigned-managed-identity"></a><span data-ttu-id="670dd-114">Create a user-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="670dd-114">Create a user-assigned managed identity</span></span>

1. <span data-ttu-id="670dd-115">Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription to create the user-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="670dd-115">Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription to create the user-assigned managed identity.</span></span>
2. <span data-ttu-id="670dd-116">In the search box, type *Managed Identities*, and under **Services**, click **Managed Identities**.</span><span class="sxs-lookup"><span data-stu-id="670dd-116">In the search box, type *Managed Identities*, and under **Services**, click **Managed Identities**.</span></span>
3. <span data-ttu-id="670dd-117">Click **Add** and enter values in the following fields under **Create user assigned managed** identity pane:</span><span class="sxs-lookup"><span data-stu-id="670dd-117">Click **Add** and enter values in the following fields under **Create user assigned managed** identity pane:</span></span>
   - <span data-ttu-id="670dd-118">**Resource Name**: This is the name for your user-assigned managed identity, for example UAI1.</span><span class="sxs-lookup"><span data-stu-id="670dd-118">**Resource Name**: This is the name for your user-assigned managed identity, for example UAI1.</span></span>
   - <span data-ttu-id="670dd-119">**Subscription**: Choose the subscription to create the user-assigned managed identity under</span><span class="sxs-lookup"><span data-stu-id="670dd-119">**Subscription**: Choose the subscription to create the user-assigned managed identity under</span></span>
   - <span data-ttu-id="670dd-120">**Resource Group**: Create a new resource group to contain your user-assigned managed identity or choose **Use existing** to create the user-assigned managed identity in an existing resource group.</span><span class="sxs-lookup"><span data-stu-id="670dd-120">**Resource Group**: Create a new resource group to contain your user-assigned managed identity or choose **Use existing** to create the user-assigned managed identity in an existing resource group.</span></span>
   - <span data-ttu-id="670dd-121">**Location**: Choose a location to deploy the user-assigned managed identity,for example **West US**.</span><span class="sxs-lookup"><span data-stu-id="670dd-121">**Location**: Choose a location to deploy the user-assigned managed identity,for example **West US**.</span></span>
4. <span data-ttu-id="670dd-122">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="670dd-122">Click **Create**.</span></span>

![Create a user-assigned managed identity](./media/how-to-manage-ua-identity-portal/create-user-assigned-managed-identity-portal.png)

## <a name="list-user-assigned-managed-identities"></a><span data-ttu-id="670dd-124">List user-assigned managed identities</span><span class="sxs-lookup"><span data-stu-id="670dd-124">List user-assigned managed identities</span></span>

1. <span data-ttu-id="670dd-125">Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription to list the user-assigned managed identities.</span><span class="sxs-lookup"><span data-stu-id="670dd-125">Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription to list the user-assigned managed identities.</span></span>
2. <span data-ttu-id="670dd-126">In the search box, type *Managed Identities*, and under Services, click **Managed Identities**.</span><span class="sxs-lookup"><span data-stu-id="670dd-126">In the search box, type *Managed Identities*, and under Services, click **Managed Identities**.</span></span>
3. <span data-ttu-id="670dd-127">A list of the user-assigned managed identities for your subscription is returned.</span><span class="sxs-lookup"><span data-stu-id="670dd-127">A list of the user-assigned managed identities for your subscription is returned.</span></span>  <span data-ttu-id="670dd-128">To see the details of a user-assigned managed identity click its name.</span><span class="sxs-lookup"><span data-stu-id="670dd-128">To see the details of a user-assigned managed identity click its name.</span></span>

![List user-assigned managed identity](./media/how-to-manage-ua-identity-portal/list-user-assigned-managed-identity-portal.png)

## <a name="delete-a-user-assigned-managed-identity"></a><span data-ttu-id="670dd-130">Delete a user-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="670dd-130">Delete a user-assigned managed identity</span></span>

1. <span data-ttu-id="670dd-131">Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription to delete a user-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="670dd-131">Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription to delete a user-assigned managed identity.</span></span>
2. <span data-ttu-id="670dd-132">Select the user-assigned managed identity and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="670dd-132">Select the user-assigned managed identity and click **Delete**.</span></span>
3. <span data-ttu-id="670dd-133">Under the confirmation box choose, **Yes**.</span><span class="sxs-lookup"><span data-stu-id="670dd-133">Under the confirmation box choose, **Yes**.</span></span>

![Delete user-assigned managed identity](./media/how-to-manage-ua-identity-portal/delete-user-assigned-managed-identity-portal.png)