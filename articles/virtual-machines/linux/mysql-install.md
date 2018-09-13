---
title: Set up MySQL on a Linux VM in Azure| Microsoft Docs
description: Learn how to install the MySQL stack on a Linux virtual machine (Ubuntu or RedHat family OS) in Azure
services: virtual-machines-linux
documentationcenter: ''
author: SuperScottz
manager: timlt
editor: ''
tags: azure-resource-manager,azure-service-management
ms.assetid: 153bae7c-897b-46b3-bd86-192a6efb94fa
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/01/2016
ms.author: mingzhan
ms.openlocfilehash: cfaa2a41d18341a2632273e0989f5e84dac33727
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553367"
---
# <a name="how-to-install-mysql-on-azure"></a><span data-ttu-id="4a9d8-103">How to install MySQL on Azure</span><span class="sxs-lookup"><span data-stu-id="4a9d8-103">How to install MySQL on Azure</span></span>
<span data-ttu-id="4a9d8-104">In this article, you will learn how to install and configure MySQL on an Azure virtual machine running Linux.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-104">In this article, you will learn how to install and configure MySQL on an Azure virtual machine running Linux.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-mysql-on-your-virtual-machine"></a><span data-ttu-id="4a9d8-105">Install MySQL on your virtual machine</span><span class="sxs-lookup"><span data-stu-id="4a9d8-105">Install MySQL on your virtual machine</span></span>
> [!NOTE]
> <span data-ttu-id="4a9d8-106">You must already have a Microsoft Azure virtual machine running Linux in order to complete this tutorial.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-106">You must already have a Microsoft Azure virtual machine running Linux in order to complete this tutorial.</span></span> <span data-ttu-id="4a9d8-107">Please see the [Azure Linux VM tutorial](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to create and set up a Linux VM with `mysqlnode` as the VM name and `azureuser` as user before proceeding.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-107">Please see the [Azure Linux VM tutorial](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to create and set up a Linux VM with `mysqlnode` as the VM name and `azureuser` as user before proceeding.</span></span>
> 
> 

<span data-ttu-id="4a9d8-108">In this case, use 3306 port as the MySQL port.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-108">In this case, use 3306 port as the MySQL port.</span></span>  

<span data-ttu-id="4a9d8-109">Connect to the Linux VM you created via putty.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-109">Connect to the Linux VM you created via putty.</span></span> <span data-ttu-id="4a9d8-110">If this is the first time you use Azure Linux VM, see how to use putty connect to a Linux VM [here](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4a9d8-110">If this is the first time you use Azure Linux VM, see how to use putty connect to a Linux VM [here](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="4a9d8-111">We will use repository package to install MySQL5.6 as an example in this article.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-111">We will use repository package to install MySQL5.6 as an example in this article.</span></span> <span data-ttu-id="4a9d8-112">Actually, MySQL5.6 has more improvement in performance than MySQL5.5.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-112">Actually, MySQL5.6 has more improvement in performance than MySQL5.5.</span></span>  <span data-ttu-id="4a9d8-113">More information [here](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/).</span><span class="sxs-lookup"><span data-stu-id="4a9d8-113">More information [here](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/).</span></span>

### <a name="how-to-install-mysql56-on-ubuntu"></a><span data-ttu-id="4a9d8-114">How to install MySQL5.6 on Ubuntu</span><span class="sxs-lookup"><span data-stu-id="4a9d8-114">How to install MySQL5.6 on Ubuntu</span></span>
<span data-ttu-id="4a9d8-115">We will use Linux VM with Ubuntu from Azure here.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-115">We will use Linux VM with Ubuntu from Azure here.</span></span>

* <span data-ttu-id="4a9d8-116">Step 1: Install MySQL Server 5.6   Switch to `root` user:</span><span class="sxs-lookup"><span data-stu-id="4a9d8-116">Step 1: Install MySQL Server 5.6   Switch to `root` user:</span></span>
  
            #[azureuser@mysqlnode:~]sudo su -
  
    <span data-ttu-id="4a9d8-117">Install mysql-server 5.6:</span><span class="sxs-lookup"><span data-stu-id="4a9d8-117">Install mysql-server 5.6:</span></span>
  
            #[root@mysqlnode ~]# apt-get update
            #[root@mysqlnode ~]# apt-get -y install mysql-server-5.6
  
    <span data-ttu-id="4a9d8-118">During installation, you will see a dialog window poping up to ask you to set MySQL root password below, and you need set the password here.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-118">During installation, you will see a dialog window poping up to ask you to set MySQL root password below, and you need set the password here.</span></span>
  
    ![image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/mysql-install/virtual-machines-linux-install-mysql-p1.png)

    <span data-ttu-id="4a9d8-120">Input the password again to confirm.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-120">Input the password again to confirm.</span></span>

    ![image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/mysql-install/virtual-machines-linux-install-mysql-p2.png)

* <span data-ttu-id="4a9d8-122">Step 2: Login MySQL Server</span><span class="sxs-lookup"><span data-stu-id="4a9d8-122">Step 2: Login MySQL Server</span></span>
  
    <span data-ttu-id="4a9d8-123">When MySQL server installation finished, MySQL service will be started automatically.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-123">When MySQL server installation finished, MySQL service will be started automatically.</span></span> <span data-ttu-id="4a9d8-124">You can login MySQL Server with `root` user.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-124">You can login MySQL Server with `root` user.</span></span>
    <span data-ttu-id="4a9d8-125">Use the below command to login and input password.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-125">Use the below command to login and input password.</span></span>
  
             #[root@mysqlnode ~]# mysql -uroot -p
* <span data-ttu-id="4a9d8-126">Step 3: Manage the running MySQL service</span><span class="sxs-lookup"><span data-stu-id="4a9d8-126">Step 3: Manage the running MySQL service</span></span>
  
    <span data-ttu-id="4a9d8-127">(a) Get status of MySQL service</span><span class="sxs-lookup"><span data-stu-id="4a9d8-127">(a) Get status of MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql status
  
    <span data-ttu-id="4a9d8-128">(b) Start MySQL Service</span><span class="sxs-lookup"><span data-stu-id="4a9d8-128">(b) Start MySQL Service</span></span>
  
             #[root@mysqlnode ~]# service mysql start
  
    <span data-ttu-id="4a9d8-129">(c) Stop MySQL service</span><span class="sxs-lookup"><span data-stu-id="4a9d8-129">(c) Stop MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql stop
  
    <span data-ttu-id="4a9d8-130">(d) Restart the MySQL service</span><span class="sxs-lookup"><span data-stu-id="4a9d8-130">(d) Restart the MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql restart

### <a name="how-to-install-mysql-on-red-hat-os-family-like-centos-oracle-linux"></a><span data-ttu-id="4a9d8-131">How to install MySQL on Red Hat OS family like CentOS, Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="4a9d8-131">How to install MySQL on Red Hat OS family like CentOS, Oracle Linux</span></span>
<span data-ttu-id="4a9d8-132">We will use Linux VM with CentOS or Oracle Linux here.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-132">We will use Linux VM with CentOS or Oracle Linux here.</span></span>

* <span data-ttu-id="4a9d8-133">Step 1: Add the MySQL Yum repository   Switch to `root` user:</span><span class="sxs-lookup"><span data-stu-id="4a9d8-133">Step 1: Add the MySQL Yum repository   Switch to `root` user:</span></span>
  
            #[azureuser@mysqlnode:~]sudo su -
  
    <span data-ttu-id="4a9d8-134">Download and install the MySQL release package:</span><span class="sxs-lookup"><span data-stu-id="4a9d8-134">Download and install the MySQL release package:</span></span>
  
            #[root@mysqlnode ~]# wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm
            #[root@mysqlnode ~]# yum localinstall -y mysql-community-release-el6-5.noarch.rpm
* <span data-ttu-id="4a9d8-135">Step 2: Edit below file to enable the MySQL repository for downloading the MySQL5.6 package.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-135">Step 2: Edit below file to enable the MySQL repository for downloading the MySQL5.6 package.</span></span>
  
            #[root@mysqlnode ~]# vim /etc/yum.repos.d/mysql-community.repo
  
    <span data-ttu-id="4a9d8-136">Update each value of this file to below:</span><span class="sxs-lookup"><span data-stu-id="4a9d8-136">Update each value of this file to below:</span></span>
  
        \# *Enable to use MySQL 5.6*
  
        [mysql56-community]
        name=MySQL 5.6 Community Server
  
        baseurl=http://repo.mysql.com/yum/mysql-5.6-community/el/6/$basearch/
  
        enabled=1
  
        gpgcheck=1
  
        gpgkey=file:/etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
* <span data-ttu-id="4a9d8-137">Step 3: Install MySQL from MySQL repository   Install MySQL:</span><span class="sxs-lookup"><span data-stu-id="4a9d8-137">Step 3: Install MySQL from MySQL repository   Install MySQL:</span></span>
  
           #[root@mysqlnode ~]#yum install mysql-community-server
  
    <span data-ttu-id="4a9d8-138">MySQL RPM package and all related packages will be installed.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-138">MySQL RPM package and all related packages will be installed.</span></span>
* <span data-ttu-id="4a9d8-139">Step 4: Manage the running MySQL service</span><span class="sxs-lookup"><span data-stu-id="4a9d8-139">Step 4: Manage the running MySQL service</span></span>
  
    <span data-ttu-id="4a9d8-140">(a) Check the service status of the MySQL server:</span><span class="sxs-lookup"><span data-stu-id="4a9d8-140">(a) Check the service status of the MySQL server:</span></span>
  
           #[root@mysqlnode ~]#service mysqld status
  
    <span data-ttu-id="4a9d8-141">(b) Check whether the default port of  MySQL server is running:</span><span class="sxs-lookup"><span data-stu-id="4a9d8-141">(b) Check whether the default port of  MySQL server is running:</span></span>
  
           #[root@mysqlnode ~]#netstat  –tunlp|grep 3306

    <span data-ttu-id="4a9d8-142">(c) Start the MySQL server:</span><span class="sxs-lookup"><span data-stu-id="4a9d8-142">(c) Start the MySQL server:</span></span>

           #[root@mysqlnode ~]#service mysqld start

    <span data-ttu-id="4a9d8-143">(d) Stop the MySQL server:</span><span class="sxs-lookup"><span data-stu-id="4a9d8-143">(d) Stop the MySQL server:</span></span>

           #[root@mysqlnode ~]#service mysqld stop

    <span data-ttu-id="4a9d8-144">(e) Set MySQL to start when the system boot-up:</span><span class="sxs-lookup"><span data-stu-id="4a9d8-144">(e) Set MySQL to start when the system boot-up:</span></span>

           #[root@mysqlnode ~]#chkconfig mysqld on


### <a name="how-to-install-mysql-on-suse-linux"></a><span data-ttu-id="4a9d8-145">How to install MySQL on SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="4a9d8-145">How to install MySQL on SUSE Linux</span></span>
<span data-ttu-id="4a9d8-146">We will use Linux VM with OpenSUSE here.</span><span class="sxs-lookup"><span data-stu-id="4a9d8-146">We will use Linux VM with OpenSUSE here.</span></span>

* <span data-ttu-id="4a9d8-147">Step 1: Download and install MySQL Server</span><span class="sxs-lookup"><span data-stu-id="4a9d8-147">Step 1: Download and install MySQL Server</span></span>
  
    <span data-ttu-id="4a9d8-148">Switch to `root` user through below command:</span><span class="sxs-lookup"><span data-stu-id="4a9d8-148">Switch to `root` user through below command:</span></span>  
  
           #sudo su -
  
    <span data-ttu-id="4a9d8-149">Download and install MySQL package:</span><span class="sxs-lookup"><span data-stu-id="4a9d8-149">Download and install MySQL package:</span></span>
  
           #[root@mysqlnode ~]# zypper update
  
           #[root@mysqlnode ~]# zypper install mysql-server mysql-devel mysql
* <span data-ttu-id="4a9d8-150">Step 2: Manage the running MySQL service</span><span class="sxs-lookup"><span data-stu-id="4a9d8-150">Step 2: Manage the running MySQL service</span></span>
  
    <span data-ttu-id="4a9d8-151">(a) Check the status of the MySQL server:</span><span class="sxs-lookup"><span data-stu-id="4a9d8-151">(a) Check the status of the MySQL server:</span></span>
  
           #[root@mysqlnode ~]# rcmysql status
  
    <span data-ttu-id="4a9d8-152">(b) Check whether the default port of the MySQL server:</span><span class="sxs-lookup"><span data-stu-id="4a9d8-152">(b) Check whether the default port of the MySQL server:</span></span>
  
           #[root@mysqlnode ~]# netstat  –tunlp|grep 3306

    <span data-ttu-id="4a9d8-153">(c) Start the MySQL server:</span><span class="sxs-lookup"><span data-stu-id="4a9d8-153">(c) Start the MySQL server:</span></span>

           #[root@mysqlnode ~]# rcmysql start

    <span data-ttu-id="4a9d8-154">(d) Stop the MySQL server:</span><span class="sxs-lookup"><span data-stu-id="4a9d8-154">(d) Stop the MySQL server:</span></span>

           #[root@mysqlnode ~]# rcmysql stop

    <span data-ttu-id="4a9d8-155">(e) Set MySQL to start when the system boot-up:</span><span class="sxs-lookup"><span data-stu-id="4a9d8-155">(e) Set MySQL to start when the system boot-up:</span></span>

           #[root@mysqlnode ~]# insserv mysql

### <a name="next-step"></a><span data-ttu-id="4a9d8-156">Next Step</span><span class="sxs-lookup"><span data-stu-id="4a9d8-156">Next Step</span></span>
<span data-ttu-id="4a9d8-157">Find more usage and information regarding MySQL [Here](https://www.mysql.com/).</span><span class="sxs-lookup"><span data-stu-id="4a9d8-157">Find more usage and information regarding MySQL [Here](https://www.mysql.com/).</span></span>



