---
title: Troubleshoot SSH connection issues to an Azure VM | Microsoft Docs
description: How to troubleshoot issues such as 'SSH connection failed' or 'SSH connection refused' for an Azure VM running Linux.
keywords: ssh connection refused, ssh error, azure ssh, SSH connection failed
services: virtual-machines-linux
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: dcb82e19-29b2-47bb-99f2-900d4cfb5bbb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: e0cec53b98d5eb5016549d0748d2824215258e88
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44823932"
---
# <a name="troubleshoot-ssh-connections-to-an-azure-linux-vm-that-fails-errors-out-or-is-refused"></a><span data-ttu-id="1fa57-104">Troubleshoot SSH connections to an Azure Linux VM that fails, errors out, or is refused</span><span class="sxs-lookup"><span data-stu-id="1fa57-104">Troubleshoot SSH connections to an Azure Linux VM that fails, errors out, or is refused</span></span>
<span data-ttu-id="1fa57-105">There are various reasons that you encounter Secure Shell (SSH) errors, SSH connection failures, or SSH is refused when you try to connect to a Linux virtual machine (VM).</span><span class="sxs-lookup"><span data-stu-id="1fa57-105">There are various reasons that you encounter Secure Shell (SSH) errors, SSH connection failures, or SSH is refused when you try to connect to a Linux virtual machine (VM).</span></span> <span data-ttu-id="1fa57-106">This article helps you find and correct the problems.</span><span class="sxs-lookup"><span data-stu-id="1fa57-106">This article helps you find and correct the problems.</span></span> <span data-ttu-id="1fa57-107">You can use the Azure portal, Azure CLI, or VM Access Extension for Linux to troubleshoot and resolve connection problems.</span><span class="sxs-lookup"><span data-stu-id="1fa57-107">You can use the Azure portal, Azure CLI, or VM Access Extension for Linux to troubleshoot and resolve connection problems.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="1fa57-108">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](http://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="1fa57-108">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](http://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="1fa57-109">Alternatively, you can file an Azure support incident.</span><span class="sxs-lookup"><span data-stu-id="1fa57-109">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="1fa57-110">Go to the [Azure support site](http://azure.microsoft.com/support/options/) and select **Get support**.</span><span class="sxs-lookup"><span data-stu-id="1fa57-110">Go to the [Azure support site](http://azure.microsoft.com/support/options/) and select **Get support**.</span></span> <span data-ttu-id="1fa57-111">For information about using Azure Support, read the [Microsoft Azure support FAQ](http://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="1fa57-111">For information about using Azure Support, read the [Microsoft Azure support FAQ](http://azure.microsoft.com/support/faq/).</span></span>

## <a name="quick-troubleshooting-steps"></a><span data-ttu-id="1fa57-112">Quick troubleshooting steps</span><span class="sxs-lookup"><span data-stu-id="1fa57-112">Quick troubleshooting steps</span></span>
<span data-ttu-id="1fa57-113">After each troubleshooting step, try reconnecting to the VM.</span><span class="sxs-lookup"><span data-stu-id="1fa57-113">After each troubleshooting step, try reconnecting to the VM.</span></span>

1. <span data-ttu-id="1fa57-114">Reset the SSH configuration.</span><span class="sxs-lookup"><span data-stu-id="1fa57-114">Reset the SSH configuration.</span></span>
2. <span data-ttu-id="1fa57-115">Reset the credentials for the user.</span><span class="sxs-lookup"><span data-stu-id="1fa57-115">Reset the credentials for the user.</span></span>
3. <span data-ttu-id="1fa57-116">Verify the [network security group](../../virtual-network/security-overview.md) rules permit SSH traffic.</span><span class="sxs-lookup"><span data-stu-id="1fa57-116">Verify the [network security group](../../virtual-network/security-overview.md) rules permit SSH traffic.</span></span>
   * <span data-ttu-id="1fa57-117">Ensure that a Network Security Group rule exists to permit SSH traffic (by default, TCP port 22).</span><span class="sxs-lookup"><span data-stu-id="1fa57-117">Ensure that a Network Security Group rule exists to permit SSH traffic (by default, TCP port 22).</span></span>
   * <span data-ttu-id="1fa57-118">You cannot use port redirection / mapping without using an Azure load balancer.</span><span class="sxs-lookup"><span data-stu-id="1fa57-118">You cannot use port redirection / mapping without using an Azure load balancer.</span></span>
4. <span data-ttu-id="1fa57-119">Check the [VM resource health](../../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1fa57-119">Check the [VM resource health](../../resource-health/resource-health-overview.md).</span></span> 
   * <span data-ttu-id="1fa57-120">Ensure that the VM reports as being healthy.</span><span class="sxs-lookup"><span data-stu-id="1fa57-120">Ensure that the VM reports as being healthy.</span></span>
   * <span data-ttu-id="1fa57-121">If you have boot diagnostics enabled, verify the VM is not reporting boot errors in the logs.</span><span class="sxs-lookup"><span data-stu-id="1fa57-121">If you have boot diagnostics enabled, verify the VM is not reporting boot errors in the logs.</span></span>
5. <span data-ttu-id="1fa57-122">Restart the VM.</span><span class="sxs-lookup"><span data-stu-id="1fa57-122">Restart the VM.</span></span>
6. <span data-ttu-id="1fa57-123">Redeploy the VM.</span><span class="sxs-lookup"><span data-stu-id="1fa57-123">Redeploy the VM.</span></span>

<span data-ttu-id="1fa57-124">Continue reading for more detailed troubleshooting steps and explanations.</span><span class="sxs-lookup"><span data-stu-id="1fa57-124">Continue reading for more detailed troubleshooting steps and explanations.</span></span>

## <a name="available-methods-to-troubleshoot-ssh-connection-issues"></a><span data-ttu-id="1fa57-125">Available methods to troubleshoot SSH connection issues</span><span class="sxs-lookup"><span data-stu-id="1fa57-125">Available methods to troubleshoot SSH connection issues</span></span>
<span data-ttu-id="1fa57-126">You can reset credentials or SSH configuration using one of the following methods:</span><span class="sxs-lookup"><span data-stu-id="1fa57-126">You can reset credentials or SSH configuration using one of the following methods:</span></span>

* <span data-ttu-id="1fa57-127">[Azure portal](#use-the-azure-portal) - great if you need to quickly reset the SSH configuration or SSH key and you don't have the Azure tools installed.</span><span class="sxs-lookup"><span data-stu-id="1fa57-127">[Azure portal](#use-the-azure-portal) - great if you need to quickly reset the SSH configuration or SSH key and you don't have the Azure tools installed.</span></span>
* <span data-ttu-id="1fa57-128">[Azure CLI 2.0](#use-the-azure-cli-20) - if you are already on the command line, quickly reset the SSH configuration or credentials.</span><span class="sxs-lookup"><span data-stu-id="1fa57-128">[Azure CLI 2.0](#use-the-azure-cli-20) - if you are already on the command line, quickly reset the SSH configuration or credentials.</span></span> <span data-ttu-id="1fa57-129">You can also use the [Azure CLI 1.0](#use-the-azure-cli-10)</span><span class="sxs-lookup"><span data-stu-id="1fa57-129">You can also use the [Azure CLI 1.0](#use-the-azure-cli-10)</span></span>
* <span data-ttu-id="1fa57-130">[Azure VMAccessForLinux extension](#use-the-vmaccess-extension) - create and reuse json definition files to reset the SSH configuration or user credentials.</span><span class="sxs-lookup"><span data-stu-id="1fa57-130">[Azure VMAccessForLinux extension](#use-the-vmaccess-extension) - create and reuse json definition files to reset the SSH configuration or user credentials.</span></span>

<span data-ttu-id="1fa57-131">After each troubleshooting step, try connecting to your VM again.</span><span class="sxs-lookup"><span data-stu-id="1fa57-131">After each troubleshooting step, try connecting to your VM again.</span></span> <span data-ttu-id="1fa57-132">If you still cannot connect, try the next step.</span><span class="sxs-lookup"><span data-stu-id="1fa57-132">If you still cannot connect, try the next step.</span></span>

## <a name="use-the-azure-portal"></a><span data-ttu-id="1fa57-133">Use the Azure portal</span><span class="sxs-lookup"><span data-stu-id="1fa57-133">Use the Azure portal</span></span>
<span data-ttu-id="1fa57-134">The Azure portal provides a quick way to reset the SSH configuration or user credentials without installing any tools on your local computer.</span><span class="sxs-lookup"><span data-stu-id="1fa57-134">The Azure portal provides a quick way to reset the SSH configuration or user credentials without installing any tools on your local computer.</span></span>

<span data-ttu-id="1fa57-135">Select your VM in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1fa57-135">Select your VM in the Azure portal.</span></span> <span data-ttu-id="1fa57-136">Scroll down to the **Support + Troubleshooting** section and select **Reset password** as in the following example:</span><span class="sxs-lookup"><span data-stu-id="1fa57-136">Scroll down to the **Support + Troubleshooting** section and select **Reset password** as in the following example:</span></span>

![Reset SSH configuration or credentials in the Azure portal](./media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-the-ssh-configuration"></a><span data-ttu-id="1fa57-138">Reset the SSH configuration</span><span class="sxs-lookup"><span data-stu-id="1fa57-138">Reset the SSH configuration</span></span>
<span data-ttu-id="1fa57-139">As a first step, select `Reset configuration only` from the **Mode** drop-down menu as in the preceding screenshot, then click the **Reset** button.</span><span class="sxs-lookup"><span data-stu-id="1fa57-139">As a first step, select `Reset configuration only` from the **Mode** drop-down menu as in the preceding screenshot, then click the **Reset** button.</span></span> <span data-ttu-id="1fa57-140">Once this action has completed, try to access your VM again.</span><span class="sxs-lookup"><span data-stu-id="1fa57-140">Once this action has completed, try to access your VM again.</span></span>

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="1fa57-141">Reset SSH credentials for a user</span><span class="sxs-lookup"><span data-stu-id="1fa57-141">Reset SSH credentials for a user</span></span>
<span data-ttu-id="1fa57-142">To reset the credentials of an existing user, select either `Reset SSH public key` or `Reset password` from the **Mode** drop-down menu as in the preceding screenshot.</span><span class="sxs-lookup"><span data-stu-id="1fa57-142">To reset the credentials of an existing user, select either `Reset SSH public key` or `Reset password` from the **Mode** drop-down menu as in the preceding screenshot.</span></span> <span data-ttu-id="1fa57-143">Specify the username and an SSH key or new password, then click the **Reset** button.</span><span class="sxs-lookup"><span data-stu-id="1fa57-143">Specify the username and an SSH key or new password, then click the **Reset** button.</span></span>

<span data-ttu-id="1fa57-144">You can also create a user with sudo privileges on the VM from this menu.</span><span class="sxs-lookup"><span data-stu-id="1fa57-144">You can also create a user with sudo privileges on the VM from this menu.</span></span> <span data-ttu-id="1fa57-145">Enter a new username and associated password or SSH key, and then click the **Reset** button.</span><span class="sxs-lookup"><span data-stu-id="1fa57-145">Enter a new username and associated password or SSH key, and then click the **Reset** button.</span></span>

### <a name="check-security-rules"></a><span data-ttu-id="1fa57-146">Check security rules</span><span class="sxs-lookup"><span data-stu-id="1fa57-146">Check security rules</span></span>

<span data-ttu-id="1fa57-147">Use [IP flow verify](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md) to confirm if a rule in a network security group is blocking traffic to or from a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1fa57-147">Use [IP flow verify](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md) to confirm if a rule in a network security group is blocking traffic to or from a virtual machine.</span></span> <span data-ttu-id="1fa57-148">You can also review effective security group rules to ensure inbound "Allow" NSG rule exists and is prioritized for SSH port (default 22).</span><span class="sxs-lookup"><span data-stu-id="1fa57-148">You can also review effective security group rules to ensure inbound "Allow" NSG rule exists and is prioritized for SSH port (default 22).</span></span> <span data-ttu-id="1fa57-149">For more information, see [Using effective security rules to troubleshoot VM traffic flow](../../virtual-network/diagnose-network-traffic-filter-problem.md).</span><span class="sxs-lookup"><span data-stu-id="1fa57-149">For more information, see [Using effective security rules to troubleshoot VM traffic flow](../../virtual-network/diagnose-network-traffic-filter-problem.md).</span></span>

### <a name="check-routing"></a><span data-ttu-id="1fa57-150">Check routing</span><span class="sxs-lookup"><span data-stu-id="1fa57-150">Check routing</span></span>

<span data-ttu-id="1fa57-151">Use Network Watcher's [Next hop](../../network-watcher/network-watcher-check-next-hop-portal.md) capability to confirm that a route isn't preventing traffic from being routed to or from a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1fa57-151">Use Network Watcher's [Next hop](../../network-watcher/network-watcher-check-next-hop-portal.md) capability to confirm that a route isn't preventing traffic from being routed to or from a virtual machine.</span></span> <span data-ttu-id="1fa57-152">You can also review effective routes to see all effective routes for a network interface.</span><span class="sxs-lookup"><span data-stu-id="1fa57-152">You can also review effective routes to see all effective routes for a network interface.</span></span> <span data-ttu-id="1fa57-153">For more information, see [Using effective routes to troubleshoot VM traffic flow](../../virtual-network/diagnose-network-routing-problem.md).</span><span class="sxs-lookup"><span data-stu-id="1fa57-153">For more information, see [Using effective routes to troubleshoot VM traffic flow](../../virtual-network/diagnose-network-routing-problem.md).</span></span>

## <a name="use-the-azure-cli-20"></a><span data-ttu-id="1fa57-154">Use the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1fa57-154">Use the Azure CLI 2.0</span></span>
<span data-ttu-id="1fa57-155">If you haven't already, install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/reference-index#az_login).</span><span class="sxs-lookup"><span data-stu-id="1fa57-155">If you haven't already, install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/reference-index#az_login).</span></span>

<span data-ttu-id="1fa57-156">If you created and uploaded a custom Linux disk image, make sure the [Microsoft Azure Linux Agent](../extensions/agent-windows.md) version 2.0.5 or later is installed.</span><span class="sxs-lookup"><span data-stu-id="1fa57-156">If you created and uploaded a custom Linux disk image, make sure the [Microsoft Azure Linux Agent](../extensions/agent-windows.md) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="1fa57-157">For VMs created using Gallery images, this access extension is already installed and configured for you.</span><span class="sxs-lookup"><span data-stu-id="1fa57-157">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="1fa57-158">Reset SSH configuration</span><span class="sxs-lookup"><span data-stu-id="1fa57-158">Reset SSH configuration</span></span>
<span data-ttu-id="1fa57-159">You can initially try resetting the SSH configuration to default values and rebooting the SSH server on the VM.</span><span class="sxs-lookup"><span data-stu-id="1fa57-159">You can initially try resetting the SSH configuration to default values and rebooting the SSH server on the VM.</span></span> <span data-ttu-id="1fa57-160">Note that this does not change the user account name, password, or SSH keys.</span><span class="sxs-lookup"><span data-stu-id="1fa57-160">Note that this does not change the user account name, password, or SSH keys.</span></span>
<span data-ttu-id="1fa57-161">The following example uses [az vm user reset-ssh](/cli/azure/vm/user#az_vm_user_reset_ssh) to reset the SSH configuration on the VM named `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="1fa57-161">The following example uses [az vm user reset-ssh](/cli/azure/vm/user#az_vm_user_reset_ssh) to reset the SSH configuration on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="1fa57-162">Use your own values as follows:</span><span class="sxs-lookup"><span data-stu-id="1fa57-162">Use your own values as follows:</span></span>

```azurecli
az vm user reset-ssh --resource-group myResourceGroup --name myVM
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="1fa57-163">Reset SSH credentials for a user</span><span class="sxs-lookup"><span data-stu-id="1fa57-163">Reset SSH credentials for a user</span></span>
<span data-ttu-id="1fa57-164">The following example uses [az vm user update](/cli/azure/vm/user#az_vm_user_update) to reset the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="1fa57-164">The following example uses [az vm user update](/cli/azure/vm/user#az_vm_user_update) to reset the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="1fa57-165">Use your own values as follows:</span><span class="sxs-lookup"><span data-stu-id="1fa57-165">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

<span data-ttu-id="1fa57-166">If using SSH key authentication, you can reset the SSH key for a given user.</span><span class="sxs-lookup"><span data-stu-id="1fa57-166">If using SSH key authentication, you can reset the SSH key for a given user.</span></span> <span data-ttu-id="1fa57-167">The following example uses **az vm access set-linux-user** to update the SSH key stored in `~/.ssh/id_rsa.pub` for the user named `myUsername`, on the VM named `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="1fa57-167">The following example uses **az vm access set-linux-user** to update the SSH key stored in `~/.ssh/id_rsa.pub` for the user named `myUsername`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="1fa57-168">Use your own values as follows:</span><span class="sxs-lookup"><span data-stu-id="1fa57-168">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-the-vmaccess-extension"></a><span data-ttu-id="1fa57-169">Use the VMAccess extension</span><span class="sxs-lookup"><span data-stu-id="1fa57-169">Use the VMAccess extension</span></span>
<span data-ttu-id="1fa57-170">The VM Access Extension for Linux reads in a json file that defines actions to carry out. These actions include resetting SSHD, resetting an SSH key, or adding a user.</span><span class="sxs-lookup"><span data-stu-id="1fa57-170">The VM Access Extension for Linux reads in a json file that defines actions to carry out. These actions include resetting SSHD, resetting an SSH key, or adding a user.</span></span> <span data-ttu-id="1fa57-171">You still use the Azure CLI to call the VMAccess extension, but you can reuse the json files across multiple VMs if desired.</span><span class="sxs-lookup"><span data-stu-id="1fa57-171">You still use the Azure CLI to call the VMAccess extension, but you can reuse the json files across multiple VMs if desired.</span></span> <span data-ttu-id="1fa57-172">This approach allows you to create a repository of json files that can then be called for given scenarios.</span><span class="sxs-lookup"><span data-stu-id="1fa57-172">This approach allows you to create a repository of json files that can then be called for given scenarios.</span></span>

### <a name="reset-sshd"></a><span data-ttu-id="1fa57-173">Reset SSHD</span><span class="sxs-lookup"><span data-stu-id="1fa57-173">Reset SSHD</span></span>
<span data-ttu-id="1fa57-174">Create a file named `settings.json` with the following content:</span><span class="sxs-lookup"><span data-stu-id="1fa57-174">Create a file named `settings.json` with the following content:</span></span>

```json
{  
    "reset_ssh":"True"
}
```

<span data-ttu-id="1fa57-175">Using the Azure CLI, you then call the `VMAccessForLinux` extension to reset your SSHD connection by specifying your json file.</span><span class="sxs-lookup"><span data-stu-id="1fa57-175">Using the Azure CLI, you then call the `VMAccessForLinux` extension to reset your SSHD connection by specifying your json file.</span></span> <span data-ttu-id="1fa57-176">The following example uses [az vm extension set](/cli/azure/vm/extension#az_vm_extension_set) to reset SSHD on the VM named `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="1fa57-176">The following example uses [az vm extension set](/cli/azure/vm/extension#az_vm_extension_set) to reset SSHD on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="1fa57-177">Use your own values as follows:</span><span class="sxs-lookup"><span data-stu-id="1fa57-177">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="1fa57-178">Reset SSH credentials for a user</span><span class="sxs-lookup"><span data-stu-id="1fa57-178">Reset SSH credentials for a user</span></span>
<span data-ttu-id="1fa57-179">If SSHD appears to function correctly, you can reset the credentials for a giver user.</span><span class="sxs-lookup"><span data-stu-id="1fa57-179">If SSHD appears to function correctly, you can reset the credentials for a giver user.</span></span> <span data-ttu-id="1fa57-180">To reset the password for a user, create a file named `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="1fa57-180">To reset the password for a user, create a file named `settings.json`.</span></span> <span data-ttu-id="1fa57-181">The following example resets the credentials for `myUsername` to the value specified in `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="1fa57-181">The following example resets the credentials for `myUsername` to the value specified in `myPassword`.</span></span> <span data-ttu-id="1fa57-182">Enter the following lines into your `settings.json` file, using your own values:</span><span class="sxs-lookup"><span data-stu-id="1fa57-182">Enter the following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

<span data-ttu-id="1fa57-183">Or to reset the SSH key for a user, first create a file named `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="1fa57-183">Or to reset the SSH key for a user, first create a file named `settings.json`.</span></span> <span data-ttu-id="1fa57-184">The following example resets the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="1fa57-184">The following example resets the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="1fa57-185">Enter the following lines into your `settings.json` file, using your own values:</span><span class="sxs-lookup"><span data-stu-id="1fa57-185">Enter the following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

<span data-ttu-id="1fa57-186">After creating your json file, use the Azure CLI to call the `VMAccessForLinux` extension to reset your SSH user credentials by specifying your json file.</span><span class="sxs-lookup"><span data-stu-id="1fa57-186">After creating your json file, use the Azure CLI to call the `VMAccessForLinux` extension to reset your SSH user credentials by specifying your json file.</span></span> <span data-ttu-id="1fa57-187">The following example resets credentials on the VM named `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="1fa57-187">The following example resets credentials on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="1fa57-188">Use your own values as follows:</span><span class="sxs-lookup"><span data-stu-id="1fa57-188">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

## <a name="use-the-azure-cli-10"></a><span data-ttu-id="1fa57-189">Use the Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1fa57-189">Use the Azure CLI 1.0</span></span>
<span data-ttu-id="1fa57-190">If you haven't already, [install the Azure CLI 1.0 and connect to your Azure subscription](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="1fa57-190">If you haven't already, [install the Azure CLI 1.0 and connect to your Azure subscription](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="1fa57-191">Make sure that you are using Resource Manager mode as follows:</span><span class="sxs-lookup"><span data-stu-id="1fa57-191">Make sure that you are using Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="1fa57-192">If you created and uploaded a custom Linux disk image, make sure the [Microsoft Azure Linux Agent](../extensions/agent-windows.md) version 2.0.5 or later is installed.</span><span class="sxs-lookup"><span data-stu-id="1fa57-192">If you created and uploaded a custom Linux disk image, make sure the [Microsoft Azure Linux Agent](../extensions/agent-windows.md) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="1fa57-193">For VMs created using Gallery images, this access extension is already installed and configured for you.</span><span class="sxs-lookup"><span data-stu-id="1fa57-193">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="1fa57-194">Reset SSH configuration</span><span class="sxs-lookup"><span data-stu-id="1fa57-194">Reset SSH configuration</span></span>
<span data-ttu-id="1fa57-195">The SSHD configuration itself may be misconfigured or the service encountered an error.</span><span class="sxs-lookup"><span data-stu-id="1fa57-195">The SSHD configuration itself may be misconfigured or the service encountered an error.</span></span> <span data-ttu-id="1fa57-196">You can reset SSHD to make sure the SSH configuration itself is valid.</span><span class="sxs-lookup"><span data-stu-id="1fa57-196">You can reset SSHD to make sure the SSH configuration itself is valid.</span></span> <span data-ttu-id="1fa57-197">Resetting SSHD should be the first troubleshooting step you take.</span><span class="sxs-lookup"><span data-stu-id="1fa57-197">Resetting SSHD should be the first troubleshooting step you take.</span></span>

<span data-ttu-id="1fa57-198">The following example resets SSHD on a VM named `myVM` in the resource group named `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="1fa57-198">The following example resets SSHD on a VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="1fa57-199">Use your own VM and resource group names as follows:</span><span class="sxs-lookup"><span data-stu-id="1fa57-199">Use your own VM and resource group names as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="1fa57-200">Reset SSH credentials for a user</span><span class="sxs-lookup"><span data-stu-id="1fa57-200">Reset SSH credentials for a user</span></span>
<span data-ttu-id="1fa57-201">If SSHD appears to function correctly, you can reset the password for a giver user.</span><span class="sxs-lookup"><span data-stu-id="1fa57-201">If SSHD appears to function correctly, you can reset the password for a giver user.</span></span> <span data-ttu-id="1fa57-202">The following example resets the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="1fa57-202">The following example resets the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="1fa57-203">Use your own values as follows:</span><span class="sxs-lookup"><span data-stu-id="1fa57-203">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

<span data-ttu-id="1fa57-204">If using SSH key authentication, you can reset the SSH key for a given user.</span><span class="sxs-lookup"><span data-stu-id="1fa57-204">If using SSH key authentication, you can reset the SSH key for a given user.</span></span> <span data-ttu-id="1fa57-205">The following example updates the SSH key stored in `~/.ssh/id_rsa.pub` for the user named `myUsername`, on the VM named `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="1fa57-205">The following example updates the SSH key stored in `~/.ssh/id_rsa.pub` for the user named `myUsername`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="1fa57-206">Use your own values as follows:</span><span class="sxs-lookup"><span data-stu-id="1fa57-206">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a><span data-ttu-id="1fa57-207">Restart a VM</span><span class="sxs-lookup"><span data-stu-id="1fa57-207">Restart a VM</span></span>
<span data-ttu-id="1fa57-208">If you have reset the SSH configuration and user credentials, or encountered an error in doing so, you can try restarting the VM to address underlying compute issues.</span><span class="sxs-lookup"><span data-stu-id="1fa57-208">If you have reset the SSH configuration and user credentials, or encountered an error in doing so, you can try restarting the VM to address underlying compute issues.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="1fa57-209">Azure portal</span><span class="sxs-lookup"><span data-stu-id="1fa57-209">Azure portal</span></span>
<span data-ttu-id="1fa57-210">To restart a VM using the Azure portal, select your VM and click the **Restart** button as in the following example:</span><span class="sxs-lookup"><span data-stu-id="1fa57-210">To restart a VM using the Azure portal, select your VM and click the **Restart** button as in the following example:</span></span>

![Restart a VM in the Azure portal](./media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="1fa57-212">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1fa57-212">Azure CLI 1.0</span></span>
<span data-ttu-id="1fa57-213">The following example restarts the VM named `myVM` in the resource group named `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="1fa57-213">The following example restarts the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="1fa57-214">Use your own values as follows:</span><span class="sxs-lookup"><span data-stu-id="1fa57-214">Use your own values as follows:</span></span>

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="1fa57-215">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1fa57-215">Azure CLI 2.0</span></span>
<span data-ttu-id="1fa57-216">The following example uses [az vm restart](/cli/azure/vm#az_vm_restart) to restart the VM named `myVM` in the resource group named `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="1fa57-216">The following example uses [az vm restart](/cli/azure/vm#az_vm_restart) to restart the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="1fa57-217">Use your own values as follows:</span><span class="sxs-lookup"><span data-stu-id="1fa57-217">Use your own values as follows:</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a><span data-ttu-id="1fa57-218">Redeploy a VM</span><span class="sxs-lookup"><span data-stu-id="1fa57-218">Redeploy a VM</span></span>
<span data-ttu-id="1fa57-219">You can redeploy a VM to another node within Azure, which may correct any underlying networking issues.</span><span class="sxs-lookup"><span data-stu-id="1fa57-219">You can redeploy a VM to another node within Azure, which may correct any underlying networking issues.</span></span> <span data-ttu-id="1fa57-220">For information about redeploying a VM, see [Redeploy virtual machine to new Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1fa57-220">For information about redeploying a VM, see [Redeploy virtual machine to new Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="1fa57-221">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with the virtual machine will be updated.</span><span class="sxs-lookup"><span data-stu-id="1fa57-221">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with the virtual machine will be updated.</span></span>
> 
> 

### <a name="azure-portal"></a><span data-ttu-id="1fa57-222">Azure portal</span><span class="sxs-lookup"><span data-stu-id="1fa57-222">Azure portal</span></span>
<span data-ttu-id="1fa57-223">To redeploy a VM using the Azure portal, select your VM and scroll down to the **Support + Troubleshooting** section.</span><span class="sxs-lookup"><span data-stu-id="1fa57-223">To redeploy a VM using the Azure portal, select your VM and scroll down to the **Support + Troubleshooting** section.</span></span> <span data-ttu-id="1fa57-224">Click the **Redeploy** button as in the following example:</span><span class="sxs-lookup"><span data-stu-id="1fa57-224">Click the **Redeploy** button as in the following example:</span></span>

![Redeploy a VM in the Azure portal](./media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="1fa57-226">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1fa57-226">Azure CLI 1.0</span></span>
<span data-ttu-id="1fa57-227">The following example redeploys the VM named `myVM` in the resource group named `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="1fa57-227">The following example redeploys the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="1fa57-228">Use your own values as follows:</span><span class="sxs-lookup"><span data-stu-id="1fa57-228">Use your own values as follows:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="1fa57-229">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1fa57-229">Azure CLI 2.0</span></span>
<span data-ttu-id="1fa57-230">The following example use [az vm redeploy](/cli/azure/vm#az_vm_redeploy) to redeploy the VM named `myVM` in the resource group named `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="1fa57-230">The following example use [az vm redeploy](/cli/azure/vm#az_vm_redeploy) to redeploy the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="1fa57-231">Use your own values as follows:</span><span class="sxs-lookup"><span data-stu-id="1fa57-231">Use your own values as follows:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-the-classic-deployment-model"></a><span data-ttu-id="1fa57-232">VMs created by using the Classic deployment model</span><span class="sxs-lookup"><span data-stu-id="1fa57-232">VMs created by using the Classic deployment model</span></span>
<span data-ttu-id="1fa57-233">Try these steps to resolve the most common SSH connection failures for VMs that were created by using the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="1fa57-233">Try these steps to resolve the most common SSH connection failures for VMs that were created by using the classic deployment model.</span></span> <span data-ttu-id="1fa57-234">After each step, try reconnecting to the VM.</span><span class="sxs-lookup"><span data-stu-id="1fa57-234">After each step, try reconnecting to the VM.</span></span>

* <span data-ttu-id="1fa57-235">Reset remote access from the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1fa57-235">Reset remote access from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="1fa57-236">On the Azure portal, select your VM and click the **Reset Remote...** button.</span><span class="sxs-lookup"><span data-stu-id="1fa57-236">On the Azure portal, select your VM and click the **Reset Remote...** button.</span></span>
* <span data-ttu-id="1fa57-237">Restart the VM.</span><span class="sxs-lookup"><span data-stu-id="1fa57-237">Restart the VM.</span></span> <span data-ttu-id="1fa57-238">On the [Azure portal](https://portal.azure.com), select your VM and click the **Restart** button.</span><span class="sxs-lookup"><span data-stu-id="1fa57-238">On the [Azure portal](https://portal.azure.com), select your VM and click the **Restart** button.</span></span>
    
* <span data-ttu-id="1fa57-239">Redeploy the VM to a new Azure node.</span><span class="sxs-lookup"><span data-stu-id="1fa57-239">Redeploy the VM to a new Azure node.</span></span> <span data-ttu-id="1fa57-240">For information about how to redeploy a VM, see [Redeploy virtual machine to new Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1fa57-240">For information about how to redeploy a VM, see [Redeploy virtual machine to new Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  
    <span data-ttu-id="1fa57-241">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with the virtual machine will be updated.</span><span class="sxs-lookup"><span data-stu-id="1fa57-241">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with the virtual machine will be updated.</span></span>
* <span data-ttu-id="1fa57-242">Follow the instructions in [How to reset a password or SSH for Linux-based virtual machines](classic/reset-access-classic.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) to:</span><span class="sxs-lookup"><span data-stu-id="1fa57-242">Follow the instructions in [How to reset a password or SSH for Linux-based virtual machines](classic/reset-access-classic.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) to:</span></span>
  
  * <span data-ttu-id="1fa57-243">Reset the password or SSH key.</span><span class="sxs-lookup"><span data-stu-id="1fa57-243">Reset the password or SSH key.</span></span>
  * <span data-ttu-id="1fa57-244">Create a *sudo* user account.</span><span class="sxs-lookup"><span data-stu-id="1fa57-244">Create a *sudo* user account.</span></span>
  * <span data-ttu-id="1fa57-245">Reset the SSH configuration.</span><span class="sxs-lookup"><span data-stu-id="1fa57-245">Reset the SSH configuration.</span></span>
* <span data-ttu-id="1fa57-246">Check the VM's resource health for any platform issues.</span><span class="sxs-lookup"><span data-stu-id="1fa57-246">Check the VM's resource health for any platform issues.</span></span><br>
     <span data-ttu-id="1fa57-247">Select your VM and scroll down **Settings** > **Check Health**.</span><span class="sxs-lookup"><span data-stu-id="1fa57-247">Select your VM and scroll down **Settings** > **Check Health**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1fa57-248">Additional resources</span><span class="sxs-lookup"><span data-stu-id="1fa57-248">Additional resources</span></span>
* <span data-ttu-id="1fa57-249">If you are still unable to SSH to your VM after following the after steps, see [more detailed troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to review additional steps to resolve your issue.</span><span class="sxs-lookup"><span data-stu-id="1fa57-249">If you are still unable to SSH to your VM after following the after steps, see [more detailed troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to review additional steps to resolve your issue.</span></span>
* <span data-ttu-id="1fa57-250">For more information about troubleshooting application access, see [Troubleshoot access to an application running on an Azure virtual machine](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="1fa57-250">For more information about troubleshooting application access, see [Troubleshoot access to an application running on an Azure virtual machine](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="1fa57-251">For more information about troubleshooting virtual machines that were created by using the classic deployment model, see [How to reset a password or SSH for Linux-based virtual machines](classic/reset-access-classic.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1fa57-251">For more information about troubleshooting virtual machines that were created by using the classic deployment model, see [How to reset a password or SSH for Linux-based virtual machines](classic/reset-access-classic.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

