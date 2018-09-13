---
title: Manage Domain-joined HDInsight clusters - Azure
description: Learn how to manage Domain-joined HDInsight clusters
services: hdinsight
ms.service: hdinsight
author: omidm1
ms.author: omidm
ms.reviewer: jasonh
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 04/17/2018
ms.openlocfilehash: 494049cffe77e23c33528747e04bf96065fac2e2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966672"
---
# <a name="manage-domain-joined-hdinsight-clusters"></a><span data-ttu-id="f6ef9-103">Manage Domain-joined HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="f6ef9-103">Manage Domain-joined HDInsight clusters</span></span>
<span data-ttu-id="f6ef9-104">Learn the users and the roles in Domain-joined HDInsight, and how to manage domain-joined HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-104">Learn the users and the roles in Domain-joined HDInsight, and how to manage domain-joined HDInsight clusters.</span></span>

## <a name="use-vscode-to-link-to-domain-joined-cluster"></a><span data-ttu-id="f6ef9-105">Use VSCode to link to domain joined cluster</span><span class="sxs-lookup"><span data-stu-id="f6ef9-105">Use VSCode to link to domain joined cluster</span></span>

<span data-ttu-id="f6ef9-106">You can link a normal cluster by using Ambari managed username, also link a security hadoop cluster by using domain username (such as: user1@contoso.com).</span><span class="sxs-lookup"><span data-stu-id="f6ef9-106">You can link a normal cluster by using Ambari managed username, also link a security hadoop cluster by using domain username (such as: user1@contoso.com).</span></span>
1. <span data-ttu-id="f6ef9-107">Open the command palette by selecting **CTRL+SHIFT+P**, and then enter **HDInsight: Link a cluster**.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-107">Open the command palette by selecting **CTRL+SHIFT+P**, and then enter **HDInsight: Link a cluster**.</span></span>

   ![link cluster command](./media/apache-domain-joined-manage/link-cluster-command.png)

2. <span data-ttu-id="f6ef9-109">Enter HDInsight cluster URL -> input Username -> input Password -> select cluster type -> it shows success info if verification passed.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-109">Enter HDInsight cluster URL -> input Username -> input Password -> select cluster type -> it shows success info if verification passed.</span></span>
   
   ![link cluster dialog](./media/apache-domain-joined-manage/link-cluster-process.png)

   > [!NOTE]
   > <span data-ttu-id="f6ef9-111">The linked username and password are used if the cluster both logged in Azure subscription and Linked a cluster.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-111">The linked username and password are used if the cluster both logged in Azure subscription and Linked a cluster.</span></span> 
   
3. <span data-ttu-id="f6ef9-112">You can see a Linked cluster by using command **List cluster**.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-112">You can see a Linked cluster by using command **List cluster**.</span></span> <span data-ttu-id="f6ef9-113">Now you can submit a script to this linked cluster.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-113">Now you can submit a script to this linked cluster.</span></span>

   ![linked cluster](./media/apache-domain-joined-manage/linked-cluster.png)

4. <span data-ttu-id="f6ef9-115">You also can unlink a cluster by inputting **HDInsight: Unlink a cluster** from command palette.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-115">You also can unlink a cluster by inputting **HDInsight: Unlink a cluster** from command palette.</span></span>

## <a name="use-intellij-to-link-to-domain-joined-cluster"></a><span data-ttu-id="f6ef9-116">Use IntelliJ to link to domain joined cluster</span><span class="sxs-lookup"><span data-stu-id="f6ef9-116">Use IntelliJ to link to domain joined cluster</span></span>

<span data-ttu-id="f6ef9-117">You can link a normal cluster by using Ambari managed username, also link a security hadoop cluster by using domain username (such as: user1@contoso.com).</span><span class="sxs-lookup"><span data-stu-id="f6ef9-117">You can link a normal cluster by using Ambari managed username, also link a security hadoop cluster by using domain username (such as: user1@contoso.com).</span></span> 
1. <span data-ttu-id="f6ef9-118">Click **Link a cluster** from **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-118">Click **Link a cluster** from **Azure Explorer**.</span></span>

   ![link cluster context menu](./media/apache-domain-joined-manage/link-a-cluster-context-menu.png)

