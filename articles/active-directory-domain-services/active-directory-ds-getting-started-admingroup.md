---
title: 'Azure Active Directory Domain Services: Getting Started | Microsoft Docs'
description: Enable Azure Active Directory Domain Services using the Azure portal
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: mtillman
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory
ms.component: domain-services
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/23/2018
ms.author: maheshu
ms.openlocfilehash: 2290273c1b998a2d75046fcbcf613762ddd588ee
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967325"
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal"></a><span data-ttu-id="431f0-103">Enable Azure Active Directory Domain Services using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="431f0-103">Enable Azure Active Directory Domain Services using the Azure portal</span></span>


## <a name="task-3-configure-administrative-group"></a><span data-ttu-id="431f0-104">Task 3: configure administrative group</span><span class="sxs-lookup"><span data-stu-id="431f0-104">Task 3: configure administrative group</span></span>
<span data-ttu-id="431f0-105">In this configuration task, you create an administrative group in your Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="431f0-105">In this configuration task, you create an administrative group in your Azure AD directory.</span></span> <span data-ttu-id="431f0-106">This special administrative group is called *AAD DC Administrators*.</span><span class="sxs-lookup"><span data-stu-id="431f0-106">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="431f0-107">Members of this group are granted administrative permissions on machines that are domain-joined to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="431f0-107">Members of this group are granted administrative permissions on machines that are domain-joined to the managed domain.</span></span> <span data-ttu-id="431f0-108">On domain-joined machines, this group is added to the administrators group.</span><span class="sxs-lookup"><span data-stu-id="431f0-108">On domain-joined machines, this group is added to the administrators group.</span></span> <span data-ttu-id="431f0-109">Additionally, members of this group can use Remote Desktop to connect remotely to domain-joined machines.</span><span class="sxs-lookup"><span data-stu-id="431f0-109">Additionally, members of this group can use Remote Desktop to connect remotely to domain-joined machines.</span></span>

> [!NOTE]
> <span data-ttu-id="431f0-110">You do not have Domain Administrator or Enterprise Administrator permissions on the managed domain that you created by using Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="431f0-110">You do not have Domain Administrator or Enterprise Administrator permissions on the managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="431f0-111">On managed domains, these permissions are reserved by the service and are not made available to users within the tenant.</span><span class="sxs-lookup"><span data-stu-id="431f0-111">On managed domains, these permissions are reserved by the service and are not made available to users within the tenant.</span></span> <span data-ttu-id="431f0-112">However, you can use the special administrative group created in this configuration task to perform some privileged operations.</span><span class="sxs-lookup"><span data-stu-id="431f0-112">However, you can use the special administrative group created in this configuration task to perform some privileged operations.</span></span> <span data-ttu-id="431f0-113">These operations include joining computers to the domain, belonging to the administration group on domain-joined machines, and configuring Group Policy.</span><span class="sxs-lookup"><span data-stu-id="431f0-113">These operations include joining computers to the domain, belonging to the administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="431f0-114">The wizard automatically creates the administrative group in your Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="431f0-114">The wizard automatically creates the administrative group in your Azure AD directory.</span></span> <span data-ttu-id="431f0-115">This group is called 'AAD DC Administrators'.</span><span class="sxs-lookup"><span data-stu-id="431f0-115">This group is called 'AAD DC Administrators'.</span></span> <span data-ttu-id="431f0-116">If you have an existing group with this name in your Azure AD directory, the wizard selects this group.</span><span class="sxs-lookup"><span data-stu-id="431f0-116">If you have an existing group with this name in your Azure AD directory, the wizard selects this group.</span></span> <span data-ttu-id="431f0-117">You can configure group membership using the **Administrator group** wizard page.</span><span class="sxs-lookup"><span data-stu-id="431f0-117">You can configure group membership using the **Administrator group** wizard page.</span></span>

