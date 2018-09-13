---
title: Detailed SSH troubleshooting for an Azure VM | Microsoft Docs
description: More detailed SSH troubleshooting steps for issues connecting to an Azure virtual machine
keywords: ssh connection refused,ssh error,azure ssh,SSH connection failed
services: virtual-machines-linux
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: b8e8be5f-e8a6-489d-9922-9df8de32e839
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: support-article
ms.date: 03/07/2017
ms.author: iainfou
ms.openlocfilehash: 01cb62ba1664d10ce93f7856cd03793106aecbd8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563282"
---
# <a name="detailed-ssh-troubleshooting-steps"></a><span data-ttu-id="1e810-104">Detailed SSH troubleshooting steps</span><span class="sxs-lookup"><span data-stu-id="1e810-104">Detailed SSH troubleshooting steps</span></span>
<span data-ttu-id="1e810-105">There are many possible reasons that the SSH client might not be able to reach the SSH service on the VM.</span><span class="sxs-lookup"><span data-stu-id="1e810-105">There are many possible reasons that the SSH client might not be able to reach the SSH service on the VM.</span></span> <span data-ttu-id="1e810-106">If you have followed through the more [general SSH troubleshooting steps](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), you need to further troubleshoot the connection issue.</span><span class="sxs-lookup"><span data-stu-id="1e810-106">If you have followed through the more [general SSH troubleshooting steps](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), you need to further troubleshoot the connection issue.</span></span> <span data-ttu-id="1e810-107">This article guides you through detailed troubleshooting steps to determine where the SSH connection is failing and how to resolve it.</span><span class="sxs-lookup"><span data-stu-id="1e810-107">This article guides you through detailed troubleshooting steps to determine where the SSH connection is failing and how to resolve it.</span></span>

## <a name="take-preliminary-steps"></a><span data-ttu-id="1e810-108">Take preliminary steps</span><span class="sxs-lookup"><span data-stu-id="1e810-108">Take preliminary steps</span></span>
<span data-ttu-id="1e810-109">The following diagram shows the components that are involved.</span><span class="sxs-lookup"><span data-stu-id="1e810-109">The following diagram shows the components that are involved.</span></span>

![Diagram that shows components of SSH service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/detailed-troubleshoot-ssh-connection/ssh-tshoot1.png)

<span data-ttu-id="1e810-111">The following steps help you isolate the source of the failure and figure out solutions or workarounds.</span><span class="sxs-lookup"><span data-stu-id="1e810-111">The following steps help you isolate the source of the failure and figure out solutions or workarounds.</span></span>

<span data-ttu-id="1e810-112">First, check the status of the VM in the portal.</span><span class="sxs-lookup"><span data-stu-id="1e810-112">First, check the status of the VM in the portal.</span></span>

