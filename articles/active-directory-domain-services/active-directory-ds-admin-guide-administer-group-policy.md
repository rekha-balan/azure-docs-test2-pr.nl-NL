---
title: 'Azure Active Directory Domain Services: Administer Group Policy on managed domains | Microsoft Docs'
description: Administer Group Policy on Azure Active Directory Domain Services managed domains
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: mtillman
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory
ms.component: domain-services
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 06/22/2018
ms.author: maheshu
ms.openlocfilehash: acdba45bef5407af4b96d8e5f805a828e10d2d61
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44789430"
---
# <a name="administer-group-policy-on-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="c1dd6-103">Administer Group Policy on an Azure AD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="c1dd6-103">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="c1dd6-104">Azure Active Directory Domain Services includes built-in Group Policy Objects (GPOs) for the 'AADDC Users' and 'AADDC Computers' containers.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-104">Azure Active Directory Domain Services includes built-in Group Policy Objects (GPOs) for the 'AADDC Users' and 'AADDC Computers' containers.</span></span> <span data-ttu-id="c1dd6-105">You can customize these built-in GPOs to configure Group Policy on the managed domain.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-105">You can customize these built-in GPOs to configure Group Policy on the managed domain.</span></span> <span data-ttu-id="c1dd6-106">Additionally, members of the 'AAD DC Administrators' group can create their own custom OUs in the managed domain.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-106">Additionally, members of the 'AAD DC Administrators' group can create their own custom OUs in the managed domain.</span></span> <span data-ttu-id="c1dd6-107">They can also create custom GPOs and link them to these custom OUs.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-107">They can also create custom GPOs and link them to these custom OUs.</span></span> <span data-ttu-id="c1dd6-108">Users who belong to the 'AAD DC Administrators' group are granted Group Policy administration privileges on the managed domain.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-108">Users who belong to the 'AAD DC Administrators' group are granted Group Policy administration privileges on the managed domain.</span></span>

[!INCLUDE [active-directory-ds-prerequisites.md](../../includes/active-directory-ds-prerequisites.md)]

