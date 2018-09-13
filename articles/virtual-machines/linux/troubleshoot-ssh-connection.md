---
title: Troubleshoot SSH connection issues to an Azure VM | Microsoft Docs
description: How to troubleshoot issues such as 'SSH connection failed' or 'SSH connection refused' for an Azure VM running Linux.
keywords: ssh connection refused, ssh error, azure ssh, SSH connection failed
services: virtual-machines-linux
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: dcb82e19-29b2-47bb-99f2-900d4cfb5bbb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: iainfou
ms.openlocfilehash: d9dff9f1af37b3f7ba453218993d9dab3deb7a2c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548884"
---
# <a name="troubleshoot-ssh-connections-to-an-azure-linux-vm-that-fails-errors-out-or-is-refused"></a><span data-ttu-id="2052b-104">Troubleshoot SSH connections to an Azure Linux VM that fails, errors out, or is refused</span><span class="sxs-lookup"><span data-stu-id="2052b-104">Troubleshoot SSH connections to an Azure Linux VM that fails, errors out, or is refused</span></span>
<span data-ttu-id="2052b-105">There are various reasons that you encounter Secure Shell (SSH) errors, SSH connection failures, or SSH is refused when you try to connect to a Linux virtual machine (VM).</span><span class="sxs-lookup"><span data-stu-id="2052b-105">There are various reasons that you encounter Secure Shell (SSH) errors, SSH connection failures, or SSH is refused when you try to connect to a Linux virtual machine (VM).</span></span> <span data-ttu-id="2052b-106">This article helps you find and correct the problems.</span><span class="sxs-lookup"><span data-stu-id="2052b-106">This article helps you find and correct the problems.</span></span> <span data-ttu-id="2052b-107">You can use the Azure portal, Azure CLI, or VM Access Extension for Linux to troubleshoot and resolve connection problems.</span><span class="sxs-lookup"><span data-stu-id="2052b-107">You can use the Azure portal, Azure CLI, or VM Access Extension for Linux to troubleshoot and resolve connection problems.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="2052b-108">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](http://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="2052b-108">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](http://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="2052b-109">Alternatively, you can file an Azure support incident.</span><span class="sxs-lookup"><span data-stu-id="2052b-109">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="2052b-110">Go to the [Azure support site](http://azure.microsoft.com/support/options/) and select **Get support**.</span><span class="sxs-lookup"><span data-stu-id="2052b-110">Go to the [Azure support site](http://azure.microsoft.com/support/options/) and select **Get support**.</span></span> <span data-ttu-id="2052b-111">For information about using Azure Support, read the [Microsoft Azure support FAQ](http://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="2052b-111">For information about using Azure Support, read the [Microsoft Azure support FAQ](http://azure.microsoft.com/support/faq/).</span></span>

## <a name="quick-troubleshooting-steps"></a><span data-ttu-id="2052b-112">Quick troubleshooting steps</span><span class="sxs-lookup"><span data-stu-id="2052b-112">Quick troubleshooting steps</span></span>
<span data-ttu-id="2052b-113">After each troubleshooting step, try reconnecting to the VM.</span><span class="sxs-lookup"><span data-stu-id="2052b-113">After each troubleshooting step, try reconnecting to the VM.</span></span>

1. <span data-ttu-id="2052b-114">Reset the SSH configuration.</span><span class="sxs-lookup"><span data-stu-id="2052b-114">Reset the SSH configuration.</span></span>
2. <span data-ttu-id="2052b-115">Reset the credentials for the user.</span><span class="sxs-lookup"><span data-stu-id="2052b-115">Reset the credentials for the user.</span></span>
3. <span data-ttu-id="2052b-116">Verify the [Network Security Group](../../virtual-network/virtual-networks-nsg.md) rules permit SSH traffic.</span><span class="sxs-lookup"><span data-stu-id="2052b-116">Verify the [Network Security Group](../../virtual-network/virtual-networks-nsg.md) rules permit SSH traffic.</span></span>
   * <span data-ttu-id="2052b-117">Ensure that a Network Security Group rule exists to permit SSH traffic (by default, TCP port 22).</span><span class="sxs-lookup"><span data-stu-id="2052b-117">Ensure that a Network Security Group rule exists to permit SSH traffic (by default, TCP port 22).</span></span>
   * <span data-ttu-id="2052b-118">You cannot use port redirection / mapping without using an Azure load balancer.</span><span class="sxs-lookup"><span data-stu-id="2052b-118">You cannot use port redirection / mapping without using an Azure load balancer.</span></span>
4. <span data-ttu-id="2052b-119">Check the [VM resource health](../../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2052b-119">Check the [VM resource health](../../resource-health/resource-health-overview.md).</span></span> 
   * <span data-ttu-id="2052b-120">Ensure that the VM reports as being healthy.</span><span class="sxs-lookup"><span data-stu-id="2052b-120">Ensure that the VM reports as being healthy.</span></span>
   * <span data-ttu-id="2052b-121">If you have boot diagnostics enabled, verify the VM is not reporting boot errors in the logs.</span><span class="sxs-lookup"><span data-stu-id="2052b-121">If you have boot diagnostics enabled, verify the VM is not reporting boot errors in the logs.</span></span>
5. <span data-ttu-id="2052b-122">Restart the VM.</span><span class="sxs-lookup"><span data-stu-id="2052b-122">Restart the VM.</span></span>
6. <span data-ttu-id="2052b-123">Redeploy the VM.</span><span class="sxs-lookup"><span data-stu-id="2052b-123">Redeploy the VM.</span></span>

<span data-ttu-id="2052b-124">Continue reading for more detailed troubleshooting steps and explanations.</span><span class="sxs-lookup"><span data-stu-id="2052b-124">Continue reading for more detailed troubleshooting steps and explanations.</span></span>

## <a name="available-methods-to-troubleshoot-ssh-connection-issues"></a><span data-ttu-id="2052b-125">Available methods to troubleshoot SSH connection issues</span><span class="sxs-lookup"><span data-stu-id="2052b-125">Available methods to troubleshoot SSH connection issues</span></span>
<span data-ttu-id="2052b-126">You can reset credentials or SSH configuration using one of the following methods:</span><span class="sxs-lookup"><span data-stu-id="2052b-126">You can reset credentials or SSH configuration using one of the following methods:</span></span>

* <span data-ttu-id="2052b-127">[Azure portal](#use-the-azure-portal) - great if you need to quickly reset the SSH configuration or SSH key and you don't have the Azure tools installed.</span><span class="sxs-lookup"><span data-stu-id="2052b-127">[Azure portal](#use-the-azure-portal) - great if you need to quickly reset the SSH configuration or SSH key and you don't have the Azure tools installed.</span></span>
* <span data-ttu-id="2052b-128">[Azure CLI 2.0](#use-the-azure-cli-20) - if you are already on the command line, quickly reset the SSH configuration or credentials.</span><span class="sxs-lookup"><span data-stu-id="2052b-128">[Azure CLI 2.0](#use-the-azure-cli-20) - if you are already on the command line, quickly reset the SSH configuration or credentials.</span></span> <span data-ttu-id="2052b-129">You can also use the [Azure CLI 1.0](#use-the-azure-cli-10)</span><span class="sxs-lookup"><span data-stu-id="2052b-129">You can also use the [Azure CLI 1.0](#use-the-azure-cli-10)</span></span>
* <span data-ttu-id="2052b-130">[Azure VMAccessForLinux extension](#use-the-vmaccess-extension) - create and reuse json definition files to reset the SSH configuration or user credentials.</span><span class="sxs-lookup"><span data-stu-id="2052b-130">[Azure VMAccessForLinux extension](#use-the-vmaccess-extension) - create and reuse json definition files to reset the SSH configuration or user credentials.</span></span>

<span data-ttu-id="2052b-131">After each troubleshooting step, try connecting to your VM again.</span><span class="sxs-lookup"><span data-stu-id="2052b-131">After each troubleshooting step, try connecting to your VM again.</span></span> <span data-ttu-id="2052b-132">If you still cannot connect, try the next step.</span><span class="sxs-lookup"><span data-stu-id="2052b-132">If you still cannot connect, try the next step.</span></span>

## <a name="use-the-azure-portal"></a><span data-ttu-id="2052b-133">Use the Azure portal</span><span class="sxs-lookup"><span data-stu-id="2052b-133">Use the Azure portal</span></span>
<span data-ttu-id="2052b-134">The Azure portal provides a quick way to reset the SSH configuration or user credentials without installing any tools on your local computer.</span><span class="sxs-lookup"><span data-stu-id="2052b-134">The Azure portal provides a quick way to reset the SSH configuration or user credentials without installing any tools on your local computer.</span></span>

<span data-ttu-id="2052b-135">Select your VM in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2052b-135">Select your VM in the Azure portal.</span></span> <span data-ttu-id="2052b-136">Scroll down to the **Support + Troubleshooting** section and select **Reset password** as in the following example:</span><span class="sxs-lookup"><span data-stu-id="2052b-136">Scroll down to the **Support + Troubleshooting** section and select **Reset password** as in the following example:</span></span>

![Reset SSH configuration or credentials in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-the-ssh-configuration"></a><span data-ttu-id="2052b-138">Reset the SSH configuration</span><span class="sxs-lookup"><span data-stu-id="2052b-138">Reset the SSH configuration</span></span>
<span data-ttu-id="2052b-139">As a first step, select `Reset SSH configuration only` from the **Mode** drop-down menu as in the preceding screenshot, then click the **Reset** button.</span><span class="sxs-lookup"><span data-stu-id="2052b-139">As a first step, select `Reset SSH configuration only` from the **Mode** drop-down menu as in the preceding screenshot, then click the **Reset** button.</span></span> <span data-ttu-id="2052b-140">Once this action has completed, try to access your VM again.</span><span class="sxs-lookup"><span data-stu-id="2052b-140">Once this action has completed, try to access your VM again.</span></span>

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="2052b-141">Reset SSH credentials for a user</span><span class="sxs-lookup"><span data-stu-id="2052b-141">Reset SSH credentials for a user</span></span>
<span data-ttu-id="2052b-142">To reset the credentials of an existing user, select either `Reset SSH public key` or `Reset password` from the **Mode** drop-down menu as in the preceding screenshot.</span><span class="sxs-lookup"><span data-stu-id="2052b-142">To reset the credentials of an existing user, select either `Reset SSH public key` or `Reset password` from the **Mode** drop-down menu as in the preceding screenshot.</span></span> <span data-ttu-id="2052b-143">Specify the username and an SSH key or new password, then click the **Reset** button.</span><span class="sxs-lookup"><span data-stu-id="2052b-143">Specify the username and an SSH key or new password, then click the **Reset** button.</span></span>

<span data-ttu-id="2052b-144">You can also create a user with sudo privileges on the VM from this menu.</span><span class="sxs-lookup"><span data-stu-id="2052b-144">You can also create a user with sudo privileges on the VM from this menu.</span></span> <span data-ttu-id="2052b-145">Enter a new username and associated password or SSH key, and then click the **Reset** button.</span><span class="sxs-lookup"><span data-stu-id="2052b-145">Enter a new username and associated password or SSH key, and then click the **Reset** button.</span></span>

## <a name="use-the-azure-cli-20"></a><span data-ttu-id="2052b-146">Use the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2052b-146">Use the Azure CLI 2.0</span></span>
<span data-ttu-id="2052b-147">If you haven't already, install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="2052b-147">If you haven't already, install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="2052b-148">If you created and uploaded a custom Linux disk image, make sure the [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span><span class="sxs-lookup"><span data-stu-id="2052b-148">If you created and uploaded a custom Linux disk image, make sure the [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="2052b-149">For VMs created using Gallery images, this access extension is already installed and configured for you.</span><span class="sxs-lookup"><span data-stu-id="2052b-149">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="2052b-150">Reset SSH credentials for a user</span><span class="sxs-lookup"><span data-stu-id="2052b-150">Reset SSH credentials for a user</span></span>
<span data-ttu-id="2052b-151">The following example uses [az vm access set-linux-user](/cli/azure/vm/access#set-linux-user) to reset the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="2052b-151">The following example uses [az vm access set-linux-user](/cli/azure/vm/access#set-linux-user) to reset the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="2052b-152">Use your own values as follows:</span><span class="sxs-lookup"><span data-stu-id="2052b-152">Use your own values as follows:</span></span>

```azurecli
az vm access set-linux-user --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

<span data-ttu-id="2052b-153">If using SSH key authentication, you can reset the SSH key for a given user.</span><span class="sxs-lookup"><span data-stu-id="2052b-153">If using SSH key authentication, you can reset the SSH key for a given user.</span></span> <span data-ttu-id="2052b-154">The following example uses **az vm access set-linux-user** to update the SSH key stored in `~/.ssh/id_rsa.pub` for the user named `myUsername`, on the VM named `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="2052b-154">The following example uses **az vm access set-linux-user** to update the SSH key stored in `~/.ssh/id_rsa.pub` for the user named `myUsername`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="2052b-155">Use your own values as follows:</span><span class="sxs-lookup"><span data-stu-id="2052b-155">Use your own values as follows:</span></span>

```azurecli
az vm access set-linux-user --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-the-vmaccess-extension"></a><span data-ttu-id="2052b-156">Use the VMAccess extension</span><span class="sxs-lookup"><span data-stu-id="2052b-156">Use the VMAccess extension</span></span>
<span data-ttu-id="2052b-157">The VM Access Extension for Linux reads in a json file that defines actions to carry out. These actions include resetting SSHD, resetting an SSH key, or adding a user.</span><span class="sxs-lookup"><span data-stu-id="2052b-157">The VM Access Extension for Linux reads in a json file that defines actions to carry out. These actions include resetting SSHD, resetting an SSH key, or adding a user.</span></span> <span data-ttu-id="2052b-158">You still use the Azure CLI to call the VMAccess extension, but you can reuse the json files across multiple VMs if desired.</span><span class="sxs-lookup"><span data-stu-id="2052b-158">You still use the Azure CLI to call the VMAccess extension, but you can reuse the json files across multiple VMs if desired.</span></span> <span data-ttu-id="2052b-159">This approach allows you to create a repository of json files that can then be called for given scenarios.</span><span class="sxs-lookup"><span data-stu-id="2052b-159">This approach allows you to create a repository of json files that can then be called for given scenarios.</span></span>

### <a name="reset-sshd"></a><span data-ttu-id="2052b-160">Reset SSHD</span><span class="sxs-lookup"><span data-stu-id="2052b-160">Reset SSHD</span></span>
<span data-ttu-id="2052b-161">Create a file named `PrivateConf.json` with the following content:</span><span class="sxs-lookup"><span data-stu-id="2052b-161">Create a file named `PrivateConf.json` with the following content:</span></span>

```json
{  
    "reset_ssh":"True"
}
```

<span data-ttu-id="2052b-162">Using the Azure CLI, you then call the `VMAccessForLinux` extension to reset your SSHD connection by specifying your json file.</span><span class="sxs-lookup"><span data-stu-id="2052b-162">Using the Azure CLI, you then call the `VMAccessForLinux` extension to reset your SSHD connection by specifying your json file.</span></span> <span data-ttu-id="2052b-163">The following example resets SSHD on the VM named `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="2052b-163">The following example resets SSHD on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="2052b-164">Use your own values as follows:</span><span class="sxs-lookup"><span data-stu-id="2052b-164">Use your own values as follows:</span></span>

```azurecli
azure vm extension set myResourceGroup myVM \
    VMAccessForLinux Microsoft.OSTCExtensions "1.2" \
    --private-config-path PrivateConf.json
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="2052b-165">Reset SSH credentials for a user</span><span class="sxs-lookup"><span data-stu-id="2052b-165">Reset SSH credentials for a user</span></span>
<span data-ttu-id="2052b-166">If SSHD appears to function correctly, you can reset the credentials for a giver user.</span><span class="sxs-lookup"><span data-stu-id="2052b-166">If SSHD appears to function correctly, you can reset the credentials for a giver user.</span></span> <span data-ttu-id="2052b-167">To reset the password for a user, create a file named `PrivateConf.json`.</span><span class="sxs-lookup"><span data-stu-id="2052b-167">To reset the password for a user, create a file named `PrivateConf.json`.</span></span> <span data-ttu-id="2052b-168">The following example resets the credentials for `myUsername` to the value specified in `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="2052b-168">The following example resets the credentials for `myUsername` to the value specified in `myPassword`.</span></span> <span data-ttu-id="2052b-169">Enter the following lines into your `PrivateConf.json` file, using your own values:</span><span class="sxs-lookup"><span data-stu-id="2052b-169">Enter the following lines into your `PrivateConf.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

<span data-ttu-id="2052b-170">Or to reset the SSH key for a user, first create a file named `PrivateConf.json`.</span><span class="sxs-lookup"><span data-stu-id="2052b-170">Or to reset the SSH key for a user, first create a file named `PrivateConf.json`.</span></span> <span data-ttu-id="2052b-171">The following example resets the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="2052b-171">The following example resets the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="2052b-172">Enter the following lines into your `PrivateConf.json` file, using your own values:</span><span class="sxs-lookup"><span data-stu-id="2052b-172">Enter the following lines into your `PrivateConf.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

<span data-ttu-id="2052b-173">After creating your json file, use the Azure CLI to call the `VMAccessForLinux` extension to reset your SSH user credentials by specifying your json file.</span><span class="sxs-lookup"><span data-stu-id="2052b-173">After creating your json file, use the Azure CLI to call the `VMAccessForLinux` extension to reset your SSH user credentials by specifying your json file.</span></span> <span data-ttu-id="2052b-174">The following example resets credentials on the VM named `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="2052b-174">The following example resets credentials on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="2052b-175">Use your own values as follows:</span><span class="sxs-lookup"><span data-stu-id="2052b-175">Use your own values as follows:</span></span>

```azurecli
azure vm extension set myResourceGroup myVM \
    VMAccessForLinux Microsoft.OSTCExtensions "1.2" \
    --private-config-path PrivateConf.json
```

## <a name="use-the-azure-cli-10"></a><span data-ttu-id="2052b-176">Use the Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="2052b-176">Use the Azure CLI 1.0</span></span>
<span data-ttu-id="2052b-177">If you haven't already, [install the Azure CLI 1.0 and connect to your Azure subscription](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="2052b-177">If you haven't already, [install the Azure CLI 1.0 and connect to your Azure subscription](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="2052b-178">Make sure that you are using Resource Manager mode as follows:</span><span class="sxs-lookup"><span data-stu-id="2052b-178">Make sure that you are using Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="2052b-179">If you created and uploaded a custom Linux disk image, make sure the [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span><span class="sxs-lookup"><span data-stu-id="2052b-179">If you created and uploaded a custom Linux disk image, make sure the [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="2052b-180">For VMs created using Gallery images, this access extension is already installed and configured for you.</span><span class="sxs-lookup"><span data-stu-id="2052b-180">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="2052b-181">Reset SSH configuration</span><span class="sxs-lookup"><span data-stu-id="2052b-181">Reset SSH configuration</span></span>
<span data-ttu-id="2052b-182">The SSHD configuration itself may be misconfigured or the service encountered an error.</span><span class="sxs-lookup"><span data-stu-id="2052b-182">The SSHD configuration itself may be misconfigured or the service encountered an error.</span></span> <span data-ttu-id="2052b-183">You can reset SSHD to make sure the SSH configuration itself is valid.</span><span class="sxs-lookup"><span data-stu-id="2052b-183">You can reset SSHD to make sure the SSH configuration itself is valid.</span></span> <span data-ttu-id="2052b-184">Resetting SSHD should be the first troubleshooting step you take.</span><span class="sxs-lookup"><span data-stu-id="2052b-184">Resetting SSHD should be the first troubleshooting step you take.</span></span>

<span data-ttu-id="2052b-185">The following example resets SSHD on a VM named `myVM` in the resource group named `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="2052b-185">The following example resets SSHD on a VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="2052b-186">Use your own VM and resource group names as follows:</span><span class="sxs-lookup"><span data-stu-id="2052b-186">Use your own VM and resource group names as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="2052b-187">Reset SSH credentials for a user</span><span class="sxs-lookup"><span data-stu-id="2052b-187">Reset SSH credentials for a user</span></span>
<span data-ttu-id="2052b-188">If SSHD appears to function correctly, you can reset the password for a giver user.</span><span class="sxs-lookup"><span data-stu-id="2052b-188">If SSHD appears to function correctly, you can reset the password for a giver user.</span></span> <span data-ttu-id="2052b-189">The following example resets the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="2052b-189">The following example resets the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="2052b-190">Use your own values as follows:</span><span class="sxs-lookup"><span data-stu-id="2052b-190">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

<span data-ttu-id="2052b-191">If using SSH key authentication, you can reset the SSH key for a given user.</span><span class="sxs-lookup"><span data-stu-id="2052b-191">If using SSH key authentication, you can reset the SSH key for a given user.</span></span> <span data-ttu-id="2052b-192">The following example updates the SSH key stored in `~/.ssh/id_rsa.pub` for the user named `myUsername`, on the VM named `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="2052b-192">The following example updates the SSH key stored in `~/.ssh/id_rsa.pub` for the user named `myUsername`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="2052b-193">Use your own values as follows:</span><span class="sxs-lookup"><span data-stu-id="2052b-193">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a><span data-ttu-id="2052b-194">Restart a VM</span><span class="sxs-lookup"><span data-stu-id="2052b-194">Restart a VM</span></span>
<span data-ttu-id="2052b-195">If you have reset the SSH configuration and user credentials, or encountered an error in doing so, you can try restarting the VM to address underlying compute issues.</span><span class="sxs-lookup"><span data-stu-id="2052b-195">If you have reset the SSH configuration and user credentials, or encountered an error in doing so, you can try restarting the VM to address underlying compute issues.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="2052b-196">Azure portal</span><span class="sxs-lookup"><span data-stu-id="2052b-196">Azure portal</span></span>
<span data-ttu-id="2052b-197">To restart a VM using the Azure portal, select your VM and click the **Restart** button as in the following example:</span><span class="sxs-lookup"><span data-stu-id="2052b-197">To restart a VM using the Azure portal, select your VM and click the **Restart** button as in the following example:</span></span>

![Restart a VM in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="2052b-199">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="2052b-199">Azure CLI 1.0</span></span>
<span data-ttu-id="2052b-200">The following example restarts the VM named `myVM` in the resource group named `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="2052b-200">The following example restarts the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="2052b-201">Use your own values as follows:</span><span class="sxs-lookup"><span data-stu-id="2052b-201">Use your own values as follows:</span></span>

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="2052b-202">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2052b-202">Azure CLI 2.0</span></span>
<span data-ttu-id="2052b-203">The following example uses [az vm restart](/cli/azure/vm#restart) to restart the VM named `myVM` in the resource group named `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="2052b-203">The following example uses [az vm restart](/cli/azure/vm#restart) to restart the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="2052b-204">Use your own values as follows:</span><span class="sxs-lookup"><span data-stu-id="2052b-204">Use your own values as follows:</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a><span data-ttu-id="2052b-205">Redeploy a VM</span><span class="sxs-lookup"><span data-stu-id="2052b-205">Redeploy a VM</span></span>
<span data-ttu-id="2052b-206">You can redeploy a VM to another node within Azure, which may correct any underlying networking issues.</span><span class="sxs-lookup"><span data-stu-id="2052b-206">You can redeploy a VM to another node within Azure, which may correct any underlying networking issues.</span></span> <span data-ttu-id="2052b-207">For information about redeploying a VM, see [Redeploy virtual machine to new Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2052b-207">For information about redeploying a VM, see [Redeploy virtual machine to new Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="2052b-208">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with the virtual machine will be updated.</span><span class="sxs-lookup"><span data-stu-id="2052b-208">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with the virtual machine will be updated.</span></span>
> 
> 

### <a name="azure-portal"></a><span data-ttu-id="2052b-209">Azure portal</span><span class="sxs-lookup"><span data-stu-id="2052b-209">Azure portal</span></span>
<span data-ttu-id="2052b-210">To redeploy a VM using the Azure portal, select your VM and scroll down to the **Support + Troubleshooting** section.</span><span class="sxs-lookup"><span data-stu-id="2052b-210">To redeploy a VM using the Azure portal, select your VM and scroll down to the **Support + Troubleshooting** section.</span></span> <span data-ttu-id="2052b-211">Click the **Redeploy** button as in the following example:</span><span class="sxs-lookup"><span data-stu-id="2052b-211">Click the **Redeploy** button as in the following example:</span></span>

![Redeploy a VM in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="2052b-213">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="2052b-213">Azure CLI 1.0</span></span>
<span data-ttu-id="2052b-214">The following example redeploys the VM named `myVM` in the resource group named `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="2052b-214">The following example redeploys the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="2052b-215">Use your own values as follows:</span><span class="sxs-lookup"><span data-stu-id="2052b-215">Use your own values as follows:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="2052b-216">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2052b-216">Azure CLI 2.0</span></span>
<span data-ttu-id="2052b-217">The following example use [az vm redeploy](/cli/azure/vm#redeploy) to redeploy the VM named `myVM` in the resource group named `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="2052b-217">The following example use [az vm redeploy](/cli/azure/vm#redeploy) to redeploy the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="2052b-218">Use your own values as follows:</span><span class="sxs-lookup"><span data-stu-id="2052b-218">Use your own values as follows:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-the-classic-deployment-model"></a><span data-ttu-id="2052b-219">VMs created by using the Classic deployment model</span><span class="sxs-lookup"><span data-stu-id="2052b-219">VMs created by using the Classic deployment model</span></span>
<span data-ttu-id="2052b-220">Try these steps to resolve the most common SSH connection failures for VMs that were created by using the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="2052b-220">Try these steps to resolve the most common SSH connection failures for VMs that were created by using the classic deployment model.</span></span> <span data-ttu-id="2052b-221">After each step, try reconnecting to the VM.</span><span class="sxs-lookup"><span data-stu-id="2052b-221">After each step, try reconnecting to the VM.</span></span>

* <span data-ttu-id="2052b-222">Reset remote access from the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2052b-222">Reset remote access from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="2052b-223">On the Azure portal, select your VM and click the **Reset Remote...** button.</span><span class="sxs-lookup"><span data-stu-id="2052b-223">On the Azure portal, select your VM and click the **Reset Remote...** button.</span></span>
* <span data-ttu-id="2052b-224">Restart the VM.</span><span class="sxs-lookup"><span data-stu-id="2052b-224">Restart the VM.</span></span> <span data-ttu-id="2052b-225">On the [Azure portal](https://portal.azure.com), select your VM and click the **Restart** button.</span><span class="sxs-lookup"><span data-stu-id="2052b-225">On the [Azure portal](https://portal.azure.com), select your VM and click the **Restart** button.</span></span>
  
    <span data-ttu-id="2052b-226">-OR-</span><span class="sxs-lookup"><span data-stu-id="2052b-226">-OR-</span></span>
  
    <span data-ttu-id="2052b-227">On the [Azure classic portal](https://manage.windowsazure.com), select **Virtual machines** > **Instances** > **Restart**.</span><span class="sxs-lookup"><span data-stu-id="2052b-227">On the [Azure classic portal](https://manage.windowsazure.com), select **Virtual machines** > **Instances** > **Restart**.</span></span>
* <span data-ttu-id="2052b-228">Redeploy the VM to a new Azure node.</span><span class="sxs-lookup"><span data-stu-id="2052b-228">Redeploy the VM to a new Azure node.</span></span> <span data-ttu-id="2052b-229">For information about how to redeploy a VM, see [Redeploy virtual machine to new Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2052b-229">For information about how to redeploy a VM, see [Redeploy virtual machine to new Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  
    <span data-ttu-id="2052b-230">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with the virtual machine will be updated.</span><span class="sxs-lookup"><span data-stu-id="2052b-230">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with the virtual machine will be updated.</span></span>
* <span data-ttu-id="2052b-231">Follow the instructions in [How to reset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) to:</span><span class="sxs-lookup"><span data-stu-id="2052b-231">Follow the instructions in [How to reset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) to:</span></span>
  
  * <span data-ttu-id="2052b-232">Reset the password or SSH key.</span><span class="sxs-lookup"><span data-stu-id="2052b-232">Reset the password or SSH key.</span></span>
  * <span data-ttu-id="2052b-233">Create a *sudo* user account.</span><span class="sxs-lookup"><span data-stu-id="2052b-233">Create a *sudo* user account.</span></span>
  * <span data-ttu-id="2052b-234">Reset the SSH configuration.</span><span class="sxs-lookup"><span data-stu-id="2052b-234">Reset the SSH configuration.</span></span>
* <span data-ttu-id="2052b-235">Check the VM's resource health for any platform issues.</span><span class="sxs-lookup"><span data-stu-id="2052b-235">Check the VM's resource health for any platform issues.</span></span><br>
     <span data-ttu-id="2052b-236">Select your VM and scroll down **Settings** > **Check Health**.</span><span class="sxs-lookup"><span data-stu-id="2052b-236">Select your VM and scroll down **Settings** > **Check Health**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2052b-237">Additional resources</span><span class="sxs-lookup"><span data-stu-id="2052b-237">Additional resources</span></span>
* <span data-ttu-id="2052b-238">If you are still unable to SSH to your VM after following the after steps, see [more detailed troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to review additional steps to resolve your issue.</span><span class="sxs-lookup"><span data-stu-id="2052b-238">If you are still unable to SSH to your VM after following the after steps, see [more detailed troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to review additional steps to resolve your issue.</span></span>
* <span data-ttu-id="2052b-239">For more information about troubleshooting application access, see [Troubleshoot access to an application running on an Azure virtual machine](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="2052b-239">For more information about troubleshooting application access, see [Troubleshoot access to an application running on an Azure virtual machine](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="2052b-240">For more information about troubleshooting virtual machines that were created by using the classic deployment model, see [How to reset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2052b-240">For more information about troubleshooting virtual machines that were created by using the classic deployment model, see [How to reset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>




