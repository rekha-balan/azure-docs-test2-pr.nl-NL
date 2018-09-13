---
title: Clusterize MySQL with load-balanced sets | Microsoft Docs
description: Set up a load-balanced, high availability Linux MySQL cluster created with the classic deployment model on Azure
services: virtual-machines-linux
documentationcenter: ''
author: bureado
manager: timlt
editor: ''
tags: azure-service-management
ms.assetid: 6c413a16-e9b5-4ffe-a8a3-ae67046bbdf3
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/14/2015
ms.author: jparrel
ms.openlocfilehash: 082d9c0e459298f3c2ed1a72e41b382090ae3dcb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556033"
---
# <a name="use-load-balanced-sets-to-clusterize-mysql-on-linux"></a><span data-ttu-id="578c6-103">Use load-balanced sets to clusterize MySQL on Linux</span><span class="sxs-lookup"><span data-stu-id="578c6-103">Use load-balanced sets to clusterize MySQL on Linux</span></span>
> [!IMPORTANT]
> <span data-ttu-id="578c6-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span><span class="sxs-lookup"><span data-stu-id="578c6-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="578c6-105">This article covers using the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="578c6-105">This article covers using the classic deployment model.</span></span> <span data-ttu-id="578c6-106">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="578c6-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="578c6-107">A [Resource Manager template](https://azure.microsoft.com/documentation/templates/mysql-replication/) is available if you need to deploy a MySQL cluster.</span><span class="sxs-lookup"><span data-stu-id="578c6-107">A [Resource Manager template](https://azure.microsoft.com/documentation/templates/mysql-replication/) is available if you need to deploy a MySQL cluster.</span></span>

<span data-ttu-id="578c6-108">This article explores and illustrates the different approaches available to deploy highly available Linux-based services on Microsoft Azure, exploring MySQL Server high availability as a primer.</span><span class="sxs-lookup"><span data-stu-id="578c6-108">This article explores and illustrates the different approaches available to deploy highly available Linux-based services on Microsoft Azure, exploring MySQL Server high availability as a primer.</span></span> <span data-ttu-id="578c6-109">A video illustrating this approach is available on [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).</span><span class="sxs-lookup"><span data-stu-id="578c6-109">A video illustrating this approach is available on [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).</span></span>

<span data-ttu-id="578c6-110">We will outline a shared-nothing, two-node, single-master MySQL high availability solution based on DRBD, Corosync, and Pacemaker.</span><span class="sxs-lookup"><span data-stu-id="578c6-110">We will outline a shared-nothing, two-node, single-master MySQL high availability solution based on DRBD, Corosync, and Pacemaker.</span></span> <span data-ttu-id="578c6-111">Only one node runs MySQL at a time.</span><span class="sxs-lookup"><span data-stu-id="578c6-111">Only one node runs MySQL at a time.</span></span> <span data-ttu-id="578c6-112">Reading and writing from the DRBD resource is also limited to only one node at a time.</span><span class="sxs-lookup"><span data-stu-id="578c6-112">Reading and writing from the DRBD resource is also limited to only one node at a time.</span></span>

<span data-ttu-id="578c6-113">There's no need for a VIP solution like LVS, because you'll use load-balanced sets in Microsoft Azure to provide round-robin functionality and endpoint detection, removal, and graceful recovery of the VIP.</span><span class="sxs-lookup"><span data-stu-id="578c6-113">There's no need for a VIP solution like LVS, because you'll use load-balanced sets in Microsoft Azure to provide round-robin functionality and endpoint detection, removal, and graceful recovery of the VIP.</span></span> <span data-ttu-id="578c6-114">The VIP is a globally routable IPv4 address assigned by Microsoft Azure when you first create the cloud service.</span><span class="sxs-lookup"><span data-stu-id="578c6-114">The VIP is a globally routable IPv4 address assigned by Microsoft Azure when you first create the cloud service.</span></span>

