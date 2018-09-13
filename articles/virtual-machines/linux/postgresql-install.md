---
title: Set up PostgreSQL on a Linux VM | Microsoft Docs
description: Learn how to install and configure PostgreSQL on a Linux virtual machine in Azure
services: virtual-machines-linux
documentationcenter: ''
author: SuperScottz
manager: timlt
editor: ''
tags: azure-resource-manager,azure-service-management
ms.assetid: 1a747363-0cc5-4ba3-9be7-084dfeb04651
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: mingzhan
ms.openlocfilehash: 7c22323e7ce726d4765ae84785a17d9274b8cb87
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563943"
---
# <a name="install-and-configure-postgresql-on-azure"></a><span data-ttu-id="1085a-103">Install and configure PostgreSQL on Azure</span><span class="sxs-lookup"><span data-stu-id="1085a-103">Install and configure PostgreSQL on Azure</span></span>
<span data-ttu-id="1085a-104">PostgreSQL is an advanced open-source database similar to Oracle and DB2.</span><span class="sxs-lookup"><span data-stu-id="1085a-104">PostgreSQL is an advanced open-source database similar to Oracle and DB2.</span></span> <span data-ttu-id="1085a-105">It includes enterprise-ready features such as full ACID compliance, reliable transactional processing, and multi-version concurrency control.</span><span class="sxs-lookup"><span data-stu-id="1085a-105">It includes enterprise-ready features such as full ACID compliance, reliable transactional processing, and multi-version concurrency control.</span></span> <span data-ttu-id="1085a-106">It also supports standards such as ANSI SQL and SQL/MED (including foreign data wrappers for Oracle, MySQL, MongoDB, and many others).</span><span class="sxs-lookup"><span data-stu-id="1085a-106">It also supports standards such as ANSI SQL and SQL/MED (including foreign data wrappers for Oracle, MySQL, MongoDB, and many others).</span></span> <span data-ttu-id="1085a-107">It is highly extensible with support for over 12 procedural languages, GIN and GiST indexes, spatial data support, and multiple NoSQL-like features for JSON or key-value-based applications.</span><span class="sxs-lookup"><span data-stu-id="1085a-107">It is highly extensible with support for over 12 procedural languages, GIN and GiST indexes, spatial data support, and multiple NoSQL-like features for JSON or key-value-based applications.</span></span>

