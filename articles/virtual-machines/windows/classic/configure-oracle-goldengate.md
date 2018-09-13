---
title: Configuring Oracle GoldenGate in VMs | Microsoft Docs
description: Step through a tutorial for setting up and implementing Oracle GoldenGate on Azure Windows Server VMs for high availability and disaster recovery.
services: virtual-machines-windows
author: rickstercdn
manager: timlt
documentationcenter: ''
tags: azure-service-management
ms.assetid: 85ca238c-5925-4c5a-86c7-08338587b8c3
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 09/06/2016
ms.author: rclaus
ms.openlocfilehash: 8b6a5e98cdc8da49e6387287a5a8d55b368a25c6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551855"
---
# <a name="configuring-oracle-goldengate-for-azure"></a><span data-ttu-id="88f19-103">Configuring Oracle GoldenGate for Azure</span><span class="sxs-lookup"><span data-stu-id="88f19-103">Configuring Oracle GoldenGate for Azure</span></span>
<span data-ttu-id="88f19-104">This tutorial demonstrates how to setup Oracle GoldenGate for Azure Virtual Machines environment for high availability and disaster recovery.</span><span class="sxs-lookup"><span data-stu-id="88f19-104">This tutorial demonstrates how to setup Oracle GoldenGate for Azure Virtual Machines environment for high availability and disaster recovery.</span></span> <span data-ttu-id="88f19-105">The tutorial focuses on [bi-directional replication](http://docs.oracle.com/goldengate/1212/gg-winux/GWUAD/wu_about_gg.htm) for non-RAC Oracle databases and requires that both sites are active.</span><span class="sxs-lookup"><span data-stu-id="88f19-105">The tutorial focuses on [bi-directional replication](http://docs.oracle.com/goldengate/1212/gg-winux/GWUAD/wu_about_gg.htm) for non-RAC Oracle databases and requires that both sites are active.</span></span>

<span data-ttu-id="88f19-106">Oracle GoldenGate supports data distribution and data integration.</span><span class="sxs-lookup"><span data-stu-id="88f19-106">Oracle GoldenGate supports data distribution and data integration.</span></span> <span data-ttu-id="88f19-107">It enables you to set up a data distribution and data synchronization solution through the Oracle-Oracle replication configuration, and provides a flexible high availability solution.</span><span class="sxs-lookup"><span data-stu-id="88f19-107">It enables you to set up a data distribution and data synchronization solution through the Oracle-Oracle replication configuration, and provides a flexible high availability solution.</span></span> <span data-ttu-id="88f19-108">Oracle GoldenGate supplements Oracle Data Guard with its replication capabilities to enable enterprise-wide information distribution and zero-downtime upgrades and migrations.</span><span class="sxs-lookup"><span data-stu-id="88f19-108">Oracle GoldenGate supplements Oracle Data Guard with its replication capabilities to enable enterprise-wide information distribution and zero-downtime upgrades and migrations.</span></span> <span data-ttu-id="88f19-109">For detailed information, see [Using Oracle GoldenGate with Oracle Data Guard](http://docs.oracle.com/cd/E11882_01/server.112/e17157/unplanned.htm).</span><span class="sxs-lookup"><span data-stu-id="88f19-109">For detailed information, see [Using Oracle GoldenGate with Oracle Data Guard](http://docs.oracle.com/cd/E11882_01/server.112/e17157/unplanned.htm).</span></span>

<span data-ttu-id="88f19-110">Oracle GoldenGate contains the following main components: Extract, Data pump, Replicat, Trails or extract files, Checkpoints, Manager and Collector.</span><span class="sxs-lookup"><span data-stu-id="88f19-110">Oracle GoldenGate contains the following main components: Extract, Data pump, Replicat, Trails or extract files, Checkpoints, Manager and Collector.</span></span> <span data-ttu-id="88f19-111">To have bi-directional replication between two sites, you need to create and start all components on both sites.</span><span class="sxs-lookup"><span data-stu-id="88f19-111">To have bi-directional replication between two sites, you need to create and start all components on both sites.</span></span> <span data-ttu-id="88f19-112">For detailed information on Oracle GoldenGate architecture, see [Oracle GoldenGate Guide](http://docs.oracle.com/goldengate/1212/gg-winux/index.html).</span><span class="sxs-lookup"><span data-stu-id="88f19-112">For detailed information on Oracle GoldenGate architecture, see [Oracle GoldenGate Guide](http://docs.oracle.com/goldengate/1212/gg-winux/index.html).</span></span>

<span data-ttu-id="88f19-113">This tutorial assumes that you already have theoretical and practical knowledge on Oracle Database High Availability and Disaster Recovery concepts as well as [Oracle GoldenGate](http://docs.oracle.com/goldengate/1212/gg-winux/index.html).</span><span class="sxs-lookup"><span data-stu-id="88f19-113">This tutorial assumes that you already have theoretical and practical knowledge on Oracle Database High Availability and Disaster Recovery concepts as well as [Oracle GoldenGate](http://docs.oracle.com/goldengate/1212/gg-winux/index.html).</span></span> <span data-ttu-id="88f19-114">For more information, see the [Oracle web site](http://www.oracle.com/technetwork/database/features/availability/index.html).</span><span class="sxs-lookup"><span data-stu-id="88f19-114">For more information, see the [Oracle web site](http://www.oracle.com/technetwork/database/features/availability/index.html).</span></span>

<span data-ttu-id="88f19-115">In addition, the tutorial assumes that you have already implemented the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="88f19-115">In addition, the tutorial assumes that you have already implemented the following prerequisites:</span></span>

* <span data-ttu-id="88f19-116">You’ve already reviewed the High Availability and Disaster Recovery Considerations section in the [Oracle Virtual Machine images - Miscellaneous Considerations](oracle-considerations.md) topic.</span><span class="sxs-lookup"><span data-stu-id="88f19-116">You’ve already reviewed the High Availability and Disaster Recovery Considerations section in the [Oracle Virtual Machine images - Miscellaneous Considerations](oracle-considerations.md) topic.</span></span> <span data-ttu-id="88f19-117">Note that Azure supports standalone Oracle Database instances but not Oracle Real Application Clusters (Oracle RAC) currently.</span><span class="sxs-lookup"><span data-stu-id="88f19-117">Note that Azure supports standalone Oracle Database instances but not Oracle Real Application Clusters (Oracle RAC) currently.</span></span>
* <span data-ttu-id="88f19-118">You’ve downloaded the Oracle GoldenGate software from the [Oracle Downloads](http://www.oracle.com/us/downloads/index.html) web site.</span><span class="sxs-lookup"><span data-stu-id="88f19-118">You’ve downloaded the Oracle GoldenGate software from the [Oracle Downloads](http://www.oracle.com/us/downloads/index.html) web site.</span></span> <span data-ttu-id="88f19-119">You’ve selected the Product Pack Oracle Fusion Middleware – Data Integration.</span><span class="sxs-lookup"><span data-stu-id="88f19-119">You’ve selected the Product Pack Oracle Fusion Middleware – Data Integration.</span></span> <span data-ttu-id="88f19-120">Then, you’ve selected Oracle GoldenGate on Oracle v11.2.1 Media Pack for Microsoft Windows x64 (64-bit) for an Oracle 11g database.</span><span class="sxs-lookup"><span data-stu-id="88f19-120">Then, you’ve selected Oracle GoldenGate on Oracle v11.2.1 Media Pack for Microsoft Windows x64 (64-bit) for an Oracle 11g database.</span></span> <span data-ttu-id="88f19-121">Next, download Oracle GoldenGate V11.2.1.0.3 for Oracle 11g 64bit on Windows 2008 (64bit).</span><span class="sxs-lookup"><span data-stu-id="88f19-121">Next, download Oracle GoldenGate V11.2.1.0.3 for Oracle 11g 64bit on Windows 2008 (64bit).</span></span>
* <span data-ttu-id="88f19-122">You have created two Virtual Machines (VMs) in Azure using Oracle Enterprise Edition on Windows Server.</span><span class="sxs-lookup"><span data-stu-id="88f19-122">You have created two Virtual Machines (VMs) in Azure using Oracle Enterprise Edition on Windows Server.</span></span> <span data-ttu-id="88f19-123">Make sure that the Virtual Machines are in the [same cloud service](../../virtual-machines-linux-load-balance.md) and in the same [Virtual Network](https://azure.microsoft.com/documentation/services/virtual-network/) to ensure they can access each other over the persistent private IP address.</span><span class="sxs-lookup"><span data-stu-id="88f19-123">Make sure that the Virtual Machines are in the [same cloud service](../../virtual-machines-linux-load-balance.md) and in the same [Virtual Network](https://azure.microsoft.com/documentation/services/virtual-network/) to ensure they can access each other over the persistent private IP address.</span></span>
* <span data-ttu-id="88f19-124">You’ve set the Virtual Machine names as “MachineGG1” for Site A and “MachineGG2” for Site B at the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="88f19-124">You’ve set the Virtual Machine names as “MachineGG1” for Site A and “MachineGG2” for Site B at the Azure classic portal.</span></span>
* <span data-ttu-id="88f19-125">You’ve created test databases “TestGG1” on Site A and “TestGG2” on Site B.</span><span class="sxs-lookup"><span data-stu-id="88f19-125">You’ve created test databases “TestGG1” on Site A and “TestGG2” on Site B.</span></span>
* <span data-ttu-id="88f19-126">You log on to your Windows server as a member of the Administrators group or a member of the **ORA_DBA** group.</span><span class="sxs-lookup"><span data-stu-id="88f19-126">You log on to your Windows server as a member of the Administrators group or a member of the **ORA_DBA** group.</span></span>

<span data-ttu-id="88f19-127">In this tutorial, you will:</span><span class="sxs-lookup"><span data-stu-id="88f19-127">In this tutorial, you will:</span></span>

1. <span data-ttu-id="88f19-128">Setup database on Site A and Site B</span><span class="sxs-lookup"><span data-stu-id="88f19-128">Setup database on Site A and Site B</span></span>  
   
   1. <span data-ttu-id="88f19-129">Perform initial data load</span><span class="sxs-lookup"><span data-stu-id="88f19-129">Perform initial data load</span></span>
2. <span data-ttu-id="88f19-130">Prepare Site A and Site B for database replication</span><span class="sxs-lookup"><span data-stu-id="88f19-130">Prepare Site A and Site B for database replication</span></span>
3. <span data-ttu-id="88f19-131">Create all necessary objects to support DDL Replication</span><span class="sxs-lookup"><span data-stu-id="88f19-131">Create all necessary objects to support DDL Replication</span></span>
4. <span data-ttu-id="88f19-132">Configure GoldenGate Manager on Site A and Site B</span><span class="sxs-lookup"><span data-stu-id="88f19-132">Configure GoldenGate Manager on Site A and Site B</span></span>
5. <span data-ttu-id="88f19-133">Create Extract Group and Data Pump processes on Site A and Site B</span><span class="sxs-lookup"><span data-stu-id="88f19-133">Create Extract Group and Data Pump processes on Site A and Site B</span></span>
   
   1. <span data-ttu-id="88f19-134">Create Extract and Data Pump processes on Site A</span><span class="sxs-lookup"><span data-stu-id="88f19-134">Create Extract and Data Pump processes on Site A</span></span>
   2. <span data-ttu-id="88f19-135">Create a GoldenGate checkpoint table on Site B</span><span class="sxs-lookup"><span data-stu-id="88f19-135">Create a GoldenGate checkpoint table on Site B</span></span>
   3. <span data-ttu-id="88f19-136">Add REPLICAT on Site B</span><span class="sxs-lookup"><span data-stu-id="88f19-136">Add REPLICAT on Site B</span></span>
   4. <span data-ttu-id="88f19-137">Create Extract and Data Pump processes on Site B</span><span class="sxs-lookup"><span data-stu-id="88f19-137">Create Extract and Data Pump processes on Site B</span></span>
   5. <span data-ttu-id="88f19-138">Create a GoldenGate checkpoint table on Site A</span><span class="sxs-lookup"><span data-stu-id="88f19-138">Create a GoldenGate checkpoint table on Site A</span></span>
   6. <span data-ttu-id="88f19-139">Add REPLICAT on Site A</span><span class="sxs-lookup"><span data-stu-id="88f19-139">Add REPLICAT on Site A</span></span>
   7. <span data-ttu-id="88f19-140">Add trandata on Site A and Site B</span><span class="sxs-lookup"><span data-stu-id="88f19-140">Add trandata on Site A and Site B</span></span>
   8. <span data-ttu-id="88f19-141">Start Extract and Data Pump processes on Site A</span><span class="sxs-lookup"><span data-stu-id="88f19-141">Start Extract and Data Pump processes on Site A</span></span>
   9. <span data-ttu-id="88f19-142">Start Extract and Data Pump processes on Site B</span><span class="sxs-lookup"><span data-stu-id="88f19-142">Start Extract and Data Pump processes on Site B</span></span>
   10. <span data-ttu-id="88f19-143">Start REPLICAT process on Site A</span><span class="sxs-lookup"><span data-stu-id="88f19-143">Start REPLICAT process on Site A</span></span>
   11. <span data-ttu-id="88f19-144">Start REPLICAT process on Site B</span><span class="sxs-lookup"><span data-stu-id="88f19-144">Start REPLICAT process on Site B</span></span>
6. <span data-ttu-id="88f19-145">Verify the bi-directional replication process</span><span class="sxs-lookup"><span data-stu-id="88f19-145">Verify the bi-directional replication process</span></span>

> [!IMPORTANT]
> <span data-ttu-id="88f19-146">This tutorial has been setup and tested against the following software configuration:</span><span class="sxs-lookup"><span data-stu-id="88f19-146">This tutorial has been setup and tested against the following software configuration:</span></span>
> 
> |  | <span data-ttu-id="88f19-147">**Site A Database**</span><span class="sxs-lookup"><span data-stu-id="88f19-147">**Site A Database**</span></span> | <span data-ttu-id="88f19-148">**Site B Database**</span><span class="sxs-lookup"><span data-stu-id="88f19-148">**Site B Database**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="88f19-149">**Oracle Release**</span><span class="sxs-lookup"><span data-stu-id="88f19-149">**Oracle Release**</span></span> |<span data-ttu-id="88f19-150">Oracle11g Release 2 – (11.2.0.1)</span><span class="sxs-lookup"><span data-stu-id="88f19-150">Oracle11g Release 2 – (11.2.0.1)</span></span> |<span data-ttu-id="88f19-151">Oracle11g Release 2 – (11.2.0.1)</span><span class="sxs-lookup"><span data-stu-id="88f19-151">Oracle11g Release 2 – (11.2.0.1)</span></span> |
> | <span data-ttu-id="88f19-152">**Machine Name**</span><span class="sxs-lookup"><span data-stu-id="88f19-152">**Machine Name**</span></span> |<span data-ttu-id="88f19-153">MachineGG1</span><span class="sxs-lookup"><span data-stu-id="88f19-153">MachineGG1</span></span> |<span data-ttu-id="88f19-154">MachineGG2</span><span class="sxs-lookup"><span data-stu-id="88f19-154">MachineGG2</span></span> |
> | <span data-ttu-id="88f19-155">**Operating System**</span><span class="sxs-lookup"><span data-stu-id="88f19-155">**Operating System**</span></span> |<span data-ttu-id="88f19-156">Windows 2008 R2</span><span class="sxs-lookup"><span data-stu-id="88f19-156">Windows 2008 R2</span></span> |<span data-ttu-id="88f19-157">Windows 2008 R2</span><span class="sxs-lookup"><span data-stu-id="88f19-157">Windows 2008 R2</span></span> |
> | <span data-ttu-id="88f19-158">**Oracle SID**</span><span class="sxs-lookup"><span data-stu-id="88f19-158">**Oracle SID**</span></span> |<span data-ttu-id="88f19-159">TESTGG1</span><span class="sxs-lookup"><span data-stu-id="88f19-159">TESTGG1</span></span> |<span data-ttu-id="88f19-160">TESTGG2</span><span class="sxs-lookup"><span data-stu-id="88f19-160">TESTGG2</span></span> |
> | <span data-ttu-id="88f19-161">**Replication Schema**</span><span class="sxs-lookup"><span data-stu-id="88f19-161">**Replication Schema**</span></span> |<span data-ttu-id="88f19-162">SCOTT</span><span class="sxs-lookup"><span data-stu-id="88f19-162">SCOTT</span></span> |<span data-ttu-id="88f19-163">SCOTT</span><span class="sxs-lookup"><span data-stu-id="88f19-163">SCOTT</span></span> |
> 
> 

<span data-ttu-id="88f19-164">For subsequent releases of Oracle Database and Oracle GoldenGate, there might be some additional changes that you need to implement.</span><span class="sxs-lookup"><span data-stu-id="88f19-164">For subsequent releases of Oracle Database and Oracle GoldenGate, there might be some additional changes that you need to implement.</span></span> <span data-ttu-id="88f19-165">For the most up-to-date version specific information, see [Oracle GoldenGate](http://docs.oracle.com/goldengate/1212/gg-winux/index.html) and [Oracle Database](http://www.oracle.com/us/corporate/features/database-12c/index.html) documentation at Oracle web site.</span><span class="sxs-lookup"><span data-stu-id="88f19-165">For the most up-to-date version specific information, see [Oracle GoldenGate](http://docs.oracle.com/goldengate/1212/gg-winux/index.html) and [Oracle Database](http://www.oracle.com/us/corporate/features/database-12c/index.html) documentation at Oracle web site.</span></span> <span data-ttu-id="88f19-166">For example, for a release 11.2.0.4 source database and later, the capture of DDL is performed by the logmining server asynchronously and requires no special triggers, tables, or other database objects to be installed.</span><span class="sxs-lookup"><span data-stu-id="88f19-166">For example, for a release 11.2.0.4 source database and later, the capture of DDL is performed by the logmining server asynchronously and requires no special triggers, tables, or other database objects to be installed.</span></span> <span data-ttu-id="88f19-167">Oracle GoldenGate upgrades can be performed without stopping user applications.</span><span class="sxs-lookup"><span data-stu-id="88f19-167">Oracle GoldenGate upgrades can be performed without stopping user applications.</span></span> <span data-ttu-id="88f19-168">The use of a DDL trigger and supporting objects is required when Extract is in integrated mode with an Oracle 11g source database that is earlier than version 11.2.0.4.</span><span class="sxs-lookup"><span data-stu-id="88f19-168">The use of a DDL trigger and supporting objects is required when Extract is in integrated mode with an Oracle 11g source database that is earlier than version 11.2.0.4.</span></span> <span data-ttu-id="88f19-169">For detailed guidance, see [Installing and Configuring Oracle GoldenGate for Oracle Database](http://docs.oracle.com/goldengate/1212/gg-winux/GIORA.pdf).</span><span class="sxs-lookup"><span data-stu-id="88f19-169">For detailed guidance, see [Installing and Configuring Oracle GoldenGate for Oracle Database](http://docs.oracle.com/goldengate/1212/gg-winux/GIORA.pdf).</span></span>

## <a name="1-setup-database-on-site-a-and-site-b"></a><span data-ttu-id="88f19-170">1. Setup database on Site A and Site B</span><span class="sxs-lookup"><span data-stu-id="88f19-170">1. Setup database on Site A and Site B</span></span>
<span data-ttu-id="88f19-171">This section explains how to perform the database prerequisites on both Site A and Site B. You must perform all the steps of this section on both sites: Site A and Site B.</span><span class="sxs-lookup"><span data-stu-id="88f19-171">This section explains how to perform the database prerequisites on both Site A and Site B. You must perform all the steps of this section on both sites: Site A and Site B.</span></span>

<span data-ttu-id="88f19-172">First, remote desktop to Site A and Site B via the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="88f19-172">First, remote desktop to Site A and Site B via the Azure classic portal.</span></span> <span data-ttu-id="88f19-173">Open up a Windows command prompt and create a home directory for Oracle GoldenGate setup files:</span><span class="sxs-lookup"><span data-stu-id="88f19-173">Open up a Windows command prompt and create a home directory for Oracle GoldenGate setup files:</span></span>

    mkdir C:\OracleGG

<span data-ttu-id="88f19-174">Then, unzip and install the Oracle GoldenGate software in this folder.</span><span class="sxs-lookup"><span data-stu-id="88f19-174">Then, unzip and install the Oracle GoldenGate software in this folder.</span></span> <span data-ttu-id="88f19-175">After this step, you can initiate the GoldenGate Software Command Interpreter (GGSCI) by executing the following command:</span><span class="sxs-lookup"><span data-stu-id="88f19-175">After this step, you can initiate the GoldenGate Software Command Interpreter (GGSCI) by executing the following command:</span></span>

    C:\OracleGG\.\ggsci

<span data-ttu-id="88f19-176">You can use [GGSCI](http://docs.oracle.com/goldengate/1212/gg-winux/GWUAD/wu_gettingstarted.htm) to run several commands that configure, control, and monitor Oracle GoldenGate.</span><span class="sxs-lookup"><span data-stu-id="88f19-176">You can use [GGSCI](http://docs.oracle.com/goldengate/1212/gg-winux/GWUAD/wu_gettingstarted.htm) to run several commands that configure, control, and monitor Oracle GoldenGate.</span></span>

<span data-ttu-id="88f19-177">Next, run the following command to create all sub-folders from the installation package:</span><span class="sxs-lookup"><span data-stu-id="88f19-177">Next, run the following command to create all sub-folders from the installation package:</span></span>

    GGSCI (Hostname) 1> CREATE SUBDIRS

<span data-ttu-id="88f19-178">Run the following command to exit the GGSCI command prompt:</span><span class="sxs-lookup"><span data-stu-id="88f19-178">Run the following command to exit the GGSCI command prompt:</span></span>

    GGSCI (Hostname) 1> EXIT

<span data-ttu-id="88f19-179">Then, you need to create a database user, which will be used by the Oracle GoldenGate Manager, Extract and Replication processes.</span><span class="sxs-lookup"><span data-stu-id="88f19-179">Then, you need to create a database user, which will be used by the Oracle GoldenGate Manager, Extract and Replication processes.</span></span> <span data-ttu-id="88f19-180">Note that you can create individual users for each process or configure only one common user.</span><span class="sxs-lookup"><span data-stu-id="88f19-180">Note that you can create individual users for each process or configure only one common user.</span></span> <span data-ttu-id="88f19-181">In this tutorial, we create one user, which is called as ggate.</span><span class="sxs-lookup"><span data-stu-id="88f19-181">In this tutorial, we create one user, which is called as ggate.</span></span> <span data-ttu-id="88f19-182">Then, we grant that user the necessary privileges.</span><span class="sxs-lookup"><span data-stu-id="88f19-182">Then, we grant that user the necessary privileges.</span></span> <span data-ttu-id="88f19-183">Note that you must perform the following operations on Site A and Site B.</span><span class="sxs-lookup"><span data-stu-id="88f19-183">Note that you must perform the following operations on Site A and Site B.</span></span>

<span data-ttu-id="88f19-184">Open up SQL\*Plus command window on Site A and Site B with database administrator privileges using **SYSDBA**, such as:</span><span class="sxs-lookup"><span data-stu-id="88f19-184">Open up SQL\*Plus command window on Site A and Site B with database administrator privileges using **SYSDBA**, such as:</span></span>

    Enter username: / as sysdba

<span data-ttu-id="88f19-185">And run:</span><span class="sxs-lookup"><span data-stu-id="88f19-185">And run:</span></span>

    SQL> create tablespace ggs_data   datafile 'c:\OracleDatabase\oradata\<DBNAME>\<DBNAME>ggs_data01.dbf' size 200m;
    SQL> create user ggate identified by ggate default tablespace ggs_data  temporary tablespace temp;
          grant connect, resource to ggate;
          grant select any dictionary, select any table to ggate;
          grant create table to ggate;
          grant flashback any table to ggate;
          grant execute on dbms_flashback to ggate;
          grant execute on utl_file to ggate;
          grant create any table to ggate;
          grant insert any table to ggate;
          grant update any table to ggate;
          grant delete any table to ggate;
          grant drop any table to ggate;

<span data-ttu-id="88f19-186">Next, locate the INIT\<DatabaseSID\>.ORA file in the %ORACLE\_HOME%\\database folder on Site A and Site B and append the following database parameters to INITTEST.ora:</span><span class="sxs-lookup"><span data-stu-id="88f19-186">Next, locate the INIT\<DatabaseSID\>.ORA file in the %ORACLE\_HOME%\\database folder on Site A and Site B and append the following database parameters to INITTEST.ora:</span></span>

    UNDO\_MANAGEMENT=AUTO
    UNDO\_RETENTION=86400

<span data-ttu-id="88f19-187">For a full list of all Oracle GoldenGate GGSCI commands, see [Reference for Oracle GoldenGate for Windows](http://docs.oracle.com/goldengate/1212/gg-winux/GWURF/ggsci_commands.htm).</span><span class="sxs-lookup"><span data-stu-id="88f19-187">For a full list of all Oracle GoldenGate GGSCI commands, see [Reference for Oracle GoldenGate for Windows](http://docs.oracle.com/goldengate/1212/gg-winux/GWURF/ggsci_commands.htm).</span></span>

### <a name="perform-initial-data-load"></a><span data-ttu-id="88f19-188">Perform initial data load</span><span class="sxs-lookup"><span data-stu-id="88f19-188">Perform initial data load</span></span>
<span data-ttu-id="88f19-189">You can perform the initial data load in the database by following several methods.</span><span class="sxs-lookup"><span data-stu-id="88f19-189">You can perform the initial data load in the database by following several methods.</span></span> <span data-ttu-id="88f19-190">For example, you can use the [Oracle GoldenGate Direct Load](http://docs.oracle.com/goldengate/1212/gg-winux/GWUAD/wu_initsync.htm) or regular Export and Import utilities to export table data from Site A to Site B.</span><span class="sxs-lookup"><span data-stu-id="88f19-190">For example, you can use the [Oracle GoldenGate Direct Load](http://docs.oracle.com/goldengate/1212/gg-winux/GWUAD/wu_initsync.htm) or regular Export and Import utilities to export table data from Site A to Site B.</span></span>

<span data-ttu-id="88f19-191">To demonstrate the Oracle GoldenGate replication process, this tutorial demonstrates creating a table on both Site A and site B by using the following commands.</span><span class="sxs-lookup"><span data-stu-id="88f19-191">To demonstrate the Oracle GoldenGate replication process, this tutorial demonstrates creating a table on both Site A and site B by using the following commands.</span></span>

<span data-ttu-id="88f19-192">First, open up SQL\*Plus command window and run the following command to create an inventory table on Site A and Site B databases:</span><span class="sxs-lookup"><span data-stu-id="88f19-192">First, open up SQL\*Plus command window and run the following command to create an inventory table on Site A and Site B databases:</span></span>

    create table scott.inventory
    (prod_id number,
    prod_category varchar2(20),
    qty_in_stock number,
    last_dml timestamp default systimestamp);

<span data-ttu-id="88f19-193">Next, add a constraint to the newly created table on Site A and Site B databases:</span><span class="sxs-lookup"><span data-stu-id="88f19-193">Next, add a constraint to the newly created table on Site A and Site B databases:</span></span>

    alter table scott.inventory add constraint pk_inventory primary key (prod_id) ;

<span data-ttu-id="88f19-194">Then, grant all privileges on the new inventory table to the user ggate on Site A and Site B:</span><span class="sxs-lookup"><span data-stu-id="88f19-194">Then, grant all privileges on the new inventory table to the user ggate on Site A and Site B:</span></span>

    grant all on scott.inventory to ggate;

<span data-ttu-id="88f19-195">Next, create and enable a database trigger, INVENTORY_CDR_TRG, on the newly created table to make sure that all transactions to the new table are recorded if the user is not ggate.</span><span class="sxs-lookup"><span data-stu-id="88f19-195">Next, create and enable a database trigger, INVENTORY_CDR_TRG, on the newly created table to make sure that all transactions to the new table are recorded if the user is not ggate.</span></span> <span data-ttu-id="88f19-196">Perform this operation on Site A and Site B.</span><span class="sxs-lookup"><span data-stu-id="88f19-196">Perform this operation on Site A and Site B.</span></span>

    CREATE OR REPLACE TRIGGER INVENTORY_CDR_TRG
    BEFORE UPDATE
    ON SCOTT.INVENTORY
    REFERENCING NEW AS New OLD AS Old
    FOR EACH ROW
    BEGIN
    IF SYS_CONTEXT ('USERENV', 'SESSION_USER') != 'GGATE'
    THEN
    :NEW.LAST_DML := SYSTIMESTAMP;
    END IF;
    END;
    /


## <a name="2-prepare-site-a-and-site-b-for-database-replication"></a><span data-ttu-id="88f19-197">2. Prepare Site A and Site B for database replication</span><span class="sxs-lookup"><span data-stu-id="88f19-197">2. Prepare Site A and Site B for database replication</span></span>
<span data-ttu-id="88f19-198">This section explains how to prepare Site A and Site B for database replication.</span><span class="sxs-lookup"><span data-stu-id="88f19-198">This section explains how to prepare Site A and Site B for database replication.</span></span> <span data-ttu-id="88f19-199">You must perform all the steps of this section on both sites: Site A and Site B.</span><span class="sxs-lookup"><span data-stu-id="88f19-199">You must perform all the steps of this section on both sites: Site A and Site B.</span></span>

<span data-ttu-id="88f19-200">First, remote desktop to Site A and Site B via the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="88f19-200">First, remote desktop to Site A and Site B via the Azure classic portal.</span></span> <span data-ttu-id="88f19-201">Switch the database to archivelog mode using the SQL\*Plus command window:</span><span class="sxs-lookup"><span data-stu-id="88f19-201">Switch the database to archivelog mode using the SQL\*Plus command window:</span></span>

    sql>shutdown immediate
    sql>startup mount
    sql>alter database archivelog;
    sql>alter database open;


<span data-ttu-id="88f19-202">Then, enable minimal [supplemental logging](http://docs.oracle.com/cd/E11882_01/server.112/e22490/logminer.htm) as follows:</span><span class="sxs-lookup"><span data-stu-id="88f19-202">Then, enable minimal [supplemental logging](http://docs.oracle.com/cd/E11882_01/server.112/e22490/logminer.htm) as follows:</span></span>

    SQL> ALTER DATABASE ADD SUPPLEMENTAL LOG DATA (ALL) COLUMNS;

<span data-ttu-id="88f19-203">Next, prepare the database to support DDL (data definition language) replication:</span><span class="sxs-lookup"><span data-stu-id="88f19-203">Next, prepare the database to support DDL (data definition language) replication:</span></span>

    SQL> alter system set recyclebin=off scope=spfile;

<span data-ttu-id="88f19-204">Then, shutdown and restart the database:</span><span class="sxs-lookup"><span data-stu-id="88f19-204">Then, shutdown and restart the database:</span></span>

    sql>shutdown immediate
    sql>startup


## <a name="3-create-all-necessary-objects-to-support-ddl-replication"></a><span data-ttu-id="88f19-205">3. Create all necessary objects to support DDL Replication</span><span class="sxs-lookup"><span data-stu-id="88f19-205">3. Create all necessary objects to support DDL Replication</span></span>
<span data-ttu-id="88f19-206">This section lists the scripts that you need to use to create all necessary objects to support DDL Replication.</span><span class="sxs-lookup"><span data-stu-id="88f19-206">This section lists the scripts that you need to use to create all necessary objects to support DDL Replication.</span></span> <span data-ttu-id="88f19-207">You need to run the scripts specified in this section on both Site A and Site B.</span><span class="sxs-lookup"><span data-stu-id="88f19-207">You need to run the scripts specified in this section on both Site A and Site B.</span></span>

<span data-ttu-id="88f19-208">Open up a Windows command prompt and navigate to the Oracle GoldenGate folder, such as C:\\OracleGG.</span><span class="sxs-lookup"><span data-stu-id="88f19-208">Open up a Windows command prompt and navigate to the Oracle GoldenGate folder, such as C:\\OracleGG.</span></span> <span data-ttu-id="88f19-209">Start SQL\*Plus command prompt with database administrator privileges, such as using **SYSDBA** on Site A and Site B.</span><span class="sxs-lookup"><span data-stu-id="88f19-209">Start SQL\*Plus command prompt with database administrator privileges, such as using **SYSDBA** on Site A and Site B.</span></span>

<span data-ttu-id="88f19-210">Then, run the following scripts:</span><span class="sxs-lookup"><span data-stu-id="88f19-210">Then, run the following scripts:</span></span>

    SQL> @marker_setup.sql  
    Enter GoldenGate schema name: ggate
    SQL> @ddl_setup.sql  
    Enter GoldenGate schema name: ggate
    SQL> @role_setup.sql
    Enter GoldenGate schema name: ggate
    SQL> grant ggs_ggsuser_role to ggate;
     Grant succeeded.
     SQL> @ddl_enable
     Trigger altered.
     SQL> @ddl_pin ggate


<span data-ttu-id="88f19-211">Oracle GoldenGate tool requires a table level login for DDL (data definition language) support.</span><span class="sxs-lookup"><span data-stu-id="88f19-211">Oracle GoldenGate tool requires a table level login for DDL (data definition language) support.</span></span> <span data-ttu-id="88f19-212">That’s why, enable supplemental logging at the table level by using the ADD TRANDATA command.</span><span class="sxs-lookup"><span data-stu-id="88f19-212">That’s why, enable supplemental logging at the table level by using the ADD TRANDATA command.</span></span> <span data-ttu-id="88f19-213">Open up Oracle GoldenGate Command interpreter window, login to database, and then run the ADD TRANDATA command:</span><span class="sxs-lookup"><span data-stu-id="88f19-213">Open up Oracle GoldenGate Command interpreter window, login to database, and then run the ADD TRANDATA command:</span></span>

    GGSCI 5> DBLOGIN USERID ggate, PASSWORD ggate

    GGSCI(Hostname) 6> add trandata scott.inventory

## <a name="4-configure-goldengate-manager-on-site-a-and-site-b"></a><span data-ttu-id="88f19-214">4. Configure GoldenGate Manager on Site A and Site B</span><span class="sxs-lookup"><span data-stu-id="88f19-214">4. Configure GoldenGate Manager on Site A and Site B</span></span>
<span data-ttu-id="88f19-215">The Oracle GoldenGate Manager performs a number of functions like starting the other GoldenGate processes, trail log file management and reporting.</span><span class="sxs-lookup"><span data-stu-id="88f19-215">The Oracle GoldenGate Manager performs a number of functions like starting the other GoldenGate processes, trail log file management and reporting.</span></span>

<span data-ttu-id="88f19-216">You need to configure the Oracle GoldenGate Manager process on both Site A and Site B. To do this, perform the following steps on Site A and Site B.</span><span class="sxs-lookup"><span data-stu-id="88f19-216">You need to configure the Oracle GoldenGate Manager process on both Site A and Site B. To do this, perform the following steps on Site A and Site B.</span></span>

<span data-ttu-id="88f19-217">Open Windows command window and initiate the Oracle GoldenGate command interpreter:</span><span class="sxs-lookup"><span data-stu-id="88f19-217">Open Windows command window and initiate the Oracle GoldenGate command interpreter:</span></span>

    cd C:\OracleGG\
    c:\OracleGG>ggsci
    Oracle GoldenGate Command Interpreter for Oracle
    Version 11.2.1.0.3 14400833 OGGCORE_11.2.1.0.3_PLATFORMS_120823.1258
    Windows x64 (optimized), Oracle 11g on Aug 23 2012 16:50:36
    Copyright (C) 1995, 2012, Oracle and/or its affiliates. All rights reserved.


<span data-ttu-id="88f19-218">Logs the GGSCI session into a database so that you can execute commands that affect the database:</span><span class="sxs-lookup"><span data-stu-id="88f19-218">Logs the GGSCI session into a database so that you can execute commands that affect the database:</span></span>

    GGSCI (HostName) 1> DBLOGIN USERID ggate, PASSWORD ggate
    Successfully logged into database.

<span data-ttu-id="88f19-219">Display the status and lag (where relevant) for all Manager, Extract, and Replicat processes on a system:</span><span class="sxs-lookup"><span data-stu-id="88f19-219">Display the status and lag (where relevant) for all Manager, Extract, and Replicat processes on a system:</span></span>

    GGSCI (HostName) 2> info all
    Program     Status      Group       Lag           Time Since Chkpt
    MANAGER     STOPPED

<span data-ttu-id="88f19-220">Open the parameter file using the EDIT PARAMS command and then append the following information:</span><span class="sxs-lookup"><span data-stu-id="88f19-220">Open the parameter file using the EDIT PARAMS command and then append the following information:</span></span>

    GGSCI (HostName) 3> edit params mgr
    PORT 7809
    USERID ggate, PASSWORD ggate
    PURGEOLDEXTRACTS  C:\OracleGG\dirdat\ex, USECHECKPOINTS

<span data-ttu-id="88f19-221">Display the status and lag (where relevant) for all Manager, Extract, and Replicat processes on a system:</span><span class="sxs-lookup"><span data-stu-id="88f19-221">Display the status and lag (where relevant) for all Manager, Extract, and Replicat processes on a system:</span></span>

    GGSCI (HostName) 46> info all
    Program     Status      Group       Lag           Time Since Chkpt
    MANAGER     STOPPED

<span data-ttu-id="88f19-222">Logs the GGSCI session into a database so that you can execute commands that affect the database:</span><span class="sxs-lookup"><span data-stu-id="88f19-222">Logs the GGSCI session into a database so that you can execute commands that affect the database:</span></span>

    GGSCI (HostName) 47> dblogin USERID ggate, PASSWORD ggate

    Successfully logged into database.

<span data-ttu-id="88f19-223">Start the manager process:</span><span class="sxs-lookup"><span data-stu-id="88f19-223">Start the manager process:</span></span>

    GGSCI (HostName) 48> start manager
    Manager started.

## <a name="5-create-extract-group-and-data-pump-processes-on-site-a-and-site-b"></a><span data-ttu-id="88f19-224">5. Create Extract Group and Data Pump processes on Site A and Site B</span><span class="sxs-lookup"><span data-stu-id="88f19-224">5. Create Extract Group and Data Pump processes on Site A and Site B</span></span>
### <a name="create-extract-and-data-pump-processes-on-site-a"></a><span data-ttu-id="88f19-225">Create Extract and Data Pump processes on Site A</span><span class="sxs-lookup"><span data-stu-id="88f19-225">Create Extract and Data Pump processes on Site A</span></span>
<span data-ttu-id="88f19-226">You need to create the Extract and Data Pump processes on Site A and Site B. Remote desktop to Site A and Site B via the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="88f19-226">You need to create the Extract and Data Pump processes on Site A and Site B. Remote desktop to Site A and Site B via the Azure classic portal.</span></span> <span data-ttu-id="88f19-227">Open up GGSCI command interpreter window.</span><span class="sxs-lookup"><span data-stu-id="88f19-227">Open up GGSCI command interpreter window.</span></span> <span data-ttu-id="88f19-228">Run the following commands on Site A:</span><span class="sxs-lookup"><span data-stu-id="88f19-228">Run the following commands on Site A:</span></span>

    GGSCI (MachineGG1) 14> add extract ext1 tranlog begin now
    EXTRACT added.
    GGSCI (MachineGG1) 4> add exttrail C:\OracleGG\dirdat\lt, extract ext1
    EXTTRAIL added.
    GGSCI (MachineGG1) 16> add extract dpump1 exttrailsource C:\OracleGG\dirdat\aa
    EXTRACT added.
    GGSCI (MachineGG1) 17> add rmttrail C:\OracleGG\dirdat\ab extract dpump1
    RMTTRAIL added.

<span data-ttu-id="88f19-229">Open the parameter file using the EDIT PARAMS command and then append the following information: GGSCI (MachineGG1) 18> edit params ext1 EXTRACT ext1 USERID ggate, PASSWORD ggate EXTTRAIL C:\OracleGG\dirdat\aa TRANLOGOPTIONS EXCLUDEUSER ggate TABLE scott.inventory, GETBEFORECOLS ( ON UPDATE KEYINCLUDING (prod_category,qty_in_stock, last_dml), ON DELETE KEYINCLUDING (prod_category,qty_in_stock, last_dml));</span><span class="sxs-lookup"><span data-stu-id="88f19-229">Open the parameter file using the EDIT PARAMS command and then append the following information: GGSCI (MachineGG1) 18> edit params ext1 EXTRACT ext1 USERID ggate, PASSWORD ggate EXTTRAIL C:\OracleGG\dirdat\aa TRANLOGOPTIONS EXCLUDEUSER ggate TABLE scott.inventory, GETBEFORECOLS ( ON UPDATE KEYINCLUDING (prod_category,qty_in_stock, last_dml), ON DELETE KEYINCLUDING (prod_category,qty_in_stock, last_dml));</span></span>

<span data-ttu-id="88f19-230">Open the parameter file using the EDIT PARAMS command and then append the following information:</span><span class="sxs-lookup"><span data-stu-id="88f19-230">Open the parameter file using the EDIT PARAMS command and then append the following information:</span></span>

    GGSCI (MachineGG1) 15> edit params dpump1
    EXTRACT dpump1
     USERID ggate, PASSWORD ggate
     RMTHOST ActiveGG2orcldb, MGRPORT 7809, TCPBUFSIZE 100000
     RMTTRAIL C:\OracleGG\dirdat\ab
     PASSTHRU
     TABLE scott.inventory;

### <a name="create-a-goldengate-checkpoint-table-on-site-b"></a><span data-ttu-id="88f19-231">Create a GoldenGate checkpoint table on Site B</span><span class="sxs-lookup"><span data-stu-id="88f19-231">Create a GoldenGate checkpoint table on Site B</span></span>
<span data-ttu-id="88f19-232">Next, you need to add a checkpoint table on Site B. To do this, you need to open up a GoldenGate command interpreter window and run:</span><span class="sxs-lookup"><span data-stu-id="88f19-232">Next, you need to add a checkpoint table on Site B. To do this, you need to open up a GoldenGate command interpreter window and run:</span></span>

    C:\OracleGG\ggsci
    GGSCI (MachineGG2) 1> DBLOGIN USERID ggate, PASSWORD ggate
    Successfully logged into database.

<span data-ttu-id="88f19-233">And then, add the checkpoint table to the database, where ggate is the owner:</span><span class="sxs-lookup"><span data-stu-id="88f19-233">And then, add the checkpoint table to the database, where ggate is the owner:</span></span>

    GGSCI (MachineGG2) 2> ADD CHECKPOINTTABLE ggate.checkpointtable
    Successfully created checkpoint table ggate.checkpointtable.

<span data-ttu-id="88f19-234">Add the name of the check point table to the GLOBALS file on the target server, which is Site B in this step.</span><span class="sxs-lookup"><span data-stu-id="88f19-234">Add the name of the check point table to the GLOBALS file on the target server, which is Site B in this step.</span></span> <span data-ttu-id="88f19-235">Edit the GLOBALS file on Site B:</span><span class="sxs-lookup"><span data-stu-id="88f19-235">Edit the GLOBALS file on Site B:</span></span>

    GGSCI (MachineGG2) 1> EDIT PARAMS ./GLOBALS

<span data-ttu-id="88f19-236">Then, append the CHECKPOINTTABLE parameter to the existing GLOBALS file:</span><span class="sxs-lookup"><span data-stu-id="88f19-236">Then, append the CHECKPOINTTABLE parameter to the existing GLOBALS file:</span></span>

    GGSCHEMA ggate
    CHECKPOINTTABLE ggate.checkpointtable

<span data-ttu-id="88f19-237">As a final step, save and close the GLOBALS parameter file.</span><span class="sxs-lookup"><span data-stu-id="88f19-237">As a final step, save and close the GLOBALS parameter file.</span></span>

### <a name="add-replicat-on-site-b"></a><span data-ttu-id="88f19-238">Add REPLICAT on Site B</span><span class="sxs-lookup"><span data-stu-id="88f19-238">Add REPLICAT on Site B</span></span>
<span data-ttu-id="88f19-239">This section describes how to add a REPLICAT process “REP2” on Site B.</span><span class="sxs-lookup"><span data-stu-id="88f19-239">This section describes how to add a REPLICAT process “REP2” on Site B.</span></span>

<span data-ttu-id="88f19-240">Use ADD REPLICAT command to create a Replicat group on Site B:</span><span class="sxs-lookup"><span data-stu-id="88f19-240">Use ADD REPLICAT command to create a Replicat group on Site B:</span></span>

    GGSCI (MachineGG2) 37> add replicat rep2 exttrail C:\OracleGG\dirdatab, checkpointtable ggate.checkpointtable

<span data-ttu-id="88f19-241">Open the parameter file using the EDIT PARAMS command and then append the following information:</span><span class="sxs-lookup"><span data-stu-id="88f19-241">Open the parameter file using the EDIT PARAMS command and then append the following information:</span></span>

    GGSCI (MachineGG2) 10> edit params rep2
    REPLICAT rep2
    ASSUMETARGETDEFS
    USERID ggate, PASSWORD ggate
    DISCARDFILE C:\OracleGG\dirdat\discard.txt, append,megabytes 10
    MAP scott.inventory, TARGET scott.inventory;

### <a name="create-extract-and-data-pump-processes-on-site-b"></a><span data-ttu-id="88f19-242">Create Extract and Data Pump processes on Site B</span><span class="sxs-lookup"><span data-stu-id="88f19-242">Create Extract and Data Pump processes on Site B</span></span>
<span data-ttu-id="88f19-243">This section describes how to create a new extract process “EXT2” and a new data pump process “DPUMP2” on Site B:</span><span class="sxs-lookup"><span data-stu-id="88f19-243">This section describes how to create a new extract process “EXT2” and a new data pump process “DPUMP2” on Site B:</span></span>

    GGSCI (MachineGG2) 3> add extract ext2 tranlog begin now
     EXTRACT added.
    GGSCI (MachineGG2) 4> add exttrail C:\OracleGG\dirdat\ac extract ext2
     EXTTRAIL added.
    GGSCI (MachineGG2) 5> add extract dpump2 exttrailsource C:\OracleGG\dirdat\ac
     EXTRACT added.
    GGSCI (MachineGG2) 6> add rmttrail C:\OracleGG\dirdat\ad extract dpump2
     RMTTRAIL added.

<span data-ttu-id="88f19-244">Open the parameter file using the EDIT PARAMS command and then append the following information:</span><span class="sxs-lookup"><span data-stu-id="88f19-244">Open the parameter file using the EDIT PARAMS command and then append the following information:</span></span>

    GGSCI (MachineGG2) 31> edit params ext2
    EXTRACT ext2
    USERID ggate, PASSWORD ggate
    EXTTRAIL C:\OracleGG\dirdat\ac
    TRANLOGOPTIONS EXCLUDEUSER ggate
    TABLE scott.inventory,
    GETBEFORECOLS (
    ON UPDATE KEYINCLUDING (prod_category,qty_in_stock, last_dml),
    ON DELETE KEYINCLUDING (prod_category,qty_in_stock, last_dml));

<span data-ttu-id="88f19-245">Open the parameter file using the EDIT PARAMS command and then append the following information:</span><span class="sxs-lookup"><span data-stu-id="88f19-245">Open the parameter file using the EDIT PARAMS command and then append the following information:</span></span>

    GGSCI (MachineGG2) 32> edit params dpump2
    EXTRACT dpump2
    USERID ggate, PASSWORD ggate
    RMTHOST MachineGG1, MGRPORT 7809, TCPBUFSIZE 100000
    RMTTRAIL C:\OracleGG\dirdat\ad
    PASSTHRU
    TABLE scott.inventory;

### <a name="create-a-goldengate-checkpoint-table-on-site-a"></a><span data-ttu-id="88f19-246">Create a GoldenGate checkpoint table on Site A</span><span class="sxs-lookup"><span data-stu-id="88f19-246">Create a GoldenGate checkpoint table on Site A</span></span>
<span data-ttu-id="88f19-247">Open up Oracle GoldenGate command interpreter window and create a checkpoint table:</span><span class="sxs-lookup"><span data-stu-id="88f19-247">Open up Oracle GoldenGate command interpreter window and create a checkpoint table:</span></span>

    GGSCI (MachineGG1) 1> DBLOGIN USERID ggate, PASSWORD ggate
    Successfully logged into database.

    GGSCI (MachineGG1) 2> ADD CHECKPOINTTABLE ggate.checkpointtable

    Successfully created checkpoint table ggate.checkpointtable.

<span data-ttu-id="88f19-248">You also need to add the name of the check point table to the GLOBALS file on Site A.</span><span class="sxs-lookup"><span data-stu-id="88f19-248">You also need to add the name of the check point table to the GLOBALS file on Site A.</span></span>

<span data-ttu-id="88f19-249">Open up Oracle GoldenGate command interpreter window and edit the GLOBALS file on Site A:</span><span class="sxs-lookup"><span data-stu-id="88f19-249">Open up Oracle GoldenGate command interpreter window and edit the GLOBALS file on Site A:</span></span>

    GGSCI (MachineGG1) 1> EDIT PARAMS ./GLOBALS
    Add the CHECKPOINTTABLE parameter to the existing GLOBALS file as follows:
    GGSCHEMA ggate
    CHECKPOINTTABLE ggate.checkpointtable

<span data-ttu-id="88f19-250">Save and close the GLOBALS parameter file.</span><span class="sxs-lookup"><span data-stu-id="88f19-250">Save and close the GLOBALS parameter file.</span></span>

### <a name="add-replicat-on-site-a"></a><span data-ttu-id="88f19-251">Add REPLICAT on Site A</span><span class="sxs-lookup"><span data-stu-id="88f19-251">Add REPLICAT on Site A</span></span>
<span data-ttu-id="88f19-252">This section describes how to add a REPLICAT process “REP1” on Site A.</span><span class="sxs-lookup"><span data-stu-id="88f19-252">This section describes how to add a REPLICAT process “REP1” on Site A.</span></span>

<span data-ttu-id="88f19-253">The following command creates a Replicat group rep1 with the name of a trail, and the associated checkpointtable.</span><span class="sxs-lookup"><span data-stu-id="88f19-253">The following command creates a Replicat group rep1 with the name of a trail, and the associated checkpointtable.</span></span>

    GGSCI (MachineGG1) 21> add replicat rep1 exttrail C:\OracleGG\dirdat\ad,checkpointtable ggate.checkpointtable
     REPLICAT added.

<span data-ttu-id="88f19-254">Open the parameter file using the EDIT PARAMS command and then append the following information:</span><span class="sxs-lookup"><span data-stu-id="88f19-254">Open the parameter file using the EDIT PARAMS command and then append the following information:</span></span>

    GGSCI (MachineGG1) 10> edit params rep1
    REPLICAT rep1
    ASSUMETARGETDEFS
    USERID ggate, PASSWORD ggate
    DISCARDFILE C:\OracleGG\dirdat\discard.txt, append, megabytes 10
    MAP scott.inventory, TARGET scott.inventory;

### <a name="add-trandata-on-site-a-and-site-b"></a><span data-ttu-id="88f19-255">Add trandata on Site A and Site B</span><span class="sxs-lookup"><span data-stu-id="88f19-255">Add trandata on Site A and Site B</span></span>
<span data-ttu-id="88f19-256">Enable supplemental logging at the table level by using the ADD TRANDATA command.</span><span class="sxs-lookup"><span data-stu-id="88f19-256">Enable supplemental logging at the table level by using the ADD TRANDATA command.</span></span> <span data-ttu-id="88f19-257">Open up Oracle GoldenGate Command interpreter window, login to database, and then run the ADD TRANDATA command.</span><span class="sxs-lookup"><span data-stu-id="88f19-257">Open up Oracle GoldenGate Command interpreter window, login to database, and then run the ADD TRANDATA command.</span></span>

<span data-ttu-id="88f19-258">Remote desktop to MachineGG1, open up Oracle GoldenGate command interpreter, and run:</span><span class="sxs-lookup"><span data-stu-id="88f19-258">Remote desktop to MachineGG1, open up Oracle GoldenGate command interpreter, and run:</span></span>

    GGSCI (MachineGG1) 11> dblogin userid ggate password ggate
     Successfully logged into database.
    GGSCI (MachineGG1) 12> add trandata scott.inventory cols (prod_category,qty_in_stock, last_dml)
    GGSCI (MachineGG1) 13> info trandata scott.inventory
    Logging of supplemental redo log data is enabled for table SCOTT.INVENTORY.
    Columns supplementally logged for table SCOTT.INVENTORY: PROD_ID, PROD_CATEGORY, QTY_IN_STOCK, LAST_DML.

<span data-ttu-id="88f19-259">Remote desktop to MachineGG2, open up Oracle GoldenGate command interpreter, and run:</span><span class="sxs-lookup"><span data-stu-id="88f19-259">Remote desktop to MachineGG2, open up Oracle GoldenGate command interpreter, and run:</span></span>

    GGSCI (MachineGG2) 18> dblogin userid ggate password ggate
     Successfully logged into database.
    GGSCI (MachineGG2) 14> add trandata scott.inventory cols (prod_category,qty_in_stock, last_dml)
    Logging of supplemental redo data enabled for table SCOTT.INVENTORY.

<span data-ttu-id="88f19-260">Display information about the state of table-level supplemental logging:</span><span class="sxs-lookup"><span data-stu-id="88f19-260">Display information about the state of table-level supplemental logging:</span></span>

    GGSCI (MachineGG2) 15> info trandata scott.inventory
    Logging of supplemental redo log data is enabled for table SCOTT.INVENTORY.
    Columns supplementally logged for table SCOTT.INVENTORY: PROD_ID, PROD_CATEGORY, QTY_IN_STOCK, LAST_DML.

### <a name="add-trandata-on-site-a-and-site-b"></a><span data-ttu-id="88f19-261">Add trandata on Site A and Site B</span><span class="sxs-lookup"><span data-stu-id="88f19-261">Add trandata on Site A and Site B</span></span>
<span data-ttu-id="88f19-262">Enable supplemental logging at the table level by using the ADD TRANDATA command.</span><span class="sxs-lookup"><span data-stu-id="88f19-262">Enable supplemental logging at the table level by using the ADD TRANDATA command.</span></span> <span data-ttu-id="88f19-263">Open up Oracle GoldenGate Command interpreter window, login to database, and then run the ADD TRANDATA command.</span><span class="sxs-lookup"><span data-stu-id="88f19-263">Open up Oracle GoldenGate Command interpreter window, login to database, and then run the ADD TRANDATA command.</span></span>

<span data-ttu-id="88f19-264">Remote desktop to MachineGG1, open up Oracle GoldenGate command interpreter, and run:</span><span class="sxs-lookup"><span data-stu-id="88f19-264">Remote desktop to MachineGG1, open up Oracle GoldenGate command interpreter, and run:</span></span>

    GGSCI (MachineGG1) 11> dblogin userid ggate password ggate
     Successfully logged into database.
    GGSCI (MachineGG1) 12> add trandata scott.inventory cols (prod_category,qty_in_stock, last_dml)
    GGSCI (MachineGG1) 13> info trandata scott.inventory
    Logging of supplemental redo log data is enabled for table SCOTT.INVENTORY.
    Columns supplementally logged for table SCOTT.INVENTORY: PROD_ID, PROD_CATEGORY, QTY_IN_STOCK, LAST_DML.

<span data-ttu-id="88f19-265">Remote desktop to MachineGG2, open up Oracle GoldenGate command interpreter, and run:</span><span class="sxs-lookup"><span data-stu-id="88f19-265">Remote desktop to MachineGG2, open up Oracle GoldenGate command interpreter, and run:</span></span>

    GGSCI (MachineGG2) 18> dblogin userid ggate password ggate
     Successfully logged into database.
    GGSCI (MachineGG2) 14> add trandata scott.inventory cols (prod_category,qty_in_stock, last_dml)
    Logging of supplemental redo data enabled for table SCOTT.INVENTORY.
    Display information about the state of table-level supplemental logging:
    GGSCI (MachineGG2) 15> info trandata scott.inventory
    Logging of supplemental redo log data is enabled for table SCOTT.INVENTORY.
    Columns supplementally logged for table SCOTT.INVENTORY: PROD_ID, PROD_CATEGORY, QTY_IN_STOCK, LAST_DML.

### <a name="start-extract-and-data-pump-processes-on-site-a"></a><span data-ttu-id="88f19-266">Start Extract and Data Pump processes on Site A</span><span class="sxs-lookup"><span data-stu-id="88f19-266">Start Extract and Data Pump processes on Site A</span></span>
<span data-ttu-id="88f19-267">Start the Extract process ext1 on Site A:</span><span class="sxs-lookup"><span data-stu-id="88f19-267">Start the Extract process ext1 on Site A:</span></span>

    GGSCI (MachineGG1) 31> start extract ext1
    Sending START request to MANAGER …
    EXTRACT EXT1 starting

<span data-ttu-id="88f19-268">Start the data pump process dpump1 on Site A:</span><span class="sxs-lookup"><span data-stu-id="88f19-268">Start the data pump process dpump1 on Site A:</span></span>

    GGSCI (MachineGG1) 23> start extract dpump1
    Sending START request to MANAGER …
    EXTRACT DPUMP1 starting
<span data-ttu-id="88f19-269">Display information about the Extract group ext1: GGSCI (MachineGG1) 32> info extract ext1 EXTRACT    EXT1      Last Started 2013-11-25 08:03   Status RUNNING Checkpoint Lag       00:00:00 (updated 00:00:02 ago) Log Read Checkpoint  Oracle Redo Logs 2013-11-25 08:03:18  Seqno 6, RBA 3230720 SCN 0.1074371 (1074371)</span><span class="sxs-lookup"><span data-stu-id="88f19-269">Display information about the Extract group ext1: GGSCI (MachineGG1) 32> info extract ext1 EXTRACT    EXT1      Last Started 2013-11-25 08:03   Status RUNNING Checkpoint Lag       00:00:00 (updated 00:00:02 ago) Log Read Checkpoint  Oracle Redo Logs 2013-11-25 08:03:18  Seqno 6, RBA 3230720 SCN 0.1074371 (1074371)</span></span>

<span data-ttu-id="88f19-270">Display the status and lag (where relevant) for all Manager, Extract, and Replicat processes on a system:</span><span class="sxs-lookup"><span data-stu-id="88f19-270">Display the status and lag (where relevant) for all Manager, Extract, and Replicat processes on a system:</span></span>

    GGSCI (MachineGG1) 16> info all
    Program     Status      Group       Lag at Chkpt  Time Since Chkpt

    MANAGER     RUNNING
    EXTRACT     RUNNING     DPUMP1      00:00:00      00:46:33
    EXTRACT     RUNNING     EXT1        00:00:00      00:00:04

### <a name="start-extract-and-data-pump-processes-on-site-b"></a><span data-ttu-id="88f19-271">Start Extract and Data Pump processes on Site B</span><span class="sxs-lookup"><span data-stu-id="88f19-271">Start Extract and Data Pump processes on Site B</span></span>
<span data-ttu-id="88f19-272">Start the Extract process ext2 on Site B:</span><span class="sxs-lookup"><span data-stu-id="88f19-272">Start the Extract process ext2 on Site B:</span></span>

    GGSCI (MachineGG2) 22> start extract ext2
    Sending START request to MANAGER …
    EXTRACT EXT2 starting

<span data-ttu-id="88f19-273">Start the data pump process dpump2 on Site B:</span><span class="sxs-lookup"><span data-stu-id="88f19-273">Start the data pump process dpump2 on Site B:</span></span>

    GGSCI (MachineGG2) 23> start extract dpump2
    Sending START request to MANAGER …
    EXTRACT DPUMP2 starting

<span data-ttu-id="88f19-274">Display the status and lag (where relevant) for all Manager, Extract, and Replicat processes on a system:</span><span class="sxs-lookup"><span data-stu-id="88f19-274">Display the status and lag (where relevant) for all Manager, Extract, and Replicat processes on a system:</span></span>

    GGSCI (ActiveGG2orcldb) 6> info all
    Program     Status      Group       Lag at Chkpt  Time Since Chkpt

    MANAGER     RUNNING
    EXTRACT     RUNNING     DPUMP2      00:00:00      136:13:33
    EXTRACT     RUNNING     EXT2        00:00:00      00:00:04

### <a name="start-replicat-process-on-site-a"></a><span data-ttu-id="88f19-275">Start REPLICAT process on Site A</span><span class="sxs-lookup"><span data-stu-id="88f19-275">Start REPLICAT process on Site A</span></span>
<span data-ttu-id="88f19-276">This section describes how to start the REPLICAT process “REP1” on Site A.</span><span class="sxs-lookup"><span data-stu-id="88f19-276">This section describes how to start the REPLICAT process “REP1” on Site A.</span></span>

<span data-ttu-id="88f19-277">Start the Replicat process on Site A:</span><span class="sxs-lookup"><span data-stu-id="88f19-277">Start the Replicat process on Site A:</span></span>

    GGSCI (MachineGG1) 38> start replicat rep1
    Sending START request to MANAGER …
    REPLICAT REP1 starting

<span data-ttu-id="88f19-278">Display the status of a Replicat group:</span><span class="sxs-lookup"><span data-stu-id="88f19-278">Display the status of a Replicat group:</span></span>

    GGSCI (MachineGG1) 39> status replicat rep1
     REPLICAT REP1: RUNNING

### <a name="start-replicat-process-on-site-b"></a><span data-ttu-id="88f19-279">Start REPLICAT process on Site B</span><span class="sxs-lookup"><span data-stu-id="88f19-279">Start REPLICAT process on Site B</span></span>
<span data-ttu-id="88f19-280">This section describes how to start the REPLICAT process “REP2” on Site B.</span><span class="sxs-lookup"><span data-stu-id="88f19-280">This section describes how to start the REPLICAT process “REP2” on Site B.</span></span>

<span data-ttu-id="88f19-281">Start the Replicat process on Site B:</span><span class="sxs-lookup"><span data-stu-id="88f19-281">Start the Replicat process on Site B:</span></span>

    GGSCI (MachineGG2) 26> start replicat rep2
    Sending START request to MANAGER …
    REPLICAT REP2 starting

<span data-ttu-id="88f19-282">Display the status of a Replicat group:</span><span class="sxs-lookup"><span data-stu-id="88f19-282">Display the status of a Replicat group:</span></span>

    GGSCI (MachineGG2) 27> status replicat rep2
    REPLICAT REP2: RUNNING

## <a name="6-verify-the-bi-directional-replication-process"></a><span data-ttu-id="88f19-283">6. Verify the bi-directional replication process</span><span class="sxs-lookup"><span data-stu-id="88f19-283">6. Verify the bi-directional replication process</span></span>
<span data-ttu-id="88f19-284">To verify the Oracle GoldenGate configuration, insert a row into the database at Site A. Remote Desktop to Site A. Open up SQL\*Plus command window and run: SQL> select name from v$database;</span><span class="sxs-lookup"><span data-stu-id="88f19-284">To verify the Oracle GoldenGate configuration, insert a row into the database at Site A. Remote Desktop to Site A. Open up SQL\*Plus command window and run: SQL> select name from v$database;</span></span>

    NAME
    ———
    TESTGG

    SQL> insert into inventory values  (100,’TV’,100,sysdate);

    1 row created.

    SQL> commit;

    Commit complete.

<span data-ttu-id="88f19-285">Then, check if that row is replicated on Site B. To do this, remote desktop to Site B. Open up SQL Plus window and run:</span><span class="sxs-lookup"><span data-stu-id="88f19-285">Then, check if that row is replicated on Site B. To do this, remote desktop to Site B. Open up SQL Plus window and run:</span></span>

    SQL> select name from v$database;

    NAME
    ———
    TESTGG

    SQL> select * from inventory;

    PROD_ID PROD_CATEGORY QTY_IN_STOCK LAST_DML
    ———- ——————– ———— ———
    100 TV 100 22-MAR-13

<span data-ttu-id="88f19-286">Insert a new record at Site B:</span><span class="sxs-lookup"><span data-stu-id="88f19-286">Insert a new record at Site B:</span></span>

    SQL> insert into inventory  values  (101,’DVD’,10,sysdate);
    1 row created.

    SQL> commit;

    Commit complete.

<span data-ttu-id="88f19-287">Remote desktop to Site A and check if the replication has taken place:</span><span class="sxs-lookup"><span data-stu-id="88f19-287">Remote desktop to Site A and check if the replication has taken place:</span></span>

    SQL> select * from inventory;

    PROD_ID PROD_CATEGORY QTY_IN_STOCK LAST_DML
    ———- ——————– ———— ———
    100 TV 100 22-MAR-13
    101 DVD 10 22-MAR-13

## <a name="additional-resources"></a><span data-ttu-id="88f19-288">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="88f19-288">Additional Resources</span></span>
[<span data-ttu-id="88f19-289">Oracle Virtual Machine images for Azure</span><span class="sxs-lookup"><span data-stu-id="88f19-289">Oracle Virtual Machine images for Azure</span></span>](../../linux/classic/oracle-images.md)