2. <span data-ttu-id="f6ef9-120">Enter **Cluster Name**, **User Name** and **Password**.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-120">Enter **Cluster Name**, **User Name** and **Password**.</span></span> <span data-ttu-id="f6ef9-121">You need to check the username and password if got the authentication failure.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-121">You need to check the username and password if got the authentication failure.</span></span> <span data-ttu-id="f6ef9-122">Optionally, add Storage Account, Storage Key, then select a container from Storage Container.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-122">Optionally, add Storage Account, Storage Key, then select a container from Storage Container.</span></span> <span data-ttu-id="f6ef9-123">Storage information is for storage explorer in the left tree</span><span class="sxs-lookup"><span data-stu-id="f6ef9-123">Storage information is for storage explorer in the left tree</span></span>
   
   ![link cluster dialog](./media/apache-domain-joined-manage/link-a-cluster-dialog.png)

   > [!NOTE]
   > <span data-ttu-id="f6ef9-125">We use the linked storage key, username and password if the cluster both logged in Azure subscription and Linked a cluster.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-125">We use the linked storage key, username and password if the cluster both logged in Azure subscription and Linked a cluster.</span></span>
   > <span data-ttu-id="f6ef9-126">![storage explorer in IntelliJ](./media/apache-domain-joined-manage/storage-explorer-in-IntelliJ.png)</span><span class="sxs-lookup"><span data-stu-id="f6ef9-126">![storage explorer in IntelliJ](./media/apache-domain-joined-manage/storage-explorer-in-IntelliJ.png)</span></span>

   
3. <span data-ttu-id="f6ef9-127">You can see a Linked cluster in **HDInsight** node if the input information are right.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-127">You can see a Linked cluster in **HDInsight** node if the input information are right.</span></span> <span data-ttu-id="f6ef9-128">Now you can submit an application to this linked cluster.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-128">Now you can submit an application to this linked cluster.</span></span>

   ![linked cluster](./media/apache-domain-joined-manage/linked-cluster-intellij.png)

4. <span data-ttu-id="f6ef9-130">You also can unlink a cluster from **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-130">You also can unlink a cluster from **Azure Explorer**.</span></span>
   
   ![unlinked cluster](./media/apache-domain-joined-manage/unlink.png)

## <a name="use-eclipse-to-link-to-domain-joined-cluster"></a><span data-ttu-id="f6ef9-132">Use Eclipse to link to domain joined cluster</span><span class="sxs-lookup"><span data-stu-id="f6ef9-132">Use Eclipse to link to domain joined cluster</span></span>

<span data-ttu-id="f6ef9-133">You can link a normal cluster by using Ambari managed username, also link a security hadoop cluster by using domain username (such as: user1@contoso.com).</span><span class="sxs-lookup"><span data-stu-id="f6ef9-133">You can link a normal cluster by using Ambari managed username, also link a security hadoop cluster by using domain username (such as: user1@contoso.com).</span></span>
1. <span data-ttu-id="f6ef9-134">Click **Link a cluster** from **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-134">Click **Link a cluster** from **Azure Explorer**.</span></span>

   ![link cluster context menu](./media/apache-domain-joined-manage/link-a-cluster-context-menu.png)

2. <span data-ttu-id="f6ef9-136">Enter **Cluster Name**, **User Name** and **Password**, then click OK button to link cluster.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-136">Enter **Cluster Name**, **User Name** and **Password**, then click OK button to link cluster.</span></span> <span data-ttu-id="f6ef9-137">Optionally, enter Storage Account, Storage Key and then select Storage Container for storage explorer to work in the left tree view</span><span class="sxs-lookup"><span data-stu-id="f6ef9-137">Optionally, enter Storage Account, Storage Key and then select Storage Container for storage explorer to work in the left tree view</span></span>
   
   ![link cluster dialog](./media/apache-domain-joined-manage/link-cluster-dialog.png)
   
   > [!NOTE]
   > <span data-ttu-id="f6ef9-139">We use the linked storage key, username and password if the cluster both logged in Azure subscription and Linked a cluster.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-139">We use the linked storage key, username and password if the cluster both logged in Azure subscription and Linked a cluster.</span></span>
   > <span data-ttu-id="f6ef9-140">![storage explorer in Eclipse](./media/apache-domain-joined-manage/storage-explorer-in-Eclipse.png)</span><span class="sxs-lookup"><span data-stu-id="f6ef9-140">![storage explorer in Eclipse](./media/apache-domain-joined-manage/storage-explorer-in-Eclipse.png)</span></span>

