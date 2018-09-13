---
title: Introduction to FreeBSD on Azure | Microsoft Docs
description: Learn about using FreeBSD virtual machines on Azure
services: virtual-machines-linux
documentationcenter: ''
author: KylieLiang
manager: timlt
editor: ''
tags: azure-service-management
ms.assetid: 32b87a5f-d024-4da0-8bf0-77e233d1422b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: kyliel
ms.openlocfilehash: d0fc5de34f7d9e5a607495eb97d9e35dc9eb21f9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563307"
---
# <a name="introduction-to-freebsd-on-azure"></a><span data-ttu-id="6c75f-103">Introduction to FreeBSD on Azure</span><span class="sxs-lookup"><span data-stu-id="6c75f-103">Introduction to FreeBSD on Azure</span></span>
<span data-ttu-id="6c75f-104">This topic provides an overview of running a FreeBSD virtual machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="6c75f-104">This topic provides an overview of running a FreeBSD virtual machine in Azure.</span></span>

## <a name="overview"></a><span data-ttu-id="6c75f-105">Overview</span><span class="sxs-lookup"><span data-stu-id="6c75f-105">Overview</span></span>
<span data-ttu-id="6c75f-106">FreeBSD for Microsoft Azure is an advanced computer operating system used to power modern servers, desktops, and embedded platforms.</span><span class="sxs-lookup"><span data-stu-id="6c75f-106">FreeBSD for Microsoft Azure is an advanced computer operating system used to power modern servers, desktops, and embedded platforms.</span></span>

<span data-ttu-id="6c75f-107">Microsoft Corporation is making images of FreeBSD available on Azure with the [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) pre-configured.</span><span class="sxs-lookup"><span data-stu-id="6c75f-107">Microsoft Corporation is making images of FreeBSD available on Azure with the [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) pre-configured.</span></span> <span data-ttu-id="6c75f-108">Currently, the following FreeBSD versions are offered as images by Microsoft:</span><span class="sxs-lookup"><span data-stu-id="6c75f-108">Currently, the following FreeBSD versions are offered as images by Microsoft:</span></span>

- <span data-ttu-id="6c75f-109">FreeBSD 10.3-RELEASE</span><span class="sxs-lookup"><span data-stu-id="6c75f-109">FreeBSD 10.3-RELEASE</span></span>
- <span data-ttu-id="6c75f-110">FreeBSD 11.0-RELEASE</span><span class="sxs-lookup"><span data-stu-id="6c75f-110">FreeBSD 11.0-RELEASE</span></span>

<span data-ttu-id="6c75f-111">The agent is responsible for communication between the FreeBSD VM and the Azure fabric for operations such as provisioning the VM on first use (user name, password or SSH key, host name, etc.) and enabling functionality for selective VM extensions.</span><span class="sxs-lookup"><span data-stu-id="6c75f-111">The agent is responsible for communication between the FreeBSD VM and the Azure fabric for operations such as provisioning the VM on first use (user name, password or SSH key, host name, etc.) and enabling functionality for selective VM extensions.</span></span>

<span data-ttu-id="6c75f-112">As for future versions of FreeBSD, the strategy is to stay current and make the latest releases available shortly after they are published by the FreeBSD release engineering team.</span><span class="sxs-lookup"><span data-stu-id="6c75f-112">As for future versions of FreeBSD, the strategy is to stay current and make the latest releases available shortly after they are published by the FreeBSD release engineering team.</span></span>

## <a name="deploying-a-freebsd-virtual-machine"></a><span data-ttu-id="6c75f-113">Deploying a FreeBSD virtual machine</span><span class="sxs-lookup"><span data-stu-id="6c75f-113">Deploying a FreeBSD virtual machine</span></span>
<span data-ttu-id="6c75f-114">Deploying a FreeBSD virtual machine is a straightforward process using an image from the Azure Marketplace from the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="6c75f-114">Deploying a FreeBSD virtual machine is a straightforward process using an image from the Azure Marketplace from the Azure portal:</span></span>

