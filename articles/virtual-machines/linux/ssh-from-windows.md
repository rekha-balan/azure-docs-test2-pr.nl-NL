---
title: Use SSH keys with Windows for Linux VMs | Microsoft Docs
description: Learn how to generate and use SSH keys on a Windows computer to connect to a Linux virtual machine on Azure.
services: virtual-machines-linux
documentationcenter: ''
author: squillace
manager: timlt
editor: ''
tags: azure-service-management,azure-resource-manager
ms.assetid: 2cacda3b-7949-4036-bd5d-837e8b09a9c8
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: rasquill
ms.openlocfilehash: 809d64863808d96aeff7edb6337ac12dc1dbebfc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549244"
---
# <a name="how-to-use-ssh-keys-with-windows-on-azure"></a><span data-ttu-id="ef04c-103">How to Use SSH keys with Windows on Azure</span><span class="sxs-lookup"><span data-stu-id="ef04c-103">How to Use SSH keys with Windows on Azure</span></span>
> [!div class="op_single_selector"]
> * [Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> * [Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
>
>

<span data-ttu-id="ef04c-106">When you connect to Linux virtual machines (VMs) in Azure, you should use [public-key cryptography](https://wikipedia.org/wiki/Public-key_cryptography) to provide a more secure way to log in to your Linux VM.</span><span class="sxs-lookup"><span data-stu-id="ef04c-106">When you connect to Linux virtual machines (VMs) in Azure, you should use [public-key cryptography](https://wikipedia.org/wiki/Public-key_cryptography) to provide a more secure way to log in to your Linux VM.</span></span> <span data-ttu-id="ef04c-107">This process involves a public and private key exchange using the secure shell (SSH) command to authenticate yourself rather than a username and password.</span><span class="sxs-lookup"><span data-stu-id="ef04c-107">This process involves a public and private key exchange using the secure shell (SSH) command to authenticate yourself rather than a username and password.</span></span> <span data-ttu-id="ef04c-108">Passwords are vulnerable to brute-force attacks, especially on Internet-facing VMs such as web servers.</span><span class="sxs-lookup"><span data-stu-id="ef04c-108">Passwords are vulnerable to brute-force attacks, especially on Internet-facing VMs such as web servers.</span></span> <span data-ttu-id="ef04c-109">This article provides an overview of SSH keys and how to generate the appropriate keys on a Windows computer.</span><span class="sxs-lookup"><span data-stu-id="ef04c-109">This article provides an overview of SSH keys and how to generate the appropriate keys on a Windows computer.</span></span>

## <a name="overview-of-ssh-and-keys"></a><span data-ttu-id="ef04c-110">Overview of SSH and keys</span><span class="sxs-lookup"><span data-stu-id="ef04c-110">Overview of SSH and keys</span></span>
<span data-ttu-id="ef04c-111">You can securely log in to your Linux VM by using public and private keys:</span><span class="sxs-lookup"><span data-stu-id="ef04c-111">You can securely log in to your Linux VM by using public and private keys:</span></span>

* <span data-ttu-id="ef04c-112">The **public key** is placed on your Linux VM, or any other service that you wish to use with public-key cryptography.</span><span class="sxs-lookup"><span data-stu-id="ef04c-112">The **public key** is placed on your Linux VM, or any other service that you wish to use with public-key cryptography.</span></span>
* <span data-ttu-id="ef04c-113">The **private key** is what you present to your Linux VM when you log in, to verify your identity.</span><span class="sxs-lookup"><span data-stu-id="ef04c-113">The **private key** is what you present to your Linux VM when you log in, to verify your identity.</span></span> <span data-ttu-id="ef04c-114">Protect this private key.</span><span class="sxs-lookup"><span data-stu-id="ef04c-114">Protect this private key.</span></span> <span data-ttu-id="ef04c-115">Do not share it.</span><span class="sxs-lookup"><span data-stu-id="ef04c-115">Do not share it.</span></span>

<span data-ttu-id="ef04c-116">These public and private keys can be used on multiple VMs and services.</span><span class="sxs-lookup"><span data-stu-id="ef04c-116">These public and private keys can be used on multiple VMs and services.</span></span> <span data-ttu-id="ef04c-117">You do not need a pair of keys for each VM or service you wish to access.</span><span class="sxs-lookup"><span data-stu-id="ef04c-117">You do not need a pair of keys for each VM or service you wish to access.</span></span> <span data-ttu-id="ef04c-118">For a more detailed overview, see [public-key cryptography](https://wikipedia.org/wiki/Public-key_cryptography).</span><span class="sxs-lookup"><span data-stu-id="ef04c-118">For a more detailed overview, see [public-key cryptography](https://wikipedia.org/wiki/Public-key_cryptography).</span></span>

<span data-ttu-id="ef04c-119">SSH is an encrypted connection protocol that allows secure logins over unsecured connections.</span><span class="sxs-lookup"><span data-stu-id="ef04c-119">SSH is an encrypted connection protocol that allows secure logins over unsecured connections.</span></span> <span data-ttu-id="ef04c-120">It is the default connection protocol for Linux VMs hosted in Azure.</span><span class="sxs-lookup"><span data-stu-id="ef04c-120">It is the default connection protocol for Linux VMs hosted in Azure.</span></span> <span data-ttu-id="ef04c-121">Although SSH itself provides an encrypted connection, using passwords with SSH connections still leaves the VM vulnerable to brute-force attacks or guessing of passwords.</span><span class="sxs-lookup"><span data-stu-id="ef04c-121">Although SSH itself provides an encrypted connection, using passwords with SSH connections still leaves the VM vulnerable to brute-force attacks or guessing of passwords.</span></span> <span data-ttu-id="ef04c-122">A more secure and preferred method of connecting to a VM using SSH is by using these public and private keys, also known as SSH keys.</span><span class="sxs-lookup"><span data-stu-id="ef04c-122">A more secure and preferred method of connecting to a VM using SSH is by using these public and private keys, also known as SSH keys.</span></span>

<span data-ttu-id="ef04c-123">If you do not wish to use SSH keys, you can still log in to your Linux VMs using a password.</span><span class="sxs-lookup"><span data-stu-id="ef04c-123">If you do not wish to use SSH keys, you can still log in to your Linux VMs using a password.</span></span> <span data-ttu-id="ef04c-124">If your VM is not exposed to the Internet, using passwords may be sufficient.</span><span class="sxs-lookup"><span data-stu-id="ef04c-124">If your VM is not exposed to the Internet, using passwords may be sufficient.</span></span> <span data-ttu-id="ef04c-125">However, you still need to manage your passwords for each Linux VM and maintain healthy password policies and practices, such as minimum password length and regularly updating them.</span><span class="sxs-lookup"><span data-stu-id="ef04c-125">However, you still need to manage your passwords for each Linux VM and maintain healthy password policies and practices, such as minimum password length and regularly updating them.</span></span> <span data-ttu-id="ef04c-126">The use of SSH keys reduces the complexity of managing individual credentials across multiple VMs.</span><span class="sxs-lookup"><span data-stu-id="ef04c-126">The use of SSH keys reduces the complexity of managing individual credentials across multiple VMs.</span></span>

## <a name="windows-packages-and-ssh-clients"></a><span data-ttu-id="ef04c-127">Windows packages and SSH clients</span><span class="sxs-lookup"><span data-stu-id="ef04c-127">Windows packages and SSH clients</span></span>
<span data-ttu-id="ef04c-128">You connect to and manage Linux VMs in Azure using an **SSH client**.</span><span class="sxs-lookup"><span data-stu-id="ef04c-128">You connect to and manage Linux VMs in Azure using an **SSH client**.</span></span> <span data-ttu-id="ef04c-129">Windows computers do not typically have an SSH client installed.</span><span class="sxs-lookup"><span data-stu-id="ef04c-129">Windows computers do not typically have an SSH client installed.</span></span> <span data-ttu-id="ef04c-130">Common Windows SSH clients you can install are included in the following packages:</span><span class="sxs-lookup"><span data-stu-id="ef04c-130">Common Windows SSH clients you can install are included in the following packages:</span></span>

* [<span data-ttu-id="ef04c-131">Git For Windows</span><span class="sxs-lookup"><span data-stu-id="ef04c-131">Git For Windows</span></span>](https://git-for-windows.github.io/)
* [<span data-ttu-id="ef04c-132">puTTY</span><span class="sxs-lookup"><span data-stu-id="ef04c-132">puTTY</span></span>](http://www.chiark.greenend.org.uk/~sgtatham/putty/)
* [<span data-ttu-id="ef04c-133">MobaXterm</span><span class="sxs-lookup"><span data-stu-id="ef04c-133">MobaXterm</span></span>](http://mobaxterm.mobatek.net/)
* [<span data-ttu-id="ef04c-134">Cygwin</span><span class="sxs-lookup"><span data-stu-id="ef04c-134">Cygwin</span></span>](https://cygwin.com/)

> [!NOTE]
> The latest Windows 10 Anniversary Update includes Bash for Windows. This feature allows you to run the Windows Subsystem for Linux and access utilities such as an SSH client. Bash for Windows is still under development, and is considered a beta release. For more information about Bash for Windows, see [Bash on Ubuntu on Windows](https://msdn.microsoft.com/commandline/wsl/about).
>
>

## <a name="which-key-files-do-you-need-to-create"></a><span data-ttu-id="ef04c-139">Which key files do you need to create?</span><span class="sxs-lookup"><span data-stu-id="ef04c-139">Which key files do you need to create?</span></span>
<span data-ttu-id="ef04c-140">Azure requires at least 2048-bit, **ssh-rsa** formatted public and private keys.</span><span class="sxs-lookup"><span data-stu-id="ef04c-140">Azure requires at least 2048-bit, **ssh-rsa** formatted public and private keys.</span></span> <span data-ttu-id="ef04c-141">If you are managing Azure resources using the Classic deployment model, you also need to generate a PEM (`.pem` file).</span><span class="sxs-lookup"><span data-stu-id="ef04c-141">If you are managing Azure resources using the Classic deployment model, you also need to generate a PEM (`.pem` file).</span></span>

<span data-ttu-id="ef04c-142">Here are the deployment scenarios, and the types of files you use in each:</span><span class="sxs-lookup"><span data-stu-id="ef04c-142">Here are the deployment scenarios, and the types of files you use in each:</span></span>

1. <span data-ttu-id="ef04c-143">**ssh-rsa** keys are required for any deployment using the [Azure portal](https://portal.azure.com), and Resource Manager deployments using the [Azure CLI](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="ef04c-143">**ssh-rsa** keys are required for any deployment using the [Azure portal](https://portal.azure.com), and Resource Manager deployments using the [Azure CLI](../../cli-install-nodejs.md).</span></span>
   * <span data-ttu-id="ef04c-144">These keys are usually all most people need.</span><span class="sxs-lookup"><span data-stu-id="ef04c-144">These keys are usually all most people need.</span></span>
2. <span data-ttu-id="ef04c-145">A `.pem` file is required to create VMs using the Classic deployment.</span><span class="sxs-lookup"><span data-stu-id="ef04c-145">A `.pem` file is required to create VMs using the Classic deployment.</span></span> <span data-ttu-id="ef04c-146">These keys are supported in Classic deployments when using the [Azure portal](https://portal.azure.com) or [Azure CLI](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="ef04c-146">These keys are supported in Classic deployments when using the [Azure portal](https://portal.azure.com) or [Azure CLI](../../cli-install-nodejs.md).</span></span>
   * <span data-ttu-id="ef04c-147">You only need to create these additional keys and certificates if you are managing resources created using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="ef04c-147">You only need to create these additional keys and certificates if you are managing resources created using the Classic deployment model.</span></span>

## <a name="install-git-for-windows"></a><span data-ttu-id="ef04c-148">Install Git for Windows</span><span class="sxs-lookup"><span data-stu-id="ef04c-148">Install Git for Windows</span></span>
<span data-ttu-id="ef04c-149">The preceding section listed several packages that include the `openssl` tool for Windows.</span><span class="sxs-lookup"><span data-stu-id="ef04c-149">The preceding section listed several packages that include the `openssl` tool for Windows.</span></span> <span data-ttu-id="ef04c-150">This tool is needed to create public and private keys.</span><span class="sxs-lookup"><span data-stu-id="ef04c-150">This tool is needed to create public and private keys.</span></span> <span data-ttu-id="ef04c-151">The following examples detail how to install and use **Git for Windows**, though you can choose whichever package you prefer.</span><span class="sxs-lookup"><span data-stu-id="ef04c-151">The following examples detail how to install and use **Git for Windows**, though you can choose whichever package you prefer.</span></span> <span data-ttu-id="ef04c-152">**Git for Windows** gives you access to some additional open-source software ([OSS](https://en.wikipedia.org/wiki/Open-source_software)) tools and utilities that may be useful as you work with Linux VMs.</span><span class="sxs-lookup"><span data-stu-id="ef04c-152">**Git for Windows** gives you access to some additional open-source software ([OSS](https://en.wikipedia.org/wiki/Open-source_software)) tools and utilities that may be useful as you work with Linux VMs.</span></span>

1. <span data-ttu-id="ef04c-153">Download and install **Git for Windows** from the following location: [https://git-for-windows.github.io/](https://git-for-windows.github.io/).</span><span class="sxs-lookup"><span data-stu-id="ef04c-153">Download and install **Git for Windows** from the following location: [https://git-for-windows.github.io/](https://git-for-windows.github.io/).</span></span>
2. <span data-ttu-id="ef04c-154">Accept the default options during the install process unless you specifically need to change them.</span><span class="sxs-lookup"><span data-stu-id="ef04c-154">Accept the default options during the install process unless you specifically need to change them.</span></span>
3. <span data-ttu-id="ef04c-155">Run **Git Bash** from the **Start Menu** > **Git** > **Git Bash**.</span><span class="sxs-lookup"><span data-stu-id="ef04c-155">Run **Git Bash** from the **Start Menu** > **Git** > **Git Bash**.</span></span> <span data-ttu-id="ef04c-156">The console looks similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="ef04c-156">The console looks similar to the following example:</span></span>

    ![Git for Windows Bash shell](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/ssh-from-windows/git-bash-window.png)

## <a name="create-a-private-key"></a><span data-ttu-id="ef04c-158">Create a private key</span><span class="sxs-lookup"><span data-stu-id="ef04c-158">Create a private key</span></span>
1. <span data-ttu-id="ef04c-159">In your **Git Bash** window, use `openssl.exe` to create a private key.</span><span class="sxs-lookup"><span data-stu-id="ef04c-159">In your **Git Bash** window, use `openssl.exe` to create a private key.</span></span> <span data-ttu-id="ef04c-160">The following example creates a key named `myPrivateKey` and certificate named `myCert.pem`:</span><span class="sxs-lookup"><span data-stu-id="ef04c-160">The following example creates a key named `myPrivateKey` and certificate named `myCert.pem`:</span></span>

    ```bash
    openssl.exe req -x509 -nodes -days 365 -newkey rsa:2048 \
        -keyout myPrivateKey.key -out myCert.pem
    ```

    <span data-ttu-id="ef04c-161">The output looks similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="ef04c-161">The output looks similar to the following example:</span></span>

    ```bash
    Generating a 2048 bit RSA private key
    .......................................+++
    .......................+++
    writing new private key to 'myPrivateKey.key'
    -----
    You are about to be asked to enter information that will be incorporated
    into your certificate request.
    What you are about to enter is what is called a Distinguished Name or a DN.
    There are quite a few fields but you can leave some blank
    For some fields there will be a default value,
    If you enter '.', the field will be left blank.
    -----
    Country Name (2 letter code) [AU]:
    ```

   <span data-ttu-id="ef04c-162">If bash reports an error, try opening a new **Git Bash** window with elevated privileges.</span><span class="sxs-lookup"><span data-stu-id="ef04c-162">If bash reports an error, try opening a new **Git Bash** window with elevated privileges.</span></span> <span data-ttu-id="ef04c-163">Then, rerun the `openssl` command.</span><span class="sxs-lookup"><span data-stu-id="ef04c-163">Then, rerun the `openssl` command.</span></span>

2. <span data-ttu-id="ef04c-164">Answer the prompts for country name, location, organization name, etc.</span><span class="sxs-lookup"><span data-stu-id="ef04c-164">Answer the prompts for country name, location, organization name, etc.</span></span>
3. <span data-ttu-id="ef04c-165">Your new private key and certificate are created in your current working directory.</span><span class="sxs-lookup"><span data-stu-id="ef04c-165">Your new private key and certificate are created in your current working directory.</span></span> <span data-ttu-id="ef04c-166">As a security measure, you should set the permissions on your private key so that only you can access it:</span><span class="sxs-lookup"><span data-stu-id="ef04c-166">As a security measure, you should set the permissions on your private key so that only you can access it:</span></span>

    ```bash
    chmod 0600 myPrivateKey.key
    ```

4. <span data-ttu-id="ef04c-167">The [next section](#create-a-private-key-for-putty) details using PuTTYgen to both view and use the public key, and create a private key specific for using PuTTY to SSH to Linux VMs.</span><span class="sxs-lookup"><span data-stu-id="ef04c-167">The [next section](#create-a-private-key-for-putty) details using PuTTYgen to both view and use the public key, and create a private key specific for using PuTTY to SSH to Linux VMs.</span></span> <span data-ttu-id="ef04c-168">The following command generates a public key file named `myPublicKey.key` that you can use right away:</span><span class="sxs-lookup"><span data-stu-id="ef04c-168">The following command generates a public key file named `myPublicKey.key` that you can use right away:</span></span>

    ```bash
    openssl.exe rsa -pubout -in myPrivateKey.key -out myPublicKey.key
    ```

5. <span data-ttu-id="ef04c-169">If you also need to manage Classic resources, convert the `myCert.pem` to `myCert.cer` (DER encoded X509 certificate).</span><span class="sxs-lookup"><span data-stu-id="ef04c-169">If you also need to manage Classic resources, convert the `myCert.pem` to `myCert.cer` (DER encoded X509 certificate).</span></span> <span data-ttu-id="ef04c-170">Perform this optional step only if you need to specifically manage older Classic resources.</span><span class="sxs-lookup"><span data-stu-id="ef04c-170">Perform this optional step only if you need to specifically manage older Classic resources.</span></span>

    <span data-ttu-id="ef04c-171">Convert the certificate using the following command:</span><span class="sxs-lookup"><span data-stu-id="ef04c-171">Convert the certificate using the following command:</span></span>

    ```bash
    openssl.exe  x509 -outform der -in myCert.pem -out myCert.cer
    ```

## <a name="create-a-private-key-for-putty"></a><span data-ttu-id="ef04c-172">Create a private key for PuTTY</span><span class="sxs-lookup"><span data-stu-id="ef04c-172">Create a private key for PuTTY</span></span>
<span data-ttu-id="ef04c-173">PuTTY is a common SSH client for Windows.</span><span class="sxs-lookup"><span data-stu-id="ef04c-173">PuTTY is a common SSH client for Windows.</span></span> <span data-ttu-id="ef04c-174">You are free to use any SSH client that you wish.</span><span class="sxs-lookup"><span data-stu-id="ef04c-174">You are free to use any SSH client that you wish.</span></span> <span data-ttu-id="ef04c-175">To use PuTTY, you need to create an additional type of key - a PuTTY Private Key (PPK).</span><span class="sxs-lookup"><span data-stu-id="ef04c-175">To use PuTTY, you need to create an additional type of key - a PuTTY Private Key (PPK).</span></span> <span data-ttu-id="ef04c-176">If you do not wish to use PuTTY, skip this section.</span><span class="sxs-lookup"><span data-stu-id="ef04c-176">If you do not wish to use PuTTY, skip this section.</span></span>

<span data-ttu-id="ef04c-177">The following example creates this additional private key specifically for PuTTY to use:</span><span class="sxs-lookup"><span data-stu-id="ef04c-177">The following example creates this additional private key specifically for PuTTY to use:</span></span>

1. <span data-ttu-id="ef04c-178">Use **Git Bash** to convert your private key into an RSA private key that PuTTYgen can understand.</span><span class="sxs-lookup"><span data-stu-id="ef04c-178">Use **Git Bash** to convert your private key into an RSA private key that PuTTYgen can understand.</span></span> <span data-ttu-id="ef04c-179">The following example creates a key named `myPrivateKey_rsa` from the existing key named `myPrivateKey`:</span><span class="sxs-lookup"><span data-stu-id="ef04c-179">The following example creates a key named `myPrivateKey_rsa` from the existing key named `myPrivateKey`:</span></span>

    ```bash
    openssl rsa -in ./myPrivateKey.key -out myPrivateKey_rsa
    ```

    <span data-ttu-id="ef04c-180">As a security measure, you should set the permissions on your private key so that only you can access it:</span><span class="sxs-lookup"><span data-stu-id="ef04c-180">As a security measure, you should set the permissions on your private key so that only you can access it:</span></span>

    ```bash
    chmod 0600 myPrivateKey_rsa
    ```
2. <span data-ttu-id="ef04c-181">Download and run PuTTYgen from the following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span><span class="sxs-lookup"><span data-stu-id="ef04c-181">Download and run PuTTYgen from the following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span></span>
3. <span data-ttu-id="ef04c-182">Click the menu: **File** > **Load Private Key**</span><span class="sxs-lookup"><span data-stu-id="ef04c-182">Click the menu: **File** > **Load Private Key**</span></span>
4. <span data-ttu-id="ef04c-183">Locate your private key (`myPrivateKey_rsa` in the previous example).</span><span class="sxs-lookup"><span data-stu-id="ef04c-183">Locate your private key (`myPrivateKey_rsa` in the previous example).</span></span> <span data-ttu-id="ef04c-184">The default directory when you start **Git Bash** is `C:\Users\%username%`.</span><span class="sxs-lookup"><span data-stu-id="ef04c-184">The default directory when you start **Git Bash** is `C:\Users\%username%`.</span></span> <span data-ttu-id="ef04c-185">Change the file filter to show **All Files (\*.\*)**:</span><span class="sxs-lookup"><span data-stu-id="ef04c-185">Change the file filter to show **All Files (\*.\*)**:</span></span>

    ![Load the existing private key into PuTTYgen](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/ssh-from-windows/load-private-key.png)
5. <span data-ttu-id="ef04c-187">Click **Open**.</span><span class="sxs-lookup"><span data-stu-id="ef04c-187">Click **Open**.</span></span> <span data-ttu-id="ef04c-188">A prompt indicates that the key has been successfully imported:</span><span class="sxs-lookup"><span data-stu-id="ef04c-188">A prompt indicates that the key has been successfully imported:</span></span>

    ![Successfully imported key to PuTTYgen](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/ssh-from-windows/successfully-imported-key.png)
6. <span data-ttu-id="ef04c-190">Click **OK** to close the prompt.</span><span class="sxs-lookup"><span data-stu-id="ef04c-190">Click **OK** to close the prompt.</span></span>
7. <span data-ttu-id="ef04c-191">The public key is displayed at the top of the **PuTTYgen** window.</span><span class="sxs-lookup"><span data-stu-id="ef04c-191">The public key is displayed at the top of the **PuTTYgen** window.</span></span> <span data-ttu-id="ef04c-192">You copy and paste this public key into the Azure portal or Azure Resource Manager template when you create a Linux VM.</span><span class="sxs-lookup"><span data-stu-id="ef04c-192">You copy and paste this public key into the Azure portal or Azure Resource Manager template when you create a Linux VM.</span></span> <span data-ttu-id="ef04c-193">You can also click **Save public key** to save a copy to your computer:</span><span class="sxs-lookup"><span data-stu-id="ef04c-193">You can also click **Save public key** to save a copy to your computer:</span></span>

    ![Save PuTTY public key file](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/ssh-from-windows/save-public-key.png)

    <span data-ttu-id="ef04c-195">The following example shows how you would copy and paste this public key into the Azure portal when you create a Linux VM.</span><span class="sxs-lookup"><span data-stu-id="ef04c-195">The following example shows how you would copy and paste this public key into the Azure portal when you create a Linux VM.</span></span> <span data-ttu-id="ef04c-196">The public key is typically then stored in `~/.ssh/authorized_keys` on your new VM.</span><span class="sxs-lookup"><span data-stu-id="ef04c-196">The public key is typically then stored in `~/.ssh/authorized_keys` on your new VM.</span></span>

    ![Use public key when you create a VM in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/ssh-from-windows/use-public-key-azure-portal.png)
8. <span data-ttu-id="ef04c-198">Back in **PuTTYgen**, Click **Save private Key**:</span><span class="sxs-lookup"><span data-stu-id="ef04c-198">Back in **PuTTYgen**, Click **Save private Key**:</span></span>

    ![Save PuTTY Private Key file](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/ssh-from-windows/save-ppk-file.png)

   > [!WARNING]
   > A prompt asks if you wish to continue without entering a passphrase for your key. A passphrase is like a password attached to your private key. Even if someone were to obtain your private key, they still would not be able to authenticate using just the key. They would also need the passphrase. Without a passphrase, if someone obtains your private key, they can log in to any VM or service that uses that key. We recommend you create a passphrase. However, if you forget the passphrase, there is no way to recover it.
   >
   >

    <span data-ttu-id="ef04c-207">If you wish to enter a passphrase, click **No**, enter a passphrase in the main PuTTYgen window, and then click **Save private key** again.</span><span class="sxs-lookup"><span data-stu-id="ef04c-207">If you wish to enter a passphrase, click **No**, enter a passphrase in the main PuTTYgen window, and then click **Save private key** again.</span></span> <span data-ttu-id="ef04c-208">Otherwise, click **Yes** to continue without providing the optional passphrase.</span><span class="sxs-lookup"><span data-stu-id="ef04c-208">Otherwise, click **Yes** to continue without providing the optional passphrase.</span></span>
9. <span data-ttu-id="ef04c-209">Enter a name and location to save your PPK file.</span><span class="sxs-lookup"><span data-stu-id="ef04c-209">Enter a name and location to save your PPK file.</span></span>

## <a name="use-putty-to-ssh-to-a-linux-machine"></a><span data-ttu-id="ef04c-210">Use Putty to SSH to a Linux Machine</span><span class="sxs-lookup"><span data-stu-id="ef04c-210">Use Putty to SSH to a Linux Machine</span></span>
<span data-ttu-id="ef04c-211">Again, PuTTY is a common SSH client for Windows.</span><span class="sxs-lookup"><span data-stu-id="ef04c-211">Again, PuTTY is a common SSH client for Windows.</span></span> <span data-ttu-id="ef04c-212">You are free to use any SSH client that you wish.</span><span class="sxs-lookup"><span data-stu-id="ef04c-212">You are free to use any SSH client that you wish.</span></span> <span data-ttu-id="ef04c-213">The following steps detail how to use your private key to authenticate with your Azure VM using SSH.</span><span class="sxs-lookup"><span data-stu-id="ef04c-213">The following steps detail how to use your private key to authenticate with your Azure VM using SSH.</span></span> <span data-ttu-id="ef04c-214">The steps are similar in other SSH key clients in terms of needing to load your private key to authenticate the SSH connection.</span><span class="sxs-lookup"><span data-stu-id="ef04c-214">The steps are similar in other SSH key clients in terms of needing to load your private key to authenticate the SSH connection.</span></span>

1. <span data-ttu-id="ef04c-215">Download and run putty from the following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span><span class="sxs-lookup"><span data-stu-id="ef04c-215">Download and run putty from the following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span></span>
2. <span data-ttu-id="ef04c-216">Fill in the host name or IP address of your VM from the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="ef04c-216">Fill in the host name or IP address of your VM from the Azure portal:</span></span>

    ![Open new PuTTY connection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/ssh-from-windows/putty-new-connection.png)
3. <span data-ttu-id="ef04c-218">Before selecting **Open**, click **Connection** > **SSH** > **Auth** tab. Browse to and select your private key:</span><span class="sxs-lookup"><span data-stu-id="ef04c-218">Before selecting **Open**, click **Connection** > **SSH** > **Auth** tab. Browse to and select your private key:</span></span>

    ![Select your PuTTY Private Key for authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/ssh-from-windows/putty-auth-dialog.png)
4. <span data-ttu-id="ef04c-220">Click **Open** to connect to your virtual machine</span><span class="sxs-lookup"><span data-stu-id="ef04c-220">Click **Open** to connect to your virtual machine</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef04c-221">Next steps</span><span class="sxs-lookup"><span data-stu-id="ef04c-221">Next steps</span></span>
<span data-ttu-id="ef04c-222">You can also generate the public and private keys [using OS X and Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ef04c-222">You can also generate the public and private keys [using OS X and Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="ef04c-223">For more information about Bash for Windows and the benefits of having OSS tools readily available on your Windows computer, see [Bash on Ubuntu on Windows](https://msdn.microsoft.com/commandline/wsl/about).</span><span class="sxs-lookup"><span data-stu-id="ef04c-223">For more information about Bash for Windows and the benefits of having OSS tools readily available on your Windows computer, see [Bash on Ubuntu on Windows](https://msdn.microsoft.com/commandline/wsl/about).</span></span>

<span data-ttu-id="ef04c-224">If you have trouble using SSH to connect to your Linux VMs, see [Troubleshoot SSH connections to an Azure Linux VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ef04c-224">If you have trouble using SSH to connect to your Linux VMs, see [Troubleshoot SSH connections to an Azure Linux VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>








