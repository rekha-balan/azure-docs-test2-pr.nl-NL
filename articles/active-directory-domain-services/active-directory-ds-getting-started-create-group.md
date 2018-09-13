---
title: 'Azure Active Directory Domain Services: Create the Azure AD DC administrators group | Microsoft Docs'
description: Getting started with Azure Active Directory Domain Services
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: maheshu
ms.openlocfilehash: bde4a5a215cc072ea014c030c22e5910014d0f72
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551628"
---
# <a name="get-started-with-azure-active-directory-domain-services"></a><span data-ttu-id="80596-103">Get started with Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="80596-103">Get started with Azure Active Directory Domain Services</span></span>
<span data-ttu-id="80596-104">This article describes and walks through the configuration tasks that are required for you to enable Azure Active Directory Domain Services (Azure AD DS) for your Azure Active Directory (Azure AD) tenant.</span><span class="sxs-lookup"><span data-stu-id="80596-104">This article describes and walks through the configuration tasks that are required for you to enable Azure Active Directory Domain Services (Azure AD DS) for your Azure Active Directory (Azure AD) tenant.</span></span>

## <a name="task-1-create-the-azure-ad-dc-administrators-group"></a><span data-ttu-id="80596-105">Task 1: Create the Azure AD DC administrators group</span><span class="sxs-lookup"><span data-stu-id="80596-105">Task 1: Create the Azure AD DC administrators group</span></span>
<span data-ttu-id="80596-106">The first task is to create an administrative group in your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="80596-106">The first task is to create an administrative group in your Azure AD tenant.</span></span> <span data-ttu-id="80596-107">This special administrative group is called *AAD DC Administrators*.</span><span class="sxs-lookup"><span data-stu-id="80596-107">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="80596-108">Members of this group are granted administrative permissions on machines that are domain-joined to the Azure Active Directory Domain Services-managed domain.</span><span class="sxs-lookup"><span data-stu-id="80596-108">Members of this group are granted administrative permissions on machines that are domain-joined to the Azure Active Directory Domain Services-managed domain.</span></span> <span data-ttu-id="80596-109">On domain-joined machines, this group is added to the administrators group.</span><span class="sxs-lookup"><span data-stu-id="80596-109">On domain-joined machines, this group is added to the administrators group.</span></span> <span data-ttu-id="80596-110">Additionally, members of this group can use Remote Desktop to connect remotely to domain-joined machines.</span><span class="sxs-lookup"><span data-stu-id="80596-110">Additionally, members of this group can use Remote Desktop to connect remotely to domain-joined machines.</span></span>  

> [!NOTE]
> <span data-ttu-id="80596-111">You do not have Domain Administrator or Enterprise Administrator permissions on the managed domain that you created by using Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="80596-111">You do not have Domain Administrator or Enterprise Administrator permissions on the managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="80596-112">On managed domains, these permissions are reserved by the service and are not made available to users within the tenant.</span><span class="sxs-lookup"><span data-stu-id="80596-112">On managed domains, these permissions are reserved by the service and are not made available to users within the tenant.</span></span> <span data-ttu-id="80596-113">However, you can use the special administrative group created in this configuration task to perform some privileged operations.</span><span class="sxs-lookup"><span data-stu-id="80596-113">However, you can use the special administrative group created in this configuration task to perform some privileged operations.</span></span> <span data-ttu-id="80596-114">These operations include joining computers to the domain, belonging to the administration group on domain-joined machines, and configuring Group Policy.</span><span class="sxs-lookup"><span data-stu-id="80596-114">These operations include joining computers to the domain, belonging to the administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="80596-115">In this configuration task, you create the administrative group and add one or more users in your directory to the group.</span><span class="sxs-lookup"><span data-stu-id="80596-115">In this configuration task, you create the administrative group and add one or more users in your directory to the group.</span></span> <span data-ttu-id="80596-116">To create the administrative group for Azure Active Directory Domain Services, do the following:</span><span class="sxs-lookup"><span data-stu-id="80596-116">To create the administrative group for Azure Active Directory Domain Services, do the following:</span></span>

1. <span data-ttu-id="80596-117">Go to the [Azure classic portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="80596-117">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="80596-118">In the left pane, select the **Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="80596-118">In the left pane, select the **Active Directory** button.</span></span>
3. <span data-ttu-id="80596-119">Select the Azure AD tenant (directory) for which you want to enable Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="80596-119">Select the Azure AD tenant (directory) for which you want to enable Azure Active Directory Domain Services.</span></span> <span data-ttu-id="80596-120">You can create only one domain for each Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="80596-120">You can create only one domain for each Azure AD directory.</span></span>

    ![Select Azure AD directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="80596-122">On the **preview directory** page, click the **Groups** tab.</span><span class="sxs-lookup"><span data-stu-id="80596-122">On the **preview directory** page, click the **Groups** tab.</span></span>
5. <span data-ttu-id="80596-123">To add a group to your Azure AD tenant, on the task pane at the bottom of the window, click **Add Group**.</span><span class="sxs-lookup"><span data-stu-id="80596-123">To add a group to your Azure AD tenant, on the task pane at the bottom of the window, click **Add Group**.</span></span>

    ![The Add Group button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/add-group-button.png)
6. <span data-ttu-id="80596-125">In the **Add Group** dialog box, create a group named **AAD DC Administrators**, and then set **Group Type** to **Security**.</span><span class="sxs-lookup"><span data-stu-id="80596-125">In the **Add Group** dialog box, create a group named **AAD DC Administrators**, and then set **Group Type** to **Security**.</span></span>

   > [!WARNING]
   > <span data-ttu-id="80596-126">To enable access within your Azure Active Directory Domain Services-managed domain, create a group with this exact name.</span><span class="sxs-lookup"><span data-stu-id="80596-126">To enable access within your Azure Active Directory Domain Services-managed domain, create a group with this exact name.</span></span>
   >
   >

    ![The Add Group dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/create-admin-group.png)
7. <span data-ttu-id="80596-128">In the **Description** box, enter a description that enables others to understand that this group grants administrative permissions within Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="80596-128">In the **Description** box, enter a description that enables others to understand that this group grants administrative permissions within Azure Active Directory Domain Services.</span></span>
8. <span data-ttu-id="80596-129">After you've created the group, click the group name to view its properties.</span><span class="sxs-lookup"><span data-stu-id="80596-129">After you've created the group, click the group name to view its properties.</span></span> 
9. <span data-ttu-id="80596-130">To add users as members of the group, at the bottom of the window, click the **Add Members** button.</span><span class="sxs-lookup"><span data-stu-id="80596-130">To add users as members of the group, at the bottom of the window, click the **Add Members** button.</span></span>

    ![Add group members button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/add-group-members-button.png)
10. <span data-ttu-id="80596-132">In the **Add members** dialog box, select the users who should be members of this group, and then click the checkmark icon at the lower right.</span><span class="sxs-lookup"><span data-stu-id="80596-132">In the **Add members** dialog box, select the users who should be members of this group, and then click the checkmark icon at the lower right.</span></span>

    ![Add users to administrators group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/add-group-members.png)

## <a name="next-steps"></a><span data-ttu-id="80596-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="80596-134">Next steps</span></span>
<span data-ttu-id="80596-135">Task 2: [Create or select an Azure virtual network](active-directory-ds-getting-started-vnet.md)</span><span class="sxs-lookup"><span data-stu-id="80596-135">Task 2: [Create or select an Azure virtual network](active-directory-ds-getting-started-vnet.md)</span></span>
  