- [<span data-ttu-id="6c75f-115">FreeBSD 10.3 on the Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="6c75f-115">FreeBSD 10.3 on the Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [<span data-ttu-id="6c75f-116">FreeBSD 11.0 on the Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="6c75f-116">FreeBSD 11.0 on the Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a><span data-ttu-id="6c75f-117">Create a FreeBSD VM through Azure CLI 2.0 on FreeBSD</span><span class="sxs-lookup"><span data-stu-id="6c75f-117">Create a FreeBSD VM through Azure CLI 2.0 on FreeBSD</span></span>
<span data-ttu-id="6c75f-118">First you need to install [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) though following command on a FreeBSD machine.</span><span class="sxs-lookup"><span data-stu-id="6c75f-118">First you need to install [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) though following command on a FreeBSD machine.</span></span>

```bash 
    curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="6c75f-119">If bash is not installed on your FreeBSD machine, run following command before the installation.</span><span class="sxs-lookup"><span data-stu-id="6c75f-119">If bash is not installed on your FreeBSD machine, run following command before the installation.</span></span> 

```
    sudo pkg install bash
```

<span data-ttu-id="6c75f-120">If python is not installed on your FreeBSD machine, run following commands before the installation.</span><span class="sxs-lookup"><span data-stu-id="6c75f-120">If python is not installed on your FreeBSD machine, run following commands before the installation.</span></span> 

```
    sudo pkg install python35
    cd /usr/local/bin 
    sudo rm /usr/local/bin/python 
    sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

<span data-ttu-id="6c75f-121">During the installation, you are asked `Modify profile to update your $PATH and enable shell/tab completion now? (Y/n)`.</span><span class="sxs-lookup"><span data-stu-id="6c75f-121">During the installation, you are asked `Modify profile to update your $PATH and enable shell/tab completion now? (Y/n)`.</span></span> <span data-ttu-id="6c75f-122">If you answer `y` and enter `/etc/rc.conf` as `a path to an rc file to update`, you may meet the problem `ERROR: [Errno 13] Permission denied`.</span><span class="sxs-lookup"><span data-stu-id="6c75f-122">If you answer `y` and enter `/etc/rc.conf` as `a path to an rc file to update`, you may meet the problem `ERROR: [Errno 13] Permission denied`.</span></span> <span data-ttu-id="6c75f-123">To resolve this problem, you should grant the write right to current user against the file `etc/rc.conf`.</span><span class="sxs-lookup"><span data-stu-id="6c75f-123">To resolve this problem, you should grant the write right to current user against the file `etc/rc.conf`.</span></span>

<span data-ttu-id="6c75f-124">Now you can log in Azure and create your FreeBSD VM.</span><span class="sxs-lookup"><span data-stu-id="6c75f-124">Now you can log in Azure and create your FreeBSD VM.</span></span> <span data-ttu-id="6c75f-125">Below is an example to create a FreeBSD 11.0 VM.</span><span class="sxs-lookup"><span data-stu-id="6c75f-125">Below is an example to create a FreeBSD 11.0 VM.</span></span> <span data-ttu-id="6c75f-126">You can also add the parameter `--public-ip-address-dns-name` with a globally unique DNS name for a newly created Public IP.</span><span class="sxs-lookup"><span data-stu-id="6c75f-126">You can also add the parameter `--public-ip-address-dns-name` with a globally unique DNS name for a newly created Public IP.</span></span> 

```azurecli
    az login 
    az group create -n myResourceGroup -l westus az vm create -n myFreeBSD11 -g myResourceGroup --image MicrosoftOSTC:FreeBSD:11.0:latest --admin-username azureuser --ssh-key-value /etc/ssh/ssh_host_rsa_key.pub 
```

<span data-ttu-id="6c75f-127">Then you can log in to your FreeBSD VM through the ip address that printed in the output of above deployment.</span><span class="sxs-lookup"><span data-stu-id="6c75f-127">Then you can log in to your FreeBSD VM through the ip address that printed in the output of above deployment.</span></span> 

```bash
    ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a><span data-ttu-id="6c75f-128">VM extensions for FreeBSD</span><span class="sxs-lookup"><span data-stu-id="6c75f-128">VM extensions for FreeBSD</span></span>
<span data-ttu-id="6c75f-129">Following are supported VM extensions in FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="6c75f-129">Following are supported VM extensions in FreeBSD.</span></span>

### <a name="vmaccess"></a><span data-ttu-id="6c75f-130">VMAccess</span><span class="sxs-lookup"><span data-stu-id="6c75f-130">VMAccess</span></span>
<span data-ttu-id="6c75f-131">The [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) extension can:</span><span class="sxs-lookup"><span data-stu-id="6c75f-131">The [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) extension can:</span></span>

* <span data-ttu-id="6c75f-132">Reset the password of the original sudo user.</span><span class="sxs-lookup"><span data-stu-id="6c75f-132">Reset the password of the original sudo user.</span></span>
* <span data-ttu-id="6c75f-133">Create a new sudo user with the password specified.</span><span class="sxs-lookup"><span data-stu-id="6c75f-133">Create a new sudo user with the password specified.</span></span>
* <span data-ttu-id="6c75f-134">Set the public host key with the key given.</span><span class="sxs-lookup"><span data-stu-id="6c75f-134">Set the public host key with the key given.</span></span>
* <span data-ttu-id="6c75f-135">Reset the public host key provided during VM provisioning if the host key is not provided.</span><span class="sxs-lookup"><span data-stu-id="6c75f-135">Reset the public host key provided during VM provisioning if the host key is not provided.</span></span>
* <span data-ttu-id="6c75f-136">Open the SSH port (22) and restore the sshd_config if reset_ssh is set to true.</span><span class="sxs-lookup"><span data-stu-id="6c75f-136">Open the SSH port (22) and restore the sshd_config if reset_ssh is set to true.</span></span>
* <span data-ttu-id="6c75f-137">Remove the existing user.</span><span class="sxs-lookup"><span data-stu-id="6c75f-137">Remove the existing user.</span></span>
* <span data-ttu-id="6c75f-138">Check disks.</span><span class="sxs-lookup"><span data-stu-id="6c75f-138">Check disks.</span></span>
* <span data-ttu-id="6c75f-139">Repair an added disk.</span><span class="sxs-lookup"><span data-stu-id="6c75f-139">Repair an added disk.</span></span>

### <a name="customscript"></a><span data-ttu-id="6c75f-140">CustomScript</span><span class="sxs-lookup"><span data-stu-id="6c75f-140">CustomScript</span></span>
<span data-ttu-id="6c75f-141">The [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) extension can:</span><span class="sxs-lookup"><span data-stu-id="6c75f-141">The [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) extension can:</span></span>

* <span data-ttu-id="6c75f-142">If provided, download the customized scripts from Azure Storage or external public storage (for example, GitHub).</span><span class="sxs-lookup"><span data-stu-id="6c75f-142">If provided, download the customized scripts from Azure Storage or external public storage (for example, GitHub).</span></span>
* <span data-ttu-id="6c75f-143">Run the entry point script.</span><span class="sxs-lookup"><span data-stu-id="6c75f-143">Run the entry point script.</span></span>
* <span data-ttu-id="6c75f-144">Support inline commands.</span><span class="sxs-lookup"><span data-stu-id="6c75f-144">Support inline commands.</span></span>
* <span data-ttu-id="6c75f-145">Convert Windows-style newline in shell and Python scripts automatically.</span><span class="sxs-lookup"><span data-stu-id="6c75f-145">Convert Windows-style newline in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="6c75f-146">Remove BOM in shell and Python scripts automatically.</span><span class="sxs-lookup"><span data-stu-id="6c75f-146">Remove BOM in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="6c75f-147">Protect sensitive data in CommandToExecute.</span><span class="sxs-lookup"><span data-stu-id="6c75f-147">Protect sensitive data in CommandToExecute.</span></span>

> [!NOTE]
> <span data-ttu-id="6c75f-148">FreeBSD VM only supports CustomScript version 1.x by now.</span><span class="sxs-lookup"><span data-stu-id="6c75f-148">FreeBSD VM only supports CustomScript version 1.x by now.</span></span>  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a><span data-ttu-id="6c75f-149">Authentication: user names, passwords, and SSH keys</span><span class="sxs-lookup"><span data-stu-id="6c75f-149">Authentication: user names, passwords, and SSH keys</span></span>
<span data-ttu-id="6c75f-150">When you're creating a FreeBSD virtual machine by using the Azure portal, you must provide a user name, password, or SSH public key.</span><span class="sxs-lookup"><span data-stu-id="6c75f-150">When you're creating a FreeBSD virtual machine by using the Azure portal, you must provide a user name, password, or SSH public key.</span></span>
<span data-ttu-id="6c75f-151">User names for deploying a FreeBSD virtual machine on Azure must not match names of system accounts (UID <100) already present in the virtual machine ("root", for example).</span><span class="sxs-lookup"><span data-stu-id="6c75f-151">User names for deploying a FreeBSD virtual machine on Azure must not match names of system accounts (UID <100) already present in the virtual machine ("root", for example).</span></span>
<span data-ttu-id="6c75f-152">Currently, only the RSA SSH key is supported.</span><span class="sxs-lookup"><span data-stu-id="6c75f-152">Currently, only the RSA SSH key is supported.</span></span> <span data-ttu-id="6c75f-153">A multiline SSH key must begin with `---- BEGIN SSH2 PUBLIC KEY ----` and end with `---- END SSH2 PUBLIC KEY ----`.</span><span class="sxs-lookup"><span data-stu-id="6c75f-153">A multiline SSH key must begin with `---- BEGIN SSH2 PUBLIC KEY ----` and end with `---- END SSH2 PUBLIC KEY ----`.</span></span>

## <a name="obtaining-superuser-privileges"></a><span data-ttu-id="6c75f-154">Obtaining superuser privileges</span><span class="sxs-lookup"><span data-stu-id="6c75f-154">Obtaining superuser privileges</span></span>
<span data-ttu-id="6c75f-155">The user account that is specified during virtual machine instance deployment on Azure is a privileged account.</span><span class="sxs-lookup"><span data-stu-id="6c75f-155">The user account that is specified during virtual machine instance deployment on Azure is a privileged account.</span></span> <span data-ttu-id="6c75f-156">The package of sudo was installed in the published FreeBSD image.</span><span class="sxs-lookup"><span data-stu-id="6c75f-156">The package of sudo was installed in the published FreeBSD image.</span></span>
<span data-ttu-id="6c75f-157">After you're logged in through this user account, you can run commands as root by using the command syntax.</span><span class="sxs-lookup"><span data-stu-id="6c75f-157">After you're logged in through this user account, you can run commands as root by using the command syntax.</span></span>

```
    $ sudo <COMMAND>
```

<span data-ttu-id="6c75f-158">You can optionally obtain a root shell by using `sudo -s`.</span><span class="sxs-lookup"><span data-stu-id="6c75f-158">You can optionally obtain a root shell by using `sudo -s`.</span></span>

## <a name="known-issues"></a><span data-ttu-id="6c75f-159">Known issues</span><span class="sxs-lookup"><span data-stu-id="6c75f-159">Known issues</span></span>
<span data-ttu-id="6c75f-160">The [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.2 has a [known issue] (https://github.com/Azure/WALinuxAgent/pull/517) that causes the provision failure for FreeBSD VM on Azure.</span><span class="sxs-lookup"><span data-stu-id="6c75f-160">The [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.2 has a [known issue] (https://github.com/Azure/WALinuxAgent/pull/517) that causes the provision failure for FreeBSD VM on Azure.</span></span> <span data-ttu-id="6c75f-161">The fix was captured by [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.3 and later releases.</span><span class="sxs-lookup"><span data-stu-id="6c75f-161">The fix was captured by [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.3 and later releases.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6c75f-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="6c75f-162">Next steps</span></span>
* <span data-ttu-id="6c75f-163">Go to [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) to create a FreeBSD VM.</span><span class="sxs-lookup"><span data-stu-id="6c75f-163">Go to [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) to create a FreeBSD VM.</span></span>
* <span data-ttu-id="6c75f-164">If you want to bring your own FreeBSD to Azure, refer to [Create and upload a FreeBSD VHD to Azure](linux/classic/freebsd-create-upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="6c75f-164">If you want to bring your own FreeBSD to Azure, refer to [Create and upload a FreeBSD VHD to Azure](linux/classic/freebsd-create-upload-vhd.md).</span></span>