1. <span data-ttu-id="431f0-118">To configure group membership, click **AAD DC Administrators**.</span><span class="sxs-lookup"><span data-stu-id="431f0-118">To configure group membership, click **AAD DC Administrators**.</span></span>

    ![Configure group membership](./media/getting-started/domain-services-blade-admingroup.png)

2. <span data-ttu-id="431f0-120">Click the **Add members** button to add users from your Azure AD directory to the administrator group.</span><span class="sxs-lookup"><span data-stu-id="431f0-120">Click the **Add members** button to add users from your Azure AD directory to the administrator group.</span></span>

3. <span data-ttu-id="431f0-121">When you are done, click **OK** to move on to the **Summary** page of the wizard.</span><span class="sxs-lookup"><span data-stu-id="431f0-121">When you are done, click **OK** to move on to the **Summary** page of the wizard.</span></span>


## <a name="deploy-your-managed-domain"></a><span data-ttu-id="431f0-122">Deploy your managed domain</span><span class="sxs-lookup"><span data-stu-id="431f0-122">Deploy your managed domain</span></span>

1. <span data-ttu-id="431f0-123">On the **Summary** page of the wizard, review the configuration settings for the managed domain.</span><span class="sxs-lookup"><span data-stu-id="431f0-123">On the **Summary** page of the wizard, review the configuration settings for the managed domain.</span></span> <span data-ttu-id="431f0-124">You can go back to any step of the wizard to make changes, if necessary.</span><span class="sxs-lookup"><span data-stu-id="431f0-124">You can go back to any step of the wizard to make changes, if necessary.</span></span> <span data-ttu-id="431f0-125">When you are done, click **OK** to create the new managed domain.</span><span class="sxs-lookup"><span data-stu-id="431f0-125">When you are done, click **OK** to create the new managed domain.</span></span>

    ![Summary](./media/getting-started/domain-services-blade-summary.png)

