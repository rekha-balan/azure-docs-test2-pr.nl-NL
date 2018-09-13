---
title: SQL Hosting Servers on Azure Stack | Microsoft Docs
description: How to add SQL instances for provisioning through the SQL Adapter Resource provider.
services: azure-stack
documentationCenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/05/2018
ms.author: jeffgilb
ms.reviewer: jeffgo
ms.openlocfilehash: 3455821400ed013c12f8250254e09cae15394526
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864600"
---
# <a name="add-hosting-servers-for-the-sql-resource-provider"></a><span data-ttu-id="50e88-103">Add hosting servers for the SQL resource provider</span><span class="sxs-lookup"><span data-stu-id="50e88-103">Add hosting servers for the SQL resource provider</span></span>

<span data-ttu-id="50e88-104">You can host a SQL instance on a virtual machine (VM) in [Azure Stack](azure-stack-poc.md), or on a VM outside your Azure Stack environment, as long as the SQL resource provider can connect to the instance.</span><span class="sxs-lookup"><span data-stu-id="50e88-104">You can host a SQL instance on a virtual machine (VM) in [Azure Stack](azure-stack-poc.md), or on a VM outside your Azure Stack environment, as long as the SQL resource provider can connect to the instance.</span></span>

## <a name="overview"></a><span data-ttu-id="50e88-105">Overview</span><span class="sxs-lookup"><span data-stu-id="50e88-105">Overview</span></span>

<span data-ttu-id="50e88-106">Before you add a SQL hosting server, review the following mandatory and general requirements.</span><span class="sxs-lookup"><span data-stu-id="50e88-106">Before you add a SQL hosting server, review the following mandatory and general requirements.</span></span>

### <a name="mandatory-requirements"></a><span data-ttu-id="50e88-107">Mandatory requirements</span><span class="sxs-lookup"><span data-stu-id="50e88-107">Mandatory requirements</span></span>

* <span data-ttu-id="50e88-108">Enable SQL authentication on the SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="50e88-108">Enable SQL authentication on the SQL Server instance.</span></span> <span data-ttu-id="50e88-109">Because the SQL resource provider VM isn't domain joined, it can only connect to a hosting server using SQL authentication.</span><span class="sxs-lookup"><span data-stu-id="50e88-109">Because the SQL resource provider VM isn't domain joined, it can only connect to a hosting server using SQL authentication.</span></span>
* <span data-ttu-id="50e88-110">Configure the IP addresses for the SQL instances as Public when installed on Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="50e88-110">Configure the IP addresses for the SQL instances as Public when installed on Azure Stack.</span></span> <span data-ttu-id="50e88-111">The resource provider, and users, such as Web Apps, communicate over the user network, so connectivity to the SQL instance on this network is required.</span><span class="sxs-lookup"><span data-stu-id="50e88-111">The resource provider, and users, such as Web Apps, communicate over the user network, so connectivity to the SQL instance on this network is required.</span></span>

### <a name="general-requirements"></a><span data-ttu-id="50e88-112">General requirements</span><span class="sxs-lookup"><span data-stu-id="50e88-112">General requirements</span></span>

* <span data-ttu-id="50e88-113">Dedicate the SQL instance for use by the resource provider and user workloads.</span><span class="sxs-lookup"><span data-stu-id="50e88-113">Dedicate the SQL instance for use by the resource provider and user workloads.</span></span> <span data-ttu-id="50e88-114">You can't use a SQL instance that's being used by any other consumer.</span><span class="sxs-lookup"><span data-stu-id="50e88-114">You can't use a SQL instance that's being used by any other consumer.</span></span> <span data-ttu-id="50e88-115">This restriction also applies to App Services.</span><span class="sxs-lookup"><span data-stu-id="50e88-115">This restriction also applies to App Services.</span></span>
* <span data-ttu-id="50e88-116">Configure an account with the appropriate privilege levels for the resource provider (described below).</span><span class="sxs-lookup"><span data-stu-id="50e88-116">Configure an account with the appropriate privilege levels for the resource provider (described below).</span></span>
* <span data-ttu-id="50e88-117">You are responsible for managing the SQL instances and their hosts.</span><span class="sxs-lookup"><span data-stu-id="50e88-117">You are responsible for managing the SQL instances and their hosts.</span></span>  <span data-ttu-id="50e88-118">For example, the resource provider doesn't apply updates, handle backups, or handle credential rotation.</span><span class="sxs-lookup"><span data-stu-id="50e88-118">For example, the resource provider doesn't apply updates, handle backups, or handle credential rotation.</span></span>

