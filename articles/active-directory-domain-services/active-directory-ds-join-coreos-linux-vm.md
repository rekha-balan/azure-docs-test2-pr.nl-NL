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
# <a name="join-a-coreos-linux-virtual-machine-to-a-managed-domain"></a>Join a CoreOS Linux virtual machine to a managed domain
This article shows you how to join a CoreOS Linux virtual machine in Azure to an Azure AD Domain Services managed domain.

[!INCLUDE [active-directory-ds-prerequisites.md](../../includes/active-directory-ds-prerequisites.md)]

## <a name="before-you-begin"></a>Before you begin
To perform the tasks listed in this article, you need:
1. A valid **Azure subscription**.
2. An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.
3. **Azure AD Domain Services** must be enabled for the Azure AD directory. If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).
4. Ensure that you have configured the IP addresses of the managed domain as the DNS servers for the virtual network. For more information, see [how to update DNS settings for the Azure virtual network](active-directory-ds-getting-started-dns.md)
5. Complete the steps required to [synchronize passwords to your Azure AD Domain Services managed domain](active-directory-ds-getting-started-password-sync.md).


## <a name="provision-a-coreos-linux-virtual-machine"></a>Provision a CoreOS Linux virtual machine
Provision a CoreOS virtual machine in Azure, using any of the following methods:
* [Azure portal](../virtual-machines/linux/quick-create-portal.md)
* [Azure CLI](../virtual-machines/linux/quick-create-cli.md)
* [Azure PowerShell](../virtual-machines/linux/quick-create-powershell.md)

This article uses the **CoreOS Linux (Stable)** virtual machine image in Azure.

> [!IMPORTANT]
> * Deploy the virtual machine into the **same virtual network in which you have enabled Azure AD Domain Services**.
> * Pick a **different subnet** than the one in which you have enabled Azure AD Domain Services.
>


## <a name="connect-remotely-to-the-newly-provisioned-linux-virtual-machine"></a>Connect remotely to the newly provisioned Linux virtual machine
The CoreOS virtual machine has been provisioned in Azure. The next task is to connect remotely to the virtual machine using the local administrator account created while provisioning the VM.

Follow the instructions in the article [How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="configure-the-hosts-file-on-the-linux-virtual-machine"></a>Configure the hosts file on the Linux virtual machine
In your SSH terminal, edit the /etc/hosts file and update your machine’s IP address and hostname.

```
sudo vi /etc/hosts
```

In the hosts file, enter the following value:

```
127.0.0.1 contoso-coreos.contoso100.com contoso-coreos
```
Here, 'contoso100.com' is the DNS domain name of your managed domain. 'contoso-coreos' is the hostname of the CoreOS virtual machine you are joining to the managed domain.


## <a name="configure-the-sssd-service-on-the-linux-virtual-machine"></a>Configure the SSSD service on the Linux virtual machine
Next, update your SSSD configuration file in ('/etc/sssd/sssd.conf') to match the following sample:

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
Replace 'CONTOSO100.COM' with the DNS domain name of your managed domain. Make sure you specify the domain name in capital case in the conf file.


## <a name="join-the-linux-virtual-machine-to-the-managed-domain"></a>Join the Linux virtual machine to the managed domain
Now that the required packages are installed on the Linux virtual machine, the next task is to join the virtual machine to the managed domain.

```
sudo adcli join -D CONTOSO100.COM -U bob@CONTOSO100.COM -K /etc/krb5.keytab -H contoso-coreos.contoso100.com -N coreos
```


> [!NOTE]
> **Troubleshooting:** If *adcli* is unable to find your managed domain:
  * Ensure that the domain is reachable from the virtual machine (try ping).
  * Check that the virtual machine has indeed been deployed to the same virtual network in which the managed domain is available.
  * Check to see if you have updated the DNS server settings for the virtual network to point to the domain controllers of the managed domain.
>

Start the SSSD service. In your SSH terminal, type the following command:
  ```
  sudo systemctl start sssd.service
  ```


## <a name="verify-domain-join"></a>Verify domain join
Verify whether the machine has been successfully joined to the managed domain. Connect to the domain joined CoreOS VM using a different SSH connection. Use a domain user account and then check to see if the user account is resolved correctly.

1. In your SSH terminal, type the following command to connect to the domain joined CoreOS virtual machine using SSH. Use a domain account that belongs to the managed domain (for example, 'bob@CONTOSO100.COM' in this case.)
    ```
    ssh -l bob@CONTOSO100.COM contoso-coreos.contoso100.com
    ```

2. In your SSH terminal, type the following command to see if the home directory was initialized correctly.
    ```
    pwd
    ```

3. In your SSH terminal, type the following command to see if the group memberships are being resolved correctly.
    ```
    id
    ```


## <a name="troubleshooting-domain-join"></a>Troubleshooting domain join
Refer to the [Troubleshooting domain join](active-directory-ds-admin-guide-join-windows-vm-portal.md#troubleshoot-joining-a-domain) article.

## <a name="related-content"></a>Related Content
* [Azure AD Domain Services - Getting Started guide](active-directory-ds-getting-started.md)
* [Join a Windows Server virtual machine to an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-join-windows-vm.md)
* [How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
