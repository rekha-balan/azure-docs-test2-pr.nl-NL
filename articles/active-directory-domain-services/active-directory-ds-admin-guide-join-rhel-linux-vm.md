---
title: 'Azure Active Directory Domain Services: Join a RHEL VM to a managed domain | Microsoft Docs'
description: Join a Red Hat Enterprise Linux virtual machine to Azure AD Domain Services
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 87291c47-1280-43f8-8fb2-da1bd61a4942
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: bec0dc312c2093793c141b7fd89646390056c506
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553744"
---
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-to-a-managed-domain"></a><span data-ttu-id="1179e-103">Join a Red Hat Enterprise Linux 7 virtual machine to a managed domain</span><span class="sxs-lookup"><span data-stu-id="1179e-103">Join a Red Hat Enterprise Linux 7 virtual machine to a managed domain</span></span>
<span data-ttu-id="1179e-104">This article shows you how to join a Red Hat Enterprise Linux (RHEL) 7 virtual machine to an Azure AD Domain Services managed domain.</span><span class="sxs-lookup"><span data-stu-id="1179e-104">This article shows you how to join a Red Hat Enterprise Linux (RHEL) 7 virtual machine to an Azure AD Domain Services managed domain.</span></span>

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a><span data-ttu-id="1179e-105">Provision a Red Hat Enterprise Linux virtual machine</span><span class="sxs-lookup"><span data-stu-id="1179e-105">Provision a Red Hat Enterprise Linux virtual machine</span></span>
<span data-ttu-id="1179e-106">Perform the following steps to provision a RHEL 7 virtual machine using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1179e-106">Perform the following steps to provision a RHEL 7 virtual machine using the Azure portal.</span></span>