3. <span data-ttu-id="f6ef9-141">You can see a Linked cluster in **HDInsight** node after clicking OK button, if the input information are right.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-141">You can see a Linked cluster in **HDInsight** node after clicking OK button, if the input information are right.</span></span> <span data-ttu-id="f6ef9-142">Now you can submit an application to this linked cluster.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-142">Now you can submit an application to this linked cluster.</span></span>

   ![linked cluster](./media/apache-domain-joined-manage/linked-cluster-intellij.png)

4. <span data-ttu-id="f6ef9-144">You also can unlink a cluster from **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-144">You also can unlink a cluster from **Azure Explorer**.</span></span>
   
   ![unlinked cluster](./media/apache-domain-joined-manage/unlink.png)

## <a name="access-the-clusters-with-enterprise-security-package"></a><span data-ttu-id="f6ef9-146">Access the clusters with Enterprise Security Package.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-146">Access the clusters with Enterprise Security Package.</span></span>

<span data-ttu-id="f6ef9-147">Enterprise Security Package (previously known as HDInsight Premium) provides multi-user access to the cluster, where authentication is done by Active Directory and authorization by Apache Ranger and Storage ACLs (ADLS ACLs).</span><span class="sxs-lookup"><span data-stu-id="f6ef9-147">Enterprise Security Package (previously known as HDInsight Premium) provides multi-user access to the cluster, where authentication is done by Active Directory and authorization by Apache Ranger and Storage ACLs (ADLS ACLs).</span></span> <span data-ttu-id="f6ef9-148">Authorization provides secure boundaries among multiple users and allows only privileged users to have access to the data based on the authorization policies.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-148">Authorization provides secure boundaries among multiple users and allows only privileged users to have access to the data based on the authorization policies.</span></span>

<span data-ttu-id="f6ef9-149">Security and user isolation are important for a HDInsight cluster with Enterprise Security Package.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-149">Security and user isolation are important for a HDInsight cluster with Enterprise Security Package.</span></span> <span data-ttu-id="f6ef9-150">To meet these requirements, SSH access to the cluster with Enterprise Security Package is blocked.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-150">To meet these requirements, SSH access to the cluster with Enterprise Security Package is blocked.</span></span> <span data-ttu-id="f6ef9-151">The following table shows the recommended access methods for each cluster type:</span><span class="sxs-lookup"><span data-stu-id="f6ef9-151">The following table shows the recommended access methods for each cluster type:</span></span>

