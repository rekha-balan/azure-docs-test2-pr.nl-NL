---
title: 'Azure Active Directory Domain Services: Join a CentOS VM to a managed domain | Microsoft Docs'
description: Join a CentOS Linux virtual machine to Azure AD Domain Services
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: mtillman
editor: curtand
ms.assetid: 16100caa-f209-4cb0-86d3-9e218aeb51c6
ms.service: active-directory
ms.component: domain-services
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 06/22/2018
ms.author: maheshu
ms.openlocfilehash: 581e2b361cf7133df369e7c8c3062c19fbe77d5c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870510"
---
# <a name="join-a-centos-linux-virtual-machine-to-a-managed-domain"></a><span data-ttu-id="453d7-103">Join a CentOS Linux virtual machine to a managed domain</span><span class="sxs-lookup"><span data-stu-id="453d7-103">Join a CentOS Linux virtual machine to a managed domain</span></span>
<span data-ttu-id="453d7-104">This article shows you how to join a CentOS Linux virtual machine in Azure to an Azure AD Domain Services managed domain.</span><span class="sxs-lookup"><span data-stu-id="453d7-104">This article shows you how to join a CentOS Linux virtual machine in Azure to an Azure AD Domain Services managed domain.</span></span>

[!INCLUDE [active-directory-ds-prerequisites.md](../../includes/active-directory-ds-prerequisites.md)]

## <a name="before-you-begin"></a><span data-ttu-id="453d7-105">Before you begin</span><span class="sxs-lookup"><span data-stu-id="453d7-105">Before you begin</span></span>
<span data-ttu-id="453d7-106">To perform the tasks listed in this article, you need:</span><span class="sxs-lookup"><span data-stu-id="453d7-106">To perform the tasks listed in this article, you need:</span></span>
1. <span data-ttu-id="453d7-107">A valid **Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="453d7-107">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="453d7-108">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span><span class="sxs-lookup"><span data-stu-id="453d7-108">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="453d7-109">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="453d7-109">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span></span> <span data-ttu-id="453d7-110">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="453d7-110">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="453d7-111">Ensure that you have configured the IP addresses of the managed domain as the DNS servers for the virtual network.</span><span class="sxs-lookup"><span data-stu-id="453d7-111">Ensure that you have configured the IP addresses of the managed domain as the DNS servers for the virtual network.</span></span> <span data-ttu-id="453d7-112">For more information, see [how to update DNS settings for the Azure virtual network](active-directory-ds-getting-started-dns.md)</span><span class="sxs-lookup"><span data-stu-id="453d7-112">For more information, see [how to update DNS settings for the Azure virtual network](active-directory-ds-getting-started-dns.md)</span></span>
5. <span data-ttu-id="453d7-113">Complete the steps required to [synchronize passwords to your Azure AD Domain Services managed domain](active-directory-ds-getting-started-password-sync.md).</span><span class="sxs-lookup"><span data-stu-id="453d7-113">Complete the steps required to [synchronize passwords to your Azure AD Domain Services managed domain](active-directory-ds-getting-started-password-sync.md).</span></span>


## <a name="provision-a-centos-linux-virtual-machine"></a><span data-ttu-id="453d7-114">Provision a CentOS Linux virtual machine</span><span class="sxs-lookup"><span data-stu-id="453d7-114">Provision a CentOS Linux virtual machine</span></span>
<span data-ttu-id="453d7-115">Provision a CentOS virtual machine in Azure, using any of the following methods:</span><span class="sxs-lookup"><span data-stu-id="453d7-115">Provision a CentOS virtual machine in Azure, using any of the following methods:</span></span>
* [<span data-ttu-id="453d7-116">Azure portal</span><span class="sxs-lookup"><span data-stu-id="453d7-116">Azure portal</span></span>](../virtual-machines/linux/quick-create-portal.md)
* [<span data-ttu-id="453d7-117">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="453d7-117">Azure CLI</span></span>](../virtual-machines/linux/quick-create-cli.md)
* [<span data-ttu-id="453d7-118">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="453d7-118">Azure PowerShell</span></span>](../virtual-machines/linux/quick-create-powershell.md)