<span data-ttu-id="578c6-115">There are other possible architectures for MySQL, including NBD Cluster, Percona, Galera, and several middleware solutions, including at least one available as a VM on [VM Depot](http://vmdepot.msopentech.com).</span><span class="sxs-lookup"><span data-stu-id="578c6-115">There are other possible architectures for MySQL, including NBD Cluster, Percona, Galera, and several middleware solutions, including at least one available as a VM on [VM Depot](http://vmdepot.msopentech.com).</span></span> <span data-ttu-id="578c6-116">As long as these solutions can replicate on unicast vs. multicast or broadcast and don't rely on shared storage or multiple network interfaces, the scenarios should be easy to deploy on Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="578c6-116">As long as these solutions can replicate on unicast vs. multicast or broadcast and don't rely on shared storage or multiple network interfaces, the scenarios should be easy to deploy on Microsoft Azure.</span></span>

<span data-ttu-id="578c6-117">These clustering architectures can be extended to other products like PostgreSQL and OpenLDAP in a similar fashion.</span><span class="sxs-lookup"><span data-stu-id="578c6-117">These clustering architectures can be extended to other products like PostgreSQL and OpenLDAP in a similar fashion.</span></span> <span data-ttu-id="578c6-118">For example, this load-balancing procedure with shared nothing was successfully tested with multi-master OpenLDAP, and you can watch it on our Channel 9 blog.</span><span class="sxs-lookup"><span data-stu-id="578c6-118">For example, this load-balancing procedure with shared nothing was successfully tested with multi-master OpenLDAP, and you can watch it on our Channel 9 blog.</span></span>

## <a name="get-ready"></a><span data-ttu-id="578c6-119">Get ready</span><span class="sxs-lookup"><span data-stu-id="578c6-119">Get ready</span></span>
<span data-ttu-id="578c6-120">You need the following resources and abilities:</span><span class="sxs-lookup"><span data-stu-id="578c6-120">You need the following resources and abilities:</span></span>

  - <span data-ttu-id="578c6-121">A Microsoft Azure account with a valid subscription, able to create at least two VMs (XS was used in this example)</span><span class="sxs-lookup"><span data-stu-id="578c6-121">A Microsoft Azure account with a valid subscription, able to create at least two VMs (XS was used in this example)</span></span>
  - <span data-ttu-id="578c6-122">A network and a subnet</span><span class="sxs-lookup"><span data-stu-id="578c6-122">A network and a subnet</span></span>
  - <span data-ttu-id="578c6-123">An affinity group</span><span class="sxs-lookup"><span data-stu-id="578c6-123">An affinity group</span></span>
  - <span data-ttu-id="578c6-124">An availability set</span><span class="sxs-lookup"><span data-stu-id="578c6-124">An availability set</span></span>
  - <span data-ttu-id="578c6-125">The ability to create VHDs in the same region as the cloud service and attach them to the Linux VMs</span><span class="sxs-lookup"><span data-stu-id="578c6-125">The ability to create VHDs in the same region as the cloud service and attach them to the Linux VMs</span></span>

### <a name="tested-environment"></a><span data-ttu-id="578c6-126">Tested environment</span><span class="sxs-lookup"><span data-stu-id="578c6-126">Tested environment</span></span>
* <span data-ttu-id="578c6-127">Ubuntu 13.10</span><span class="sxs-lookup"><span data-stu-id="578c6-127">Ubuntu 13.10</span></span>
  * <span data-ttu-id="578c6-128">DRBD</span><span class="sxs-lookup"><span data-stu-id="578c6-128">DRBD</span></span>
  * <span data-ttu-id="578c6-129">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="578c6-129">MySQL Server</span></span>
  * <span data-ttu-id="578c6-130">Corosync and Pacemaker</span><span class="sxs-lookup"><span data-stu-id="578c6-130">Corosync and Pacemaker</span></span>

### <a name="affinity-group"></a><span data-ttu-id="578c6-131">Affinity group</span><span class="sxs-lookup"><span data-stu-id="578c6-131">Affinity group</span></span>
<span data-ttu-id="578c6-132">Create an affinity group for the solution by signing in to the Azure classic portal, selecting **Settings**, and creating an affinity group.</span><span class="sxs-lookup"><span data-stu-id="578c6-132">Create an affinity group for the solution by signing in to the Azure classic portal, selecting **Settings**, and creating an affinity group.</span></span> <span data-ttu-id="578c6-133">Allocated resources created later will be assigned to this affinity group.</span><span class="sxs-lookup"><span data-stu-id="578c6-133">Allocated resources created later will be assigned to this affinity group.</span></span>

### <a name="networks"></a><span data-ttu-id="578c6-134">Networks</span><span class="sxs-lookup"><span data-stu-id="578c6-134">Networks</span></span>
<span data-ttu-id="578c6-135">A new network is created, and a subnet is created inside the network.</span><span class="sxs-lookup"><span data-stu-id="578c6-135">A new network is created, and a subnet is created inside the network.</span></span> <span data-ttu-id="578c6-136">This example uses a 10.10.10.0/24 network with only one /24 subnet inside.</span><span class="sxs-lookup"><span data-stu-id="578c6-136">This example uses a 10.10.10.0/24 network with only one /24 subnet inside.</span></span>

### <a name="virtual-machines"></a><span data-ttu-id="578c6-137">Virtual machines</span><span class="sxs-lookup"><span data-stu-id="578c6-137">Virtual machines</span></span>
<span data-ttu-id="578c6-138">The first Ubuntu 13.10 VM is created by using an Endorsed Ubuntu Gallery image and is called `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="578c6-138">The first Ubuntu 13.10 VM is created by using an Endorsed Ubuntu Gallery image and is called `hadb01`.</span></span> <span data-ttu-id="578c6-139">A new cloud service is created in the process, called hadb.</span><span class="sxs-lookup"><span data-stu-id="578c6-139">A new cloud service is created in the process, called hadb.</span></span> <span data-ttu-id="578c6-140">This name illustrates the shared, load-balanced nature that the service will have when more resources are added.</span><span class="sxs-lookup"><span data-stu-id="578c6-140">This name illustrates the shared, load-balanced nature that the service will have when more resources are added.</span></span> <span data-ttu-id="578c6-141">The creation of `hadb01` is uneventful and completed by using the portal.</span><span class="sxs-lookup"><span data-stu-id="578c6-141">The creation of `hadb01` is uneventful and completed by using the portal.</span></span> <span data-ttu-id="578c6-142">An endpoint for SSH is automatically created, and the new network is selected.</span><span class="sxs-lookup"><span data-stu-id="578c6-142">An endpoint for SSH is automatically created, and the new network is selected.</span></span> <span data-ttu-id="578c6-143">Now you can create an availability set for the VMs.</span><span class="sxs-lookup"><span data-stu-id="578c6-143">Now you can create an availability set for the VMs.</span></span>

<span data-ttu-id="578c6-144">After the first VM is created (technically, when the cloud service is created), create the second VM, `hadb02`.</span><span class="sxs-lookup"><span data-stu-id="578c6-144">After the first VM is created (technically, when the cloud service is created), create the second VM, `hadb02`.</span></span> <span data-ttu-id="578c6-145">For the second VM, use Ubuntu 13.10 VM from the Gallery by using the portal, but use an existing cloud service, `hadb.cloudapp.net`, instead of creating a new one.</span><span class="sxs-lookup"><span data-stu-id="578c6-145">For the second VM, use Ubuntu 13.10 VM from the Gallery by using the portal, but use an existing cloud service, `hadb.cloudapp.net`, instead of creating a new one.</span></span> <span data-ttu-id="578c6-146">The network and availability set should be automatically selected.</span><span class="sxs-lookup"><span data-stu-id="578c6-146">The network and availability set should be automatically selected.</span></span> <span data-ttu-id="578c6-147">An SSH endpoint will be created, too.</span><span class="sxs-lookup"><span data-stu-id="578c6-147">An SSH endpoint will be created, too.</span></span>

<span data-ttu-id="578c6-148">After both VMs have been created, take note of the SSH port for `hadb01` (TCP 22) and `hadb02` (automatically assigned by Azure).</span><span class="sxs-lookup"><span data-stu-id="578c6-148">After both VMs have been created, take note of the SSH port for `hadb01` (TCP 22) and `hadb02` (automatically assigned by Azure).</span></span>

### <a name="attached-storage"></a><span data-ttu-id="578c6-149">Attached storage</span><span class="sxs-lookup"><span data-stu-id="578c6-149">Attached storage</span></span>
<span data-ttu-id="578c6-150">Attach a new disk to both VMs and create 5-GB disks in the process.</span><span class="sxs-lookup"><span data-stu-id="578c6-150">Attach a new disk to both VMs and create 5-GB disks in the process.</span></span> <span data-ttu-id="578c6-151">The disks are hosted in the VHD container in use for your main operating system disks.</span><span class="sxs-lookup"><span data-stu-id="578c6-151">The disks are hosted in the VHD container in use for your main operating system disks.</span></span> <span data-ttu-id="578c6-152">After disks are created and attached, there is no need to restart Linux because the kernel will see the new device.</span><span class="sxs-lookup"><span data-stu-id="578c6-152">After disks are created and attached, there is no need to restart Linux because the kernel will see the new device.</span></span> <span data-ttu-id="578c6-153">This device is usually `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="578c6-153">This device is usually `/dev/sdc`.</span></span> <span data-ttu-id="578c6-154">Check `dmesg` for the output.</span><span class="sxs-lookup"><span data-stu-id="578c6-154">Check `dmesg` for the output.</span></span>

<span data-ttu-id="578c6-155">On each VM, create a partition by using `cfdisk` (primary, Linux partition) and write the new partition table.</span><span class="sxs-lookup"><span data-stu-id="578c6-155">On each VM, create a partition by using `cfdisk` (primary, Linux partition) and write the new partition table.</span></span> <span data-ttu-id="578c6-156">Do not create a file system on this partition.</span><span class="sxs-lookup"><span data-stu-id="578c6-156">Do not create a file system on this partition.</span></span>

## <a name="set-up-the-cluster"></a><span data-ttu-id="578c6-157">Set up the cluster</span><span class="sxs-lookup"><span data-stu-id="578c6-157">Set up the cluster</span></span>
<span data-ttu-id="578c6-158">Use APT to install Corosync, Pacemaker, and DRBD on both Ubuntu VMs.</span><span class="sxs-lookup"><span data-stu-id="578c6-158">Use APT to install Corosync, Pacemaker, and DRBD on both Ubuntu VMs.</span></span> <span data-ttu-id="578c6-159">To do so with `apt-get`, run the following code:</span><span class="sxs-lookup"><span data-stu-id="578c6-159">To do so with `apt-get`, run the following code:</span></span>

    sudo apt-get install corosync pacemaker drbd8-utils.

<span data-ttu-id="578c6-160">Do not install MySQL at this time.</span><span class="sxs-lookup"><span data-stu-id="578c6-160">Do not install MySQL at this time.</span></span> <span data-ttu-id="578c6-161">Debian and Ubuntu installation scripts will initialize a MySQL data directory on `/var/lib/mysql`, but because the directory will be superseded by a DRBD file system, you need to install MySQL later.</span><span class="sxs-lookup"><span data-stu-id="578c6-161">Debian and Ubuntu installation scripts will initialize a MySQL data directory on `/var/lib/mysql`, but because the directory will be superseded by a DRBD file system, you need to install MySQL later.</span></span>

<span data-ttu-id="578c6-162">Verify (by using `/sbin/ifconfig`) that both VMs are using addresses in the 10.10.10.0/24 subnet and that they can ping each other by name.</span><span class="sxs-lookup"><span data-stu-id="578c6-162">Verify (by using `/sbin/ifconfig`) that both VMs are using addresses in the 10.10.10.0/24 subnet and that they can ping each other by name.</span></span> <span data-ttu-id="578c6-163">You can also use `ssh-keygen` and `ssh-copy-id` to make sure both VMs can communicate via SSH without requiring a password.</span><span class="sxs-lookup"><span data-stu-id="578c6-163">You can also use `ssh-keygen` and `ssh-copy-id` to make sure both VMs can communicate via SSH without requiring a password.</span></span>

### <a name="set-up-drbd"></a><span data-ttu-id="578c6-164">Set up DRBD</span><span class="sxs-lookup"><span data-stu-id="578c6-164">Set up DRBD</span></span>
<span data-ttu-id="578c6-165">Create a DRBD resource that uses the underlying `/dev/sdc1` partition to produce a `/dev/drbd1` resource that can be formatted by using ext3 and used in both primary and secondary nodes.</span><span class="sxs-lookup"><span data-stu-id="578c6-165">Create a DRBD resource that uses the underlying `/dev/sdc1` partition to produce a `/dev/drbd1` resource that can be formatted by using ext3 and used in both primary and secondary nodes.</span></span>

1. <span data-ttu-id="578c6-166">Open `/etc/drbd.d/r0.res` and copy the following resource definition on both VMs:</span><span class="sxs-lookup"><span data-stu-id="578c6-166">Open `/etc/drbd.d/r0.res` and copy the following resource definition on both VMs:</span></span>

        resource r0 {
          on `hadb01` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.4:7789;
            meta-disk internal;
          }
          on `hadb02` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.5:7789;
            meta-disk internal;
          }
        }