<span data-ttu-id="1085a-108">In this article, you will learn how to install and configure PostgreSQL on an Azure virtual machine running Linux.</span><span class="sxs-lookup"><span data-stu-id="1085a-108">In this article, you will learn how to install and configure PostgreSQL on an Azure virtual machine running Linux.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-postgresql"></a><span data-ttu-id="1085a-109">Install PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="1085a-109">Install PostgreSQL</span></span>
> [!NOTE]
> <span data-ttu-id="1085a-110">You must already have an Azure virtual machine running Linux in order to complete this tutorial.</span><span class="sxs-lookup"><span data-stu-id="1085a-110">You must already have an Azure virtual machine running Linux in order to complete this tutorial.</span></span> <span data-ttu-id="1085a-111">To create and set up a Linux VM before proceeding, see the [Azure Linux VM tutorial](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1085a-111">To create and set up a Linux VM before proceeding, see the [Azure Linux VM tutorial](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

<span data-ttu-id="1085a-112">In this case, use port 1999 as the PostgreSQL port.</span><span class="sxs-lookup"><span data-stu-id="1085a-112">In this case, use port 1999 as the PostgreSQL port.</span></span>  

<span data-ttu-id="1085a-113">Connect to the Linux VM you created via PuTTY.</span><span class="sxs-lookup"><span data-stu-id="1085a-113">Connect to the Linux VM you created via PuTTY.</span></span> <span data-ttu-id="1085a-114">If this is the first time you're using an Azure Linux VM, see [How to Use SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to learn how to use PuTTY to connect to a Linux VM.</span><span class="sxs-lookup"><span data-stu-id="1085a-114">If this is the first time you're using an Azure Linux VM, see [How to Use SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to learn how to use PuTTY to connect to a Linux VM.</span></span>

1. <span data-ttu-id="1085a-115">Run the following command to switch to the root (admin):</span><span class="sxs-lookup"><span data-stu-id="1085a-115">Run the following command to switch to the root (admin):</span></span>
   
        # sudo su -
2. <span data-ttu-id="1085a-116">Some distributions have dependencies that you must install before installing PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="1085a-116">Some distributions have dependencies that you must install before installing PostgreSQL.</span></span> <span data-ttu-id="1085a-117">Check for your distro in this list and run the appropriate command:</span><span class="sxs-lookup"><span data-stu-id="1085a-117">Check for your distro in this list and run the appropriate command:</span></span>
   
   * <span data-ttu-id="1085a-118">Red Hat base Linux:</span><span class="sxs-lookup"><span data-stu-id="1085a-118">Red Hat base Linux:</span></span>
     
           # yum install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
   * <span data-ttu-id="1085a-119">Debian base Linux:</span><span class="sxs-lookup"><span data-stu-id="1085a-119">Debian base Linux:</span></span>
     
            # apt-get install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam libxslt-devel tcl-devel python-devel -y  
   * <span data-ttu-id="1085a-120">SUSE Linux:</span><span class="sxs-lookup"><span data-stu-id="1085a-120">SUSE Linux:</span></span>
     
           # zypper install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
3. <span data-ttu-id="1085a-121">Download PostgreSQL into the root directory, and then unzip the package:</span><span class="sxs-lookup"><span data-stu-id="1085a-121">Download PostgreSQL into the root directory, and then unzip the package:</span></span>
   
        # wget https://ftp.postgresql.org/pub/source/v9.3.5/postgresql-9.3.5.tar.bz2 -P /root/
   
        # tar jxvf  postgresql-9.3.5.tar.bz2
   
    <span data-ttu-id="1085a-122">The above is an example.</span><span class="sxs-lookup"><span data-stu-id="1085a-122">The above is an example.</span></span> <span data-ttu-id="1085a-123">You can find the more detailed download address in the [Index of /pub/source/](https://ftp.postgresql.org/pub/source/).</span><span class="sxs-lookup"><span data-stu-id="1085a-123">You can find the more detailed download address in the [Index of /pub/source/](https://ftp.postgresql.org/pub/source/).</span></span>
4. <span data-ttu-id="1085a-124">To start the build, run these commands:</span><span class="sxs-lookup"><span data-stu-id="1085a-124">To start the build, run these commands:</span></span>
   
        # cd postgresql-9.3.5
   
        # ./configure --prefix=/opt/postgresql-9.3.5
5. <span data-ttu-id="1085a-125">If  you want to build everything that can be built, including the documentation (HTML and man pages) and additional modules (contrib), run the following command instead:</span><span class="sxs-lookup"><span data-stu-id="1085a-125">If  you want to build everything that can be built, including the documentation (HTML and man pages) and additional modules (contrib), run the following command instead:</span></span>
   
        # gmake install-world
   
    <span data-ttu-id="1085a-126">You should receive the following confirmation message:</span><span class="sxs-lookup"><span data-stu-id="1085a-126">You should receive the following confirmation message:</span></span>
   
        PostgreSQL, contrib, and documentation successfully made. Ready to install.

## <a name="configure-postgresql"></a><span data-ttu-id="1085a-127">Configure PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="1085a-127">Configure PostgreSQL</span></span>
1. <span data-ttu-id="1085a-128">(Optional) Create a symbolic link to shorten the PostgreSQL reference to not include the version number:</span><span class="sxs-lookup"><span data-stu-id="1085a-128">(Optional) Create a symbolic link to shorten the PostgreSQL reference to not include the version number:</span></span>
   
        # ln -s /opt/pgsql9.3.5 /opt/pgsql
2. <span data-ttu-id="1085a-129">Create a directory for the database:</span><span class="sxs-lookup"><span data-stu-id="1085a-129">Create a directory for the database:</span></span>
   
        # mkdir -p /opt/pgsql_data
3. <span data-ttu-id="1085a-130">Create a non-root user and modify that user’s profile.</span><span class="sxs-lookup"><span data-stu-id="1085a-130">Create a non-root user and modify that user’s profile.</span></span> <span data-ttu-id="1085a-131">Then, switch to this new user (called *postgres* in our example):</span><span class="sxs-lookup"><span data-stu-id="1085a-131">Then, switch to this new user (called *postgres* in our example):</span></span>
   
        # useradd postgres
   
        # chown -R postgres.postgres /opt/pgsql_data
   
        # su - postgres
   
   > [!NOTE]
   > <span data-ttu-id="1085a-132">For security reasons, PostgreSQL uses a non-root user to initialize, start, or shut down the database.</span><span class="sxs-lookup"><span data-stu-id="1085a-132">For security reasons, PostgreSQL uses a non-root user to initialize, start, or shut down the database.</span></span>
   > 
   > 
4. <span data-ttu-id="1085a-133">Edit the *bash_profile* file by entering the commands below.</span><span class="sxs-lookup"><span data-stu-id="1085a-133">Edit the *bash_profile* file by entering the commands below.</span></span> <span data-ttu-id="1085a-134">These lines will be added to the end of the *bash_profile* file:</span><span class="sxs-lookup"><span data-stu-id="1085a-134">These lines will be added to the end of the *bash_profile* file:</span></span>
   
        cat >> ~/.bash_profile <<EOF
        export PGPORT=1999
        export PGDATA=/opt/pgsql_data
        export LANG=en_US.utf8
        export PGHOME=/opt/pgsql
        export PATH=\$PATH:\$PGHOME/bin
        export MANPATH=\$MANPATH:\$PGHOME/share/man
        export DATA=`date +"%Y%m%d%H%M"`
        export PGUSER=postgres
        alias rm='rm -i'
        alias ll='ls -lh'
        EOF
5. <span data-ttu-id="1085a-135">Execute the *bash_profile* file:</span><span class="sxs-lookup"><span data-stu-id="1085a-135">Execute the *bash_profile* file:</span></span>
   
        $ source .bash_profile
6. <span data-ttu-id="1085a-136">Validate your installation by using the following command:</span><span class="sxs-lookup"><span data-stu-id="1085a-136">Validate your installation by using the following command:</span></span>
   
        $ which psql
   
    <span data-ttu-id="1085a-137">If your installation is successful, you will see the following response:</span><span class="sxs-lookup"><span data-stu-id="1085a-137">If your installation is successful, you will see the following response:</span></span>
   
        /opt/pgsql/bin/psql
7. <span data-ttu-id="1085a-138">You can also check the PostgreSQL version:</span><span class="sxs-lookup"><span data-stu-id="1085a-138">You can also check the PostgreSQL version:</span></span>
   
        $ psql -V
8. <span data-ttu-id="1085a-139">Initialize the database:</span><span class="sxs-lookup"><span data-stu-id="1085a-139">Initialize the database:</span></span>
   
        $ initdb -D $PGDATA -E UTF8 --locale=C -U postgres -W
   
    <span data-ttu-id="1085a-140">You should receive the following output:</span><span class="sxs-lookup"><span data-stu-id="1085a-140">You should receive the following output:</span></span>

![image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/postgresql-install/no1.png)

## <a name="set-up-postgresql"></a><span data-ttu-id="1085a-142">Set up PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="1085a-142">Set up PostgreSQL</span></span>
<!--    [postgres@ test ~]$ exit -->

<span data-ttu-id="1085a-143">Run the following commands:</span><span class="sxs-lookup"><span data-stu-id="1085a-143">Run the following commands:</span></span>

    # cd /root/postgresql-9.3.5/contrib/start-scripts

    # cp linux /etc/init.d/postgresql

<span data-ttu-id="1085a-144">Modify two variables in the /etc/init.d/postgresql file.</span><span class="sxs-lookup"><span data-stu-id="1085a-144">Modify two variables in the /etc/init.d/postgresql file.</span></span> <span data-ttu-id="1085a-145">The prefix is set to the installation path of PostgreSQL: **/opt/pgsql**.</span><span class="sxs-lookup"><span data-stu-id="1085a-145">The prefix is set to the installation path of PostgreSQL: **/opt/pgsql**.</span></span> <span data-ttu-id="1085a-146">PGDATA is set to the data storage path of PostgreSQL: **/opt/pgsql_data**.</span><span class="sxs-lookup"><span data-stu-id="1085a-146">PGDATA is set to the data storage path of PostgreSQL: **/opt/pgsql_data**.</span></span>

    # sed -i '32s#usr/local#opt#' /etc/init.d/postgresql

    # sed -i '35s#usr/local/pgsql/data#opt/pgsql_data#' /etc/init.d/postgresql

![image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/postgresql-install/no2.png)

<span data-ttu-id="1085a-148">Change the file to make it executable:</span><span class="sxs-lookup"><span data-stu-id="1085a-148">Change the file to make it executable:</span></span>

    # chmod +x /etc/init.d/postgresql

<span data-ttu-id="1085a-149">Start PostgreSQL:</span><span class="sxs-lookup"><span data-stu-id="1085a-149">Start PostgreSQL:</span></span>

    # /etc/init.d/postgresql start

<span data-ttu-id="1085a-150">Check if the endpoint of PostgreSQL is on:</span><span class="sxs-lookup"><span data-stu-id="1085a-150">Check if the endpoint of PostgreSQL is on:</span></span>

    # netstat -tunlp|grep 1999

<span data-ttu-id="1085a-151">You should see the following output:</span><span class="sxs-lookup"><span data-stu-id="1085a-151">You should see the following output:</span></span>

![image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/postgresql-install/no3.png)

## <a name="connect-to-the-postgres-database"></a><span data-ttu-id="1085a-153">Connect to the Postgres database</span><span class="sxs-lookup"><span data-stu-id="1085a-153">Connect to the Postgres database</span></span>
<span data-ttu-id="1085a-154">Switch to the postgres user once again:</span><span class="sxs-lookup"><span data-stu-id="1085a-154">Switch to the postgres user once again:</span></span>

    # su - postgres

<span data-ttu-id="1085a-155">Create a Postgres database:</span><span class="sxs-lookup"><span data-stu-id="1085a-155">Create a Postgres database:</span></span>

    $ createdb events

<span data-ttu-id="1085a-156">Connect to the events database that you just created:</span><span class="sxs-lookup"><span data-stu-id="1085a-156">Connect to the events database that you just created:</span></span>

    $ psql -d events

## <a name="create-and-delete-a-postgres-table"></a><span data-ttu-id="1085a-157">Create and delete a Postgres table</span><span class="sxs-lookup"><span data-stu-id="1085a-157">Create and delete a Postgres table</span></span>
<span data-ttu-id="1085a-158">Now that you have connected to the database, you can create tables in it.</span><span class="sxs-lookup"><span data-stu-id="1085a-158">Now that you have connected to the database, you can create tables in it.</span></span>

<span data-ttu-id="1085a-159">For example, create a new example Postgres table by using the following command:</span><span class="sxs-lookup"><span data-stu-id="1085a-159">For example, create a new example Postgres table by using the following command:</span></span>

    CREATE TABLE potluck (name VARCHAR(20),    food VARCHAR(30),    confirmed CHAR(1), signup_date DATE);

<span data-ttu-id="1085a-160">You have now set up a four-column table with the following column names and restrictions:</span><span class="sxs-lookup"><span data-stu-id="1085a-160">You have now set up a four-column table with the following column names and restrictions:</span></span>

1. <span data-ttu-id="1085a-161">The “name” column has been limited by the VARCHAR command to be under 20 characters long.</span><span class="sxs-lookup"><span data-stu-id="1085a-161">The “name” column has been limited by the VARCHAR command to be under 20 characters long.</span></span>
2. <span data-ttu-id="1085a-162">The “food” column indicates the food item that each person will bring.</span><span class="sxs-lookup"><span data-stu-id="1085a-162">The “food” column indicates the food item that each person will bring.</span></span> <span data-ttu-id="1085a-163">VARCHAR limits this text to be under 30 characters.</span><span class="sxs-lookup"><span data-stu-id="1085a-163">VARCHAR limits this text to be under 30 characters.</span></span>
3. <span data-ttu-id="1085a-164">The “confirmed” column records whether the person has RSVP’d to the potluck.</span><span class="sxs-lookup"><span data-stu-id="1085a-164">The “confirmed” column records whether the person has RSVP’d to the potluck.</span></span> <span data-ttu-id="1085a-165">The acceptable values are "Y" and "N".</span><span class="sxs-lookup"><span data-stu-id="1085a-165">The acceptable values are "Y" and "N".</span></span>
4. <span data-ttu-id="1085a-166">The “date” column shows when they signed up for the event.</span><span class="sxs-lookup"><span data-stu-id="1085a-166">The “date” column shows when they signed up for the event.</span></span> <span data-ttu-id="1085a-167">Postgres requires that dates be written as yyyy-mm-dd.</span><span class="sxs-lookup"><span data-stu-id="1085a-167">Postgres requires that dates be written as yyyy-mm-dd.</span></span>

<span data-ttu-id="1085a-168">You should see the following if your table has been successfully created:</span><span class="sxs-lookup"><span data-stu-id="1085a-168">You should see the following if your table has been successfully created:</span></span>

![image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/postgresql-install/no4.png)

<span data-ttu-id="1085a-170">You can also check the table structure by using the following command:</span><span class="sxs-lookup"><span data-stu-id="1085a-170">You can also check the table structure by using the following command:</span></span>

![image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/postgresql-install/no5.png)

### <a name="add-data-to-a-table"></a><span data-ttu-id="1085a-172">Add data to a table</span><span class="sxs-lookup"><span data-stu-id="1085a-172">Add data to a table</span></span>
<span data-ttu-id="1085a-173">First, insert information into a row:</span><span class="sxs-lookup"><span data-stu-id="1085a-173">First, insert information into a row:</span></span>

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('John', 'Casserole', 'Y', '2012-04-11');

<span data-ttu-id="1085a-174">You should see this output:</span><span class="sxs-lookup"><span data-stu-id="1085a-174">You should see this output:</span></span>

![image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/postgresql-install/no6.png)

<span data-ttu-id="1085a-176">You can add a couple more people to the table as well.</span><span class="sxs-lookup"><span data-stu-id="1085a-176">You can add a couple more people to the table as well.</span></span> <span data-ttu-id="1085a-177">Here are some options, or you can create your own:</span><span class="sxs-lookup"><span data-stu-id="1085a-177">Here are some options, or you can create your own:</span></span>

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Sandy', 'Key Lime Tarts', 'N', '2012-04-14');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES ('Tom', 'BBQ','Y', '2012-04-18');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Tina', 'Salad', 'Y', '2012-04-18');

### <a name="show-tables"></a><span data-ttu-id="1085a-178">Show tables</span><span class="sxs-lookup"><span data-stu-id="1085a-178">Show tables</span></span>
<span data-ttu-id="1085a-179">Use the following command to show a table:</span><span class="sxs-lookup"><span data-stu-id="1085a-179">Use the following command to show a table:</span></span>

    select * from potluck;

<span data-ttu-id="1085a-180">The output is:</span><span class="sxs-lookup"><span data-stu-id="1085a-180">The output is:</span></span>

![image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/postgresql-install/no7.png)

### <a name="delete-data-in-a-table"></a><span data-ttu-id="1085a-182">Delete data in a table</span><span class="sxs-lookup"><span data-stu-id="1085a-182">Delete data in a table</span></span>
<span data-ttu-id="1085a-183">Use the following command to delete data in a table:</span><span class="sxs-lookup"><span data-stu-id="1085a-183">Use the following command to delete data in a table:</span></span>

    delete from potluck where name=’John’;

<span data-ttu-id="1085a-184">This deletes all the information in the "John" row.</span><span class="sxs-lookup"><span data-stu-id="1085a-184">This deletes all the information in the "John" row.</span></span> <span data-ttu-id="1085a-185">The output is:</span><span class="sxs-lookup"><span data-stu-id="1085a-185">The output is:</span></span>

![image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/postgresql-install/no8.png)

### <a name="update-data-in-a-table"></a><span data-ttu-id="1085a-187">Update data in a table</span><span class="sxs-lookup"><span data-stu-id="1085a-187">Update data in a table</span></span>
<span data-ttu-id="1085a-188">Use the following command to update data in a table.</span><span class="sxs-lookup"><span data-stu-id="1085a-188">Use the following command to update data in a table.</span></span> <span data-ttu-id="1085a-189">For this one, Sandy has confirmed that she is attending, so we will change her RSVP from "N" to "Y":</span><span class="sxs-lookup"><span data-stu-id="1085a-189">For this one, Sandy has confirmed that she is attending, so we will change her RSVP from "N" to "Y":</span></span>

     UPDATE potluck set confirmed = 'Y' WHERE name = 'Sandy';


## <a name="get-more-information-about-postgresql"></a><span data-ttu-id="1085a-190">Get more information about PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="1085a-190">Get more information about PostgreSQL</span></span>
<span data-ttu-id="1085a-191">Now that you have completed the installation of PostgreSQL in an Azure Linux VM, you can enjoy using it in Azure.</span><span class="sxs-lookup"><span data-stu-id="1085a-191">Now that you have completed the installation of PostgreSQL in an Azure Linux VM, you can enjoy using it in Azure.</span></span> <span data-ttu-id="1085a-192">To learn more about PostgreSQL, visit the [PostgreSQL website](http://www.postgresql.org/).</span><span class="sxs-lookup"><span data-stu-id="1085a-192">To learn more about PostgreSQL, visit the [PostgreSQL website](http://www.postgresql.org/).</span></span>









