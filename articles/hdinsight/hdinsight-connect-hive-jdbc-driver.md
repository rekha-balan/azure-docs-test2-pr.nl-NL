---
title: Use JDBC to query Hive on Azure HDInsight
description: Learn how to use JDBC to connect to Hive on Azure HDInsight and remotely run queries on data stored in the cloud.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 928f8d2a-684d-48cb-894c-11c59a5599ae
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/13/2017
ms.author: larryfr
ms.openlocfilehash: 803e55c033e53d1a2552ff16fab6ee378be36ebc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563382"
---
# <a name="connect-to-hive-on-azure-hdinsight-using-the-hive-jdbc-driver"></a><span data-ttu-id="15ea3-103">Connect to Hive on Azure HDInsight using the Hive JDBC driver</span><span class="sxs-lookup"><span data-stu-id="15ea3-103">Connect to Hive on Azure HDInsight using the Hive JDBC driver</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="15ea3-104">In this document, you will learn how to use JDBC from a Java application to remotely submit Hive queries to an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="15ea3-104">In this document, you will learn how to use JDBC from a Java application to remotely submit Hive queries to an HDInsight cluster.</span></span> <span data-ttu-id="15ea3-105">You will learn how to connect from the SQuirreL SQL client, and how to connect programmatically from Java.</span><span class="sxs-lookup"><span data-stu-id="15ea3-105">You will learn how to connect from the SQuirreL SQL client, and how to connect programmatically from Java.</span></span>