2. <span data-ttu-id="578c6-167">Initialize the resource by using `drbdadm` on both VMs:</span><span class="sxs-lookup"><span data-stu-id="578c6-167">Initialize the resource by using `drbdadm` on both VMs:</span></span>

        sudo drbdadm -c /etc/drbd.conf role r0
        sudo drbdadm up r0

3. <span data-ttu-id="578c6-168">On the primary VM (`hadb01`), force ownership (primary) of the DRBD resource:</span><span class="sxs-lookup"><span data-stu-id="578c6-168">On the primary VM (`hadb01`), force ownership (primary) of the DRBD resource:</span></span>

        sudo drbdadm primary --force r0

<span data-ttu-id="578c6-169">If you examine the contents of /proc/drbd (`sudo cat /proc/drbd`) on both VMs, you should see `Primary/Secondary` on `hadb01` and `Secondary/Primary` on `hadb02`, consistent with the solution at this point.</span><span class="sxs-lookup"><span data-stu-id="578c6-169">If you examine the contents of /proc/drbd (`sudo cat /proc/drbd`) on both VMs, you should see `Primary/Secondary` on `hadb01` and `Secondary/Primary` on `hadb02`, consistent with the solution at this point.</span></span> <span data-ttu-id="578c6-170">The 5-GB disk is synchronized over the 10.10.10.0/24 network at no charge to customers.</span><span class="sxs-lookup"><span data-stu-id="578c6-170">The 5-GB disk is synchronized over the 10.10.10.0/24 network at no charge to customers.</span></span>

