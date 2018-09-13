---
title: Connect Excel to Hadoop with the Hive ODBC Driver | Microsoft Docs
description: Learn how to set up and use the Microsoft Hive ODBC driver for Excel to query data in an HDInsight cluster.
services: hdinsight
documentationcenter: ''
author: mumian
manager: jhubbard
tags: azure-portal
editor: cgronlun
ms.assetid: a7665a14-0211-4521-b3e7-3b26e8029cc0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/06/2017
ms.author: jgao
ms.openlocfilehash: 1de90ca09bac6317ddef2d95cdcfc455fc4cb699
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555552"
---
# <a name="connect-excel-to-hadoop-with-the-microsoft-hive-odbc-driver"></a><span data-ttu-id="5947d-103">Connect Excel to Hadoop with the Microsoft Hive ODBC driver</span><span class="sxs-lookup"><span data-stu-id="5947d-103">Connect Excel to Hadoop with the Microsoft Hive ODBC driver</span></span>
[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="5947d-104">Microsoft's Big Data solution integrates  Microsoft Business Intelligence (BI) components with Apache Hadoop clusters that have been deployed by the Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5947d-104">Microsoft's Big Data solution integrates  Microsoft Business Intelligence (BI) components with Apache Hadoop clusters that have been deployed by the Azure HDInsight.</span></span> <span data-ttu-id="5947d-105">An example of this integration is the ability to connect Excel to the Hive data warehouse of an Hadoop cluster in HDInsight using the Microsoft Hive Open Database Connectivity (ODBC) Driver.</span><span class="sxs-lookup"><span data-stu-id="5947d-105">An example of this integration is the ability to connect Excel to the Hive data warehouse of an Hadoop cluster in HDInsight using the Microsoft Hive Open Database Connectivity (ODBC) Driver.</span></span>

<span data-ttu-id="5947d-106">It is also possible to connect the data associated with an HDInsight cluster and other data sources, including other (non-HDInsight) Hadoop clusters, from Excel using the Microsoft Power Query add-in for Excel.</span><span class="sxs-lookup"><span data-stu-id="5947d-106">It is also possible to connect the data associated with an HDInsight cluster and other data sources, including other (non-HDInsight) Hadoop clusters, from Excel using the Microsoft Power Query add-in for Excel.</span></span> <span data-ttu-id="5947d-107">For information on installing and using Power Query, see [Connect Excel to HDInsight with Power Query][hdinsight-power-query].</span><span class="sxs-lookup"><span data-stu-id="5947d-107">For information on installing and using Power Query, see [Connect Excel to HDInsight with Power Query][hdinsight-power-query].</span></span>

> [!NOTE]
> <span data-ttu-id="5947d-108">While the steps in this article can be used with either a Linux or Windows-based HDInsight cluster, Windows is required for the client workstation.</span><span class="sxs-lookup"><span data-stu-id="5947d-108">While the steps in this article can be used with either a Linux or Windows-based HDInsight cluster, Windows is required for the client workstation.</span></span>
> 
> 

<span data-ttu-id="5947d-109">**Prerequisites**:</span><span class="sxs-lookup"><span data-stu-id="5947d-109">**Prerequisites**:</span></span>

<span data-ttu-id="5947d-110">Before you begin this article, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="5947d-110">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="5947d-111">**An HDInsight cluster**.</span><span class="sxs-lookup"><span data-stu-id="5947d-111">**An HDInsight cluster**.</span></span> <span data-ttu-id="5947d-112">To create one, see [Get started with Azure HDInsight][hdinsight-get-started].</span><span class="sxs-lookup"><span data-stu-id="5947d-112">To create one, see [Get started with Azure HDInsight][hdinsight-get-started].</span></span>
* <span data-ttu-id="5947d-113">**A workstation** with Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span><span class="sxs-lookup"><span data-stu-id="5947d-113">**A workstation** with Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="install-microsoft-hive-odbc-driver"></a><span data-ttu-id="5947d-114">Install Microsoft Hive ODBC driver</span><span class="sxs-lookup"><span data-stu-id="5947d-114">Install Microsoft Hive ODBC driver</span></span>
<span data-ttu-id="5947d-115">Download and install Microsoft Hive ODBC Driver from the [Download Center][hive-odbc-driver-download].</span><span class="sxs-lookup"><span data-stu-id="5947d-115">Download and install Microsoft Hive ODBC Driver from the [Download Center][hive-odbc-driver-download].</span></span>

<span data-ttu-id="5947d-116">This driver can be installed on 32-bit or 64-bit versions of Windows 7, Windows 8, Windows 10, Windows Server 2008 R2 and Windows Server 2012 and will allow connection to Azure HDInsight (version 1.6 and later) and Azure HDInsight Emulator (v.1.0.0.0 and later).</span><span class="sxs-lookup"><span data-stu-id="5947d-116">This driver can be installed on 32-bit or 64-bit versions of Windows 7, Windows 8, Windows 10, Windows Server 2008 R2 and Windows Server 2012 and will allow connection to Azure HDInsight (version 1.6 and later) and Azure HDInsight Emulator (v.1.0.0.0 and later).</span></span> <span data-ttu-id="5947d-117">You should install the version that matches the version of the application where you will be using the ODBC driver.</span><span class="sxs-lookup"><span data-stu-id="5947d-117">You should install the version that matches the version of the application where you will be using the ODBC driver.</span></span> <span data-ttu-id="5947d-118">For this tutorial, the driver will be used from Office Excel.</span><span class="sxs-lookup"><span data-stu-id="5947d-118">For this tutorial, the driver will be used from Office Excel.</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="5947d-119">Create Hive ODBC data source</span><span class="sxs-lookup"><span data-stu-id="5947d-119">Create Hive ODBC data source</span></span>
<span data-ttu-id="5947d-120">The following steps show you how to create a Hive ODBC Data Source.</span><span class="sxs-lookup"><span data-stu-id="5947d-120">The following steps show you how to create a Hive ODBC Data Source.</span></span>

1. <span data-ttu-id="5947d-121">From Windows 8 or Windows 10, press the Windows key to open the Start screen, and then type **data sources**.</span><span class="sxs-lookup"><span data-stu-id="5947d-121">From Windows 8 or Windows 10, press the Windows key to open the Start screen, and then type **data sources**.</span></span>
2. <span data-ttu-id="5947d-122">Click **Set up ODBC Data sources (32-bit)** or **Set up ODBC Data Sources (64-bit)** depending on your Office version.</span><span class="sxs-lookup"><span data-stu-id="5947d-122">Click **Set up ODBC Data sources (32-bit)** or **Set up ODBC Data Sources (64-bit)** depending on your Office version.</span></span> <span data-ttu-id="5947d-123">If you are using Windows 7, choose **ODBC Data Sources (32 bit)** or **ODBC Data Sources (64 bit)** from **Administrative Tools**.</span><span class="sxs-lookup"><span data-stu-id="5947d-123">If you are using Windows 7, choose **ODBC Data Sources (32 bit)** or **ODBC Data Sources (64 bit)** from **Administrative Tools**.</span></span> <span data-ttu-id="5947d-124">This will launch the **ODBC Data Source Administrator** dialog.</span><span class="sxs-lookup"><span data-stu-id="5947d-124">This will launch the **ODBC Data Source Administrator** dialog.</span></span>
   
    ![OBDC data source administrator][img-hdi-simbahiveodbc-datasource-admin]
3. <span data-ttu-id="5947d-126">From User DNS, click **Add** to open the **Create New Data Source** wizard.</span><span class="sxs-lookup"><span data-stu-id="5947d-126">From User DNS, click **Add** to open the **Create New Data Source** wizard.</span></span>
4. <span data-ttu-id="5947d-127">Select **Microsoft Hive ODBC Driver**, and then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="5947d-127">Select **Microsoft Hive ODBC Driver**, and then click **Finish**.</span></span> <span data-ttu-id="5947d-128">This will launch the **Microsoft Hive ODBC Driver DNS Setup** dialog.</span><span class="sxs-lookup"><span data-stu-id="5947d-128">This will launch the **Microsoft Hive ODBC Driver DNS Setup** dialog.</span></span>
5. <span data-ttu-id="5947d-129">Type or select the following values:</span><span class="sxs-lookup"><span data-stu-id="5947d-129">Type or select the following values:</span></span>
   
   | <span data-ttu-id="5947d-130">Property</span><span class="sxs-lookup"><span data-stu-id="5947d-130">Property</span></span> | <span data-ttu-id="5947d-131">Description</span><span class="sxs-lookup"><span data-stu-id="5947d-131">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="5947d-132">Data Source Name</span><span class="sxs-lookup"><span data-stu-id="5947d-132">Data Source Name</span></span> |<span data-ttu-id="5947d-133">Give a name to your data source</span><span class="sxs-lookup"><span data-stu-id="5947d-133">Give a name to your data source</span></span> |
   |  <span data-ttu-id="5947d-134">Host</span><span class="sxs-lookup"><span data-stu-id="5947d-134">Host</span></span> |<span data-ttu-id="5947d-135">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="5947d-135">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="5947d-136">For example, myHDICluster.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="5947d-136">For example, myHDICluster.azurehdinsight.net</span></span> |
   |  <span data-ttu-id="5947d-137">Port</span><span class="sxs-lookup"><span data-stu-id="5947d-137">Port</span></span> |<span data-ttu-id="5947d-138">Use <strong>443</strong>.</span><span class="sxs-lookup"><span data-stu-id="5947d-138">Use <strong>443</strong>.</span></span> <span data-ttu-id="5947d-139">(This port has been changed from 563 to 443.)</span><span class="sxs-lookup"><span data-stu-id="5947d-139">(This port has been changed from 563 to 443.)</span></span> |
   |  <span data-ttu-id="5947d-140">Database</span><span class="sxs-lookup"><span data-stu-id="5947d-140">Database</span></span> |<span data-ttu-id="5947d-141">Use <strong>Default</strong>.</span><span class="sxs-lookup"><span data-stu-id="5947d-141">Use <strong>Default</strong>.</span></span> |
   |  <span data-ttu-id="5947d-142">Hive Server Type</span><span class="sxs-lookup"><span data-stu-id="5947d-142">Hive Server Type</span></span> |<span data-ttu-id="5947d-143">Select <strong>Hive Server 2</strong></span><span class="sxs-lookup"><span data-stu-id="5947d-143">Select <strong>Hive Server 2</strong></span></span> |
   |  <span data-ttu-id="5947d-144">Mechanism</span><span class="sxs-lookup"><span data-stu-id="5947d-144">Mechanism</span></span> |<span data-ttu-id="5947d-145">Select <strong>Azure HDInsight Service</strong></span><span class="sxs-lookup"><span data-stu-id="5947d-145">Select <strong>Azure HDInsight Service</strong></span></span> |
   |  <span data-ttu-id="5947d-146">HTTP Path</span><span class="sxs-lookup"><span data-stu-id="5947d-146">HTTP Path</span></span> |<span data-ttu-id="5947d-147">Leave it blank.</span><span class="sxs-lookup"><span data-stu-id="5947d-147">Leave it blank.</span></span> |
   |  <span data-ttu-id="5947d-148">User Name</span><span class="sxs-lookup"><span data-stu-id="5947d-148">User Name</span></span> |<span data-ttu-id="5947d-149">Enter HDInsight cluster user username.</span><span class="sxs-lookup"><span data-stu-id="5947d-149">Enter HDInsight cluster user username.</span></span> <span data-ttu-id="5947d-150">This is the username created during the cluster provision process.</span><span class="sxs-lookup"><span data-stu-id="5947d-150">This is the username created during the cluster provision process.</span></span> <span data-ttu-id="5947d-151">If you used the quick create option, the default username is <strong>admin</strong>.</span><span class="sxs-lookup"><span data-stu-id="5947d-151">If you used the quick create option, the default username is <strong>admin</strong>.</span></span> |
   |  <span data-ttu-id="5947d-152">Password</span><span class="sxs-lookup"><span data-stu-id="5947d-152">Password</span></span> |<span data-ttu-id="5947d-153">Enter HDInsight cluster user password.</span><span class="sxs-lookup"><span data-stu-id="5947d-153">Enter HDInsight cluster user password.</span></span> |
   
    </table>
   
    <span data-ttu-id="5947d-154">There are some important parameters to be aware of when you click **Advanced Options**:</span><span class="sxs-lookup"><span data-stu-id="5947d-154">There are some important parameters to be aware of when you click **Advanced Options**:</span></span>
   
   | <span data-ttu-id="5947d-155">Parameter</span><span class="sxs-lookup"><span data-stu-id="5947d-155">Parameter</span></span> | <span data-ttu-id="5947d-156">Description</span><span class="sxs-lookup"><span data-stu-id="5947d-156">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="5947d-157">Use Native Query</span><span class="sxs-lookup"><span data-stu-id="5947d-157">Use Native Query</span></span> |<span data-ttu-id="5947d-158">When it is selected, the ODBC driver will NOT try to convert TSQL into HiveQL.</span><span class="sxs-lookup"><span data-stu-id="5947d-158">When it is selected, the ODBC driver will NOT try to convert TSQL into HiveQL.</span></span> <span data-ttu-id="5947d-159">You shall use it only if you are 100% sure you are submitting pure HiveQL statements.</span><span class="sxs-lookup"><span data-stu-id="5947d-159">You shall use it only if you are 100% sure you are submitting pure HiveQL statements.</span></span> <span data-ttu-id="5947d-160">When connecting to SQL Server or Azure SQL Database, you should leave it unchecked.</span><span class="sxs-lookup"><span data-stu-id="5947d-160">When connecting to SQL Server or Azure SQL Database, you should leave it unchecked.</span></span> |
   |  <span data-ttu-id="5947d-161">Rows fetched per block</span><span class="sxs-lookup"><span data-stu-id="5947d-161">Rows fetched per block</span></span> |<span data-ttu-id="5947d-162">When fetching a large amount of records, tuning this parameter may be required to ensure optimal performances.</span><span class="sxs-lookup"><span data-stu-id="5947d-162">When fetching a large amount of records, tuning this parameter may be required to ensure optimal performances.</span></span> |
   |  <span data-ttu-id="5947d-163">Default string column length, Binary column length, Decimal column scale</span><span class="sxs-lookup"><span data-stu-id="5947d-163">Default string column length, Binary column length, Decimal column scale</span></span> |<span data-ttu-id="5947d-164">The data type lengths and precisions may affect how data is returned.</span><span class="sxs-lookup"><span data-stu-id="5947d-164">The data type lengths and precisions may affect how data is returned.</span></span> <span data-ttu-id="5947d-165">They will cause incorrect information to be returned due to loss of precision and/or truncation.</span><span class="sxs-lookup"><span data-stu-id="5947d-165">They will cause incorrect information to be returned due to loss of precision and/or truncation.</span></span> |

    ![Advanced options][img-HiveOdbc-DataSource-AdvancedOptions]

1. <span data-ttu-id="5947d-167">Click **Test** to test the data source.</span><span class="sxs-lookup"><span data-stu-id="5947d-167">Click **Test** to test the data source.</span></span> <span data-ttu-id="5947d-168">When the data source is configured correctly, it shows *TESTS COMPLETED SUCCESSFULLY!*.</span><span class="sxs-lookup"><span data-stu-id="5947d-168">When the data source is configured correctly, it shows *TESTS COMPLETED SUCCESSFULLY!*.</span></span>
2. <span data-ttu-id="5947d-169">Click **OK** to close the Test dialog.</span><span class="sxs-lookup"><span data-stu-id="5947d-169">Click **OK** to close the Test dialog.</span></span> <span data-ttu-id="5947d-170">The new data source should now be listed on the **ODBC Data Source Administrator**.</span><span class="sxs-lookup"><span data-stu-id="5947d-170">The new data source should now be listed on the **ODBC Data Source Administrator**.</span></span>
3. <span data-ttu-id="5947d-171">Click **OK** to exit the wizard.</span><span class="sxs-lookup"><span data-stu-id="5947d-171">Click **OK** to exit the wizard.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="5947d-172">Import data into Excel from HDInsight</span><span class="sxs-lookup"><span data-stu-id="5947d-172">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="5947d-173">The steps below describe the way to import data from a hive table into an Excel workbook using the ODBC data source that you created in the steps above.</span><span class="sxs-lookup"><span data-stu-id="5947d-173">The steps below describe the way to import data from a hive table into an Excel workbook using the ODBC data source that you created in the steps above.</span></span>

1. <span data-ttu-id="5947d-174">Open a new or existing workbook in Excel.</span><span class="sxs-lookup"><span data-stu-id="5947d-174">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="5947d-175">From the **Data** tab, click **From Other Data Sources**, and then click **From Data Connection Wizard** to launch the **Data Connection Wizard**.</span><span class="sxs-lookup"><span data-stu-id="5947d-175">From the **Data** tab, click **From Other Data Sources**, and then click **From Data Connection Wizard** to launch the **Data Connection Wizard**.</span></span>
   
    ![Open data connection wizard][img-hdi-simbahiveodbc.excel.dataconnection]
3. <span data-ttu-id="5947d-177">Select **ODBC DSN** as the data source, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5947d-177">Select **ODBC DSN** as the data source, and then click **Next**.</span></span>
4. <span data-ttu-id="5947d-178">From ODBC data sources, select the data source name that you created in the previous step, and then  click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5947d-178">From ODBC data sources, select the data source name that you created in the previous step, and then  click **Next**.</span></span>
5. <span data-ttu-id="5947d-179">Re-enter the password for the cluster in the wizard, and then click **Test** to verify the configuration once again, if required.</span><span class="sxs-lookup"><span data-stu-id="5947d-179">Re-enter the password for the cluster in the wizard, and then click **Test** to verify the configuration once again, if required.</span></span>
6. <span data-ttu-id="5947d-180">Click **OK** to close the test dialog.</span><span class="sxs-lookup"><span data-stu-id="5947d-180">Click **OK** to close the test dialog.</span></span>
7. <span data-ttu-id="5947d-181">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="5947d-181">Click **OK**.</span></span> <span data-ttu-id="5947d-182">Wait for the **Select Database and Table** dialog to open.</span><span class="sxs-lookup"><span data-stu-id="5947d-182">Wait for the **Select Database and Table** dialog to open.</span></span> <span data-ttu-id="5947d-183">This can take a few seconds.</span><span class="sxs-lookup"><span data-stu-id="5947d-183">This can take a few seconds.</span></span>
8. <span data-ttu-id="5947d-184">Select the table that you want to import, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5947d-184">Select the table that you want to import, and then click **Next**.</span></span> <span data-ttu-id="5947d-185">The *hivesampletable* is a sample hive table that comes with HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="5947d-185">The *hivesampletable* is a sample hive table that comes with HDInsight clusters.</span></span>  <span data-ttu-id="5947d-186">You can choose it if you haven't created one.</span><span class="sxs-lookup"><span data-stu-id="5947d-186">You can choose it if you haven't created one.</span></span> <span data-ttu-id="5947d-187">For more information on run Hive queries and create Hive tables, see [Use Hive with HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="5947d-187">For more information on run Hive queries and create Hive tables, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
9. <span data-ttu-id="5947d-188">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="5947d-188">Click **Finish**.</span></span>
10. <span data-ttu-id="5947d-189">In the **Import Data** dialog, you can change or specify the query.</span><span class="sxs-lookup"><span data-stu-id="5947d-189">In the **Import Data** dialog, you can change or specify the query.</span></span> <span data-ttu-id="5947d-190">To do so, click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="5947d-190">To do so, click **Properties**.</span></span> <span data-ttu-id="5947d-191">This can take a few seconds.</span><span class="sxs-lookup"><span data-stu-id="5947d-191">This can take a few seconds.</span></span>
11. <span data-ttu-id="5947d-192">Click on the **Definition** tab,  and then append **LIMIT 200** to the Hive select statement in the **Command text** textbox.</span><span class="sxs-lookup"><span data-stu-id="5947d-192">Click on the **Definition** tab,  and then append **LIMIT 200** to the Hive select statement in the **Command text** textbox.</span></span> <span data-ttu-id="5947d-193">The modification will limit the returned record set to 200.</span><span class="sxs-lookup"><span data-stu-id="5947d-193">The modification will limit the returned record set to 200.</span></span>
    
    ![Connection Properties][img-hdi-simbahiveodbc-excel-connectionproperties]
12. <span data-ttu-id="5947d-195">Click **OK** to close the Connection Properties dialog.</span><span class="sxs-lookup"><span data-stu-id="5947d-195">Click **OK** to close the Connection Properties dialog.</span></span>
13. <span data-ttu-id="5947d-196">Click **OK** to close the **Import Data** dialog.</span><span class="sxs-lookup"><span data-stu-id="5947d-196">Click **OK** to close the **Import Data** dialog.</span></span>  
14. <span data-ttu-id="5947d-197">Re-enter the password, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="5947d-197">Re-enter the password, and then click **OK**.</span></span> <span data-ttu-id="5947d-198">It takes a few seconds before data gets imported to Excel.</span><span class="sxs-lookup"><span data-stu-id="5947d-198">It takes a few seconds before data gets imported to Excel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5947d-199">Next steps</span><span class="sxs-lookup"><span data-stu-id="5947d-199">Next steps</span></span>
<span data-ttu-id="5947d-200">In this article you learned how to use the Microsoft Hive ODBC driver to retrieve data from the HDInsight Service into Excel.</span><span class="sxs-lookup"><span data-stu-id="5947d-200">In this article you learned how to use the Microsoft Hive ODBC driver to retrieve data from the HDInsight Service into Excel.</span></span> <span data-ttu-id="5947d-201">Similarly, you can retrieve data from the HDInsight Service into SQL Database.</span><span class="sxs-lookup"><span data-stu-id="5947d-201">Similarly, you can retrieve data from the HDInsight Service into SQL Database.</span></span> <span data-ttu-id="5947d-202">It is also possible to upload data into an HDInsight Service.</span><span class="sxs-lookup"><span data-stu-id="5947d-202">It is also possible to upload data into an HDInsight Service.</span></span> <span data-ttu-id="5947d-203">To learn more, see:</span><span class="sxs-lookup"><span data-stu-id="5947d-203">To learn more, see:</span></span>

* <span data-ttu-id="5947d-204">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]</span><span class="sxs-lookup"><span data-stu-id="5947d-204">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]</span></span>
* <span data-ttu-id="5947d-205">[Upload Data to HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="5947d-205">[Upload Data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="5947d-206">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="5947d-206">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-get-started]: hdinsight-hadoop-tutorial-get-started-windows.md

[hive-odbc-driver-download]: http://go.microsoft.com/fwlink/?LinkID=286698

[img-hdi-simbahiveodbc-datasource-admin]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png
[img-HiveOdbc-DataSource-AdvancedOptions]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png
[img-hdi-simbahiveodbc-excel-connectionproperties]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveODBC.Excel.ConnectionProperties1.png
[img-hdi-simbahiveodbc.excel.dataconnection]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png




