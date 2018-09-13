---
title: Configuring Oracle Data Guard in VMs | Microsoft Docs
description: Step through a tutorial for setting up and implementing Oracle Data Guard on Azure virtual machines for high availability and disaster recovery.
services: virtual-machines-windows
author: rickstercdn
manager: timlt
documentationcenter: ''
tags: azure-service-management
ms.assetid: 5ec5b9a1-7b09-4e01-ab0a-4897585d08d7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 09/06/2016
ms.author: rclaus
ms.openlocfilehash: 2085b485311f0889c646bc100a32bb41b7363cd2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552066"
---
# <a name="configuring-oracle-data-guard-for-azure"></a><span data-ttu-id="7e433-103">Configuring Oracle Data Guard for Azure</span><span class="sxs-lookup"><span data-stu-id="7e433-103">Configuring Oracle Data Guard for Azure</span></span>
<span data-ttu-id="7e433-104">This tutorial demonstrates how to set up and implement Oracle Data Guard in Azure Virtual Machines environment for high availability and disaster recovery.</span><span class="sxs-lookup"><span data-stu-id="7e433-104">This tutorial demonstrates how to set up and implement Oracle Data Guard in Azure Virtual Machines environment for high availability and disaster recovery.</span></span> <span data-ttu-id="7e433-105">The tutorial focuses on one-way replication for non-RAC Oracle databases.</span><span class="sxs-lookup"><span data-stu-id="7e433-105">The tutorial focuses on one-way replication for non-RAC Oracle databases.</span></span>

<span data-ttu-id="7e433-106">Oracle Data Guard supports data protection and disaster recovery for Oracle Database.</span><span class="sxs-lookup"><span data-stu-id="7e433-106">Oracle Data Guard supports data protection and disaster recovery for Oracle Database.</span></span> <span data-ttu-id="7e433-107">It is a simple, high-performance, drop-in solution for disaster recovery, data protection, and high availability for the entire Oracle database.</span><span class="sxs-lookup"><span data-stu-id="7e433-107">It is a simple, high-performance, drop-in solution for disaster recovery, data protection, and high availability for the entire Oracle database.</span></span>