### <a name="sql-server-virtual-machine-images"></a><span data-ttu-id="50e88-119">SQL Server virtual machine images</span><span class="sxs-lookup"><span data-stu-id="50e88-119">SQL Server virtual machine images</span></span>

<span data-ttu-id="50e88-120">SQL IaaS virtual machine images are available through the Marketplace Management feature.</span><span class="sxs-lookup"><span data-stu-id="50e88-120">SQL IaaS virtual machine images are available through the Marketplace Management feature.</span></span> <span data-ttu-id="50e88-121">These images are the same as the SQL VMs that are available in Azure.</span><span class="sxs-lookup"><span data-stu-id="50e88-121">These images are the same as the SQL VMs that are available in Azure.</span></span>

<span data-ttu-id="50e88-122">Make sure you always download the latest version of the **SQL IaaS Extension** before you deploy a SQL VM using a Marketplace item.</span><span class="sxs-lookup"><span data-stu-id="50e88-122">Make sure you always download the latest version of the **SQL IaaS Extension** before you deploy a SQL VM using a Marketplace item.</span></span> <span data-ttu-id="50e88-123">The IaaS extension and corresponding portal enhancements provide additional features such as automatic patching and backup.</span><span class="sxs-lookup"><span data-stu-id="50e88-123">The IaaS extension and corresponding portal enhancements provide additional features such as automatic patching and backup.</span></span> <span data-ttu-id="50e88-124">For more information about this extension, see [Automate management tasks on Azure Virtual Machines with the SQL Server Agent Extension](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-agent-extension).</span><span class="sxs-lookup"><span data-stu-id="50e88-124">For more information about this extension, see [Automate management tasks on Azure Virtual Machines with the SQL Server Agent Extension](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-agent-extension).</span></span>

> [!NOTE]
> <span data-ttu-id="50e88-125">The SQL IaaS Extension is _required_ for all SQL on Windows images in the marketplace; the VM will fail to deploy if you did not download the extension.</span><span class="sxs-lookup"><span data-stu-id="50e88-125">The SQL IaaS Extension is _required_ for all SQL on Windows images in the marketplace; the VM will fail to deploy if you did not download the extension.</span></span> <span data-ttu-id="50e88-126">It is not used with Linux-based SQL virtual machine images.</span><span class="sxs-lookup"><span data-stu-id="50e88-126">It is not used with Linux-based SQL virtual machine images.</span></span>

