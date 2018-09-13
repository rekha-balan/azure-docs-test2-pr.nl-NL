---
title: Connect HDInsight to your on-premises network - Azure HDInsight
description: Learn how to create an HDInsight cluster in an Azure Virtual Network, and then connect it to your on-premises network. Learn how to configure name resolution between HDInsight and your on-premises network by using a custom DNS server.
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 02/23/2018
ms.author: jasonh
ms.openlocfilehash: b8ff139e3cf9fbadbee6eb2c371b30cde6f6de29
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871438"
---
# <a name="connect-hdinsight-to-your-on-premises-network"></a><span data-ttu-id="dbfc4-104">Connect HDInsight to your on-premises network</span><span class="sxs-lookup"><span data-stu-id="dbfc4-104">Connect HDInsight to your on-premises network</span></span>

<span data-ttu-id="dbfc4-105">Learn how to connect HDInsight to your on-premises network by using Azure Virtual Networks and a VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-105">Learn how to connect HDInsight to your on-premises network by using Azure Virtual Networks and a VPN gateway.</span></span> <span data-ttu-id="dbfc4-106">This document provides planning information on:</span><span class="sxs-lookup"><span data-stu-id="dbfc4-106">This document provides planning information on:</span></span>

* <span data-ttu-id="dbfc4-107">Using HDInsight in an Azure Virtual Network that connects to your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-107">Using HDInsight in an Azure Virtual Network that connects to your on-premises network.</span></span>

* <span data-ttu-id="dbfc4-108">Configuring DNS name resolution between the virtual network and your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-108">Configuring DNS name resolution between the virtual network and your on-premises network.</span></span>

* <span data-ttu-id="dbfc4-109">Configuring network security groups to restrict internet access to HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-109">Configuring network security groups to restrict internet access to HDInsight.</span></span>

* <span data-ttu-id="dbfc4-110">Ports provided by HDInsight on the virtual network.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-110">Ports provided by HDInsight on the virtual network.</span></span>

## <a name="create-the-virtual-network-configuration"></a><span data-ttu-id="dbfc4-111">Create the Virtual network configuration</span><span class="sxs-lookup"><span data-stu-id="dbfc4-111">Create the Virtual network configuration</span></span>

<span data-ttu-id="dbfc4-112">Use the following documents to learn how to create an Azure Virtual Network that is connected to your on-premises network:</span><span class="sxs-lookup"><span data-stu-id="dbfc4-112">Use the following documents to learn how to create an Azure Virtual Network that is connected to your on-premises network:</span></span>
    