2. <span data-ttu-id="431f0-127">You see a notification that shows the progress of your Azure AD Domain Services deployment.</span><span class="sxs-lookup"><span data-stu-id="431f0-127">You see a notification that shows the progress of your Azure AD Domain Services deployment.</span></span> <span data-ttu-id="431f0-128">Click the notification to see detailed progress for the deployment.</span><span class="sxs-lookup"><span data-stu-id="431f0-128">Click the notification to see detailed progress for the deployment.</span></span>

    ![Notification - deployment in progress](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="check-the-deployment-status-of-your-managed-domain"></a><span data-ttu-id="431f0-130">Check the deployment status of your managed domain</span><span class="sxs-lookup"><span data-stu-id="431f0-130">Check the deployment status of your managed domain</span></span>
<span data-ttu-id="431f0-131">The process of provisioning your managed domain can take up to an hour.</span><span class="sxs-lookup"><span data-stu-id="431f0-131">The process of provisioning your managed domain can take up to an hour.</span></span>

1. <span data-ttu-id="431f0-132">While your deployment is in progress, you can search for 'domain services' in the **Search resources** search box.</span><span class="sxs-lookup"><span data-stu-id="431f0-132">While your deployment is in progress, you can search for 'domain services' in the **Search resources** search box.</span></span> <span data-ttu-id="431f0-133">Select **Azure AD Domain Services** from the search result.</span><span class="sxs-lookup"><span data-stu-id="431f0-133">Select **Azure AD Domain Services** from the search result.</span></span> <span data-ttu-id="431f0-134">The **Azure AD Domain Services** blade lists the managed domain that is being provisioned.</span><span class="sxs-lookup"><span data-stu-id="431f0-134">The **Azure AD Domain Services** blade lists the managed domain that is being provisioned.</span></span>

    ![Find managed domain being provisioned](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="431f0-136">Click the name of the managed domain (for example, 'contoso100.com') to see more details about the managed domain.</span><span class="sxs-lookup"><span data-stu-id="431f0-136">Click the name of the managed domain (for example, 'contoso100.com') to see more details about the managed domain.</span></span>

    ![Domain Services - provisioning state](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="431f0-138">The **Overview** tab shows that the managed domain is currently being provisioned.</span><span class="sxs-lookup"><span data-stu-id="431f0-138">The **Overview** tab shows that the managed domain is currently being provisioned.</span></span> <span data-ttu-id="431f0-139">You cannot configure the managed domain until it is fully provisioned.</span><span class="sxs-lookup"><span data-stu-id="431f0-139">You cannot configure the managed domain until it is fully provisioned.</span></span> <span data-ttu-id="431f0-140">It may take up to an hour for your managed domain to be fully provisioned.</span><span class="sxs-lookup"><span data-stu-id="431f0-140">It may take up to an hour for your managed domain to be fully provisioned.</span></span>

    ![<span data-ttu-id="431f0-141">Domain Services - Overview tab during the provisioning state</span><span class="sxs-lookup"><span data-stu-id="431f0-141">Domain Services - Overview tab during the provisioning state</span></span> ](./media/getting-started/domain-services-provisioning-state-details.png)

4. <span data-ttu-id="431f0-142">When the managed domain is fully provisioned, the **Overview** tab shows the domain status as **Running**.</span><span class="sxs-lookup"><span data-stu-id="431f0-142">When the managed domain is fully provisioned, the **Overview** tab shows the domain status as **Running**.</span></span>

    ![Domain Services - Overview tab after fully provisioned](./media/getting-started/domain-services-provisioned.png)
    >[!NOTE]
    ><span data-ttu-id="431f0-144">During the provisioning process, Azure AD Domain Services creates Enterprise Applications named "Domain Controller Services" and "AzureActiveDirectoryDomainControllerServices" within your directory.</span><span class="sxs-lookup"><span data-stu-id="431f0-144">During the provisioning process, Azure AD Domain Services creates Enterprise Applications named "Domain Controller Services" and "AzureActiveDirectoryDomainControllerServices" within your directory.</span></span> <span data-ttu-id="431f0-145">These Enterprise Applications are needed to service your managed domain.</span><span class="sxs-lookup"><span data-stu-id="431f0-145">These Enterprise Applications are needed to service your managed domain.</span></span> <span data-ttu-id="431f0-146">It is imperative that these are not deleted at any time.</span><span class="sxs-lookup"><span data-stu-id="431f0-146">It is imperative that these are not deleted at any time.</span></span>
    >

5. <span data-ttu-id="431f0-147">On the **Properties** tab, you see two IP addresses at which domain controllers are available for the virtual network.</span><span class="sxs-lookup"><span data-stu-id="431f0-147">On the **Properties** tab, you see two IP addresses at which domain controllers are available for the virtual network.</span></span>

    ![Domain Services - Properties tab after fully provisioned](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="need-help"></a><span data-ttu-id="431f0-149">Need help?</span><span class="sxs-lookup"><span data-stu-id="431f0-149">Need help?</span></span>
<span data-ttu-id="431f0-150">It may take an hour or two for both domain controllers for your managed domain to be provisioned.</span><span class="sxs-lookup"><span data-stu-id="431f0-150">It may take an hour or two for both domain controllers for your managed domain to be provisioned.</span></span> <span data-ttu-id="431f0-151">If your deployment failed or is stuck in the 'Pending' state for more than a couple of hours, feel free to [contact the product team for help](active-directory-ds-contact-us.md).</span><span class="sxs-lookup"><span data-stu-id="431f0-151">If your deployment failed or is stuck in the 'Pending' state for more than a couple of hours, feel free to [contact the product team for help](active-directory-ds-contact-us.md).</span></span>


## <a name="next-step"></a><span data-ttu-id="431f0-152">Next step</span><span class="sxs-lookup"><span data-stu-id="431f0-152">Next step</span></span>
[<span data-ttu-id="431f0-153">Task 4: update the DNS settings for the Azure virtual network</span><span class="sxs-lookup"><span data-stu-id="431f0-153">Task 4: update the DNS settings for the Azure virtual network</span></span>](active-directory-ds-getting-started-dns.md)
