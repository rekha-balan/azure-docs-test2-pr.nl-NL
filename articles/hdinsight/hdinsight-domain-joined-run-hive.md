---
title: Configure Hive policies in Domain-joined HDInsight | Microsoft Docs
description: Learn ....
services: hdinsight
documentationcenter: ''
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3fade1e5-c2e1-4ad5-b371-f95caea23f6d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 370d141b752ea2058b3ffd2e3f5205233be559c1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660982"
---
# <a name="configure-hive-policies-in-domain-joined-hdinsight-preview"></a><span data-ttu-id="5047d-103">Configure Hive policies in Domain-joined HDInsight (Preview)</span><span class="sxs-lookup"><span data-stu-id="5047d-103">Configure Hive policies in Domain-joined HDInsight (Preview)</span></span>
<span data-ttu-id="5047d-104">Learn how to configure Apache Ranger policies for Hive.</span><span class="sxs-lookup"><span data-stu-id="5047d-104">Learn how to configure Apache Ranger policies for Hive.</span></span> <span data-ttu-id="5047d-105">In this article, you create two Ranger policies to restrict access to the hivesampletable.</span><span class="sxs-lookup"><span data-stu-id="5047d-105">In this article, you create two Ranger policies to restrict access to the hivesampletable.</span></span> <span data-ttu-id="5047d-106">The hivesampletable comes with HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="5047d-106">The hivesampletable comes with HDInsight clusters.</span></span> <span data-ttu-id="5047d-107">After you have configured the policies, you use Excel and ODBC driver to connect to Hive tables in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5047d-107">After you have configured the policies, you use Excel and ODBC driver to connect to Hive tables in HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5047d-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5047d-108">Prerequisites</span></span>
* <span data-ttu-id="5047d-109">A Domain-joined HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="5047d-109">A Domain-joined HDInsight cluster.</span></span> <span data-ttu-id="5047d-110">See [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span><span class="sxs-lookup"><span data-stu-id="5047d-110">See [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="5047d-111">A workstation with Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span><span class="sxs-lookup"><span data-stu-id="5047d-111">A workstation with Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="connect-to-apache-ranger-admin-ui"></a><span data-ttu-id="5047d-112">Connect to Apache Ranger Admin UI</span><span class="sxs-lookup"><span data-stu-id="5047d-112">Connect to Apache Ranger Admin UI</span></span>
<span data-ttu-id="5047d-113">**To connect to Ranger Admin UI**</span><span class="sxs-lookup"><span data-stu-id="5047d-113">**To connect to Ranger Admin UI**</span></span>

1. <span data-ttu-id="5047d-114">From a browser, connect to Ranger Admin UI.</span><span class="sxs-lookup"><span data-stu-id="5047d-114">From a browser, connect to Ranger Admin UI.</span></span> <span data-ttu-id="5047d-115">The URL is https://&lt;ClusterName>.azurehdinsight.net/Ranger/.</span><span class="sxs-lookup"><span data-stu-id="5047d-115">The URL is https://&lt;ClusterName>.azurehdinsight.net/Ranger/.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5047d-116">Ranger uses different credentials than Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="5047d-116">Ranger uses different credentials than Hadoop cluster.</span></span> <span data-ttu-id="5047d-117">To prevent browsers using cached Hadoop credentials, use new inprivate browser window to connect to the Ranger Admin UI.</span><span class="sxs-lookup"><span data-stu-id="5047d-117">To prevent browsers using cached Hadoop credentials, use new inprivate browser window to connect to the Ranger Admin UI.</span></span>
   >
   >
2. <span data-ttu-id="5047d-118">Log in using the cluster administrator domain user name and password:</span><span class="sxs-lookup"><span data-stu-id="5047d-118">Log in using the cluster administrator domain user name and password:</span></span>

    ![HDInsight Domain-joined Ranger home page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-ranger-home-page.png)

    <span data-ttu-id="5047d-120">Currently, Ranger only works with Yarn and Hive.</span><span class="sxs-lookup"><span data-stu-id="5047d-120">Currently, Ranger only works with Yarn and Hive.</span></span>

## <a name="create-domain-users"></a><span data-ttu-id="5047d-121">Create Domain users</span><span class="sxs-lookup"><span data-stu-id="5047d-121">Create Domain users</span></span>
<span data-ttu-id="5047d-122">In [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad), you have created hiveruser1 and hiveuser2.</span><span class="sxs-lookup"><span data-stu-id="5047d-122">In [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad), you have created hiveruser1 and hiveuser2.</span></span> <span data-ttu-id="5047d-123">You will use the two user account in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="5047d-123">You will use the two user account in this tutorial.</span></span>

## <a name="create-ranger-policies"></a><span data-ttu-id="5047d-124">Create Ranger policies</span><span class="sxs-lookup"><span data-stu-id="5047d-124">Create Ranger policies</span></span>
<span data-ttu-id="5047d-125">In this section, you will create two Ranger policies for accessing hivesampletable.</span><span class="sxs-lookup"><span data-stu-id="5047d-125">In this section, you will create two Ranger policies for accessing hivesampletable.</span></span> <span data-ttu-id="5047d-126">You give select permission on different set of columns.</span><span class="sxs-lookup"><span data-stu-id="5047d-126">You give select permission on different set of columns.</span></span> <span data-ttu-id="5047d-127">Both users were created in [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).</span><span class="sxs-lookup"><span data-stu-id="5047d-127">Both users were created in [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).</span></span>  <span data-ttu-id="5047d-128">In the next section, you will test the two policies in Excel.</span><span class="sxs-lookup"><span data-stu-id="5047d-128">In the next section, you will test the two policies in Excel.</span></span>

<span data-ttu-id="5047d-129">**To create Ranger policies**</span><span class="sxs-lookup"><span data-stu-id="5047d-129">**To create Ranger policies**</span></span>

1. <span data-ttu-id="5047d-130">Open Ranger Admin UI.</span><span class="sxs-lookup"><span data-stu-id="5047d-130">Open Ranger Admin UI.</span></span> <span data-ttu-id="5047d-131">See [Connect to Apache Ranger Admin UI](#connect-to-apache-ranager-admin-ui).</span><span class="sxs-lookup"><span data-stu-id="5047d-131">See [Connect to Apache Ranger Admin UI](#connect-to-apache-ranager-admin-ui).</span></span>
2. <span data-ttu-id="5047d-132">Click **&lt;ClusterName>_hive**, under **Hive**.</span><span class="sxs-lookup"><span data-stu-id="5047d-132">Click **&lt;ClusterName>_hive**, under **Hive**.</span></span> <span data-ttu-id="5047d-133">You shall see two pre-configure policies.</span><span class="sxs-lookup"><span data-stu-id="5047d-133">You shall see two pre-configure policies.</span></span>
3. <span data-ttu-id="5047d-134">Click **Add New Policy**, and then enter the following values:</span><span class="sxs-lookup"><span data-stu-id="5047d-134">Click **Add New Policy**, and then enter the following values:</span></span>

   * <span data-ttu-id="5047d-135">Policy name: read-hivesampletable-all</span><span class="sxs-lookup"><span data-stu-id="5047d-135">Policy name: read-hivesampletable-all</span></span>
   * <span data-ttu-id="5047d-136">Hive Database: default</span><span class="sxs-lookup"><span data-stu-id="5047d-136">Hive Database: default</span></span>
   * <span data-ttu-id="5047d-137">table: hivesampletable</span><span class="sxs-lookup"><span data-stu-id="5047d-137">table: hivesampletable</span></span>
   * <span data-ttu-id="5047d-138">Hive column: \*</span><span class="sxs-lookup"><span data-stu-id="5047d-138">Hive column: \*</span></span>
   * <span data-ttu-id="5047d-139">Select User: hiveuser1</span><span class="sxs-lookup"><span data-stu-id="5047d-139">Select User: hiveuser1</span></span>
   * <span data-ttu-id="5047d-140">Permissions: select</span><span class="sxs-lookup"><span data-stu-id="5047d-140">Permissions: select</span></span>

     ![HDInsight Domain-joined Ranger Hive policy configure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-configure-ranger-policy.png)<span data-ttu-id="5047d-142">.</span><span class="sxs-lookup"><span data-stu-id="5047d-142">.</span></span>

     > [!NOTE]
     > <span data-ttu-id="5047d-143">If a domain user is not populated in Select User, wait a few moments for Ranger to sync with AAD.</span><span class="sxs-lookup"><span data-stu-id="5047d-143">If a domain user is not populated in Select User, wait a few moments for Ranger to sync with AAD.</span></span>
     >
     >
4. <span data-ttu-id="5047d-144">Click **Add** to save the policy.</span><span class="sxs-lookup"><span data-stu-id="5047d-144">Click **Add** to save the policy.</span></span>
5. <span data-ttu-id="5047d-145">Repeat the last two steps to create another policy with the following properties:</span><span class="sxs-lookup"><span data-stu-id="5047d-145">Repeat the last two steps to create another policy with the following properties:</span></span>

   * <span data-ttu-id="5047d-146">Policy name: read-hivesampletable-devicemake</span><span class="sxs-lookup"><span data-stu-id="5047d-146">Policy name: read-hivesampletable-devicemake</span></span>
   * <span data-ttu-id="5047d-147">Hive Database: default</span><span class="sxs-lookup"><span data-stu-id="5047d-147">Hive Database: default</span></span>
   * <span data-ttu-id="5047d-148">table: hivesampletable</span><span class="sxs-lookup"><span data-stu-id="5047d-148">table: hivesampletable</span></span>
   * <span data-ttu-id="5047d-149">Hive column: clientid, devicemake</span><span class="sxs-lookup"><span data-stu-id="5047d-149">Hive column: clientid, devicemake</span></span>
   * <span data-ttu-id="5047d-150">Select User: hiveuser2</span><span class="sxs-lookup"><span data-stu-id="5047d-150">Select User: hiveuser2</span></span>
   * <span data-ttu-id="5047d-151">Permissions: select</span><span class="sxs-lookup"><span data-stu-id="5047d-151">Permissions: select</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="5047d-152">Create Hive ODBC data source</span><span class="sxs-lookup"><span data-stu-id="5047d-152">Create Hive ODBC data source</span></span>
<span data-ttu-id="5047d-153">The instructions can be found in [Create Hive ODBC data source](hdinsight-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="5047d-153">The instructions can be found in [Create Hive ODBC data source](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>  

    <span data-ttu-id="5047d-154">Property</span><span class="sxs-lookup"><span data-stu-id="5047d-154">Property</span></span>|<span data-ttu-id="5047d-155">Description</span><span class="sxs-lookup"><span data-stu-id="5047d-155">Description</span></span>
    ---|---
    <span data-ttu-id="5047d-156">Data Source Name</span><span class="sxs-lookup"><span data-stu-id="5047d-156">Data Source Name</span></span>|<span data-ttu-id="5047d-157">Give a name to your data source</span><span class="sxs-lookup"><span data-stu-id="5047d-157">Give a name to your data source</span></span>
    <span data-ttu-id="5047d-158">Host</span><span class="sxs-lookup"><span data-stu-id="5047d-158">Host</span></span>|<span data-ttu-id="5047d-159">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="5047d-159">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="5047d-160">For example, myHDICluster.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="5047d-160">For example, myHDICluster.azurehdinsight.net</span></span>
    <span data-ttu-id="5047d-161">Port</span><span class="sxs-lookup"><span data-stu-id="5047d-161">Port</span></span>|<span data-ttu-id="5047d-162">Use <strong>443</strong>.</span><span class="sxs-lookup"><span data-stu-id="5047d-162">Use <strong>443</strong>.</span></span> <span data-ttu-id="5047d-163">(This port has been changed from 563 to 443.)</span><span class="sxs-lookup"><span data-stu-id="5047d-163">(This port has been changed from 563 to 443.)</span></span>
    <span data-ttu-id="5047d-164">Database</span><span class="sxs-lookup"><span data-stu-id="5047d-164">Database</span></span>|<span data-ttu-id="5047d-165">Use <strong>Default</strong>.</span><span class="sxs-lookup"><span data-stu-id="5047d-165">Use <strong>Default</strong>.</span></span>
    <span data-ttu-id="5047d-166">Hive Server Type</span><span class="sxs-lookup"><span data-stu-id="5047d-166">Hive Server Type</span></span>|<span data-ttu-id="5047d-167">Select <strong>Hive Server 2</strong></span><span class="sxs-lookup"><span data-stu-id="5047d-167">Select <strong>Hive Server 2</strong></span></span>
    <span data-ttu-id="5047d-168">Mechanism</span><span class="sxs-lookup"><span data-stu-id="5047d-168">Mechanism</span></span>|<span data-ttu-id="5047d-169">Select <strong>Azure HDInsight Service</strong></span><span class="sxs-lookup"><span data-stu-id="5047d-169">Select <strong>Azure HDInsight Service</strong></span></span>
    <span data-ttu-id="5047d-170">HTTP Path</span><span class="sxs-lookup"><span data-stu-id="5047d-170">HTTP Path</span></span>|<span data-ttu-id="5047d-171">Leave it blank.</span><span class="sxs-lookup"><span data-stu-id="5047d-171">Leave it blank.</span></span>
    <span data-ttu-id="5047d-172">User Name</span><span class="sxs-lookup"><span data-stu-id="5047d-172">User Name</span></span>|<span data-ttu-id="5047d-173">Enter hiveuser1@contoso158.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="5047d-173">Enter hiveuser1@contoso158.onmicrosoft.com.</span></span> <span data-ttu-id="5047d-174">Update the domain name if it is different.</span><span class="sxs-lookup"><span data-stu-id="5047d-174">Update the domain name if it is different.</span></span>
    <span data-ttu-id="5047d-175">Password</span><span class="sxs-lookup"><span data-stu-id="5047d-175">Password</span></span>|<span data-ttu-id="5047d-176">Enter the password for hiveuser1.</span><span class="sxs-lookup"><span data-stu-id="5047d-176">Enter the password for hiveuser1.</span></span>
    </table>

<span data-ttu-id="5047d-177">Make sure to click **Test** before saving the data source.</span><span class="sxs-lookup"><span data-stu-id="5047d-177">Make sure to click **Test** before saving the data source.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="5047d-178">Import data into Excel from HDInsight</span><span class="sxs-lookup"><span data-stu-id="5047d-178">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="5047d-179">In the last section, you have configured two policies.</span><span class="sxs-lookup"><span data-stu-id="5047d-179">In the last section, you have configured two policies.</span></span>  <span data-ttu-id="5047d-180">hiveuser1 has the select permission on all the columns, and hiveuser2 has the select permission on two columns.</span><span class="sxs-lookup"><span data-stu-id="5047d-180">hiveuser1 has the select permission on all the columns, and hiveuser2 has the select permission on two columns.</span></span> <span data-ttu-id="5047d-181">In this section, you impersonate the two users to import data into Excel.</span><span class="sxs-lookup"><span data-stu-id="5047d-181">In this section, you impersonate the two users to import data into Excel.</span></span>

1. <span data-ttu-id="5047d-182">Open a new or existing workbook in Excel.</span><span class="sxs-lookup"><span data-stu-id="5047d-182">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="5047d-183">From the **Data** tab, click **From Other Data Sources**, and then click **From Data Connection Wizard** to launch the **Data Connection Wizard**.</span><span class="sxs-lookup"><span data-stu-id="5047d-183">From the **Data** tab, click **From Other Data Sources**, and then click **From Data Connection Wizard** to launch the **Data Connection Wizard**.</span></span>

    <span data-ttu-id="5047d-184">![Open data connection wizard][img-hdi-simbahiveodbc.excel.dataconnection]</span><span class="sxs-lookup"><span data-stu-id="5047d-184">![Open data connection wizard][img-hdi-simbahiveodbc.excel.dataconnection]</span></span>
3. <span data-ttu-id="5047d-185">Select **ODBC DSN** as the data source, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5047d-185">Select **ODBC DSN** as the data source, and then click **Next**.</span></span>
4. <span data-ttu-id="5047d-186">From ODBC data sources, select the data source name that you created in the previous step, and then  click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5047d-186">From ODBC data sources, select the data source name that you created in the previous step, and then  click **Next**.</span></span>
5. <span data-ttu-id="5047d-187">Re-enter the password for the cluster in the wizard, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="5047d-187">Re-enter the password for the cluster in the wizard, and then click **OK**.</span></span> <span data-ttu-id="5047d-188">Wait for the **Select Database and Table** dialog to open.</span><span class="sxs-lookup"><span data-stu-id="5047d-188">Wait for the **Select Database and Table** dialog to open.</span></span> <span data-ttu-id="5047d-189">This can take a few seconds.</span><span class="sxs-lookup"><span data-stu-id="5047d-189">This can take a few seconds.</span></span>
6. <span data-ttu-id="5047d-190">Select **hivesampletable**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5047d-190">Select **hivesampletable**, and then click **Next**.</span></span>
7. <span data-ttu-id="5047d-191">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="5047d-191">Click **Finish**.</span></span>
8. <span data-ttu-id="5047d-192">In the **Import Data** dialog, you can change or specify the query.</span><span class="sxs-lookup"><span data-stu-id="5047d-192">In the **Import Data** dialog, you can change or specify the query.</span></span> <span data-ttu-id="5047d-193">To do so, click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="5047d-193">To do so, click **Properties**.</span></span> <span data-ttu-id="5047d-194">This can take a few seconds.</span><span class="sxs-lookup"><span data-stu-id="5047d-194">This can take a few seconds.</span></span>
9. <span data-ttu-id="5047d-195">Click the **Definition** tab. The command text is:</span><span class="sxs-lookup"><span data-stu-id="5047d-195">Click the **Definition** tab. The command text is:</span></span>

       SELECT * FROM "HIVE"."default"."hivesampletable"

   <span data-ttu-id="5047d-196">By the Ranger policies you defined,  hiveuser1 has select permission on all the columns.</span><span class="sxs-lookup"><span data-stu-id="5047d-196">By the Ranger policies you defined,  hiveuser1 has select permission on all the columns.</span></span>  <span data-ttu-id="5047d-197">So this query works with hiveuser1's credentials, but this query does not not work with hiveuser2's credentials.</span><span class="sxs-lookup"><span data-stu-id="5047d-197">So this query works with hiveuser1's credentials, but this query does not not work with hiveuser2's credentials.</span></span>

   <span data-ttu-id="5047d-198">![Connection Properties][img-hdi-simbahiveodbc-excel-connectionproperties]</span><span class="sxs-lookup"><span data-stu-id="5047d-198">![Connection Properties][img-hdi-simbahiveodbc-excel-connectionproperties]</span></span>
10. <span data-ttu-id="5047d-199">Click **OK** to close the Connection Properties dialog.</span><span class="sxs-lookup"><span data-stu-id="5047d-199">Click **OK** to close the Connection Properties dialog.</span></span>
11. <span data-ttu-id="5047d-200">Click **OK** to close the **Import Data** dialog.</span><span class="sxs-lookup"><span data-stu-id="5047d-200">Click **OK** to close the **Import Data** dialog.</span></span>  
12. <span data-ttu-id="5047d-201">Reenter the password for hiveuser1, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="5047d-201">Reenter the password for hiveuser1, and then click **OK**.</span></span> <span data-ttu-id="5047d-202">It takes a few seconds before data gets imported to Excel.</span><span class="sxs-lookup"><span data-stu-id="5047d-202">It takes a few seconds before data gets imported to Excel.</span></span> <span data-ttu-id="5047d-203">When it is done, you shall see 11 columns of data.</span><span class="sxs-lookup"><span data-stu-id="5047d-203">When it is done, you shall see 11 columns of data.</span></span>

<span data-ttu-id="5047d-204">To test the second policy (read-hivesampletable-devicemake) you created in the last section</span><span class="sxs-lookup"><span data-stu-id="5047d-204">To test the second policy (read-hivesampletable-devicemake) you created in the last section</span></span>

1. <span data-ttu-id="5047d-205">Add a new sheet in Excel.</span><span class="sxs-lookup"><span data-stu-id="5047d-205">Add a new sheet in Excel.</span></span>
2. <span data-ttu-id="5047d-206">Follow the last procedure to import the data.</span><span class="sxs-lookup"><span data-stu-id="5047d-206">Follow the last procedure to import the data.</span></span>  <span data-ttu-id="5047d-207">The only change you will make is to use hiveuser2's credentials instead of hiveuser1's.</span><span class="sxs-lookup"><span data-stu-id="5047d-207">The only change you will make is to use hiveuser2's credentials instead of hiveuser1's.</span></span> <span data-ttu-id="5047d-208">This will fail because hiveuser2 only has permission to see two columns.</span><span class="sxs-lookup"><span data-stu-id="5047d-208">This will fail because hiveuser2 only has permission to see two columns.</span></span> <span data-ttu-id="5047d-209">You shall get the following error:</span><span class="sxs-lookup"><span data-stu-id="5047d-209">You shall get the following error:</span></span>

        [Microsoft][HiveODBC] (35) Error from Hive: error code: '40000' error message: 'Error while compiling statement: FAILED: HiveAccessControlException Permission denied: user [hiveuser2] does not have [SELECT] privilege on [default/hivesampletable/clientid,country ...]'.
3. <span data-ttu-id="5047d-210">Follow the same procedure to import data.</span><span class="sxs-lookup"><span data-stu-id="5047d-210">Follow the same procedure to import data.</span></span> <span data-ttu-id="5047d-211">This time, use hiveuser2's credentials, and also modify the select statement from:</span><span class="sxs-lookup"><span data-stu-id="5047d-211">This time, use hiveuser2's credentials, and also modify the select statement from:</span></span>

        SELECT * FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="5047d-212">to:</span><span class="sxs-lookup"><span data-stu-id="5047d-212">to:</span></span>

        SELECT clientid, devicemake FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="5047d-213">When it is done, you shall see two columns of data imported.</span><span class="sxs-lookup"><span data-stu-id="5047d-213">When it is done, you shall see two columns of data imported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5047d-214">Next steps</span><span class="sxs-lookup"><span data-stu-id="5047d-214">Next steps</span></span>
* <span data-ttu-id="5047d-215">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span><span class="sxs-lookup"><span data-stu-id="5047d-215">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="5047d-216">For managing a Domain-joined HDInsight clusters, see [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span><span class="sxs-lookup"><span data-stu-id="5047d-216">For managing a Domain-joined HDInsight clusters, see [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>
* <span data-ttu-id="5047d-217">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span><span class="sxs-lookup"><span data-stu-id="5047d-217">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>
* <span data-ttu-id="5047d-218">For Connecting Hive using Hive JDBC, see [Connect to Hive on Azure HDInsight using the Hive JDBC driver](hdinsight-connect-hive-jdbc-driver.md)</span><span class="sxs-lookup"><span data-stu-id="5047d-218">For Connecting Hive using Hive JDBC, see [Connect to Hive on Azure HDInsight using the Hive JDBC driver](hdinsight-connect-hive-jdbc-driver.md)</span></span>
* <span data-ttu-id="5047d-219">For connecting Excel to Hadoop using Hive ODBC, see [Connect Excel to Hadoop with the Microsoft Hive ODBC drive](hdinsight-connect-excel-hive-odbc-driver.md)</span><span class="sxs-lookup"><span data-stu-id="5047d-219">For connecting Excel to Hadoop using Hive ODBC, see [Connect Excel to Hadoop with the Microsoft Hive ODBC drive](hdinsight-connect-excel-hive-odbc-driver.md)</span></span>
* <span data-ttu-id="5047d-220">For connecting Excel to Hadoop using Power Query, see [Connect Excel to Hadoop by using Power Query](hdinsight-connect-excel-power-query.md)</span><span class="sxs-lookup"><span data-stu-id="5047d-220">For connecting Excel to Hadoop using Power Query, see [Connect Excel to Hadoop by using Power Query](hdinsight-connect-excel-power-query.md)</span></span>


