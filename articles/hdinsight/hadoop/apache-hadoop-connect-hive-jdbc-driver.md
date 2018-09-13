---
title: Query Hive through the JDBC driver - Azure HDInsight
description: Use the JDBC driver from a Java application to submit Hive queries to Hadoop on HDInsight. Connect programmatically and from the SQuirrel SQL client.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.topic: conceptual
ms.date: 04/02/2018
ms.author: jasonh
ms.openlocfilehash: da2b3484f80f7116664cf5a25c7de99da723f202
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856012"
---
# <a name="query-hive-through-the-jdbc-driver-in-hdinsight"></a><span data-ttu-id="076b6-104">Query Hive through the JDBC driver in HDInsight</span><span class="sxs-lookup"><span data-stu-id="076b6-104">Query Hive through the JDBC driver in HDInsight</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="076b6-105">Learn how to use the JDBC driver from a Java application to submit Hive queries to Hadoop in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="076b6-105">Learn how to use the JDBC driver from a Java application to submit Hive queries to Hadoop in Azure HDInsight.</span></span> <span data-ttu-id="076b6-106">The information in this document demonstrates how to connect programmatically and from the SQuirrel SQL client.</span><span class="sxs-lookup"><span data-stu-id="076b6-106">The information in this document demonstrates how to connect programmatically and from the SQuirrel SQL client.</span></span>

