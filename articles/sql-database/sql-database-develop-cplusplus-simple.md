---
title: Connect to SQL Database using C and C++ | Microsoft Docs
description: Use the sample code in this quick start to build a modern application with C++ and backed by a powerful relational database in the cloud with Azure SQL Database.
services: sql-database
documentationcenter: ''
author: asthana86
manager: danmoth
editor: ''
ms.assetid: 07d9e0b1-3234-4f17-a252-a7559160a9db
ms.service: sql-database
ms.custom: development
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 03/06/2017
ms.author: tobiast
ms.openlocfilehash: 026bd59d04beacb8512f981b68b485f06d35118c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554953"
---
# <a name="connect-to-sql-database-using-c-and-c"></a><span data-ttu-id="862f6-103">Connect to SQL Database using C and C++</span><span class="sxs-lookup"><span data-stu-id="862f6-103">Connect to SQL Database using C and C++</span></span>
<span data-ttu-id="862f6-104">This post is aimed at C and C++ developers trying to connect to Azure SQL DB.</span><span class="sxs-lookup"><span data-stu-id="862f6-104">This post is aimed at C and C++ developers trying to connect to Azure SQL DB.</span></span> <span data-ttu-id="862f6-105">It is broken down into sections so you can jump to the section that best captures your interest.</span><span class="sxs-lookup"><span data-stu-id="862f6-105">It is broken down into sections so you can jump to the section that best captures your interest.</span></span> 

## <a name="prerequisites-for-the-cc-tutorial"></a><span data-ttu-id="862f6-106">Prerequisites for the C/C++ tutorial</span><span class="sxs-lookup"><span data-stu-id="862f6-106">Prerequisites for the C/C++ tutorial</span></span>
<span data-ttu-id="862f6-107">Make sure you have the following items:</span><span class="sxs-lookup"><span data-stu-id="862f6-107">Make sure you have the following items:</span></span>

