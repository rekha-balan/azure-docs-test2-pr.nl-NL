---
title: Connect to a SQL Server Virtual Machine (Resource Manager) | Microsoft Docs
description: Learn how to connect to SQL Server running on a Virtual Machine in Azure. This topic uses the classic deployment model. The scenarios differ depending on the networking configuration and the location of the client.
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.assetid: aa5bf144-37a3-4781-892d-e0e300913d03
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 02/28/2017
ms.author: jroth
ms.openlocfilehash: 6e6b4d32612e71a67eb108f1837f9f631640e3d3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551379"
---
# <a name="connect-to-a-sql-server-virtual-machine-on-azure-resource-manager"></a><span data-ttu-id="67c6f-105">Connect to a SQL Server Virtual Machine on Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="67c6f-105">Connect to a SQL Server Virtual Machine on Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager](virtual-machines-windows-sql-connect.md)
> * [Classic](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="67c6f-108">Overview</span><span class="sxs-lookup"><span data-stu-id="67c6f-108">Overview</span></span>
<span data-ttu-id="67c6f-109">This topic describes how to connect to your SQL Server instance running on an Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="67c6f-109">This topic describes how to connect to your SQL Server instance running on an Azure virtual machine.</span></span> <span data-ttu-id="67c6f-110">It covers some [general connectivity scenarios](#connection-scenarios) and then provides [detailed steps for configuring SQL Server connectivity in an Azure VM](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="67c6f-110">It covers some [general connectivity scenarios](#connection-scenarios) and then provides [detailed steps for configuring SQL Server connectivity in an Azure VM](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="67c6f-111">To view the classic version of this article, see [Connect to a SQL Server Virtual Machine on Azure Classic](../classic/sql-connect.md).</span><span class="sxs-lookup"><span data-stu-id="67c6f-111">To view the classic version of this article, see [Connect to a SQL Server Virtual Machine on Azure Classic](../classic/sql-connect.md).</span></span>

<span data-ttu-id="67c6f-112">If you would rather have a full walk-through of both provisioning and connectivity, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="67c6f-112">If you would rather have a full walk-through of both provisioning and connectivity, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="connection-scenarios"></a><span data-ttu-id="67c6f-113">Connection scenarios</span><span class="sxs-lookup"><span data-stu-id="67c6f-113">Connection scenarios</span></span>
<span data-ttu-id="67c6f-114">The way a client connects to SQL Server running on a Virtual Machine differs depending on the location of the client and the machine/networking configuration.</span><span class="sxs-lookup"><span data-stu-id="67c6f-114">The way a client connects to SQL Server running on a Virtual Machine differs depending on the location of the client and the machine/networking configuration.</span></span> <span data-ttu-id="67c6f-115">These scenarios include:</span><span class="sxs-lookup"><span data-stu-id="67c6f-115">These scenarios include:</span></span>

* [<span data-ttu-id="67c6f-116">Connect to SQL Server over the internet</span><span class="sxs-lookup"><span data-stu-id="67c6f-116">Connect to SQL Server over the internet</span></span>](#connect-to-sql-server-over-the-internet)
* [<span data-ttu-id="67c6f-117">Connect to SQL Server in the same virtual network</span><span class="sxs-lookup"><span data-stu-id="67c6f-117">Connect to SQL Server in the same virtual network</span></span>](#connect-to-sql-server-in-the-same-virtual-network)

### <a name="connect-to-sql-server-over-the-internet"></a><span data-ttu-id="67c6f-118">Connect to SQL Server over the Internet</span><span class="sxs-lookup"><span data-stu-id="67c6f-118">Connect to SQL Server over the Internet</span></span>
<span data-ttu-id="67c6f-119">If you want to connect to your SQL Server database engine from the Internet, there are several steps required, such as configuring the firewall, enabling SQL Authentication, and configuring your network security group you must have a Network Security Group rule to allow TCP traffic on port 1433.</span><span class="sxs-lookup"><span data-stu-id="67c6f-119">If you want to connect to your SQL Server database engine from the Internet, there are several steps required, such as configuring the firewall, enabling SQL Authentication, and configuring your network security group you must have a Network Security Group rule to allow TCP traffic on port 1433.</span></span>

<span data-ttu-id="67c6f-120">If you use the portal to provision a SQL Server virtual machine image with the resource manager, these steps are done for you when you select **Public** for the SQL connectivity option:</span><span class="sxs-lookup"><span data-stu-id="67c6f-120">If you use the portal to provision a SQL Server virtual machine image with the resource manager, these steps are done for you when you select **Public** for the SQL connectivity option:</span></span>

![Public SQL connectivity option during provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity.png)

<span data-ttu-id="67c6f-122">If this was not one during provisioning, then you can manually configure SQL Server and your virtual machines by following the [steps in this article to manually configure connectivity](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="67c6f-122">If this was not one during provisioning, then you can manually configure SQL Server and your virtual machines by following the [steps in this article to manually configure connectivity](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

> [!NOTE]
> The virtual machine image for SQL Server Express edition does not automatically enable the TCP/IP protocol. For Express edition, you must use SQL Server Configuration Manager to [manually enable the TCP/IP protocol](#configure-sql-server-to-listen-on-the-tcp-protocol) after creating the VM.
> 
> 

<span data-ttu-id="67c6f-125">Once this is done, any client with internet access can connect to the SQL Server instance by specifying either the public IP address of the virtual machine or the DNS label assigned to that IP address.</span><span class="sxs-lookup"><span data-stu-id="67c6f-125">Once this is done, any client with internet access can connect to the SQL Server instance by specifying either the public IP address of the virtual machine or the DNS label assigned to that IP address.</span></span> <span data-ttu-id="67c6f-126">If the SQL Server port is 1433, you do not need to specify it in the connection string.</span><span class="sxs-lookup"><span data-stu-id="67c6f-126">If the SQL Server port is 1433, you do not need to specify it in the connection string.</span></span>

    "Server=sqlvmlabel.eastus.cloudapp.azure.com;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

<span data-ttu-id="67c6f-127">Although this enables connectivity for clients over the internet, this does not imply that anyone can connect to your SQL Server.</span><span class="sxs-lookup"><span data-stu-id="67c6f-127">Although this enables connectivity for clients over the internet, this does not imply that anyone can connect to your SQL Server.</span></span> <span data-ttu-id="67c6f-128">Outside clients have to the correct username and password.</span><span class="sxs-lookup"><span data-stu-id="67c6f-128">Outside clients have to the correct username and password.</span></span> <span data-ttu-id="67c6f-129">For additional security, you can avoid the well-known port 1433.</span><span class="sxs-lookup"><span data-stu-id="67c6f-129">For additional security, you can avoid the well-known port 1433.</span></span> <span data-ttu-id="67c6f-130">For example, if you configured SQL Server to listen on port 1500 and established proper firewall and network security group rules, you could connect by appending the port number to the Server name as in the following example:</span><span class="sxs-lookup"><span data-stu-id="67c6f-130">For example, if you configured SQL Server to listen on port 1500 and established proper firewall and network security group rules, you could connect by appending the port number to the Server name as in the following example:</span></span>

    "Server=sqlvmlabel.eastus.cloudapp.azure.com,1500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

> [!NOTE]
> It is important to note that when you use this technique to communicate with SQL Server, all outgoing data from the Azure datacenter is subject to normal [pricing on outbound data transfers](https://azure.microsoft.com/pricing/details/data-transfers/).
> 
> 

### <a name="connect-to-sql-server-in-the-same-virtual-network"></a><span data-ttu-id="67c6f-132">Connect to SQL Server in the same virtual network</span><span class="sxs-lookup"><span data-stu-id="67c6f-132">Connect to SQL Server in the same virtual network</span></span>
<span data-ttu-id="67c6f-133">[Virtual Network](../../../virtual-network/virtual-networks-overview.md) enables additional scenarios.</span><span class="sxs-lookup"><span data-stu-id="67c6f-133">[Virtual Network](../../../virtual-network/virtual-networks-overview.md) enables additional scenarios.</span></span> <span data-ttu-id="67c6f-134">You can connect VMs in the same virtual network, even if those VMs exist in different resource groups.</span><span class="sxs-lookup"><span data-stu-id="67c6f-134">You can connect VMs in the same virtual network, even if those VMs exist in different resource groups.</span></span> <span data-ttu-id="67c6f-135">And with a [site-to-site VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), you can create a hybrid architecture that connects VMs with on-premises networks and machines.</span><span class="sxs-lookup"><span data-stu-id="67c6f-135">And with a [site-to-site VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), you can create a hybrid architecture that connects VMs with on-premises networks and machines.</span></span>

<span data-ttu-id="67c6f-136">Virtual networks also enables you to join your Azure VMs to a domain.</span><span class="sxs-lookup"><span data-stu-id="67c6f-136">Virtual networks also enables you to join your Azure VMs to a domain.</span></span> <span data-ttu-id="67c6f-137">This is the only way to use Windows Authentication to SQL Server.</span><span class="sxs-lookup"><span data-stu-id="67c6f-137">This is the only way to use Windows Authentication to SQL Server.</span></span> <span data-ttu-id="67c6f-138">The other connection scenarios require SQL Authentication with user names and passwords.</span><span class="sxs-lookup"><span data-stu-id="67c6f-138">The other connection scenarios require SQL Authentication with user names and passwords.</span></span>

<span data-ttu-id="67c6f-139">If you use the portal to provision a SQL Server virtual machine image with the resource manager, the proper firewall rules for communication on the virtual network are setup when you select **Private** for the SQL connectivity option.</span><span class="sxs-lookup"><span data-stu-id="67c6f-139">If you use the portal to provision a SQL Server virtual machine image with the resource manager, the proper firewall rules for communication on the virtual network are setup when you select **Private** for the SQL connectivity option.</span></span> <span data-ttu-id="67c6f-140">If this was not one during provisioning, then you can manually configure SQL Server and your virtual machines by following the [steps in this article to manually configure connectivity](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="67c6f-140">If this was not one during provisioning, then you can manually configure SQL Server and your virtual machines by following the [steps in this article to manually configure connectivity](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span></span> <span data-ttu-id="67c6f-141">But if you are planning to configure a domain environment and Windows Authentication, you do not need to use the steps in this article to configure SQL Authentication and logins.</span><span class="sxs-lookup"><span data-stu-id="67c6f-141">But if you are planning to configure a domain environment and Windows Authentication, you do not need to use the steps in this article to configure SQL Authentication and logins.</span></span> <span data-ttu-id="67c6f-142">You also do not need to configure Network Security Group rules for access over the internet.</span><span class="sxs-lookup"><span data-stu-id="67c6f-142">You also do not need to configure Network Security Group rules for access over the internet.</span></span>

> [!NOTE]
> The virtual machine image for SQL Server Express edition does not automatically enable the TCP/IP protocol. For Express edition, you must use SQL Server Configuration Manager to [manually enable the TCP/IP protocol](#configure-sql-server-to-listen-on-the-tcp-protocol) after creating the VM.
> 
> 

<span data-ttu-id="67c6f-145">Assuming that you have configured DNS in your virtual network, you can connect to your SQL Server instance by specifying the SQL Server VM computer name in the connection string.</span><span class="sxs-lookup"><span data-stu-id="67c6f-145">Assuming that you have configured DNS in your virtual network, you can connect to your SQL Server instance by specifying the SQL Server VM computer name in the connection string.</span></span> <span data-ttu-id="67c6f-146">The following example also assumes that Windows Authentication has also been configured and that the user has been granted access to the SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="67c6f-146">The following example also assumes that Windows Authentication has also been configured and that the user has been granted access to the SQL Server instance.</span></span>

    "Server=mysqlvm;Integrated Security=true"

<span data-ttu-id="67c6f-147">Note that in this scenario, you could also specify the IP address of the VM.</span><span class="sxs-lookup"><span data-stu-id="67c6f-147">Note that in this scenario, you could also specify the IP address of the VM.</span></span>

## <a name="steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm"></a><span data-ttu-id="67c6f-148">Steps for manually configuring SQL Server connectivity in an Azure VM</span><span class="sxs-lookup"><span data-stu-id="67c6f-148">Steps for manually configuring SQL Server connectivity in an Azure VM</span></span>
<span data-ttu-id="67c6f-149">The following steps demonstrate how to manually setup connectivity to the SQL Server instance and then optionally connect over the internet using SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="67c6f-149">The following steps demonstrate how to manually setup connectivity to the SQL Server instance and then optionally connect over the internet using SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="67c6f-150">Note that many of these steps are done for you when you select the appropriate SQL Server connectivity options in the portal.</span><span class="sxs-lookup"><span data-stu-id="67c6f-150">Note that many of these steps are done for you when you select the appropriate SQL Server connectivity options in the portal.</span></span>

<span data-ttu-id="67c6f-151">Before you can connect to the instance of SQL Server from another VM or the internet, you must complete the following tasks as described in the sections that follow:</span><span class="sxs-lookup"><span data-stu-id="67c6f-151">Before you can connect to the instance of SQL Server from another VM or the internet, you must complete the following tasks as described in the sections that follow:</span></span>

* [<span data-ttu-id="67c6f-152">Open TCP ports in the Windows firewall</span><span class="sxs-lookup"><span data-stu-id="67c6f-152">Open TCP ports in the Windows firewall</span></span>](#open-tcp-ports-in-the-windows-firewall-for-the-default-instance-of-the-database-engine)
* [<span data-ttu-id="67c6f-153">Configure SQL Server to listen on the TCP protocol</span><span class="sxs-lookup"><span data-stu-id="67c6f-153">Configure SQL Server to listen on the TCP protocol</span></span>](#configure-sql-server-to-listen-on-the-tcp-protocol)
* [<span data-ttu-id="67c6f-154">Configure SQL Server for mixed mode authentication</span><span class="sxs-lookup"><span data-stu-id="67c6f-154">Configure SQL Server for mixed mode authentication</span></span>](#configure-sql-server-for-mixed-mode-authentication)
* [<span data-ttu-id="67c6f-155">Create SQL Server authentication logins</span><span class="sxs-lookup"><span data-stu-id="67c6f-155">Create SQL Server authentication logins</span></span>](#create-sql-server-authentication-logins)
* [<span data-ttu-id="67c6f-156">Configure a Network Security Group inbound rule</span><span class="sxs-lookup"><span data-stu-id="67c6f-156">Configure a Network Security Group inbound rule</span></span>](#configure-a-network-security-group-inbound-rule-for-the-vm)
* [<span data-ttu-id="67c6f-157">Configure a DNS Label for the public IP address</span><span class="sxs-lookup"><span data-stu-id="67c6f-157">Configure a DNS Label for the public IP address</span></span>](#configure-a-dns-label-for-the-public-ip-address)
* [<span data-ttu-id="67c6f-158">Connect to the Database Engine from another computer</span><span class="sxs-lookup"><span data-stu-id="67c6f-158">Connect to the Database Engine from another computer</span></span>](#connect-to-the-database-engine-from-another-computer)

[!INCLUDE [Connect to SQL Server in a VM](../../../../includes/virtual-machines-sql-server-connection-steps.md)]

[!INCLUDE [Connect to SQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager-nsg-rule.md)]

[!INCLUDE [Connect to SQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="67c6f-159">Next Steps</span><span class="sxs-lookup"><span data-stu-id="67c6f-159">Next Steps</span></span>
<span data-ttu-id="67c6f-160">To see provisioning instructions along with these connectivity steps, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="67c6f-160">To see provisioning instructions along with these connectivity steps, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

<span data-ttu-id="67c6f-161">[Explore the Learning Path](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) for SQL Server on Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="67c6f-161">[Explore the Learning Path](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) for SQL Server on Azure virtual machines.</span></span>

<span data-ttu-id="67c6f-162">For other topics related to running SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="67c6f-162">For other topics related to running SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>