> [!IMPORTANT]
> * <span data-ttu-id="453d7-119">Deploy the virtual machine into the **same virtual network in which you have enabled Azure AD Domain Services**.</span><span class="sxs-lookup"><span data-stu-id="453d7-119">Deploy the virtual machine into the **same virtual network in which you have enabled Azure AD Domain Services**.</span></span>
> * <span data-ttu-id="453d7-120">Pick a **different subnet** than the one in which you have enabled Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="453d7-120">Pick a **different subnet** than the one in which you have enabled Azure AD Domain Services.</span></span>
>


## <a name="connect-remotely-to-the-newly-provisioned-linux-virtual-machine"></a><span data-ttu-id="453d7-121">Connect remotely to the newly provisioned Linux virtual machine</span><span class="sxs-lookup"><span data-stu-id="453d7-121">Connect remotely to the newly provisioned Linux virtual machine</span></span>
<span data-ttu-id="453d7-122">The CentOS virtual machine has been provisioned in Azure.</span><span class="sxs-lookup"><span data-stu-id="453d7-122">The CentOS virtual machine has been provisioned in Azure.</span></span> <span data-ttu-id="453d7-123">The next task is to connect remotely to the virtual machine using the local administrator account created while provisioning the VM.</span><span class="sxs-lookup"><span data-stu-id="453d7-123">The next task is to connect remotely to the virtual machine using the local administrator account created while provisioning the VM.</span></span>