<span data-ttu-id="076b6-107">For more information on the Hive JDBC Interface, see [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span><span class="sxs-lookup"><span data-stu-id="076b6-107">For more information on the Hive JDBC Interface, see [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="076b6-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="076b6-108">Prerequisites</span></span>

* <span data-ttu-id="076b6-109">A Hadoop on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="076b6-109">A Hadoop on HDInsight cluster.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="076b6-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="076b6-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="076b6-111">For more information, see [HDInsight 3.3 retirement](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="076b6-111">For more information, see [HDInsight 3.3 retirement](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="076b6-112">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span><span class="sxs-lookup"><span data-stu-id="076b6-112">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span></span> <span data-ttu-id="076b6-113">SQuirreL is a JDBC client application.</span><span class="sxs-lookup"><span data-stu-id="076b6-113">SQuirreL is a JDBC client application.</span></span>

* <span data-ttu-id="076b6-114">The [Java Developer Kit (JDK) version 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span><span class="sxs-lookup"><span data-stu-id="076b6-114">The [Java Developer Kit (JDK) version 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span>

* <span data-ttu-id="076b6-115">[Apache Maven](https://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="076b6-115">[Apache Maven](https://maven.apache.org).</span></span> <span data-ttu-id="076b6-116">Maven is a project build system for Java projects that is used by the project associated with this article.</span><span class="sxs-lookup"><span data-stu-id="076b6-116">Maven is a project build system for Java projects that is used by the project associated with this article.</span></span>

## <a name="jdbc-connection-string"></a><span data-ttu-id="076b6-117">JDBC connection string</span><span class="sxs-lookup"><span data-stu-id="076b6-117">JDBC connection string</span></span>

<span data-ttu-id="076b6-118">JDBC connections to an HDInsight cluster on Azure are made over 443, and the traffic is secured using SSL.</span><span class="sxs-lookup"><span data-stu-id="076b6-118">JDBC connections to an HDInsight cluster on Azure are made over 443, and the traffic is secured using SSL.</span></span> <span data-ttu-id="076b6-119">The public gateway that the clusters sit behind redirects the traffic to the port that HiveServer2 is actually listening on.</span><span class="sxs-lookup"><span data-stu-id="076b6-119">The public gateway that the clusters sit behind redirects the traffic to the port that HiveServer2 is actually listening on.</span></span> <span data-ttu-id="076b6-120">The following connection string shows the format to use for HDInsight:</span><span class="sxs-lookup"><span data-stu-id="076b6-120">The following connection string shows the format to use for HDInsight:</span></span>

    jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

<span data-ttu-id="076b6-121">Replace `CLUSTERNAME` with the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="076b6-121">Replace `CLUSTERNAME` with the name of your HDInsight cluster.</span></span>

## <a name="authentication"></a><span data-ttu-id="076b6-122">Authentication</span><span class="sxs-lookup"><span data-stu-id="076b6-122">Authentication</span></span>

<span data-ttu-id="076b6-123">When establishing the connection, you must use the HDInsight cluster admin name and password to authenticate to the cluster gateway.</span><span class="sxs-lookup"><span data-stu-id="076b6-123">When establishing the connection, you must use the HDInsight cluster admin name and password to authenticate to the cluster gateway.</span></span> <span data-ttu-id="076b6-124">When connecting from JDBC clients such as SQuirreL SQL, you must enter the admin name and password in client settings.</span><span class="sxs-lookup"><span data-stu-id="076b6-124">When connecting from JDBC clients such as SQuirreL SQL, you must enter the admin name and password in client settings.</span></span>

<span data-ttu-id="076b6-125">From a Java application, you must use the name and password when establishing a connection.</span><span class="sxs-lookup"><span data-stu-id="076b6-125">From a Java application, you must use the name and password when establishing a connection.</span></span> <span data-ttu-id="076b6-126">For example, the following Java code opens a new connection using the connection string, admin name, and password:</span><span class="sxs-lookup"><span data-stu-id="076b6-126">For example, the following Java code opens a new connection using the connection string, admin name, and password:</span></span>

```java
DriverManager.getConnection(connectionString,clusterAdmin,clusterPassword);
```

## <a name="connect-with-squirrel-sql-client"></a><span data-ttu-id="076b6-127">Connect with SQuirreL SQL client</span><span class="sxs-lookup"><span data-stu-id="076b6-127">Connect with SQuirreL SQL client</span></span>

<span data-ttu-id="076b6-128">SQuirreL SQL is a JDBC client that can be used to remotely run Hive queries with your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="076b6-128">SQuirreL SQL is a JDBC client that can be used to remotely run Hive queries with your HDInsight cluster.</span></span> <span data-ttu-id="076b6-129">The following steps assume that you have already installed SQuirreL SQL.</span><span class="sxs-lookup"><span data-stu-id="076b6-129">The following steps assume that you have already installed SQuirreL SQL.</span></span>

1. <span data-ttu-id="076b6-130">Create a directory that contains the files.</span><span class="sxs-lookup"><span data-stu-id="076b6-130">Create a directory that contains the files.</span></span> <span data-ttu-id="076b6-131">For example, `mkdir hivedriver`.</span><span class="sxs-lookup"><span data-stu-id="076b6-131">For example, `mkdir hivedriver`.</span></span>

2. <span data-ttu-id="076b6-132">From a command line, use the following commands to copy the files from the HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="076b6-132">From a command line, use the following commands to copy the files from the HDInsight cluster:</span></span>

    ```bash
    scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-common.jar .
    scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-auth.jar .
    scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/lib/log4j-*.jar .
    scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/lib/slf4j-*.jar .
    scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/hive-*-1.2*.jar .
    scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/httpclient-*.jar .
    scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/httpcore-*.jar .
    scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/libthrift-*.jar .
    scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/libfb*.jar .
    scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-logging-*.jar .
    ```

    <span data-ttu-id="076b6-133">Replace `USERNAME` with the SSH user account name for the cluster.</span><span class="sxs-lookup"><span data-stu-id="076b6-133">Replace `USERNAME` with the SSH user account name for the cluster.</span></span> <span data-ttu-id="076b6-134">Replace `CLUSTERNAME` with the HDInsight cluster name.</span><span class="sxs-lookup"><span data-stu-id="076b6-134">Replace `CLUSTERNAME` with the HDInsight cluster name.</span></span>

3. <span data-ttu-id="076b6-135">Start the SQuirreL SQL application.</span><span class="sxs-lookup"><span data-stu-id="076b6-135">Start the SQuirreL SQL application.</span></span> <span data-ttu-id="076b6-136">From the left of the window, select **Drivers**.</span><span class="sxs-lookup"><span data-stu-id="076b6-136">From the left of the window, select **Drivers**.</span></span>

    ![Drivers tab on the left of the window](./media/apache-hadoop-connect-hive-jdbc-driver/squirreldrivers.png)

4. <span data-ttu-id="076b6-138">From the icons at the top of the **Drivers** dialog, select the **+** icon to create a driver.</span><span class="sxs-lookup"><span data-stu-id="076b6-138">From the icons at the top of the **Drivers** dialog, select the **+** icon to create a driver.</span></span>

    ![Drivers icons](./media/apache-hadoop-connect-hive-jdbc-driver/driversicons.png)

5. <span data-ttu-id="076b6-140">In the Add Driver dialog, add the following information:</span><span class="sxs-lookup"><span data-stu-id="076b6-140">In the Add Driver dialog, add the following information:</span></span>

    * <span data-ttu-id="076b6-141">**Name**: Hive</span><span class="sxs-lookup"><span data-stu-id="076b6-141">**Name**: Hive</span></span>
    * <span data-ttu-id="076b6-142">**Example URL**: `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span><span class="sxs-lookup"><span data-stu-id="076b6-142">**Example URL**: `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span></span>
    * <span data-ttu-id="076b6-143">**Extra Class Path**: Use the Add button to add the all of jar files downloaded earlier</span><span class="sxs-lookup"><span data-stu-id="076b6-143">**Extra Class Path**: Use the Add button to add the all of jar files downloaded earlier</span></span>
    * <span data-ttu-id="076b6-144">**Class Name**: org.apache.hive.jdbc.HiveDriver</span><span class="sxs-lookup"><span data-stu-id="076b6-144">**Class Name**: org.apache.hive.jdbc.HiveDriver</span></span>

   ![add driver dialog](./media/apache-hadoop-connect-hive-jdbc-driver/adddriver.png)

   <span data-ttu-id="076b6-146">Click **OK** to save these settings.</span><span class="sxs-lookup"><span data-stu-id="076b6-146">Click **OK** to save these settings.</span></span>

6. <span data-ttu-id="076b6-147">On the left of the SQuirreL SQL window, select **Aliases**.</span><span class="sxs-lookup"><span data-stu-id="076b6-147">On the left of the SQuirreL SQL window, select **Aliases**.</span></span> <span data-ttu-id="076b6-148">Then click the **+** icon to create a connection alias.</span><span class="sxs-lookup"><span data-stu-id="076b6-148">Then click the **+** icon to create a connection alias.</span></span>

    ![add new alias](./media/apache-hadoop-connect-hive-jdbc-driver/aliases.png)

7. <span data-ttu-id="076b6-150">Use the following values for the **Add Alias** dialog.</span><span class="sxs-lookup"><span data-stu-id="076b6-150">Use the following values for the **Add Alias** dialog.</span></span>

    * <span data-ttu-id="076b6-151">**Name**: Hive on HDInsight</span><span class="sxs-lookup"><span data-stu-id="076b6-151">**Name**: Hive on HDInsight</span></span>

    * <span data-ttu-id="076b6-152">**Driver**: Use the dropdown to select the **Hive** driver</span><span class="sxs-lookup"><span data-stu-id="076b6-152">**Driver**: Use the dropdown to select the **Hive** driver</span></span>

    * <span data-ttu-id="076b6-153">**URL**: `jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span><span class="sxs-lookup"><span data-stu-id="076b6-153">**URL**: `jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span></span>

        <span data-ttu-id="076b6-154">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="076b6-154">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>

    * <span data-ttu-id="076b6-155">**User Name**: The cluster login account name for your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="076b6-155">**User Name**: The cluster login account name for your HDInsight cluster.</span></span> <span data-ttu-id="076b6-156">The default is `admin`.</span><span class="sxs-lookup"><span data-stu-id="076b6-156">The default is `admin`.</span></span>

    * <span data-ttu-id="076b6-157">**Password**: The password for the cluster login account.</span><span class="sxs-lookup"><span data-stu-id="076b6-157">**Password**: The password for the cluster login account.</span></span>

 ![add alias dialog](./media/apache-hadoop-connect-hive-jdbc-driver/addalias.png)

    > [!IMPORTANT] 
    > <span data-ttu-id="076b6-159">Use the **Test** button to verify that the connection works.</span><span class="sxs-lookup"><span data-stu-id="076b6-159">Use the **Test** button to verify that the connection works.</span></span> <span data-ttu-id="076b6-160">When **Connect to: Hive on HDInsight** dialog appears, select **Connect** to perform the test.</span><span class="sxs-lookup"><span data-stu-id="076b6-160">When **Connect to: Hive on HDInsight** dialog appears, select **Connect** to perform the test.</span></span> <span data-ttu-id="076b6-161">If the test succeeds, you see a **Connection successful** dialog.</span><span class="sxs-lookup"><span data-stu-id="076b6-161">If the test succeeds, you see a **Connection successful** dialog.</span></span> <span data-ttu-id="076b6-162">If an error occurs, see [Troubleshooting](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="076b6-162">If an error occurs, see [Troubleshooting](#troubleshooting).</span></span>

    <span data-ttu-id="076b6-163">To save the connection alias, use the **Ok** button at the bottom of the **Add Alias** dialog.</span><span class="sxs-lookup"><span data-stu-id="076b6-163">To save the connection alias, use the **Ok** button at the bottom of the **Add Alias** dialog.</span></span>

8. <span data-ttu-id="076b6-164">From the **Connect to** dropdown at the top of SQuirreL SQL, select **Hive on HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="076b6-164">From the **Connect to** dropdown at the top of SQuirreL SQL, select **Hive on HDInsight**.</span></span> <span data-ttu-id="076b6-165">When prompted, select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="076b6-165">When prompted, select **Connect**.</span></span>

    ![connection dialog](./media/apache-hadoop-connect-hive-jdbc-driver/connect.png)

9. <span data-ttu-id="076b6-167">Once connected, enter the following query into the SQL query dialog, and then select the **Run** icon.</span><span class="sxs-lookup"><span data-stu-id="076b6-167">Once connected, enter the following query into the SQL query dialog, and then select the **Run** icon.</span></span> <span data-ttu-id="076b6-168">The results area should show the results of the query.</span><span class="sxs-lookup"><span data-stu-id="076b6-168">The results area should show the results of the query.</span></span>

        select * from hivesampletable limit 10;

    ![sql query dialog, including results](./media/apache-hadoop-connect-hive-jdbc-driver/sqlquery.png)

## <a name="connect-from-an-example-java-application"></a><span data-ttu-id="076b6-170">Connect from an example Java application</span><span class="sxs-lookup"><span data-stu-id="076b6-170">Connect from an example Java application</span></span>

<span data-ttu-id="076b6-171">An example of using a Java client to query Hive on HDInsight is available at [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span><span class="sxs-lookup"><span data-stu-id="076b6-171">An example of using a Java client to query Hive on HDInsight is available at [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span></span> <span data-ttu-id="076b6-172">Follow the instructions in the repository to build and run the sample.</span><span class="sxs-lookup"><span data-stu-id="076b6-172">Follow the instructions in the repository to build and run the sample.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="076b6-173">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="076b6-173">Troubleshooting</span></span>

### <a name="unexpected-error-occurred-attempting-to-open-an-sql-connection"></a><span data-ttu-id="076b6-174">Unexpected Error occurred attempting to open an SQL connection</span><span class="sxs-lookup"><span data-stu-id="076b6-174">Unexpected Error occurred attempting to open an SQL connection</span></span>

<span data-ttu-id="076b6-175">**Symptoms**: When connecting to an HDInsight cluster that is version 3.3 or greater, you may receive an error that an unexpected error occurred.</span><span class="sxs-lookup"><span data-stu-id="076b6-175">**Symptoms**: When connecting to an HDInsight cluster that is version 3.3 or greater, you may receive an error that an unexpected error occurred.</span></span> <span data-ttu-id="076b6-176">The stack trace for this error begins with the following lines:</span><span class="sxs-lookup"><span data-stu-id="076b6-176">The stack trace for this error begins with the following lines:</span></span>

```java
java.util.concurrent.ExecutionException: java.lang.RuntimeException: java.lang.NoSuchMethodError: org.apache.commons.codec.binary.Base64.<init>(I)V
at java.util.concurrent.FutureTas...(FutureTask.java:122)
at java.util.concurrent.FutureTask.get(FutureTask.java:206)
```

<span data-ttu-id="076b6-177">**Cause**: This error is caused by an older version commons-codec.jar file included with SQuirreL.</span><span class="sxs-lookup"><span data-stu-id="076b6-177">**Cause**: This error is caused by an older version commons-codec.jar file included with SQuirreL.</span></span>

<span data-ttu-id="076b6-178">**Resolution**: To fix this error, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="076b6-178">**Resolution**: To fix this error, use the following steps:</span></span>

1. <span data-ttu-id="076b6-179">Download the commons-codec jar file from your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="076b6-179">Download the commons-codec jar file from your HDInsight cluster.</span></span>

        scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-codec*.jar ./commons-codec.jar

2. <span data-ttu-id="076b6-180">Exit SQuirreL, and then go to the directory where SQuirreL is installed on your system.</span><span class="sxs-lookup"><span data-stu-id="076b6-180">Exit SQuirreL, and then go to the directory where SQuirreL is installed on your system.</span></span> <span data-ttu-id="076b6-181">In the SquirreL directory, under the `lib` directory, replace the existing commons-codec.jar with the one downloaded from the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="076b6-181">In the SquirreL directory, under the `lib` directory, replace the existing commons-codec.jar with the one downloaded from the HDInsight cluster.</span></span>

3. <span data-ttu-id="076b6-182">Restart SQuirreL.</span><span class="sxs-lookup"><span data-stu-id="076b6-182">Restart SQuirreL.</span></span> <span data-ttu-id="076b6-183">The error should no longer occur when connecting to Hive on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="076b6-183">The error should no longer occur when connecting to Hive on HDInsight.</span></span>

## <a name="next-steps"></a><span data-ttu-id="076b6-184">Next steps</span><span class="sxs-lookup"><span data-stu-id="076b6-184">Next steps</span></span>

<span data-ttu-id="076b6-185">Now that you have learned how to use JDBC to work with Hive, use the following links to explore other ways to work with Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="076b6-185">Now that you have learned how to use JDBC to work with Hive, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* <span data-ttu-id="076b6-186">[Visualize Hive data with Microsoft Power BI in Azure HDInsight](apache-hadoop-connect-hive-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="076b6-186">[Visualize Hive data with Microsoft Power BI in Azure HDInsight](apache-hadoop-connect-hive-power-bi.md).</span></span>
* <span data-ttu-id="076b6-187">[Visualize Interactive Query Hive data with Power BI in Azure HDInsight](../interactive-query/apache-hadoop-connect-hive-power-bi-directquery.md).</span><span class="sxs-lookup"><span data-stu-id="076b6-187">[Visualize Interactive Query Hive data with Power BI in Azure HDInsight](../interactive-query/apache-hadoop-connect-hive-power-bi-directquery.md).</span></span>
* <span data-ttu-id="076b6-188">[Use Zeppelin to run Hive queries in Azure HDInsight](./../hdinsight-connect-hive-zeppelin.md).</span><span class="sxs-lookup"><span data-stu-id="076b6-188">[Use Zeppelin to run Hive queries in Azure HDInsight](./../hdinsight-connect-hive-zeppelin.md).</span></span>
* <span data-ttu-id="076b6-189">[Connect Excel to HDInsight with the Microsoft Hive ODBC Driver](apache-hadoop-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="076b6-189">[Connect Excel to HDInsight with the Microsoft Hive ODBC Driver](apache-hadoop-connect-excel-hive-odbc-driver.md).</span></span>
* <span data-ttu-id="076b6-190">[Connect Excel to Hadoop by using Power Query](apache-hadoop-connect-excel-power-query.md).</span><span class="sxs-lookup"><span data-stu-id="076b6-190">[Connect Excel to Hadoop by using Power Query](apache-hadoop-connect-excel-power-query.md).</span></span>
* <span data-ttu-id="076b6-191">[Connect to Azure HDInsight and run Hive queries using Data Lake Tools for Visual Studio](apache-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="076b6-191">[Connect to Azure HDInsight and run Hive queries using Data Lake Tools for Visual Studio](apache-hadoop-visual-studio-tools-get-started.md).</span></span>
* <span data-ttu-id="076b6-192">[Use Azure HDInsight Tool for Visual Studio Code](../hdinsight-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="076b6-192">[Use Azure HDInsight Tool for Visual Studio Code](../hdinsight-for-vscode.md).</span></span>
* [<span data-ttu-id="076b6-193">Upload data to HDInsight</span><span class="sxs-lookup"><span data-stu-id="076b6-193">Upload data to HDInsight</span></span>](../hdinsight-upload-data.md)
* [<span data-ttu-id="076b6-194">Use Hive with HDInsight</span><span class="sxs-lookup"><span data-stu-id="076b6-194">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="076b6-195">Use Pig with HDInsight</span><span class="sxs-lookup"><span data-stu-id="076b6-195">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="076b6-196">Use MapReduce jobs with HDInsight</span><span class="sxs-lookup"><span data-stu-id="076b6-196">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