<span data-ttu-id="578c6-171">After the disk is synchronized, you can create the file system on `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="578c6-171">After the disk is synchronized, you can create the file system on `hadb01`.</span></span> <span data-ttu-id="578c6-172">For testing purposes, we used ext2, but the following code will create an ext3 file system:</span><span class="sxs-lookup"><span data-stu-id="578c6-172">For testing purposes, we used ext2, but the following code will create an ext3 file system:</span></span>

    mkfs.ext3 /dev/drbd1

### <a name="mount-the-drbd-resource"></a><span data-ttu-id="578c6-173">Mount the DRBD resource</span><span class="sxs-lookup"><span data-stu-id="578c6-173">Mount the DRBD resource</span></span>
<span data-ttu-id="578c6-174">You're now ready to mount the DRBD resources on `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="578c6-174">You're now ready to mount the DRBD resources on `hadb01`.</span></span> <span data-ttu-id="578c6-175">Debian and derivatives use `/var/lib/mysql` as MySQL's data directory.</span><span class="sxs-lookup"><span data-stu-id="578c6-175">Debian and derivatives use `/var/lib/mysql` as MySQL's data directory.</span></span> <span data-ttu-id="578c6-176">Because you haven't installed MySQL, create the directory and mount the DRBD resource.</span><span class="sxs-lookup"><span data-stu-id="578c6-176">Because you haven't installed MySQL, create the directory and mount the DRBD resource.</span></span> <span data-ttu-id="578c6-177">To perform this option, run the following code on `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="578c6-177">To perform this option, run the following code on `hadb01`:</span></span>

    sudo mkdir /var/lib/mysql
    sudo mount /dev/drbd1 /var/lib/mysql

## <a name="set-up-mysql"></a><span data-ttu-id="578c6-178">Set up MySQL</span><span class="sxs-lookup"><span data-stu-id="578c6-178">Set up MySQL</span></span>
<span data-ttu-id="578c6-179">Now you're ready to install MySQL on `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="578c6-179">Now you're ready to install MySQL on `hadb01`:</span></span>

    sudo apt-get install mysql-server