* <span data-ttu-id="862f6-108">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="862f6-108">An active Azure account.</span></span> <span data-ttu-id="862f6-109">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="862f6-109">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="862f6-110">[Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="862f6-110">[Visual Studio](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="862f6-111">You must install the C++ language components to build and run this sample.</span><span class="sxs-lookup"><span data-stu-id="862f6-111">You must install the C++ language components to build and run this sample.</span></span>
* <span data-ttu-id="862f6-112">[Visual Studio Linux Development](https://visualstudiogallery.msdn.microsoft.com/725025cf-7067-45c2-8d01-1e0fd359ae6e).</span><span class="sxs-lookup"><span data-stu-id="862f6-112">[Visual Studio Linux Development](https://visualstudiogallery.msdn.microsoft.com/725025cf-7067-45c2-8d01-1e0fd359ae6e).</span></span> <span data-ttu-id="862f6-113">If you are developing on Linux, you must also install the Visual Studio Linux extension.</span><span class="sxs-lookup"><span data-stu-id="862f6-113">If you are developing on Linux, you must also install the Visual Studio Linux extension.</span></span> 

## <a id="AzureSQL"></a><span data-ttu-id="862f6-114">Azure SQL Database and SQL Server on virtual machines</span><span class="sxs-lookup"><span data-stu-id="862f6-114">Azure SQL Database and SQL Server on virtual machines</span></span>
<span data-ttu-id="862f6-115">Azure SQL is built on Microsoft SQL Server and is designed to provide a high-availability, performant, and scalable service.</span><span class="sxs-lookup"><span data-stu-id="862f6-115">Azure SQL is built on Microsoft SQL Server and is designed to provide a high-availability, performant, and scalable service.</span></span> <span data-ttu-id="862f6-116">There are many benefits to using SQL Azure over your proprietary database running on premises.</span><span class="sxs-lookup"><span data-stu-id="862f6-116">There are many benefits to using SQL Azure over your proprietary database running on premises.</span></span> <span data-ttu-id="862f6-117">With SQL Azure you don’t have to install, set up, maintain, or manage your database but only the content and the structure of your database.</span><span class="sxs-lookup"><span data-stu-id="862f6-117">With SQL Azure you don’t have to install, set up, maintain, or manage your database but only the content and the structure of your database.</span></span> <span data-ttu-id="862f6-118">Typical things that we worry about with databases like fault tolerance and redundancy are all built in.</span><span class="sxs-lookup"><span data-stu-id="862f6-118">Typical things that we worry about with databases like fault tolerance and redundancy are all built in.</span></span> 

<span data-ttu-id="862f6-119">Azure currently has two options for hosting SQL server workloads: Azure SQL database, database as a service and SQL server on Virtual Machines (VM).</span><span class="sxs-lookup"><span data-stu-id="862f6-119">Azure currently has two options for hosting SQL server workloads: Azure SQL database, database as a service and SQL server on Virtual Machines (VM).</span></span> <span data-ttu-id="862f6-120">We will not get into detail about the differences between these two except that Azure SQL database is your best bet for new cloud-based applications to take advantage of the cost savings and performance optimization that cloud services provide.</span><span class="sxs-lookup"><span data-stu-id="862f6-120">We will not get into detail about the differences between these two except that Azure SQL database is your best bet for new cloud-based applications to take advantage of the cost savings and performance optimization that cloud services provide.</span></span> <span data-ttu-id="862f6-121">If you are considering migrating or extending your on-premises applications to the cloud, SQL server on Azure virtual machine might work out better for you.</span><span class="sxs-lookup"><span data-stu-id="862f6-121">If you are considering migrating or extending your on-premises applications to the cloud, SQL server on Azure virtual machine might work out better for you.</span></span> <span data-ttu-id="862f6-122">To keep things simple for this article, let's create an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="862f6-122">To keep things simple for this article, let's create an Azure SQL database.</span></span> 

## <a id="ODBC"></a><span data-ttu-id="862f6-123">Data access technologies: ODBC and OLE DB</span><span class="sxs-lookup"><span data-stu-id="862f6-123">Data access technologies: ODBC and OLE DB</span></span>
<span data-ttu-id="862f6-124">Connecting to Azure SQL DB is no different and currently there are two ways to connect to databases: ODBC (Open Database connectivity) and OLE DB (Object Linking and Embedding database).</span><span class="sxs-lookup"><span data-stu-id="862f6-124">Connecting to Azure SQL DB is no different and currently there are two ways to connect to databases: ODBC (Open Database connectivity) and OLE DB (Object Linking and Embedding database).</span></span> <span data-ttu-id="862f6-125">In recent years, Microsoft has aligned with [ODBC for native relational data access](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/).</span><span class="sxs-lookup"><span data-stu-id="862f6-125">In recent years, Microsoft has aligned with [ODBC for native relational data access](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/).</span></span> <span data-ttu-id="862f6-126">ODBC is relatively simple, and also much faster than OLE DB.</span><span class="sxs-lookup"><span data-stu-id="862f6-126">ODBC is relatively simple, and also much faster than OLE DB.</span></span> <span data-ttu-id="862f6-127">The only caveat here is that ODBC does use an old C-style API.</span><span class="sxs-lookup"><span data-stu-id="862f6-127">The only caveat here is that ODBC does use an old C-style API.</span></span> 

## <a id="Create"></a><span data-ttu-id="862f6-128">Step 1:  Creating your Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="862f6-128">Step 1:  Creating your Azure SQL Database</span></span>
<span data-ttu-id="862f6-129">See the [getting started page](sql-database-get-started-portal.md) to learn how to create a sample database.</span><span class="sxs-lookup"><span data-stu-id="862f6-129">See the [getting started page](sql-database-get-started-portal.md) to learn how to create a sample database.</span></span>  <span data-ttu-id="862f6-130">Alternatively, you can follow this [short two-minute video](https://azure.microsoft.com/documentation/videos/azure-sql-database-create-dbs-in-seconds/) to create an Azure SQL database using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="862f6-130">Alternatively, you can follow this [short two-minute video](https://azure.microsoft.com/documentation/videos/azure-sql-database-create-dbs-in-seconds/) to create an Azure SQL database using the Azure portal.</span></span>

## <a id="ConnectionString"></a><span data-ttu-id="862f6-131">Step 2:  Get connection string</span><span class="sxs-lookup"><span data-stu-id="862f6-131">Step 2:  Get connection string</span></span>
<span data-ttu-id="862f6-132">After your Azure SQL database has been provisioned, you need to carry out the following steps to determine connection information and add your client IP for firewall access.</span><span class="sxs-lookup"><span data-stu-id="862f6-132">After your Azure SQL database has been provisioned, you need to carry out the following steps to determine connection information and add your client IP for firewall access.</span></span> 

<span data-ttu-id="862f6-133">In [Azure portal](https://portal.azure.com/), go to your Azure SQL database ODBC connection string by using the **Show database connection strings** listed as a part of the overview section for your database:</span><span class="sxs-lookup"><span data-stu-id="862f6-133">In [Azure portal](https://portal.azure.com/), go to your Azure SQL database ODBC connection string by using the **Show database connection strings** listed as a part of the overview section for your database:</span></span> 

![ODBCConnectionString](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-develop-cplusplus-simple/azureportal.png)

![ODBCConnectionStringProps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-develop-cplusplus-simple/dbconnection.png)

<span data-ttu-id="862f6-136">Copy the contents of the **ODBC (Includes Node.js) [SQL authentication]** string.</span><span class="sxs-lookup"><span data-stu-id="862f6-136">Copy the contents of the **ODBC (Includes Node.js) [SQL authentication]** string.</span></span> <span data-ttu-id="862f6-137">We use this string later to connect from our C++ ODBC command-line interpreter.</span><span class="sxs-lookup"><span data-stu-id="862f6-137">We use this string later to connect from our C++ ODBC command-line interpreter.</span></span> <span data-ttu-id="862f6-138">This string provides details such as the driver, server, and other database connection parameters.</span><span class="sxs-lookup"><span data-stu-id="862f6-138">This string provides details such as the driver, server, and other database connection parameters.</span></span> 

## <a id="Firewall"></a><span data-ttu-id="862f6-139">Step 3:  Add your IP to the firewall</span><span class="sxs-lookup"><span data-stu-id="862f6-139">Step 3:  Add your IP to the firewall</span></span>
<span data-ttu-id="862f6-140">Go to the firewall section for your Database server and add your [client IP to the firewall using these steps](sql-database-configure-firewall-settings.md) to make sure we can establish a successful connection:</span><span class="sxs-lookup"><span data-stu-id="862f6-140">Go to the firewall section for your Database server and add your [client IP to the firewall using these steps](sql-database-configure-firewall-settings.md) to make sure we can establish a successful connection:</span></span> 

![AddyourIPWindow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-develop-cplusplus-simple/ip.png)

<span data-ttu-id="862f6-142">At this point, you have configured your Azure SQL DB and are ready to connect from your C++ code.</span><span class="sxs-lookup"><span data-stu-id="862f6-142">At this point, you have configured your Azure SQL DB and are ready to connect from your C++ code.</span></span> 

## <a id="Windows"></a><span data-ttu-id="862f6-143">Step 4: Connecting from a Windows C/C++ application</span><span class="sxs-lookup"><span data-stu-id="862f6-143">Step 4: Connecting from a Windows C/C++ application</span></span>
<span data-ttu-id="862f6-144">You can easily connect to your [Azure SQL DB using ODBC on Windows using this sample](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29) that builds with Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="862f6-144">You can easily connect to your [Azure SQL DB using ODBC on Windows using this sample](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29) that builds with Visual Studio.</span></span> <span data-ttu-id="862f6-145">The sample implements an ODBC command-line interpreter that can be used to connect to our Azure SQL DB.</span><span class="sxs-lookup"><span data-stu-id="862f6-145">The sample implements an ODBC command-line interpreter that can be used to connect to our Azure SQL DB.</span></span> <span data-ttu-id="862f6-146">This sample takes either a Database source name file (DSN) file as a command-line argument or the verbose connection string that we copied earlier from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="862f6-146">This sample takes either a Database source name file (DSN) file as a command-line argument or the verbose connection string that we copied earlier from the Azure portal.</span></span> <span data-ttu-id="862f6-147">Bring up the property page for this project and paste the connection string as a command argument as shown here:</span><span class="sxs-lookup"><span data-stu-id="862f6-147">Bring up the property page for this project and paste the connection string as a command argument as shown here:</span></span> 

![DSN Propsfile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-develop-cplusplus-simple/props.png)

<span data-ttu-id="862f6-149">Make sure you provide the right authentication details for your database as a part of that database connection string.</span><span class="sxs-lookup"><span data-stu-id="862f6-149">Make sure you provide the right authentication details for your database as a part of that database connection string.</span></span> 

<span data-ttu-id="862f6-150">Launch the application to build it.</span><span class="sxs-lookup"><span data-stu-id="862f6-150">Launch the application to build it.</span></span> <span data-ttu-id="862f6-151">You should see the following window validating a successful connection.</span><span class="sxs-lookup"><span data-stu-id="862f6-151">You should see the following window validating a successful connection.</span></span> <span data-ttu-id="862f6-152">You can even run some basic SQL commands like **create table** to validate your database connectivity:</span><span class="sxs-lookup"><span data-stu-id="862f6-152">You can even run some basic SQL commands like **create table** to validate your database connectivity:</span></span>

![SQL Commands](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-develop-cplusplus-simple/sqlcommands.png)

<span data-ttu-id="862f6-154">Alternatively, you could create a DSN file using the wizard that is launched when no command arguments are provided.</span><span class="sxs-lookup"><span data-stu-id="862f6-154">Alternatively, you could create a DSN file using the wizard that is launched when no command arguments are provided.</span></span> <span data-ttu-id="862f6-155">We recommend that you try this option as well.</span><span class="sxs-lookup"><span data-stu-id="862f6-155">We recommend that you try this option as well.</span></span> <span data-ttu-id="862f6-156">You can use this DSN file for automation and protecting your authentication settings:</span><span class="sxs-lookup"><span data-stu-id="862f6-156">You can use this DSN file for automation and protecting your authentication settings:</span></span> 

![Create DSN File](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-develop-cplusplus-simple/datasource.png)

<span data-ttu-id="862f6-158">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="862f6-158">Congratulations!</span></span> <span data-ttu-id="862f6-159">You have now successfully connected to Azure SQL using C++ and ODBC on Windows.</span><span class="sxs-lookup"><span data-stu-id="862f6-159">You have now successfully connected to Azure SQL using C++ and ODBC on Windows.</span></span> <span data-ttu-id="862f6-160">You can continue reading to do the same for Linux platform as well.</span><span class="sxs-lookup"><span data-stu-id="862f6-160">You can continue reading to do the same for Linux platform as well.</span></span> 

## <a id="Linux"></a><span data-ttu-id="862f6-161">Step 5: Connecting from a Linux C/C++ application</span><span class="sxs-lookup"><span data-stu-id="862f6-161">Step 5: Connecting from a Linux C/C++ application</span></span>
<span data-ttu-id="862f6-162">In case you haven’t heard the news yet, Visual Studio now allows you to develop C++ Linux application as well.</span><span class="sxs-lookup"><span data-stu-id="862f6-162">In case you haven’t heard the news yet, Visual Studio now allows you to develop C++ Linux application as well.</span></span> <span data-ttu-id="862f6-163">You can read about this new scenario in the [Visual C++ for Linux Development](https://blogs.msdn.microsoft.com/vcblog/2016/03/30/visual-c-for-linux-development/) blog.</span><span class="sxs-lookup"><span data-stu-id="862f6-163">You can read about this new scenario in the [Visual C++ for Linux Development](https://blogs.msdn.microsoft.com/vcblog/2016/03/30/visual-c-for-linux-development/) blog.</span></span> <span data-ttu-id="862f6-164">To build for Linux, you need a remote machine where your Linux distro is running.</span><span class="sxs-lookup"><span data-stu-id="862f6-164">To build for Linux, you need a remote machine where your Linux distro is running.</span></span> <span data-ttu-id="862f6-165">If you don’t have one available, you can set one up quickly using [Linux Azure Virtual machines](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="862f6-165">If you don’t have one available, you can set one up quickly using [Linux Azure Virtual machines](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="862f6-166">For this tutorial, let us assume that you have an Ubuntu 16.04 Linux distribution set up.</span><span class="sxs-lookup"><span data-stu-id="862f6-166">For this tutorial, let us assume that you have an Ubuntu 16.04 Linux distribution set up.</span></span> <span data-ttu-id="862f6-167">The steps here should also apply to Ubuntu 15.10, Red Hat 6, and Red Hat 7.</span><span class="sxs-lookup"><span data-stu-id="862f6-167">The steps here should also apply to Ubuntu 15.10, Red Hat 6, and Red Hat 7.</span></span> 

<span data-ttu-id="862f6-168">The following steps install the libraries needed for SQL and ODBC for your distro:</span><span class="sxs-lookup"><span data-stu-id="862f6-168">The following steps install the libraries needed for SQL and ODBC for your distro:</span></span>

    sudo su
    sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/mssql-ubuntu-test/ xenial main" > /etc/apt/sources.list.d/mssqlpreview.list'
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    apt-get update
    apt-get install msodbcsql
    apt-get install unixodbc-dev-utf16 #this step is optional but recommended*

<span data-ttu-id="862f6-169">Launch Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="862f6-169">Launch Visual Studio.</span></span> <span data-ttu-id="862f6-170">Under Tools -> Options -> Cross Platform -> Connection Manager, add a connection to your Linux box:</span><span class="sxs-lookup"><span data-stu-id="862f6-170">Under Tools -> Options -> Cross Platform -> Connection Manager, add a connection to your Linux box:</span></span> 

![Tools Options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-develop-cplusplus-simple/tools.png)

<span data-ttu-id="862f6-172">After connection over SSH is established, create an Empty project (Linux) template:</span><span class="sxs-lookup"><span data-stu-id="862f6-172">After connection over SSH is established, create an Empty project (Linux) template:</span></span> 

![New project template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-develop-cplusplus-simple/template.png)

<span data-ttu-id="862f6-174">You can then add a [new C source file and replace it with this content](https://github.com/Microsoft/VCSamples/blob/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29/odbcconnector/odbcconnector.c).</span><span class="sxs-lookup"><span data-stu-id="862f6-174">You can then add a [new C source file and replace it with this content](https://github.com/Microsoft/VCSamples/blob/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29/odbcconnector/odbcconnector.c).</span></span> <span data-ttu-id="862f6-175">Using the ODBC APIs SQLAllocHandle, SQLSetConnectAttr, and SQLDriverConnect, you should be able to initialize and establish a connection to your database.</span><span class="sxs-lookup"><span data-stu-id="862f6-175">Using the ODBC APIs SQLAllocHandle, SQLSetConnectAttr, and SQLDriverConnect, you should be able to initialize and establish a connection to your database.</span></span> <span data-ttu-id="862f6-176">Like with the Windows ODBC sample, you need to replace the SQLDriverConnect call with the details from your database connection string parameters copied from the Azure portal previously.</span><span class="sxs-lookup"><span data-stu-id="862f6-176">Like with the Windows ODBC sample, you need to replace the SQLDriverConnect call with the details from your database connection string parameters copied from the Azure portal previously.</span></span> 

     retcode = SQLDriverConnect(
        hdbc, NULL, "Driver=ODBC Driver 13 for SQL"
                    "Server;Server=<yourserver>;Uid=<yourusername>;Pwd=<"
                    "yourpassword>;database=<yourdatabase>",
        SQL_NTS, outstr, sizeof(outstr), &outstrlen, SQL_DRIVER_NOPROMPT);

<span data-ttu-id="862f6-177">The last thing to do before compiling is to add **odbc** as a library dependency:</span><span class="sxs-lookup"><span data-stu-id="862f6-177">The last thing to do before compiling is to add **odbc** as a library dependency:</span></span> 

![Adding ODBC as an input library](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-develop-cplusplus-simple/lib.png)

<span data-ttu-id="862f6-179">To launch your application, bring up the Linux Console from the **Debug** menu:</span><span class="sxs-lookup"><span data-stu-id="862f6-179">To launch your application, bring up the Linux Console from the **Debug** menu:</span></span> 

![Linux Console](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-develop-cplusplus-simple/linuxconsole.png)

<span data-ttu-id="862f6-181">If your connection was successful, you should now see the current database name printed in the Linux Console:</span><span class="sxs-lookup"><span data-stu-id="862f6-181">If your connection was successful, you should now see the current database name printed in the Linux Console:</span></span> 

![Linux Console Window Output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-develop-cplusplus-simple/linuxconsolewindow.png)

<span data-ttu-id="862f6-183">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="862f6-183">Congratulations!</span></span> <span data-ttu-id="862f6-184">You have successfully completed the tutorial and can now connect to your Azure SQL DB from C++ on Windows and Linux platforms.</span><span class="sxs-lookup"><span data-stu-id="862f6-184">You have successfully completed the tutorial and can now connect to your Azure SQL DB from C++ on Windows and Linux platforms.</span></span>

## <a id="GetSolution"></a><span data-ttu-id="862f6-185">Get the complete C/C++ tutorial solution</span><span class="sxs-lookup"><span data-stu-id="862f6-185">Get the complete C/C++ tutorial solution</span></span>
<span data-ttu-id="862f6-186">You can find the GetStarted solution that contains all the samples in this article at github:</span><span class="sxs-lookup"><span data-stu-id="862f6-186">You can find the GetStarted solution that contains all the samples in this article at github:</span></span>

* <span data-ttu-id="862f6-187">[ODBC C++ Windows sample](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29), Download the Windows C++ ODBC Sample to connect to Azure SQL</span><span class="sxs-lookup"><span data-stu-id="862f6-187">[ODBC C++ Windows sample](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29), Download the Windows C++ ODBC Sample to connect to Azure SQL</span></span>
* <span data-ttu-id="862f6-188">[ODBC C++ Linux sample](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29), Download the Linux C++ ODBC Sample to connect to Azure SQL</span><span class="sxs-lookup"><span data-stu-id="862f6-188">[ODBC C++ Linux sample](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29), Download the Linux C++ ODBC Sample to connect to Azure SQL</span></span>

## <a name="next-steps"></a><span data-ttu-id="862f6-189">Next steps</span><span class="sxs-lookup"><span data-stu-id="862f6-189">Next steps</span></span>
* <span data-ttu-id="862f6-190">Review the [SQL Database Development Overview](sql-database-develop-overview.md)</span><span class="sxs-lookup"><span data-stu-id="862f6-190">Review the [SQL Database Development Overview](sql-database-develop-overview.md)</span></span>
* <span data-ttu-id="862f6-191">More information on the [ODBC API Reference](https://docs.microsoft.com/sql/odbc/reference/syntax/odbc-api-reference/)</span><span class="sxs-lookup"><span data-stu-id="862f6-191">More information on the [ODBC API Reference](https://docs.microsoft.com/sql/odbc/reference/syntax/odbc-api-reference/)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="862f6-192">Additional resources</span><span class="sxs-lookup"><span data-stu-id="862f6-192">Additional resources</span></span>
* [<span data-ttu-id="862f6-193">Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="862f6-193">Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database</span></span>](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* <span data-ttu-id="862f6-194">Explore all the [capabilities of SQL Database](https://azure.microsoft.com/services/sql-database/)</span><span class="sxs-lookup"><span data-stu-id="862f6-194">Explore all the [capabilities of SQL Database](https://azure.microsoft.com/services/sql-database/)</span></span>












