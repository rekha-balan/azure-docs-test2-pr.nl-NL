---
title: 'Azure Active Directory Domain Services: Administer Group Policy on managed domains | Microsoft Docs'
description: Administer Group Policy on Azure Active Directory Domain Services managed domains
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 591cf1b89a674acfd5f1537c6b4559195fd94144
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564350"
---
# <a name="administer-group-policy-on-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="97d7b-103">Administer Group Policy on an Azure AD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="97d7b-103">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="97d7b-104">Azure Active Directory Domain Services includes built-in Group Policy Objects (GPOs) for the 'AADDC Users' and 'AADDC Computers' containers.</span><span class="sxs-lookup"><span data-stu-id="97d7b-104">Azure Active Directory Domain Services includes built-in Group Policy Objects (GPOs) for the 'AADDC Users' and 'AADDC Computers' containers.</span></span> <span data-ttu-id="97d7b-105">You can customize these built-in GPOs to configure Group Policy on the managed domain.</span><span class="sxs-lookup"><span data-stu-id="97d7b-105">You can customize these built-in GPOs to configure Group Policy on the managed domain.</span></span> <span data-ttu-id="97d7b-106">Additionally, members of the 'AAD DC Administrators' group can create their own custom OUs in the managed domain.</span><span class="sxs-lookup"><span data-stu-id="97d7b-106">Additionally, members of the 'AAD DC Administrators' group can create their own custom OUs in the managed domain.</span></span> <span data-ttu-id="97d7b-107">They can also create custom GPOs and link them to these custom OUs.</span><span class="sxs-lookup"><span data-stu-id="97d7b-107">They can also create custom GPOs and link them to these custom OUs.</span></span> <span data-ttu-id="97d7b-108">Users who belong to the 'AAD DC Administrators' group are granted Group Policy administration privileges on the managed domain.</span><span class="sxs-lookup"><span data-stu-id="97d7b-108">Users who belong to the 'AAD DC Administrators' group are granted Group Policy administration privileges on the managed domain.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="97d7b-109">Before you begin</span><span class="sxs-lookup"><span data-stu-id="97d7b-109">Before you begin</span></span>
<span data-ttu-id="97d7b-110">To perform the tasks listed in this article, you need:</span><span class="sxs-lookup"><span data-stu-id="97d7b-110">To perform the tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="97d7b-111">A valid **Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="97d7b-111">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="97d7b-112">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span><span class="sxs-lookup"><span data-stu-id="97d7b-112">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="97d7b-113">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="97d7b-113">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span></span> <span data-ttu-id="97d7b-114">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="97d7b-114">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="97d7b-115">A **domain-joined virtual machine** from which you administer the Azure AD Domain Services managed domain.</span><span class="sxs-lookup"><span data-stu-id="97d7b-115">A **domain-joined virtual machine** from which you administer the Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="97d7b-116">If you don't have such a virtual machine, follow all the tasks outlined in the article titled [Join a Windows virtual machine to a managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span><span class="sxs-lookup"><span data-stu-id="97d7b-116">If you don't have such a virtual machine, follow all the tasks outlined in the article titled [Join a Windows virtual machine to a managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>
5. <span data-ttu-id="97d7b-117">You need the credentials of a **user account belonging to the 'AAD DC Administrators' group** in your directory, to administer Group Policy for your managed domain.</span><span class="sxs-lookup"><span data-stu-id="97d7b-117">You need the credentials of a **user account belonging to the 'AAD DC Administrators' group** in your directory, to administer Group Policy for your managed domain.</span></span>

<br>

## <a name="task-1---provision-a-domain-joined-virtual-machine-to-remotely-administer-group-policy-for-the-managed-domain"></a><span data-ttu-id="97d7b-118">Task 1 - Provision a domain-joined virtual machine to remotely administer Group Policy for the managed domain</span><span class="sxs-lookup"><span data-stu-id="97d7b-118">Task 1 - Provision a domain-joined virtual machine to remotely administer Group Policy for the managed domain</span></span>
<span data-ttu-id="97d7b-119">Azure AD Domain Services managed domains can be managed remotely using familiar Active Directory administrative tools such as the Active Directory Administrative Center (ADAC) or AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="97d7b-119">Azure AD Domain Services managed domains can be managed remotely using familiar Active Directory administrative tools such as the Active Directory Administrative Center (ADAC) or AD PowerShell.</span></span> <span data-ttu-id="97d7b-120">Similarly, Group Policy for the managed domain can be administered remotely using the Group Policy administration tools.</span><span class="sxs-lookup"><span data-stu-id="97d7b-120">Similarly, Group Policy for the managed domain can be administered remotely using the Group Policy administration tools.</span></span>

<span data-ttu-id="97d7b-121">Administrators in your Azure AD directory do not have privileges to connect to domain controllers on the managed domain via Remote Desktop.</span><span class="sxs-lookup"><span data-stu-id="97d7b-121">Administrators in your Azure AD directory do not have privileges to connect to domain controllers on the managed domain via Remote Desktop.</span></span> <span data-ttu-id="97d7b-122">Members of the 'AAD DC Administrators' group can administer Group Policy for managed domains remotely.</span><span class="sxs-lookup"><span data-stu-id="97d7b-122">Members of the 'AAD DC Administrators' group can administer Group Policy for managed domains remotely.</span></span> <span data-ttu-id="97d7b-123">They can use Group Policy tools on a Windows Server/client computer joined to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="97d7b-123">They can use Group Policy tools on a Windows Server/client computer joined to the managed domain.</span></span> <span data-ttu-id="97d7b-124">Group Policy tools can be installed as part of the Group Policy Management optional feature on Windows Server and client machines joined to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="97d7b-124">Group Policy tools can be installed as part of the Group Policy Management optional feature on Windows Server and client machines joined to the managed domain.</span></span>

<span data-ttu-id="97d7b-125">The first task is to provision a Windows Server virtual machine that is joined to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="97d7b-125">The first task is to provision a Windows Server virtual machine that is joined to the managed domain.</span></span> <span data-ttu-id="97d7b-126">For instructions, refer to the article titled [join a Windows Server virtual machine to an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span><span class="sxs-lookup"><span data-stu-id="97d7b-126">For instructions, refer to the article titled [join a Windows Server virtual machine to an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>

## <a name="task-2---install-group-policy-tools-on-the-virtual-machine"></a><span data-ttu-id="97d7b-127">Task 2 - Install Group Policy tools on the virtual machine</span><span class="sxs-lookup"><span data-stu-id="97d7b-127">Task 2 - Install Group Policy tools on the virtual machine</span></span>
<span data-ttu-id="97d7b-128">Perform the following steps to install the Group Policy Administration tools on the domain joined virtual machine.</span><span class="sxs-lookup"><span data-stu-id="97d7b-128">Perform the following steps to install the Group Policy Administration tools on the domain joined virtual machine.</span></span>

1. <span data-ttu-id="97d7b-129">Navigate to **Virtual Machines** node in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="97d7b-129">Navigate to **Virtual Machines** node in the Azure classic portal.</span></span> <span data-ttu-id="97d7b-130">Select the virtual machine you created in Task 1 and click **Connect** on the command bar at the bottom of the window.</span><span class="sxs-lookup"><span data-stu-id="97d7b-130">Select the virtual machine you created in Task 1 and click **Connect** on the command bar at the bottom of the window.</span></span>

    ![Connect to Windows virtual machine](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. <span data-ttu-id="97d7b-132">The classic portal prompts you to open or save a file with a '.rdp' extension, which is used to connect to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="97d7b-132">The classic portal prompts you to open or save a file with a '.rdp' extension, which is used to connect to the virtual machine.</span></span> <span data-ttu-id="97d7b-133">Click the file when it has finished downloading.</span><span class="sxs-lookup"><span data-stu-id="97d7b-133">Click the file when it has finished downloading.</span></span>
3. <span data-ttu-id="97d7b-134">At the login prompt, use the credentials of a user belonging to the 'AAD DC Administrators' group.</span><span class="sxs-lookup"><span data-stu-id="97d7b-134">At the login prompt, use the credentials of a user belonging to the 'AAD DC Administrators' group.</span></span> <span data-ttu-id="97d7b-135">For example, we use 'bob@domainservicespreview.onmicrosoft.com' in our case.</span><span class="sxs-lookup"><span data-stu-id="97d7b-135">For example, we use 'bob@domainservicespreview.onmicrosoft.com' in our case.</span></span>
4. <span data-ttu-id="97d7b-136">From the Start screen, open **Server Manager**.</span><span class="sxs-lookup"><span data-stu-id="97d7b-136">From the Start screen, open **Server Manager**.</span></span> <span data-ttu-id="97d7b-137">Click **Add Roles and Features** in the central pane of the Server Manager window.</span><span class="sxs-lookup"><span data-stu-id="97d7b-137">Click **Add Roles and Features** in the central pane of the Server Manager window.</span></span>

    ![Launch Server Manager on virtual machine](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/install-rsat-server-manager.png)
5. <span data-ttu-id="97d7b-139">On the **Before You Begin** page of the **Add Roles and Features Wizard**, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="97d7b-139">On the **Before You Begin** page of the **Add Roles and Features Wizard**, click **Next**.</span></span>

    ![Before You Begin page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-begin.png)
6. <span data-ttu-id="97d7b-141">On the **Installation Type** page, leave the **Role-based or feature-based installation** option checked and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="97d7b-141">On the **Installation Type** page, leave the **Role-based or feature-based installation** option checked and click **Next**.</span></span>

    ![Installation Type page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-type.png)
7. <span data-ttu-id="97d7b-143">On the **Server Selection** page, select the current virtual machine from the server pool, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="97d7b-143">On the **Server Selection** page, select the current virtual machine from the server pool, and click **Next**.</span></span>

    ![Server Selection page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-server.png)
8. <span data-ttu-id="97d7b-145">On the **Server Roles** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="97d7b-145">On the **Server Roles** page, click **Next**.</span></span> <span data-ttu-id="97d7b-146">We skip this page since we are not installing any roles on the server.</span><span class="sxs-lookup"><span data-stu-id="97d7b-146">We skip this page since we are not installing any roles on the server.</span></span>
9. <span data-ttu-id="97d7b-147">On the **Features** page, select the **Group Policy Management** feature.</span><span class="sxs-lookup"><span data-stu-id="97d7b-147">On the **Features** page, select the **Group Policy Management** feature.</span></span>

    ![Features page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management.png)
10. <span data-ttu-id="97d7b-149">On the **Confirmation** page, click **Install** to install the Group Policy Management feature on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="97d7b-149">On the **Confirmation** page, click **Install** to install the Group Policy Management feature on the virtual machine.</span></span> <span data-ttu-id="97d7b-150">When feature installation completes successfully, click **Close** to exit the **Add Roles and Features** wizard.</span><span class="sxs-lookup"><span data-stu-id="97d7b-150">When feature installation completes successfully, click **Close** to exit the **Add Roles and Features** wizard.</span></span>

    ![Confirmation page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management-confirmation.png)

## <a name="task-3---launch-the-group-policy-management-console-to-administer-group-policy"></a><span data-ttu-id="97d7b-152">Task 3 - Launch the Group Policy management console to administer Group Policy</span><span class="sxs-lookup"><span data-stu-id="97d7b-152">Task 3 - Launch the Group Policy management console to administer Group Policy</span></span>
<span data-ttu-id="97d7b-153">You can use the Group Policy management console on the domain-joined virtual machine to administer Group Policy on the managed domain.</span><span class="sxs-lookup"><span data-stu-id="97d7b-153">You can use the Group Policy management console on the domain-joined virtual machine to administer Group Policy on the managed domain.</span></span>

> [!NOTE]
> <span data-ttu-id="97d7b-154">You need to be a member of the 'AAD DC Administrators' group, to administer Group Policy on the managed domain.</span><span class="sxs-lookup"><span data-stu-id="97d7b-154">You need to be a member of the 'AAD DC Administrators' group, to administer Group Policy on the managed domain.</span></span>
>
>

1. <span data-ttu-id="97d7b-155">From the Start screen, click **Administrative Tools**.</span><span class="sxs-lookup"><span data-stu-id="97d7b-155">From the Start screen, click **Administrative Tools**.</span></span> <span data-ttu-id="97d7b-156">You should see the **Group Policy Management** console installed on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="97d7b-156">You should see the **Group Policy Management** console installed on the virtual machine.</span></span>

    ![Launch Group Policy Management](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/gp-management-installed.png)
2. <span data-ttu-id="97d7b-158">Click **Group Policy Management** to launch the Group Policy Management console.</span><span class="sxs-lookup"><span data-stu-id="97d7b-158">Click **Group Policy Management** to launch the Group Policy Management console.</span></span>

    ![Group Policy Console](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/gp-management-console.png)

## <a name="task-4---customize-built-in-group-policy-objects"></a><span data-ttu-id="97d7b-160">Task 4 - Customize built-in Group Policy Objects</span><span class="sxs-lookup"><span data-stu-id="97d7b-160">Task 4 - Customize built-in Group Policy Objects</span></span>
<span data-ttu-id="97d7b-161">There are two built-in Group Policy Objects (GPOs) - one each for the 'AADDC Computers' and 'AADDC Users' containers in your managed domain.</span><span class="sxs-lookup"><span data-stu-id="97d7b-161">There are two built-in Group Policy Objects (GPOs) - one each for the 'AADDC Computers' and 'AADDC Users' containers in your managed domain.</span></span> <span data-ttu-id="97d7b-162">You can customize these GPOs to configure group policy on the managed domain.</span><span class="sxs-lookup"><span data-stu-id="97d7b-162">You can customize these GPOs to configure group policy on the managed domain.</span></span>

1. <span data-ttu-id="97d7b-163">In the **Group Policy Management** console, click to expand the **Forest: contoso100.com** and **Domains** nodes to see the group policies for your managed domain.</span><span class="sxs-lookup"><span data-stu-id="97d7b-163">In the **Group Policy Management** console, click to expand the **Forest: contoso100.com** and **Domains** nodes to see the group policies for your managed domain.</span></span>

    ![Built-in GPOs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/builtin-gpos.png)
2. <span data-ttu-id="97d7b-165">You can customize these built-in GPOs to configure group policies on your managed domain.</span><span class="sxs-lookup"><span data-stu-id="97d7b-165">You can customize these built-in GPOs to configure group policies on your managed domain.</span></span> <span data-ttu-id="97d7b-166">Right-click the GPO and click **Edit...** to customize the built-in GPO.</span><span class="sxs-lookup"><span data-stu-id="97d7b-166">Right-click the GPO and click **Edit...** to customize the built-in GPO.</span></span> <span data-ttu-id="97d7b-167">The Group Policy Configuration Editor tool enables you to customize the GPO.</span><span class="sxs-lookup"><span data-stu-id="97d7b-167">The Group Policy Configuration Editor tool enables you to customize the GPO.</span></span>

    ![Edit built-in GPO](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/edit-builtin-gpo.png)
3. <span data-ttu-id="97d7b-169">You can now use the **Group Policy Management Editor** console to edit the built-in GPO.</span><span class="sxs-lookup"><span data-stu-id="97d7b-169">You can now use the **Group Policy Management Editor** console to edit the built-in GPO.</span></span> <span data-ttu-id="97d7b-170">For instance, the following screenshot shows how to customize the built-in 'AADDC Computers' GPO.</span><span class="sxs-lookup"><span data-stu-id="97d7b-170">For instance, the following screenshot shows how to customize the built-in 'AADDC Computers' GPO.</span></span>

    ![Customize GPO](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/gp-editor.png)

## <a name="task-5---create-a-custom-group-policy-object-gpo"></a><span data-ttu-id="97d7b-172">Task 5 - Create a custom Group Policy Object (GPO)</span><span class="sxs-lookup"><span data-stu-id="97d7b-172">Task 5 - Create a custom Group Policy Object (GPO)</span></span>
<span data-ttu-id="97d7b-173">You can create or import your own custom group policy objects.</span><span class="sxs-lookup"><span data-stu-id="97d7b-173">You can create or import your own custom group policy objects.</span></span> <span data-ttu-id="97d7b-174">You can also link custom GPOs to a custom OU you have created in your managed domain.</span><span class="sxs-lookup"><span data-stu-id="97d7b-174">You can also link custom GPOs to a custom OU you have created in your managed domain.</span></span> <span data-ttu-id="97d7b-175">For more information on creating custom organizational units, see [create a custom OU on a managed domain](active-directory-ds-admin-guide-create-ou.md).</span><span class="sxs-lookup"><span data-stu-id="97d7b-175">For more information on creating custom organizational units, see [create a custom OU on a managed domain](active-directory-ds-admin-guide-create-ou.md).</span></span>

> [!NOTE]
> <span data-ttu-id="97d7b-176">You need to be a member of the 'AAD DC Administrators' group, to administer Group Policy on the managed domain.</span><span class="sxs-lookup"><span data-stu-id="97d7b-176">You need to be a member of the 'AAD DC Administrators' group, to administer Group Policy on the managed domain.</span></span>
>
>

1. <span data-ttu-id="97d7b-177">In the **Group Policy Management** console, click to select your custom organizational unit (OU).</span><span class="sxs-lookup"><span data-stu-id="97d7b-177">In the **Group Policy Management** console, click to select your custom organizational unit (OU).</span></span> <span data-ttu-id="97d7b-178">Right-click the OU and click **Create a GPO in this domain, and Link it here...**.</span><span class="sxs-lookup"><span data-stu-id="97d7b-178">Right-click the OU and click **Create a GPO in this domain, and Link it here...**.</span></span>

    ![Create a custom GPO](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/gp-create-gpo.png)
2. <span data-ttu-id="97d7b-180">Specify a name for the new GPO and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="97d7b-180">Specify a name for the new GPO and click **OK**.</span></span>

    ![Specify a name for GPO](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/gp-specify-gpo-name.png)
3. <span data-ttu-id="97d7b-182">A new GPO is created and linked to your custom OU.</span><span class="sxs-lookup"><span data-stu-id="97d7b-182">A new GPO is created and linked to your custom OU.</span></span> <span data-ttu-id="97d7b-183">Right-click the GPO and click **Edit...** from the menu.</span><span class="sxs-lookup"><span data-stu-id="97d7b-183">Right-click the GPO and click **Edit...** from the menu.</span></span>

    ![Newly created GPO](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/gp-gpo-created.png)
4. <span data-ttu-id="97d7b-185">You can customize the newly created GPO using the **Group Policy Management Editor**.</span><span class="sxs-lookup"><span data-stu-id="97d7b-185">You can customize the newly created GPO using the **Group Policy Management Editor**.</span></span>

    ![Customize new GPO](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/gp-customize-gpo.png)


<span data-ttu-id="97d7b-187">More information about using [Group Policy Management Console](https://technet.microsoft.com/library/cc753298.aspx) is available on Technet.</span><span class="sxs-lookup"><span data-stu-id="97d7b-187">More information about using [Group Policy Management Console](https://technet.microsoft.com/library/cc753298.aspx) is available on Technet.</span></span>

## <a name="related-content"></a><span data-ttu-id="97d7b-188">Related Content</span><span class="sxs-lookup"><span data-stu-id="97d7b-188">Related Content</span></span>
* [<span data-ttu-id="97d7b-189">Azure AD Domain Services - Getting Started guide</span><span class="sxs-lookup"><span data-stu-id="97d7b-189">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="97d7b-190">Join a Windows Server virtual machine to an Azure AD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="97d7b-190">Join a Windows Server virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="97d7b-191">Administer an Azure AD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="97d7b-191">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="97d7b-192">Group Policy Management Console</span><span class="sxs-lookup"><span data-stu-id="97d7b-192">Group Policy Management Console</span></span>](https://technet.microsoft.com/library/cc753298.aspx)
















