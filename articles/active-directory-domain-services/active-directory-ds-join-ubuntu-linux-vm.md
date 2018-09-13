---
title: 'Azure Active Directory Domain Services: Join an Ubuntu VM to a managed domain | Microsoft Docs'
description: Join an Ubuntu Linux virtual machine to Azure AD Domain Services
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: mtillman
editor: curtand
ms.assetid: 804438c4-51a1-497d-8ccc-5be775980203
ms.service: active-directory
ms.component: domain-services
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 06/22/2018
ms.author: maheshu
ms.openlocfilehash: 645e1eaedf3832b384a174d9f9ede5ea835047cd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864524"
---
# <a name="join-an-ubuntu-virtual-machine-in-azure-to-a-managed-domain"></a><span data-ttu-id="b5e9c-103">Join an Ubuntu virtual machine in Azure to a managed domain</span><span class="sxs-lookup"><span data-stu-id="b5e9c-103">Join an Ubuntu virtual machine in Azure to a managed domain</span></span>
<span data-ttu-id="b5e9c-104">This article shows you how to join an Ubuntu Linux virtual machine to an Azure AD Domain Services managed domain.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-104">This article shows you how to join an Ubuntu Linux virtual machine to an Azure AD Domain Services managed domain.</span></span>

[!INCLUDE [active-directory-ds-prerequisites.md](../../includes/active-directory-ds-prerequisites.md)]

## <a name="before-you-begin"></a><span data-ttu-id="b5e9c-105">Before you begin</span><span class="sxs-lookup"><span data-stu-id="b5e9c-105">Before you begin</span></span>
<span data-ttu-id="b5e9c-106">To perform the tasks listed in this article, you need:</span><span class="sxs-lookup"><span data-stu-id="b5e9c-106">To perform the tasks listed in this article, you need:</span></span>  
1. <span data-ttu-id="b5e9c-107">A valid **Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-107">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="b5e9c-108">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-108">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="b5e9c-109">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-109">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span></span> <span data-ttu-id="b5e9c-110">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="b5e9c-110">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="b5e9c-111">Ensure that you have configured the IP addresses of the managed domain as the DNS servers for the virtual network.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-111">Ensure that you have configured the IP addresses of the managed domain as the DNS servers for the virtual network.</span></span> <span data-ttu-id="b5e9c-112">For more information, see [how to update DNS settings for the Azure virtual network](active-directory-ds-getting-started-dns.md)</span><span class="sxs-lookup"><span data-stu-id="b5e9c-112">For more information, see [how to update DNS settings for the Azure virtual network](active-directory-ds-getting-started-dns.md)</span></span>
5. <span data-ttu-id="b5e9c-113">Complete the steps required to [synchronize passwords to your Azure AD Domain Services managed domain](active-directory-ds-getting-started-password-sync.md).</span><span class="sxs-lookup"><span data-stu-id="b5e9c-113">Complete the steps required to [synchronize passwords to your Azure AD Domain Services managed domain](active-directory-ds-getting-started-password-sync.md).</span></span>