<span data-ttu-id="453d7-124">Follow the instructions in the article [How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="453d7-124">Follow the instructions in the article [How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="configure-the-hosts-file-on-the-linux-virtual-machine"></a><span data-ttu-id="453d7-125">Configure the hosts file on the Linux virtual machine</span><span class="sxs-lookup"><span data-stu-id="453d7-125">Configure the hosts file on the Linux virtual machine</span></span>
<span data-ttu-id="453d7-126">In your SSH terminal, edit the /etc/hosts file and update your machine’s IP address and hostname.</span><span class="sxs-lookup"><span data-stu-id="453d7-126">In your SSH terminal, edit the /etc/hosts file and update your machine’s IP address and hostname.</span></span>

```
sudo vi /etc/hosts
```

<span data-ttu-id="453d7-127">In the hosts file, enter the following value:</span><span class="sxs-lookup"><span data-stu-id="453d7-127">In the hosts file, enter the following value:</span></span>

```
127.0.0.1 contoso-centos.contoso100.com contoso-centos
```
<span data-ttu-id="453d7-128">Here, 'contoso100.com' is the DNS domain name of your managed domain.</span><span class="sxs-lookup"><span data-stu-id="453d7-128">Here, 'contoso100.com' is the DNS domain name of your managed domain.</span></span> <span data-ttu-id="453d7-129">'contoso-centos' is the hostname of the CentOS virtual machine you are joining to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="453d7-129">'contoso-centos' is the hostname of the CentOS virtual machine you are joining to the managed domain.</span></span>


## <a name="install-required-packages-on-the-linux-virtual-machine"></a><span data-ttu-id="453d7-130">Install required packages on the Linux virtual machine</span><span class="sxs-lookup"><span data-stu-id="453d7-130">Install required packages on the Linux virtual machine</span></span>
<span data-ttu-id="453d7-131">Next, install packages required for domain join on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="453d7-131">Next, install packages required for domain join on the virtual machine.</span></span> <span data-ttu-id="453d7-132">In your SSH terminal, type the following command to install the required packages:</span><span class="sxs-lookup"><span data-stu-id="453d7-132">In your SSH terminal, type the following command to install the required packages:</span></span>

    ```
    sudo yum install realmd sssd krb5-workstation krb5-libs oddjob oddjob-mkhomedir samba-common-tools
    ```


## <a name="join-the-linux-virtual-machine-to-the-managed-domain"></a><span data-ttu-id="453d7-133">Join the Linux virtual machine to the managed domain</span><span class="sxs-lookup"><span data-stu-id="453d7-133">Join the Linux virtual machine to the managed domain</span></span>
<span data-ttu-id="453d7-134">Now that the required packages are installed on the Linux virtual machine, the next task is to join the virtual machine to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="453d7-134">Now that the required packages are installed on the Linux virtual machine, the next task is to join the virtual machine to the managed domain.</span></span>

1. <span data-ttu-id="453d7-135">Discover the AAD Domain Services managed domain.</span><span class="sxs-lookup"><span data-stu-id="453d7-135">Discover the AAD Domain Services managed domain.</span></span> <span data-ttu-id="453d7-136">In your SSH terminal, type the following command:</span><span class="sxs-lookup"><span data-stu-id="453d7-136">In your SSH terminal, type the following command:</span></span>

    ```
    sudo realm discover CONTOSO100.COM
    ```

    > [!NOTE]
    > <span data-ttu-id="453d7-137">**Troubleshooting:** If *realm discover* is unable to find your managed domain:</span><span class="sxs-lookup"><span data-stu-id="453d7-137">**Troubleshooting:** If *realm discover* is unable to find your managed domain:</span></span>  
      * <span data-ttu-id="453d7-138">Ensure that the domain is reachable from the virtual machine (try ping).</span><span class="sxs-lookup"><span data-stu-id="453d7-138">Ensure that the domain is reachable from the virtual machine (try ping).</span></span>  
      * <span data-ttu-id="453d7-139">Check that the virtual machine has indeed been deployed to the same virtual network in which the managed domain is available.</span><span class="sxs-lookup"><span data-stu-id="453d7-139">Check that the virtual machine has indeed been deployed to the same virtual network in which the managed domain is available.</span></span>
      * <span data-ttu-id="453d7-140">Check to see if you have updated the DNS server settings for the virtual network to point to the domain controllers of the managed domain.</span><span class="sxs-lookup"><span data-stu-id="453d7-140">Check to see if you have updated the DNS server settings for the virtual network to point to the domain controllers of the managed domain.</span></span>  
      >

2. <span data-ttu-id="453d7-141">Initialize Kerberos.</span><span class="sxs-lookup"><span data-stu-id="453d7-141">Initialize Kerberos.</span></span> <span data-ttu-id="453d7-142">In your SSH terminal, type the following command:</span><span class="sxs-lookup"><span data-stu-id="453d7-142">In your SSH terminal, type the following command:</span></span>

    > [!TIP]
    > * <span data-ttu-id="453d7-143">Specify a user who belongs to the 'AAD DC Administrators' group.</span><span class="sxs-lookup"><span data-stu-id="453d7-143">Specify a user who belongs to the 'AAD DC Administrators' group.</span></span>
    > * <span data-ttu-id="453d7-144">Specify the domain name in capital letters, else kinit fails.</span><span class="sxs-lookup"><span data-stu-id="453d7-144">Specify the domain name in capital letters, else kinit fails.</span></span>
    >

    ```
    kinit bob@CONTOSO100.COM
    ```

3. <span data-ttu-id="453d7-145">Join the machine to the domain.</span><span class="sxs-lookup"><span data-stu-id="453d7-145">Join the machine to the domain.</span></span> <span data-ttu-id="453d7-146">In your SSH terminal, type the following command:</span><span class="sxs-lookup"><span data-stu-id="453d7-146">In your SSH terminal, type the following command:</span></span>

    > [!TIP]
    > <span data-ttu-id="453d7-147">Use the same user account you specified in the preceding step ('kinit').</span><span class="sxs-lookup"><span data-stu-id="453d7-147">Use the same user account you specified in the preceding step ('kinit').</span></span>
    >

    ```
    sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'
    ```

<span data-ttu-id="453d7-148">You should get a message ("Successfully enrolled machine in realm") when the machine is successfully joined to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="453d7-148">You should get a message ("Successfully enrolled machine in realm") when the machine is successfully joined to the managed domain.</span></span>


## <a name="verify-domain-join"></a><span data-ttu-id="453d7-149">Verify domain join</span><span class="sxs-lookup"><span data-stu-id="453d7-149">Verify domain join</span></span>
<span data-ttu-id="453d7-150">Verify whether the machine has been successfully joined to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="453d7-150">Verify whether the machine has been successfully joined to the managed domain.</span></span> <span data-ttu-id="453d7-151">Connect to the domain joined CentOS VM using a different SSH connection.</span><span class="sxs-lookup"><span data-stu-id="453d7-151">Connect to the domain joined CentOS VM using a different SSH connection.</span></span> <span data-ttu-id="453d7-152">Use a domain user account and then check to see if the user account is resolved correctly.</span><span class="sxs-lookup"><span data-stu-id="453d7-152">Use a domain user account and then check to see if the user account is resolved correctly.</span></span>

1. <span data-ttu-id="453d7-153">In your SSH terminal, type the following command to connect to the domain joined CentOS virtual machine using SSH.</span><span class="sxs-lookup"><span data-stu-id="453d7-153">In your SSH terminal, type the following command to connect to the domain joined CentOS virtual machine using SSH.</span></span> <span data-ttu-id="453d7-154">Use a domain account that belongs to the managed domain (for example, 'bob@CONTOSO100.COM' in this case.)</span><span class="sxs-lookup"><span data-stu-id="453d7-154">Use a domain account that belongs to the managed domain (for example, 'bob@CONTOSO100.COM' in this case.)</span></span>
    ```
    ssh -l bob@CONTOSO100.COM contoso-centos.contoso100.com
    ```

2. <span data-ttu-id="453d7-155">In your SSH terminal, type the following command to see if the home directory was initialized correctly.</span><span class="sxs-lookup"><span data-stu-id="453d7-155">In your SSH terminal, type the following command to see if the home directory was initialized correctly.</span></span>
    ```
    pwd
    ```

3. <span data-ttu-id="453d7-156">In your SSH terminal, type the following command to see if the group memberships are being resolved correctly.</span><span class="sxs-lookup"><span data-stu-id="453d7-156">In your SSH terminal, type the following command to see if the group memberships are being resolved correctly.</span></span>
    ```
    id
    ```


## <a name="troubleshooting-domain-join"></a><span data-ttu-id="453d7-157">Troubleshooting domain join</span><span class="sxs-lookup"><span data-stu-id="453d7-157">Troubleshooting domain join</span></span>
<span data-ttu-id="453d7-158">Refer to the [Troubleshooting domain join](active-directory-ds-admin-guide-join-windows-vm-portal.md#troubleshoot-joining-a-domain) article.</span><span class="sxs-lookup"><span data-stu-id="453d7-158">Refer to the [Troubleshooting domain join](active-directory-ds-admin-guide-join-windows-vm-portal.md#troubleshoot-joining-a-domain) article.</span></span>

## <a name="related-content"></a><span data-ttu-id="453d7-159">Related Content</span><span class="sxs-lookup"><span data-stu-id="453d7-159">Related Content</span></span>
* [<span data-ttu-id="453d7-160">Azure AD Domain Services - Getting Started guide</span><span class="sxs-lookup"><span data-stu-id="453d7-160">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="453d7-161">Join a Windows Server virtual machine to an Azure AD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="453d7-161">Join a Windows Server virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* <span data-ttu-id="453d7-162">[How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="453d7-162">[How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* [<span data-ttu-id="453d7-163">Installing Kerberos</span><span class="sxs-lookup"><span data-stu-id="453d7-163">Installing Kerberos</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [<span data-ttu-id="453d7-164">Red Hat Enterprise Linux 7 - Windows Integration Guide</span><span class="sxs-lookup"><span data-stu-id="453d7-164">Red Hat Enterprise Linux 7 - Windows Integration Guide</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)