<span data-ttu-id="1e810-113">In the [Azure portal](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="1e810-113">In the [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="1e810-114">For VMs created by using the Resource Manager model, select **Virtual machines** > *VM name*.</span><span class="sxs-lookup"><span data-stu-id="1e810-114">For VMs created by using the Resource Manager model, select **Virtual machines** > *VM name*.</span></span>
   
    <span data-ttu-id="1e810-115">-OR-</span><span class="sxs-lookup"><span data-stu-id="1e810-115">-OR-</span></span>
   
    <span data-ttu-id="1e810-116">For VMs created by using the classic deployment model, select **Virtual machines (classic)** > *VM name*.</span><span class="sxs-lookup"><span data-stu-id="1e810-116">For VMs created by using the classic deployment model, select **Virtual machines (classic)** > *VM name*.</span></span>
   
    <span data-ttu-id="1e810-117">The status pane for the VM should show **Running**.</span><span class="sxs-lookup"><span data-stu-id="1e810-117">The status pane for the VM should show **Running**.</span></span> <span data-ttu-id="1e810-118">Scroll down to show recent activity for compute, storage, and network resources.</span><span class="sxs-lookup"><span data-stu-id="1e810-118">Scroll down to show recent activity for compute, storage, and network resources.</span></span>

2. <span data-ttu-id="1e810-119">Select **Settings** to examine endpoints, IP addresses, and other settings.</span><span class="sxs-lookup"><span data-stu-id="1e810-119">Select **Settings** to examine endpoints, IP addresses, and other settings.</span></span>
   
    <span data-ttu-id="1e810-120">To identify endpoints in VMs that were created by using Resource Manager, verify that a [network security group](../../virtual-network/virtual-networks-nsg.md) has been defined.</span><span class="sxs-lookup"><span data-stu-id="1e810-120">To identify endpoints in VMs that were created by using Resource Manager, verify that a [network security group](../../virtual-network/virtual-networks-nsg.md) has been defined.</span></span> <span data-ttu-id="1e810-121">Also verify that the rules have been applied to the network security group and that they're referenced in the subnet.</span><span class="sxs-lookup"><span data-stu-id="1e810-121">Also verify that the rules have been applied to the network security group and that they're referenced in the subnet.</span></span>

<span data-ttu-id="1e810-122">In the [Azure classic portal](https://manage.windowsazure.com), for VMs that were created by using the classic deployment model:</span><span class="sxs-lookup"><span data-stu-id="1e810-122">In the [Azure classic portal](https://manage.windowsazure.com), for VMs that were created by using the classic deployment model:</span></span>

1. <span data-ttu-id="1e810-123">Select **Virtual machines** > *VM name*.</span><span class="sxs-lookup"><span data-stu-id="1e810-123">Select **Virtual machines** > *VM name*.</span></span>
2. <span data-ttu-id="1e810-124">Select the VM's **Dashboard** to check its status.</span><span class="sxs-lookup"><span data-stu-id="1e810-124">Select the VM's **Dashboard** to check its status.</span></span>
3. <span data-ttu-id="1e810-125">Select **Monitor** to see recent activity for compute, storage, and network resources.</span><span class="sxs-lookup"><span data-stu-id="1e810-125">Select **Monitor** to see recent activity for compute, storage, and network resources.</span></span>
4. <span data-ttu-id="1e810-126">Select **Endpoints** to ensure that there is an endpoint for SSH traffic.</span><span class="sxs-lookup"><span data-stu-id="1e810-126">Select **Endpoints** to ensure that there is an endpoint for SSH traffic.</span></span>

<span data-ttu-id="1e810-127">To verify network connectivity, check the configured endpoints and see if you can reach the VM through another protocol, such as HTTP or another service.</span><span class="sxs-lookup"><span data-stu-id="1e810-127">To verify network connectivity, check the configured endpoints and see if you can reach the VM through another protocol, such as HTTP or another service.</span></span>

<span data-ttu-id="1e810-128">After these steps, try the SSH connection again.</span><span class="sxs-lookup"><span data-stu-id="1e810-128">After these steps, try the SSH connection again.</span></span>

## <a name="find-the-source-of-the-issue"></a><span data-ttu-id="1e810-129">Find the source of the issue</span><span class="sxs-lookup"><span data-stu-id="1e810-129">Find the source of the issue</span></span>
<span data-ttu-id="1e810-130">The SSH client on your computer might fail to reach the SSH service on the Azure VM due to issues or misconfigurations in the following areas:</span><span class="sxs-lookup"><span data-stu-id="1e810-130">The SSH client on your computer might fail to reach the SSH service on the Azure VM due to issues or misconfigurations in the following areas:</span></span>

* [<span data-ttu-id="1e810-131">SSH client computer</span><span class="sxs-lookup"><span data-stu-id="1e810-131">SSH client computer</span></span>](#source-1-ssh-client-computer)
* [<span data-ttu-id="1e810-132">Organization edge device</span><span class="sxs-lookup"><span data-stu-id="1e810-132">Organization edge device</span></span>](#source-2-organization-edge-device)
* [<span data-ttu-id="1e810-133">Cloud service endpoint and access control list (ACL)</span><span class="sxs-lookup"><span data-stu-id="1e810-133">Cloud service endpoint and access control list (ACL)</span></span>](#source-3-cloud-service-endpoint-and-acl)
* [<span data-ttu-id="1e810-134">Network security groups</span><span class="sxs-lookup"><span data-stu-id="1e810-134">Network security groups</span></span>](#source-4-network-security-groups)
* [<span data-ttu-id="1e810-135">Linux-based Azure VM</span><span class="sxs-lookup"><span data-stu-id="1e810-135">Linux-based Azure VM</span></span>](#source-5-linux-based-azure-virtual-machine)

## <a name="source-1-ssh-client-computer"></a><span data-ttu-id="1e810-136">Source 1: SSH client computer</span><span class="sxs-lookup"><span data-stu-id="1e810-136">Source 1: SSH client computer</span></span>
<span data-ttu-id="1e810-137">To eliminate your computer as the source of the failure, verify that it can make SSH connections to another on-premises, Linux-based computer.</span><span class="sxs-lookup"><span data-stu-id="1e810-137">To eliminate your computer as the source of the failure, verify that it can make SSH connections to another on-premises, Linux-based computer.</span></span>

![Diagram that highlights SSH client computer components](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/detailed-troubleshoot-ssh-connection/ssh-tshoot2.png)

<span data-ttu-id="1e810-139">If the connection fails, check for the following issues on your computer:</span><span class="sxs-lookup"><span data-stu-id="1e810-139">If the connection fails, check for the following issues on your computer:</span></span>

* <span data-ttu-id="1e810-140">A local firewall setting that is blocking inbound or outbound SSH traffic (TCP 22)</span><span class="sxs-lookup"><span data-stu-id="1e810-140">A local firewall setting that is blocking inbound or outbound SSH traffic (TCP 22)</span></span>
* <span data-ttu-id="1e810-141">Locally installed client proxy software that is preventing SSH connections</span><span class="sxs-lookup"><span data-stu-id="1e810-141">Locally installed client proxy software that is preventing SSH connections</span></span>
* <span data-ttu-id="1e810-142">Locally installed network monitoring software that is preventing SSH connections</span><span class="sxs-lookup"><span data-stu-id="1e810-142">Locally installed network monitoring software that is preventing SSH connections</span></span>
* <span data-ttu-id="1e810-143">Other types of security software that either monitor traffic or allow/disallow specific types of traffic</span><span class="sxs-lookup"><span data-stu-id="1e810-143">Other types of security software that either monitor traffic or allow/disallow specific types of traffic</span></span>

<span data-ttu-id="1e810-144">If one of these conditions apply, temporarily disable the software and try an SSH connection to an on-premises computer to find out the reason the connection is being blocked on your computer.</span><span class="sxs-lookup"><span data-stu-id="1e810-144">If one of these conditions apply, temporarily disable the software and try an SSH connection to an on-premises computer to find out the reason the connection is being blocked on your computer.</span></span> <span data-ttu-id="1e810-145">Then work with your network administrator to correct the software settings to allow SSH connections.</span><span class="sxs-lookup"><span data-stu-id="1e810-145">Then work with your network administrator to correct the software settings to allow SSH connections.</span></span>

<span data-ttu-id="1e810-146">If you are using certificate authentication, verify that you have these permissions to the .ssh folder in your home directory:</span><span class="sxs-lookup"><span data-stu-id="1e810-146">If you are using certificate authentication, verify that you have these permissions to the .ssh folder in your home directory:</span></span>

* <span data-ttu-id="1e810-147">Chmod 700 ~/.ssh</span><span class="sxs-lookup"><span data-stu-id="1e810-147">Chmod 700 ~/.ssh</span></span>
* <span data-ttu-id="1e810-148">Chmod 644 ~/.ssh/\*.pub</span><span class="sxs-lookup"><span data-stu-id="1e810-148">Chmod 644 ~/.ssh/\*.pub</span></span>
* <span data-ttu-id="1e810-149">Chmod 600 ~/.ssh/id_rsa (or any other files that have your private keys stored in them)</span><span class="sxs-lookup"><span data-stu-id="1e810-149">Chmod 600 ~/.ssh/id_rsa (or any other files that have your private keys stored in them)</span></span>
* <span data-ttu-id="1e810-150">Chmod 644 ~/.ssh/known_hosts (contains hosts that you’ve connected to via SSH)</span><span class="sxs-lookup"><span data-stu-id="1e810-150">Chmod 644 ~/.ssh/known_hosts (contains hosts that you’ve connected to via SSH)</span></span>

## <a name="source-2-organization-edge-device"></a><span data-ttu-id="1e810-151">Source 2: Organization edge device</span><span class="sxs-lookup"><span data-stu-id="1e810-151">Source 2: Organization edge device</span></span>
<span data-ttu-id="1e810-152">To eliminate your organization edge device as the source of the failure, verify that a computer that's directly connected to the Internet can make SSH connections to your Azure VM.</span><span class="sxs-lookup"><span data-stu-id="1e810-152">To eliminate your organization edge device as the source of the failure, verify that a computer that's directly connected to the Internet can make SSH connections to your Azure VM.</span></span> <span data-ttu-id="1e810-153">If you are accessing the VM over a site-to-site VPN or an Azure ExpressRoute connection, skip to [Source 4: Network security groups](#nsg).</span><span class="sxs-lookup"><span data-stu-id="1e810-153">If you are accessing the VM over a site-to-site VPN or an Azure ExpressRoute connection, skip to [Source 4: Network security groups](#nsg).</span></span>

![Diagram that highlights organization edge device](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/detailed-troubleshoot-ssh-connection/ssh-tshoot3.png)

<span data-ttu-id="1e810-155">If you don't have a computer that is directly connected to the Internet, create a new Azure VM in its own resource group or cloud service and use it.</span><span class="sxs-lookup"><span data-stu-id="1e810-155">If you don't have a computer that is directly connected to the Internet, create a new Azure VM in its own resource group or cloud service and use it.</span></span> <span data-ttu-id="1e810-156">For more information, see [Create a virtual machine running Linux in Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1e810-156">For more information, see [Create a virtual machine running Linux in Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="1e810-157">Delete the resource group or VM and cloud service when you're done with your testing.</span><span class="sxs-lookup"><span data-stu-id="1e810-157">Delete the resource group or VM and cloud service when you're done with your testing.</span></span>

<span data-ttu-id="1e810-158">If you can create an SSH connection with a computer that's directly connected to the Internet, check your organization edge device for:</span><span class="sxs-lookup"><span data-stu-id="1e810-158">If you can create an SSH connection with a computer that's directly connected to the Internet, check your organization edge device for:</span></span>

* <span data-ttu-id="1e810-159">An internal firewall that's blocking SSH traffic with the Internet</span><span class="sxs-lookup"><span data-stu-id="1e810-159">An internal firewall that's blocking SSH traffic with the Internet</span></span>
* <span data-ttu-id="1e810-160">A proxy server that's preventing SSH connections</span><span class="sxs-lookup"><span data-stu-id="1e810-160">A proxy server that's preventing SSH connections</span></span>
* <span data-ttu-id="1e810-161">Intrusion detection or network monitoring software running on devices in your edge network that's preventing SSH connections</span><span class="sxs-lookup"><span data-stu-id="1e810-161">Intrusion detection or network monitoring software running on devices in your edge network that's preventing SSH connections</span></span>

<span data-ttu-id="1e810-162">Work with your network administrator to correct the settings of your organization edge devices to allow SSH traffic with the Internet.</span><span class="sxs-lookup"><span data-stu-id="1e810-162">Work with your network administrator to correct the settings of your organization edge devices to allow SSH traffic with the Internet.</span></span>

## <a name="source-3-cloud-service-endpoint-and-acl"></a><span data-ttu-id="1e810-163">Source 3: Cloud service endpoint and ACL</span><span class="sxs-lookup"><span data-stu-id="1e810-163">Source 3: Cloud service endpoint and ACL</span></span>
> [!NOTE]
> <span data-ttu-id="1e810-164">This source applies only to VMs that were created by using the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="1e810-164">This source applies only to VMs that were created by using the classic deployment model.</span></span> <span data-ttu-id="1e810-165">For VMs that were created by using Resource Manager, skip to [source 4: Network security groups](#nsg).</span><span class="sxs-lookup"><span data-stu-id="1e810-165">For VMs that were created by using Resource Manager, skip to [source 4: Network security groups](#nsg).</span></span>

<span data-ttu-id="1e810-166">To eliminate the cloud service endpoint and ACL as the source of the failure, verify that another Azure VM in the same virtual network can make SSH connections to your VM.</span><span class="sxs-lookup"><span data-stu-id="1e810-166">To eliminate the cloud service endpoint and ACL as the source of the failure, verify that another Azure VM in the same virtual network can make SSH connections to your VM.</span></span>

![Diagram that highlights cloud service endpoint and ACL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/detailed-troubleshoot-ssh-connection/ssh-tshoot4.png)

<span data-ttu-id="1e810-168">If you don't have another VM in the same virtual network, you can easily create one.</span><span class="sxs-lookup"><span data-stu-id="1e810-168">If you don't have another VM in the same virtual network, you can easily create one.</span></span> <span data-ttu-id="1e810-169">For more information, see [Create a Linux VM on Azure using the CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1e810-169">For more information, see [Create a Linux VM on Azure using the CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="1e810-170">Delete the extra VM when you are done with your testing.</span><span class="sxs-lookup"><span data-stu-id="1e810-170">Delete the extra VM when you are done with your testing.</span></span>

<span data-ttu-id="1e810-171">If you can create an SSH connection with a VM in the same virtual network, check the following areas:</span><span class="sxs-lookup"><span data-stu-id="1e810-171">If you can create an SSH connection with a VM in the same virtual network, check the following areas:</span></span>

* <span data-ttu-id="1e810-172">**The endpoint configuration for SSH traffic on the target VM.**</span><span class="sxs-lookup"><span data-stu-id="1e810-172">**The endpoint configuration for SSH traffic on the target VM.**</span></span> <span data-ttu-id="1e810-173">The private TCP port of the endpoint should match the TCP port on which the SSH service on the VM is listening.</span><span class="sxs-lookup"><span data-stu-id="1e810-173">The private TCP port of the endpoint should match the TCP port on which the SSH service on the VM is listening.</span></span> <span data-ttu-id="1e810-174">(The default port is 22).</span><span class="sxs-lookup"><span data-stu-id="1e810-174">(The default port is 22).</span></span> <span data-ttu-id="1e810-175">For VMs created by using the Resource Manager deployment model, verify the SSH TCP port number in the Azure portal by selecting **Virtual machines** > *VM name* > **Settings** > **Endpoints**.</span><span class="sxs-lookup"><span data-stu-id="1e810-175">For VMs created by using the Resource Manager deployment model, verify the SSH TCP port number in the Azure portal by selecting **Virtual machines** > *VM name* > **Settings** > **Endpoints**.</span></span>
* <span data-ttu-id="1e810-176">**The ACL for the SSH traffic endpoint on the target virtual machine.**</span><span class="sxs-lookup"><span data-stu-id="1e810-176">**The ACL for the SSH traffic endpoint on the target virtual machine.**</span></span> <span data-ttu-id="1e810-177">An ACL enables you to specify allowed or denied incoming traffic from the Internet, based on its source IP address.</span><span class="sxs-lookup"><span data-stu-id="1e810-177">An ACL enables you to specify allowed or denied incoming traffic from the Internet, based on its source IP address.</span></span> <span data-ttu-id="1e810-178">Misconfigured ACLs can prevent incoming SSH traffic to the endpoint.</span><span class="sxs-lookup"><span data-stu-id="1e810-178">Misconfigured ACLs can prevent incoming SSH traffic to the endpoint.</span></span> <span data-ttu-id="1e810-179">Check your ACLs to ensure that incoming traffic from the public IP addresses of your proxy or other edge server is allowed.</span><span class="sxs-lookup"><span data-stu-id="1e810-179">Check your ACLs to ensure that incoming traffic from the public IP addresses of your proxy or other edge server is allowed.</span></span> <span data-ttu-id="1e810-180">For more information, see [About network access control lists (ACLs)](../../virtual-network/virtual-networks-acl.md).</span><span class="sxs-lookup"><span data-stu-id="1e810-180">For more information, see [About network access control lists (ACLs)](../../virtual-network/virtual-networks-acl.md).</span></span>

<span data-ttu-id="1e810-181">To eliminate the endpoint as a source of the problem, remove the current endpoint, create another endpoint, and specify the SSH name (TCP port 22 for the public and private port number).</span><span class="sxs-lookup"><span data-stu-id="1e810-181">To eliminate the endpoint as a source of the problem, remove the current endpoint, create another endpoint, and specify the SSH name (TCP port 22 for the public and private port number).</span></span> <span data-ttu-id="1e810-182">For more information, see [Set up endpoints on a virtual machine in Azure](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1e810-182">For more information, see [Set up endpoints on a virtual machine in Azure](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<a id="nsg"></a>

## <a name="source-4-network-security-groups"></a><span data-ttu-id="1e810-183">Source 4: Network security groups</span><span class="sxs-lookup"><span data-stu-id="1e810-183">Source 4: Network security groups</span></span>
<span data-ttu-id="1e810-184">Network security groups enable you to have more granular control of allowed inbound and outbound traffic.</span><span class="sxs-lookup"><span data-stu-id="1e810-184">Network security groups enable you to have more granular control of allowed inbound and outbound traffic.</span></span> <span data-ttu-id="1e810-185">You can create rules that span subnets and cloud services in an Azure virtual network.</span><span class="sxs-lookup"><span data-stu-id="1e810-185">You can create rules that span subnets and cloud services in an Azure virtual network.</span></span> <span data-ttu-id="1e810-186">Check your network security group rules to ensure that SSH traffic to and from the Internet is allowed.</span><span class="sxs-lookup"><span data-stu-id="1e810-186">Check your network security group rules to ensure that SSH traffic to and from the Internet is allowed.</span></span>
<span data-ttu-id="1e810-187">For more information, see [About network security groups](../../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="1e810-187">For more information, see [About network security groups](../../virtual-network/virtual-networks-nsg.md).</span></span>

## <a name="source-5-linux-based-azure-virtual-machine"></a><span data-ttu-id="1e810-188">Source 5: Linux-based Azure virtual machine</span><span class="sxs-lookup"><span data-stu-id="1e810-188">Source 5: Linux-based Azure virtual machine</span></span>
<span data-ttu-id="1e810-189">The last source of possible problems is the Azure virtual machine itself.</span><span class="sxs-lookup"><span data-stu-id="1e810-189">The last source of possible problems is the Azure virtual machine itself.</span></span>

![Diagram that highlights Linux-based Azure virtual machine](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/detailed-troubleshoot-ssh-connection/ssh-tshoot5.png)

<span data-ttu-id="1e810-191">If you haven't done so already, follow the instructions [to reset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1e810-191">If you haven't done so already, follow the instructions [to reset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="1e810-192">Try connecting from your computer again.</span><span class="sxs-lookup"><span data-stu-id="1e810-192">Try connecting from your computer again.</span></span> <span data-ttu-id="1e810-193">If it still fails, the following are some of the possible issues:</span><span class="sxs-lookup"><span data-stu-id="1e810-193">If it still fails, the following are some of the possible issues:</span></span>

* <span data-ttu-id="1e810-194">The SSH service is not running on the target virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1e810-194">The SSH service is not running on the target virtual machine.</span></span>
* <span data-ttu-id="1e810-195">The SSH service is not listening on TCP port 22.</span><span class="sxs-lookup"><span data-stu-id="1e810-195">The SSH service is not listening on TCP port 22.</span></span> <span data-ttu-id="1e810-196">To test, install a telnet client on your local computer and run "telnet *cloudServiceName*.cloudapp.net 22".</span><span class="sxs-lookup"><span data-stu-id="1e810-196">To test, install a telnet client on your local computer and run "telnet *cloudServiceName*.cloudapp.net 22".</span></span> <span data-ttu-id="1e810-197">This step determines if the virtual machine allows inbound and outbound communication to the SSH endpoint.</span><span class="sxs-lookup"><span data-stu-id="1e810-197">This step determines if the virtual machine allows inbound and outbound communication to the SSH endpoint.</span></span>
* <span data-ttu-id="1e810-198">The local firewall on the target virtual machine has rules that are preventing inbound or outbound SSH traffic.</span><span class="sxs-lookup"><span data-stu-id="1e810-198">The local firewall on the target virtual machine has rules that are preventing inbound or outbound SSH traffic.</span></span>
* <span data-ttu-id="1e810-199">Intrusion detection or network monitoring software that's running on the Azure virtual machine is preventing SSH connections.</span><span class="sxs-lookup"><span data-stu-id="1e810-199">Intrusion detection or network monitoring software that's running on the Azure virtual machine is preventing SSH connections.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1e810-200">Additional resources</span><span class="sxs-lookup"><span data-stu-id="1e810-200">Additional resources</span></span>
<span data-ttu-id="1e810-201">For more information about troubleshooting application access, see [Troubleshoot access to an application running on an Azure virtual machine](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="1e810-201">For more information about troubleshooting application access, see [Troubleshoot access to an application running on an Azure virtual machine](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>






