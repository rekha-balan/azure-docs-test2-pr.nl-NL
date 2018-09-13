---
title: Run a MariaDB (MySQL) cluster on Azure | Microsoft Docs
description: Create a MariaDB + Galera MySQL cluster on Azure virtual machines
services: virtual-machines-linux
documentationcenter: ''
author: sabbour
manager: timlt
editor: ''
tags: azure-service-management
ms.assetid: d0d21937-7aac-4222-8255-2fdc4f2ea65b
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/15/2015
ms.author: asabbour
ms.openlocfilehash: bbeeb35ee18323c6e288789e6230c88f3d8f8127
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44672067"
---
# <a name="mariadb-mysql-cluster-azure-tutorial"></a><span data-ttu-id="72cc6-103">MariaDB (MySQL) cluster: Azure tutorial</span><span class="sxs-lookup"><span data-stu-id="72cc6-103">MariaDB (MySQL) cluster: Azure tutorial</span></span>
> [!IMPORTANT]
> <span data-ttu-id="72cc6-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span><span class="sxs-lookup"><span data-stu-id="72cc6-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="72cc6-105">This article covers the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="72cc6-105">This article covers the classic deployment model.</span></span> <span data-ttu-id="72cc6-106">Microsoft recommends that most new deployments use the Azure Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="72cc6-106">Microsoft recommends that most new deployments use the Azure Resource Manager model.</span></span>

> [!NOTE]
> <span data-ttu-id="72cc6-107">MariaDB Enterprise cluster is now available in the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="72cc6-107">MariaDB Enterprise cluster is now available in the Azure Marketplace.</span></span> <span data-ttu-id="72cc6-108">The new offering will automatically deploy a MariaDB Galera cluster on Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="72cc6-108">The new offering will automatically deploy a MariaDB Galera cluster on Azure Resource Manager.</span></span> <span data-ttu-id="72cc6-109">You should use the new offering from [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).</span><span class="sxs-lookup"><span data-stu-id="72cc6-109">You should use the new offering from [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).</span></span>
>
>