<span data-ttu-id="50e88-127">There are other options for deploying SQL VMs, including templates in the [Azure Stack Quickstart Gallery](https://github.com/Azure/AzureStack-QuickStart-Templates).</span><span class="sxs-lookup"><span data-stu-id="50e88-127">There are other options for deploying SQL VMs, including templates in the [Azure Stack Quickstart Gallery](https://github.com/Azure/AzureStack-QuickStart-Templates).</span></span>

> [!NOTE]
> <span data-ttu-id="50e88-128">Any hosting servers installed on a multi-node Azure Stack must be created from a user subscription and not the Default Provider Subscription.</span><span class="sxs-lookup"><span data-stu-id="50e88-128">Any hosting servers installed on a multi-node Azure Stack must be created from a user subscription and not the Default Provider Subscription.</span></span> <span data-ttu-id="50e88-129">They must be created from the user portal or from a PowerShell session with an appropriate login.</span><span class="sxs-lookup"><span data-stu-id="50e88-129">They must be created from the user portal or from a PowerShell session with an appropriate login.</span></span> <span data-ttu-id="50e88-130">All hosting servers are billable VMs and must have appropriate SQL licenses.</span><span class="sxs-lookup"><span data-stu-id="50e88-130">All hosting servers are billable VMs and must have appropriate SQL licenses.</span></span> <span data-ttu-id="50e88-131">The service administrator _can_ be the owner of that subscription.</span><span class="sxs-lookup"><span data-stu-id="50e88-131">The service administrator _can_ be the owner of that subscription.</span></span>

### <a name="required-privileges"></a><span data-ttu-id="50e88-132">Required Privileges</span><span class="sxs-lookup"><span data-stu-id="50e88-132">Required Privileges</span></span>

<span data-ttu-id="50e88-133">You can create an administrative user with lower privileges than a SQL sysadmin.</span><span class="sxs-lookup"><span data-stu-id="50e88-133">You can create an administrative user with lower privileges than a SQL sysadmin.</span></span> <span data-ttu-id="50e88-134">The user only needs permissions for the following operations:</span><span class="sxs-lookup"><span data-stu-id="50e88-134">The user only needs permissions for the following operations:</span></span>

* <span data-ttu-id="50e88-135">Database: Create, Alter, With Containment (for Always On only), Drop, Backup</span><span class="sxs-lookup"><span data-stu-id="50e88-135">Database: Create, Alter, With Containment (for Always On only), Drop, Backup</span></span>
* <span data-ttu-id="50e88-136">Availability Group: Alter, Join, Add/Remove Database</span><span class="sxs-lookup"><span data-stu-id="50e88-136">Availability Group: Alter, Join, Add/Remove Database</span></span>
* <span data-ttu-id="50e88-137">Login: Create, Select, Alter, Drop, Revoke</span><span class="sxs-lookup"><span data-stu-id="50e88-137">Login: Create, Select, Alter, Drop, Revoke</span></span>
* <span data-ttu-id="50e88-138">Select Operations: \[master\].\[sys\].\[availability_group_listeners\] (AlwaysOn), sys.availability_replicas (AlwaysOn), sys.databases, \[master\].\[sys\].\[dm_os_sys_memory\], SERVERPROPERTY, \[master\].\[sys\].\[availability_groups\] (AlwaysOn), sys.master_files</span><span class="sxs-lookup"><span data-stu-id="50e88-138">Select Operations: \[master\].\[sys\].\[availability_group_listeners\] (AlwaysOn), sys.availability_replicas (AlwaysOn), sys.databases, \[master\].\[sys\].\[dm_os_sys_memory\], SERVERPROPERTY, \[master\].\[sys\].\[availability_groups\] (AlwaysOn), sys.master_files</span></span>

### <a name="additional-security-information"></a><span data-ttu-id="50e88-139">Additional Security Information</span><span class="sxs-lookup"><span data-stu-id="50e88-139">Additional Security Information</span></span>

<span data-ttu-id="50e88-140">The following information provides additional security guidance:</span><span class="sxs-lookup"><span data-stu-id="50e88-140">The following information provides additional security guidance:</span></span>

* <span data-ttu-id="50e88-141">All Azure Stack storage is encrypted using BitLocker, so any SQL instance on Azure Stack will use encrypted blob storage.</span><span class="sxs-lookup"><span data-stu-id="50e88-141">All Azure Stack storage is encrypted using BitLocker, so any SQL instance on Azure Stack will use encrypted blob storage.</span></span>
* <span data-ttu-id="50e88-142">The SQL Resource Provider fully supports TLS 1.2.</span><span class="sxs-lookup"><span data-stu-id="50e88-142">The SQL Resource Provider fully supports TLS 1.2.</span></span> <span data-ttu-id="50e88-143">Ensure that any SQL Server that is managed through the SQL RP is configured for TLS 1.2 _only_ and the RP will default to that.</span><span class="sxs-lookup"><span data-stu-id="50e88-143">Ensure that any SQL Server that is managed through the SQL RP is configured for TLS 1.2 _only_ and the RP will default to that.</span></span> <span data-ttu-id="50e88-144">All supported versions of SQL Server support TLS 1.2, see [TLS 1.2 support for Microsoft SQL Server](https://support.microsoft.com/en-us/help/3135244/tls-1-2-support-for-microsoft-sql-server).</span><span class="sxs-lookup"><span data-stu-id="50e88-144">All supported versions of SQL Server support TLS 1.2, see [TLS 1.2 support for Microsoft SQL Server](https://support.microsoft.com/en-us/help/3135244/tls-1-2-support-for-microsoft-sql-server).</span></span>
* <span data-ttu-id="50e88-145">Use SQL Server Configuration Manager to set the **ForceEncryption** option to ensure all communications to the SQL server are always encrypted.</span><span class="sxs-lookup"><span data-stu-id="50e88-145">Use SQL Server Configuration Manager to set the **ForceEncryption** option to ensure all communications to the SQL server are always encrypted.</span></span> <span data-ttu-id="50e88-146">See [To configure the server to force encrypted connections](https://docs.microsoft.com/sql/database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine?view=sql-server-2017#ConfigureServerConnections).</span><span class="sxs-lookup"><span data-stu-id="50e88-146">See [To configure the server to force encrypted connections](https://docs.microsoft.com/sql/database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine?view=sql-server-2017#ConfigureServerConnections).</span></span>
* <span data-ttu-id="50e88-147">Ensure any client application is also communicating over an encrypted connection.</span><span class="sxs-lookup"><span data-stu-id="50e88-147">Ensure any client application is also communicating over an encrypted connection.</span></span>
* <span data-ttu-id="50e88-148">The RP is configured to trust the certificates used by the SQL Server instances.</span><span class="sxs-lookup"><span data-stu-id="50e88-148">The RP is configured to trust the certificates used by the SQL Server instances.</span></span>

## <a name="provide-capacity-by-connecting-to-a-standalone-hosting-sql-server"></a><span data-ttu-id="50e88-149">Provide capacity by connecting to a standalone hosting SQL server</span><span class="sxs-lookup"><span data-stu-id="50e88-149">Provide capacity by connecting to a standalone hosting SQL server</span></span>

<span data-ttu-id="50e88-150">You can use standalone (non-HA) SQL servers using any edition of SQL Server 2014 or SQL Server 2016.</span><span class="sxs-lookup"><span data-stu-id="50e88-150">You can use standalone (non-HA) SQL servers using any edition of SQL Server 2014 or SQL Server 2016.</span></span> <span data-ttu-id="50e88-151">Make sure you have the credentials for an account with sysadmin privileges.</span><span class="sxs-lookup"><span data-stu-id="50e88-151">Make sure you have the credentials for an account with sysadmin privileges.</span></span>

<span data-ttu-id="50e88-152">To add a standalone hosting server that's already set up, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="50e88-152">To add a standalone hosting server that's already set up, follow these steps:</span></span>

1. <span data-ttu-id="50e88-153">Sign in to the Azure Stack operator portal as a service administrator.</span><span class="sxs-lookup"><span data-stu-id="50e88-153">Sign in to the Azure Stack operator portal as a service administrator.</span></span>

2. <span data-ttu-id="50e88-154">Select **All services** &gt; **ADMINISTRATIVE RESOURCES** &gt; **SQL Hosting Servers**.</span><span class="sxs-lookup"><span data-stu-id="50e88-154">Select **All services** &gt; **ADMINISTRATIVE RESOURCES** &gt; **SQL Hosting Servers**.</span></span>

   ![SQL Hosting Servers](./media/azure-stack-sql-rp-deploy/sqlhostingservers.png)

   <span data-ttu-id="50e88-156">Under **SQL Hosting Servers**,  you can connect the SQL resource provider to instances of SQL Server that will serve as the resource provider’s backend.</span><span class="sxs-lookup"><span data-stu-id="50e88-156">Under **SQL Hosting Servers**,  you can connect the SQL resource provider to instances of SQL Server that will serve as the resource provider’s backend.</span></span>

   ![SQL Adapter dashboard](./media/azure-stack-sql-rp-deploy/sqlrp-hostingserver.png)

3. <span data-ttu-id="50e88-158">Click **Add** and then provide the connection details for your SQL Server instance on the **Add a SQL Hosting Server** blade.</span><span class="sxs-lookup"><span data-stu-id="50e88-158">Click **Add** and then provide the connection details for your SQL Server instance on the **Add a SQL Hosting Server** blade.</span></span>

   ![Add a SQL Hosting Server](./media/azure-stack-sql-rp-deploy/sqlrp-newhostingserver.png)

    <span data-ttu-id="50e88-160">Optionally, provide an instance name, and specify a port number if the instance isn't assigned to the default port of 1433.</span><span class="sxs-lookup"><span data-stu-id="50e88-160">Optionally, provide an instance name, and specify a port number if the instance isn't assigned to the default port of 1433.</span></span>

   > [!NOTE]
   > <span data-ttu-id="50e88-161">As long as the SQL instance can be accessed by the user and admin Azure Resource Manager, it can be placed under control of the resource provider.</span><span class="sxs-lookup"><span data-stu-id="50e88-161">As long as the SQL instance can be accessed by the user and admin Azure Resource Manager, it can be placed under control of the resource provider.</span></span> <span data-ttu-id="50e88-162">The SQL instance __must__ be allocated exclusively to the resource provider.</span><span class="sxs-lookup"><span data-stu-id="50e88-162">The SQL instance __must__ be allocated exclusively to the resource provider.</span></span>

4. <span data-ttu-id="50e88-163">As you add servers, you must assign them to an existing SKU or create a new SKU.</span><span class="sxs-lookup"><span data-stu-id="50e88-163">As you add servers, you must assign them to an existing SKU or create a new SKU.</span></span> <span data-ttu-id="50e88-164">Under **Add a Hosting Server**, select **SKUs**.</span><span class="sxs-lookup"><span data-stu-id="50e88-164">Under **Add a Hosting Server**, select **SKUs**.</span></span>

   * <span data-ttu-id="50e88-165">To use an existing SKU, choose an available SKU and then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="50e88-165">To use an existing SKU, choose an available SKU and then select **Create**.</span></span>
   * <span data-ttu-id="50e88-166">To create a SKU, select **+ Create new SKU**.</span><span class="sxs-lookup"><span data-stu-id="50e88-166">To create a SKU, select **+ Create new SKU**.</span></span> <span data-ttu-id="50e88-167">In **Create SKU**, enter the required information, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="50e88-167">In **Create SKU**, enter the required information, and then select **OK**.</span></span>

     ![Create a SKU](./media/azure-stack-sql-rp-deploy/sqlrp-newsku.png)

## <a name="provide-high-availability-using-sql-always-on-availability-groups"></a><span data-ttu-id="50e88-169">Provide high availability using SQL Always On Availability Groups</span><span class="sxs-lookup"><span data-stu-id="50e88-169">Provide high availability using SQL Always On Availability Groups</span></span>

<span data-ttu-id="50e88-170">Configuring SQL Always On instances requires additional steps and requires three VMs (or physical machines.) This article assumes that you already have a solid understanding of Always On availability groups.</span><span class="sxs-lookup"><span data-stu-id="50e88-170">Configuring SQL Always On instances requires additional steps and requires three VMs (or physical machines.) This article assumes that you already have a solid understanding of Always On availability groups.</span></span> <span data-ttu-id="50e88-171">For more information, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="50e88-171">For more information, see the following articles:</span></span>

* [<span data-ttu-id="50e88-172">Introducing SQL Server Always On availability groups on Azure virtual machines</span><span class="sxs-lookup"><span data-stu-id="50e88-172">Introducing SQL Server Always On availability groups on Azure virtual machines</span></span>](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-availability-group-overview)
* [<span data-ttu-id="50e88-173">Always On Availability Groups (SQL Server)</span><span class="sxs-lookup"><span data-stu-id="50e88-173">Always On Availability Groups (SQL Server)</span></span>](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/always-on-availability-groups-sql-server?view=sql-server-2017)

> [!NOTE]
> <span data-ttu-id="50e88-174">The SQL adapter resource provider _only_ supports SQL 2016 SP1 Enterprise or later instances for Always On Availability Groups.</span><span class="sxs-lookup"><span data-stu-id="50e88-174">The SQL adapter resource provider _only_ supports SQL 2016 SP1 Enterprise or later instances for Always On Availability Groups.</span></span> <span data-ttu-id="50e88-175">This adapter configuration requires new SQL features such as automatic seeding.</span><span class="sxs-lookup"><span data-stu-id="50e88-175">This adapter configuration requires new SQL features such as automatic seeding.</span></span>

### <a name="automatic-seeding"></a><span data-ttu-id="50e88-176">Automatic seeding</span><span class="sxs-lookup"><span data-stu-id="50e88-176">Automatic seeding</span></span>

<span data-ttu-id="50e88-177">You must enable [Automatic Seeding](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/automatically-initialize-always-on-availability-group) on each availability group for each instance of SQL Server.</span><span class="sxs-lookup"><span data-stu-id="50e88-177">You must enable [Automatic Seeding](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/automatically-initialize-always-on-availability-group) on each availability group for each instance of SQL Server.</span></span>

<span data-ttu-id="50e88-178">To enable automatic seeding on all instances, edit and then run the following SQL command on the primary replica for each secondary instance:</span><span class="sxs-lookup"><span data-stu-id="50e88-178">To enable automatic seeding on all instances, edit and then run the following SQL command on the primary replica for each secondary instance:</span></span>

  ```sql
  ALTER AVAILABILITY GROUP [<availability_group_name>]
      MODIFY REPLICA ON '<secondary_node>'
      WITH (SEEDING_MODE = AUTOMATIC)
  GO
  ```

<span data-ttu-id="50e88-179">The availability group must be enclosed in square brackets.</span><span class="sxs-lookup"><span data-stu-id="50e88-179">The availability group must be enclosed in square brackets.</span></span>

<span data-ttu-id="50e88-180">On the secondary nodes, run the following SQL command:</span><span class="sxs-lookup"><span data-stu-id="50e88-180">On the secondary nodes, run the following SQL command:</span></span>

  ```sql
  ALTER AVAILABILITY GROUP [<availability_group_name>] GRANT CREATE ANY DATABASE
  GO
  ```

### <a name="configure-contained-database-authentication"></a><span data-ttu-id="50e88-181">Configure contained database authentication</span><span class="sxs-lookup"><span data-stu-id="50e88-181">Configure contained database authentication</span></span>

<span data-ttu-id="50e88-182">Before adding a contained database to an availability group, ensure that the contained database authentication server option is set to 1 on every server instance that hosts an availability replica for the availability group.</span><span class="sxs-lookup"><span data-stu-id="50e88-182">Before adding a contained database to an availability group, ensure that the contained database authentication server option is set to 1 on every server instance that hosts an availability replica for the availability group.</span></span> <span data-ttu-id="50e88-183">For more information, see [contained database authentication Server Configuration Option](https://docs.microsoft.com/sql/database-engine/configure-windows/contained-database-authentication-server-configuration-option?view=sql-server-2017).</span><span class="sxs-lookup"><span data-stu-id="50e88-183">For more information, see [contained database authentication Server Configuration Option](https://docs.microsoft.com/sql/database-engine/configure-windows/contained-database-authentication-server-configuration-option?view=sql-server-2017).</span></span>

<span data-ttu-id="50e88-184">Use these commands to set the contained database authentication server option for each instance:</span><span class="sxs-lookup"><span data-stu-id="50e88-184">Use these commands to set the contained database authentication server option for each instance:</span></span>

  ```sql
  EXEC sp_configure 'contained database authentication', 1
  GO
  RECONFIGURE
  GO
  ```

### <a name="to-add-sql-always-on-hosting-servers"></a><span data-ttu-id="50e88-185">To add SQL Always On hosting servers</span><span class="sxs-lookup"><span data-stu-id="50e88-185">To add SQL Always On hosting servers</span></span>

1. <span data-ttu-id="50e88-186">Sign in to the Azure Stack Administration portal as a service admin.</span><span class="sxs-lookup"><span data-stu-id="50e88-186">Sign in to the Azure Stack Administration portal as a service admin.</span></span>

2. <span data-ttu-id="50e88-187">Select **Browse** &gt; **ADMINISTRATIVE RESOURCES** &gt; **SQL Hosting Servers** &gt; **+Add**.</span><span class="sxs-lookup"><span data-stu-id="50e88-187">Select **Browse** &gt; **ADMINISTRATIVE RESOURCES** &gt; **SQL Hosting Servers** &gt; **+Add**.</span></span>

   <span data-ttu-id="50e88-188">Under **SQL Hosting Servers**, you can connect the SQL Server Resource Provider to actual instances of SQL Server that serve as the resource provider’s backend.</span><span class="sxs-lookup"><span data-stu-id="50e88-188">Under **SQL Hosting Servers**, you can connect the SQL Server Resource Provider to actual instances of SQL Server that serve as the resource provider’s backend.</span></span>

3. <span data-ttu-id="50e88-189">Fill out the form with the connection details for your SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="50e88-189">Fill out the form with the connection details for your SQL Server instance.</span></span> <span data-ttu-id="50e88-190">Make sure that you use the FQDN address of the Always On Listener (and optional port number and instance name).</span><span class="sxs-lookup"><span data-stu-id="50e88-190">Make sure that you use the FQDN address of the Always On Listener (and optional port number and instance name).</span></span> <span data-ttu-id="50e88-191">Provide the information for the account you configured with sysadmin privileges.</span><span class="sxs-lookup"><span data-stu-id="50e88-191">Provide the information for the account you configured with sysadmin privileges.</span></span>

4. <span data-ttu-id="50e88-192">Check the Always On Availability Group box to enable support for SQL Always On Availability Group instances.</span><span class="sxs-lookup"><span data-stu-id="50e88-192">Check the Always On Availability Group box to enable support for SQL Always On Availability Group instances.</span></span>

   ![Enable Always On](./media/azure-stack-sql-rp-deploy/AlwaysOn.PNG)

5. <span data-ttu-id="50e88-194">Add the SQL Always On instance to a SKU.</span><span class="sxs-lookup"><span data-stu-id="50e88-194">Add the SQL Always On instance to a SKU.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="50e88-195">You can't mix standalone servers with Always On instances in the same SKU.</span><span class="sxs-lookup"><span data-stu-id="50e88-195">You can't mix standalone servers with Always On instances in the same SKU.</span></span> <span data-ttu-id="50e88-196">Attempting to mix types after adding the first hosting server results in an error.</span><span class="sxs-lookup"><span data-stu-id="50e88-196">Attempting to mix types after adding the first hosting server results in an error.</span></span>

## <a name="sku-notes"></a><span data-ttu-id="50e88-197">SKU notes</span><span class="sxs-lookup"><span data-stu-id="50e88-197">SKU notes</span></span>

<span data-ttu-id="50e88-198">You can use SKUs to differentiate service offerings.</span><span class="sxs-lookup"><span data-stu-id="50e88-198">You can use SKUs to differentiate service offerings.</span></span> <span data-ttu-id="50e88-199">For example, you can have a SQL Enterprise instance that has the following characteristics:</span><span class="sxs-lookup"><span data-stu-id="50e88-199">For example, you can have a SQL Enterprise instance that has the following characteristics:</span></span>
  
* <span data-ttu-id="50e88-200">high capacity</span><span class="sxs-lookup"><span data-stu-id="50e88-200">high capacity</span></span>
* <span data-ttu-id="50e88-201">high-performance</span><span class="sxs-lookup"><span data-stu-id="50e88-201">high-performance</span></span>
* <span data-ttu-id="50e88-202">high availability</span><span class="sxs-lookup"><span data-stu-id="50e88-202">high availability</span></span>

<span data-ttu-id="50e88-203">SKUs can't be assigned to specific users or groups in this release.</span><span class="sxs-lookup"><span data-stu-id="50e88-203">SKUs can't be assigned to specific users or groups in this release.</span></span>

 <span data-ttu-id="50e88-204">SKUs can take up to an hour to be visible in the portal.</span><span class="sxs-lookup"><span data-stu-id="50e88-204">SKUs can take up to an hour to be visible in the portal.</span></span> <span data-ttu-id="50e88-205">Users can't create a database until the SKU is fully created.</span><span class="sxs-lookup"><span data-stu-id="50e88-205">Users can't create a database until the SKU is fully created.</span></span>

>[!TIP]
><span data-ttu-id="50e88-206">Use a SKU name that reflects describes the capabilities of the servers in the SKU, such as capacity and performance.</span><span class="sxs-lookup"><span data-stu-id="50e88-206">Use a SKU name that reflects describes the capabilities of the servers in the SKU, such as capacity and performance.</span></span> <span data-ttu-id="50e88-207">The name serves as an aid to help users deploy their databases to the appropriate SKU.</span><span class="sxs-lookup"><span data-stu-id="50e88-207">The name serves as an aid to help users deploy their databases to the appropriate SKU.</span></span>

<span data-ttu-id="50e88-208">As a best practice, all the hosting servers in a SKU should have the same resource and performance characteristics.</span><span class="sxs-lookup"><span data-stu-id="50e88-208">As a best practice, all the hosting servers in a SKU should have the same resource and performance characteristics.</span></span>

## <a name="make-the-sql-databases-available-to-users"></a><span data-ttu-id="50e88-209">Make the SQL databases available to users</span><span class="sxs-lookup"><span data-stu-id="50e88-209">Make the SQL databases available to users</span></span>

<span data-ttu-id="50e88-210">Create plans and offers to make SQL databases available for users.</span><span class="sxs-lookup"><span data-stu-id="50e88-210">Create plans and offers to make SQL databases available for users.</span></span> <span data-ttu-id="50e88-211">Add the **Microsoft.SqlAdapter** service to the plan and create a new quota.</span><span class="sxs-lookup"><span data-stu-id="50e88-211">Add the **Microsoft.SqlAdapter** service to the plan and create a new quota.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50e88-212">Next steps</span><span class="sxs-lookup"><span data-stu-id="50e88-212">Next steps</span></span>

[<span data-ttu-id="50e88-213">Add databases</span><span class="sxs-lookup"><span data-stu-id="50e88-213">Add databases</span></span>](azure-stack-sql-resource-provider-databases.md)
