---
title: Enable Secure LDAP (LDAPS) in Azure AD Domain Services | Microsoft Docs
description: Enable Secure LDAP (LDAPS) for an Azure AD Domain Services managed domain
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: mtillman
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory
ms.component: domain-services
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 08/01/2018
ms.author: maheshu
ms.openlocfilehash: befab32a9daf5a22a326396c84223e07d401f72b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867730"
---
# <a name="enable-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="1fa0a-103">Enable secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="1fa0a-103">Enable secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1fa0a-104">Before you begin</span><span class="sxs-lookup"><span data-stu-id="1fa0a-104">Before you begin</span></span>
<span data-ttu-id="1fa0a-105">Complete [Task 2 - export the secure LDAP certificate to a .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span><span class="sxs-lookup"><span data-stu-id="1fa0a-105">Complete [Task 2 - export the secure LDAP certificate to a .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>


## <a name="task-3-enable-secure-ldap-for-the-managed-domain-using-the-azure-portal"></a><span data-ttu-id="1fa0a-106">Task 3: Enable secure LDAP for the managed domain using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="1fa0a-106">Task 3: Enable secure LDAP for the managed domain using the Azure portal</span></span>
<span data-ttu-id="1fa0a-107">To enable secure LDAP, perform the following configuration steps:</span><span class="sxs-lookup"><span data-stu-id="1fa0a-107">To enable secure LDAP, perform the following configuration steps:</span></span>

1. <span data-ttu-id="1fa0a-108">Navigate to the **[Azure portal](https://portal.azure.com)**.</span><span class="sxs-lookup"><span data-stu-id="1fa0a-108">Navigate to the **[Azure portal](https://portal.azure.com)**.</span></span>

2. <span data-ttu-id="1fa0a-109">Search for 'domain services' in the **Search resources** search box.</span><span class="sxs-lookup"><span data-stu-id="1fa0a-109">Search for 'domain services' in the **Search resources** search box.</span></span> <span data-ttu-id="1fa0a-110">Select **Azure AD Domain Services** from the search result.</span><span class="sxs-lookup"><span data-stu-id="1fa0a-110">Select **Azure AD Domain Services** from the search result.</span></span> <span data-ttu-id="1fa0a-111">The **Azure AD Domain Services** page lists your managed domain.</span><span class="sxs-lookup"><span data-stu-id="1fa0a-111">The **Azure AD Domain Services** page lists your managed domain.</span></span>

    ![Find managed domain being provisioned](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="1fa0a-113">Click the name of the managed domain (for example, 'contoso100.com') to see more details about the domain.</span><span class="sxs-lookup"><span data-stu-id="1fa0a-113">Click the name of the managed domain (for example, 'contoso100.com') to see more details about the domain.</span></span>

    ![Domain Services - provisioning state](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="1fa0a-115">Click **Secure LDAP** on the navigation pane.</span><span class="sxs-lookup"><span data-stu-id="1fa0a-115">Click **Secure LDAP** on the navigation pane.</span></span>

    ![Domain Services - Secure LDAP page](./media/active-directory-domain-services-admin-guide/secure-ldap-blade.png)

4. <span data-ttu-id="1fa0a-117">By default, secure LDAP access to your managed domain is disabled.</span><span class="sxs-lookup"><span data-stu-id="1fa0a-117">By default, secure LDAP access to your managed domain is disabled.</span></span> <span data-ttu-id="1fa0a-118">Toggle **Secure LDAP** to **Enable**.</span><span class="sxs-lookup"><span data-stu-id="1fa0a-118">Toggle **Secure LDAP** to **Enable**.</span></span>

    ![Enable secure LDAP](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configure.png)
5. <span data-ttu-id="1fa0a-120">By default, secure LDAP access to your managed domain over the internet is disabled.</span><span class="sxs-lookup"><span data-stu-id="1fa0a-120">By default, secure LDAP access to your managed domain over the internet is disabled.</span></span> <span data-ttu-id="1fa0a-121">Toggle **Allow secure LDAP access over the internet** to **Enable**, if you need to.</span><span class="sxs-lookup"><span data-stu-id="1fa0a-121">Toggle **Allow secure LDAP access over the internet** to **Enable**, if you need to.</span></span>

    > [!WARNING]
    > <span data-ttu-id="1fa0a-122">When you enable secure LDAP access over the internet, your domain is susceptible to password brute force attacks over the internet.</span><span class="sxs-lookup"><span data-stu-id="1fa0a-122">When you enable secure LDAP access over the internet, your domain is susceptible to password brute force attacks over the internet.</span></span> <span data-ttu-id="1fa0a-123">Therefore, we recommend setting up an NSG to lock down access to required source IP address ranges.</span><span class="sxs-lookup"><span data-stu-id="1fa0a-123">Therefore, we recommend setting up an NSG to lock down access to required source IP address ranges.</span></span> <span data-ttu-id="1fa0a-124">See the instructions to [lock down LDAPS access to your managed domain over the internet](#task-5---lock-down-secure-ldap-access-to-your-managed-domain-over-the-internet).</span><span class="sxs-lookup"><span data-stu-id="1fa0a-124">See the instructions to [lock down LDAPS access to your managed domain over the internet](#task-5---lock-down-secure-ldap-access-to-your-managed-domain-over-the-internet).</span></span>
    >

6. <span data-ttu-id="1fa0a-125">Click the folder icon following **.PFX file with secure LDAP certificate**.</span><span class="sxs-lookup"><span data-stu-id="1fa0a-125">Click the folder icon following **.PFX file with secure LDAP certificate**.</span></span> <span data-ttu-id="1fa0a-126">Specify the path to the PFX file with the certificate for secure LDAP access to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="1fa0a-126">Specify the path to the PFX file with the certificate for secure LDAP access to the managed domain.</span></span>

7. <span data-ttu-id="1fa0a-127">Specify the **Password to decrypt .PFX file**.</span><span class="sxs-lookup"><span data-stu-id="1fa0a-127">Specify the **Password to decrypt .PFX file**.</span></span> <span data-ttu-id="1fa0a-128">Provide the same password you used when exporting the certificate to the PFX file.</span><span class="sxs-lookup"><span data-stu-id="1fa0a-128">Provide the same password you used when exporting the certificate to the PFX file.</span></span>

8. <span data-ttu-id="1fa0a-129">When you're done, click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="1fa0a-129">When you're done, click the **Save** button.</span></span>

9. <span data-ttu-id="1fa0a-130">You see a notification that informs you secure LDAP is being configured for the managed domain.</span><span class="sxs-lookup"><span data-stu-id="1fa0a-130">You see a notification that informs you secure LDAP is being configured for the managed domain.</span></span> <span data-ttu-id="1fa0a-131">Until this operation is complete, you can't modify other settings for the domain.</span><span class="sxs-lookup"><span data-stu-id="1fa0a-131">Until this operation is complete, you can't modify other settings for the domain.</span></span>

    ![Configuring secure LDAP for the managed domain](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configuring.png)

> [!NOTE]
> <span data-ttu-id="1fa0a-133">It takes about 10 to 15 minutes to enable secure LDAP for your managed domain.</span><span class="sxs-lookup"><span data-stu-id="1fa0a-133">It takes about 10 to 15 minutes to enable secure LDAP for your managed domain.</span></span> <span data-ttu-id="1fa0a-134">If the provided secure LDAP certificate does not match the required criteria, secure LDAP is not enabled for your directory and you see a failure.</span><span class="sxs-lookup"><span data-stu-id="1fa0a-134">If the provided secure LDAP certificate does not match the required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="1fa0a-135">For example, the domain name is incorrect, the certificate has already expired or expires soon.</span><span class="sxs-lookup"><span data-stu-id="1fa0a-135">For example, the domain name is incorrect, the certificate has already expired or expires soon.</span></span> <span data-ttu-id="1fa0a-136">In this case, retry with a valid certificate.</span><span class="sxs-lookup"><span data-stu-id="1fa0a-136">In this case, retry with a valid certificate.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="1fa0a-137">Next step</span><span class="sxs-lookup"><span data-stu-id="1fa0a-137">Next step</span></span>
[<span data-ttu-id="1fa0a-138">Task 4: configure DNS to access the managed domain from the internet</span><span class="sxs-lookup"><span data-stu-id="1fa0a-138">Task 4: configure DNS to access the managed domain from the internet</span></span>](active-directory-ds-ldaps-configure-dns.md)
