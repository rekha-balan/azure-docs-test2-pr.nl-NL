---
title: Connect to a SQL Server Virtual Machine (Classic) | Microsoft Docs
description: Learn how to connect to SQL Server running on a Virtual Machine in Azure. This topic uses the classic deployment model. The scenarios differ depending on the networking configuration and the location of the client.
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: 416948af-454f-4cfe-8fd2-7cf971cbd3e9
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: jroth
ms.openlocfilehash: 1e9038e075383c77a1d665e1984d75af2ff35d41
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555560"
---
# <a name="connect-to-a-sql-server-virtual-machine-on-azure-classic-deployment"></a><span data-ttu-id="55003-105">Connect to a SQL Server Virtual Machine on Azure (Classic Deployment)</span><span class="sxs-lookup"><span data-stu-id="55003-105">Connect to a SQL Server Virtual Machine on Azure (Classic Deployment)</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager](../sql/virtual-machines-windows-sql-connect.md)
> * [Classic](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="55003-108">Overview</span><span class="sxs-lookup"><span data-stu-id="55003-108">Overview</span></span>
<span data-ttu-id="55003-109">This topic describes how to connect to your SQL Server instance running on an Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="55003-109">This topic describes how to connect to your SQL Server instance running on an Azure virtual machine.</span></span> <span data-ttu-id="55003-110">It covers some [general connectivity scenarios](#connection-scenarios) and then provides [detailed steps for configuring SQL Server connectivity in an Azure VM](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="55003-110">It covers some [general connectivity scenarios](#connection-scenarios) and then provides [detailed steps for configuring SQL Server connectivity in an Azure VM](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

> [!IMPORTANT] 
> Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md). This article covers using the Classic deployment model. Microsoft recommends that most new deployments use the Resource Manager model. If you are using Resource Manager VMs, see [Connect to a SQL Server Virtual Machine on Azure using Resource Manager](../sql/virtual-machines-windows-sql-connect.md).

## <a name="connection-scenarios"></a><span data-ttu-id="55003-115">Connection scenarios</span><span class="sxs-lookup"><span data-stu-id="55003-115">Connection scenarios</span></span>
<span data-ttu-id="55003-116">The way a client connects to SQL Server running on a Virtual Machine differs depending on the location of the client and the machine/networking configuration.</span><span class="sxs-lookup"><span data-stu-id="55003-116">The way a client connects to SQL Server running on a Virtual Machine differs depending on the location of the client and the machine/networking configuration.</span></span> <span data-ttu-id="55003-117">These scenarios include:</span><span class="sxs-lookup"><span data-stu-id="55003-117">These scenarios include:</span></span>

* [<span data-ttu-id="55003-118">Connect to SQL Server in the same cloud service</span><span class="sxs-lookup"><span data-stu-id="55003-118">Connect to SQL Server in the same cloud service</span></span>](#connect-to-sql-server-in-the-same-cloud-service)
* [<span data-ttu-id="55003-119">Connect to SQL Server over the internet</span><span class="sxs-lookup"><span data-stu-id="55003-119">Connect to SQL Server over the internet</span></span>](#connect-to-sql-server-over-the-internet)
* [<span data-ttu-id="55003-120">Connect to SQL Server in the same virtual network</span><span class="sxs-lookup"><span data-stu-id="55003-120">Connect to SQL Server in the same virtual network</span></span>](#connect-to-sql-server-in-the-same-virtual-network)

> [!NOTE]
> Before you connect with any of these methods, you must follow the [steps in this article to configure connectivity](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).
> 
> 

### <a name="connect-to-sql-server-in-the-same-cloud-service"></a><span data-ttu-id="55003-122">Connect to SQL Server in the same cloud service</span><span class="sxs-lookup"><span data-stu-id="55003-122">Connect to SQL Server in the same cloud service</span></span>
<span data-ttu-id="55003-123">Multiple virtual machines can be created in the same cloud service.</span><span class="sxs-lookup"><span data-stu-id="55003-123">Multiple virtual machines can be created in the same cloud service.</span></span> <span data-ttu-id="55003-124">To understand this virtual machines scenario, see [How to connect virtual machines with a virtual network or cloud service](../classic/connect-vms.md#connect-vms-in-a-standalone-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="55003-124">To understand this virtual machines scenario, see [How to connect virtual machines with a virtual network or cloud service](../classic/connect-vms.md#connect-vms-in-a-standalone-cloud-service).</span></span> <span data-ttu-id="55003-125">This scenario is when a client on one virtual machine attempts to connect to SQL Server running on another virtual machine in the same cloud service.</span><span class="sxs-lookup"><span data-stu-id="55003-125">This scenario is when a client on one virtual machine attempts to connect to SQL Server running on another virtual machine in the same cloud service.</span></span>

<span data-ttu-id="55003-126">In this scenario, you can connect using the VM **Name** (also shown as **Computer Name** or **hostname** in the portal).</span><span class="sxs-lookup"><span data-stu-id="55003-126">In this scenario, you can connect using the VM **Name** (also shown as **Computer Name** or **hostname** in the portal).</span></span> <span data-ttu-id="55003-127">This is the name you provided for the VM during creation.</span><span class="sxs-lookup"><span data-stu-id="55003-127">This is the name you provided for the VM during creation.</span></span> <span data-ttu-id="55003-128">For example, if you named your SQL VM **mysqlvm**, a client VM in the same cloud service could use the following connection string to connect:</span><span class="sxs-lookup"><span data-stu-id="55003-128">For example, if you named your SQL VM **mysqlvm**, a client VM in the same cloud service could use the following connection string to connect:</span></span>

    "Server=mysqlvm;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

### <a name="connect-to-sql-server-over-the-internet"></a><span data-ttu-id="55003-129">Connect to SQL Server over the Internet</span><span class="sxs-lookup"><span data-stu-id="55003-129">Connect to SQL Server over the Internet</span></span>
<span data-ttu-id="55003-130">If you want to connect to your SQL Server database engine from the Internet, you must create a virtual machine endpoint for incoming TCP communication.</span><span class="sxs-lookup"><span data-stu-id="55003-130">If you want to connect to your SQL Server database engine from the Internet, you must create a virtual machine endpoint for incoming TCP communication.</span></span> <span data-ttu-id="55003-131">This Azure configuration step, directs incoming TCP port traffic to a TCP port that is accessible to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="55003-131">This Azure configuration step, directs incoming TCP port traffic to a TCP port that is accessible to the virtual machine.</span></span>

<span data-ttu-id="55003-132">To connect over the internet, you must use the VM's DNS name and the VM endpoint port number (configured later in this article).</span><span class="sxs-lookup"><span data-stu-id="55003-132">To connect over the internet, you must use the VM's DNS name and the VM endpoint port number (configured later in this article).</span></span> <span data-ttu-id="55003-133">To find the DNS Name, navigate to the Azure portal, and select **Virtual machines (classic)**.</span><span class="sxs-lookup"><span data-stu-id="55003-133">To find the DNS Name, navigate to the Azure portal, and select **Virtual machines (classic)**.</span></span> <span data-ttu-id="55003-134">Then select your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="55003-134">Then select your virtual machine.</span></span> <span data-ttu-id="55003-135">The **DNS name** is shown in the **Overview** section.</span><span class="sxs-lookup"><span data-stu-id="55003-135">The **DNS name** is shown in the **Overview** section.</span></span>

<span data-ttu-id="55003-136">For example, consider a classic virtual machine named **mysqlvm** with a DNS Name of **mysqlvm7777.cloudapp.net** and a VM endpoint of **57500**.</span><span class="sxs-lookup"><span data-stu-id="55003-136">For example, consider a classic virtual machine named **mysqlvm** with a DNS Name of **mysqlvm7777.cloudapp.net** and a VM endpoint of **57500**.</span></span> <span data-ttu-id="55003-137">Assuming properly configured connectivity, the following connection string could be used to access the virtual machine from anywhere on the internet:</span><span class="sxs-lookup"><span data-stu-id="55003-137">Assuming properly configured connectivity, the following connection string could be used to access the virtual machine from anywhere on the internet:</span></span>

    "Server=mycloudservice.cloudapp.net,57500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

<span data-ttu-id="55003-138">Although this enables connectivity for clients over the internet, this does not imply that anyone can connect to your SQL Server.</span><span class="sxs-lookup"><span data-stu-id="55003-138">Although this enables connectivity for clients over the internet, this does not imply that anyone can connect to your SQL Server.</span></span> <span data-ttu-id="55003-139">Outside clients have to the correct username and password.</span><span class="sxs-lookup"><span data-stu-id="55003-139">Outside clients have to the correct username and password.</span></span> <span data-ttu-id="55003-140">For additional security, don't use the well-known port 1433 for the public virtual machine endpoint.</span><span class="sxs-lookup"><span data-stu-id="55003-140">For additional security, don't use the well-known port 1433 for the public virtual machine endpoint.</span></span> <span data-ttu-id="55003-141">And if possible, consider adding an ACL on your endpoint to restrict traffic only to the clients you permit.</span><span class="sxs-lookup"><span data-stu-id="55003-141">And if possible, consider adding an ACL on your endpoint to restrict traffic only to the clients you permit.</span></span> <span data-ttu-id="55003-142">For instructions on using ACLs with endpoints, see [Manage the ACL on an endpoint](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span><span class="sxs-lookup"><span data-stu-id="55003-142">For instructions on using ACLs with endpoints, see [Manage the ACL on an endpoint](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span></span>

> [!NOTE]
> It is important to note that when you use this technique to communicate with SQL Server, all outgoing data from the Azure datacenter is subject to normal [pricing on outbound data transfers](https://azure.microsoft.com/pricing/details/data-transfers/).
> 
> 

### <a name="connect-to-sql-server-in-the-same-virtual-network"></a><span data-ttu-id="55003-144">Connect to SQL Server in the same virtual network</span><span class="sxs-lookup"><span data-stu-id="55003-144">Connect to SQL Server in the same virtual network</span></span>
<span data-ttu-id="55003-145">[Virtual Network](../../../virtual-network/virtual-networks-overview.md) enables additional scenarios.</span><span class="sxs-lookup"><span data-stu-id="55003-145">[Virtual Network](../../../virtual-network/virtual-networks-overview.md) enables additional scenarios.</span></span> <span data-ttu-id="55003-146">You can connect VMs in the same virtual network, even if those VMs exist in different cloud services.</span><span class="sxs-lookup"><span data-stu-id="55003-146">You can connect VMs in the same virtual network, even if those VMs exist in different cloud services.</span></span> <span data-ttu-id="55003-147">And with a [site-to-site VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), you can create a hybrid architecture that connects VMs with on-premises networks and machines.</span><span class="sxs-lookup"><span data-stu-id="55003-147">And with a [site-to-site VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), you can create a hybrid architecture that connects VMs with on-premises networks and machines.</span></span>

<span data-ttu-id="55003-148">Virtual networks also enables you to join your Azure VMs to a domain.</span><span class="sxs-lookup"><span data-stu-id="55003-148">Virtual networks also enables you to join your Azure VMs to a domain.</span></span> <span data-ttu-id="55003-149">This is the only way to use Windows Authentication to SQL Server.</span><span class="sxs-lookup"><span data-stu-id="55003-149">This is the only way to use Windows Authentication to SQL Server.</span></span> <span data-ttu-id="55003-150">The other connection scenarios require SQL Authentication with user names and passwords.</span><span class="sxs-lookup"><span data-stu-id="55003-150">The other connection scenarios require SQL Authentication with user names and passwords.</span></span>

<span data-ttu-id="55003-151">If you are going to configure a domain environment and Windows Authentication, you do not need to use the steps in this article to configure the public endpoint or the SQL Authentication and logins.</span><span class="sxs-lookup"><span data-stu-id="55003-151">If you are going to configure a domain environment and Windows Authentication, you do not need to use the steps in this article to configure the public endpoint or the SQL Authentication and logins.</span></span> <span data-ttu-id="55003-152">In this scenario, you can connect to your SQL Server instance by specifying the SQL Server VM name in the connection string.</span><span class="sxs-lookup"><span data-stu-id="55003-152">In this scenario, you can connect to your SQL Server instance by specifying the SQL Server VM name in the connection string.</span></span> <span data-ttu-id="55003-153">The following example assumes that Windows Authentication has also been configured and that the user has been granted access to the SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="55003-153">The following example assumes that Windows Authentication has also been configured and that the user has been granted access to the SQL Server instance.</span></span>

    "Server=mysqlvm;Integrated Security=true"

## <a name="steps-for-configuring-sql-server-connectivity-in-an-azure-vm"></a><span data-ttu-id="55003-154">Steps for configuring SQL Server connectivity in an Azure VM</span><span class="sxs-lookup"><span data-stu-id="55003-154">Steps for configuring SQL Server connectivity in an Azure VM</span></span>
<span data-ttu-id="55003-155">The following steps demonstrate how to connect to the SQL Server instance over the internet using SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="55003-155">The following steps demonstrate how to connect to the SQL Server instance over the internet using SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="55003-156">However, the same steps apply to making your SQL Server virtual machine accessible for your applications, running both on-premises and in Azure.</span><span class="sxs-lookup"><span data-stu-id="55003-156">However, the same steps apply to making your SQL Server virtual machine accessible for your applications, running both on-premises and in Azure.</span></span>

<span data-ttu-id="55003-157">Before you can connect to the instance of SQL Server from another VM or the internet, you must complete the following tasks as described in the sections that follow:</span><span class="sxs-lookup"><span data-stu-id="55003-157">Before you can connect to the instance of SQL Server from another VM or the internet, you must complete the following tasks as described in the sections that follow:</span></span>

* [<span data-ttu-id="55003-158">Create a TCP endpoint for the virtual machine</span><span class="sxs-lookup"><span data-stu-id="55003-158">Create a TCP endpoint for the virtual machine</span></span>](#create-a-tcp-endpoint-for-the-virtual-machine)
* [<span data-ttu-id="55003-159">Open TCP ports in the Windows firewall</span><span class="sxs-lookup"><span data-stu-id="55003-159">Open TCP ports in the Windows firewall</span></span>](#open-tcp-ports-in-the-windows-firewall-for-the-default-instance-of-the-database-engine)
* [<span data-ttu-id="55003-160">Configure SQL Server to listen on the TCP protocol</span><span class="sxs-lookup"><span data-stu-id="55003-160">Configure SQL Server to listen on the TCP protocol</span></span>](#configure-sql-server-to-listen-on-the-tcp-protocol)
* [<span data-ttu-id="55003-161">Configure SQL Server for mixed mode authentication</span><span class="sxs-lookup"><span data-stu-id="55003-161">Configure SQL Server for mixed mode authentication</span></span>](#configure-sql-server-for-mixed-mode-authentication)
* [<span data-ttu-id="55003-162">Create SQL Server authentication logins</span><span class="sxs-lookup"><span data-stu-id="55003-162">Create SQL Server authentication logins</span></span>](#create-sql-server-authentication-logins)
* [<span data-ttu-id="55003-163">Determine the DNS name of the virtual machine</span><span class="sxs-lookup"><span data-stu-id="55003-163">Determine the DNS name of the virtual machine</span></span>](#determine-the-dns-name-of-the-virtual-machine)
* [<span data-ttu-id="55003-164">Connect to the Database Engine from another computer</span><span class="sxs-lookup"><span data-stu-id="55003-164">Connect to the Database Engine from another computer</span></span>](#connect-to-the-database-engine-from-another-computer)

<span data-ttu-id="55003-165">The connection path is summarized by the following diagram:</span><span class="sxs-lookup"><span data-stu-id="55003-165">The connection path is summarized by the following diagram:</span></span>

![Connecting to a SQL Server virtual machine](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-sql-server-connection-steps/SQLServerinVMConnectionMap.png)

[!INCLUDE [Connect to SQL Server in a VM Classic TCP Endpoint](../../../../includes/virtual-machines-sql-server-connection-steps-classic-tcp-endpoint.md)]

[!INCLUDE [Connect to SQL Server in a VM](../../../../includes/virtual-machines-sql-server-connection-steps.md)]

[!INCLUDE [Connect to SQL Server in a VM Classic Steps](../../../../includes/virtual-machines-sql-server-connection-steps-classic.md)]

## <a name="next-steps"></a><span data-ttu-id="55003-167">Next Steps</span><span class="sxs-lookup"><span data-stu-id="55003-167">Next Steps</span></span>
<span data-ttu-id="55003-168">If you are also planning to use AlwaysOn Availability Groups for high availability and disaster recovery, you should consider implementing a listener.</span><span class="sxs-lookup"><span data-stu-id="55003-168">If you are also planning to use AlwaysOn Availability Groups for high availability and disaster recovery, you should consider implementing a listener.</span></span> <span data-ttu-id="55003-169">Database clients connect to the listener rather than directly to one of the SQL Server instances.</span><span class="sxs-lookup"><span data-stu-id="55003-169">Database clients connect to the listener rather than directly to one of the SQL Server instances.</span></span> <span data-ttu-id="55003-170">The listener routes clients to the primary replica in the availability group.</span><span class="sxs-lookup"><span data-stu-id="55003-170">The listener routes clients to the primary replica in the availability group.</span></span> <span data-ttu-id="55003-171">For more information, see [Configure an ILB listener for AlwaysOn Availability Groups in Azure](../classic/ps-sql-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="55003-171">For more information, see [Configure an ILB listener for AlwaysOn Availability Groups in Azure](../classic/ps-sql-int-listener.md).</span></span>

<span data-ttu-id="55003-172">It is important to review all of the security best practices for SQL Server running on an Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="55003-172">It is important to review all of the security best practices for SQL Server running on an Azure virtual machine.</span></span> <span data-ttu-id="55003-173">For more information, see [Security Considerations for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-security.md).</span><span class="sxs-lookup"><span data-stu-id="55003-173">For more information, see [Security Considerations for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-security.md).</span></span>

<span data-ttu-id="55003-174">[Explore the Learning Path](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) for SQL Server on Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="55003-174">[Explore the Learning Path](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) for SQL Server on Azure virtual machines.</span></span> 

<span data-ttu-id="55003-175">For other topics related to running SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="55003-175">For other topics related to running SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>


