---
title: 'Azure Active Directory Domain Services: Join a CoreOS Linux VM to a managed domain | Microsoft Docs'
description: Join a CoreOS Linux virtual machine to Azure AD Domain Services
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: mtillman
editor: curtand
ms.assetid: 5db65f30-bf69-4ea3-9ea5-add1db83fdb8
ms.service: active-directory
ms.component: domain-services
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 06/22/2018
ms.author: maheshu
ms.openlocfilehash: 1574a6a4cf727198b17f5c62488d12be12d928f4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866170"
---
# <a name="join-a-coreos-linux-virtual-machine-to-a-managed-domain"></a><span data-ttu-id="d0d72-103">Join a CoreOS Linux virtual machine to a managed domain</span><span class="sxs-lookup"><span data-stu-id="d0d72-103">Join a CoreOS Linux virtual machine to a managed domain</span></span>
<span data-ttu-id="d0d72-104">This article shows you how to join a CoreOS Linux virtual machine in Azure to an Azure AD Domain Services managed domain.</span><span class="sxs-lookup"><span data-stu-id="d0d72-104">This article shows you how to join a CoreOS Linux virtual machine in Azure to an Azure AD Domain Services managed domain.</span></span>

[!INCLUDE [active-directory-ds-prerequisites.md](../../includes/active-directory-ds-prerequisites.md)]

## <a name="before-you-begin"></a><span data-ttu-id="d0d72-105">Before you begin</span><span class="sxs-lookup"><span data-stu-id="d0d72-105">Before you begin</span></span>
<span data-ttu-id="d0d72-106">To perform the tasks listed in this article, you need:</span><span class="sxs-lookup"><span data-stu-id="d0d72-106">To perform the tasks listed in this article, you need:</span></span>
1. <span data-ttu-id="d0d72-107">A valid **Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="d0d72-107">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="d0d72-108">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span><span class="sxs-lookup"><span data-stu-id="d0d72-108">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="d0d72-109">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="d0d72-109">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span></span> <span data-ttu-id="d0d72-110">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="d0d72-110">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="d0d72-111">Ensure that you have configured the IP addresses of the managed domain as the DNS servers for the virtual network.</span><span class="sxs-lookup"><span data-stu-id="d0d72-111">Ensure that you have configured the IP addresses of the managed domain as the DNS servers for the virtual network.</span></span> <span data-ttu-id="d0d72-112">For more information, see [how to update DNS settings for the Azure virtual network](active-directory-ds-getting-started-dns.md)</span><span class="sxs-lookup"><span data-stu-id="d0d72-112">For more information, see [how to update DNS settings for the Azure virtual network](active-directory-ds-getting-started-dns.md)</span></span>
5. <span data-ttu-id="d0d72-113">Complete the steps required to [synchronize passwords to your Azure AD Domain Services managed domain](active-directory-ds-getting-started-password-sync.md).</span><span class="sxs-lookup"><span data-stu-id="d0d72-113">Complete the steps required to [synchronize passwords to your Azure AD Domain Services managed domain](active-directory-ds-getting-started-password-sync.md).</span></span>