## <a name="before-you-begin"></a><span data-ttu-id="c1dd6-109">Before you begin</span><span class="sxs-lookup"><span data-stu-id="c1dd6-109">Before you begin</span></span>
<span data-ttu-id="c1dd6-110">To perform the tasks listed in this article, you need:</span><span class="sxs-lookup"><span data-stu-id="c1dd6-110">To perform the tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="c1dd6-111">A valid **Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-111">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="c1dd6-112">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-112">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="c1dd6-113">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-113">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span></span> <span data-ttu-id="c1dd6-114">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="c1dd6-114">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="c1dd6-115">A **domain-joined virtual machine** from which you administer the Azure AD Domain Services managed domain.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-115">A **domain-joined virtual machine** from which you administer the Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="c1dd6-116">If you don't have such a virtual machine, follow all the tasks outlined in the article titled [Join a Windows virtual machine to a managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span><span class="sxs-lookup"><span data-stu-id="c1dd6-116">If you don't have such a virtual machine, follow all the tasks outlined in the article titled [Join a Windows virtual machine to a managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>
5. <span data-ttu-id="c1dd6-117">You need the credentials of a **user account belonging to the 'AAD DC Administrators' group** in your directory, to administer Group Policy for your managed domain.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-117">You need the credentials of a **user account belonging to the 'AAD DC Administrators' group** in your directory, to administer Group Policy for your managed domain.</span></span>

<br>

## <a name="task-1---provision-a-domain-joined-virtual-machine-to-remotely-administer-group-policy-for-the-managed-domain"></a><span data-ttu-id="c1dd6-118">Task 1 - Provision a domain-joined virtual machine to remotely administer Group Policy for the managed domain</span><span class="sxs-lookup"><span data-stu-id="c1dd6-118">Task 1 - Provision a domain-joined virtual machine to remotely administer Group Policy for the managed domain</span></span>
<span data-ttu-id="c1dd6-119">Azure AD Domain Services managed domains can be managed remotely using familiar Active Directory administrative tools such as the Active Directory Administrative Center (ADAC) or AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-119">Azure AD Domain Services managed domains can be managed remotely using familiar Active Directory administrative tools such as the Active Directory Administrative Center (ADAC) or AD PowerShell.</span></span> <span data-ttu-id="c1dd6-120">Similarly, Group Policy for the managed domain can be administered remotely using the Group Policy administration tools.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-120">Similarly, Group Policy for the managed domain can be administered remotely using the Group Policy administration tools.</span></span>

<span data-ttu-id="c1dd6-121">Administrators in your Azure AD directory do not have privileges to connect to domain controllers on the managed domain via Remote Desktop.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-121">Administrators in your Azure AD directory do not have privileges to connect to domain controllers on the managed domain via Remote Desktop.</span></span> <span data-ttu-id="c1dd6-122">Members of the 'AAD DC Administrators' group can administer Group Policy for managed domains remotely.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-122">Members of the 'AAD DC Administrators' group can administer Group Policy for managed domains remotely.</span></span> <span data-ttu-id="c1dd6-123">They can use Group Policy tools on a Windows Server/client computer joined to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-123">They can use Group Policy tools on a Windows Server/client computer joined to the managed domain.</span></span> <span data-ttu-id="c1dd6-124">Group Policy tools can be installed as part of the Group Policy Management optional feature on Windows Server and client machines joined to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-124">Group Policy tools can be installed as part of the Group Policy Management optional feature on Windows Server and client machines joined to the managed domain.</span></span>

<span data-ttu-id="c1dd6-125">The first task is to provision a Windows Server virtual machine that is joined to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-125">The first task is to provision a Windows Server virtual machine that is joined to the managed domain.</span></span> <span data-ttu-id="c1dd6-126">For instructions, refer to the article titled [join a Windows Server virtual machine to an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span><span class="sxs-lookup"><span data-stu-id="c1dd6-126">For instructions, refer to the article titled [join a Windows Server virtual machine to an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>

## <a name="task-2---install-group-policy-tools-on-the-virtual-machine"></a><span data-ttu-id="c1dd6-127">Task 2 - Install Group Policy tools on the virtual machine</span><span class="sxs-lookup"><span data-stu-id="c1dd6-127">Task 2 - Install Group Policy tools on the virtual machine</span></span>
<span data-ttu-id="c1dd6-128">Perform the following steps to install the Group Policy Administration tools on the domain joined virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-128">Perform the following steps to install the Group Policy Administration tools on the domain joined virtual machine.</span></span>

1. <span data-ttu-id="c1dd6-129">Navigate to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-129">Navigate to the Azure portal.</span></span> <span data-ttu-id="c1dd6-130">Click **All resources** on the left-hand panel.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-130">Click **All resources** on the left-hand panel.</span></span> <span data-ttu-id="c1dd6-131">Locate and click the virtual machine you created in Task 1.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-131">Locate and click the virtual machine you created in Task 1.</span></span>
2. <span data-ttu-id="c1dd6-132">Click the **Connect** button on the Overview tab. A Remote Desktop Protocol (.rdp) file is created and downloaded.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-132">Click the **Connect** button on the Overview tab. A Remote Desktop Protocol (.rdp) file is created and downloaded.</span></span>

    ![Connect to Windows virtual machine](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
3. <span data-ttu-id="c1dd6-134">To connect to your VM, open the downloaded RDP file.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-134">To connect to your VM, open the downloaded RDP file.</span></span> <span data-ttu-id="c1dd6-135">If prompted, click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-135">If prompted, click **Connect**.</span></span> <span data-ttu-id="c1dd6-136">At the login prompt, use the credentials of a user belonging to the 'AAD DC Administrators' group.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-136">At the login prompt, use the credentials of a user belonging to the 'AAD DC Administrators' group.</span></span> <span data-ttu-id="c1dd6-137">For example, we use 'bob@domainservicespreview.onmicrosoft.com' in our case.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-137">For example, we use 'bob@domainservicespreview.onmicrosoft.com' in our case.</span></span> <span data-ttu-id="c1dd6-138">You may receive a certificate warning during the sign-in process.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-138">You may receive a certificate warning during the sign-in process.</span></span> <span data-ttu-id="c1dd6-139">Click Yes or Continue to proceed with the connection.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-139">Click Yes or Continue to proceed with the connection.</span></span>
4. <span data-ttu-id="c1dd6-140">From the Start screen, open **Server Manager**.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-140">From the Start screen, open **Server Manager**.</span></span> <span data-ttu-id="c1dd6-141">Click **Add Roles and Features** in the central pane of the Server Manager window.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-141">Click **Add Roles and Features** in the central pane of the Server Manager window.</span></span>

    ![Launch Server Manager on virtual machine](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager.png)
5. <span data-ttu-id="c1dd6-143">On the **Before You Begin** page of the **Add Roles and Features Wizard**, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-143">On the **Before You Begin** page of the **Add Roles and Features Wizard**, click **Next**.</span></span>

    ![Before You Begin page](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-begin.png)
6. <span data-ttu-id="c1dd6-145">On the **Installation Type** page, leave the **Role-based or feature-based installation** option checked and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-145">On the **Installation Type** page, leave the **Role-based or feature-based installation** option checked and click **Next**.</span></span>

    ![Installation Type page](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-type.png)
7. <span data-ttu-id="c1dd6-147">On the **Server Selection** page, select the current virtual machine from the server pool, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-147">On the **Server Selection** page, select the current virtual machine from the server pool, and click **Next**.</span></span>

    ![Server Selection page](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-server.png)
8. <span data-ttu-id="c1dd6-149">On the **Server Roles** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-149">On the **Server Roles** page, click **Next**.</span></span> <span data-ttu-id="c1dd6-150">We skip this page since we are not installing any roles on the server.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-150">We skip this page since we are not installing any roles on the server.</span></span>
9. <span data-ttu-id="c1dd6-151">On the **Features** page, select the **Group Policy Management** feature.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-151">On the **Features** page, select the **Group Policy Management** feature.</span></span>

    ![Features page](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management.png)
10. <span data-ttu-id="c1dd6-153">On the **Confirmation** page, click **Install** to install the Group Policy Management feature on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-153">On the **Confirmation** page, click **Install** to install the Group Policy Management feature on the virtual machine.</span></span> <span data-ttu-id="c1dd6-154">When feature installation completes successfully, click **Close** to exit the **Add Roles and Features** wizard.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-154">When feature installation completes successfully, click **Close** to exit the **Add Roles and Features** wizard.</span></span>

    ![Confirmation page](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management-confirmation.png)

## <a name="task-3---launch-the-group-policy-management-console-to-administer-group-policy"></a><span data-ttu-id="c1dd6-156">Task 3 - Launch the Group Policy management console to administer Group Policy</span><span class="sxs-lookup"><span data-stu-id="c1dd6-156">Task 3 - Launch the Group Policy management console to administer Group Policy</span></span>
<span data-ttu-id="c1dd6-157">You can use the Group Policy management console on the domain-joined virtual machine to administer Group Policy on the managed domain.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-157">You can use the Group Policy management console on the domain-joined virtual machine to administer Group Policy on the managed domain.</span></span>

> [!NOTE]
> <span data-ttu-id="c1dd6-158">You need to be a member of the 'AAD DC Administrators' group, to administer Group Policy on the managed domain.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-158">You need to be a member of the 'AAD DC Administrators' group, to administer Group Policy on the managed domain.</span></span>
>
>

1. <span data-ttu-id="c1dd6-159">From the Start screen, click **Administrative Tools**.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-159">From the Start screen, click **Administrative Tools**.</span></span> <span data-ttu-id="c1dd6-160">You should see the **Group Policy Management** console installed on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-160">You should see the **Group Policy Management** console installed on the virtual machine.</span></span>

    ![Launch Group Policy Management](./media/active-directory-domain-services-admin-guide/gp-management-installed.png)
2. <span data-ttu-id="c1dd6-162">Click **Group Policy Management** to launch the Group Policy Management console.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-162">Click **Group Policy Management** to launch the Group Policy Management console.</span></span>

    ![Group Policy Console](./media/active-directory-domain-services-admin-guide/gp-management-console.png)

## <a name="task-4---customize-built-in-group-policy-objects"></a><span data-ttu-id="c1dd6-164">Task 4 - Customize built-in Group Policy Objects</span><span class="sxs-lookup"><span data-stu-id="c1dd6-164">Task 4 - Customize built-in Group Policy Objects</span></span>
<span data-ttu-id="c1dd6-165">There are two built-in Group Policy Objects (GPOs) - one each for the 'AADDC Computers' and 'AADDC Users' containers in your managed domain.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-165">There are two built-in Group Policy Objects (GPOs) - one each for the 'AADDC Computers' and 'AADDC Users' containers in your managed domain.</span></span> <span data-ttu-id="c1dd6-166">You can customize these GPOs to configure group policy on the managed domain.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-166">You can customize these GPOs to configure group policy on the managed domain.</span></span>

1. <span data-ttu-id="c1dd6-167">In the **Group Policy Management** console, click to expand the **Forest: contoso100.com** and **Domains** nodes to see the group policies for your managed domain.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-167">In the **Group Policy Management** console, click to expand the **Forest: contoso100.com** and **Domains** nodes to see the group policies for your managed domain.</span></span>

    ![Built-in GPOs](./media/active-directory-domain-services-admin-guide/builtin-gpos.png)
2. <span data-ttu-id="c1dd6-169">You can customize these built-in GPOs to configure group policies on your managed domain.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-169">You can customize these built-in GPOs to configure group policies on your managed domain.</span></span> <span data-ttu-id="c1dd6-170">Right-click the GPO and click **Edit...** to customize the built-in GPO.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-170">Right-click the GPO and click **Edit...** to customize the built-in GPO.</span></span> <span data-ttu-id="c1dd6-171">The Group Policy Configuration Editor tool enables you to customize the GPO.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-171">The Group Policy Configuration Editor tool enables you to customize the GPO.</span></span>

    ![Edit built-in GPO](./media/active-directory-domain-services-admin-guide/edit-builtin-gpo.png)
3. <span data-ttu-id="c1dd6-173">You can now use the **Group Policy Management Editor** console to edit the built-in GPO.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-173">You can now use the **Group Policy Management Editor** console to edit the built-in GPO.</span></span> <span data-ttu-id="c1dd6-174">For instance, the following screenshot shows how to customize the built-in 'AADDC Computers' GPO.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-174">For instance, the following screenshot shows how to customize the built-in 'AADDC Computers' GPO.</span></span>

    ![Customize GPO](./media/active-directory-domain-services-admin-guide/gp-editor.png)

## <a name="task-5---create-a-custom-group-policy-object-gpo"></a><span data-ttu-id="c1dd6-176">Task 5 - Create a custom Group Policy Object (GPO)</span><span class="sxs-lookup"><span data-stu-id="c1dd6-176">Task 5 - Create a custom Group Policy Object (GPO)</span></span>
<span data-ttu-id="c1dd6-177">You can create or import your own custom group policy objects.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-177">You can create or import your own custom group policy objects.</span></span> <span data-ttu-id="c1dd6-178">You can also link custom GPOs to a custom OU you have created in your managed domain.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-178">You can also link custom GPOs to a custom OU you have created in your managed domain.</span></span> <span data-ttu-id="c1dd6-179">For more information on creating custom organizational units, see [create a custom OU on a managed domain](active-directory-ds-admin-guide-create-ou.md).</span><span class="sxs-lookup"><span data-stu-id="c1dd6-179">For more information on creating custom organizational units, see [create a custom OU on a managed domain](active-directory-ds-admin-guide-create-ou.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c1dd6-180">You need to be a member of the 'AAD DC Administrators' group, to administer Group Policy on the managed domain.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-180">You need to be a member of the 'AAD DC Administrators' group, to administer Group Policy on the managed domain.</span></span>
>
>

1. <span data-ttu-id="c1dd6-181">In the **Group Policy Management** console, click to select your custom organizational unit (OU).</span><span class="sxs-lookup"><span data-stu-id="c1dd6-181">In the **Group Policy Management** console, click to select your custom organizational unit (OU).</span></span> <span data-ttu-id="c1dd6-182">Right-click the OU and click **Create a GPO in this domain, and Link it here...**.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-182">Right-click the OU and click **Create a GPO in this domain, and Link it here...**.</span></span>

    ![Create a custom GPO](./media/active-directory-domain-services-admin-guide/gp-create-gpo.png)
2. <span data-ttu-id="c1dd6-184">Specify a name for the new GPO and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-184">Specify a name for the new GPO and click **OK**.</span></span>

    ![Specify a name for GPO](./media/active-directory-domain-services-admin-guide/gp-specify-gpo-name.png)
3. <span data-ttu-id="c1dd6-186">A new GPO is created and linked to your custom OU.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-186">A new GPO is created and linked to your custom OU.</span></span> <span data-ttu-id="c1dd6-187">Right-click the GPO and click **Edit...** from the menu.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-187">Right-click the GPO and click **Edit...** from the menu.</span></span>

    ![Newly created GPO](./media/active-directory-domain-services-admin-guide/gp-gpo-created.png)
4. <span data-ttu-id="c1dd6-189">You can customize the newly created GPO using the **Group Policy Management Editor**.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-189">You can customize the newly created GPO using the **Group Policy Management Editor**.</span></span>

    ![Customize new GPO](./media/active-directory-domain-services-admin-guide/gp-customize-gpo.png)


<span data-ttu-id="c1dd6-191">More information about using [Group Policy Management Console](https://technet.microsoft.com/library/cc753298.aspx) is available on Technet.</span><span class="sxs-lookup"><span data-stu-id="c1dd6-191">More information about using [Group Policy Management Console](https://technet.microsoft.com/library/cc753298.aspx) is available on Technet.</span></span>

## <a name="related-content"></a><span data-ttu-id="c1dd6-192">Related Content</span><span class="sxs-lookup"><span data-stu-id="c1dd6-192">Related Content</span></span>
* [<span data-ttu-id="c1dd6-193">Azure AD Domain Services - Getting Started guide</span><span class="sxs-lookup"><span data-stu-id="c1dd6-193">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="c1dd6-194">Join a Windows Server virtual machine to an Azure AD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="c1dd6-194">Join a Windows Server virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="c1dd6-195">Administer an Azure AD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="c1dd6-195">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="c1dd6-196">Group Policy Management Console</span><span class="sxs-lookup"><span data-stu-id="c1dd6-196">Group Policy Management Console</span></span>](https://technet.microsoft.com/library/cc753298.aspx)