1. <span data-ttu-id="1179e-107">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1179e-107">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

    ![Azure portal dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. <span data-ttu-id="1179e-109">Click **New** on the left pane and type **Red Hat** into the search bar as shown in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="1179e-109">Click **New** on the left pane and type **Red Hat** into the search bar as shown in the following screenshot.</span></span> <span data-ttu-id="1179e-110">Entries for Red Hat Enterprise Linux appear in the search results.</span><span class="sxs-lookup"><span data-stu-id="1179e-110">Entries for Red Hat Enterprise Linux appear in the search results.</span></span> <span data-ttu-id="1179e-111">Click **Red Hat Enterprise Linux 7.2**.</span><span class="sxs-lookup"><span data-stu-id="1179e-111">Click **Red Hat Enterprise Linux 7.2**.</span></span>

    ![Select RHEL in results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. <span data-ttu-id="1179e-113">The search results in the **Everything** pane should list the Red Hat Enterprise Linux 7.2 image.</span><span class="sxs-lookup"><span data-stu-id="1179e-113">The search results in the **Everything** pane should list the Red Hat Enterprise Linux 7.2 image.</span></span> <span data-ttu-id="1179e-114">Click **Red Hat Enterprise Linux 7.2** to view more information about the virtual machine image.</span><span class="sxs-lookup"><span data-stu-id="1179e-114">Click **Red Hat Enterprise Linux 7.2** to view more information about the virtual machine image.</span></span>

    ![Select RHEL in results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. <span data-ttu-id="1179e-116">In the **Red Hat Enterprise Linux 7.2** pane, you should see more information about the virtual machine image.</span><span class="sxs-lookup"><span data-stu-id="1179e-116">In the **Red Hat Enterprise Linux 7.2** pane, you should see more information about the virtual machine image.</span></span> <span data-ttu-id="1179e-117">In the **Select a deployment model** dropdown, select **Classic**.</span><span class="sxs-lookup"><span data-stu-id="1179e-117">In the **Select a deployment model** dropdown, select **Classic**.</span></span> <span data-ttu-id="1179e-118">Then click the **Create** button.</span><span class="sxs-lookup"><span data-stu-id="1179e-118">Then click the **Create** button.</span></span>

    ![View image details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. <span data-ttu-id="1179e-120">In the **Basics** page of the **Create virtual machine** wizard, enter the **Host Name** for the new virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1179e-120">In the **Basics** page of the **Create virtual machine** wizard, enter the **Host Name** for the new virtual machine.</span></span> <span data-ttu-id="1179e-121">Also specify a local administrator user name in the **User name** field and a **Password**.</span><span class="sxs-lookup"><span data-stu-id="1179e-121">Also specify a local administrator user name in the **User name** field and a **Password**.</span></span> <span data-ttu-id="1179e-122">You may also choose to use an SSH key to authenticate the local administrator user.</span><span class="sxs-lookup"><span data-stu-id="1179e-122">You may also choose to use an SSH key to authenticate the local administrator user.</span></span> <span data-ttu-id="1179e-123">Also select a **Pricing Tier** for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1179e-123">Also select a **Pricing Tier** for the virtual machine.</span></span>

    ![Create VM - basics page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. <span data-ttu-id="1179e-125">In the **Size** page of the **Create virtual machine** wizard, select the size for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1179e-125">In the **Size** page of the **Create virtual machine** wizard, select the size for the virtual machine.</span></span>

    ![Create VM - select size](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. <span data-ttu-id="1179e-127">In the **Settings** page of the **Create virtual machine** wizard, select the storage account for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1179e-127">In the **Settings** page of the **Create virtual machine** wizard, select the storage account for the virtual machine.</span></span> <span data-ttu-id="1179e-128">Click **Virtual Network** to select the virtual network to which the Linux VM should be deployed.</span><span class="sxs-lookup"><span data-stu-id="1179e-128">Click **Virtual Network** to select the virtual network to which the Linux VM should be deployed.</span></span> <span data-ttu-id="1179e-129">In the **Virtual Network** blade, select the virtual network in which Azure AD Domain Services is available.</span><span class="sxs-lookup"><span data-stu-id="1179e-129">In the **Virtual Network** blade, select the virtual network in which Azure AD Domain Services is available.</span></span> <span data-ttu-id="1179e-130">In this example, we pick the 'MyPreviewVNet' virtual network.</span><span class="sxs-lookup"><span data-stu-id="1179e-130">In this example, we pick the 'MyPreviewVNet' virtual network.</span></span>

    ![Create VM - select virtual network](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. <span data-ttu-id="1179e-132">On the **Summary** page of the **Create virtual machine** wizard, review and click the **OK** button.</span><span class="sxs-lookup"><span data-stu-id="1179e-132">On the **Summary** page of the **Create virtual machine** wizard, review and click the **OK** button.</span></span>

    ![Create VM - virtual network selected](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. <span data-ttu-id="1179e-134">Deployment of the new virtual machine based on the RHEL 7.2 image should start.</span><span class="sxs-lookup"><span data-stu-id="1179e-134">Deployment of the new virtual machine based on the RHEL 7.2 image should start.</span></span>

    ![Create VM - deployment started](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. <span data-ttu-id="1179e-136">After a few minutes, the virtual machine should be deployed successfully and ready for use.</span><span class="sxs-lookup"><span data-stu-id="1179e-136">After a few minutes, the virtual machine should be deployed successfully and ready for use.</span></span>

    ![Create VM - deployed](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-to-the-newly-provisioned-linux-virtual-machine"></a><span data-ttu-id="1179e-138">Connect remotely to the newly provisioned Linux virtual machine</span><span class="sxs-lookup"><span data-stu-id="1179e-138">Connect remotely to the newly provisioned Linux virtual machine</span></span>
<span data-ttu-id="1179e-139">The RHEL 7.2 virtual machine has been provisioned in Azure.</span><span class="sxs-lookup"><span data-stu-id="1179e-139">The RHEL 7.2 virtual machine has been provisioned in Azure.</span></span> <span data-ttu-id="1179e-140">The next task is to connect remotely to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1179e-140">The next task is to connect remotely to the virtual machine.</span></span>

<span data-ttu-id="1179e-141">**Connect to the RHEL 7.2 virtual machine** Follow the instructions in the article [How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1179e-141">**Connect to the RHEL 7.2 virtual machine** Follow the instructions in the article [How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="1179e-142">The rest of the steps assume you use the PuTTY SSH client to connect to the RHEL virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1179e-142">The rest of the steps assume you use the PuTTY SSH client to connect to the RHEL virtual machine.</span></span> <span data-ttu-id="1179e-143">For more information, see the [PuTTY Download page](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="1179e-143">For more information, see the [PuTTY Download page](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

1. <span data-ttu-id="1179e-144">Open the PuTTY program.</span><span class="sxs-lookup"><span data-stu-id="1179e-144">Open the PuTTY program.</span></span>
2. <span data-ttu-id="1179e-145">Enter the **Host Name** for the newly created RHEL virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1179e-145">Enter the **Host Name** for the newly created RHEL virtual machine.</span></span> <span data-ttu-id="1179e-146">In this example, our virtual machine has the host name 'contoso-rhel.cloudapp.net'.</span><span class="sxs-lookup"><span data-stu-id="1179e-146">In this example, our virtual machine has the host name 'contoso-rhel.cloudapp.net'.</span></span> <span data-ttu-id="1179e-147">If you are not sure of the host name of your VM, refer to the VM dashboard on the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1179e-147">If you are not sure of the host name of your VM, refer to the VM dashboard on the Azure portal.</span></span>

    ![PuTTY connect](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. <span data-ttu-id="1179e-149">Log on to the virtual machine using the local administrator credentials you specified when the virtual machine was created.</span><span class="sxs-lookup"><span data-stu-id="1179e-149">Log on to the virtual machine using the local administrator credentials you specified when the virtual machine was created.</span></span> <span data-ttu-id="1179e-150">In this example, we used the local administrator account "mahesh".</span><span class="sxs-lookup"><span data-stu-id="1179e-150">In this example, we used the local administrator account "mahesh".</span></span>

    ![PuTTY login](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-the-linux-virtual-machine"></a><span data-ttu-id="1179e-152">Install required packages on the Linux virtual machine</span><span class="sxs-lookup"><span data-stu-id="1179e-152">Install required packages on the Linux virtual machine</span></span>
<span data-ttu-id="1179e-153">After connecting to the virtual machine, the next task is to install packages required for domain join on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1179e-153">After connecting to the virtual machine, the next task is to install packages required for domain join on the virtual machine.</span></span> <span data-ttu-id="1179e-154">Perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1179e-154">Perform the following steps:</span></span>

1. <span data-ttu-id="1179e-155">**Install realmd:** The realmd package is used for domain join.</span><span class="sxs-lookup"><span data-stu-id="1179e-155">**Install realmd:** The realmd package is used for domain join.</span></span> <span data-ttu-id="1179e-156">In your PuTTY terminal, type the following command:</span><span class="sxs-lookup"><span data-stu-id="1179e-156">In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="1179e-157">sudo yum install realmd</span><span class="sxs-lookup"><span data-stu-id="1179e-157">sudo yum install realmd</span></span>

    ![Install realmd](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    <span data-ttu-id="1179e-159">After a few minutes, the realmd package should get installed on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1179e-159">After a few minutes, the realmd package should get installed on the virtual machine.</span></span>

    ![realmd installed](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. <span data-ttu-id="1179e-161">**Install sssd:** The realmd package depends on sssd to perform domain join operations.</span><span class="sxs-lookup"><span data-stu-id="1179e-161">**Install sssd:** The realmd package depends on sssd to perform domain join operations.</span></span> <span data-ttu-id="1179e-162">In your PuTTY terminal, type the following command:</span><span class="sxs-lookup"><span data-stu-id="1179e-162">In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="1179e-163">sudo yum install sssd</span><span class="sxs-lookup"><span data-stu-id="1179e-163">sudo yum install sssd</span></span>

    ![Install sssd](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    <span data-ttu-id="1179e-165">After a few minutes, the sssd package should get installed on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1179e-165">After a few minutes, the sssd package should get installed on the virtual machine.</span></span>

    ![realmd installed](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. <span data-ttu-id="1179e-167">**Install kerberos:** In your PuTTY terminal, type the following command:</span><span class="sxs-lookup"><span data-stu-id="1179e-167">**Install kerberos:** In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="1179e-168">sudo yum install krb5-workstation krb5-libs</span><span class="sxs-lookup"><span data-stu-id="1179e-168">sudo yum install krb5-workstation krb5-libs</span></span>

    ![Install kerberos](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    <span data-ttu-id="1179e-170">After a few minutes, the realmd package should get installed on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1179e-170">After a few minutes, the realmd package should get installed on the virtual machine.</span></span>

    ![Kerberos installed](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-the-linux-virtual-machine-to-the-managed-domain"></a><span data-ttu-id="1179e-172">Join the Linux virtual machine to the managed domain</span><span class="sxs-lookup"><span data-stu-id="1179e-172">Join the Linux virtual machine to the managed domain</span></span>
<span data-ttu-id="1179e-173">Now that the required packages are installed on the Linux virtual machine, the next task is to join the virtual machine to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="1179e-173">Now that the required packages are installed on the Linux virtual machine, the next task is to join the virtual machine to the managed domain.</span></span>

1. <span data-ttu-id="1179e-174">Discover the AAD Domain Services managed domain.</span><span class="sxs-lookup"><span data-stu-id="1179e-174">Discover the AAD Domain Services managed domain.</span></span> <span data-ttu-id="1179e-175">In your PuTTY terminal, type the following command:</span><span class="sxs-lookup"><span data-stu-id="1179e-175">In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="1179e-176">sudo realm discover CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="1179e-176">sudo realm discover CONTOSO100.COM</span></span>

    ![Realm discover](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    <span data-ttu-id="1179e-178">If **realm discover** is unable to find your managed domain, ensure that the domain is reachable from the virtual machine (try ping).</span><span class="sxs-lookup"><span data-stu-id="1179e-178">If **realm discover** is unable to find your managed domain, ensure that the domain is reachable from the virtual machine (try ping).</span></span> <span data-ttu-id="1179e-179">Also ensure that the virtual machine has indeed been deployed to the same virtual network in which the managed domain is available.</span><span class="sxs-lookup"><span data-stu-id="1179e-179">Also ensure that the virtual machine has indeed been deployed to the same virtual network in which the managed domain is available.</span></span>
2. <span data-ttu-id="1179e-180">Initialize kerberos.</span><span class="sxs-lookup"><span data-stu-id="1179e-180">Initialize kerberos.</span></span> <span data-ttu-id="1179e-181">In your PuTTY terminal, type the following command.</span><span class="sxs-lookup"><span data-stu-id="1179e-181">In your PuTTY terminal, type the following command.</span></span> <span data-ttu-id="1179e-182">Ensure that you specify a user who belongs to the 'AAD DC Administrators' group.</span><span class="sxs-lookup"><span data-stu-id="1179e-182">Ensure that you specify a user who belongs to the 'AAD DC Administrators' group.</span></span> <span data-ttu-id="1179e-183">Only these users can join computers to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="1179e-183">Only these users can join computers to the managed domain.</span></span>

    <span data-ttu-id="1179e-184">kinit bob@CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="1179e-184">kinit bob@CONTOSO100.COM</span></span>

    ![Kinit](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    <span data-ttu-id="1179e-186">Ensure that you specify the domain name in capital letters, else kinit fails.</span><span class="sxs-lookup"><span data-stu-id="1179e-186">Ensure that you specify the domain name in capital letters, else kinit fails.</span></span>
3. <span data-ttu-id="1179e-187">Join the machine to the domain.</span><span class="sxs-lookup"><span data-stu-id="1179e-187">Join the machine to the domain.</span></span> <span data-ttu-id="1179e-188">In your PuTTY terminal, type the following command.</span><span class="sxs-lookup"><span data-stu-id="1179e-188">In your PuTTY terminal, type the following command.</span></span> <span data-ttu-id="1179e-189">Specify the same user you specified in the preceding step ('kinit').</span><span class="sxs-lookup"><span data-stu-id="1179e-189">Specify the same user you specified in the preceding step ('kinit').</span></span>

    <span data-ttu-id="1179e-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span><span class="sxs-lookup"><span data-stu-id="1179e-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span></span>

    ![Realm join](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

<span data-ttu-id="1179e-192">You should get a message ("Successfully enrolled machine in realm") when the machine is successfully joined to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="1179e-192">You should get a message ("Successfully enrolled machine in realm") when the machine is successfully joined to the managed domain.</span></span>

## <a name="verify-domain-join"></a><span data-ttu-id="1179e-193">Verify domain join</span><span class="sxs-lookup"><span data-stu-id="1179e-193">Verify domain join</span></span>
<span data-ttu-id="1179e-194">You can quickly verify whether the machine has been successfully joined to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="1179e-194">You can quickly verify whether the machine has been successfully joined to the managed domain.</span></span> <span data-ttu-id="1179e-195">Connect to the newly domain joined RHEL VM using SSH and a domain user account and then check to see if the user account is resolved correctly.</span><span class="sxs-lookup"><span data-stu-id="1179e-195">Connect to the newly domain joined RHEL VM using SSH and a domain user account and then check to see if the user account is resolved correctly.</span></span>

1. <span data-ttu-id="1179e-196">In your PuTTY terminal, type the following command to connect to the newly domain joined RHEL virtual machine using SSH.</span><span class="sxs-lookup"><span data-stu-id="1179e-196">In your PuTTY terminal, type the following command to connect to the newly domain joined RHEL virtual machine using SSH.</span></span> <span data-ttu-id="1179e-197">Use a domain account that belongs to the managed domain (for example, 'bob@CONTOSO100.COM' in this case.)</span><span class="sxs-lookup"><span data-stu-id="1179e-197">Use a domain account that belongs to the managed domain (for example, 'bob@CONTOSO100.COM' in this case.)</span></span>

    <span data-ttu-id="1179e-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="1179e-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span></span>
2. <span data-ttu-id="1179e-199">In your PuTTY terminal, type the following command to see if the home directory was initialized correctly.</span><span class="sxs-lookup"><span data-stu-id="1179e-199">In your PuTTY terminal, type the following command to see if the home directory was initialized correctly.</span></span>

    <span data-ttu-id="1179e-200">pwd</span><span class="sxs-lookup"><span data-stu-id="1179e-200">pwd</span></span>
3. <span data-ttu-id="1179e-201">In your PuTTY terminal, type the following command to see if the group memberships are being resolved correctly.</span><span class="sxs-lookup"><span data-stu-id="1179e-201">In your PuTTY terminal, type the following command to see if the group memberships are being resolved correctly.</span></span>

    <span data-ttu-id="1179e-202">id</span><span class="sxs-lookup"><span data-stu-id="1179e-202">id</span></span>

<span data-ttu-id="1179e-203">A sample output of these commands follows:</span><span class="sxs-lookup"><span data-stu-id="1179e-203">A sample output of these commands follows:</span></span>

![Verify domain join](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a><span data-ttu-id="1179e-205">Troubleshooting domain join</span><span class="sxs-lookup"><span data-stu-id="1179e-205">Troubleshooting domain join</span></span>
<span data-ttu-id="1179e-206">Refer to the [Troubleshooting domain join](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) article.</span><span class="sxs-lookup"><span data-stu-id="1179e-206">Refer to the [Troubleshooting domain join](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) article.</span></span>

## <a name="related-content"></a><span data-ttu-id="1179e-207">Related Content</span><span class="sxs-lookup"><span data-stu-id="1179e-207">Related Content</span></span>
* [<span data-ttu-id="1179e-208">Azure AD Domain Services - Getting Started guide</span><span class="sxs-lookup"><span data-stu-id="1179e-208">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="1179e-209">Join a Windows Server virtual machine to an Azure AD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="1179e-209">Join a Windows Server virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* <span data-ttu-id="1179e-210">[How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1179e-210">[How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* [<span data-ttu-id="1179e-211">Installing Kerberos</span><span class="sxs-lookup"><span data-stu-id="1179e-211">Installing Kerberos</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [<span data-ttu-id="1179e-212">Red Hat Enterprise Linux 7 - Windows Integration Guide</span><span class="sxs-lookup"><span data-stu-id="1179e-212">Red Hat Enterprise Linux 7 - Windows Integration Guide</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)






