<span data-ttu-id="578c6-180">For `hadb02`, you have two options.</span><span class="sxs-lookup"><span data-stu-id="578c6-180">For `hadb02`, you have two options.</span></span> <span data-ttu-id="578c6-181">You can install mysql-server, which will create /var/lib/mysql, fill it with a new data directory, and then remove the contents.</span><span class="sxs-lookup"><span data-stu-id="578c6-181">You can install mysql-server, which will create /var/lib/mysql, fill it with a new data directory, and then remove the contents.</span></span> <span data-ttu-id="578c6-182">To perform this option, run the following code on `hadb02`:</span><span class="sxs-lookup"><span data-stu-id="578c6-182">To perform this option, run the following code on `hadb02`:</span></span>

    sudo apt-get install mysql-server
    sudo service mysql stop
    sudo rm –rf /var/lib/mysql/*

<span data-ttu-id="578c6-183">The second option is to failover to `hadb02` and then install mysql-server there.</span><span class="sxs-lookup"><span data-stu-id="578c6-183">The second option is to failover to `hadb02` and then install mysql-server there.</span></span> <span data-ttu-id="578c6-184">Installation scripts will notice the existing installation and won't touch it.</span><span class="sxs-lookup"><span data-stu-id="578c6-184">Installation scripts will notice the existing installation and won't touch it.</span></span>

<span data-ttu-id="578c6-185">Run the following code on `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="578c6-185">Run the following code on `hadb01`:</span></span>

    sudo drbdadm secondary –force r0

<span data-ttu-id="578c6-186">Run the following code on `hadb02`:</span><span class="sxs-lookup"><span data-stu-id="578c6-186">Run the following code on `hadb02`:</span></span>

    sudo drbdadm primary –force r0
    sudo apt-get install mysql-server

<span data-ttu-id="578c6-187">If you don't plan to failover DRBD now, the first option is easier although arguably less elegant.</span><span class="sxs-lookup"><span data-stu-id="578c6-187">If you don't plan to failover DRBD now, the first option is easier although arguably less elegant.</span></span> <span data-ttu-id="578c6-188">After you set this up, you can start working on your MySQL database.</span><span class="sxs-lookup"><span data-stu-id="578c6-188">After you set this up, you can start working on your MySQL database.</span></span> <span data-ttu-id="578c6-189">Run the following code on `hadb02` (or whichever one of the servers is active, according to DRBD):</span><span class="sxs-lookup"><span data-stu-id="578c6-189">Run the following code on `hadb02` (or whichever one of the servers is active, according to DRBD):</span></span>

    mysql –u root –p
    CREATE DATABASE azureha;
    CREATE TABLE things ( id SERIAL, name VARCHAR(255) );
    INSERT INTO things VALUES (1, "Yet another entity");
    GRANT ALL ON things.\* TO root;

> [!WARNING]
> <span data-ttu-id="578c6-190">This last statement effectively disables authentication for the root user in this table.</span><span class="sxs-lookup"><span data-stu-id="578c6-190">This last statement effectively disables authentication for the root user in this table.</span></span> <span data-ttu-id="578c6-191">This should be replaced by your production-grade GRANT statements and is included only for illustrative purposes.</span><span class="sxs-lookup"><span data-stu-id="578c6-191">This should be replaced by your production-grade GRANT statements and is included only for illustrative purposes.</span></span>

<span data-ttu-id="578c6-192">If you want to make queries from outside the VMs (which is the purpose of this guide), you also need to enable networking for MySQL.</span><span class="sxs-lookup"><span data-stu-id="578c6-192">If you want to make queries from outside the VMs (which is the purpose of this guide), you also need to enable networking for MySQL.</span></span> <span data-ttu-id="578c6-193">On both VMs, open `/etc/mysql/my.cnf` and go to `bind-address`.</span><span class="sxs-lookup"><span data-stu-id="578c6-193">On both VMs, open `/etc/mysql/my.cnf` and go to `bind-address`.</span></span> <span data-ttu-id="578c6-194">Change the address from 127.0.0.1 to 0.0.0.0.</span><span class="sxs-lookup"><span data-stu-id="578c6-194">Change the address from 127.0.0.1 to 0.0.0.0.</span></span> <span data-ttu-id="578c6-195">After saving the file, issue a `sudo service mysql restart` on your current primary.</span><span class="sxs-lookup"><span data-stu-id="578c6-195">After saving the file, issue a `sudo service mysql restart` on your current primary.</span></span>

### <a name="create-the-mysql-load-balanced-set"></a><span data-ttu-id="578c6-196">Create the MySQL load-balanced set</span><span class="sxs-lookup"><span data-stu-id="578c6-196">Create the MySQL load-balanced set</span></span>
<span data-ttu-id="578c6-197">Go back to the portal, go to `hadb01`, and choose **Endpoints**.</span><span class="sxs-lookup"><span data-stu-id="578c6-197">Go back to the portal, go to `hadb01`, and choose **Endpoints**.</span></span> <span data-ttu-id="578c6-198">To create an endpoint, choose MySQL (TCP 3306) from the drop-down list and select **Create new load balanced set**.</span><span class="sxs-lookup"><span data-stu-id="578c6-198">To create an endpoint, choose MySQL (TCP 3306) from the drop-down list and select **Create new load balanced set**.</span></span> <span data-ttu-id="578c6-199">Name the load-balanced endpoint `lb-mysql`.</span><span class="sxs-lookup"><span data-stu-id="578c6-199">Name the load-balanced endpoint `lb-mysql`.</span></span> <span data-ttu-id="578c6-200">Set **Time** to 5 seconds, minimum.</span><span class="sxs-lookup"><span data-stu-id="578c6-200">Set **Time** to 5 seconds, minimum.</span></span>

<span data-ttu-id="578c6-201">After you create the endpoint, go to `hadb02`, choose **Endpoints**, and create an endpoint.</span><span class="sxs-lookup"><span data-stu-id="578c6-201">After you create the endpoint, go to `hadb02`, choose **Endpoints**, and create an endpoint.</span></span> <span data-ttu-id="578c6-202">Choose `lb-mysql`, and then select MySQL from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="578c6-202">Choose `lb-mysql`, and then select MySQL from the drop-down list.</span></span> <span data-ttu-id="578c6-203">You can also use the Azure CLI for this step.</span><span class="sxs-lookup"><span data-stu-id="578c6-203">You can also use the Azure CLI for this step.</span></span>

<span data-ttu-id="578c6-204">You now have everything you need for manual operation of the cluster.</span><span class="sxs-lookup"><span data-stu-id="578c6-204">You now have everything you need for manual operation of the cluster.</span></span>

### <a name="test-the-load-balanced-set"></a><span data-ttu-id="578c6-205">Test the load-balanced set</span><span class="sxs-lookup"><span data-stu-id="578c6-205">Test the load-balanced set</span></span>
<span data-ttu-id="578c6-206">Tests can be performed from an outside machine by using any MySQL client, or by using certain applications, like phpMyAdmin running as an Azure website.</span><span class="sxs-lookup"><span data-stu-id="578c6-206">Tests can be performed from an outside machine by using any MySQL client, or by using certain applications, like phpMyAdmin running as an Azure website.</span></span> <span data-ttu-id="578c6-207">In this case, you used MySQL's command-line tool on another Linux box:</span><span class="sxs-lookup"><span data-stu-id="578c6-207">In this case, you used MySQL's command-line tool on another Linux box:</span></span>

    mysql azureha –u root –h hadb.cloudapp.net –e "select * from things;"

### <a name="manually-failing-over"></a><span data-ttu-id="578c6-208">Manually failing over</span><span class="sxs-lookup"><span data-stu-id="578c6-208">Manually failing over</span></span>
<span data-ttu-id="578c6-209">You can simulate failovers by shutting down MySQL, switching DRBD's primary, and starting MySQL again.</span><span class="sxs-lookup"><span data-stu-id="578c6-209">You can simulate failovers by shutting down MySQL, switching DRBD's primary, and starting MySQL again.</span></span>

<span data-ttu-id="578c6-210">To perform this task, run the following code on hadb01:</span><span class="sxs-lookup"><span data-stu-id="578c6-210">To perform this task, run the following code on hadb01:</span></span>

    service mysql stop && umount /var/lib/mysql ; drbdadm secondary r0

<span data-ttu-id="578c6-211">Then, on hadb02:</span><span class="sxs-lookup"><span data-stu-id="578c6-211">Then, on hadb02:</span></span>

    drbdadm primary r0 ; mount /dev/drbd1 /var/lib/mysql && service mysql start

<span data-ttu-id="578c6-212">After you fail over manually, you can repeat your remote query and it should work perfectly.</span><span class="sxs-lookup"><span data-stu-id="578c6-212">After you fail over manually, you can repeat your remote query and it should work perfectly.</span></span>

## <a name="set-up-corosync"></a><span data-ttu-id="578c6-213">Set up Corosync</span><span class="sxs-lookup"><span data-stu-id="578c6-213">Set up Corosync</span></span>
<span data-ttu-id="578c6-214">Corosync is the underlying cluster infrastructure required for Pacemaker to work.</span><span class="sxs-lookup"><span data-stu-id="578c6-214">Corosync is the underlying cluster infrastructure required for Pacemaker to work.</span></span> <span data-ttu-id="578c6-215">For Heartbeat (and other methodologies like Ultramonkey), Corosync is a split of the CRM functionalities, while Pacemaker remains more similar to Heartbeat in functionality.</span><span class="sxs-lookup"><span data-stu-id="578c6-215">For Heartbeat (and other methodologies like Ultramonkey), Corosync is a split of the CRM functionalities, while Pacemaker remains more similar to Heartbeat in functionality.</span></span>

<span data-ttu-id="578c6-216">The main constraint for Corosync on Azure is that Corosync prefers multicast over broadcast over unicast communications, but Microsoft Azure networking only supports unicast.</span><span class="sxs-lookup"><span data-stu-id="578c6-216">The main constraint for Corosync on Azure is that Corosync prefers multicast over broadcast over unicast communications, but Microsoft Azure networking only supports unicast.</span></span>

<span data-ttu-id="578c6-217">Fortunately, Corosync has a working unicast mode.</span><span class="sxs-lookup"><span data-stu-id="578c6-217">Fortunately, Corosync has a working unicast mode.</span></span> <span data-ttu-id="578c6-218">The only real constraint is that because all nodes are not communicating among themselves, you need to define the nodes in your configuration files, including their IP addresses.</span><span class="sxs-lookup"><span data-stu-id="578c6-218">The only real constraint is that because all nodes are not communicating among themselves, you need to define the nodes in your configuration files, including their IP addresses.</span></span> <span data-ttu-id="578c6-219">We can use the Corosync example files for Unicast and change bind address, node lists, and logging directories (Ubuntu uses `/var/log/corosync` while the example files use `/var/log/cluster`), and enable quorum tools.</span><span class="sxs-lookup"><span data-stu-id="578c6-219">We can use the Corosync example files for Unicast and change bind address, node lists, and logging directories (Ubuntu uses `/var/log/corosync` while the example files use `/var/log/cluster`), and enable quorum tools.</span></span>

> [!NOTE]
> <span data-ttu-id="578c6-220">Use the following `transport: udpu` directive and the manually defined IP addresses for both nodes.</span><span class="sxs-lookup"><span data-stu-id="578c6-220">Use the following `transport: udpu` directive and the manually defined IP addresses for both nodes.</span></span>

<span data-ttu-id="578c6-221">Run the following code on `/etc/corosync/corosync.conf` for both nodes:</span><span class="sxs-lookup"><span data-stu-id="578c6-221">Run the following code on `/etc/corosync/corosync.conf` for both nodes:</span></span>

    totem {
      version: 2
      crypto_cipher: none
      crypto_hash: none
      interface {
        ringnumber: 0
        bindnetaddr: 10.10.10.0
        mcastport: 5405
        ttl: 1
      }
      transport: udpu
    }

    logging {
      fileline: off
      to_logfile: yes
      to_syslog: yes
      logfile: /var/log/corosync/corosync.log
      debug: off
      timestamp: on
      logger_subsys {
        subsys: QUORUM
        debug: off
        }
      }

    nodelist {
      node {
        ring0_addr: 10.10.10.4
        nodeid: 1
      }

      node {
        ring0_addr: 10.10.10.5
        nodeid: 2
      }
    }

    quorum {
      provider: corosync_votequorum
    }

<span data-ttu-id="578c6-222">Copy this configuration file on both VMs and start Corosync in both nodes:</span><span class="sxs-lookup"><span data-stu-id="578c6-222">Copy this configuration file on both VMs and start Corosync in both nodes:</span></span>

    sudo service start corosync

<span data-ttu-id="578c6-223">Shortly after starting the service, the cluster should be established in the current ring, and quorum should be constituted.</span><span class="sxs-lookup"><span data-stu-id="578c6-223">Shortly after starting the service, the cluster should be established in the current ring, and quorum should be constituted.</span></span> <span data-ttu-id="578c6-224">We can check this functionality by reviewing logs or by running the following code:</span><span class="sxs-lookup"><span data-stu-id="578c6-224">We can check this functionality by reviewing logs or by running the following code:</span></span>

    sudo corosync-quorumtool –l

<span data-ttu-id="578c6-225">You will see output similar to the following image:</span><span class="sxs-lookup"><span data-stu-id="578c6-225">You will see output similar to the following image:</span></span>

![corosync-quorumtool -l sample output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/mysql-cluster/image001.png)

## <a name="set-up-pacemaker"></a><span data-ttu-id="578c6-227">Set up Pacemaker</span><span class="sxs-lookup"><span data-stu-id="578c6-227">Set up Pacemaker</span></span>
<span data-ttu-id="578c6-228">Pacemaker uses the cluster to monitor for resources, define when primaries go down, and switch those resources to secondaries.</span><span class="sxs-lookup"><span data-stu-id="578c6-228">Pacemaker uses the cluster to monitor for resources, define when primaries go down, and switch those resources to secondaries.</span></span> <span data-ttu-id="578c6-229">Resources can be defined from a set of available scripts or from LSB (init-like) scripts, among other choices.</span><span class="sxs-lookup"><span data-stu-id="578c6-229">Resources can be defined from a set of available scripts or from LSB (init-like) scripts, among other choices.</span></span>

<span data-ttu-id="578c6-230">We want Pacemaker to "own" the DRBD resource, the mount point, and the MySQL service.</span><span class="sxs-lookup"><span data-stu-id="578c6-230">We want Pacemaker to "own" the DRBD resource, the mount point, and the MySQL service.</span></span> <span data-ttu-id="578c6-231">If Pacemaker can turn on and off DRBD, mount and unmount it, and then start and stop MySQL in the right order when something bad happens with the primary, setup is complete.</span><span class="sxs-lookup"><span data-stu-id="578c6-231">If Pacemaker can turn on and off DRBD, mount and unmount it, and then start and stop MySQL in the right order when something bad happens with the primary, setup is complete.</span></span>

<span data-ttu-id="578c6-232">When you first install Pacemaker, your configuration should be simple enough, something like:</span><span class="sxs-lookup"><span data-stu-id="578c6-232">When you first install Pacemaker, your configuration should be simple enough, something like:</span></span>

    node $id="1" hadb01
      attributes standby="off"
    node $id="2" hadb02
      attributes standby="off"

1. <span data-ttu-id="578c6-233">Check the configuration by running `sudo crm configure show`.</span><span class="sxs-lookup"><span data-stu-id="578c6-233">Check the configuration by running `sudo crm configure show`.</span></span>
2. <span data-ttu-id="578c6-234">Then create a file (like `/tmp/cluster.conf`) with the following resources:</span><span class="sxs-lookup"><span data-stu-id="578c6-234">Then create a file (like `/tmp/cluster.conf`) with the following resources:</span></span>

        primitive drbd_mysql ocf:linbit:drbd \
              params drbd_resource="r0" \
              op monitor interval="29s" role="Master" \
              op monitor interval="31s" role="Slave"

        ms ms_drbd_mysql drbd_mysql \
              meta master-max="1" master-node-max="1" \
                clone-max="2" clone-node-max="1" \
                notify="true"

        primitive fs_mysql ocf:heartbeat:Filesystem \
              params device="/dev/drbd/by-res/r0" \
              directory="/var/lib/mysql" fstype="ext3"

        primitive mysqld lsb:mysql

        group mysql fs_mysql mysqld

        colocation mysql_on_drbd \
               inf: mysql ms_drbd_mysql:Master

        order mysql_after_drbd \
               inf: ms_drbd_mysql:promote mysql:start

        property stonith-enabled=false

        property no-quorum-policy=ignore

3. <span data-ttu-id="578c6-235">Load the file into the configuration.</span><span class="sxs-lookup"><span data-stu-id="578c6-235">Load the file into the configuration.</span></span> <span data-ttu-id="578c6-236">You only need to do this in one node.</span><span class="sxs-lookup"><span data-stu-id="578c6-236">You only need to do this in one node.</span></span>

        sudo crm configure
          load update /tmp/cluster.conf
          commit
          exit

4. <span data-ttu-id="578c6-237">Make sure that Pacemaker starts at boot in both nodes:</span><span class="sxs-lookup"><span data-stu-id="578c6-237">Make sure that Pacemaker starts at boot in both nodes:</span></span>

        sudo update-rc.d pacemaker defaults

5. <span data-ttu-id="578c6-238">By using `sudo crm_mon –L`, verify that one of your nodes has become the master for the cluster and is running all the resources.</span><span class="sxs-lookup"><span data-stu-id="578c6-238">By using `sudo crm_mon –L`, verify that one of your nodes has become the master for the cluster and is running all the resources.</span></span> <span data-ttu-id="578c6-239">You can use mount and ps to check that the resources are running.</span><span class="sxs-lookup"><span data-stu-id="578c6-239">You can use mount and ps to check that the resources are running.</span></span>

<span data-ttu-id="578c6-240">The following screenshot shows `crm_mon` with one node stopped (exit by selecting Ctrl+C):</span><span class="sxs-lookup"><span data-stu-id="578c6-240">The following screenshot shows `crm_mon` with one node stopped (exit by selecting Ctrl+C):</span></span>

![crm_mon node stopped](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/mysql-cluster/image002.png)

<span data-ttu-id="578c6-242">This screenshot shows both nodes, one master and one slave:</span><span class="sxs-lookup"><span data-stu-id="578c6-242">This screenshot shows both nodes, one master and one slave:</span></span>

![crm_mon operational master/slave](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/mysql-cluster/image003.png)

## <a name="testing"></a><span data-ttu-id="578c6-244">Testing</span><span class="sxs-lookup"><span data-stu-id="578c6-244">Testing</span></span>
<span data-ttu-id="578c6-245">You're ready for an automatic failover simulation.</span><span class="sxs-lookup"><span data-stu-id="578c6-245">You're ready for an automatic failover simulation.</span></span> <span data-ttu-id="578c6-246">There are two ways to do this: soft and hard.</span><span class="sxs-lookup"><span data-stu-id="578c6-246">There are two ways to do this: soft and hard.</span></span>

<span data-ttu-id="578c6-247">The soft way uses the cluster's shutdown function: ``crm_standby -U `uname -n` -v on``.</span><span class="sxs-lookup"><span data-stu-id="578c6-247">The soft way uses the cluster's shutdown function: ``crm_standby -U `uname -n` -v on``.</span></span> <span data-ttu-id="578c6-248">If you use this on the master, the slave takes over.</span><span class="sxs-lookup"><span data-stu-id="578c6-248">If you use this on the master, the slave takes over.</span></span> <span data-ttu-id="578c6-249">Remember to set this back to off.</span><span class="sxs-lookup"><span data-stu-id="578c6-249">Remember to set this back to off.</span></span> <span data-ttu-id="578c6-250">If you don't, crm_mon will show one node on standby.</span><span class="sxs-lookup"><span data-stu-id="578c6-250">If you don't, crm_mon will show one node on standby.</span></span>

<span data-ttu-id="578c6-251">The hard way is shutting down the primary VM (hadb01) via the portal or by changing the runlevel on the VM (that is, halt, shutdown).</span><span class="sxs-lookup"><span data-stu-id="578c6-251">The hard way is shutting down the primary VM (hadb01) via the portal or by changing the runlevel on the VM (that is, halt, shutdown).</span></span> <span data-ttu-id="578c6-252">This helps Corosync and Pacemaker by signaling that the master's going down.</span><span class="sxs-lookup"><span data-stu-id="578c6-252">This helps Corosync and Pacemaker by signaling that the master's going down.</span></span> <span data-ttu-id="578c6-253">You can test this (useful for maintenance windows), but you can also force the scenario by freezing the VM.</span><span class="sxs-lookup"><span data-stu-id="578c6-253">You can test this (useful for maintenance windows), but you can also force the scenario by freezing the VM.</span></span>

## <a name="stonith"></a><span data-ttu-id="578c6-254">STONITH</span><span class="sxs-lookup"><span data-stu-id="578c6-254">STONITH</span></span>
<span data-ttu-id="578c6-255">It should be possible to issue a VM shutdown via the Azure CLI in lieu of a STONITH script that controls a physical device.</span><span class="sxs-lookup"><span data-stu-id="578c6-255">It should be possible to issue a VM shutdown via the Azure CLI in lieu of a STONITH script that controls a physical device.</span></span> <span data-ttu-id="578c6-256">You can use `/usr/lib/stonith/plugins/external/ssh` as a base and enable STONITH in the cluster's configuration.</span><span class="sxs-lookup"><span data-stu-id="578c6-256">You can use `/usr/lib/stonith/plugins/external/ssh` as a base and enable STONITH in the cluster's configuration.</span></span> <span data-ttu-id="578c6-257">Azure CLI should be globally installed, and the publish settings and profile should be loaded for the cluster's user.</span><span class="sxs-lookup"><span data-stu-id="578c6-257">Azure CLI should be globally installed, and the publish settings and profile should be loaded for the cluster's user.</span></span>

<span data-ttu-id="578c6-258">Sample code for the resource is available on [GitHub](https://github.com/bureado/aztonith).</span><span class="sxs-lookup"><span data-stu-id="578c6-258">Sample code for the resource is available on [GitHub](https://github.com/bureado/aztonith).</span></span> <span data-ttu-id="578c6-259">Change the cluster's configuration by adding the following to `sudo crm configure`:</span><span class="sxs-lookup"><span data-stu-id="578c6-259">Change the cluster's configuration by adding the following to `sudo crm configure`:</span></span>

    primitive st-azure stonith:external/azure \
      params hostlist="hadb01 hadb02" \
      clone fencing st-azure \
      property stonith-enabled=true \
      commit

> [!NOTE]
> <span data-ttu-id="578c6-260">The script doesn't perform up/down checks.</span><span class="sxs-lookup"><span data-stu-id="578c6-260">The script doesn't perform up/down checks.</span></span> <span data-ttu-id="578c6-261">The original SSH resource had 15 ping checks, but recovery time for an Azure VM might be more variable.</span><span class="sxs-lookup"><span data-stu-id="578c6-261">The original SSH resource had 15 ping checks, but recovery time for an Azure VM might be more variable.</span></span>

## <a name="limitations"></a><span data-ttu-id="578c6-262">Limitations</span><span class="sxs-lookup"><span data-stu-id="578c6-262">Limitations</span></span>
<span data-ttu-id="578c6-263">The following limitations apply:</span><span class="sxs-lookup"><span data-stu-id="578c6-263">The following limitations apply:</span></span>

* <span data-ttu-id="578c6-264">The linbit DRBD resource script that manages DRBD as a resource in Pacemaker uses `drbdadm down` when shutting down a node, even if the node is just going on standby.</span><span class="sxs-lookup"><span data-stu-id="578c6-264">The linbit DRBD resource script that manages DRBD as a resource in Pacemaker uses `drbdadm down` when shutting down a node, even if the node is just going on standby.</span></span> <span data-ttu-id="578c6-265">This is not ideal because the slave will not be synchronizing the DRBD resource while the master gets writes.</span><span class="sxs-lookup"><span data-stu-id="578c6-265">This is not ideal because the slave will not be synchronizing the DRBD resource while the master gets writes.</span></span> <span data-ttu-id="578c6-266">If the master does not fail graciously, the slave can take over an older file system state.</span><span class="sxs-lookup"><span data-stu-id="578c6-266">If the master does not fail graciously, the slave can take over an older file system state.</span></span> <span data-ttu-id="578c6-267">There are two potential ways of solving this:</span><span class="sxs-lookup"><span data-stu-id="578c6-267">There are two potential ways of solving this:</span></span>
  * <span data-ttu-id="578c6-268">Enforcing a `drbdadm up r0` in all cluster nodes via a local (not clusterized) watchdog</span><span class="sxs-lookup"><span data-stu-id="578c6-268">Enforcing a `drbdadm up r0` in all cluster nodes via a local (not clusterized) watchdog</span></span>
  * <span data-ttu-id="578c6-269">Editing the linbit DRBD script, making sure that `down` is not called in `/usr/lib/ocf/resource.d/linbit/drbd`</span><span class="sxs-lookup"><span data-stu-id="578c6-269">Editing the linbit DRBD script, making sure that `down` is not called in `/usr/lib/ocf/resource.d/linbit/drbd`</span></span>
* <span data-ttu-id="578c6-270">The load balancer needs at least five seconds to respond, so applications should be cluster-aware and be more tolerant of timeout.</span><span class="sxs-lookup"><span data-stu-id="578c6-270">The load balancer needs at least five seconds to respond, so applications should be cluster-aware and be more tolerant of timeout.</span></span> <span data-ttu-id="578c6-271">Other architectures, like in-app queues and query middlewares, can also help.</span><span class="sxs-lookup"><span data-stu-id="578c6-271">Other architectures, like in-app queues and query middlewares, can also help.</span></span>
* <span data-ttu-id="578c6-272">MySQL tuning is necessary to ensure that writing is done at a manageable pace and caches are flushed to disk as frequently as possible to minimize memory loss.</span><span class="sxs-lookup"><span data-stu-id="578c6-272">MySQL tuning is necessary to ensure that writing is done at a manageable pace and caches are flushed to disk as frequently as possible to minimize memory loss.</span></span>
* <span data-ttu-id="578c6-273">Write performance is dependent in VM interconnect in the virtual switch because this is the mechanism used by DRBD to replicate the device.</span><span class="sxs-lookup"><span data-stu-id="578c6-273">Write performance is dependent in VM interconnect in the virtual switch because this is the mechanism used by DRBD to replicate the device.</span></span>