<span data-ttu-id="7e433-108">This tutorial assumes that you already have theoretical and practical knowledge on Oracle Database High Availability and Disaster Recovery concepts.</span><span class="sxs-lookup"><span data-stu-id="7e433-108">This tutorial assumes that you already have theoretical and practical knowledge on Oracle Database High Availability and Disaster Recovery concepts.</span></span> <span data-ttu-id="7e433-109">For information, see the [Oracle web site](http://www.oracle.com/technetwork/database/features/availability/index.html) and also the [Oracle Data Guard Concepts and Administration Guide](https://docs.oracle.com/cd/E11882_01/server.112/e41134/toc.htm).</span><span class="sxs-lookup"><span data-stu-id="7e433-109">For information, see the [Oracle web site](http://www.oracle.com/technetwork/database/features/availability/index.html) and also the [Oracle Data Guard Concepts and Administration Guide](https://docs.oracle.com/cd/E11882_01/server.112/e41134/toc.htm).</span></span>

<span data-ttu-id="7e433-110">In addition, the tutorial assumes that you have already implemented the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="7e433-110">In addition, the tutorial assumes that you have already implemented the following prerequisites:</span></span>

* <span data-ttu-id="7e433-111">You’ve already reviewed the High Availability and Disaster Recovery Considerations section in the [Oracle Virtual Machine images - Miscellaneous Considerations](oracle-considerations.md) topic.</span><span class="sxs-lookup"><span data-stu-id="7e433-111">You’ve already reviewed the High Availability and Disaster Recovery Considerations section in the [Oracle Virtual Machine images - Miscellaneous Considerations](oracle-considerations.md) topic.</span></span> <span data-ttu-id="7e433-112">Azure supports standalone Oracle Database instances but not Oracle Real Application Clusters (Oracle RAC) currently.</span><span class="sxs-lookup"><span data-stu-id="7e433-112">Azure supports standalone Oracle Database instances but not Oracle Real Application Clusters (Oracle RAC) currently.</span></span>
* <span data-ttu-id="7e433-113">You have created two Virtual Machines (VMs) in Azure using the same platform provided Oracle Enterprise Edition image.</span><span class="sxs-lookup"><span data-stu-id="7e433-113">You have created two Virtual Machines (VMs) in Azure using the same platform provided Oracle Enterprise Edition image.</span></span> <span data-ttu-id="7e433-114">Make sure the Virtual Machines are in the [same cloud service](../../virtual-machines-windows-load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and in the same Virtual Network to ensure they can access each other over the persistent private IP address.</span><span class="sxs-lookup"><span data-stu-id="7e433-114">Make sure the Virtual Machines are in the [same cloud service](../../virtual-machines-windows-load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and in the same Virtual Network to ensure they can access each other over the persistent private IP address.</span></span> <span data-ttu-id="7e433-115">Additionally, it is recommended to place the VMs in the same [availability set](../../virtual-machines-windows-manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to allow Azure to place them into separate fault domains and upgrade domains.</span><span class="sxs-lookup"><span data-stu-id="7e433-115">Additionally, it is recommended to place the VMs in the same [availability set](../../virtual-machines-windows-manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to allow Azure to place them into separate fault domains and upgrade domains.</span></span> <span data-ttu-id="7e433-116">Oracle Data Guard is only available with Oracle Database Enterprise Edition.</span><span class="sxs-lookup"><span data-stu-id="7e433-116">Oracle Data Guard is only available with Oracle Database Enterprise Edition.</span></span> <span data-ttu-id="7e433-117">Each machine must have at least 2 GB of memory and 5 GB of disk space.</span><span class="sxs-lookup"><span data-stu-id="7e433-117">Each machine must have at least 2 GB of memory and 5 GB of disk space.</span></span> <span data-ttu-id="7e433-118">For the most up-to-date information on the platform provided VM sizes, see [Virtual Machine Sizes for Azure](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7e433-118">For the most up-to-date information on the platform provided VM sizes, see [Virtual Machine Sizes for Azure](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="7e433-119">If you need additional disk volume for your VMs, you can attach additional disks.</span><span class="sxs-lookup"><span data-stu-id="7e433-119">If you need additional disk volume for your VMs, you can attach additional disks.</span></span> <span data-ttu-id="7e433-120">For information, see [How to Attach a Data Disk to a Virtual Machine](attach-disk.md).</span><span class="sxs-lookup"><span data-stu-id="7e433-120">For information, see [How to Attach a Data Disk to a Virtual Machine](attach-disk.md).</span></span>
* <span data-ttu-id="7e433-121">You’ve set the Virtual Machine names as “Machine1” for the primary VM and “Machine2” for the standby VM at the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="7e433-121">You’ve set the Virtual Machine names as “Machine1” for the primary VM and “Machine2” for the standby VM at the Azure classic portal.</span></span>
* <span data-ttu-id="7e433-122">You’ve set the **ORACLE_HOME** environment variable to point to the same oracle root installation path in the primary and standby Virtual Machines, such as `C:\OracleDatabase\product\11.2.0\dbhome_1\database`.</span><span class="sxs-lookup"><span data-stu-id="7e433-122">You’ve set the **ORACLE_HOME** environment variable to point to the same oracle root installation path in the primary and standby Virtual Machines, such as `C:\OracleDatabase\product\11.2.0\dbhome_1\database`.</span></span>
* <span data-ttu-id="7e433-123">You log on to your Windows server as a member of the **Administrators** group or a member of the **ORA_DBA** group.</span><span class="sxs-lookup"><span data-stu-id="7e433-123">You log on to your Windows server as a member of the **Administrators** group or a member of the **ORA_DBA** group.</span></span>

<span data-ttu-id="7e433-124">In this tutorial, you will:</span><span class="sxs-lookup"><span data-stu-id="7e433-124">In this tutorial, you will:</span></span>

<span data-ttu-id="7e433-125">Implement the physical standby database environment</span><span class="sxs-lookup"><span data-stu-id="7e433-125">Implement the physical standby database environment</span></span>

1. <span data-ttu-id="7e433-126">Create a primary database</span><span class="sxs-lookup"><span data-stu-id="7e433-126">Create a primary database</span></span>
2. <span data-ttu-id="7e433-127">Prepare the primary database for standby database creation</span><span class="sxs-lookup"><span data-stu-id="7e433-127">Prepare the primary database for standby database creation</span></span>
   
   1. <span data-ttu-id="7e433-128">Enable forced logging</span><span class="sxs-lookup"><span data-stu-id="7e433-128">Enable forced logging</span></span>
   2. <span data-ttu-id="7e433-129">Create a password file</span><span class="sxs-lookup"><span data-stu-id="7e433-129">Create a password file</span></span>
   3. <span data-ttu-id="7e433-130">Configure a standby redo log</span><span class="sxs-lookup"><span data-stu-id="7e433-130">Configure a standby redo log</span></span>
   4. <span data-ttu-id="7e433-131">Enable Archiving</span><span class="sxs-lookup"><span data-stu-id="7e433-131">Enable Archiving</span></span>
   5. <span data-ttu-id="7e433-132">Set primary database initialization parameters</span><span class="sxs-lookup"><span data-stu-id="7e433-132">Set primary database initialization parameters</span></span>

<span data-ttu-id="7e433-133">Create a physical standby database</span><span class="sxs-lookup"><span data-stu-id="7e433-133">Create a physical standby database</span></span>

1. <span data-ttu-id="7e433-134">Prepare an initialization parameter file for standby database</span><span class="sxs-lookup"><span data-stu-id="7e433-134">Prepare an initialization parameter file for standby database</span></span>
2. <span data-ttu-id="7e433-135">Configure the listener and tnsnames to support the database on primary and standby machines</span><span class="sxs-lookup"><span data-stu-id="7e433-135">Configure the listener and tnsnames to support the database on primary and standby machines</span></span>
   
   1. <span data-ttu-id="7e433-136">Configure listener.ora on both servers to hold entries for both databases</span><span class="sxs-lookup"><span data-stu-id="7e433-136">Configure listener.ora on both servers to hold entries for both databases</span></span>
   2. <span data-ttu-id="7e433-137">To hold entries for both primary and standby databases, configure tnsnames.ora on the primary and standby Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="7e433-137">To hold entries for both primary and standby databases, configure tnsnames.ora on the primary and standby Virtual Machines.</span></span> 
   3. <span data-ttu-id="7e433-138">Start the listener and check tnsping on both Virtual Machines to both services.</span><span class="sxs-lookup"><span data-stu-id="7e433-138">Start the listener and check tnsping on both Virtual Machines to both services.</span></span>
3. <span data-ttu-id="7e433-139">Start up the standby instance in nomount state</span><span class="sxs-lookup"><span data-stu-id="7e433-139">Start up the standby instance in nomount state</span></span>
4. <span data-ttu-id="7e433-140">Use RMAN to clone the database and to create a standby database</span><span class="sxs-lookup"><span data-stu-id="7e433-140">Use RMAN to clone the database and to create a standby database</span></span>
5. <span data-ttu-id="7e433-141">Start the physical standby database in managed recovery mode</span><span class="sxs-lookup"><span data-stu-id="7e433-141">Start the physical standby database in managed recovery mode</span></span>
6. <span data-ttu-id="7e433-142">Verify the physical standby database</span><span class="sxs-lookup"><span data-stu-id="7e433-142">Verify the physical standby database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7e433-143">This tutorial has been set up and tested against the following hardware and software configuration:</span><span class="sxs-lookup"><span data-stu-id="7e433-143">This tutorial has been set up and tested against the following hardware and software configuration:</span></span>
> 
> |  | <span data-ttu-id="7e433-144">**Primary Database**</span><span class="sxs-lookup"><span data-stu-id="7e433-144">**Primary Database**</span></span> | <span data-ttu-id="7e433-145">**Standby Database**</span><span class="sxs-lookup"><span data-stu-id="7e433-145">**Standby Database**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="7e433-146">**Oracle Release**</span><span class="sxs-lookup"><span data-stu-id="7e433-146">**Oracle Release**</span></span> |<span data-ttu-id="7e433-147">Oracle11g Enterprise Release (11.2.0.4.0)</span><span class="sxs-lookup"><span data-stu-id="7e433-147">Oracle11g Enterprise Release (11.2.0.4.0)</span></span> |<span data-ttu-id="7e433-148">Oracle11g Enterprise Release (11.2.0.4.0)</span><span class="sxs-lookup"><span data-stu-id="7e433-148">Oracle11g Enterprise Release (11.2.0.4.0)</span></span> |
> | <span data-ttu-id="7e433-149">**Machine Name**</span><span class="sxs-lookup"><span data-stu-id="7e433-149">**Machine Name**</span></span> |<span data-ttu-id="7e433-150">Machine1</span><span class="sxs-lookup"><span data-stu-id="7e433-150">Machine1</span></span> |<span data-ttu-id="7e433-151">Machine2</span><span class="sxs-lookup"><span data-stu-id="7e433-151">Machine2</span></span> |
> | <span data-ttu-id="7e433-152">**Operating System**</span><span class="sxs-lookup"><span data-stu-id="7e433-152">**Operating System**</span></span> |<span data-ttu-id="7e433-153">Windows 2008 R2</span><span class="sxs-lookup"><span data-stu-id="7e433-153">Windows 2008 R2</span></span> |<span data-ttu-id="7e433-154">Windows 2008 R2</span><span class="sxs-lookup"><span data-stu-id="7e433-154">Windows 2008 R2</span></span> |
> | <span data-ttu-id="7e433-155">**Oracle SID**</span><span class="sxs-lookup"><span data-stu-id="7e433-155">**Oracle SID**</span></span> |<span data-ttu-id="7e433-156">TEST</span><span class="sxs-lookup"><span data-stu-id="7e433-156">TEST</span></span> |<span data-ttu-id="7e433-157">TEST\_STBY</span><span class="sxs-lookup"><span data-stu-id="7e433-157">TEST\_STBY</span></span> |
> | <span data-ttu-id="7e433-158">**Memory**</span><span class="sxs-lookup"><span data-stu-id="7e433-158">**Memory**</span></span> |<span data-ttu-id="7e433-159">Min 2 GB</span><span class="sxs-lookup"><span data-stu-id="7e433-159">Min 2 GB</span></span> |<span data-ttu-id="7e433-160">Min 2 GB</span><span class="sxs-lookup"><span data-stu-id="7e433-160">Min 2 GB</span></span> |
> | <span data-ttu-id="7e433-161">**Disk Space**</span><span class="sxs-lookup"><span data-stu-id="7e433-161">**Disk Space**</span></span> |<span data-ttu-id="7e433-162">Min 5 GB</span><span class="sxs-lookup"><span data-stu-id="7e433-162">Min 5 GB</span></span> |<span data-ttu-id="7e433-163">Min 5 GB</span><span class="sxs-lookup"><span data-stu-id="7e433-163">Min 5 GB</span></span> |
> 
> 

<span data-ttu-id="7e433-164">For subsequent releases of Oracle Database and Oracle Data Guard, there might be some additional changes that you need to implement.</span><span class="sxs-lookup"><span data-stu-id="7e433-164">For subsequent releases of Oracle Database and Oracle Data Guard, there might be some additional changes that you need to implement.</span></span> <span data-ttu-id="7e433-165">For the most up-to-date version-specific information, see [Data Guard](http://www.oracle.com/technetwork/database/features/availability/data-guard-documentation-152848.html) and [Oracle Database](http://www.oracle.com/us/corporate/features/database-12c/index.html) documentation at Oracle web site.</span><span class="sxs-lookup"><span data-stu-id="7e433-165">For the most up-to-date version-specific information, see [Data Guard](http://www.oracle.com/technetwork/database/features/availability/data-guard-documentation-152848.html) and [Oracle Database](http://www.oracle.com/us/corporate/features/database-12c/index.html) documentation at Oracle web site.</span></span>

## <a name="implement-the-physical-standby-database-environment"></a><span data-ttu-id="7e433-166">Implement the physical standby database environment</span><span class="sxs-lookup"><span data-stu-id="7e433-166">Implement the physical standby database environment</span></span>
### <a name="1-create-a-primary-database"></a><span data-ttu-id="7e433-167">1. Create a primary database</span><span class="sxs-lookup"><span data-stu-id="7e433-167">1. Create a primary database</span></span>
* <span data-ttu-id="7e433-168">Create a primary database “TEST” in the primary Virtual Machine.</span><span class="sxs-lookup"><span data-stu-id="7e433-168">Create a primary database “TEST” in the primary Virtual Machine.</span></span> <span data-ttu-id="7e433-169">For information, see Creating and Configuring an Oracle Database.</span><span class="sxs-lookup"><span data-stu-id="7e433-169">For information, see Creating and Configuring an Oracle Database.</span></span>
* <span data-ttu-id="7e433-170">To see the name of your database, connect to your database as the SYS user with SYSDBA role in the SQL\*Plus command prompt and run the following statement:</span><span class="sxs-lookup"><span data-stu-id="7e433-170">To see the name of your database, connect to your database as the SYS user with SYSDBA role in the SQL\*Plus command prompt and run the following statement:</span></span>
  
        SQL> select name from v$database;
  
        The result will display like the following:
  
        NAME
        ---------
        TEST
* <span data-ttu-id="7e433-171">Next, query the names of the database files from the dba_data_files system view:</span><span class="sxs-lookup"><span data-stu-id="7e433-171">Next, query the names of the database files from the dba_data_files system view:</span></span>
  
        SQL> select file_name from dba_data_files;
        FILE_NAME
        -------------------------------------------------------------------------------
        C:\ <YourLocalFolder>\TEST\USERS01.DBF
        C:\ <YourLocalFolder>\TEST\UNDOTBS01.DBF
        C:\ <YourLocalFolder>\TEST\SYSAUX01.DBF
        C:\<YourLocalFolder>\TEST\SYSTEM01.DBF
        C:\<YourLocalFolder>\TEST\EXAMPLE01.DBF

### <a name="2-prepare-the-primary-database-for-standby-database-creation"></a><span data-ttu-id="7e433-172">2. Prepare the primary database for standby database creation</span><span class="sxs-lookup"><span data-stu-id="7e433-172">2. Prepare the primary database for standby database creation</span></span>
<span data-ttu-id="7e433-173">Before creating a standby database, it’s recommended that you ensure the primary database is configured properly.</span><span class="sxs-lookup"><span data-stu-id="7e433-173">Before creating a standby database, it’s recommended that you ensure the primary database is configured properly.</span></span> <span data-ttu-id="7e433-174">The following is a list of steps that you need to perform:</span><span class="sxs-lookup"><span data-stu-id="7e433-174">The following is a list of steps that you need to perform:</span></span>

1. <span data-ttu-id="7e433-175">Enable forced logging</span><span class="sxs-lookup"><span data-stu-id="7e433-175">Enable forced logging</span></span>
2. <span data-ttu-id="7e433-176">Create a password file</span><span class="sxs-lookup"><span data-stu-id="7e433-176">Create a password file</span></span>
3. <span data-ttu-id="7e433-177">Configure a standby redo log</span><span class="sxs-lookup"><span data-stu-id="7e433-177">Configure a standby redo log</span></span>
4. <span data-ttu-id="7e433-178">Enable Archiving</span><span class="sxs-lookup"><span data-stu-id="7e433-178">Enable Archiving</span></span>
5. <span data-ttu-id="7e433-179">Set primary database initialization parameters</span><span class="sxs-lookup"><span data-stu-id="7e433-179">Set primary database initialization parameters</span></span>

#### <a name="enable-forced-logging"></a><span data-ttu-id="7e433-180">Enable forced logging</span><span class="sxs-lookup"><span data-stu-id="7e433-180">Enable forced logging</span></span>
<span data-ttu-id="7e433-181">To implement a Standby Database, we need to enable 'Forced Logging' in the primary database.</span><span class="sxs-lookup"><span data-stu-id="7e433-181">To implement a Standby Database, we need to enable 'Forced Logging' in the primary database.</span></span> <span data-ttu-id="7e433-182">This option ensures that even if an 'nologging' operation is done, force logging takes precedence and all operations are logged into the redo logs.</span><span class="sxs-lookup"><span data-stu-id="7e433-182">This option ensures that even if an 'nologging' operation is done, force logging takes precedence and all operations are logged into the redo logs.</span></span> <span data-ttu-id="7e433-183">Therefore, we make sure that everything in the primary database is logged and replication to the standby includes all operations in the primary database.</span><span class="sxs-lookup"><span data-stu-id="7e433-183">Therefore, we make sure that everything in the primary database is logged and replication to the standby includes all operations in the primary database.</span></span> <span data-ttu-id="7e433-184">To enable force logging, run the alter database statement:</span><span class="sxs-lookup"><span data-stu-id="7e433-184">To enable force logging, run the alter database statement:</span></span>

    SQL> ALTER DATABASE FORCE LOGGING;

    Database altered.

#### <a name="create-a-password-file"></a><span data-ttu-id="7e433-185">Create a password file</span><span class="sxs-lookup"><span data-stu-id="7e433-185">Create a password file</span></span>
<span data-ttu-id="7e433-186">To be able to ship and apply archived logs from the Primary server to the Standby server, the sys password must be identical on both primary and standby servers.</span><span class="sxs-lookup"><span data-stu-id="7e433-186">To be able to ship and apply archived logs from the Primary server to the Standby server, the sys password must be identical on both primary and standby servers.</span></span> <span data-ttu-id="7e433-187">That’s why you create a password file on the primary database and copy it to the Standby server.</span><span class="sxs-lookup"><span data-stu-id="7e433-187">That’s why you create a password file on the primary database and copy it to the Standby server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7e433-188">When using Oracle Database 12c, there is a new user, **SYSDG**, which you can use to administer Oracle Data Guard.</span><span class="sxs-lookup"><span data-stu-id="7e433-188">When using Oracle Database 12c, there is a new user, **SYSDG**, which you can use to administer Oracle Data Guard.</span></span> <span data-ttu-id="7e433-189">For more information, see [Changes in Oracle Database 12c Release](http://docs.oracle.com/database/121/UNXAR/release_changes.htm#UNXAR404).</span><span class="sxs-lookup"><span data-stu-id="7e433-189">For more information, see [Changes in Oracle Database 12c Release](http://docs.oracle.com/database/121/UNXAR/release_changes.htm#UNXAR404).</span></span>
> 
> 

<span data-ttu-id="7e433-190">In addition, make sure that the ORACLE\_HOME environment is already defined in Machine1.</span><span class="sxs-lookup"><span data-stu-id="7e433-190">In addition, make sure that the ORACLE\_HOME environment is already defined in Machine1.</span></span> <span data-ttu-id="7e433-191">If not, define it as an environment variable using the Environment Variables dialog box.</span><span class="sxs-lookup"><span data-stu-id="7e433-191">If not, define it as an environment variable using the Environment Variables dialog box.</span></span> <span data-ttu-id="7e433-192">To access this dialog box, start the **System** utility by double-clicking the System icon in the **Control Panel**; then click the **Advanced** tab and choose **Environment Variables**.</span><span class="sxs-lookup"><span data-stu-id="7e433-192">To access this dialog box, start the **System** utility by double-clicking the System icon in the **Control Panel**; then click the **Advanced** tab and choose **Environment Variables**.</span></span> <span data-ttu-id="7e433-193">To set the environment variables, click the **New** button under **System Variables**.</span><span class="sxs-lookup"><span data-stu-id="7e433-193">To set the environment variables, click the **New** button under **System Variables**.</span></span> <span data-ttu-id="7e433-194">After setting up the environment variables, close the existing Windows command prompt and open up a new one.</span><span class="sxs-lookup"><span data-stu-id="7e433-194">After setting up the environment variables, close the existing Windows command prompt and open up a new one.</span></span>

<span data-ttu-id="7e433-195">Run the following statement to switch to the Oracle\_Home directory, such as C:\\OracleDatabase\\product\\11.2.0\\dbhome\_1\\database.</span><span class="sxs-lookup"><span data-stu-id="7e433-195">Run the following statement to switch to the Oracle\_Home directory, such as C:\\OracleDatabase\\product\\11.2.0\\dbhome\_1\\database.</span></span>

    cd %ORACLE_HOME%\database

<span data-ttu-id="7e433-196">Then, create a password file using the password file creation utility, [ORAPWD](http://docs.oracle.com/cd/B28359_01/server.111/b28310/dba007.htm).</span><span class="sxs-lookup"><span data-stu-id="7e433-196">Then, create a password file using the password file creation utility, [ORAPWD](http://docs.oracle.com/cd/B28359_01/server.111/b28310/dba007.htm).</span></span> <span data-ttu-id="7e433-197">In the same Windows command prompt in Machine1, run the following command by setting the password value as the password of **SYS**:</span><span class="sxs-lookup"><span data-stu-id="7e433-197">In the same Windows command prompt in Machine1, run the following command by setting the password value as the password of **SYS**:</span></span>

    ORAPWD FILE=PWDTEST.ora PASSWORD=password FORCE=y

<span data-ttu-id="7e433-198">This command creates a password file, named as PWDTEST.ora, in the ORACLE\_HOME\\database directory.</span><span class="sxs-lookup"><span data-stu-id="7e433-198">This command creates a password file, named as PWDTEST.ora, in the ORACLE\_HOME\\database directory.</span></span> <span data-ttu-id="7e433-199">You should copy this file to %ORACLE\_HOME%\\database directory in Machine2 manually.</span><span class="sxs-lookup"><span data-stu-id="7e433-199">You should copy this file to %ORACLE\_HOME%\\database directory in Machine2 manually.</span></span>

#### <a name="configure-a-standby-redo-log"></a><span data-ttu-id="7e433-200">Configure a standby redo log</span><span class="sxs-lookup"><span data-stu-id="7e433-200">Configure a standby redo log</span></span>
<span data-ttu-id="7e433-201">Then, you need to configure a Standby Redo Log so that the primary can correctly receive the redo when it becomes a standby.</span><span class="sxs-lookup"><span data-stu-id="7e433-201">Then, you need to configure a Standby Redo Log so that the primary can correctly receive the redo when it becomes a standby.</span></span> <span data-ttu-id="7e433-202">Pre-creating them here also allows the standby redo logs to be automatically created on the standby.</span><span class="sxs-lookup"><span data-stu-id="7e433-202">Pre-creating them here also allows the standby redo logs to be automatically created on the standby.</span></span> <span data-ttu-id="7e433-203">It is important to configure the Standby Redo Logs (SRL) with the same size as the online redo logs.</span><span class="sxs-lookup"><span data-stu-id="7e433-203">It is important to configure the Standby Redo Logs (SRL) with the same size as the online redo logs.</span></span> <span data-ttu-id="7e433-204">The size of the current standby redo log files must exactly match the size of the current primary database online redo log files.</span><span class="sxs-lookup"><span data-stu-id="7e433-204">The size of the current standby redo log files must exactly match the size of the current primary database online redo log files.</span></span>

<span data-ttu-id="7e433-205">Run the following statement in the SQL\*PLUS command prompt in Machine1.</span><span class="sxs-lookup"><span data-stu-id="7e433-205">Run the following statement in the SQL\*PLUS command prompt in Machine1.</span></span> <span data-ttu-id="7e433-206">The v$logfile is a system view that contains information about redo log files.</span><span class="sxs-lookup"><span data-stu-id="7e433-206">The v$logfile is a system view that contains information about redo log files.</span></span>

    SQL> select * from v$logfile;
    GROUP# STATUS  TYPE    MEMBER                                                       IS_
    ---------- ------- ------- ------------------------------------------------------------ ---
    3         ONLINE  C:\<YourLocalFolder>\TEST\REDO03.LOG               NO
    2         ONLINE  C:\<YourLocalFolder>\TEST\REDO02.LOG               NO
    1         ONLINE  C:\<YourLocalFolder>\TEST\REDO01.LOG               NO
    Next, query the v$log system view, displays log file information from the control file.
    SQL> select bytes from v$log;
    BYTES
    ----------
    52428800
    52428800
    52428800


<span data-ttu-id="7e433-207">Note that 52428800 is 50 megabytes.</span><span class="sxs-lookup"><span data-stu-id="7e433-207">Note that 52428800 is 50 megabytes.</span></span>

<span data-ttu-id="7e433-208">Then, in the SQL\*Plus window, run the following statements to add a new standby redo log file group to a standby database and specify a number that identifies the group using the GROUP clause.</span><span class="sxs-lookup"><span data-stu-id="7e433-208">Then, in the SQL\*Plus window, run the following statements to add a new standby redo log file group to a standby database and specify a number that identifies the group using the GROUP clause.</span></span> <span data-ttu-id="7e433-209">Using group numbers can make administering standby redo log file groups easier:</span><span class="sxs-lookup"><span data-stu-id="7e433-209">Using group numbers can make administering standby redo log file groups easier:</span></span>

    SQL> ALTER DATABASE ADD STANDBY LOGFILE GROUP 4 'C:\<YourLocalFolder>\TEST\REDO04.LOG' SIZE 50M;
    Database altered.
    SQL> ALTER DATABASE ADD STANDBY LOGFILE GROUP 5 'C:\<YourLocalFolder>\TEST\REDO05.LOG' SIZE 50M;
    Database altered.
    SQL> ALTER DATABASE ADD STANDBY LOGFILE GROUP 6 'C:\<YourLocalFolder>\TEST\REDO06.LOG' SIZE 50M;
    Database altered.

<span data-ttu-id="7e433-210">Next, run the following system view to list information about redo log files.</span><span class="sxs-lookup"><span data-stu-id="7e433-210">Next, run the following system view to list information about redo log files.</span></span> <span data-ttu-id="7e433-211">This operation also verifies that the standby redo log file groups were created:</span><span class="sxs-lookup"><span data-stu-id="7e433-211">This operation also verifies that the standby redo log file groups were created:</span></span>

    SQL> select * from v$logfile;
    GROUP# STATUS  TYPE MEMBER IS_
    ---------- ------- ------- --------------------------------------------- ---
    3         ONLINE C:\<YourLocalFolder>\TEST\REDO03.LOG NO
    2         ONLINE C:\<YourLocalFolder>\TEST\REDO02.LOG NO
    1         ONLINE C:\<YourLocalFolder>\TEST\REDO01.LOG NO
    4         STANDBY C:\<YourLocalFolder>\TEST\REDO04.LOG
    5         STANDBY C:\<YourLocalFolder>\TEST\REDO05.LOG NO
    6         STANDBY C:\<YourLocalFolder>\TEST\REDO06.LOG NO
    6 rows selected.

#### <a name="enable-archiving"></a><span data-ttu-id="7e433-212">Enable Archiving</span><span class="sxs-lookup"><span data-stu-id="7e433-212">Enable Archiving</span></span>
<span data-ttu-id="7e433-213">Then, enable archiving by running the following statements to put the primary database in ARCHIVELOG mode and enable automatic archiving.</span><span class="sxs-lookup"><span data-stu-id="7e433-213">Then, enable archiving by running the following statements to put the primary database in ARCHIVELOG mode and enable automatic archiving.</span></span> <span data-ttu-id="7e433-214">You can enable archive log mode by mounting the database and then executing the archivelog command.</span><span class="sxs-lookup"><span data-stu-id="7e433-214">You can enable archive log mode by mounting the database and then executing the archivelog command.</span></span>

<span data-ttu-id="7e433-215">First, log in as sysdba.</span><span class="sxs-lookup"><span data-stu-id="7e433-215">First, log in as sysdba.</span></span> <span data-ttu-id="7e433-216">In the Windows command prompt, run:</span><span class="sxs-lookup"><span data-stu-id="7e433-216">In the Windows command prompt, run:</span></span>

    sqlplus /nolog

    connect / as sysdba

<span data-ttu-id="7e433-217">Then, shutdown the database in the SQL\*Plus command prompt:</span><span class="sxs-lookup"><span data-stu-id="7e433-217">Then, shutdown the database in the SQL\*Plus command prompt:</span></span>

    SQL> shutdown immediate;
    Database closed.
    Database dismounted.
    ORACLE instance shut down.

<span data-ttu-id="7e433-218">Then, execute the startup mount command to mount the database.</span><span class="sxs-lookup"><span data-stu-id="7e433-218">Then, execute the startup mount command to mount the database.</span></span> <span data-ttu-id="7e433-219">This ensures that Oracle associates the instance with the specified database.</span><span class="sxs-lookup"><span data-stu-id="7e433-219">This ensures that Oracle associates the instance with the specified database.</span></span>

    SQL> startup mount;
    ORACLE instance started.
    Total System Global Area 1503199232 bytes
    Fixed Size                  2281416 bytes
    Variable Size             922746936 bytes
    Database Buffers          570425344 bytes
    Redo Buffers                7745536 bytes
    Database mounted.

<span data-ttu-id="7e433-220">Then, run:</span><span class="sxs-lookup"><span data-stu-id="7e433-220">Then, run:</span></span>

    SQL> alter database archivelog;
    Database altered.

<span data-ttu-id="7e433-221">Then, run the Alter database statement with the Open clause to make the database available for normal use:</span><span class="sxs-lookup"><span data-stu-id="7e433-221">Then, run the Alter database statement with the Open clause to make the database available for normal use:</span></span>

    SQL> alter database open;

    Database altered.

#### <a name="set-primary-database-initialization-parameters"></a><span data-ttu-id="7e433-222">Set primary database initialization parameters</span><span class="sxs-lookup"><span data-stu-id="7e433-222">Set primary database initialization parameters</span></span>
<span data-ttu-id="7e433-223">To configure the Data Guard, you need to create and configure the standby parameters on a regular pfile (text initialization parameter file) first.</span><span class="sxs-lookup"><span data-stu-id="7e433-223">To configure the Data Guard, you need to create and configure the standby parameters on a regular pfile (text initialization parameter file) first.</span></span> <span data-ttu-id="7e433-224">When the pfile is ready, you need to convert it to a server parameter file (SPFILE).</span><span class="sxs-lookup"><span data-stu-id="7e433-224">When the pfile is ready, you need to convert it to a server parameter file (SPFILE).</span></span>

<span data-ttu-id="7e433-225">You can control the Data Guard environment using the parameters in the INIT.ORA file.</span><span class="sxs-lookup"><span data-stu-id="7e433-225">You can control the Data Guard environment using the parameters in the INIT.ORA file.</span></span> <span data-ttu-id="7e433-226">When following this tutorial, you need to update the Primary database INIT.ORA so that it can hold both roles: Primary or Standby.</span><span class="sxs-lookup"><span data-stu-id="7e433-226">When following this tutorial, you need to update the Primary database INIT.ORA so that it can hold both roles: Primary or Standby.</span></span>

    SQL> create pfile from spfile;
    File created.

<span data-ttu-id="7e433-227">Next, you need to edit the pfile to add the standby parameters.</span><span class="sxs-lookup"><span data-stu-id="7e433-227">Next, you need to edit the pfile to add the standby parameters.</span></span> <span data-ttu-id="7e433-228">To do this, open the INITTEST.ORA file in the location of %ORACLE\_HOME%\\database.</span><span class="sxs-lookup"><span data-stu-id="7e433-228">To do this, open the INITTEST.ORA file in the location of %ORACLE\_HOME%\\database.</span></span> <span data-ttu-id="7e433-229">Next, append the following statements to the INITTEST.ora file.</span><span class="sxs-lookup"><span data-stu-id="7e433-229">Next, append the following statements to the INITTEST.ora file.</span></span> <span data-ttu-id="7e433-230">The naming convention for your INIT.ORA file is INIT\<YourDatabaseName\>.ORA.</span><span class="sxs-lookup"><span data-stu-id="7e433-230">The naming convention for your INIT.ORA file is INIT\<YourDatabaseName\>.ORA.</span></span>

    db_name='TEST'
    db_unique_name='TEST'
    LOG_ARCHIVE_CONFIG='DG_CONFIG=(TEST,TEST_STBY)'
    LOG_ARCHIVE_DEST_1= 'LOCATION=C:\OracleDatabase\archive   VALID_FOR=(ALL_LOGFILES,ALL_ROLES) DB_UNIQUE_NAME=TEST'
    LOG_ARCHIVE_DEST_2= 'SERVICE=TEST_STBY LGWR ASYNC VALID_FOR=(ONLINE_LOGFILES,PRIMARY_ROLE) DB_UNIQUE_NAME=TEST_STBY'
    LOG_ARCHIVE_DEST_STATE_1=ENABLE
    LOG_ARCHIVE_DEST_STATE_2=ENABLE
    REMOTE_LOGIN_PASSWORDFILE=EXCLUSIVE
    LOG_ARCHIVE_FORMAT=%t_%s_%r.arc
    LOG_ARCHIVE_MAX_PROCESSES=30
    # Standby role parameters --------------------------------------------------------------------
    fal_server=TEST_STBY
    fal_client=TEST
    standby_file_management=auto
    db_file_name_convert='TEST_STBY','TEST'
    log_file_name_convert='TEST_STBY','TEST'
    # ---------------------------------------------------------------------------------------------


<span data-ttu-id="7e433-231">The previous statement block includes three important setup items:</span><span class="sxs-lookup"><span data-stu-id="7e433-231">The previous statement block includes three important setup items:</span></span>

* <span data-ttu-id="7e433-232">**LOG_ARCHIVE_CONFIG...:** You define the unique database ids using this statement.</span><span class="sxs-lookup"><span data-stu-id="7e433-232">**LOG_ARCHIVE_CONFIG...:** You define the unique database ids using this statement.</span></span>
* <span data-ttu-id="7e433-233">**LOG_ARCHIVE_DEST_1...:** You define the local archive folder location using this statement.</span><span class="sxs-lookup"><span data-stu-id="7e433-233">**LOG_ARCHIVE_DEST_1...:** You define the local archive folder location using this statement.</span></span> <span data-ttu-id="7e433-234">We recommend you create a new directory for your database’s archiving needs and specify the local archive location using this statement explicitly rather than using Oracle’s default folder %ORACLE_HOME%\database\archive.</span><span class="sxs-lookup"><span data-stu-id="7e433-234">We recommend you create a new directory for your database’s archiving needs and specify the local archive location using this statement explicitly rather than using Oracle’s default folder %ORACLE_HOME%\database\archive.</span></span>
* <span data-ttu-id="7e433-235">**LOG_ARCHIVE_DEST_2 .... LGWR ASYNC...:** You define an asynchronous log writer process (LGWR) to collect transaction redo data and transmit it to standby destinations.</span><span class="sxs-lookup"><span data-stu-id="7e433-235">**LOG_ARCHIVE_DEST_2 .... LGWR ASYNC...:** You define an asynchronous log writer process (LGWR) to collect transaction redo data and transmit it to standby destinations.</span></span> <span data-ttu-id="7e433-236">Here, the DB_UNIQUE_NAME specifies a unique name for the database at the destination standby server.</span><span class="sxs-lookup"><span data-stu-id="7e433-236">Here, the DB_UNIQUE_NAME specifies a unique name for the database at the destination standby server.</span></span>

<span data-ttu-id="7e433-237">Once the new parameter file is ready, you need to create the spfile from it.</span><span class="sxs-lookup"><span data-stu-id="7e433-237">Once the new parameter file is ready, you need to create the spfile from it.</span></span>

<span data-ttu-id="7e433-238">First, shutdown the database:</span><span class="sxs-lookup"><span data-stu-id="7e433-238">First, shutdown the database:</span></span>

    SQL> shutdown immediate;

    Database closed.

    Database dismounted.

    ORACLE instance shut down.

<span data-ttu-id="7e433-239">Next, run startup nomount command as follows:</span><span class="sxs-lookup"><span data-stu-id="7e433-239">Next, run startup nomount command as follows:</span></span>

    SQL> startup nomount pfile='c:\OracleDatabase\product\11.2.0\dbhome_1\database\initTEST.ora';
    ORACLE instance started.
    Total System Global Area 1503199232 bytes
    Fixed Size                  2281416 bytes
    Variable Size             922746936 bytes
    Database Buffers          570425344 bytes
    Redo Buffers                7745536 bytes

<span data-ttu-id="7e433-240">Now, create an spfile:</span><span class="sxs-lookup"><span data-stu-id="7e433-240">Now, create an spfile:</span></span>

    SQL>create spfile frompfile='c:\OracleDatabase\product\11.2.0\dbhome\_1\database\initTEST.ora';

    File created.

<span data-ttu-id="7e433-241">Then, shutdown the database:</span><span class="sxs-lookup"><span data-stu-id="7e433-241">Then, shutdown the database:</span></span>

    SQL> shutdown immediate;

    ORA-01507: database not mounted

<span data-ttu-id="7e433-242">Then, use the startup command to start an instance:</span><span class="sxs-lookup"><span data-stu-id="7e433-242">Then, use the startup command to start an instance:</span></span>

    SQL> startup;
    ORACLE instance started.
    Total System Global Area 1503199232 bytes
    Fixed Size                  2281416 bytes
    Variable Size             922746936 bytes
    Database Buffers          570425344 bytes
    Redo Buffers                7745536 bytes
    Database mounted.
    Database opened.

## <a name="create-a-physical-standby-database"></a><span data-ttu-id="7e433-243">Create a physical standby database</span><span class="sxs-lookup"><span data-stu-id="7e433-243">Create a physical standby database</span></span>
<span data-ttu-id="7e433-244">This section focuses on the steps that you must perform in Machine2 to prepare the physical standby database.</span><span class="sxs-lookup"><span data-stu-id="7e433-244">This section focuses on the steps that you must perform in Machine2 to prepare the physical standby database.</span></span>

<span data-ttu-id="7e433-245">First, you need to remote desktop to Machine2 via the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="7e433-245">First, you need to remote desktop to Machine2 via the Azure classic portal.</span></span>

<span data-ttu-id="7e433-246">Then, on the Standby Server (Machine2), create all the necessary folders for the standby database, such as C:\\\<YourLocalFolder\>\\TEST.</span><span class="sxs-lookup"><span data-stu-id="7e433-246">Then, on the Standby Server (Machine2), create all the necessary folders for the standby database, such as C:\\\<YourLocalFolder\>\\TEST.</span></span> <span data-ttu-id="7e433-247">While following this tutorial, make sure that the folder structure matches the folder structure on Machine1 to keep all the necessary files, such as controlfile, datafiles, redologfiles, udump, bdump, and cdump files.</span><span class="sxs-lookup"><span data-stu-id="7e433-247">While following this tutorial, make sure that the folder structure matches the folder structure on Machine1 to keep all the necessary files, such as controlfile, datafiles, redologfiles, udump, bdump, and cdump files.</span></span> <span data-ttu-id="7e433-248">In addition, define the ORACLE\_HOME and ORACLE\_BASE environment variables in Machine2.</span><span class="sxs-lookup"><span data-stu-id="7e433-248">In addition, define the ORACLE\_HOME and ORACLE\_BASE environment variables in Machine2.</span></span> <span data-ttu-id="7e433-249">If not, define them as an environment variable using the Environment Variables dialog box.</span><span class="sxs-lookup"><span data-stu-id="7e433-249">If not, define them as an environment variable using the Environment Variables dialog box.</span></span> <span data-ttu-id="7e433-250">To access this dialog box, start the **System** utility by double-clicking the System icon in the **Control Panel**; then click the **Advanced** tab and choose **Environment Variables**.</span><span class="sxs-lookup"><span data-stu-id="7e433-250">To access this dialog box, start the **System** utility by double-clicking the System icon in the **Control Panel**; then click the **Advanced** tab and choose **Environment Variables**.</span></span> <span data-ttu-id="7e433-251">To set the environment variables, click the **New** button under the **System Variables**.</span><span class="sxs-lookup"><span data-stu-id="7e433-251">To set the environment variables, click the **New** button under the **System Variables**.</span></span> <span data-ttu-id="7e433-252">After setting up the environment variables, you need to close the existing Windows command prompt and open up a new one to see the changes.</span><span class="sxs-lookup"><span data-stu-id="7e433-252">After setting up the environment variables, you need to close the existing Windows command prompt and open up a new one to see the changes.</span></span>

<span data-ttu-id="7e433-253">Next, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="7e433-253">Next, follow these steps:</span></span>

1. <span data-ttu-id="7e433-254">Prepare an initialization parameter file for standby database</span><span class="sxs-lookup"><span data-stu-id="7e433-254">Prepare an initialization parameter file for standby database</span></span>
2. <span data-ttu-id="7e433-255">Configure the listener and tnsnames to support the database on primary and standby machines</span><span class="sxs-lookup"><span data-stu-id="7e433-255">Configure the listener and tnsnames to support the database on primary and standby machines</span></span>
   
   1. <span data-ttu-id="7e433-256">Configure listener.ora on both servers to hold entries for both databases</span><span class="sxs-lookup"><span data-stu-id="7e433-256">Configure listener.ora on both servers to hold entries for both databases</span></span>
   2. <span data-ttu-id="7e433-257">Configure tnsnames.ora on the primary and standby Virtual Machines to hold entries for both primary and standby databases</span><span class="sxs-lookup"><span data-stu-id="7e433-257">Configure tnsnames.ora on the primary and standby Virtual Machines to hold entries for both primary and standby databases</span></span>
   3. <span data-ttu-id="7e433-258">Start the listener and check tnsping on both Virtual Machines to both services.</span><span class="sxs-lookup"><span data-stu-id="7e433-258">Start the listener and check tnsping on both Virtual Machines to both services.</span></span>
3. <span data-ttu-id="7e433-259">Start up the standby instance in nomount state</span><span class="sxs-lookup"><span data-stu-id="7e433-259">Start up the standby instance in nomount state</span></span>
4. <span data-ttu-id="7e433-260">Use RMAN to clone the database and to create a standby database</span><span class="sxs-lookup"><span data-stu-id="7e433-260">Use RMAN to clone the database and to create a standby database</span></span>
5. <span data-ttu-id="7e433-261">Start the physical standby database in managed recovery mode</span><span class="sxs-lookup"><span data-stu-id="7e433-261">Start the physical standby database in managed recovery mode</span></span>
6. <span data-ttu-id="7e433-262">Verify the physical standby database</span><span class="sxs-lookup"><span data-stu-id="7e433-262">Verify the physical standby database</span></span>

### <a name="1-prepare-an-initialization-parameter-file-for-standby-database"></a><span data-ttu-id="7e433-263">1. Prepare an initialization parameter file for standby database</span><span class="sxs-lookup"><span data-stu-id="7e433-263">1. Prepare an initialization parameter file for standby database</span></span>
<span data-ttu-id="7e433-264">This section demonstrates how to prepare an initialization parameter file for the standby database.</span><span class="sxs-lookup"><span data-stu-id="7e433-264">This section demonstrates how to prepare an initialization parameter file for the standby database.</span></span> <span data-ttu-id="7e433-265">To do this, first copy the INITTEST.ORA file from Machine 1 to Machine2 manually.</span><span class="sxs-lookup"><span data-stu-id="7e433-265">To do this, first copy the INITTEST.ORA file from Machine 1 to Machine2 manually.</span></span> <span data-ttu-id="7e433-266">You should be able to see the INITTEST.ORA file in the %ORACLE\_HOME%\\database folder in both machines.</span><span class="sxs-lookup"><span data-stu-id="7e433-266">You should be able to see the INITTEST.ORA file in the %ORACLE\_HOME%\\database folder in both machines.</span></span> <span data-ttu-id="7e433-267">Then, modify the INITTEST.ora file in Machine2 to set it up for the standby role as specified below:</span><span class="sxs-lookup"><span data-stu-id="7e433-267">Then, modify the INITTEST.ora file in Machine2 to set it up for the standby role as specified below:</span></span>

    db_name='TEST'
    db_unique_name='TEST_STBY'
    db_create_file_dest='c:\OracleDatabase\oradata\test_stby’
    db_file_name_convert=’TEST’,’TEST_STBY’
    log_file_name_convert='TEST','TEST_STBY'


    job_queue_processes=10
    LOG_ARCHIVE_CONFIG='DG_CONFIG=(TEST,TEST_STBY)'
    LOG_ARCHIVE_DEST_1='LOCATION=c:\OracleDatabase\TEST_STBY\archives VALID_FOR=(ALL_LOGFILES,ALL_ROLES) DB_UNIQUE_NAME=’TEST'
    LOG_ARCHIVE_DEST_2='SERVICE=TEST LGWR ASYNC VALID_FOR=(ONLINE_LOGFILES,PRIMARY_ROLE)
    LOG_ARCHIVE_DEST_STATE_1='ENABLE'
    LOG_ARCHIVE_DEST_STATE_2='ENABLE'
    LOG_ARCHIVE_FORMAT='%t_%s_%r.arc'
    LOG_ARCHIVE_MAX_PROCESSES=30


<span data-ttu-id="7e433-268">The previous statement block includes two important setup items:</span><span class="sxs-lookup"><span data-stu-id="7e433-268">The previous statement block includes two important setup items:</span></span>

* <span data-ttu-id="7e433-269">**\*.LOG_ARCHIVE_DEST_1:** You need to create the c:\OracleDatabase\TEST_STBY\archives folder in Machine2 manually.</span><span class="sxs-lookup"><span data-stu-id="7e433-269">**\*.LOG_ARCHIVE_DEST_1:** You need to create the c:\OracleDatabase\TEST_STBY\archives folder in Machine2 manually.</span></span>
* <span data-ttu-id="7e433-270">**\*.LOG_ARCHIVE_DEST_2:** This is an optional step.</span><span class="sxs-lookup"><span data-stu-id="7e433-270">**\*.LOG_ARCHIVE_DEST_2:** This is an optional step.</span></span> <span data-ttu-id="7e433-271">You set this as it might be needed when the primary machine is in maintenance and the standby machine becomes a primary database.</span><span class="sxs-lookup"><span data-stu-id="7e433-271">You set this as it might be needed when the primary machine is in maintenance and the standby machine becomes a primary database.</span></span>

<span data-ttu-id="7e433-272">Then, you need to start the standby instance.</span><span class="sxs-lookup"><span data-stu-id="7e433-272">Then, you need to start the standby instance.</span></span> <span data-ttu-id="7e433-273">On the standby database server, enter the following command at a Windows command prompt to create an Oracle instance by creating a Windows service:</span><span class="sxs-lookup"><span data-stu-id="7e433-273">On the standby database server, enter the following command at a Windows command prompt to create an Oracle instance by creating a Windows service:</span></span>

    oradim -NEW -SID TEST\_STBY -STARTMODE MANUAL

<span data-ttu-id="7e433-274">The **Oradim** command creates an Oracle instance but does not start it.</span><span class="sxs-lookup"><span data-stu-id="7e433-274">The **Oradim** command creates an Oracle instance but does not start it.</span></span> <span data-ttu-id="7e433-275">You can find it in the C:\\OracleDatabase\\product\\11.2.0\\dbhome\_1\\BIN directory.</span><span class="sxs-lookup"><span data-stu-id="7e433-275">You can find it in the C:\\OracleDatabase\\product\\11.2.0\\dbhome\_1\\BIN directory.</span></span>

## <a name="configure-the-listener-and-tnsnames-to-support-the-database-on-primary-and-standby-machines"></a><span data-ttu-id="7e433-276">Configure the listener and tnsnames to support the database on primary and standby machines</span><span class="sxs-lookup"><span data-stu-id="7e433-276">Configure the listener and tnsnames to support the database on primary and standby machines</span></span>
<span data-ttu-id="7e433-277">Before you create a standby database, you need to make sure that the primary and standby databases in your configuration can talk to each other.</span><span class="sxs-lookup"><span data-stu-id="7e433-277">Before you create a standby database, you need to make sure that the primary and standby databases in your configuration can talk to each other.</span></span> <span data-ttu-id="7e433-278">To do this, you need to configure both the listener and TNSNames either manually or by using the network configuration utility NETCA.</span><span class="sxs-lookup"><span data-stu-id="7e433-278">To do this, you need to configure both the listener and TNSNames either manually or by using the network configuration utility NETCA.</span></span> <span data-ttu-id="7e433-279">This is a mandatory task when you use the Recovery Manager utility (RMAN).</span><span class="sxs-lookup"><span data-stu-id="7e433-279">This is a mandatory task when you use the Recovery Manager utility (RMAN).</span></span>

### <a name="configure-listenerora-on-both-servers-to-hold-entries-for-both-databases"></a><span data-ttu-id="7e433-280">Configure listener.ora on both servers to hold entries for both databases</span><span class="sxs-lookup"><span data-stu-id="7e433-280">Configure listener.ora on both servers to hold entries for both databases</span></span>
<span data-ttu-id="7e433-281">Remote desktop to Machine1 and edit the listener.ora file as specified below.</span><span class="sxs-lookup"><span data-stu-id="7e433-281">Remote desktop to Machine1 and edit the listener.ora file as specified below.</span></span> <span data-ttu-id="7e433-282">When you edit the listener.ora file, always make sure that the opening and closing parenthesis line up in the same column.</span><span class="sxs-lookup"><span data-stu-id="7e433-282">When you edit the listener.ora file, always make sure that the opening and closing parenthesis line up in the same column.</span></span> <span data-ttu-id="7e433-283">You can find the listener.ora file in the following folder: c:\\OracleDatabase\\product\\11.2.0\\dbhome\_1\\NETWORK\\ADMIN\\.</span><span class="sxs-lookup"><span data-stu-id="7e433-283">You can find the listener.ora file in the following folder: c:\\OracleDatabase\\product\\11.2.0\\dbhome\_1\\NETWORK\\ADMIN\\.</span></span>

    # listener.ora Network Configuration File: C:\OracleDatabase\product\11.2.0\dbhome_1\network\admin\listener.ora

    # Generated by Oracle configuration tools.

    SID_LIST_LISTENER =
      (SID_LIST =
        (SID_DESC =
          (SID_NAME = test)
          (ORACLE_HOME = C:\OracleDatabase\product\11.2.0\dbhome_1)
          (PROGRAM = extproc)
          (ENVS = "EXTPROC_DLLS=ONLY:C:\OracleDatabase\product\11.2.0\dbhome_1\bin\oraclr11.dll")
        )
      )

    LISTENER =
      (DESCRIPTION_LIST =
        (DESCRIPTION =
          (ADDRESS = (PROTOCOL = TCP)(HOST = MACHINE1)(PORT = 1521))
          (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
        )
      )

<span data-ttu-id="7e433-284">Next, remote desktop to Machine2 and edit the listener.ora file as follows:</span><span class="sxs-lookup"><span data-stu-id="7e433-284">Next, remote desktop to Machine2 and edit the listener.ora file as follows:</span></span>

    # listener.ora Network Configuration File: C:\OracleDatabase\product\11.2.0\dbhome_1\network\admin\listener.ora

    # Generated by Oracle configuration tools.

    SID_LIST_LISTENER =
      (SID_LIST =
        (SID_DESC =
          (SID_NAME = test_stby)
          (ORACLE_HOME = C:\OracleDatabase\product\11.2.0\dbhome_1)
          (PROGRAM = extproc)
          (ENVS = "EXTPROC_DLLS=ONLY:C:\OracleDatabase\product\11.2.0\dbhome_1\bin\oraclr11.dll")
        )
      )

    LISTENER =
      (DESCRIPTION_LIST =
        (DESCRIPTION =
          (ADDRESS = (PROTOCOL = TCP)(HOST = MACHINE2)(PORT = 1521))
          (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
        )
      )


### <a name="configure-tnsnamesora-on-the-primary-and-standby-virtual-machines-to-hold-entries-for-both-primary-and-standby-databases"></a><span data-ttu-id="7e433-285">Configure tnsnames.ora on the primary and standby Virtual Machines to hold entries for both primary and standby databases</span><span class="sxs-lookup"><span data-stu-id="7e433-285">Configure tnsnames.ora on the primary and standby Virtual Machines to hold entries for both primary and standby databases</span></span>
<span data-ttu-id="7e433-286">Remote desktop to Machine1 and edit the tnsnames.ora file as specified below.</span><span class="sxs-lookup"><span data-stu-id="7e433-286">Remote desktop to Machine1 and edit the tnsnames.ora file as specified below.</span></span> <span data-ttu-id="7e433-287">You can find the tnsnames.ora file in the following folder: c:\\OracleDatabase\\product\\11.2.0\\dbhome\_1\\NETWORK\\ADMIN\\.</span><span class="sxs-lookup"><span data-stu-id="7e433-287">You can find the tnsnames.ora file in the following folder: c:\\OracleDatabase\\product\\11.2.0\\dbhome\_1\\NETWORK\\ADMIN\\.</span></span>

    TEST =
      (DESCRIPTION =
        (ADDRESS_LIST =
          (ADDRESS = (PROTOCOL = TCP)(HOST = MACHINE1)(PORT = 1521))
        )
        (CONNECT_DATA =
          (SERVICE_NAME = test)
        )
      )

    TEST_STBY =
      (DESCRIPTION =
        (ADDRESS_LIST =
          (ADDRESS = (PROTOCOL = TCP)(HOST = MACHINE2)(PORT = 1521))
        )
        (CONNECT_DATA =
          (SERVICE_NAME = test_stby)
        )
      )

<span data-ttu-id="7e433-288">Remote desktop to Machine2 and edit the tnsnames.ora file as follows:</span><span class="sxs-lookup"><span data-stu-id="7e433-288">Remote desktop to Machine2 and edit the tnsnames.ora file as follows:</span></span>

    TEST =
      (DESCRIPTION =
        (ADDRESS_LIST =
          (ADDRESS = (PROTOCOL = TCP)(HOST = MACHINE1)(PORT = 1521))
        )
        (CONNECT_DATA =
          (SERVICE_NAME = test)
        )
      )

    TEST_STBY =
      (DESCRIPTION =
        (ADDRESS_LIST =
          (ADDRESS = (PROTOCOL = TCP)(HOST = MACHINE2)(PORT = 1521))
        )
        (CONNECT_DATA =
          (SERVICE_NAME = test_stby)
        )
      )


### <a name="start-the-listener-and-check-tnsping-on-both-virtual-machines-to-both-services"></a><span data-ttu-id="7e433-289">Start the listener and check tnsping on both Virtual Machines to both services.</span><span class="sxs-lookup"><span data-stu-id="7e433-289">Start the listener and check tnsping on both Virtual Machines to both services.</span></span>
<span data-ttu-id="7e433-290">Open up a new Windows command prompt in both primary and standby Virtual Machines and run the following statements:</span><span class="sxs-lookup"><span data-stu-id="7e433-290">Open up a new Windows command prompt in both primary and standby Virtual Machines and run the following statements:</span></span>

    C:\Users\DBAdmin>tnsping test

    TNS Ping Utility for 64-bit Windows: Version 11.2.0.1.0 - Production on 14-NOV-2013 06:29:08
    Copyright (c) 1997, 2010, Oracle.  All rights reserved.
    Used parameter files:
    C:\OracleDatabase\product\11.2.0\dbhome_1\network\admin\sqlnet.ora
    Used TNSNAMES adapter to resolve the alias
    Attempting to contact (DESCRIPTION = (ADDRESS_LIST = (ADDRESS = (PROTOCOL = TCP)(HOST = MACHINE1)(PORT = 1521))) (CONNECT_DATA = (SER
    VICE_NAME = test)))
    OK (0 msec)


    C:\Users\DBAdmin>tnsping test_stby

    TNS Ping Utility for 64-bit Windows: Version 11.2.0.1.0 - Production on 14-NOV-2013 06:29:16
    Copyright (c) 1997, 2010, Oracle.  All rights reserved.
    Used parameter files:
    C:\OracleDatabase\product\11.2.0\dbhome_1\network\admin\sqlnet.ora
    Used TNSNAMES adapter to resolve the alias
    Attempting to contact (DESCRIPTION = (ADDRESS_LIST = (ADDRESS = (PROTOCOL = TCP)(HOST = MACHINE2)(PORT = 1521))) (CONNECT_DATA = (SER
    VICE_NAME = test_stby)))
    OK (260 msec)


## <a name="start-up-the-standby-instance-in-nomount-state"></a><span data-ttu-id="7e433-291">Start up the standby instance in nomount state</span><span class="sxs-lookup"><span data-stu-id="7e433-291">Start up the standby instance in nomount state</span></span>
<span data-ttu-id="7e433-292">To set up the environment to support the standby database on the standby Virtual Machine (MACHINE2).</span><span class="sxs-lookup"><span data-stu-id="7e433-292">To set up the environment to support the standby database on the standby Virtual Machine (MACHINE2).</span></span>

<span data-ttu-id="7e433-293">First, copy the password file from the primary machine (Machine1) to the standby machine (Machine2) manually.</span><span class="sxs-lookup"><span data-stu-id="7e433-293">First, copy the password file from the primary machine (Machine1) to the standby machine (Machine2) manually.</span></span> <span data-ttu-id="7e433-294">This is necessary as the **sys** password must be identical on both machines.</span><span class="sxs-lookup"><span data-stu-id="7e433-294">This is necessary as the **sys** password must be identical on both machines.</span></span>

<span data-ttu-id="7e433-295">Then, open the Windows command prompt in Machine2, and setup the environment variables to point to the Standby database as follows:</span><span class="sxs-lookup"><span data-stu-id="7e433-295">Then, open the Windows command prompt in Machine2, and setup the environment variables to point to the Standby database as follows:</span></span>

    SET ORACLE_HOME=C:\OracleDatabase\product\11.2.0\dbhome_1
    SET ORACLE_SID=TEST_STBY

<span data-ttu-id="7e433-296">Next, start the Standby database in nomount state and then generate an spfile.</span><span class="sxs-lookup"><span data-stu-id="7e433-296">Next, start the Standby database in nomount state and then generate an spfile.</span></span>

<span data-ttu-id="7e433-297">Start the database:</span><span class="sxs-lookup"><span data-stu-id="7e433-297">Start the database:</span></span>

    SQL>shutdown immediate;

    SQL>startup nomount
    ORACLE instance started.

    Total System Global Area  747417600 bytes
    Fixed Size                  2179496 bytes
    Variable Size             473960024 bytes
    Database Buffers          264241152 bytes
    Redo Buffers                7036928 bytes


## <a name="use-rman-to-clone-the-database-and-to-create-a-standby-database"></a><span data-ttu-id="7e433-298">Use RMAN to clone the database and to create a standby database</span><span class="sxs-lookup"><span data-stu-id="7e433-298">Use RMAN to clone the database and to create a standby database</span></span>
<span data-ttu-id="7e433-299">You can use the Recovery Manager utility (RMAN) to take any backup copy of the primary database to create the physical standby database.</span><span class="sxs-lookup"><span data-stu-id="7e433-299">You can use the Recovery Manager utility (RMAN) to take any backup copy of the primary database to create the physical standby database.</span></span>

<span data-ttu-id="7e433-300">Remote desktop to the standby Virtual Machine (MACHINE2) and run the RMAN utility by specifying a full connection string for both the TARGET (primary database, Machine1) and AUXILLARY (standby database, Machine2) instances.</span><span class="sxs-lookup"><span data-stu-id="7e433-300">Remote desktop to the standby Virtual Machine (MACHINE2) and run the RMAN utility by specifying a full connection string for both the TARGET (primary database, Machine1) and AUXILLARY (standby database, Machine2) instances.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7e433-301">Do not use the operating system authentication as there is no database in the standby server machine yet.</span><span class="sxs-lookup"><span data-stu-id="7e433-301">Do not use the operating system authentication as there is no database in the standby server machine yet.</span></span>
> 
> 

    C:\> RMAN TARGET sys/password@test AUXILIARY sys/password@test_STBY

    RMAN>DUPLICATE TARGET DATABASE
      FOR STANDBY
      FROM ACTIVE DATABASE
      DORECOVER
        NOFILENAMECHECK;

## <a name="start-the-physical-standby-database-in-managed-recovery-mode"></a><span data-ttu-id="7e433-302">Start the physical standby database in managed recovery mode</span><span class="sxs-lookup"><span data-stu-id="7e433-302">Start the physical standby database in managed recovery mode</span></span>
<span data-ttu-id="7e433-303">This tutorial demonstrates how to create a physical standby database.</span><span class="sxs-lookup"><span data-stu-id="7e433-303">This tutorial demonstrates how to create a physical standby database.</span></span> <span data-ttu-id="7e433-304">For information on creating a logical standby database, see the Oracle documentation.</span><span class="sxs-lookup"><span data-stu-id="7e433-304">For information on creating a logical standby database, see the Oracle documentation.</span></span>

<span data-ttu-id="7e433-305">Open up SQL\*Plus command prompt and enable the Data Guard on the standby Virtual Machine or server (MACHINE2) as follows:</span><span class="sxs-lookup"><span data-stu-id="7e433-305">Open up SQL\*Plus command prompt and enable the Data Guard on the standby Virtual Machine or server (MACHINE2) as follows:</span></span>

    SHUTDOWN IMMEDIATE;
    STARTUP MOUNT;
    ALTER DATABASE RECOVER MANAGED STANDBY DATABASE DISCONNECT FROM SESSION;

<span data-ttu-id="7e433-306">When you open the standby database in **MOUNT** mode, the archive log shipping continues and the managed recovery process continues log applying on the standby database.</span><span class="sxs-lookup"><span data-stu-id="7e433-306">When you open the standby database in **MOUNT** mode, the archive log shipping continues and the managed recovery process continues log applying on the standby database.</span></span> <span data-ttu-id="7e433-307">This ensures that the standby database remains up-to-date with the primary database.</span><span class="sxs-lookup"><span data-stu-id="7e433-307">This ensures that the standby database remains up-to-date with the primary database.</span></span> <span data-ttu-id="7e433-308">Note that the standby database cannot be accessible for reporting purposes during this time.</span><span class="sxs-lookup"><span data-stu-id="7e433-308">Note that the standby database cannot be accessible for reporting purposes during this time.</span></span>

<span data-ttu-id="7e433-309">When you open the standby database in **READ ONLY** mode, the archive log shipping continues.</span><span class="sxs-lookup"><span data-stu-id="7e433-309">When you open the standby database in **READ ONLY** mode, the archive log shipping continues.</span></span> <span data-ttu-id="7e433-310">But the managed recovery process stops.</span><span class="sxs-lookup"><span data-stu-id="7e433-310">But the managed recovery process stops.</span></span> <span data-ttu-id="7e433-311">This causes the standby database to become increasingly out of date until the managed recovery process is resumed.</span><span class="sxs-lookup"><span data-stu-id="7e433-311">This causes the standby database to become increasingly out of date until the managed recovery process is resumed.</span></span> <span data-ttu-id="7e433-312">You can access the standby database for reporting purposes during this time but data may not reflect the latest changes.</span><span class="sxs-lookup"><span data-stu-id="7e433-312">You can access the standby database for reporting purposes during this time but data may not reflect the latest changes.</span></span>

<span data-ttu-id="7e433-313">In general, we recommend that you keep the standby database in **MOUNT** mode to keep the data in the standby database up-to-date if there is a failure of the primary database.</span><span class="sxs-lookup"><span data-stu-id="7e433-313">In general, we recommend that you keep the standby database in **MOUNT** mode to keep the data in the standby database up-to-date if there is a failure of the primary database.</span></span> <span data-ttu-id="7e433-314">However, you can keep the standby database in **READ ONLY** mode for reporting purposes depending on your application’s requirements.</span><span class="sxs-lookup"><span data-stu-id="7e433-314">However, you can keep the standby database in **READ ONLY** mode for reporting purposes depending on your application’s requirements.</span></span> <span data-ttu-id="7e433-315">The following steps demonstrate how to enable the Data Guard in read-only mode using SQL\*Plus:</span><span class="sxs-lookup"><span data-stu-id="7e433-315">The following steps demonstrate how to enable the Data Guard in read-only mode using SQL\*Plus:</span></span>

    SHUTDOWN IMMEDIATE;
    STARTUP MOUNT;
    ALTER DATABASE OPEN READ ONLY;


## <a name="verify-the-physical-standby-database"></a><span data-ttu-id="7e433-316">Verify the physical standby database</span><span class="sxs-lookup"><span data-stu-id="7e433-316">Verify the physical standby database</span></span>
<span data-ttu-id="7e433-317">This section demonstrates how to verify the high availability configuration as an administrator.</span><span class="sxs-lookup"><span data-stu-id="7e433-317">This section demonstrates how to verify the high availability configuration as an administrator.</span></span>

<span data-ttu-id="7e433-318">Open up SQL\*Plus command prompt window and check archived redo log on the Standby Virtual Machine (Machine2):</span><span class="sxs-lookup"><span data-stu-id="7e433-318">Open up SQL\*Plus command prompt window and check archived redo log on the Standby Virtual Machine (Machine2):</span></span>

    SQL> show parameters db_unique_name;

    NAME                                TYPE       VALUE
    ------------------------------------ ----------- ------------------------------
    db_unique_name                      string     TEST_STBY

    SQL> SELECT NAME FROM V$DATABASE

    SQL> SELECT SEQUENCE#, FIRST_TIME, NEXT_TIME, APPLIED FROM V$ARCHIVED_LOG ORDER BY SEQUENCE#;

    SEQUENCE# FIRST_TIM NEXT_TIM APPLIED
    ----------------  ---------------  --------------- ------------
    45                    23-FEB-14   23-FEB-14   YES
    45                    23-FEB-14   23-FEB-14   NO
    46                    23-FEB-14   23-FEB-14   NO
    46                    23-FEB-14   23-FEB-14   YES
    47                    23-FEB-14   23-FEB-14   NO
    47                    23-FEB-14   23-FEB-14   NO

<span data-ttu-id="7e433-319">Open up SQL\*Plus command prompt window and switch logfiles on the Primary machine (Machine1):</span><span class="sxs-lookup"><span data-stu-id="7e433-319">Open up SQL\*Plus command prompt window and switch logfiles on the Primary machine (Machine1):</span></span>

    SQL> alter system switch logfile;
    System altered.

    SQL> archive log list
    Database log mode              Archive Mode
    Automatic archival             Enabled
    Archive destination            C:\OracleDatabase\archive
    Oldest online log sequence     69
    Next log sequence to archive   71
    Current log sequence           71

<span data-ttu-id="7e433-320">Check archived redo log on the Standby Virtual Machine (Machine2):</span><span class="sxs-lookup"><span data-stu-id="7e433-320">Check archived redo log on the Standby Virtual Machine (Machine2):</span></span>

    SQL> SELECT SEQUENCE#, FIRST_TIME, NEXT_TIME, APPLIED FROM V$ARCHIVED_LOG ORDER BY SEQUENCE#;

    SEQUENCE# FIRST_TIM NEXT_TIM APPLIED
    ----------------  ---------------  --------------- ------------
    45                    23-FEB-14   23-FEB-14   YES
    46                    23-FEB-14   23-FEB-14   YES
    47                    23-FEB-14   23-FEB-14   YES
    48                    23-FEB-14   23-FEB-14   YES

    49                    23-FEB-14   23-FEB-14   YES
    50                    23-FEB-14   23-FEB-14   IN-MEMORY

<span data-ttu-id="7e433-321">Check for any gap on the Standby Virtual Machine (Machine2):</span><span class="sxs-lookup"><span data-stu-id="7e433-321">Check for any gap on the Standby Virtual Machine (Machine2):</span></span>

    SQL> SELECT * FROM V$ARCHIVE_GAP;
    no rows selected.

<span data-ttu-id="7e433-322">Another verification method could be to failover to the standby database and then test if it is possible to failback to the primary database.</span><span class="sxs-lookup"><span data-stu-id="7e433-322">Another verification method could be to failover to the standby database and then test if it is possible to failback to the primary database.</span></span> <span data-ttu-id="7e433-323">To activate the standby database as a primary database, use the following statements:</span><span class="sxs-lookup"><span data-stu-id="7e433-323">To activate the standby database as a primary database, use the following statements:</span></span>

    SQL> ALTER DATABASE RECOVER MANAGED STANDBY DATABASE FINISH;
    SQL> ALTER DATABASE ACTIVATE STANDBY DATABASE;

<span data-ttu-id="7e433-324">If you have not enabled flashback on the original primary database, it’s recommended that you drop the original primary database and recreate as a standby database.</span><span class="sxs-lookup"><span data-stu-id="7e433-324">If you have not enabled flashback on the original primary database, it’s recommended that you drop the original primary database and recreate as a standby database.</span></span>

<span data-ttu-id="7e433-325">We recommend that you enable flashback database on the primary and the standby databases.</span><span class="sxs-lookup"><span data-stu-id="7e433-325">We recommend that you enable flashback database on the primary and the standby databases.</span></span> <span data-ttu-id="7e433-326">When a failover happens, the primary database can be flashed back to the time before the failover and quickly converted to a standby database.</span><span class="sxs-lookup"><span data-stu-id="7e433-326">When a failover happens, the primary database can be flashed back to the time before the failover and quickly converted to a standby database.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7e433-327">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="7e433-327">Additional Resources</span></span>
[<span data-ttu-id="7e433-328">Oracle Virtual Machine images for Azure</span><span class="sxs-lookup"><span data-stu-id="7e433-328">Oracle Virtual Machine images for Azure</span></span>](oracle-images.md)