* [<span data-ttu-id="dbfc4-113">Using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="dbfc4-113">Using the Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

* [<span data-ttu-id="dbfc4-114">Using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="dbfc4-114">Using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

* [<span data-ttu-id="dbfc4-115">Using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="dbfc4-115">Using Azure CLI</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="configure-name-resolution"></a><span data-ttu-id="dbfc4-116">Configure name resolution</span><span class="sxs-lookup"><span data-stu-id="dbfc4-116">Configure name resolution</span></span>

<span data-ttu-id="dbfc4-117">To allow HDInsight and resources in the joined network to communicate by name, you must perform the following actions:</span><span class="sxs-lookup"><span data-stu-id="dbfc4-117">To allow HDInsight and resources in the joined network to communicate by name, you must perform the following actions:</span></span>

* <span data-ttu-id="dbfc4-118">Create a custom DNS server in the Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-118">Create a custom DNS server in the Azure Virtual Network.</span></span>

* <span data-ttu-id="dbfc4-119">Configure the virtual network to use the custom DNS server instead of the default Azure Recursive Resolver.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-119">Configure the virtual network to use the custom DNS server instead of the default Azure Recursive Resolver.</span></span>

* <span data-ttu-id="dbfc4-120">Configure forwarding between the custom DNS server and your on-premises DNS server.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-120">Configure forwarding between the custom DNS server and your on-premises DNS server.</span></span>

<span data-ttu-id="dbfc4-121">This configuration enables the following behavior:</span><span class="sxs-lookup"><span data-stu-id="dbfc4-121">This configuration enables the following behavior:</span></span>

* <span data-ttu-id="dbfc4-122">Requests for fully qualified domain names that have the DNS suffix __for the virtual network__ are forwarded to the custom DNS server.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-122">Requests for fully qualified domain names that have the DNS suffix __for the virtual network__ are forwarded to the custom DNS server.</span></span> <span data-ttu-id="dbfc4-123">The custom DNS server then forwards these requests to the Azure Recursive Resolver, which returns the IP address.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-123">The custom DNS server then forwards these requests to the Azure Recursive Resolver, which returns the IP address.</span></span>

* <span data-ttu-id="dbfc4-124">All other requests are forwarded to the on-premises DNS server.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-124">All other requests are forwarded to the on-premises DNS server.</span></span> <span data-ttu-id="dbfc4-125">Even requests for public internet resources such as microsoft.com are forwarded to the on-premises DNS server for name resolution.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-125">Even requests for public internet resources such as microsoft.com are forwarded to the on-premises DNS server for name resolution.</span></span>

<span data-ttu-id="dbfc4-126">In the following diagram, green lines are requests for resources that end in the DNS suffix of the virtual network.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-126">In the following diagram, green lines are requests for resources that end in the DNS suffix of the virtual network.</span></span> <span data-ttu-id="dbfc4-127">Blue lines are requests for resources in the on-premises network or on the public internet.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-127">Blue lines are requests for resources in the on-premises network or on the public internet.</span></span>

![Diagram of how DNS requests are resolved in the configuration used in this document](./media/connect-on-premises-network/on-premises-to-cloud-dns.png)

### <a name="create-a-custom-dns-server"></a><span data-ttu-id="dbfc4-129">Create a custom DNS server</span><span class="sxs-lookup"><span data-stu-id="dbfc4-129">Create a custom DNS server</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dbfc4-130">You must create and configure the DNS server before installing HDInsight into the virtual network.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-130">You must create and configure the DNS server before installing HDInsight into the virtual network.</span></span>

<span data-ttu-id="dbfc4-131">To create a Linux VM that uses the [Bind](https://www.isc.org/downloads/bind/) DNS software, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="dbfc4-131">To create a Linux VM that uses the [Bind](https://www.isc.org/downloads/bind/) DNS software, use the following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="dbfc4-132">The following steps use the [Azure portal](https://portal.azure.com) to create an Azure Virtual Machine.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-132">The following steps use the [Azure portal](https://portal.azure.com) to create an Azure Virtual Machine.</span></span> <span data-ttu-id="dbfc4-133">For other ways to create a virtual machine, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="dbfc4-133">For other ways to create a virtual machine, see the following documents:</span></span>
>
> * [<span data-ttu-id="dbfc4-134">Create VM - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="dbfc4-134">Create VM - Azure CLI</span></span>](../virtual-machines/linux/quick-create-cli.md)
> * [<span data-ttu-id="dbfc4-135">Create VM - Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="dbfc4-135">Create VM - Azure PowerShell</span></span>](../virtual-machines/linux/quick-create-portal.md)

1. <span data-ttu-id="dbfc4-136">From the [Azure portal](https://portal.azure.com), select __+__, __Compute__, and __Ubuntu Server 16.04 LTS__.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-136">From the [Azure portal](https://portal.azure.com), select __+__, __Compute__, and __Ubuntu Server 16.04 LTS__.</span></span>

    ![Create an Ubuntu virtual machine](./media/connect-on-premises-network/create-ubuntu-vm.png)

2. <span data-ttu-id="dbfc4-138">From the __Basics__ section, enter the following information:</span><span class="sxs-lookup"><span data-stu-id="dbfc4-138">From the __Basics__ section, enter the following information:</span></span>

    * <span data-ttu-id="dbfc4-139">__Name__: A friendly name that identifies this virtual machine.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-139">__Name__: A friendly name that identifies this virtual machine.</span></span> <span data-ttu-id="dbfc4-140">For example, __DNSProxy__.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-140">For example, __DNSProxy__.</span></span>
    * <span data-ttu-id="dbfc4-141">__User name__: The name of the SSH account.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-141">__User name__: The name of the SSH account.</span></span>
    * <span data-ttu-id="dbfc4-142">__SSH public key__ or __Password__: The authentication method for the SSH account.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-142">__SSH public key__ or __Password__: The authentication method for the SSH account.</span></span> <span data-ttu-id="dbfc4-143">We recommend using public keys, as they are more secure.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-143">We recommend using public keys, as they are more secure.</span></span> <span data-ttu-id="dbfc4-144">For more information, see the [Create and use SSH keys for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md) document.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-144">For more information, see the [Create and use SSH keys for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md) document.</span></span>
    * <span data-ttu-id="dbfc4-145">__Resource group__: Select __Use existing__, and then select the resource group that contains the virtual network created earlier.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-145">__Resource group__: Select __Use existing__, and then select the resource group that contains the virtual network created earlier.</span></span>
    * <span data-ttu-id="dbfc4-146">__Location__: Select the same location as the virtual network.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-146">__Location__: Select the same location as the virtual network.</span></span>

    ![Virtual machine basic configuration](./media/connect-on-premises-network/vm-basics.png)

    <span data-ttu-id="dbfc4-148">Leave other entries at the default values and then select __OK__.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-148">Leave other entries at the default values and then select __OK__.</span></span>

3. <span data-ttu-id="dbfc4-149">From the __Choose a size__ section, select the VM size.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-149">From the __Choose a size__ section, select the VM size.</span></span> <span data-ttu-id="dbfc4-150">For this tutorial, select the smallest and lowest cost option.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-150">For this tutorial, select the smallest and lowest cost option.</span></span> <span data-ttu-id="dbfc4-151">To continue, use the __Select__ button.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-151">To continue, use the __Select__ button.</span></span>

4. <span data-ttu-id="dbfc4-152">From the __Settings__ section, enter the following information:</span><span class="sxs-lookup"><span data-stu-id="dbfc4-152">From the __Settings__ section, enter the following information:</span></span>

    * <span data-ttu-id="dbfc4-153">__Virtual network__: Select the virtual network that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-153">__Virtual network__: Select the virtual network that you created earlier.</span></span>

    * <span data-ttu-id="dbfc4-154">__Subnet__: Select the default subnet for the virtual network.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-154">__Subnet__: Select the default subnet for the virtual network.</span></span> <span data-ttu-id="dbfc4-155">Do __not__ select the subnet used by the VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-155">Do __not__ select the subnet used by the VPN gateway.</span></span>

    * <span data-ttu-id="dbfc4-156">__Diagnostics storage account__: Either select an existing storage account or create a new one.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-156">__Diagnostics storage account__: Either select an existing storage account or create a new one.</span></span>

    ![Virtual network settings](./media/connect-on-premises-network/virtual-network-settings.png)

    <span data-ttu-id="dbfc4-158">Leave the other entries at the default value, then select __OK__ to continue.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-158">Leave the other entries at the default value, then select __OK__ to continue.</span></span>

5. <span data-ttu-id="dbfc4-159">From the __Purchase__ section, select the __Purchase__ button to create the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-159">From the __Purchase__ section, select the __Purchase__ button to create the virtual machine.</span></span>

6. <span data-ttu-id="dbfc4-160">Once the virtual machine has been created, its __Overview__ section is displayed.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-160">Once the virtual machine has been created, its __Overview__ section is displayed.</span></span> <span data-ttu-id="dbfc4-161">From the list on the left, select __Properties__.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-161">From the list on the left, select __Properties__.</span></span> <span data-ttu-id="dbfc4-162">Save the __Public IP address__ and __Private IP address__ values.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-162">Save the __Public IP address__ and __Private IP address__ values.</span></span> <span data-ttu-id="dbfc4-163">It will be used in the next section.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-163">It will be used in the next section.</span></span>

    ![Public and private IP addresses](./media/connect-on-premises-network/vm-ip-addresses.png)

### <a name="install-and-configure-bind-dns-software"></a><span data-ttu-id="dbfc4-165">Install and configure Bind (DNS software)</span><span class="sxs-lookup"><span data-stu-id="dbfc4-165">Install and configure Bind (DNS software)</span></span>

1. <span data-ttu-id="dbfc4-166">Use SSH to connect to the __public IP address__ of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-166">Use SSH to connect to the __public IP address__ of the virtual machine.</span></span> <span data-ttu-id="dbfc4-167">The following example connects to a virtual machine at 40.68.254.142:</span><span class="sxs-lookup"><span data-stu-id="dbfc4-167">The following example connects to a virtual machine at 40.68.254.142:</span></span>

    ```bash
    ssh sshuser@40.68.254.142
    ```

    <span data-ttu-id="dbfc4-168">Replace `sshuser` with the SSH user account you specified when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-168">Replace `sshuser` with the SSH user account you specified when creating the cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="dbfc4-169">There are a variety of ways to obtain the `ssh` utility.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-169">There are a variety of ways to obtain the `ssh` utility.</span></span> <span data-ttu-id="dbfc4-170">On Linux, Unix, and macOS, it is provided as part of the operating system.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-170">On Linux, Unix, and macOS, it is provided as part of the operating system.</span></span> <span data-ttu-id="dbfc4-171">If you are using Windows, consider one of the following options:</span><span class="sxs-lookup"><span data-stu-id="dbfc4-171">If you are using Windows, consider one of the following options:</span></span>
    >
    > * [<span data-ttu-id="dbfc4-172">Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="dbfc4-172">Azure Cloud Shell</span></span>](../cloud-shell/quickstart.md)
    > * [<span data-ttu-id="dbfc4-173">Bash on Ubuntu on Windows 10</span><span class="sxs-lookup"><span data-stu-id="dbfc4-173">Bash on Ubuntu on Windows 10</span></span>](https://msdn.microsoft.com/commandline/wsl/about)
    > * [<span data-ttu-id="dbfc4-174">Git (https://git-scm.com/)</span><span class="sxs-lookup"><span data-stu-id="dbfc4-174">Git (https://git-scm.com/)</span></span>](https://git-scm.com/)
    > * [<span data-ttu-id="dbfc4-175">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span><span class="sxs-lookup"><span data-stu-id="dbfc4-175">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span></span>](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

2. <span data-ttu-id="dbfc4-176">To install Bind, use the following commands from the SSH session:</span><span class="sxs-lookup"><span data-stu-id="dbfc4-176">To install Bind, use the following commands from the SSH session:</span></span>

    ```bash
    sudo apt-get update -y
    sudo apt-get install bind9 -y
    ```

3. <span data-ttu-id="dbfc4-177">To configure Bind to forward name resolution requests to your on-prem DNS server, use the following text as the contents of the `/etc/bind/named.conf.options` file:</span><span class="sxs-lookup"><span data-stu-id="dbfc4-177">To configure Bind to forward name resolution requests to your on-prem DNS server, use the following text as the contents of the `/etc/bind/named.conf.options` file:</span></span>

        acl goodclients {
            10.0.0.0/16; # Replace with the IP address range of the virtual network
            10.1.0.0/16; # Replace with the IP address range of the on-premises network
            localhost;
            localnets;
        };

        options {
                directory "/var/cache/bind";

                recursion yes;

                allow-query { goodclients; };

                forwarders {
                192.168.0.1; # Replace with the IP address of the on-premises DNS server
                };

                dnssec-validation auto;

                auth-nxdomain no;    # conform to RFC1035
                listen-on { any; };
        };

    > [!IMPORTANT]
    > <span data-ttu-id="dbfc4-178">Replace the values in the `goodclients` section with the IP address range of the virtual network and on-premises network.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-178">Replace the values in the `goodclients` section with the IP address range of the virtual network and on-premises network.</span></span> <span data-ttu-id="dbfc4-179">This section defines the addresses that this DNS server accepts requests from.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-179">This section defines the addresses that this DNS server accepts requests from.</span></span>
    >
    > <span data-ttu-id="dbfc4-180">Replace the `192.168.0.1` entry in the `forwarders` section with the IP address of your on-premises DNS server.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-180">Replace the `192.168.0.1` entry in the `forwarders` section with the IP address of your on-premises DNS server.</span></span> <span data-ttu-id="dbfc4-181">This entry routes DNS requests to your on-premises DNS server for resolution.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-181">This entry routes DNS requests to your on-premises DNS server for resolution.</span></span>

    <span data-ttu-id="dbfc4-182">To edit this file, use the following command:</span><span class="sxs-lookup"><span data-stu-id="dbfc4-182">To edit this file, use the following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.options
    ```

    <span data-ttu-id="dbfc4-183">To save the file, use __Ctrl+X__, __Y__, and then __Enter__.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-183">To save the file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

4. <span data-ttu-id="dbfc4-184">From the SSH session, use the following command:</span><span class="sxs-lookup"><span data-stu-id="dbfc4-184">From the SSH session, use the following command:</span></span>

    ```bash
    hostname -f
    ```

    <span data-ttu-id="dbfc4-185">This command returns a value similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="dbfc4-185">This command returns a value similar to the following text:</span></span>

        dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net

    <span data-ttu-id="dbfc4-186">The `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` text is the __DNS suffix__ for this virtual network.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-186">The `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` text is the __DNS suffix__ for this virtual network.</span></span> <span data-ttu-id="dbfc4-187">Save this value, as it is used later.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-187">Save this value, as it is used later.</span></span>

5. <span data-ttu-id="dbfc4-188">To configure Bind to resolve DNS names for resources within the virtual network, use the following text as the contents of the `/etc/bind/named.conf.local` file:</span><span class="sxs-lookup"><span data-stu-id="dbfc4-188">To configure Bind to resolve DNS names for resources within the virtual network, use the following text as the contents of the `/etc/bind/named.conf.local` file:</span></span>

        // Replace the following with the DNS suffix for your virtual network
        zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
            type forward;
            forwarders {168.63.129.16;}; # The Azure recursive resolver
        };

    > [!IMPORTANT]
    > <span data-ttu-id="dbfc4-189">You must replace the `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` with the DNS suffix you retrieved earlier.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-189">You must replace the `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` with the DNS suffix you retrieved earlier.</span></span>

    <span data-ttu-id="dbfc4-190">To edit this file, use the following command:</span><span class="sxs-lookup"><span data-stu-id="dbfc4-190">To edit this file, use the following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.local
    ```

    <span data-ttu-id="dbfc4-191">To save the file, use __Ctrl+X__, __Y__, and then __Enter__.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-191">To save the file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

6. <span data-ttu-id="dbfc4-192">To start Bind, use the following command:</span><span class="sxs-lookup"><span data-stu-id="dbfc4-192">To start Bind, use the following command:</span></span>

    ```bash
    sudo service bind9 restart
    ```

7. <span data-ttu-id="dbfc4-193">To verify that bind can resolve the names of resources in your on-premises network, use the following commands:</span><span class="sxs-lookup"><span data-stu-id="dbfc4-193">To verify that bind can resolve the names of resources in your on-premises network, use the following commands:</span></span>

    ```bash
    sudo apt install dnsutils
    nslookup dns.mynetwork.net 10.0.0.4
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="dbfc4-194">Replace `dns.mynetwork.net` with the fully qualified domain name (FQDN) of a resource in your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-194">Replace `dns.mynetwork.net` with the fully qualified domain name (FQDN) of a resource in your on-premises network.</span></span>
    >
    > <span data-ttu-id="dbfc4-195">Replace `10.0.0.4` with the __internal IP address__ of your custom DNS server in the virtual network.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-195">Replace `10.0.0.4` with the __internal IP address__ of your custom DNS server in the virtual network.</span></span>

    <span data-ttu-id="dbfc4-196">The response appears similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="dbfc4-196">The response appears similar to the following text:</span></span>

        Server:         10.0.0.4
        Address:        10.0.0.4#53

        Non-authoritative answer:
        Name:   dns.mynetwork.net
        Address: 192.168.0.4

### <a name="configure-the-virtual-network-to-use-the-custom-dns-server"></a><span data-ttu-id="dbfc4-197">Configure the virtual network to use the custom DNS server</span><span class="sxs-lookup"><span data-stu-id="dbfc4-197">Configure the virtual network to use the custom DNS server</span></span>

<span data-ttu-id="dbfc4-198">To configure the virtual network to use the custom DNS server instead of the Azure recursive resolver, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="dbfc4-198">To configure the virtual network to use the custom DNS server instead of the Azure recursive resolver, use the following steps:</span></span>

1. <span data-ttu-id="dbfc4-199">In the [Azure portal](https://portal.azure.com), select the virtual network, and then select __DNS Servers__.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-199">In the [Azure portal](https://portal.azure.com), select the virtual network, and then select __DNS Servers__.</span></span>

2. <span data-ttu-id="dbfc4-200">Select __Custom__, and enter the __internal IP address__ of the custom DNS server.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-200">Select __Custom__, and enter the __internal IP address__ of the custom DNS server.</span></span> <span data-ttu-id="dbfc4-201">Finally, select __Save__.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-201">Finally, select __Save__.</span></span>

    ![Set the custom DNS server for the network](./media/connect-on-premises-network/configure-custom-dns.png)

### <a name="configure-the-on-premises-dns-server"></a><span data-ttu-id="dbfc4-203">Configure the on-premises DNS server</span><span class="sxs-lookup"><span data-stu-id="dbfc4-203">Configure the on-premises DNS server</span></span>

<span data-ttu-id="dbfc4-204">In the previous section, you configured the custom DNS server to forward requests to the on-premises DNS server.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-204">In the previous section, you configured the custom DNS server to forward requests to the on-premises DNS server.</span></span> <span data-ttu-id="dbfc4-205">Next, you must configure the on-premises DNS server to forward requests to the custom DNS server.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-205">Next, you must configure the on-premises DNS server to forward requests to the custom DNS server.</span></span>

<span data-ttu-id="dbfc4-206">For specific steps on how to configure your DNS server, consult the documentation for your DNS server software.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-206">For specific steps on how to configure your DNS server, consult the documentation for your DNS server software.</span></span> <span data-ttu-id="dbfc4-207">Look for the steps on how to configure a __conditional forwarder__.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-207">Look for the steps on how to configure a __conditional forwarder__.</span></span>

<span data-ttu-id="dbfc4-208">A conditional forward only forwards requests for a specific DNS suffix.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-208">A conditional forward only forwards requests for a specific DNS suffix.</span></span> <span data-ttu-id="dbfc4-209">In this case, you must configure a forwarder for the DNS suffix of the virtual network.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-209">In this case, you must configure a forwarder for the DNS suffix of the virtual network.</span></span> <span data-ttu-id="dbfc4-210">Requests for this suffix should be forwarded to the IP address of the custom DNS server.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-210">Requests for this suffix should be forwarded to the IP address of the custom DNS server.</span></span> 

<span data-ttu-id="dbfc4-211">The following text is an example of a conditional forwarder configuration for the **Bind** DNS software:</span><span class="sxs-lookup"><span data-stu-id="dbfc4-211">The following text is an example of a conditional forwarder configuration for the **Bind** DNS software:</span></span>

    zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # The custom DNS server's internal IP address
    };

<span data-ttu-id="dbfc4-212">For information on using DNS on **Windows Server 2016**, see the [Add-DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) documentation...</span><span class="sxs-lookup"><span data-stu-id="dbfc4-212">For information on using DNS on **Windows Server 2016**, see the [Add-DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) documentation...</span></span>

<span data-ttu-id="dbfc4-213">Once you have configured the on-premises DNS server, you can use `nslookup` from the on-premises network to verify that you can resolve names in the virtual network.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-213">Once you have configured the on-premises DNS server, you can use `nslookup` from the on-premises network to verify that you can resolve names in the virtual network.</span></span> <span data-ttu-id="dbfc4-214">The following example</span><span class="sxs-lookup"><span data-stu-id="dbfc4-214">The following example</span></span> 

```bash
nslookup dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net 196.168.0.4
```

<span data-ttu-id="dbfc4-215">This example uses the on-premises DNS server at 196.168.0.4 to resolve the name of the custom DNS server.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-215">This example uses the on-premises DNS server at 196.168.0.4 to resolve the name of the custom DNS server.</span></span> <span data-ttu-id="dbfc4-216">Replace the IP address with the one for the on-premises DNS server.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-216">Replace the IP address with the one for the on-premises DNS server.</span></span> <span data-ttu-id="dbfc4-217">Replace the `dnsproxy` address with the fully qualified domain name of the custom DNS server.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-217">Replace the `dnsproxy` address with the fully qualified domain name of the custom DNS server.</span></span>

## <a name="optional-control-network-traffic"></a><span data-ttu-id="dbfc4-218">Optional: Control network traffic</span><span class="sxs-lookup"><span data-stu-id="dbfc4-218">Optional: Control network traffic</span></span>

<span data-ttu-id="dbfc4-219">You can use network security groups (NSG) or user-defined routes (UDR) to control network traffic.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-219">You can use network security groups (NSG) or user-defined routes (UDR) to control network traffic.</span></span> <span data-ttu-id="dbfc4-220">NSGs allow you to filter inbound and outbound traffic, and allow or deny the traffic.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-220">NSGs allow you to filter inbound and outbound traffic, and allow or deny the traffic.</span></span> <span data-ttu-id="dbfc4-221">UDRs allow you to control how traffic flows between resources in the virtual network, the internet, and the on-premises network.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-221">UDRs allow you to control how traffic flows between resources in the virtual network, the internet, and the on-premises network.</span></span>

> [!WARNING]
> <span data-ttu-id="dbfc4-222">HDInsight requires inbound access from specific IP addresses in the Azure cloud, and unrestricted outbound access.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-222">HDInsight requires inbound access from specific IP addresses in the Azure cloud, and unrestricted outbound access.</span></span> <span data-ttu-id="dbfc4-223">When using NSGs or UDRs to control traffic, you must perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="dbfc4-223">When using NSGs or UDRs to control traffic, you must perform the following steps:</span></span>

1. <span data-ttu-id="dbfc4-224">Find the IP addresses for the location that contains your virtual network.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-224">Find the IP addresses for the location that contains your virtual network.</span></span> <span data-ttu-id="dbfc4-225">For a list of required IPs by location, see [Required IP addresses](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span><span class="sxs-lookup"><span data-stu-id="dbfc4-225">For a list of required IPs by location, see [Required IP addresses](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span></span>

2. <span data-ttu-id="dbfc4-226">For the IP addresses identified in step 1, allow inbound traffic from that IP addresses.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-226">For the IP addresses identified in step 1, allow inbound traffic from that IP addresses.</span></span>

   * <span data-ttu-id="dbfc4-227">If you are using __NSG__: Allow __inbound__ traffic on port __443__ for the IP addresses.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-227">If you are using __NSG__: Allow __inbound__ traffic on port __443__ for the IP addresses.</span></span>
   * <span data-ttu-id="dbfc4-228">If you are using __UDR__: Set the __Next Hop__ type of the route to __Internet__ for the IP addresses.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-228">If you are using __UDR__: Set the __Next Hop__ type of the route to __Internet__ for the IP addresses.</span></span>

<span data-ttu-id="dbfc4-229">For an example of using Azure PowerShell or the Azure CLI to create NSGs, see the [Extend HDInsight with Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) document.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-229">For an example of using Azure PowerShell or the Azure CLI to create NSGs, see the [Extend HDInsight with Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) document.</span></span>

## <a name="create-the-hdinsight-cluster"></a><span data-ttu-id="dbfc4-230">Create the HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="dbfc4-230">Create the HDInsight cluster</span></span>

> [!WARNING]
> <span data-ttu-id="dbfc4-231">You must configure the custom DNS server before installing HDInsight in the virtual network.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-231">You must configure the custom DNS server before installing HDInsight in the virtual network.</span></span>

<span data-ttu-id="dbfc4-232">Use the steps in the [Create an HDInsight cluster using the Azure portal](./hdinsight-hadoop-create-linux-clusters-portal.md) document to create an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-232">Use the steps in the [Create an HDInsight cluster using the Azure portal](./hdinsight-hadoop-create-linux-clusters-portal.md) document to create an HDInsight cluster.</span></span>

> [!WARNING]
> * <span data-ttu-id="dbfc4-233">During cluster creation, you must choose the location that contains your virtual network.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-233">During cluster creation, you must choose the location that contains your virtual network.</span></span>
>
> * <span data-ttu-id="dbfc4-234">In the __Advanced settings__ part of configuration, you must select the virtual network and subnet that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-234">In the __Advanced settings__ part of configuration, you must select the virtual network and subnet that you created earlier.</span></span>

## <a name="connecting-to-hdinsight"></a><span data-ttu-id="dbfc4-235">Connecting to HDInsight</span><span class="sxs-lookup"><span data-stu-id="dbfc4-235">Connecting to HDInsight</span></span>

<span data-ttu-id="dbfc4-236">Most documentation on HDInsight assumes that you have access to the cluster over the internet.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-236">Most documentation on HDInsight assumes that you have access to the cluster over the internet.</span></span> <span data-ttu-id="dbfc4-237">For example, that you can connect to the cluster at https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-237">For example, that you can connect to the cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="dbfc4-238">This address uses the public gateway, which is not available if you have used NSGs or UDRs to restrict access from the internet.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-238">This address uses the public gateway, which is not available if you have used NSGs or UDRs to restrict access from the internet.</span></span>

<span data-ttu-id="dbfc4-239">Some documentation also references `headnodehost` when connecting to the cluster from an SSH session.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-239">Some documentation also references `headnodehost` when connecting to the cluster from an SSH session.</span></span> <span data-ttu-id="dbfc4-240">This address is only available from nodes within a cluster, and is not usable on clients connected over the virtual network.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-240">This address is only available from nodes within a cluster, and is not usable on clients connected over the virtual network.</span></span>

<span data-ttu-id="dbfc4-241">To directly connect to HDInsight through the virtual network, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="dbfc4-241">To directly connect to HDInsight through the virtual network, use the following steps:</span></span>

1. <span data-ttu-id="dbfc4-242">To discover the internal fully qualified domain names of the HDInsight cluster nodes, use one of the following methods:</span><span class="sxs-lookup"><span data-stu-id="dbfc4-242">To discover the internal fully qualified domain names of the HDInsight cluster nodes, use one of the following methods:</span></span>

    ```powershell
    $resourceGroupName = "The resource group that contains the virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

2. <span data-ttu-id="dbfc4-243">To determine the port that a service is available on, see the [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-243">To determine the port that a service is available on, see the [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="dbfc4-244">Some services hosted on the head nodes are only active on one node at a time.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-244">Some services hosted on the head nodes are only active on one node at a time.</span></span> <span data-ttu-id="dbfc4-245">If you try accessing a service on one head node and it fails, switch to the other head node.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-245">If you try accessing a service on one head node and it fails, switch to the other head node.</span></span>
    >
    > <span data-ttu-id="dbfc4-246">For example, Ambari is only active on one head node at a time.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-246">For example, Ambari is only active on one head node at a time.</span></span> <span data-ttu-id="dbfc4-247">If you try accessing Ambari on one head node and it returns a 404 error, then it is running on the other head node.</span><span class="sxs-lookup"><span data-stu-id="dbfc4-247">If you try accessing Ambari on one head node and it returns a 404 error, then it is running on the other head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dbfc4-248">Next steps</span><span class="sxs-lookup"><span data-stu-id="dbfc4-248">Next steps</span></span>

* <span data-ttu-id="dbfc4-249">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="dbfc4-249">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

* <span data-ttu-id="dbfc4-250">For more information on Azure virtual networks, see the [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dbfc4-250">For more information on Azure virtual networks, see the [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="dbfc4-251">For more information on network security groups, see [Network security groups](../virtual-network/security-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dbfc4-251">For more information on network security groups, see [Network security groups](../virtual-network/security-overview.md).</span></span>

* <span data-ttu-id="dbfc4-252">For more information on user-defined routes, see [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dbfc4-252">For more information on user-defined routes, see [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>