<span data-ttu-id="15ea3-106">For more information on the Hive JDBC Interface, see [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span><span class="sxs-lookup"><span data-stu-id="15ea3-106">For more information on the Hive JDBC Interface, see [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15ea3-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="15ea3-107">Prerequisites</span></span>

<span data-ttu-id="15ea3-108">To complete the steps in this article, you will need the following:</span><span class="sxs-lookup"><span data-stu-id="15ea3-108">To complete the steps in this article, you will need the following:</span></span>

* <span data-ttu-id="15ea3-109">A Hadoop on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="15ea3-109">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="15ea3-110">Either Linux-based or Windows-based clusters will work.</span><span class="sxs-lookup"><span data-stu-id="15ea3-110">Either Linux-based or Windows-based clusters will work.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="15ea3-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="15ea3-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="15ea3-112">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="15ea3-112">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

* <span data-ttu-id="15ea3-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span><span class="sxs-lookup"><span data-stu-id="15ea3-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span></span> <span data-ttu-id="15ea3-114">SQuirreL is a JDBC client application.</span><span class="sxs-lookup"><span data-stu-id="15ea3-114">SQuirreL is a JDBC client application.</span></span>

<span data-ttu-id="15ea3-115">To build and run the example Java application linked from this article, you will need the following.</span><span class="sxs-lookup"><span data-stu-id="15ea3-115">To build and run the example Java application linked from this article, you will need the following.</span></span>

* <span data-ttu-id="15ea3-116">The [Java Developer Kit (JDK) version 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span><span class="sxs-lookup"><span data-stu-id="15ea3-116">The [Java Developer Kit (JDK) version 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span>
* <span data-ttu-id="15ea3-117">[Apache Maven](https://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="15ea3-117">[Apache Maven](https://maven.apache.org).</span></span> <span data-ttu-id="15ea3-118">Maven is a project build system for Java projects that is used by the project associated with this article.</span><span class="sxs-lookup"><span data-stu-id="15ea3-118">Maven is a project build system for Java projects that is used by the project associated with this article.</span></span>

## <a name="connection-string"></a><span data-ttu-id="15ea3-119">Connection string</span><span class="sxs-lookup"><span data-stu-id="15ea3-119">Connection string</span></span>

<span data-ttu-id="15ea3-120">JDBC connections to an HDInsight cluster on Azure are made over 443, and the traffic is secured using SSL.</span><span class="sxs-lookup"><span data-stu-id="15ea3-120">JDBC connections to an HDInsight cluster on Azure are made over 443, and the traffic is secured using SSL.</span></span> <span data-ttu-id="15ea3-121">The public gateway that the clusters sit behind redirects the traffic to the port that HiveServer2 is actually listening on.</span><span class="sxs-lookup"><span data-stu-id="15ea3-121">The public gateway that the clusters sit behind redirects the traffic to the port that HiveServer2 is actually listening on.</span></span> <span data-ttu-id="15ea3-122">So a typical connection string would like the following:</span><span class="sxs-lookup"><span data-stu-id="15ea3-122">So a typical connection string would like the following:</span></span>

    jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;ssl=true?hive.server2.transport.mode=http;hive.server2.thrift.http.path=/hive2

<span data-ttu-id="15ea3-123">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="15ea3-123">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>

## <a name="authentication"></a><span data-ttu-id="15ea3-124">Authentication</span><span class="sxs-lookup"><span data-stu-id="15ea3-124">Authentication</span></span>

<span data-ttu-id="15ea3-125">When establishing the connection, you must use the HDInsight cluster admin name and password to authenticate to the cluster gateway.</span><span class="sxs-lookup"><span data-stu-id="15ea3-125">When establishing the connection, you must use the HDInsight cluster admin name and password to authenticate to the cluster gateway.</span></span> <span data-ttu-id="15ea3-126">When connecting from JDBC clients such as SQuirreL SQL, you must enter the admin name and password in client settings.</span><span class="sxs-lookup"><span data-stu-id="15ea3-126">When connecting from JDBC clients such as SQuirreL SQL, you must enter the admin name and password in client settings.</span></span>

<span data-ttu-id="15ea3-127">From a Java application, you must use the name and password when establishing a connection.</span><span class="sxs-lookup"><span data-stu-id="15ea3-127">From a Java application, you must use the name and password when establishing a connection.</span></span> <span data-ttu-id="15ea3-128">For example, the following Java code opens a new connection using the connection string, admin name, and password:</span><span class="sxs-lookup"><span data-stu-id="15ea3-128">For example, the following Java code opens a new connection using the connection string, admin name, and password:</span></span>

```java
DriverManager.getConnection(connectionString,clusterAdmin,clusterPassword);
```

## <a name="connect-with-squirrel-sql-client"></a><span data-ttu-id="15ea3-129">Connect with SQuirreL SQL client</span><span class="sxs-lookup"><span data-stu-id="15ea3-129">Connect with SQuirreL SQL client</span></span>

<span data-ttu-id="15ea3-130">SQuirreL SQL is a JDBC client that can be used to remotely run Hive queries with your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="15ea3-130">SQuirreL SQL is a JDBC client that can be used to remotely run Hive queries with your HDInsight cluster.</span></span> <span data-ttu-id="15ea3-131">The following steps assume that you have already installed SQuirreL SQL, and will walk you through downloading and configuring the drivers for Hive.</span><span class="sxs-lookup"><span data-stu-id="15ea3-131">The following steps assume that you have already installed SQuirreL SQL, and will walk you through downloading and configuring the drivers for Hive.</span></span>

1. <span data-ttu-id="15ea3-132">Copy the Hive JDBC drivers from your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="15ea3-132">Copy the Hive JDBC drivers from your HDInsight cluster.</span></span>

    * <span data-ttu-id="15ea3-133">For **Linux-based HDInsight**, use the following steps to download the required jar files.</span><span class="sxs-lookup"><span data-stu-id="15ea3-133">For **Linux-based HDInsight**, use the following steps to download the required jar files.</span></span>

        1. <span data-ttu-id="15ea3-134">Create a new directory that will contain the files.</span><span class="sxs-lookup"><span data-stu-id="15ea3-134">Create a new directory that will contain the files.</span></span> <span data-ttu-id="15ea3-135">For example, `mkdir hivedriver`.</span><span class="sxs-lookup"><span data-stu-id="15ea3-135">For example, `mkdir hivedriver`.</span></span>
        2. <span data-ttu-id="15ea3-136">From a command prompt, Bash, PowerShell or other command-line prompt, change directories to the new directory and use the following commands to copy the files from the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="15ea3-136">From a command prompt, Bash, PowerShell or other command-line prompt, change directories to the new directory and use the following commands to copy the files from the HDInsight cluster.</span></span>

                scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/hive-jdbc*standalone.jar .
                scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-common.jar .
                scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-auth.jar .

            <span data-ttu-id="15ea3-137">Replace **USERNAME** with the SSH user account name for the cluster.</span><span class="sxs-lookup"><span data-stu-id="15ea3-137">Replace **USERNAME** with the SSH user account name for the cluster.</span></span> <span data-ttu-id="15ea3-138">Replace **CLUSTERNAME** with the HDInsight cluster name.</span><span class="sxs-lookup"><span data-stu-id="15ea3-138">Replace **CLUSTERNAME** with the HDInsight cluster name.</span></span>

        > [!NOTE]
        > <span data-ttu-id="15ea3-139">On Windows environments, you may not have the `scp` command.</span><span class="sxs-lookup"><span data-stu-id="15ea3-139">On Windows environments, you may not have the `scp` command.</span></span> <span data-ttu-id="15ea3-140">If so, use the PSCP utility instead.</span><span class="sxs-lookup"><span data-stu-id="15ea3-140">If so, use the PSCP utility instead.</span></span> <span data-ttu-id="15ea3-141">You can download it from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="15ea3-141">You can download it from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

    * <span data-ttu-id="15ea3-142">For **Windows-based HDInsight**, use the following steps to download the jar files.</span><span class="sxs-lookup"><span data-stu-id="15ea3-142">For **Windows-based HDInsight**, use the following steps to download the jar files.</span></span>

        1. <span data-ttu-id="15ea3-143">From the Azure portal, select your HDInsight cluster, and then select the **Remote Desktop** icon.</span><span class="sxs-lookup"><span data-stu-id="15ea3-143">From the Azure portal, select your HDInsight cluster, and then select the **Remote Desktop** icon.</span></span>

            ![Remote Desktop icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-connect-hive-jdbc-driver/remotedesktopicon.png)

        2. <span data-ttu-id="15ea3-145">On the Remote Desktop blade, use the **Connect** button to connect to the cluster.</span><span class="sxs-lookup"><span data-stu-id="15ea3-145">On the Remote Desktop blade, use the **Connect** button to connect to the cluster.</span></span> <span data-ttu-id="15ea3-146">If the Remote Desktop is not enabled, use the form to provide a user name and password, then select **Enable** to enable Remote Desktop for the cluster.</span><span class="sxs-lookup"><span data-stu-id="15ea3-146">If the Remote Desktop is not enabled, use the form to provide a user name and password, then select **Enable** to enable Remote Desktop for the cluster.</span></span>

            ![Remote desktop blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-connect-hive-jdbc-driver/remotedesktopblade.png)

            <span data-ttu-id="15ea3-148">After selecting **Connect**, a .rdp file will be downloaded.</span><span class="sxs-lookup"><span data-stu-id="15ea3-148">After selecting **Connect**, a .rdp file will be downloaded.</span></span> <span data-ttu-id="15ea3-149">Use this file to launch the Remote Desktop client.</span><span class="sxs-lookup"><span data-stu-id="15ea3-149">Use this file to launch the Remote Desktop client.</span></span> <span data-ttu-id="15ea3-150">When prompted, use the user name and password you entered for Remote Desktop access.</span><span class="sxs-lookup"><span data-stu-id="15ea3-150">When prompted, use the user name and password you entered for Remote Desktop access.</span></span>

        3. <span data-ttu-id="15ea3-151">Once connected, copy the following files from the Remote Desktop session to your local machine.</span><span class="sxs-lookup"><span data-stu-id="15ea3-151">Once connected, copy the following files from the Remote Desktop session to your local machine.</span></span> <span data-ttu-id="15ea3-152">Put them in a local directory named `hivedriver`.</span><span class="sxs-lookup"><span data-stu-id="15ea3-152">Put them in a local directory named `hivedriver`.</span></span>

            * <span data-ttu-id="15ea3-153">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar</span><span class="sxs-lookup"><span data-stu-id="15ea3-153">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar</span></span>
            * <span data-ttu-id="15ea3-154">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar</span><span class="sxs-lookup"><span data-stu-id="15ea3-154">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar</span></span>
            * <span data-ttu-id="15ea3-155">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar</span><span class="sxs-lookup"><span data-stu-id="15ea3-155">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar</span></span>

            > [!NOTE]
            > <span data-ttu-id="15ea3-156">The version numbers included in the paths and file names may be different for your cluster.</span><span class="sxs-lookup"><span data-stu-id="15ea3-156">The version numbers included in the paths and file names may be different for your cluster.</span></span>

        4. <span data-ttu-id="15ea3-157">Disconnect the Remote Desktop session once you have finished copying the files.</span><span class="sxs-lookup"><span data-stu-id="15ea3-157">Disconnect the Remote Desktop session once you have finished copying the files.</span></span>

2. <span data-ttu-id="15ea3-158">Start the SQuirreL SQL application.</span><span class="sxs-lookup"><span data-stu-id="15ea3-158">Start the SQuirreL SQL application.</span></span> <span data-ttu-id="15ea3-159">From the left of the window, select **Drivers**.</span><span class="sxs-lookup"><span data-stu-id="15ea3-159">From the left of the window, select **Drivers**.</span></span>

    ![Drivers tab on the left of the window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-connect-hive-jdbc-driver/squirreldrivers.png)

3. <span data-ttu-id="15ea3-161">From the icons at the top of the **Drivers** dialog, select the **+** icon to create a new driver.</span><span class="sxs-lookup"><span data-stu-id="15ea3-161">From the icons at the top of the **Drivers** dialog, select the **+** icon to create a new driver.</span></span>

    ![Drivers icons](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-connect-hive-jdbc-driver/driversicons.png)

4. <span data-ttu-id="15ea3-163">In the Add Driver dialog, add the following information.</span><span class="sxs-lookup"><span data-stu-id="15ea3-163">In the Add Driver dialog, add the following information.</span></span>

    * <span data-ttu-id="15ea3-164">**Name**: Hive</span><span class="sxs-lookup"><span data-stu-id="15ea3-164">**Name**: Hive</span></span>
    * <span data-ttu-id="15ea3-165">**Example URL**: `jdbc:hive2://localhost:443/default;ssl=true?hive.server2.transport.mode=http;hive.server2.thrift.http.path=/hive2`</span><span class="sxs-lookup"><span data-stu-id="15ea3-165">**Example URL**: `jdbc:hive2://localhost:443/default;ssl=true?hive.server2.transport.mode=http;hive.server2.thrift.http.path=/hive2`</span></span>
    * <span data-ttu-id="15ea3-166">**Extra Class Path**: Use the Add button to add the jar files downloaded earlier</span><span class="sxs-lookup"><span data-stu-id="15ea3-166">**Extra Class Path**: Use the Add button to add the jar files downloaded earlier</span></span>
    * <span data-ttu-id="15ea3-167">**Class Name**: org.apache.hive.jdbc.HiveDriver</span><span class="sxs-lookup"><span data-stu-id="15ea3-167">**Class Name**: org.apache.hive.jdbc.HiveDriver</span></span>

   ![add driver dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-connect-hive-jdbc-driver/adddriver.png)

   <span data-ttu-id="15ea3-169">Click **OK** to save these settings.</span><span class="sxs-lookup"><span data-stu-id="15ea3-169">Click **OK** to save these settings.</span></span>

5. <span data-ttu-id="15ea3-170">On the left of the SQuirreL SQL window, select **Aliases**.</span><span class="sxs-lookup"><span data-stu-id="15ea3-170">On the left of the SQuirreL SQL window, select **Aliases**.</span></span> <span data-ttu-id="15ea3-171">Then click the **+** icon to create a new connection alias.</span><span class="sxs-lookup"><span data-stu-id="15ea3-171">Then click the **+** icon to create a new connection alias.</span></span>

    ![add new alias](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-connect-hive-jdbc-driver/aliases.png)

6. <span data-ttu-id="15ea3-173">Use the following values for the **Add Alias** dialog.</span><span class="sxs-lookup"><span data-stu-id="15ea3-173">Use the following values for the **Add Alias** dialog.</span></span>

    * <span data-ttu-id="15ea3-174">**Name**: Hive on HDInsight</span><span class="sxs-lookup"><span data-stu-id="15ea3-174">**Name**: Hive on HDInsight</span></span>

    * <span data-ttu-id="15ea3-175">**Driver**: Use the dropdown to select the **Hive** driver</span><span class="sxs-lookup"><span data-stu-id="15ea3-175">**Driver**: Use the dropdown to select the **Hive** driver</span></span>

    * <span data-ttu-id="15ea3-176">**URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;ssl=true?hive.server2.transport.mode=http;hive.server2.thrift.http.path=/hive2</span><span class="sxs-lookup"><span data-stu-id="15ea3-176">**URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;ssl=true?hive.server2.transport.mode=http;hive.server2.thrift.http.path=/hive2</span></span>

        <span data-ttu-id="15ea3-177">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="15ea3-177">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>

    * <span data-ttu-id="15ea3-178">**User Name**: The cluster login account name for your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="15ea3-178">**User Name**: The cluster login account name for your HDInsight cluster.</span></span> <span data-ttu-id="15ea3-179">The default is `admin`.</span><span class="sxs-lookup"><span data-stu-id="15ea3-179">The default is `admin`.</span></span>

    * <span data-ttu-id="15ea3-180">**Password**: The password for the cluster login account.</span><span class="sxs-lookup"><span data-stu-id="15ea3-180">**Password**: The password for the cluster login account.</span></span> <span data-ttu-id="15ea3-181">This is a password you provided when creating the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="15ea3-181">This is a password you provided when creating the HDInsight cluster.</span></span>

    ![add alias dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-connect-hive-jdbc-driver/addalias.png)

    <span data-ttu-id="15ea3-183">Use the **Test** button to verify that the connection works.</span><span class="sxs-lookup"><span data-stu-id="15ea3-183">Use the **Test** button to verify that the connection works.</span></span> <span data-ttu-id="15ea3-184">When **Connect to: Hive on HDInsight** dialog appears, select **Connect** to perform the test.</span><span class="sxs-lookup"><span data-stu-id="15ea3-184">When **Connect to: Hive on HDInsight** dialog appears, select **Connect** to perform the test.</span></span> <span data-ttu-id="15ea3-185">If the test succeeds, you will see a **Connection successful** dialog.</span><span class="sxs-lookup"><span data-stu-id="15ea3-185">If the test succeeds, you will see a **Connection successful** dialog.</span></span>

    <span data-ttu-id="15ea3-186">Use the **Ok** button at the bottom of the **Add Alias** dialog to save the connection alias.</span><span class="sxs-lookup"><span data-stu-id="15ea3-186">Use the **Ok** button at the bottom of the **Add Alias** dialog to save the connection alias.</span></span>

7. <span data-ttu-id="15ea3-187">From the **Connect to** dropdown at the top of SQuirreL SQL, select **Hive on HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="15ea3-187">From the **Connect to** dropdown at the top of SQuirreL SQL, select **Hive on HDInsight**.</span></span> <span data-ttu-id="15ea3-188">When prompted, select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="15ea3-188">When prompted, select **Connect**.</span></span>

    ![connection dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-connect-hive-jdbc-driver/connect.png)

8. <span data-ttu-id="15ea3-190">Once connected, enter the following query into the SQL query dialog, and then select the **Run** icon.</span><span class="sxs-lookup"><span data-stu-id="15ea3-190">Once connected, enter the following query into the SQL query dialog, and then select the **Run** icon.</span></span> <span data-ttu-id="15ea3-191">The results area should show the results of the query.</span><span class="sxs-lookup"><span data-stu-id="15ea3-191">The results area should show the results of the query.</span></span>

        select * from hivesampletable limit 10;

    ![sql query dialog, including results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-connect-hive-jdbc-driver/sqlquery.png)

## <a name="connect-from-an-example-java-application"></a><span data-ttu-id="15ea3-193">Connect from an example Java application</span><span class="sxs-lookup"><span data-stu-id="15ea3-193">Connect from an example Java application</span></span>

<span data-ttu-id="15ea3-194">An example of using a Java client to query Hive on HDInsight is available at [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span><span class="sxs-lookup"><span data-stu-id="15ea3-194">An example of using a Java client to query Hive on HDInsight is available at [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span></span> <span data-ttu-id="15ea3-195">Follow the instructions in the repository to build and run the sample.</span><span class="sxs-lookup"><span data-stu-id="15ea3-195">Follow the instructions in the repository to build and run the sample.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="15ea3-196">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="15ea3-196">Troubleshooting</span></span>

### <a name="unexpected-error-occurred-attempting-to-open-an-sql-connection"></a><span data-ttu-id="15ea3-197">Unexpected Error occurred attempting to open an SQL connection</span><span class="sxs-lookup"><span data-stu-id="15ea3-197">Unexpected Error occurred attempting to open an SQL connection</span></span>

<span data-ttu-id="15ea3-198">**Symptoms**: When connecting to an HDInsight cluster that is version 3.3 or 3.4, you may receive an error that an unexpected error occurred.</span><span class="sxs-lookup"><span data-stu-id="15ea3-198">**Symptoms**: When connecting to an HDInsight cluster that is version 3.3 or 3.4, you may receive an error that an unexpected error occurred.</span></span> <span data-ttu-id="15ea3-199">The stack trace for this error will begin with the following lines:</span><span class="sxs-lookup"><span data-stu-id="15ea3-199">The stack trace for this error will begin with the following lines:</span></span>

```java
java.util.concurrent.ExecutionException: java.lang.RuntimeException: java.lang.NoSuchMethodError: org.apache.commons.codec.binary.Base64.<init>(I)V
at java.util.concurrent.FutureTas...(FutureTask.java:122)
at java.util.concurrent.FutureTask.get(FutureTask.java:206)
```

<span data-ttu-id="15ea3-200">**Cause**: This error is caused by a mismatch in the version of the commons-codec.jar file used by SQuirreL and the one required by the Hive JDBC components downloaded from the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="15ea3-200">**Cause**: This error is caused by a mismatch in the version of the commons-codec.jar file used by SQuirreL and the one required by the Hive JDBC components downloaded from the HDInsight cluster.</span></span>

<span data-ttu-id="15ea3-201">**Resolution**: To fix this error, use the following steps.</span><span class="sxs-lookup"><span data-stu-id="15ea3-201">**Resolution**: To fix this error, use the following steps.</span></span>

1. <span data-ttu-id="15ea3-202">Download the commons-codec jar file from your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="15ea3-202">Download the commons-codec jar file from your HDInsight cluster.</span></span>

        scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-codec*.jar ./commons-codec.jar

2. <span data-ttu-id="15ea3-203">Exit SQuirreL, and then go to the directory where SQuirreL is installed on your system.</span><span class="sxs-lookup"><span data-stu-id="15ea3-203">Exit SQuirreL, and then go to the directory where SQuirreL is installed on your system.</span></span> <span data-ttu-id="15ea3-204">In the SquirreL directory, under the `lib` directory, replace the existing commons-codec.jar with the one downloaded from the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="15ea3-204">In the SquirreL directory, under the `lib` directory, replace the existing commons-codec.jar with the one downloaded from the HDInsight cluster.</span></span>

3. <span data-ttu-id="15ea3-205">Restart SQuirreL.</span><span class="sxs-lookup"><span data-stu-id="15ea3-205">Restart SQuirreL.</span></span> <span data-ttu-id="15ea3-206">The error should no longer occur when connecting to Hive on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="15ea3-206">The error should no longer occur when connecting to Hive on HDInsight.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15ea3-207">Next steps</span><span class="sxs-lookup"><span data-stu-id="15ea3-207">Next steps</span></span>

<span data-ttu-id="15ea3-208">Now that you have learned how to use JDBC to work with Hive, use the following links to explore other ways to work with Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="15ea3-208">Now that you have learned how to use JDBC to work with Hive, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* [<span data-ttu-id="15ea3-209">Upload data to HDInsight</span><span class="sxs-lookup"><span data-stu-id="15ea3-209">Upload data to HDInsight</span></span>](hdinsight-upload-data.md)
* [<span data-ttu-id="15ea3-210">Use Hive with HDInsight</span><span class="sxs-lookup"><span data-stu-id="15ea3-210">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="15ea3-211">Use Pig with HDInsight</span><span class="sxs-lookup"><span data-stu-id="15ea3-211">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="15ea3-212">Use MapReduce jobs with HDInsight</span><span class="sxs-lookup"><span data-stu-id="15ea3-212">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)