## <a name="provision-an-ubuntu-linux-virtual-machine"></a><span data-ttu-id="b5e9c-114">Provision an Ubuntu Linux virtual machine</span><span class="sxs-lookup"><span data-stu-id="b5e9c-114">Provision an Ubuntu Linux virtual machine</span></span>
<span data-ttu-id="b5e9c-115">Provision an Ubuntu Linux virtual machine in Azure, using any of the following methods:</span><span class="sxs-lookup"><span data-stu-id="b5e9c-115">Provision an Ubuntu Linux virtual machine in Azure, using any of the following methods:</span></span>
* [<span data-ttu-id="b5e9c-116">Azure portal</span><span class="sxs-lookup"><span data-stu-id="b5e9c-116">Azure portal</span></span>](../virtual-machines/linux/quick-create-portal.md)
* [<span data-ttu-id="b5e9c-117">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b5e9c-117">Azure CLI</span></span>](../virtual-machines/linux/quick-create-cli.md)
* [<span data-ttu-id="b5e9c-118">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b5e9c-118">Azure PowerShell</span></span>](../virtual-machines/linux/quick-create-powershell.md)

> [!IMPORTANT]
> * <span data-ttu-id="b5e9c-119">Deploy the virtual machine into the **same virtual network in which you have enabled Azure AD Domain Services**.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-119">Deploy the virtual machine into the **same virtual network in which you have enabled Azure AD Domain Services**.</span></span>
> * <span data-ttu-id="b5e9c-120">Pick a **different subnet** than the one in which you have enabled Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-120">Pick a **different subnet** than the one in which you have enabled Azure AD Domain Services.</span></span>
>


## <a name="connect-remotely-to-the-ubuntu-linux-virtual-machine"></a><span data-ttu-id="b5e9c-121">Connect remotely to the Ubuntu Linux virtual machine</span><span class="sxs-lookup"><span data-stu-id="b5e9c-121">Connect remotely to the Ubuntu Linux virtual machine</span></span>
<span data-ttu-id="b5e9c-122">The Ubuntu virtual machine has been provisioned in Azure.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-122">The Ubuntu virtual machine has been provisioned in Azure.</span></span> <span data-ttu-id="b5e9c-123">The next task is to connect remotely to the virtual machine using the local administrator account created while provisioning the VM.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-123">The next task is to connect remotely to the virtual machine using the local administrator account created while provisioning the VM.</span></span>

<span data-ttu-id="b5e9c-124">Follow the instructions in the article [How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b5e9c-124">Follow the instructions in the article [How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="configure-the-hosts-file-on-the-linux-virtual-machine"></a><span data-ttu-id="b5e9c-125">Configure the hosts file on the Linux virtual machine</span><span class="sxs-lookup"><span data-stu-id="b5e9c-125">Configure the hosts file on the Linux virtual machine</span></span>
<span data-ttu-id="b5e9c-126">In your SSH terminal, edit the /etc/hosts file and update your machine’s IP address and hostname.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-126">In your SSH terminal, edit the /etc/hosts file and update your machine’s IP address and hostname.</span></span>

```
sudo vi /etc/hosts
```

<span data-ttu-id="b5e9c-127">In the hosts file, enter the following value:</span><span class="sxs-lookup"><span data-stu-id="b5e9c-127">In the hosts file, enter the following value:</span></span>

```
127.0.0.1 contoso-ubuntu.contoso100.com contoso-ubuntu
```
<span data-ttu-id="b5e9c-128">Here, 'contoso100.com' is the DNS domain name of your managed domain.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-128">Here, 'contoso100.com' is the DNS domain name of your managed domain.</span></span> <span data-ttu-id="b5e9c-129">'contoso-ubuntu' is the hostname of the Ubuntu virtual machine you are joining to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-129">'contoso-ubuntu' is the hostname of the Ubuntu virtual machine you are joining to the managed domain.</span></span>


## <a name="install-required-packages-on-the-linux-virtual-machine"></a><span data-ttu-id="b5e9c-130">Install required packages on the Linux virtual machine</span><span class="sxs-lookup"><span data-stu-id="b5e9c-130">Install required packages on the Linux virtual machine</span></span>
<span data-ttu-id="b5e9c-131">Next, install packages required for domain join on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-131">Next, install packages required for domain join on the virtual machine.</span></span> <span data-ttu-id="b5e9c-132">Perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b5e9c-132">Perform the following steps:</span></span>

1.  <span data-ttu-id="b5e9c-133">In your SSH terminal, type the following command to download the package lists from the repositories.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-133">In your SSH terminal, type the following command to download the package lists from the repositories.</span></span> <span data-ttu-id="b5e9c-134">This command updates the package lists to get information on the newest versions of packages and their dependencies.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-134">This command updates the package lists to get information on the newest versions of packages and their dependencies.</span></span>

    ```
    sudo apt-get update
    ```

2. <span data-ttu-id="b5e9c-135">Type the following command to install the required packages.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-135">Type the following command to install the required packages.</span></span>
    ```
      sudo apt-get install krb5-user samba sssd sssd-tools libnss-sss libpam-sss ntp ntpdate realmd adcli
    ```

3. <span data-ttu-id="b5e9c-136">During the Kerberos installation, you see a pink screen.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-136">During the Kerberos installation, you see a pink screen.</span></span> <span data-ttu-id="b5e9c-137">The installation of the 'krb5-user' package prompts for the realm name (in ALL UPPERCASE).</span><span class="sxs-lookup"><span data-stu-id="b5e9c-137">The installation of the 'krb5-user' package prompts for the realm name (in ALL UPPERCASE).</span></span> <span data-ttu-id="b5e9c-138">The installation writes the [realm] and [domain_realm] sections in /etc/krb5.conf.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-138">The installation writes the [realm] and [domain_realm] sections in /etc/krb5.conf.</span></span>

    > [!TIP]
    > <span data-ttu-id="b5e9c-139">If the name of your managed domain is contoso100.com, enter CONTOSO100.COM as the realm.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-139">If the name of your managed domain is contoso100.com, enter CONTOSO100.COM as the realm.</span></span> <span data-ttu-id="b5e9c-140">Remember, the realm name must be specified in UPPERCASE.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-140">Remember, the realm name must be specified in UPPERCASE.</span></span>
    >
    >


## <a name="configure-the-ntp-network-time-protocol-settings-on-the-linux-virtual-machine"></a><span data-ttu-id="b5e9c-141">Configure the NTP (Network Time Protocol) settings on the Linux virtual machine</span><span class="sxs-lookup"><span data-stu-id="b5e9c-141">Configure the NTP (Network Time Protocol) settings on the Linux virtual machine</span></span>
<span data-ttu-id="b5e9c-142">The date and time of your Ubuntu VM must synchronize with the managed domain.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-142">The date and time of your Ubuntu VM must synchronize with the managed domain.</span></span> <span data-ttu-id="b5e9c-143">Add your managed domain's NTP hostname in the /etc/ntp.conf file.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-143">Add your managed domain's NTP hostname in the /etc/ntp.conf file.</span></span>

```
sudo vi /etc/ntp.conf
```

<span data-ttu-id="b5e9c-144">In the ntp.conf file, enter the following value and save the file:</span><span class="sxs-lookup"><span data-stu-id="b5e9c-144">In the ntp.conf file, enter the following value and save the file:</span></span>

```
server contoso100.com
```
<span data-ttu-id="b5e9c-145">Here, 'contoso100.com' is the DNS domain name of your managed domain.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-145">Here, 'contoso100.com' is the DNS domain name of your managed domain.</span></span>

<span data-ttu-id="b5e9c-146">Now sync the Ubuntu VM's date and time with NTP server and then start the NTP service:</span><span class="sxs-lookup"><span data-stu-id="b5e9c-146">Now sync the Ubuntu VM's date and time with NTP server and then start the NTP service:</span></span>

```
sudo systemctl stop ntp
sudo ntpdate contoso100.com
sudo systemctl start ntp
```


## <a name="join-the-linux-virtual-machine-to-the-managed-domain"></a><span data-ttu-id="b5e9c-147">Join the Linux virtual machine to the managed domain</span><span class="sxs-lookup"><span data-stu-id="b5e9c-147">Join the Linux virtual machine to the managed domain</span></span>
<span data-ttu-id="b5e9c-148">Now that the required packages are installed on the Linux virtual machine, the next task is to join the virtual machine to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-148">Now that the required packages are installed on the Linux virtual machine, the next task is to join the virtual machine to the managed domain.</span></span>

1. <span data-ttu-id="b5e9c-149">Discover the AAD Domain Services managed domain.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-149">Discover the AAD Domain Services managed domain.</span></span> <span data-ttu-id="b5e9c-150">In your SSH terminal, type the following command:</span><span class="sxs-lookup"><span data-stu-id="b5e9c-150">In your SSH terminal, type the following command:</span></span>

    ```
    sudo realm discover CONTOSO100.COM
    ```

   > [!NOTE]
   > <span data-ttu-id="b5e9c-151">**Troubleshooting:** If *realm discover* is unable to find your managed domain:</span><span class="sxs-lookup"><span data-stu-id="b5e9c-151">**Troubleshooting:** If *realm discover* is unable to find your managed domain:</span></span>
     * <span data-ttu-id="b5e9c-152">Ensure that the domain is reachable from the virtual machine (try ping).</span><span class="sxs-lookup"><span data-stu-id="b5e9c-152">Ensure that the domain is reachable from the virtual machine (try ping).</span></span>
     * <span data-ttu-id="b5e9c-153">Check that the virtual machine has indeed been deployed to the same virtual network in which the managed domain is available.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-153">Check that the virtual machine has indeed been deployed to the same virtual network in which the managed domain is available.</span></span>
     * <span data-ttu-id="b5e9c-154">Check to see if you have updated the DNS server settings for the virtual network to point to the domain controllers of the managed domain.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-154">Check to see if you have updated the DNS server settings for the virtual network to point to the domain controllers of the managed domain.</span></span>
   >

2. <span data-ttu-id="b5e9c-155">Initialize Kerberos.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-155">Initialize Kerberos.</span></span> <span data-ttu-id="b5e9c-156">In your SSH terminal, type the following command:</span><span class="sxs-lookup"><span data-stu-id="b5e9c-156">In your SSH terminal, type the following command:</span></span>

    > [!TIP]
    > * <span data-ttu-id="b5e9c-157">Ensure that you specify a user who belongs to the 'AAD DC Administrators' group.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-157">Ensure that you specify a user who belongs to the 'AAD DC Administrators' group.</span></span>
    > * <span data-ttu-id="b5e9c-158">Specify the domain name in capital letters, else kinit fails.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-158">Specify the domain name in capital letters, else kinit fails.</span></span>
    >

    ```
    kinit bob@CONTOSO100.COM
    ```

3. <span data-ttu-id="b5e9c-159">Join the machine to the domain.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-159">Join the machine to the domain.</span></span> <span data-ttu-id="b5e9c-160">In your SSH terminal, type the following command:</span><span class="sxs-lookup"><span data-stu-id="b5e9c-160">In your SSH terminal, type the following command:</span></span>

    > [!TIP]
    > <span data-ttu-id="b5e9c-161">Use the same user account you specified in the preceding step ('kinit').</span><span class="sxs-lookup"><span data-stu-id="b5e9c-161">Use the same user account you specified in the preceding step ('kinit').</span></span>
    >

    ```
    sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM' --install=/
    ```

<span data-ttu-id="b5e9c-162">You should get a message ("Successfully enrolled machine in realm") when the machine is successfully joined to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-162">You should get a message ("Successfully enrolled machine in realm") when the machine is successfully joined to the managed domain.</span></span>


## <a name="update-the-sssd-configuration-and-restart-the-service"></a><span data-ttu-id="b5e9c-163">Update the SSSD configuration and restart the service</span><span class="sxs-lookup"><span data-stu-id="b5e9c-163">Update the SSSD configuration and restart the service</span></span>
1. <span data-ttu-id="b5e9c-164">In your SSH terminal, type the following command.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-164">In your SSH terminal, type the following command.</span></span> <span data-ttu-id="b5e9c-165">Open the sssd.conf file and make the following change</span><span class="sxs-lookup"><span data-stu-id="b5e9c-165">Open the sssd.conf file and make the following change</span></span>
    ```
    sudo vi /etc/sssd/sssd.conf
    ```

2. <span data-ttu-id="b5e9c-166">Comment out the line **use_fully_qualified_names = True** and save the file.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-166">Comment out the line **use_fully_qualified_names = True** and save the file.</span></span>
    ```
    # use_fully_qualified_names = True
    ```

3. <span data-ttu-id="b5e9c-167">Restart the SSSD service.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-167">Restart the SSSD service.</span></span>
    ```
    sudo service sssd restart
    ```


## <a name="configure-automatic-home-directory-creation"></a><span data-ttu-id="b5e9c-168">Configure automatic home directory creation</span><span class="sxs-lookup"><span data-stu-id="b5e9c-168">Configure automatic home directory creation</span></span>
<span data-ttu-id="b5e9c-169">To enable automatic creation of the home directory after logging in users, type the following commands in your PuTTY terminal:</span><span class="sxs-lookup"><span data-stu-id="b5e9c-169">To enable automatic creation of the home directory after logging in users, type the following commands in your PuTTY terminal:</span></span>
```
sudo vi /etc/pam.d/common-session
```

<span data-ttu-id="b5e9c-170">Add the following line in this file below the line 'session optional pam_sss.so' and save it:</span><span class="sxs-lookup"><span data-stu-id="b5e9c-170">Add the following line in this file below the line 'session optional pam_sss.so' and save it:</span></span>
```
session required pam_mkhomedir.so skel=/etc/skel/ umask=0077
```


## <a name="verify-domain-join"></a><span data-ttu-id="b5e9c-171">Verify domain join</span><span class="sxs-lookup"><span data-stu-id="b5e9c-171">Verify domain join</span></span>
<span data-ttu-id="b5e9c-172">Verify whether the machine has been successfully joined to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-172">Verify whether the machine has been successfully joined to the managed domain.</span></span> <span data-ttu-id="b5e9c-173">Connect to the domain joined Ubuntu VM using a different SSH connection.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-173">Connect to the domain joined Ubuntu VM using a different SSH connection.</span></span> <span data-ttu-id="b5e9c-174">Use a domain user account and then check to see if the user account is resolved correctly.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-174">Use a domain user account and then check to see if the user account is resolved correctly.</span></span>

1. <span data-ttu-id="b5e9c-175">In your SSH terminal, type the following command to connect to the domain joined Ubuntu virtual machine using SSH.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-175">In your SSH terminal, type the following command to connect to the domain joined Ubuntu virtual machine using SSH.</span></span> <span data-ttu-id="b5e9c-176">Use a domain account that belongs to the managed domain (for example, 'bob@CONTOSO100.COM' in this case.)</span><span class="sxs-lookup"><span data-stu-id="b5e9c-176">Use a domain account that belongs to the managed domain (for example, 'bob@CONTOSO100.COM' in this case.)</span></span>
    ```
    ssh -l bob@CONTOSO100.COM contoso-ubuntu.contoso100.com
    ```

2. <span data-ttu-id="b5e9c-177">In your SSH terminal, type the following command to see if the home directory was initialized correctly.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-177">In your SSH terminal, type the following command to see if the home directory was initialized correctly.</span></span>
    ```
    pwd
    ```

3. <span data-ttu-id="b5e9c-178">In your SSH terminal, type the following command to see if the group memberships are being resolved correctly.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-178">In your SSH terminal, type the following command to see if the group memberships are being resolved correctly.</span></span>
    ```
    id
    ```


## <a name="grant-the-aad-dc-administrators-group-sudo-privileges"></a><span data-ttu-id="b5e9c-179">Grant the 'AAD DC Administrators' group sudo privileges</span><span class="sxs-lookup"><span data-stu-id="b5e9c-179">Grant the 'AAD DC Administrators' group sudo privileges</span></span>
<span data-ttu-id="b5e9c-180">You can grant members of the 'AAD DC Administrators' group administrative privileges on the Ubuntu VM.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-180">You can grant members of the 'AAD DC Administrators' group administrative privileges on the Ubuntu VM.</span></span> <span data-ttu-id="b5e9c-181">The sudo file is located at /etc/sudoers.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-181">The sudo file is located at /etc/sudoers.</span></span> <span data-ttu-id="b5e9c-182">The members of AD groups added in sudoers can perform sudo.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-182">The members of AD groups added in sudoers can perform sudo.</span></span>

1. <span data-ttu-id="b5e9c-183">In your SSH terminal, ensure you are logged in with superuser privileges.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-183">In your SSH terminal, ensure you are logged in with superuser privileges.</span></span> <span data-ttu-id="b5e9c-184">You can use the local administrator account you specified while creating the VM.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-184">You can use the local administrator account you specified while creating the VM.</span></span> <span data-ttu-id="b5e9c-185">Execute the following command:</span><span class="sxs-lookup"><span data-stu-id="b5e9c-185">Execute the following command:</span></span>
    ```
    sudo vi /etc/sudoers
    ```

2. <span data-ttu-id="b5e9c-186">Add the following entry to the /etc/sudoers file and save it:</span><span class="sxs-lookup"><span data-stu-id="b5e9c-186">Add the following entry to the /etc/sudoers file and save it:</span></span>
    ```
    # Add 'AAD DC Administrators' group members as admins.
    %AAD\ DC\ Administrators ALL=(ALL) NOPASSWD:ALL
    ```

3. <span data-ttu-id="b5e9c-187">You can now log in as a member of the 'AAD DC Administrators' group and should have administrative privileges on the VM.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-187">You can now log in as a member of the 'AAD DC Administrators' group and should have administrative privileges on the VM.</span></span>


## <a name="troubleshooting-domain-join"></a><span data-ttu-id="b5e9c-188">Troubleshooting domain join</span><span class="sxs-lookup"><span data-stu-id="b5e9c-188">Troubleshooting domain join</span></span>
<span data-ttu-id="b5e9c-189">Refer to the [Troubleshooting domain join](active-directory-ds-admin-guide-join-windows-vm-portal.md#troubleshoot-joining-a-domain) article.</span><span class="sxs-lookup"><span data-stu-id="b5e9c-189">Refer to the [Troubleshooting domain join](active-directory-ds-admin-guide-join-windows-vm-portal.md#troubleshoot-joining-a-domain) article.</span></span>


## <a name="related-content"></a><span data-ttu-id="b5e9c-190">Related Content</span><span class="sxs-lookup"><span data-stu-id="b5e9c-190">Related Content</span></span>
* [<span data-ttu-id="b5e9c-191">Azure AD Domain Services - Getting Started guide</span><span class="sxs-lookup"><span data-stu-id="b5e9c-191">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="b5e9c-192">Join a Windows Server virtual machine to an Azure AD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="b5e9c-192">Join a Windows Server virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* <span data-ttu-id="b5e9c-193">[How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b5e9c-193">[How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
