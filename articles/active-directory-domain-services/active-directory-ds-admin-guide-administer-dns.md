---
title: 'Azure Active Directory Domain Services: Administer DNS on managed domains | Microsoft Docs'
description: Administer DNS on Azure Active Directory Domain Services managed domains
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
ms.openlocfilehash: 2682a40c5bdacfe44fa22ff6c3f5afd3e9b041f6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554482"
---
# <a name="administer-dns-on-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="a2adb-103">Administer DNS on an Azure AD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="a2adb-103">Administer DNS on an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="a2adb-104">Azure Active Directory Domain Services includes a DNS (Domain Name Resolution) server that provides DNS resolution for the managed domain.</span><span class="sxs-lookup"><span data-stu-id="a2adb-104">Azure Active Directory Domain Services includes a DNS (Domain Name Resolution) server that provides DNS resolution for the managed domain.</span></span> <span data-ttu-id="a2adb-105">Occasionally, you may need to configure DNS on the managed domain.</span><span class="sxs-lookup"><span data-stu-id="a2adb-105">Occasionally, you may need to configure DNS on the managed domain.</span></span> <span data-ttu-id="a2adb-106">You may need to create DNS records for machines that are not joined to the domain, configure virtual IP addresses for load-balancers or setup external DNS forwarders.</span><span class="sxs-lookup"><span data-stu-id="a2adb-106">You may need to create DNS records for machines that are not joined to the domain, configure virtual IP addresses for load-balancers or setup external DNS forwarders.</span></span> <span data-ttu-id="a2adb-107">For this reason, users who belong to the 'AAD DC Administrators' group are granted DNS administration privileges on the managed domain.</span><span class="sxs-lookup"><span data-stu-id="a2adb-107">For this reason, users who belong to the 'AAD DC Administrators' group are granted DNS administration privileges on the managed domain.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a2adb-108">Before you begin</span><span class="sxs-lookup"><span data-stu-id="a2adb-108">Before you begin</span></span>
<span data-ttu-id="a2adb-109">To perform the tasks listed in this article, you need:</span><span class="sxs-lookup"><span data-stu-id="a2adb-109">To perform the tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="a2adb-110">A valid **Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="a2adb-110">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="a2adb-111">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span><span class="sxs-lookup"><span data-stu-id="a2adb-111">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="a2adb-112">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="a2adb-112">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span></span> <span data-ttu-id="a2adb-113">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="a2adb-113">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="a2adb-114">A **domain-joined virtual machine** from which you administer the Azure AD Domain Services managed domain.</span><span class="sxs-lookup"><span data-stu-id="a2adb-114">A **domain-joined virtual machine** from which you administer the Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="a2adb-115">If you don't have such a virtual machine, follow all the tasks outlined in the article titled [Join a Windows virtual machine to a managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span><span class="sxs-lookup"><span data-stu-id="a2adb-115">If you don't have such a virtual machine, follow all the tasks outlined in the article titled [Join a Windows virtual machine to a managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>
5. <span data-ttu-id="a2adb-116">You need the credentials of a **user account belonging to the 'AAD DC Administrators' group** in your directory, to administer DNS for your managed domain.</span><span class="sxs-lookup"><span data-stu-id="a2adb-116">You need the credentials of a **user account belonging to the 'AAD DC Administrators' group** in your directory, to administer DNS for your managed domain.</span></span>

<br>

## <a name="task-1---provision-a-domain-joined-virtual-machine-to-remotely-administer-dns-for-the-managed-domain"></a><span data-ttu-id="a2adb-117">Task 1 - Provision a domain-joined virtual machine to remotely administer DNS for the managed domain</span><span class="sxs-lookup"><span data-stu-id="a2adb-117">Task 1 - Provision a domain-joined virtual machine to remotely administer DNS for the managed domain</span></span>
<span data-ttu-id="a2adb-118">Azure AD Domain Services managed domains can be managed remotely using familiar Active Directory administrative tools such as the Active Directory Administrative Center (ADAC) or AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a2adb-118">Azure AD Domain Services managed domains can be managed remotely using familiar Active Directory administrative tools such as the Active Directory Administrative Center (ADAC) or AD PowerShell.</span></span> <span data-ttu-id="a2adb-119">Similarly, DNS for the managed domain can be administered remotely using the DNS Server administration tools.</span><span class="sxs-lookup"><span data-stu-id="a2adb-119">Similarly, DNS for the managed domain can be administered remotely using the DNS Server administration tools.</span></span>

<span data-ttu-id="a2adb-120">Administrators in your Azure AD directory do not have privileges to connect to domain controllers on the managed domain via Remote Desktop.</span><span class="sxs-lookup"><span data-stu-id="a2adb-120">Administrators in your Azure AD directory do not have privileges to connect to domain controllers on the managed domain via Remote Desktop.</span></span> <span data-ttu-id="a2adb-121">Members of the 'AAD DC Administrators' group can administer DNS for managed domains remotely using DNS Server tools from a Windows Server/client computer that is joined to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="a2adb-121">Members of the 'AAD DC Administrators' group can administer DNS for managed domains remotely using DNS Server tools from a Windows Server/client computer that is joined to the managed domain.</span></span> <span data-ttu-id="a2adb-122">DNS Server tools can be installed as part of the Remote Server Administration Tools (RSAT) optional feature on Windows Server and client machines joined to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="a2adb-122">DNS Server tools can be installed as part of the Remote Server Administration Tools (RSAT) optional feature on Windows Server and client machines joined to the managed domain.</span></span>

<span data-ttu-id="a2adb-123">The first task is to provision a Windows Server virtual machine that is joined to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="a2adb-123">The first task is to provision a Windows Server virtual machine that is joined to the managed domain.</span></span> <span data-ttu-id="a2adb-124">For instructions, refer to the article titled [join a Windows Server virtual machine to an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span><span class="sxs-lookup"><span data-stu-id="a2adb-124">For instructions, refer to the article titled [join a Windows Server virtual machine to an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>

## <a name="task-2---install-dns-server-tools-on-the-virtual-machine"></a><span data-ttu-id="a2adb-125">Task 2 - Install DNS Server tools on the virtual machine</span><span class="sxs-lookup"><span data-stu-id="a2adb-125">Task 2 - Install DNS Server tools on the virtual machine</span></span>
<span data-ttu-id="a2adb-126">Perform the following steps to install the DNS Administration tools on the domain joined virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a2adb-126">Perform the following steps to install the DNS Administration tools on the domain joined virtual machine.</span></span> <span data-ttu-id="a2adb-127">For more information on [installing and using Remote Server Administration Tools](https://technet.microsoft.com/library/hh831501.aspx), see Technet.</span><span class="sxs-lookup"><span data-stu-id="a2adb-127">For more information on [installing and using Remote Server Administration Tools](https://technet.microsoft.com/library/hh831501.aspx), see Technet.</span></span>

1. <span data-ttu-id="a2adb-128">Navigate to **Virtual Machines** node in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="a2adb-128">Navigate to **Virtual Machines** node in the Azure classic portal.</span></span> <span data-ttu-id="a2adb-129">Select the virtual machine you created in Task 1 and click **Connect** on the command bar at the bottom of the window.</span><span class="sxs-lookup"><span data-stu-id="a2adb-129">Select the virtual machine you created in Task 1 and click **Connect** on the command bar at the bottom of the window.</span></span>

    ![Connect to Windows virtual machine](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. <span data-ttu-id="a2adb-131">The classic portal prompts you to open or save a file with a '.rdp' extension, which is used to connect to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a2adb-131">The classic portal prompts you to open or save a file with a '.rdp' extension, which is used to connect to the virtual machine.</span></span> <span data-ttu-id="a2adb-132">Click the file when it has finished downloading.</span><span class="sxs-lookup"><span data-stu-id="a2adb-132">Click the file when it has finished downloading.</span></span>
3. <span data-ttu-id="a2adb-133">At the login prompt, use the credentials of a user belonging to the 'AAD DC Administrators' group.</span><span class="sxs-lookup"><span data-stu-id="a2adb-133">At the login prompt, use the credentials of a user belonging to the 'AAD DC Administrators' group.</span></span> <span data-ttu-id="a2adb-134">For example, we use 'bob@domainservicespreview.onmicrosoft.com' in our case.</span><span class="sxs-lookup"><span data-stu-id="a2adb-134">For example, we use 'bob@domainservicespreview.onmicrosoft.com' in our case.</span></span>
4. <span data-ttu-id="a2adb-135">From the Start screen, open **Server Manager**.</span><span class="sxs-lookup"><span data-stu-id="a2adb-135">From the Start screen, open **Server Manager**.</span></span> <span data-ttu-id="a2adb-136">Click **Add Roles and Features** in the central pane of the Server Manager window.</span><span class="sxs-lookup"><span data-stu-id="a2adb-136">Click **Add Roles and Features** in the central pane of the Server Manager window.</span></span>

    ![Launch Server Manager on virtual machine](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/install-rsat-server-manager.png)
5. <span data-ttu-id="a2adb-138">On the **Before You Begin** page of the **Add Roles and Features Wizard**, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a2adb-138">On the **Before You Begin** page of the **Add Roles and Features Wizard**, click **Next**.</span></span>

    ![Before You Begin page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-begin.png)
6. <span data-ttu-id="a2adb-140">On the **Installation Type** page, leave the **Role-based or feature-based installation** option checked and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a2adb-140">On the **Installation Type** page, leave the **Role-based or feature-based installation** option checked and click **Next**.</span></span>

    ![Installation Type page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-type.png)
7. <span data-ttu-id="a2adb-142">On the **Server Selection** page, select the current virtual machine from the server pool, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a2adb-142">On the **Server Selection** page, select the current virtual machine from the server pool, and click **Next**.</span></span>

    ![Server Selection page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-server.png)
8. <span data-ttu-id="a2adb-144">On the **Server Roles** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a2adb-144">On the **Server Roles** page, click **Next**.</span></span> <span data-ttu-id="a2adb-145">We skip this page since we are not installing any roles on the server.</span><span class="sxs-lookup"><span data-stu-id="a2adb-145">We skip this page since we are not installing any roles on the server.</span></span>
9. <span data-ttu-id="a2adb-146">On the **Features** page, click to expand the **Remote Server Administration Tools** node and then click to expand the **Role Administration Tools** node.</span><span class="sxs-lookup"><span data-stu-id="a2adb-146">On the **Features** page, click to expand the **Remote Server Administration Tools** node and then click to expand the **Role Administration Tools** node.</span></span> <span data-ttu-id="a2adb-147">Select **DNS Server Tools** feature from the list of role administration tools.</span><span class="sxs-lookup"><span data-stu-id="a2adb-147">Select **DNS Server Tools** feature from the list of role administration tools.</span></span>

    ![Features page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-dns-tools.png)
10. <span data-ttu-id="a2adb-149">On the **Confirmation** page, click **Install** to install the DNS Server tools feature on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a2adb-149">On the **Confirmation** page, click **Install** to install the DNS Server tools feature on the virtual machine.</span></span> <span data-ttu-id="a2adb-150">When feature installation completes successfully, click **Close** to exit the **Add Roles and Features** wizard.</span><span class="sxs-lookup"><span data-stu-id="a2adb-150">When feature installation completes successfully, click **Close** to exit the **Add Roles and Features** wizard.</span></span>

    ![Confirmation page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-dns-confirmation.png)

## <a name="task-3---launch-the-dns-management-console-to-administer-dns"></a><span data-ttu-id="a2adb-152">Task 3 - Launch the DNS management console to administer DNS</span><span class="sxs-lookup"><span data-stu-id="a2adb-152">Task 3 - Launch the DNS management console to administer DNS</span></span>
<span data-ttu-id="a2adb-153">Now that the DNS Server Tools feature is installed on the domain joined virtual machine, we can use the DNS tools to administer DNS on the managed domain.</span><span class="sxs-lookup"><span data-stu-id="a2adb-153">Now that the DNS Server Tools feature is installed on the domain joined virtual machine, we can use the DNS tools to administer DNS on the managed domain.</span></span>

> [!NOTE]
> <span data-ttu-id="a2adb-154">You need to be a member of the 'AAD DC Administrators' group, to administer DNS on the managed domain.</span><span class="sxs-lookup"><span data-stu-id="a2adb-154">You need to be a member of the 'AAD DC Administrators' group, to administer DNS on the managed domain.</span></span>
>
>

1. <span data-ttu-id="a2adb-155">From the Start screen, click **Administrative Tools**.</span><span class="sxs-lookup"><span data-stu-id="a2adb-155">From the Start screen, click **Administrative Tools**.</span></span> <span data-ttu-id="a2adb-156">You should see the **DNS** console installed on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a2adb-156">You should see the **DNS** console installed on the virtual machine.</span></span>

    ![Administrative tools - DNS Console](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/install-rsat-dns-tools-installed.png)
2. <span data-ttu-id="a2adb-158">Click **DNS** to launch the DNS Management console.</span><span class="sxs-lookup"><span data-stu-id="a2adb-158">Click **DNS** to launch the DNS Management console.</span></span>
3. <span data-ttu-id="a2adb-159">In the **Connect to DNS Server** dialog, click the option titled **The following computer**, and enter the DNS domain name of the managed domain (for example, 'contoso100.com').</span><span class="sxs-lookup"><span data-stu-id="a2adb-159">In the **Connect to DNS Server** dialog, click the option titled **The following computer**, and enter the DNS domain name of the managed domain (for example, 'contoso100.com').</span></span>

    ![DNS Console - connect to domain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/dns-console-connect-to-domain.png)
4. <span data-ttu-id="a2adb-161">The DNS Console connects to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="a2adb-161">The DNS Console connects to the managed domain.</span></span>

    ![DNS Console - administer domain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/dns-console-managed-domain.png)
5. <span data-ttu-id="a2adb-163">You can now use the DNS console to add DNS entries for computers within the virtual network in which you've enabled AAD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="a2adb-163">You can now use the DNS console to add DNS entries for computers within the virtual network in which you've enabled AAD Domain Services.</span></span>

> [!WARNING]
> <span data-ttu-id="a2adb-164">Be careful when administering DNS for the managed domain using DNS administration tools.</span><span class="sxs-lookup"><span data-stu-id="a2adb-164">Be careful when administering DNS for the managed domain using DNS administration tools.</span></span> <span data-ttu-id="a2adb-165">Ensure that you **do not delete or modify the built-in DNS records that are used by Domain Services in the domain**.</span><span class="sxs-lookup"><span data-stu-id="a2adb-165">Ensure that you **do not delete or modify the built-in DNS records that are used by Domain Services in the domain**.</span></span> <span data-ttu-id="a2adb-166">Built-in DNS records include domain DNS records, name server records, and other records used for DC location.</span><span class="sxs-lookup"><span data-stu-id="a2adb-166">Built-in DNS records include domain DNS records, name server records, and other records used for DC location.</span></span> <span data-ttu-id="a2adb-167">If you modify these records, domain services are disrupted on the virtual network.</span><span class="sxs-lookup"><span data-stu-id="a2adb-167">If you modify these records, domain services are disrupted on the virtual network.</span></span>
>
>

<span data-ttu-id="a2adb-168">See the [DNS tools article on Technet](https://technet.microsoft.com/library/cc753579.aspx) for more information about managing DNS.</span><span class="sxs-lookup"><span data-stu-id="a2adb-168">See the [DNS tools article on Technet](https://technet.microsoft.com/library/cc753579.aspx) for more information about managing DNS.</span></span>

## <a name="related-content"></a><span data-ttu-id="a2adb-169">Related Content</span><span class="sxs-lookup"><span data-stu-id="a2adb-169">Related Content</span></span>
* [<span data-ttu-id="a2adb-170">Azure AD Domain Services - Getting Started guide</span><span class="sxs-lookup"><span data-stu-id="a2adb-170">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="a2adb-171">Join a Windows Server virtual machine to an Azure AD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="a2adb-171">Join a Windows Server virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="a2adb-172">Administer an Azure AD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="a2adb-172">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="a2adb-173">DNS administration tools</span><span class="sxs-lookup"><span data-stu-id="a2adb-173">DNS administration tools</span></span>](https://technet.microsoft.com/library/cc753579.aspx)