## <a name="provision-a-coreos-linux-virtual-machine"></a><span data-ttu-id="d0d72-114">Provision a CoreOS Linux virtual machine</span><span class="sxs-lookup"><span data-stu-id="d0d72-114">Provision a CoreOS Linux virtual machine</span></span>
<span data-ttu-id="d0d72-115">Provision a CoreOS virtual machine in Azure, using any of the following methods:</span><span class="sxs-lookup"><span data-stu-id="d0d72-115">Provision a CoreOS virtual machine in Azure, using any of the following methods:</span></span>
* [<span data-ttu-id="d0d72-116">Azure portal</span><span class="sxs-lookup"><span data-stu-id="d0d72-116">Azure portal</span></span>](../virtual-machines/linux/quick-create-portal.md)
* [<span data-ttu-id="d0d72-117">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d0d72-117">Azure CLI</span></span>](../virtual-machines/linux/quick-create-cli.md)
* [<span data-ttu-id="d0d72-118">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d0d72-118">Azure PowerShell</span></span>](../virtual-machines/linux/quick-create-powershell.md)

<span data-ttu-id="d0d72-119">This article uses the **CoreOS Linux (Stable)** virtual machine image in Azure.</span><span class="sxs-lookup"><span data-stu-id="d0d72-119">This article uses the **CoreOS Linux (Stable)** virtual machine image in Azure.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="d0d72-120">Deploy the virtual machine into the **same virtual network in which you have enabled Azure AD Domain Services**.</span><span class="sxs-lookup"><span data-stu-id="d0d72-120">Deploy the virtual machine into the **same virtual network in which you have enabled Azure AD Domain Services**.</span></span>
> * <span data-ttu-id="d0d72-121">Pick a **different subnet** than the one in which you have enabled Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="d0d72-121">Pick a **different subnet** than the one in which you have enabled Azure AD Domain Services.</span></span>
>


## <a name="connect-remotely-to-the-newly-provisioned-linux-virtual-machine"></a><span data-ttu-id="d0d72-122">Connect remotely to the newly provisioned Linux virtual machine</span><span class="sxs-lookup"><span data-stu-id="d0d72-122">Connect remotely to the newly provisioned Linux virtual machine</span></span>
<span data-ttu-id="d0d72-123">The CoreOS virtual machine has been provisioned in Azure.</span><span class="sxs-lookup"><span data-stu-id="d0d72-123">The CoreOS virtual machine has been provisioned in Azure.</span></span> <span data-ttu-id="d0d72-124">The next task is to connect remotely to the virtual machine using the local administrator account created while provisioning the VM.</span><span class="sxs-lookup"><span data-stu-id="d0d72-124">The next task is to connect remotely to the virtual machine using the local administrator account created while provisioning the VM.</span></span>

<span data-ttu-id="d0d72-125">Follow the instructions in the article [How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d0d72-125">Follow the instructions in the article [How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="configure-the-hosts-file-on-the-linux-virtual-machine"></a><span data-ttu-id="d0d72-126">Configure the hosts file on the Linux virtual machine</span><span class="sxs-lookup"><span data-stu-id="d0d72-126">Configure the hosts file on the Linux virtual machine</span></span>
<span data-ttu-id="d0d72-127">In your SSH terminal, edit the /etc/hosts file and update your machine’s IP address and hostname.</span><span class="sxs-lookup"><span data-stu-id="d0d72-127">In your SSH terminal, edit the /etc/hosts file and update your machine’s IP address and hostname.</span></span>

```
sudo vi /etc/hosts
```

<span data-ttu-id="d0d72-128">In the hosts file, enter the following value:</span><span class="sxs-lookup"><span data-stu-id="d0d72-128">In the hosts file, enter the following value:</span></span>

```
127.0.0.1 contoso-coreos.contoso100.com contoso-coreos
```
<span data-ttu-id="d0d72-129">Here, 'contoso100.com' is the DNS domain name of your managed domain.</span><span class="sxs-lookup"><span data-stu-id="d0d72-129">Here, 'contoso100.com' is the DNS domain name of your managed domain.</span></span> <span data-ttu-id="d0d72-130">'contoso-coreos' is the hostname of the CoreOS virtual machine you are joining to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="d0d72-130">'contoso-coreos' is the hostname of the CoreOS virtual machine you are joining to the managed domain.</span></span>


## <a name="configure-the-sssd-service-on-the-linux-virtual-machine"></a><span data-ttu-id="d0d72-131">Configure the SSSD service on the Linux virtual machine</span><span class="sxs-lookup"><span data-stu-id="d0d72-131">Configure the SSSD service on the Linux virtual machine</span></span>
<span data-ttu-id="d0d72-132">Next, update your SSSD configuration file in ('/etc/sssd/sssd.conf') to match the following sample:</span><span class="sxs-lookup"><span data-stu-id="d0d72-132">Next, update your SSSD configuration file in ('/etc/sssd/sssd.conf') to match the following sample:</span></span>

 ```
 [sssd]
 config_file_version = 2
 services = nss, pam
 domains = CONTOSO100.COM

 [domain/CONTOSO100.COM]
 id_provider = ad
 auth_provider = ad
 chpass_provider = ad

 ldap_uri = ldap://contoso100.com
 ldap_search_base = dc=contoso100,dc=com
 ldap_schema = rfc2307bis
 ldap_sasl_mech = GSSAPI
 ldap_user_object_class = user
 ldap_group_object_class = group
 ldap_user_home_directory = unixHomeDirectory
 ldap_user_principal = userPrincipalName
 ldap_account_expire_policy = ad
 ldap_force_upper_case_realm = true
 fallback_homedir = /home/%d/%u

 krb5_server = contoso100.com
 krb5_realm = CONTOSO100.COM
 ```
<span data-ttu-id="d0d72-133">Replace 'CONTOSO100.COM' with the DNS domain name of your managed domain.</span><span class="sxs-lookup"><span data-stu-id="d0d72-133">Replace 'CONTOSO100.COM' with the DNS domain name of your managed domain.</span></span> <span data-ttu-id="d0d72-134">Make sure you specify the domain name in capital case in the conf file.</span><span class="sxs-lookup"><span data-stu-id="d0d72-134">Make sure you specify the domain name in capital case in the conf file.</span></span>


## <a name="join-the-linux-virtual-machine-to-the-managed-domain"></a><span data-ttu-id="d0d72-135">Join the Linux virtual machine to the managed domain</span><span class="sxs-lookup"><span data-stu-id="d0d72-135">Join the Linux virtual machine to the managed domain</span></span>
<span data-ttu-id="d0d72-136">Now that the required packages are installed on the Linux virtual machine, the next task is to join the virtual machine to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="d0d72-136">Now that the required packages are installed on the Linux virtual machine, the next task is to join the virtual machine to the managed domain.</span></span>

```
sudo adcli join -D CONTOSO100.COM -U bob@CONTOSO100.COM -K /etc/krb5.keytab -H contoso-coreos.contoso100.com -N coreos
```


> [!NOTE]
> <span data-ttu-id="d0d72-137">**Troubleshooting:** If *adcli* is unable to find your managed domain:</span><span class="sxs-lookup"><span data-stu-id="d0d72-137">**Troubleshooting:** If *adcli* is unable to find your managed domain:</span></span>
  * <span data-ttu-id="d0d72-138">Ensure that the domain is reachable from the virtual machine (try ping).</span><span class="sxs-lookup"><span data-stu-id="d0d72-138">Ensure that the domain is reachable from the virtual machine (try ping).</span></span>
  * <span data-ttu-id="d0d72-139">Check that the virtual machine has indeed been deployed to the same virtual network in which the managed domain is available.</span><span class="sxs-lookup"><span data-stu-id="d0d72-139">Check that the virtual machine has indeed been deployed to the same virtual network in which the managed domain is available.</span></span>
  * <span data-ttu-id="d0d72-140">Check to see if you have updated the DNS server settings for the virtual network to point to the domain controllers of the managed domain.</span><span class="sxs-lookup"><span data-stu-id="d0d72-140">Check to see if you have updated the DNS server settings for the virtual network to point to the domain controllers of the managed domain.</span></span>
>

<span data-ttu-id="d0d72-141">Start the SSSD service.</span><span class="sxs-lookup"><span data-stu-id="d0d72-141">Start the SSSD service.</span></span> <span data-ttu-id="d0d72-142">In your SSH terminal, type the following command:</span><span class="sxs-lookup"><span data-stu-id="d0d72-142">In your SSH terminal, type the following command:</span></span>
  ```
  sudo systemctl start sssd.service
  ```


## <a name="verify-domain-join"></a><span data-ttu-id="d0d72-143">Verify domain join</span><span class="sxs-lookup"><span data-stu-id="d0d72-143">Verify domain join</span></span>
<span data-ttu-id="d0d72-144">Verify whether the machine has been successfully joined to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="d0d72-144">Verify whether the machine has been successfully joined to the managed domain.</span></span> <span data-ttu-id="d0d72-145">Connect to the domain joined CoreOS VM using a different SSH connection.</span><span class="sxs-lookup"><span data-stu-id="d0d72-145">Connect to the domain joined CoreOS VM using a different SSH connection.</span></span> <span data-ttu-id="d0d72-146">Use a domain user account and then check to see if the user account is resolved correctly.</span><span class="sxs-lookup"><span data-stu-id="d0d72-146">Use a domain user account and then check to see if the user account is resolved correctly.</span></span>

1. <span data-ttu-id="d0d72-147">In your SSH terminal, type the following command to connect to the domain joined CoreOS virtual machine using SSH.</span><span class="sxs-lookup"><span data-stu-id="d0d72-147">In your SSH terminal, type the following command to connect to the domain joined CoreOS virtual machine using SSH.</span></span> <span data-ttu-id="d0d72-148">Use a domain account that belongs to the managed domain (for example, 'bob@CONTOSO100.COM' in this case.)</span><span class="sxs-lookup"><span data-stu-id="d0d72-148">Use a domain account that belongs to the managed domain (for example, 'bob@CONTOSO100.COM' in this case.)</span></span>
    ```
    ssh -l bob@CONTOSO100.COM contoso-coreos.contoso100.com
    ```

2. <span data-ttu-id="d0d72-149">In your SSH terminal, type the following command to see if the home directory was initialized correctly.</span><span class="sxs-lookup"><span data-stu-id="d0d72-149">In your SSH terminal, type the following command to see if the home directory was initialized correctly.</span></span>
    ```
    pwd
    ```

3. <span data-ttu-id="d0d72-150">In your SSH terminal, type the following command to see if the group memberships are being resolved correctly.</span><span class="sxs-lookup"><span data-stu-id="d0d72-150">In your SSH terminal, type the following command to see if the group memberships are being resolved correctly.</span></span>
    ```
    id
    ```


## <a name="troubleshooting-domain-join"></a><span data-ttu-id="d0d72-151">Troubleshooting domain join</span><span class="sxs-lookup"><span data-stu-id="d0d72-151">Troubleshooting domain join</span></span>
<span data-ttu-id="d0d72-152">Refer to the [Troubleshooting domain join](active-directory-ds-admin-guide-join-windows-vm-portal.md#troubleshoot-joining-a-domain) article.</span><span class="sxs-lookup"><span data-stu-id="d0d72-152">Refer to the [Troubleshooting domain join](active-directory-ds-admin-guide-join-windows-vm-portal.md#troubleshoot-joining-a-domain) article.</span></span>

## <a name="related-content"></a><span data-ttu-id="d0d72-153">Related Content</span><span class="sxs-lookup"><span data-stu-id="d0d72-153">Related Content</span></span>
* [<span data-ttu-id="d0d72-154">Azure AD Domain Services - Getting Started guide</span><span class="sxs-lookup"><span data-stu-id="d0d72-154">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="d0d72-155">Join a Windows Server virtual machine to an Azure AD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="d0d72-155">Join a Windows Server virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* <span data-ttu-id="d0d72-156">[How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d0d72-156">[How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