<span data-ttu-id="72cc6-110">This article shows you how to create a multi-Master [Galera](http://galeracluster.com/products/) cluster of [MariaDBs](https://mariadb.org/en/about/) (a robust, scalable, and reliable drop-in replacement for MySQL) to work in a highly available environment on Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="72cc6-110">This article shows you how to create a multi-Master [Galera](http://galeracluster.com/products/) cluster of [MariaDBs](https://mariadb.org/en/about/) (a robust, scalable, and reliable drop-in replacement for MySQL) to work in a highly available environment on Azure virtual machines.</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="72cc6-111">Architecture overview</span><span class="sxs-lookup"><span data-stu-id="72cc6-111">Architecture overview</span></span>
<span data-ttu-id="72cc6-112">This article describes how to complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="72cc6-112">This article describes how to complete the following steps:</span></span>

- <span data-ttu-id="72cc6-113">Create a three-node cluster.</span><span class="sxs-lookup"><span data-stu-id="72cc6-113">Create a three-node cluster.</span></span>
- <span data-ttu-id="72cc6-114">Separate the data disks from the OS disk.</span><span class="sxs-lookup"><span data-stu-id="72cc6-114">Separate the data disks from the OS disk.</span></span>
- <span data-ttu-id="72cc6-115">Create the data disks in RAID-0/striped setting to increase IOPS.</span><span class="sxs-lookup"><span data-stu-id="72cc6-115">Create the data disks in RAID-0/striped setting to increase IOPS.</span></span>
- <span data-ttu-id="72cc6-116">Use Azure Load Balancer to balance the load for the three nodes.</span><span class="sxs-lookup"><span data-stu-id="72cc6-116">Use Azure Load Balancer to balance the load for the three nodes.</span></span>
- <span data-ttu-id="72cc6-117">To minimize repetitive work, create a VM image that contains MariaDB + Galera and use it to create the other cluster VMs.</span><span class="sxs-lookup"><span data-stu-id="72cc6-117">To minimize repetitive work, create a VM image that contains MariaDB + Galera and use it to create the other cluster VMs.</span></span>

![System architecture](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/mariadb-mysql-cluster/setup.png)

> [!NOTE]
> <span data-ttu-id="72cc6-119">This topic uses the [Azure CLI](../../../cli-install-nodejs.md) tools, so make sure to download them and connect them to your Azure subscription according to the instructions.</span><span class="sxs-lookup"><span data-stu-id="72cc6-119">This topic uses the [Azure CLI](../../../cli-install-nodejs.md) tools, so make sure to download them and connect them to your Azure subscription according to the instructions.</span></span> <span data-ttu-id="72cc6-120">If you need a reference to the commands available in the Azure CLI, see the [Azure CLI command reference](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="72cc6-120">If you need a reference to the commands available in the Azure CLI, see the [Azure CLI command reference](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="72cc6-121">You will also need to [create an SSH key for authentication] and make note of the .pem file location.</span><span class="sxs-lookup"><span data-stu-id="72cc6-121">You will also need to [create an SSH key for authentication] and make note of the .pem file location.</span></span>
>
>

## <a name="create-the-template"></a><span data-ttu-id="72cc6-122">Create the template</span><span class="sxs-lookup"><span data-stu-id="72cc6-122">Create the template</span></span>
### <a name="infrastructure"></a><span data-ttu-id="72cc6-123">Infrastructure</span><span class="sxs-lookup"><span data-stu-id="72cc6-123">Infrastructure</span></span>
1. <span data-ttu-id="72cc6-124">Create an affinity group to hold the resources together.</span><span class="sxs-lookup"><span data-stu-id="72cc6-124">Create an affinity group to hold the resources together.</span></span>

        azure account affinity-group create mariadbcluster --location "North Europe" --label "MariaDB Cluster"
2. <span data-ttu-id="72cc6-125">Create a virtual network.</span><span class="sxs-lookup"><span data-stu-id="72cc6-125">Create a virtual network.</span></span>

        azure network vnet create --address-space 10.0.0.0 --cidr 8 --subnet-name mariadb --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --affinity-group mariadbcluster mariadbvnet
3. <span data-ttu-id="72cc6-126">Create a storage account to host all our disks.</span><span class="sxs-lookup"><span data-stu-id="72cc6-126">Create a storage account to host all our disks.</span></span> <span data-ttu-id="72cc6-127">You shouldn't place more than 40 heavily used disks on the same storage account to avoid hitting the 20,000 IOPS storage account limit.</span><span class="sxs-lookup"><span data-stu-id="72cc6-127">You shouldn't place more than 40 heavily used disks on the same storage account to avoid hitting the 20,000 IOPS storage account limit.</span></span> <span data-ttu-id="72cc6-128">In this case, you're well below that limit, so you'll store everything on the same account for simplicity.</span><span class="sxs-lookup"><span data-stu-id="72cc6-128">In this case, you're well below that limit, so you'll store everything on the same account for simplicity.</span></span>

        azure storage account create mariadbstorage --label mariadbstorage --affinity-group mariadbcluster
4. <span data-ttu-id="72cc6-129">Find the name of the CentOS 7 virtual machine image.</span><span class="sxs-lookup"><span data-stu-id="72cc6-129">Find the name of the CentOS 7 virtual machine image.</span></span>

        azure vm image list | findstr CentOS
   <span data-ttu-id="72cc6-130">The output will be something like `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.</span><span class="sxs-lookup"><span data-stu-id="72cc6-130">The output will be something like `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.</span></span>

   <span data-ttu-id="72cc6-131">Use that name in the following step.</span><span class="sxs-lookup"><span data-stu-id="72cc6-131">Use that name in the following step.</span></span>
5. <span data-ttu-id="72cc6-132">Create the VM template and replace /path/to/key.pem with the path where you stored the generated .pem SSH key.</span><span class="sxs-lookup"><span data-stu-id="72cc6-132">Create the VM template and replace /path/to/key.pem with the path where you stored the generated .pem SSH key.</span></span>

        azure vm create --virtual-network-name mariadbvnet --subnet-names mariadb --blob-url "http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-os.vhd"  --vm-size Medium --ssh 22 --ssh-cert "/path/to/key.pem" --no-ssh-password mariadbtemplate 5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926 azureuser
6. <span data-ttu-id="72cc6-133">Attach four 500-GB data disks to the VM for use in the RAID configuration.</span><span class="sxs-lookup"><span data-stu-id="72cc6-133">Attach four 500-GB data disks to the VM for use in the RAID configuration.</span></span>

        FOR /L %d IN (1,1,4) DO azure vm disk attach-new mariadbhatemplate 512 http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-data-%d.vhd
7. <span data-ttu-id="72cc6-134">Use SSH to sign in to the template VM that you created at mariadbhatemplate.cloudapp.net:22, and connect by using your private key.</span><span class="sxs-lookup"><span data-stu-id="72cc6-134">Use SSH to sign in to the template VM that you created at mariadbhatemplate.cloudapp.net:22, and connect by using your private key.</span></span>

### <a name="software"></a><span data-ttu-id="72cc6-135">Software</span><span class="sxs-lookup"><span data-stu-id="72cc6-135">Software</span></span>
1. <span data-ttu-id="72cc6-136">Get the root.</span><span class="sxs-lookup"><span data-stu-id="72cc6-136">Get the root.</span></span>

        sudo su

2. <span data-ttu-id="72cc6-137">Install RAID support:</span><span class="sxs-lookup"><span data-stu-id="72cc6-137">Install RAID support:</span></span>

    <span data-ttu-id="72cc6-138">a.</span><span class="sxs-lookup"><span data-stu-id="72cc6-138">a.</span></span> <span data-ttu-id="72cc6-139">Install mdadm.</span><span class="sxs-lookup"><span data-stu-id="72cc6-139">Install mdadm.</span></span>

              yum install mdadm

    <span data-ttu-id="72cc6-140">b.</span><span class="sxs-lookup"><span data-stu-id="72cc6-140">b.</span></span> <span data-ttu-id="72cc6-141">Create the RAID0/stripe configuration with an EXT4 file system.</span><span class="sxs-lookup"><span data-stu-id="72cc6-141">Create the RAID0/stripe configuration with an EXT4 file system.</span></span>

              mdadm --create --verbose /dev/md0 --level=stripe --raid-devices=4 /dev/sdc /dev/sdd /dev/sde /dev/sdf
              mdadm --detail --scan >> /etc/mdadm.conf
              mkfs -t ext4 /dev/md0
    <span data-ttu-id="72cc6-142">c.</span><span class="sxs-lookup"><span data-stu-id="72cc6-142">c.</span></span> <span data-ttu-id="72cc6-143">Create the mount point directory.</span><span class="sxs-lookup"><span data-stu-id="72cc6-143">Create the mount point directory.</span></span>

              mkdir /mnt/data
    <span data-ttu-id="72cc6-144">d.</span><span class="sxs-lookup"><span data-stu-id="72cc6-144">d.</span></span> <span data-ttu-id="72cc6-145">Retrieve the UUID of the newly created RAID device.</span><span class="sxs-lookup"><span data-stu-id="72cc6-145">Retrieve the UUID of the newly created RAID device.</span></span>

              blkid | grep /dev/md0
    <span data-ttu-id="72cc6-146">e.</span><span class="sxs-lookup"><span data-stu-id="72cc6-146">e.</span></span> <span data-ttu-id="72cc6-147">Edit /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="72cc6-147">Edit /etc/fstab.</span></span>

              vi /etc/fstab
    <span data-ttu-id="72cc6-148">f.</span><span class="sxs-lookup"><span data-stu-id="72cc6-148">f.</span></span> <span data-ttu-id="72cc6-149">Add the device to enable auto mounting on reboot, replacing the UUID with the value obtained from the previous **blkid** command.</span><span class="sxs-lookup"><span data-stu-id="72cc6-149">Add the device to enable auto mounting on reboot, replacing the UUID with the value obtained from the previous **blkid** command.</span></span>

              UUID=<UUID FROM PREVIOUS>   /mnt/data ext4   defaults,noatime   1 2
    <span data-ttu-id="72cc6-150">g.</span><span class="sxs-lookup"><span data-stu-id="72cc6-150">g.</span></span> <span data-ttu-id="72cc6-151">Mount the new partition.</span><span class="sxs-lookup"><span data-stu-id="72cc6-151">Mount the new partition.</span></span>

              mount /mnt/data

3. <span data-ttu-id="72cc6-152">Install MariaDB.</span><span class="sxs-lookup"><span data-stu-id="72cc6-152">Install MariaDB.</span></span>

    <span data-ttu-id="72cc6-153">a.</span><span class="sxs-lookup"><span data-stu-id="72cc6-153">a.</span></span> <span data-ttu-id="72cc6-154">Create the MariaDB.repo file.</span><span class="sxs-lookup"><span data-stu-id="72cc6-154">Create the MariaDB.repo file.</span></span>

                vi /etc/yum.repos.d/MariaDB.repo

    <span data-ttu-id="72cc6-155">b.</span><span class="sxs-lookup"><span data-stu-id="72cc6-155">b.</span></span> <span data-ttu-id="72cc6-156">Fill the repo file with the following content:</span><span class="sxs-lookup"><span data-stu-id="72cc6-156">Fill the repo file with the following content:</span></span>

              [mariadb]
              name = MariaDB
              baseurl = http://yum.mariadb.org/10.0/centos7-amd64
              gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
              gpgcheck=1
    <span data-ttu-id="72cc6-157">c.</span><span class="sxs-lookup"><span data-stu-id="72cc6-157">c.</span></span> <span data-ttu-id="72cc6-158">To avoid conflicts, remove existing postfix and mariadb-libs.</span><span class="sxs-lookup"><span data-stu-id="72cc6-158">To avoid conflicts, remove existing postfix and mariadb-libs.</span></span>

           yum remove postfix mariadb-libs-*
    <span data-ttu-id="72cc6-159">d.</span><span class="sxs-lookup"><span data-stu-id="72cc6-159">d.</span></span> <span data-ttu-id="72cc6-160">Install MariaDB with Galera.</span><span class="sxs-lookup"><span data-stu-id="72cc6-160">Install MariaDB with Galera.</span></span>

           yum install MariaDB-Galera-server MariaDB-client galera

4. <span data-ttu-id="72cc6-161">Move the MySQL data directory to the RAID block device.</span><span class="sxs-lookup"><span data-stu-id="72cc6-161">Move the MySQL data directory to the RAID block device.</span></span>

    <span data-ttu-id="72cc6-162">a.</span><span class="sxs-lookup"><span data-stu-id="72cc6-162">a.</span></span> <span data-ttu-id="72cc6-163">Copy the current MySQL directory into its new location and remove the old directory.</span><span class="sxs-lookup"><span data-stu-id="72cc6-163">Copy the current MySQL directory into its new location and remove the old directory.</span></span>

           cp -avr /var/lib/mysql /mnt/data  
           rm -rf /var/lib/mysql
    <span data-ttu-id="72cc6-164">b.</span><span class="sxs-lookup"><span data-stu-id="72cc6-164">b.</span></span> <span data-ttu-id="72cc6-165">Set permissions for the new directory accordingly.</span><span class="sxs-lookup"><span data-stu-id="72cc6-165">Set permissions for the new directory accordingly.</span></span>

           chown -R mysql:mysql /mnt/data && chmod -R 755 /mnt/data/

    <span data-ttu-id="72cc6-166">c.</span><span class="sxs-lookup"><span data-stu-id="72cc6-166">c.</span></span> <span data-ttu-id="72cc6-167">Create a symlink that points the old directory to the new location on the RAID partition.</span><span class="sxs-lookup"><span data-stu-id="72cc6-167">Create a symlink that points the old directory to the new location on the RAID partition.</span></span>

           ln -s /mnt/data/mysql /var/lib/mysql

5. <span data-ttu-id="72cc6-168">Because [SELinux interferes with the cluster operations](http://galeracluster.com/documentation-webpages/configuration.html#selinux), it is necessary to disable it for the current session.</span><span class="sxs-lookup"><span data-stu-id="72cc6-168">Because [SELinux interferes with the cluster operations](http://galeracluster.com/documentation-webpages/configuration.html#selinux), it is necessary to disable it for the current session.</span></span> <span data-ttu-id="72cc6-169">Edit `/etc/selinux/config` to disable it for subsequent restarts.</span><span class="sxs-lookup"><span data-stu-id="72cc6-169">Edit `/etc/selinux/config` to disable it for subsequent restarts.</span></span>

            setenforce 0

            then editing `/etc/selinux/config` to set `SELINUX=permissive`
6. <span data-ttu-id="72cc6-170">Validate MySQL runs.</span><span class="sxs-lookup"><span data-stu-id="72cc6-170">Validate MySQL runs.</span></span>

   <span data-ttu-id="72cc6-171">a.</span><span class="sxs-lookup"><span data-stu-id="72cc6-171">a.</span></span> <span data-ttu-id="72cc6-172">Start MySQL.</span><span class="sxs-lookup"><span data-stu-id="72cc6-172">Start MySQL.</span></span>

           service mysql start
   <span data-ttu-id="72cc6-173">b.</span><span class="sxs-lookup"><span data-stu-id="72cc6-173">b.</span></span> <span data-ttu-id="72cc6-174">Secure the MySQL installation, set the root password, remove anonymous users to disable remote root login, and remove the test database.</span><span class="sxs-lookup"><span data-stu-id="72cc6-174">Secure the MySQL installation, set the root password, remove anonymous users to disable remote root login, and remove the test database.</span></span>

           mysql_secure_installation
   <span data-ttu-id="72cc6-175">c.</span><span class="sxs-lookup"><span data-stu-id="72cc6-175">c.</span></span> <span data-ttu-id="72cc6-176">Create a user on the database for cluster operations, and optionally for your applications.</span><span class="sxs-lookup"><span data-stu-id="72cc6-176">Create a user on the database for cluster operations, and optionally for your applications.</span></span>

           mysql -u root -p
           GRANT ALL PRIVILEGES ON *.* TO 'cluster'@'%' IDENTIFIED BY 'p@ssw0rd' WITH GRANT OPTION; FLUSH PRIVILEGES;
           exit

   <span data-ttu-id="72cc6-177">d.</span><span class="sxs-lookup"><span data-stu-id="72cc6-177">d.</span></span> <span data-ttu-id="72cc6-178">Stop MySQL.</span><span class="sxs-lookup"><span data-stu-id="72cc6-178">Stop MySQL.</span></span>

            service mysql stop
7. <span data-ttu-id="72cc6-179">Create a configuration placeholder.</span><span class="sxs-lookup"><span data-stu-id="72cc6-179">Create a configuration placeholder.</span></span>

   <span data-ttu-id="72cc6-180">a.</span><span class="sxs-lookup"><span data-stu-id="72cc6-180">a.</span></span> <span data-ttu-id="72cc6-181">Edit the MySQL configuration to create a placeholder for the cluster settings.</span><span class="sxs-lookup"><span data-stu-id="72cc6-181">Edit the MySQL configuration to create a placeholder for the cluster settings.</span></span> <span data-ttu-id="72cc6-182">Do not replace the **`<Variables>`** or uncomment now.</span><span class="sxs-lookup"><span data-stu-id="72cc6-182">Do not replace the **`<Variables>`** or uncomment now.</span></span> <span data-ttu-id="72cc6-183">That will happen after you create a VM from this template.</span><span class="sxs-lookup"><span data-stu-id="72cc6-183">That will happen after you create a VM from this template.</span></span>

            vi /etc/my.cnf.d/server.cnf
   <span data-ttu-id="72cc6-184">b.</span><span class="sxs-lookup"><span data-stu-id="72cc6-184">b.</span></span> <span data-ttu-id="72cc6-185">Edit the **[galera]** section and clear it out.</span><span class="sxs-lookup"><span data-stu-id="72cc6-185">Edit the **[galera]** section and clear it out.</span></span>

   <span data-ttu-id="72cc6-186">c.</span><span class="sxs-lookup"><span data-stu-id="72cc6-186">c.</span></span> <span data-ttu-id="72cc6-187">Edit the **[mariadb]** section.</span><span class="sxs-lookup"><span data-stu-id="72cc6-187">Edit the **[mariadb]** section.</span></span>

           wsrep_provider=/usr/lib64/galera/libgalera_smm.so
           binlog_format=ROW
           wsrep_sst_method=rsync
           bind-address=0.0.0.0 # When set to 0.0.0.0, the server listens to remote connections
           default_storage_engine=InnoDB
           innodb_autoinc_lock_mode=2

           wsrep_sst_auth=cluster:p@ssw0rd # CHANGE: Username and password you created for the SST cluster MySQL user
           #wsrep_cluster_name='mariadbcluster' # CHANGE: Uncomment and set your desired cluster name
           #wsrep_cluster_address="gcomm://mariadb1,mariadb2,mariadb3" # CHANGE: Uncomment and Add all your servers
           #wsrep_node_address='<ServerIP>' # CHANGE: Uncomment and set IP address of this server
           #wsrep_node_name='<NodeName>' # CHANGE: Uncomment and set the node name of this server
8. <span data-ttu-id="72cc6-188">Open required ports on the firewall by using FirewallD on CentOS 7.</span><span class="sxs-lookup"><span data-stu-id="72cc6-188">Open required ports on the firewall by using FirewallD on CentOS 7.</span></span>

   * <span data-ttu-id="72cc6-189">MySQL: `firewall-cmd --zone=public --add-port=3306/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="72cc6-189">MySQL: `firewall-cmd --zone=public --add-port=3306/tcp --permanent`</span></span>
   * <span data-ttu-id="72cc6-190">GALERA: `firewall-cmd --zone=public --add-port=4567/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="72cc6-190">GALERA: `firewall-cmd --zone=public --add-port=4567/tcp --permanent`</span></span>
   * <span data-ttu-id="72cc6-191">GALERA IST: `firewall-cmd --zone=public --add-port=4568/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="72cc6-191">GALERA IST: `firewall-cmd --zone=public --add-port=4568/tcp --permanent`</span></span>
   * <span data-ttu-id="72cc6-192">RSYNC: `firewall-cmd --zone=public --add-port=4444/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="72cc6-192">RSYNC: `firewall-cmd --zone=public --add-port=4444/tcp --permanent`</span></span>
   * <span data-ttu-id="72cc6-193">Reload the firewall: `firewall-cmd --reload`</span><span class="sxs-lookup"><span data-stu-id="72cc6-193">Reload the firewall: `firewall-cmd --reload`</span></span>

9. <span data-ttu-id="72cc6-194">Optimize the system for performance.</span><span class="sxs-lookup"><span data-stu-id="72cc6-194">Optimize the system for performance.</span></span> <span data-ttu-id="72cc6-195">For more information, see [performance tuning strategy](optimize-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="72cc6-195">For more information, see [performance tuning strategy](optimize-mysql.md).</span></span>

   <span data-ttu-id="72cc6-196">a.</span><span class="sxs-lookup"><span data-stu-id="72cc6-196">a.</span></span> <span data-ttu-id="72cc6-197">Edit the MySQL configuration file again.</span><span class="sxs-lookup"><span data-stu-id="72cc6-197">Edit the MySQL configuration file again.</span></span>

            vi /etc/my.cnf.d/server.cnf
   <span data-ttu-id="72cc6-198">b.</span><span class="sxs-lookup"><span data-stu-id="72cc6-198">b.</span></span> <span data-ttu-id="72cc6-199">Edit the **[mariadb]** section and append the following content:</span><span class="sxs-lookup"><span data-stu-id="72cc6-199">Edit the **[mariadb]** section and append the following content:</span></span>

   > [!NOTE]
   > <span data-ttu-id="72cc6-200">We recommend that innodb\_buffer\_pool_size is 70 percent of your VM's memory.</span><span class="sxs-lookup"><span data-stu-id="72cc6-200">We recommend that innodb\_buffer\_pool_size is 70 percent of your VM's memory.</span></span> <span data-ttu-id="72cc6-201">In this example, it has been set at 2.45 GB for the medium Azure VM with 3.5 GB of RAM.</span><span class="sxs-lookup"><span data-stu-id="72cc6-201">In this example, it has been set at 2.45 GB for the medium Azure VM with 3.5 GB of RAM.</span></span>
   >
   >

           innodb_buffer_pool_size = 2508M # The buffer pool contains buffered data and the index. This is usually set to 70 percent of physical memory.
           innodb_log_file_size = 512M #  Redo logs ensure that write operations are fast, reliable, and recoverable after a crash
           max_connections = 5000 # A larger value will give the server more time to recycle idled connections
           innodb_file_per_table = 1 # Speed up the table space transmission and optimize the debris management performance
           innodb_log_buffer_size = 128M # The log buffer allows transactions to run without having to flush the log to disk before the transactions commit
           innodb_flush_log_at_trx_commit = 2 # The setting of 2 enables the most data integrity and is suitable for Master in MySQL cluster
           query_cache_size = 0
10. <span data-ttu-id="72cc6-202">Stop MySQL, disable MySQL service from running on startup to avoid disrupting the cluster when adding a node, and deprovision the machine.</span><span class="sxs-lookup"><span data-stu-id="72cc6-202">Stop MySQL, disable MySQL service from running on startup to avoid disrupting the cluster when adding a node, and deprovision the machine.</span></span>

        service mysql stop
        chkconfig mysql off
        waagent -deprovision
11. <span data-ttu-id="72cc6-203">Capture the VM through the portal.</span><span class="sxs-lookup"><span data-stu-id="72cc6-203">Capture the VM through the portal.</span></span> <span data-ttu-id="72cc6-204">(Currently, [issue #1268 in the Azure CLI tools](https://github.com/Azure/azure-xplat-cli/issues/1268) describes the fact that images captured by the Azure CLI tools do not capture the attached data disks.)</span><span class="sxs-lookup"><span data-stu-id="72cc6-204">(Currently, [issue #1268 in the Azure CLI tools](https://github.com/Azure/azure-xplat-cli/issues/1268) describes the fact that images captured by the Azure CLI tools do not capture the attached data disks.)</span></span>

    <span data-ttu-id="72cc6-205">a.</span><span class="sxs-lookup"><span data-stu-id="72cc6-205">a.</span></span> <span data-ttu-id="72cc6-206">Shut down the machine through the portal.</span><span class="sxs-lookup"><span data-stu-id="72cc6-206">Shut down the machine through the portal.</span></span>

    <span data-ttu-id="72cc6-207">b.</span><span class="sxs-lookup"><span data-stu-id="72cc6-207">b.</span></span> <span data-ttu-id="72cc6-208">Click **Capture** and specify the image name as **mariadb-galera-image**.</span><span class="sxs-lookup"><span data-stu-id="72cc6-208">Click **Capture** and specify the image name as **mariadb-galera-image**.</span></span> <span data-ttu-id="72cc6-209">Provide a description and check "I have run waagent."</span><span class="sxs-lookup"><span data-stu-id="72cc6-209">Provide a description and check "I have run waagent."</span></span>
      
      ![Capture the virtual machine](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/mariadb-mysql-cluster/capture2.png)

## <a name="create-the-cluster"></a><span data-ttu-id="72cc6-211">Create the cluster</span><span class="sxs-lookup"><span data-stu-id="72cc6-211">Create the cluster</span></span>
<span data-ttu-id="72cc6-212">Create three VMs with the template you created, and then configure and start the cluster.</span><span class="sxs-lookup"><span data-stu-id="72cc6-212">Create three VMs with the template you created, and then configure and start the cluster.</span></span>

1. <span data-ttu-id="72cc6-213">Create the first CentOS 7 VM from the mariadb-galera-image image you created, providing the following information:</span><span class="sxs-lookup"><span data-stu-id="72cc6-213">Create the first CentOS 7 VM from the mariadb-galera-image image you created, providing the following information:</span></span>

 - <span data-ttu-id="72cc6-214">Virtual network name: mariadbvnet</span><span class="sxs-lookup"><span data-stu-id="72cc6-214">Virtual network name: mariadbvnet</span></span>
 - <span data-ttu-id="72cc6-215">Subnet: mariadb</span><span class="sxs-lookup"><span data-stu-id="72cc6-215">Subnet: mariadb</span></span>
 - <span data-ttu-id="72cc6-216">Machine size: medium</span><span class="sxs-lookup"><span data-stu-id="72cc6-216">Machine size: medium</span></span>
 - <span data-ttu-id="72cc6-217">Cloud service name: mariadbha (or whatever name you want to be accessed through mariadbha.cloudapp.net)</span><span class="sxs-lookup"><span data-stu-id="72cc6-217">Cloud service name: mariadbha (or whatever name you want to be accessed through mariadbha.cloudapp.net)</span></span>
 - <span data-ttu-id="72cc6-218">Machine name: mariadb1</span><span class="sxs-lookup"><span data-stu-id="72cc6-218">Machine name: mariadb1</span></span>
 - <span data-ttu-id="72cc6-219">Username: azureuser</span><span class="sxs-lookup"><span data-stu-id="72cc6-219">Username: azureuser</span></span>
 - <span data-ttu-id="72cc6-220">SSH access: enabled</span><span class="sxs-lookup"><span data-stu-id="72cc6-220">SSH access: enabled</span></span>
 - <span data-ttu-id="72cc6-221">Passing the SSH certificate .pem file and replacing /path/to/key.pem with the path where you stored the generated .pem SSH key.</span><span class="sxs-lookup"><span data-stu-id="72cc6-221">Passing the SSH certificate .pem file and replacing /path/to/key.pem with the path where you stored the generated .pem SSH key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="72cc6-222">The following commands are split over multiple lines for clarity, but you should enter each as one line.</span><span class="sxs-lookup"><span data-stu-id="72cc6-222">The following commands are split over multiple lines for clarity, but you should enter each as one line.</span></span>
   >
   >
        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 22
        --vm-name mariadb1
        mariadbha mariadb-galera-image azureuser
2. <span data-ttu-id="72cc6-223">Create two more virtual machines by connecting them to the mariadbha cloud service.</span><span class="sxs-lookup"><span data-stu-id="72cc6-223">Create two more virtual machines by connecting them to the mariadbha cloud service.</span></span> <span data-ttu-id="72cc6-224">Change the VM name and the SSH port to a unique port not conflicting with other VMs in the same cloud service.</span><span class="sxs-lookup"><span data-stu-id="72cc6-224">Change the VM name and the SSH port to a unique port not conflicting with other VMs in the same cloud service.</span></span>

        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 23
        --vm-name mariadb2
        --connect mariadbha mariadb-galera-image azureuser
  <span data-ttu-id="72cc6-225">For MariaDB3:</span><span class="sxs-lookup"><span data-stu-id="72cc6-225">For MariaDB3:</span></span>

        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 24
        --vm-name mariadb3
        --connect mariadbha mariadb-galera-image azureuser
3. <span data-ttu-id="72cc6-226">You will need to get the internal IP address of each of the three VMs for the next step:</span><span class="sxs-lookup"><span data-stu-id="72cc6-226">You will need to get the internal IP address of each of the three VMs for the next step:</span></span>

    ![Getting IP address](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/mariadb-mysql-cluster/ip.png)
4. <span data-ttu-id="72cc6-228">Use SSH to sign in to the three VMs and edit the configuration file on each of them.</span><span class="sxs-lookup"><span data-stu-id="72cc6-228">Use SSH to sign in to the three VMs and edit the configuration file on each of them.</span></span>

        sudo vi /etc/my.cnf.d/server.cnf

    <span data-ttu-id="72cc6-229">Uncomment **`wsrep_cluster_name`** and **`wsrep_cluster_address`** by removing the **#** at the beginning of the line.</span><span class="sxs-lookup"><span data-stu-id="72cc6-229">Uncomment **`wsrep_cluster_name`** and **`wsrep_cluster_address`** by removing the **#** at the beginning of the line.</span></span>
    <span data-ttu-id="72cc6-230">Additionally, replace **`<ServerIP>`** in **`wsrep_node_address`** and **`<NodeName>`** in **`wsrep_node_name`** with the VM's IP address and name, respectively, and uncomment those lines as well.</span><span class="sxs-lookup"><span data-stu-id="72cc6-230">Additionally, replace **`<ServerIP>`** in **`wsrep_node_address`** and **`<NodeName>`** in **`wsrep_node_name`** with the VM's IP address and name, respectively, and uncomment those lines as well.</span></span>
5. <span data-ttu-id="72cc6-231">Start the cluster on MariaDB1 and let it run at startup.</span><span class="sxs-lookup"><span data-stu-id="72cc6-231">Start the cluster on MariaDB1 and let it run at startup.</span></span>

        sudo service mysql bootstrap
        chkconfig mysql on
6. <span data-ttu-id="72cc6-232">Start MySQL on MariaDB2 and MariaDB3 and let it run at startup.</span><span class="sxs-lookup"><span data-stu-id="72cc6-232">Start MySQL on MariaDB2 and MariaDB3 and let it run at startup.</span></span>

        sudo service mysql start
        chkconfig mysql on

## <a name="load-balance-the-cluster"></a><span data-ttu-id="72cc6-233">Load balance the cluster</span><span class="sxs-lookup"><span data-stu-id="72cc6-233">Load balance the cluster</span></span>
<span data-ttu-id="72cc6-234">When you created the clustered VMs, you added them into an availability set called clusteravset to ensure that they were put on different fault and update domains and that Azure never does maintenance on all machines at once.</span><span class="sxs-lookup"><span data-stu-id="72cc6-234">When you created the clustered VMs, you added them into an availability set called clusteravset to ensure that they were put on different fault and update domains and that Azure never does maintenance on all machines at once.</span></span> <span data-ttu-id="72cc6-235">This configuration meets the requirements to be supported by the Azure service level agreement (SLA).</span><span class="sxs-lookup"><span data-stu-id="72cc6-235">This configuration meets the requirements to be supported by the Azure service level agreement (SLA).</span></span>

<span data-ttu-id="72cc6-236">Now use Azure Load Balancer to balance requests between the three nodes.</span><span class="sxs-lookup"><span data-stu-id="72cc6-236">Now use Azure Load Balancer to balance requests between the three nodes.</span></span>

<span data-ttu-id="72cc6-237">Run the following commands on your machine by using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="72cc6-237">Run the following commands on your machine by using the Azure CLI.</span></span>

<span data-ttu-id="72cc6-238">The command parameters structure is: `azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`</span><span class="sxs-lookup"><span data-stu-id="72cc6-238">The command parameters structure is: `azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`</span></span>

    azure vm endpoint create-multiple mariadb1 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb2 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb3 3306:3306:tcp:false:MySQL:tcp:3306

<span data-ttu-id="72cc6-239">The CLI sets the load balancer probe interval to 15 seconds, which might be a bit too long.</span><span class="sxs-lookup"><span data-stu-id="72cc6-239">The CLI sets the load balancer probe interval to 15 seconds, which might be a bit too long.</span></span> <span data-ttu-id="72cc6-240">Change it in the portal under **Endpoints** for any of the VMs.</span><span class="sxs-lookup"><span data-stu-id="72cc6-240">Change it in the portal under **Endpoints** for any of the VMs.</span></span>

![Edit endpoint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/mariadb-mysql-cluster/endpoint.png)

<span data-ttu-id="72cc6-242">Select **Reconfigure the Load-Balanced Set**.</span><span class="sxs-lookup"><span data-stu-id="72cc6-242">Select **Reconfigure the Load-Balanced Set**.</span></span>

![Reconfigure the load-balanced Set](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/mariadb-mysql-cluster/endpoint2.png)

<span data-ttu-id="72cc6-244">Change **Probe Interval** to 5 seconds and save your changes.</span><span class="sxs-lookup"><span data-stu-id="72cc6-244">Change **Probe Interval** to 5 seconds and save your changes.</span></span>

![Change probe interval](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/mariadb-mysql-cluster/endpoint3.png)

## <a name="validate-the-cluster"></a><span data-ttu-id="72cc6-246">Validate the cluster</span><span class="sxs-lookup"><span data-stu-id="72cc6-246">Validate the cluster</span></span>
<span data-ttu-id="72cc6-247">The hard work is done.</span><span class="sxs-lookup"><span data-stu-id="72cc6-247">The hard work is done.</span></span> <span data-ttu-id="72cc6-248">The cluster should be now accessible at `mariadbha.cloudapp.net:3306`, which hits the load balancer and route requests between the three VMs smoothly and efficiently.</span><span class="sxs-lookup"><span data-stu-id="72cc6-248">The cluster should be now accessible at `mariadbha.cloudapp.net:3306`, which hits the load balancer and route requests between the three VMs smoothly and efficiently.</span></span>

<span data-ttu-id="72cc6-249">Use your favorite MySQL client to connect, or connect from one of the VMs to verify that this cluster is working.</span><span class="sxs-lookup"><span data-stu-id="72cc6-249">Use your favorite MySQL client to connect, or connect from one of the VMs to verify that this cluster is working.</span></span>

     mysql -u cluster -h mariadbha.cloudapp.net -p

<span data-ttu-id="72cc6-250">Then create a database and populate it with some data.</span><span class="sxs-lookup"><span data-stu-id="72cc6-250">Then create a database and populate it with some data.</span></span>

    CREATE DATABASE TestDB;
    USE TestDB;
    CREATE TABLE TestTable (id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, value VARCHAR(255));
    INSERT INTO TestTable (value)  VALUES ('Value1');
    INSERT INTO TestTable (value)  VALUES ('Value2');
    SELECT * FROM TestTable;

<span data-ttu-id="72cc6-251">The database you created returns the following table:</span><span class="sxs-lookup"><span data-stu-id="72cc6-251">The database you created returns the following table:</span></span>

    +----+--------+
    | id | value  |
    +----+--------+
    |  1 | Value1 |
    |  4 | Value2 |
    +----+--------+
    2 rows in set (0.00 sec)

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="72cc6-252">Next steps</span><span class="sxs-lookup"><span data-stu-id="72cc6-252">Next steps</span></span>
<span data-ttu-id="72cc6-253">In this article, you created a three-node MariaDB + Galera highly available cluster on Azure virtual machines running CentOS 7.</span><span class="sxs-lookup"><span data-stu-id="72cc6-253">In this article, you created a three-node MariaDB + Galera highly available cluster on Azure virtual machines running CentOS 7.</span></span> <span data-ttu-id="72cc6-254">The VMs are load balanced with Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="72cc6-254">The VMs are load balanced with Azure Load Balancer.</span></span>

<span data-ttu-id="72cc6-255">You might want to look at [another way to cluster MySQL on Linux](mysql-cluster.md) and ways to [optimize and test MySQL performance on Azure Linux VMs](optimize-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="72cc6-255">You might want to look at [another way to cluster MySQL on Linux](mysql-cluster.md) and ways to [optimize and test MySQL performance on Azure Linux VMs](optimize-mysql.md).</span></span>

<!--Anchors-->
[Architecture overview]:#architecture-overview
[Creating the template]:#creating-the-template
[Creating the cluster]:#creating-the-cluster
[Load balancing the cluster]:#load-balancing-the-cluster
[Validating the cluster]:#validating-the-cluster
[Next steps]:#next-steps

<!--Image references-->

<!--Link references-->
[Galera]:http://galeracluster.com/products/
[MariaDBs]:https://mariadb.org/en/about/
[create an SSH key for authentication]:http://www.jeff.wilcox.name/2013/06/secure-linux-vms-with-ssh-certificates/
[issue #1268 in the Azure CLI]:https://github.com/Azure/azure-xplat-cli/issues/1268