|<span data-ttu-id="f6ef9-152">Workload</span><span class="sxs-lookup"><span data-stu-id="f6ef9-152">Workload</span></span>|<span data-ttu-id="f6ef9-153">Scenario</span><span class="sxs-lookup"><span data-stu-id="f6ef9-153">Scenario</span></span>|<span data-ttu-id="f6ef9-154">Access Method</span><span class="sxs-lookup"><span data-stu-id="f6ef9-154">Access Method</span></span>|
|--------|--------|-------------|
|<span data-ttu-id="f6ef9-155">Hadoop</span><span class="sxs-lookup"><span data-stu-id="f6ef9-155">Hadoop</span></span>|<span data-ttu-id="f6ef9-156">Hive – Interactive Jobs/Queries</span><span class="sxs-lookup"><span data-stu-id="f6ef9-156">Hive – Interactive Jobs/Queries</span></span> |<ul><li>[<span data-ttu-id="f6ef9-157">Beeline</span><span class="sxs-lookup"><span data-stu-id="f6ef9-157">Beeline</span></span>](#beeline)</li><li>[<span data-ttu-id="f6ef9-158">Hive View</span><span class="sxs-lookup"><span data-stu-id="f6ef9-158">Hive View</span></span>](../hadoop/apache-hadoop-use-hive-ambari-view.md)</li><li>[<span data-ttu-id="f6ef9-159">ODBC/JDBC – Power BI</span><span class="sxs-lookup"><span data-stu-id="f6ef9-159">ODBC/JDBC – Power BI</span></span>](../hadoop/apache-hadoop-connect-hive-power-bi.md)</li><li>[<span data-ttu-id="f6ef9-160">Visual Studio Tools</span><span class="sxs-lookup"><span data-stu-id="f6ef9-160">Visual Studio Tools</span></span>](../hadoop/apache-hadoop-visual-studio-tools-get-started.md)</li></ul>|
|<span data-ttu-id="f6ef9-161">Spark</span><span class="sxs-lookup"><span data-stu-id="f6ef9-161">Spark</span></span>|<span data-ttu-id="f6ef9-162">Interactive Jobs/Queries, PySpark interactive</span><span class="sxs-lookup"><span data-stu-id="f6ef9-162">Interactive Jobs/Queries, PySpark interactive</span></span>|<ul><li>[<span data-ttu-id="f6ef9-163">Beeline</span><span class="sxs-lookup"><span data-stu-id="f6ef9-163">Beeline</span></span>](#beeline)</li><li>[<span data-ttu-id="f6ef9-164">Zeppelin with Livy</span><span class="sxs-lookup"><span data-stu-id="f6ef9-164">Zeppelin with Livy</span></span>](../spark/apache-spark-zeppelin-notebook.md)</li><li>[<span data-ttu-id="f6ef9-165">Hive View</span><span class="sxs-lookup"><span data-stu-id="f6ef9-165">Hive View</span></span>](../hadoop/apache-hadoop-use-hive-ambari-view.md)</li><li>[<span data-ttu-id="f6ef9-166">ODBC/JDBC – Power BI</span><span class="sxs-lookup"><span data-stu-id="f6ef9-166">ODBC/JDBC – Power BI</span></span>](../hadoop/apache-hadoop-connect-hive-power-bi.md)</li><li>[<span data-ttu-id="f6ef9-167">Visual Studio Tools</span><span class="sxs-lookup"><span data-stu-id="f6ef9-167">Visual Studio Tools</span></span>](../hadoop/apache-hadoop-visual-studio-tools-get-started.md)</li></ul>|
|<span data-ttu-id="f6ef9-168">Spark</span><span class="sxs-lookup"><span data-stu-id="f6ef9-168">Spark</span></span>|<span data-ttu-id="f6ef9-169">Batch Scenarios – Spark submit, PySpark</span><span class="sxs-lookup"><span data-stu-id="f6ef9-169">Batch Scenarios – Spark submit, PySpark</span></span>|<ul><li>[<span data-ttu-id="f6ef9-170">Livy</span><span class="sxs-lookup"><span data-stu-id="f6ef9-170">Livy</span></span>](../spark/apache-spark-livy-rest-interface.md)</li></ul>|
|<span data-ttu-id="f6ef9-171">Interactive Query (LLAP)</span><span class="sxs-lookup"><span data-stu-id="f6ef9-171">Interactive Query (LLAP)</span></span>|<span data-ttu-id="f6ef9-172">Interactive</span><span class="sxs-lookup"><span data-stu-id="f6ef9-172">Interactive</span></span>|<ul><li>[<span data-ttu-id="f6ef9-173">Beeline</span><span class="sxs-lookup"><span data-stu-id="f6ef9-173">Beeline</span></span>](#beeline)</li><li>[<span data-ttu-id="f6ef9-174">Hive View</span><span class="sxs-lookup"><span data-stu-id="f6ef9-174">Hive View</span></span>](../hadoop/apache-hadoop-use-hive-ambari-view.md)</li><li>[<span data-ttu-id="f6ef9-175">ODBC/JDBC – Power BI</span><span class="sxs-lookup"><span data-stu-id="f6ef9-175">ODBC/JDBC – Power BI</span></span>](../hadoop/apache-hadoop-connect-hive-power-bi.md)</li><li>[<span data-ttu-id="f6ef9-176">Visual Studio Tools</span><span class="sxs-lookup"><span data-stu-id="f6ef9-176">Visual Studio Tools</span></span>](../hadoop/apache-hadoop-visual-studio-tools-get-started.md)</li></ul>|
|<span data-ttu-id="f6ef9-177">Any</span><span class="sxs-lookup"><span data-stu-id="f6ef9-177">Any</span></span>|<span data-ttu-id="f6ef9-178">Install Custom Application</span><span class="sxs-lookup"><span data-stu-id="f6ef9-178">Install Custom Application</span></span>|<ul><li>[<span data-ttu-id="f6ef9-179">Script Actions</span><span class="sxs-lookup"><span data-stu-id="f6ef9-179">Script Actions</span></span>](../hdinsight-hadoop-customize-cluster-linux.md)</li></ul>|

   > [!NOTE]
   > <span data-ttu-id="f6ef9-180">Jupyter is not installed/supported in Enterprise Security Package.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-180">Jupyter is not installed/supported in Enterprise Security Package.</span></span>

<span data-ttu-id="f6ef9-181">Using the standard APIs helps from security perspective.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-181">Using the standard APIs helps from security perspective.</span></span> <span data-ttu-id="f6ef9-182">In addition, you get the following benefits:</span><span class="sxs-lookup"><span data-stu-id="f6ef9-182">In addition, you get the following benefits:</span></span>

1.  <span data-ttu-id="f6ef9-183">**Management** – You can manage your code and automate jobs using standard APIs – Livy, HS2 etc.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-183">**Management** – You can manage your code and automate jobs using standard APIs – Livy, HS2 etc.</span></span>
2.  <span data-ttu-id="f6ef9-184">**Audit** – With SSH, there is no way to audit, which users SSH’d to the cluster.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-184">**Audit** – With SSH, there is no way to audit, which users SSH’d to the cluster.</span></span> <span data-ttu-id="f6ef9-185">This wouldn’t be the case when jobs are constructed via standard endpoints as they would be executed in context of user.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-185">This wouldn’t be the case when jobs are constructed via standard endpoints as they would be executed in context of user.</span></span> 



### <a name="beeline"></a><span data-ttu-id="f6ef9-186">Use Beeline</span><span class="sxs-lookup"><span data-stu-id="f6ef9-186">Use Beeline</span></span> 
<span data-ttu-id="f6ef9-187">Install Beeline on your machine, and connect over the public internet, use the following parameters:</span><span class="sxs-lookup"><span data-stu-id="f6ef9-187">Install Beeline on your machine, and connect over the public internet, use the following parameters:</span></span> 

```
- Connection string: -u 'jdbc:hive2://<clustername>.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'
- Cluster login name: -n admin
- Cluster login password -p 'password'
```

<span data-ttu-id="f6ef9-188">If you have Beeline installed locally, and connect over an Azure Virtual Network, use the following parameters:</span><span class="sxs-lookup"><span data-stu-id="f6ef9-188">If you have Beeline installed locally, and connect over an Azure Virtual Network, use the following parameters:</span></span> 

```
- Connection string: -u 'jdbc:hive2://<headnode-FQDN>:10001/;transportMode=http'
```

<span data-ttu-id="f6ef9-189">To find the fully qualified domain name of a headnode, use the information in the Manage HDInsight using the Ambari REST API document.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-189">To find the fully qualified domain name of a headnode, use the information in the Manage HDInsight using the Ambari REST API document.</span></span>














## <a name="users-of-domain-joined-hdinsight-clusters"></a><span data-ttu-id="f6ef9-190">Users of Domain-joined HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="f6ef9-190">Users of Domain-joined HDInsight clusters</span></span>
<span data-ttu-id="f6ef9-191">An HDInsight cluster that is not domain-joined has two user accounts that are created during the cluster creation:</span><span class="sxs-lookup"><span data-stu-id="f6ef9-191">An HDInsight cluster that is not domain-joined has two user accounts that are created during the cluster creation:</span></span>

* <span data-ttu-id="f6ef9-192">**Ambari admin**: This account is also known as *Hadoop user* or *HTTP user*.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-192">**Ambari admin**: This account is also known as *Hadoop user* or *HTTP user*.</span></span> <span data-ttu-id="f6ef9-193">This account can be used to log on to Ambari at https://&lt;clustername>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-193">This account can be used to log on to Ambari at https://&lt;clustername>.azurehdinsight.net.</span></span> <span data-ttu-id="f6ef9-194">It can also be used to run queries on Ambari views, execute jobs via external tools (for example, PowerShell, Templeton, Visual Studio), and authenticate with the Hive ODBC driver and BI tools (for example, Excel, PowerBI, or Tableau).</span><span class="sxs-lookup"><span data-stu-id="f6ef9-194">It can also be used to run queries on Ambari views, execute jobs via external tools (for example, PowerShell, Templeton, Visual Studio), and authenticate with the Hive ODBC driver and BI tools (for example, Excel, PowerBI, or Tableau).</span></span>

<span data-ttu-id="f6ef9-195">A domain-joined HDInsight cluster has three new users in addition to Ambari Admin.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-195">A domain-joined HDInsight cluster has three new users in addition to Ambari Admin.</span></span>

* <span data-ttu-id="f6ef9-196">**Ranger admin**:  This account is the local Apache Ranger admin account.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-196">**Ranger admin**:  This account is the local Apache Ranger admin account.</span></span> <span data-ttu-id="f6ef9-197">It is not an active directory domain user.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-197">It is not an active directory domain user.</span></span> <span data-ttu-id="f6ef9-198">This account can be used to setup policies and make other users admins or delegated admins (so that those users can manage policies).</span><span class="sxs-lookup"><span data-stu-id="f6ef9-198">This account can be used to setup policies and make other users admins or delegated admins (so that those users can manage policies).</span></span> <span data-ttu-id="f6ef9-199">By default, the username is *admin* and the password is the same as the Ambari admin password.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-199">By default, the username is *admin* and the password is the same as the Ambari admin password.</span></span> <span data-ttu-id="f6ef9-200">The password can be updated from the Settings page in Ranger.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-200">The password can be updated from the Settings page in Ranger.</span></span>
* <span data-ttu-id="f6ef9-201">**Cluster admin domain user**: This account is an active directory domain user designated as the Hadoop cluster admin including Ambari and Ranger.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-201">**Cluster admin domain user**: This account is an active directory domain user designated as the Hadoop cluster admin including Ambari and Ranger.</span></span> <span data-ttu-id="f6ef9-202">You must provide this user’s credentials during cluster creation.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-202">You must provide this user’s credentials during cluster creation.</span></span> <span data-ttu-id="f6ef9-203">This user has the following privileges:</span><span class="sxs-lookup"><span data-stu-id="f6ef9-203">This user has the following privileges:</span></span>

  * <span data-ttu-id="f6ef9-204">Join machines to the domain and place them within the OU that you specify during cluster creation.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-204">Join machines to the domain and place them within the OU that you specify during cluster creation.</span></span>
  * <span data-ttu-id="f6ef9-205">Create service principals within the OU that you specify during cluster creation.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-205">Create service principals within the OU that you specify during cluster creation.</span></span>
  * <span data-ttu-id="f6ef9-206">Create reverse DNS entries.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-206">Create reverse DNS entries.</span></span>

    <span data-ttu-id="f6ef9-207">Note the other AD users also have these privileges.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-207">Note the other AD users also have these privileges.</span></span>

    <span data-ttu-id="f6ef9-208">There are some end points within the cluster (for example, Templeton) which are not managed by Ranger, and hence are not secure.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-208">There are some end points within the cluster (for example, Templeton) which are not managed by Ranger, and hence are not secure.</span></span> <span data-ttu-id="f6ef9-209">These end points are locked down for all users except the cluster admin domain user.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-209">These end points are locked down for all users except the cluster admin domain user.</span></span>
* <span data-ttu-id="f6ef9-210">**Regular**: During cluster creation, you can provide multiple active directory groups.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-210">**Regular**: During cluster creation, you can provide multiple active directory groups.</span></span> <span data-ttu-id="f6ef9-211">The users in these groups are synced to Ranger and Ambari.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-211">The users in these groups are synced to Ranger and Ambari.</span></span> <span data-ttu-id="f6ef9-212">These users are domain users and have access to only Ranger-managed endpoints (for example, Hiveserver2).</span><span class="sxs-lookup"><span data-stu-id="f6ef9-212">These users are domain users and have access to only Ranger-managed endpoints (for example, Hiveserver2).</span></span> <span data-ttu-id="f6ef9-213">All the RBAC policies and auditing will be applicable to these users.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-213">All the RBAC policies and auditing will be applicable to these users.</span></span>

## <a name="roles-of-domain-joined-hdinsight-clusters"></a><span data-ttu-id="f6ef9-214">Roles of Domain-joined HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="f6ef9-214">Roles of Domain-joined HDInsight clusters</span></span>
<span data-ttu-id="f6ef9-215">Domain-joined HDInsight have the following roles:</span><span class="sxs-lookup"><span data-stu-id="f6ef9-215">Domain-joined HDInsight have the following roles:</span></span>

* <span data-ttu-id="f6ef9-216">Cluster Administrator</span><span class="sxs-lookup"><span data-stu-id="f6ef9-216">Cluster Administrator</span></span>
* <span data-ttu-id="f6ef9-217">Cluster Operator</span><span class="sxs-lookup"><span data-stu-id="f6ef9-217">Cluster Operator</span></span>
* <span data-ttu-id="f6ef9-218">Service Administrator</span><span class="sxs-lookup"><span data-stu-id="f6ef9-218">Service Administrator</span></span>
* <span data-ttu-id="f6ef9-219">Service Operator</span><span class="sxs-lookup"><span data-stu-id="f6ef9-219">Service Operator</span></span>
* <span data-ttu-id="f6ef9-220">Cluster User</span><span class="sxs-lookup"><span data-stu-id="f6ef9-220">Cluster User</span></span>

<span data-ttu-id="f6ef9-221">**To see the permissions of these roles**</span><span class="sxs-lookup"><span data-stu-id="f6ef9-221">**To see the permissions of these roles**</span></span>

1. <span data-ttu-id="f6ef9-222">Open the Ambari Management UI.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-222">Open the Ambari Management UI.</span></span>  <span data-ttu-id="f6ef9-223">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="f6ef9-223">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="f6ef9-224">From the left menu, click **Roles**.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-224">From the left menu, click **Roles**.</span></span>
3. <span data-ttu-id="f6ef9-225">Click the blue question mark to see the permissions:</span><span class="sxs-lookup"><span data-stu-id="f6ef9-225">Click the blue question mark to see the permissions:</span></span>

    ![Domain-joined HDInsight roles permissions](./media/apache-domain-joined-manage/hdinsight-domain-joined-roles-permissions.png)

## <a name="open-the-ambari-management-ui"></a><span data-ttu-id="f6ef9-227">Open the Ambari Management UI</span><span class="sxs-lookup"><span data-stu-id="f6ef9-227">Open the Ambari Management UI</span></span>

1. <span data-ttu-id="f6ef9-228">Sign on to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f6ef9-228">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f6ef9-229">Open your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-229">Open your HDInsight cluster.</span></span> <span data-ttu-id="f6ef9-230">See [List and show clusters](../hdinsight-administer-use-management-portal.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="f6ef9-230">See [List and show clusters](../hdinsight-administer-use-management-portal.md#list-and-show-clusters).</span></span>
3. <span data-ttu-id="f6ef9-231">Click **Dashboard** from the top menu to open Ambari.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-231">Click **Dashboard** from the top menu to open Ambari.</span></span>
4. <span data-ttu-id="f6ef9-232">Log on to Ambari using the cluster administrator domain user name and password.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-232">Log on to Ambari using the cluster administrator domain user name and password.</span></span>
5. <span data-ttu-id="f6ef9-233">Click the **Admin** dropdown menu from the upper right corner, and then click **Manage Ambari**.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-233">Click the **Admin** dropdown menu from the upper right corner, and then click **Manage Ambari**.</span></span>

    ![Domain-joined HDInsight manage Ambari](./media/apache-domain-joined-manage/hdinsight-domain-joined-manage-ambari.png)

    <span data-ttu-id="f6ef9-235">The UI looks like:</span><span class="sxs-lookup"><span data-stu-id="f6ef9-235">The UI looks like:</span></span>

    ![Domain-joined HDInsight Ambari management UI](./media/apache-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui.png)

## <a name="list-the-domain-users-synchronized-from-your-active-directory"></a><span data-ttu-id="f6ef9-237">List the domain users synchronized from your Active Directory</span><span class="sxs-lookup"><span data-stu-id="f6ef9-237">List the domain users synchronized from your Active Directory</span></span>
1. <span data-ttu-id="f6ef9-238">Open the Ambari Management UI.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-238">Open the Ambari Management UI.</span></span>  <span data-ttu-id="f6ef9-239">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="f6ef9-239">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="f6ef9-240">From the left menu, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-240">From the left menu, click **Users**.</span></span> <span data-ttu-id="f6ef9-241">You shall see all the users synced from your Active Directory to the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-241">You shall see all the users synced from your Active Directory to the HDInsight cluster.</span></span>

    ![Domain-joined HDInsight Ambari management UI list users](./media/apache-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-users.png)

## <a name="list-the-domain-groups-synchronized-from-your-active-directory"></a><span data-ttu-id="f6ef9-243">List the domain groups synchronized from your Active Directory</span><span class="sxs-lookup"><span data-stu-id="f6ef9-243">List the domain groups synchronized from your Active Directory</span></span>
1. <span data-ttu-id="f6ef9-244">Open the Ambari Management UI.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-244">Open the Ambari Management UI.</span></span>  <span data-ttu-id="f6ef9-245">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="f6ef9-245">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="f6ef9-246">From the left menu, click **Groups**.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-246">From the left menu, click **Groups**.</span></span> <span data-ttu-id="f6ef9-247">You shall see all the groups synced from your Active Directory to the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-247">You shall see all the groups synced from your Active Directory to the HDInsight cluster.</span></span>

    ![Domain-joined HDInsight Ambari management UI list groups](./media/apache-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-groups.png)

## <a name="configure-hive-views-permissions"></a><span data-ttu-id="f6ef9-249">Configure Hive Views permissions</span><span class="sxs-lookup"><span data-stu-id="f6ef9-249">Configure Hive Views permissions</span></span>
1. <span data-ttu-id="f6ef9-250">Open the Ambari Management UI.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-250">Open the Ambari Management UI.</span></span>  <span data-ttu-id="f6ef9-251">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="f6ef9-251">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="f6ef9-252">From the left menu, click **Views**.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-252">From the left menu, click **Views**.</span></span>
3. <span data-ttu-id="f6ef9-253">Click **HIVE** to show the details.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-253">Click **HIVE** to show the details.</span></span>

    ![Domain-joined HDInsight Ambari management UI Hive Views](./media/apache-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views.png)
4. <span data-ttu-id="f6ef9-255">Click the **Hive View** link to configure Hive Views.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-255">Click the **Hive View** link to configure Hive Views.</span></span>
5. <span data-ttu-id="f6ef9-256">Scroll down to the **Permissions** section.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-256">Scroll down to the **Permissions** section.</span></span>

    ![Domain-joined HDInsight Ambari management UI Hive Views configure permissions](./media/apache-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views-permissions.png)
6. <span data-ttu-id="f6ef9-258">Click **Add User** or **Add Group**, and then specify the users or groups that can use Hive Views.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-258">Click **Add User** or **Add Group**, and then specify the users or groups that can use Hive Views.</span></span>

## <a name="configure-users-for-the-roles"></a><span data-ttu-id="f6ef9-259">Configure users for the roles</span><span class="sxs-lookup"><span data-stu-id="f6ef9-259">Configure users for the roles</span></span>
 <span data-ttu-id="f6ef9-260">To see a list of roles and their permissions, see [Roles of Domain-joined HDInsight clusters](#roles-of-domain---joined-hdinsight-clusters).</span><span class="sxs-lookup"><span data-stu-id="f6ef9-260">To see a list of roles and their permissions, see [Roles of Domain-joined HDInsight clusters](#roles-of-domain---joined-hdinsight-clusters).</span></span>

1. <span data-ttu-id="f6ef9-261">Open the Ambari Management UI.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-261">Open the Ambari Management UI.</span></span>  <span data-ttu-id="f6ef9-262">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="f6ef9-262">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="f6ef9-263">From the left menu, click **Roles**.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-263">From the left menu, click **Roles**.</span></span>
3. <span data-ttu-id="f6ef9-264">Click **Add User** or **Add Group** to assign users and groups to different roles.</span><span class="sxs-lookup"><span data-stu-id="f6ef9-264">Click **Add User** or **Add Group** to assign users and groups to different roles.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6ef9-265">Next steps</span><span class="sxs-lookup"><span data-stu-id="f6ef9-265">Next steps</span></span>
* <span data-ttu-id="f6ef9-266">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](apache-domain-joined-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f6ef9-266">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](apache-domain-joined-configure.md).</span></span>
* <span data-ttu-id="f6ef9-267">For configuring Hive policies and run Hive queries, see [Configure Hive policies for Domain-joined HDInsight clusters](apache-domain-joined-run-hive.md).</span><span class="sxs-lookup"><span data-stu-id="f6ef9-267">For configuring Hive policies and run Hive queries, see [Configure Hive policies for Domain-joined HDInsight clusters](apache-domain-joined-run-hive.md).</span></span>
