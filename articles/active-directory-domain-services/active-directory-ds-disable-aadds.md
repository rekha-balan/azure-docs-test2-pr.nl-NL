---
title: Disable Azure Active Directory Domain Services | Microsoft Docs
description: Disable Azure Active Directory Domain Services using the Azure portal
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: mtillman
editor: curtand
ms.assetid: 89e407e1-e1e0-49d1-8b89-de11484eee46
ms.service: active-directory
ms.component: domain-services
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 10/27/2017
ms.author: maheshu
ms.openlocfilehash: af24c7f9b721aab4f1ab810cf42f737fd14bdf88
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869829"
---
# <a name="disable-azure-active-directory-domain-services-using-the-azure-portal"></a><span data-ttu-id="6e8d0-103">Disable Azure Active Directory Domain Services using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="6e8d0-103">Disable Azure Active Directory Domain Services using the Azure portal</span></span>
<span data-ttu-id="6e8d0-104">This article shows you how to use the Azure portal to disable Azure Active Directory (AD) Domain Services for your Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="6e8d0-104">This article shows you how to use the Azure portal to disable Azure Active Directory (AD) Domain Services for your Azure AD directory.</span></span>

> [!WARNING]
> <span data-ttu-id="6e8d0-105">**Deletion is permanent and cannot be reversed.**</span><span class="sxs-lookup"><span data-stu-id="6e8d0-105">**Deletion is permanent and cannot be reversed.**</span></span>
> <span data-ttu-id="6e8d0-106">Proceed with caution!</span><span class="sxs-lookup"><span data-stu-id="6e8d0-106">Proceed with caution!</span></span> <span data-ttu-id="6e8d0-107">When you delete the managed domain:</span><span class="sxs-lookup"><span data-stu-id="6e8d0-107">When you delete the managed domain:</span></span>
  * <span data-ttu-id="6e8d0-108">Domain controllers for the managed domain are de-provisioned and removed from the virtual network.</span><span class="sxs-lookup"><span data-stu-id="6e8d0-108">Domain controllers for the managed domain are de-provisioned and removed from the virtual network.</span></span>
  * <span data-ttu-id="6e8d0-109">Data on the managed domain is deleted permanently.</span><span class="sxs-lookup"><span data-stu-id="6e8d0-109">Data on the managed domain is deleted permanently.</span></span> <span data-ttu-id="6e8d0-110">This includes custom OUs, GPOs, custom DNS records, service principals, GMSAs etc. that you have created on the managed domain.</span><span class="sxs-lookup"><span data-stu-id="6e8d0-110">This includes custom OUs, GPOs, custom DNS records, service principals, GMSAs etc. that you have created on the managed domain.</span></span>
  * <span data-ttu-id="6e8d0-111">Machines joined to the managed domain lose their trust relationship with the domain and need to be unjoined from the domain.</span><span class="sxs-lookup"><span data-stu-id="6e8d0-111">Machines joined to the managed domain lose their trust relationship with the domain and need to be unjoined from the domain.</span></span>
  * <span data-ttu-id="6e8d0-112">You cannot sign in to these machines using corporate AD credentials.</span><span class="sxs-lookup"><span data-stu-id="6e8d0-112">You cannot sign in to these machines using corporate AD credentials.</span></span> <span data-ttu-id="6e8d0-113">Use the local administrator credentials for the machine, instead.</span><span class="sxs-lookup"><span data-stu-id="6e8d0-113">Use the local administrator credentials for the machine, instead.</span></span>
<span data-ttu-id="6e8d0-114">Deleting the managed domain does not delete your Azure AD directory or otherwise adversely impact the directory.</span><span class="sxs-lookup"><span data-stu-id="6e8d0-114">Deleting the managed domain does not delete your Azure AD directory or otherwise adversely impact the directory.</span></span>
>

<span data-ttu-id="6e8d0-115">Perform the following steps to delete your Azure AD Domain Services managed domain:</span><span class="sxs-lookup"><span data-stu-id="6e8d0-115">Perform the following steps to delete your Azure AD Domain Services managed domain:</span></span>
1. <span data-ttu-id="6e8d0-116">Navigate to the [Azure AD Domain Services extension](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.AAD%2FdomainServices) in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6e8d0-116">Navigate to the [Azure AD Domain Services extension](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.AAD%2FdomainServices) in the Azure portal.</span></span>
2. <span data-ttu-id="6e8d0-117">Click the name of your managed domain.</span><span class="sxs-lookup"><span data-stu-id="6e8d0-117">Click the name of your managed domain.</span></span>

    ![Select domain to delete](./media/getting-started/domain-services-delete-select-domain.png)

3. <span data-ttu-id="6e8d0-119">On the **Overview** page, click the **Delete** button.</span><span class="sxs-lookup"><span data-stu-id="6e8d0-119">On the **Overview** page, click the **Delete** button.</span></span>

    ![Delete domain](./media/getting-started/domain-services-delete-domain.png)

4. <span data-ttu-id="6e8d0-121">To confirm the deletion, type the DNS domain name of the managed domain.</span><span class="sxs-lookup"><span data-stu-id="6e8d0-121">To confirm the deletion, type the DNS domain name of the managed domain.</span></span> <span data-ttu-id="6e8d0-122">Click the **Delete** button when you are done.</span><span class="sxs-lookup"><span data-stu-id="6e8d0-122">Click the **Delete** button when you are done.</span></span>

    ![Delete domain confirmation](./media/getting-started/domain-services-delete-domain-confirm.png)

<span data-ttu-id="6e8d0-124">The managed domain is deleted in about 15-20 minutes.</span><span class="sxs-lookup"><span data-stu-id="6e8d0-124">The managed domain is deleted in about 15-20 minutes.</span></span>

<span data-ttu-id="6e8d0-125">Consider [sharing feedback](active-directory-ds-contact-us.md) to help us understand what features would help you chose Azure AD Domain Services in the future.</span><span class="sxs-lookup"><span data-stu-id="6e8d0-125">Consider [sharing feedback](active-directory-ds-contact-us.md) to help us understand what features would help you chose Azure AD Domain Services in the future.</span></span> <span data-ttu-id="6e8d0-126">This feedback helps us evolve the service to better suit your deployment needs and use-cases.</span><span class="sxs-lookup"><span data-stu-id="6e8d0-126">This feedback helps us evolve the service to better suit your deployment needs and use-cases.</span></span>
