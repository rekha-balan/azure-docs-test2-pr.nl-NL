---
title: Apache Hadoop Oozie workflows in Azure HDInsight domain-joined clusters
description: Use Hadoop Oozie in a Linux-based HDInsight domain-joined Enterprise Security Package. Learn how to define an Oozie workflow and submit an Oozie job.
services: hdinsight
ms.service: hdinsight
author: omidm1
ms.author: omidm
ms.reviewer: jasonh
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 06/26/2018
ms.openlocfilehash: 69bf885ad5d6244997c7ce9cf61bdee9e05c1826
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864605"
---
# <a name="run-apache-oozie-in-domain-joined-hdinsight-hadoop-clusters"></a><span data-ttu-id="ff697-104">Run Apache Oozie in domain-joined HDInsight Hadoop clusters</span><span class="sxs-lookup"><span data-stu-id="ff697-104">Run Apache Oozie in domain-joined HDInsight Hadoop clusters</span></span>
<span data-ttu-id="ff697-105">Oozie is a workflow and coordination system that manages Hadoop jobs.</span><span class="sxs-lookup"><span data-stu-id="ff697-105">Oozie is a workflow and coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="ff697-106">Oozie is integrated with the Hadoop stack, and it supports the following jobs:</span><span class="sxs-lookup"><span data-stu-id="ff697-106">Oozie is integrated with the Hadoop stack, and it supports the following jobs:</span></span>
- <span data-ttu-id="ff697-107">Apache MapReduce</span><span class="sxs-lookup"><span data-stu-id="ff697-107">Apache MapReduce</span></span>
- <span data-ttu-id="ff697-108">Apache Pig</span><span class="sxs-lookup"><span data-stu-id="ff697-108">Apache Pig</span></span>
- <span data-ttu-id="ff697-109">Apache Hive</span><span class="sxs-lookup"><span data-stu-id="ff697-109">Apache Hive</span></span>
- <span data-ttu-id="ff697-110">Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="ff697-110">Apache Sqoop</span></span>

<span data-ttu-id="ff697-111">You can also use Oozie to schedule jobs that are specific to a system, like Java programs or shell scripts.</span><span class="sxs-lookup"><span data-stu-id="ff697-111">You can also use Oozie to schedule jobs that are specific to a system, like Java programs or shell scripts.</span></span>

## <a name="prerequisite"></a><span data-ttu-id="ff697-112">Prerequisite</span><span class="sxs-lookup"><span data-stu-id="ff697-112">Prerequisite</span></span>
- <span data-ttu-id="ff697-113">A domain-joined Azure HDInsight Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="ff697-113">A domain-joined Azure HDInsight Hadoop cluster.</span></span> <span data-ttu-id="ff697-114">See [Configure domain-joined HDInsight clusters](./apache-domain-joined-configure-using-azure-adds.md).</span><span class="sxs-lookup"><span data-stu-id="ff697-114">See [Configure domain-joined HDInsight clusters](./apache-domain-joined-configure-using-azure-adds.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="ff697-115">For detailed instructions on using Oozie on nondomain-joined clusters, see [Use Hadoop Oozie workflows in Linux-based Azure HDInsight](../hdinsight-use-oozie-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="ff697-115">For detailed instructions on using Oozie on nondomain-joined clusters, see [Use Hadoop Oozie workflows in Linux-based Azure HDInsight](../hdinsight-use-oozie-linux-mac.md).</span></span>

## <a name="connect-to-a-domain-joined-cluster"></a><span data-ttu-id="ff697-116">Connect to a domain-joined cluster</span><span class="sxs-lookup"><span data-stu-id="ff697-116">Connect to a domain-joined cluster</span></span>

<span data-ttu-id="ff697-117">For more information on Secure Shell (SSH), see [Connect to HDInsight (Hadoop) using SSH](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="ff697-117">For more information on Secure Shell (SSH), see [Connect to HDInsight (Hadoop) using SSH](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="ff697-118">Connect to the HDInsight cluster by using SSH:</span><span class="sxs-lookup"><span data-stu-id="ff697-118">Connect to the HDInsight cluster by using SSH:</span></span>  
 ```bash
ssh [DomainUserName]@<clustername>-ssh.azurehdinsight.net
 ```

2. <span data-ttu-id="ff697-119">To verify successful Kerberos authentication, use the `klist` command.</span><span class="sxs-lookup"><span data-stu-id="ff697-119">To verify successful Kerberos authentication, use the `klist` command.</span></span> <span data-ttu-id="ff697-120">If not, use `kinit` to start Kerberos authentication.</span><span class="sxs-lookup"><span data-stu-id="ff697-120">If not, use `kinit` to start Kerberos authentication.</span></span>

3. <span data-ttu-id="ff697-121">Sign in to the HDInsight gateway to register the OAuth token required to access Azure Data Lake Storage:</span><span class="sxs-lookup"><span data-stu-id="ff697-121">Sign in to the HDInsight gateway to register the OAuth token required to access Azure Data Lake Storage:</span></span>   
     ```bash
     curl -I -u [DomainUserName@Domain.com]:[DomainUserPassword] https://<clustername>.azurehdinsight.net
     ```

    <span data-ttu-id="ff697-122">A status response code of **200 OK** indicates successful registration.</span><span class="sxs-lookup"><span data-stu-id="ff697-122">A status response code of **200 OK** indicates successful registration.</span></span> <span data-ttu-id="ff697-123">Check the username and password if an unauthorized response is received, such as 401.</span><span class="sxs-lookup"><span data-stu-id="ff697-123">Check the username and password if an unauthorized response is received, such as 401.</span></span>

## <a name="define-the-workflow"></a><span data-ttu-id="ff697-124">Define the workflow</span><span class="sxs-lookup"><span data-stu-id="ff697-124">Define the workflow</span></span>
<span data-ttu-id="ff697-125">Oozie workflow definitions are written in Hadoop Process Definition Language (hPDL).</span><span class="sxs-lookup"><span data-stu-id="ff697-125">Oozie workflow definitions are written in Hadoop Process Definition Language (hPDL).</span></span> <span data-ttu-id="ff697-126">hPDL is an XML process definition language.</span><span class="sxs-lookup"><span data-stu-id="ff697-126">hPDL is an XML process definition language.</span></span> <span data-ttu-id="ff697-127">Take the following steps to define the workflow:</span><span class="sxs-lookup"><span data-stu-id="ff697-127">Take the following steps to define the workflow:</span></span>

1.  <span data-ttu-id="ff697-128">Set up a domain user’s workspace:</span><span class="sxs-lookup"><span data-stu-id="ff697-128">Set up a domain user’s workspace:</span></span>
 ```bash
hdfs dfs -mkdir /user/<DomainUser>
cd /home/<DomainUserPath>
cp /usr/hdp/<ClusterVersion>/oozie/doc/oozie-examples.tar.gz .
tar -xvf oozie-examples.tar.gz
hdfs dfs -put examples /user/<DomainUser>/
 ```
<span data-ttu-id="ff697-129">Replace `DomainUser` with the domain user name.</span><span class="sxs-lookup"><span data-stu-id="ff697-129">Replace `DomainUser` with the domain user name.</span></span> <span data-ttu-id="ff697-130">Replace `DomainUserPath` with the home directory path for the domain user.</span><span class="sxs-lookup"><span data-stu-id="ff697-130">Replace `DomainUserPath` with the home directory path for the domain user.</span></span> <span data-ttu-id="ff697-131">Replace `ClusterVersion` with your cluster Hortonworks Data Platform (HDP) version.</span><span class="sxs-lookup"><span data-stu-id="ff697-131">Replace `ClusterVersion` with your cluster Hortonworks Data Platform (HDP) version.</span></span>

2.  <span data-ttu-id="ff697-132">Use the following statement to create and edit a new file:</span><span class="sxs-lookup"><span data-stu-id="ff697-132">Use the following statement to create and edit a new file:</span></span>
 ```bash
nano workflow.xml
 ```

3. <span data-ttu-id="ff697-133">After the nano editor opens, enter the following XML as the file contents:</span><span class="sxs-lookup"><span data-stu-id="ff697-133">After the nano editor opens, enter the following XML as the file contents:</span></span>
 ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <workflow-app xmlns="uri:oozie:workflow:0.4" name="map-reduce-wf">
       <credentials>
          <credential name="metastore_token" type="hcat">
             <property>
                <name>hcat.metastore.uri</name>
                <value>thrift://hn0-<clustername>.<Domain>.com:9083</value>
             </property>
             <property>
                <name>hcat.metastore.principal</name>
                <value>hive/_HOST@<Domain>.COM</value>
             </property>
          </credential>
          <credential name="hs2-creds" type="hive2">
             <property>
                <name>hive2.server.principal</name>
                <value>${jdbcPrincipal}</value>
             </property>
             <property>
                <name>hive2.jdbc.url</name>
                <value>${jdbcURL}</value>
             </property>
          </credential>
       </credentials>
       <start to="mr-test" />
       <action name="mr-test">
          <map-reduce>
             <job-tracker>${jobTracker}</job-tracker>
             <name-node>${nameNode}</name-node>
             <prepare>
                <delete path="${nameNode}/user/${wf:user()}/examples/output-data/mrresult" />
             </prepare>
             <configuration>
                <property>
                   <name>mapred.job.queue.name</name>
                   <value>${queueName}</value>
                </property>
                <property>
                   <name>mapred.mapper.class</name>
                   <value>org.apache.oozie.example.SampleMapper</value>
                </property>
                <property>
                   <name>mapred.reducer.class</name>
                   <value>org.apache.oozie.example.SampleReducer</value>
                </property>
                <property>
                   <name>mapred.map.tasks</name>
                   <value>1</value>
                </property>
                <property>
                   <name>mapred.input.dir</name>
                   <value>/user/${wf:user()}/${examplesRoot}/input-data/text</value>
                </property>
                <property>
                   <name>mapred.output.dir</name>
                   <value>/user/${wf:user()}/${examplesRoot}/output-data/mrresult</value>
                </property>
             </configuration>
          </map-reduce>
          <ok to="myHive2" />
          <error to="fail" />
       </action>
       <action name="myHive2" cred="hs2-creds">
          <hive2 xmlns="uri:oozie:hive2-action:0.2">
             <job-tracker>${jobTracker}</job-tracker>
             <name-node>${nameNode}</name-node>
             <jdbc-url>${jdbcURL}</jdbc-url>
             <script>${hiveScript2}</script>
             <param>hiveOutputDirectory2=${hiveOutputDirectory2}</param>
          </hive2>
          <ok to="myHive" />
          <error to="fail" />
       </action>
       <action name="myHive" cred="metastore_token">
          <hive xmlns="uri:oozie:hive-action:0.2">
             <job-tracker>${jobTracker}</job-tracker>
             <name-node>${nameNode}</name-node>
             <configuration>
                <property>
                   <name>mapred.job.queue.name</name>
                   <value>${queueName}</value>
                </property>
             </configuration>
             <script>${hiveScript1}</script>
             <param>hiveOutputDirectory1=${hiveOutputDirectory1}</param>
          </hive>
          <ok to="end" />
          <error to="fail" />
       </action>
       <kill name="fail">
          <message>Oozie job failed, error message[${wf:errorMessage(wf:lastErrorNode())}]</message>
       </kill>
       <end name="end" />
    </workflow-app>
 ```
4. <span data-ttu-id="ff697-134">Replace `clustername` with the name of the cluster.</span><span class="sxs-lookup"><span data-stu-id="ff697-134">Replace `clustername` with the name of the cluster.</span></span> 

5. <span data-ttu-id="ff697-135">To save the file, select Ctrl+X.</span><span class="sxs-lookup"><span data-stu-id="ff697-135">To save the file, select Ctrl+X.</span></span> <span data-ttu-id="ff697-136">Enter `Y`.</span><span class="sxs-lookup"><span data-stu-id="ff697-136">Enter `Y`.</span></span> <span data-ttu-id="ff697-137">Then select **Enter**.</span><span class="sxs-lookup"><span data-stu-id="ff697-137">Then select **Enter**.</span></span>

    <span data-ttu-id="ff697-138">The workflow is divided into two parts:</span><span class="sxs-lookup"><span data-stu-id="ff697-138">The workflow is divided into two parts:</span></span>
    *   <span data-ttu-id="ff697-139">**Credential section.**</span><span class="sxs-lookup"><span data-stu-id="ff697-139">**Credential section.**</span></span> <span data-ttu-id="ff697-140">This section takes in the credentials that are used for authenticating Oozie actions:</span><span class="sxs-lookup"><span data-stu-id="ff697-140">This section takes in the credentials that are used for authenticating Oozie actions:</span></span>

       <span data-ttu-id="ff697-141">This example uses authentication for Hive actions.</span><span class="sxs-lookup"><span data-stu-id="ff697-141">This example uses authentication for Hive actions.</span></span> <span data-ttu-id="ff697-142">To learn more, see [Action Authentication](https://oozie.apache.org/docs/4.2.0/DG_ActionAuthentication.html).</span><span class="sxs-lookup"><span data-stu-id="ff697-142">To learn more, see [Action Authentication](https://oozie.apache.org/docs/4.2.0/DG_ActionAuthentication.html).</span></span>

       <span data-ttu-id="ff697-143">The credential service allows Oozie actions to impersonate the user for accessing Hadoop services.</span><span class="sxs-lookup"><span data-stu-id="ff697-143">The credential service allows Oozie actions to impersonate the user for accessing Hadoop services.</span></span>

    *   <span data-ttu-id="ff697-144">**Action section.**</span><span class="sxs-lookup"><span data-stu-id="ff697-144">**Action section.**</span></span> <span data-ttu-id="ff697-145">This section has three actions: map-reduce, Hive server 2, and Hive server 1:</span><span class="sxs-lookup"><span data-stu-id="ff697-145">This section has three actions: map-reduce, Hive server 2, and Hive server 1:</span></span>

      - <span data-ttu-id="ff697-146">The map-reduce action runs an example from an Oozie package for map-reduce that outputs the aggregated word count.</span><span class="sxs-lookup"><span data-stu-id="ff697-146">The map-reduce action runs an example from an Oozie package for map-reduce that outputs the aggregated word count.</span></span>

       - <span data-ttu-id="ff697-147">The Hive server 2 and Hive server 1 actions run a query on a sample Hive table provided with HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ff697-147">The Hive server 2 and Hive server 1 actions run a query on a sample Hive table provided with HDInsight.</span></span>

        <span data-ttu-id="ff697-148">The Hive actions use the credentials defined in the credentials section for authentication by using the keyword `cred` in the action element.</span><span class="sxs-lookup"><span data-stu-id="ff697-148">The Hive actions use the credentials defined in the credentials section for authentication by using the keyword `cred` in the action element.</span></span>

6. <span data-ttu-id="ff697-149">Use the following command to copy the `workflow.xml` file to `/user/<domainuser>/examples/apps/map-reduce/workflow.xml`:</span><span class="sxs-lookup"><span data-stu-id="ff697-149">Use the following command to copy the `workflow.xml` file to `/user/<domainuser>/examples/apps/map-reduce/workflow.xml`:</span></span>
     ```bash
    hdfs dfs -put workflow.xml /user/<domainuser>/examples/apps/map-reduce/workflow.xml
     ```

7. <span data-ttu-id="ff697-150">Replace `domainuser` with your username for the domain.</span><span class="sxs-lookup"><span data-stu-id="ff697-150">Replace `domainuser` with your username for the domain.</span></span>

## <a name="define-the-properties-file-for-the-oozie-job"></a><span data-ttu-id="ff697-151">Define the properties file for the Oozie job</span><span class="sxs-lookup"><span data-stu-id="ff697-151">Define the properties file for the Oozie job</span></span>

1. <span data-ttu-id="ff697-152">Use the following statement to create and edit a new file for job properties:</span><span class="sxs-lookup"><span data-stu-id="ff697-152">Use the following statement to create and edit a new file for job properties:</span></span>

   ```bash
   nano job.properties
   ```

2. <span data-ttu-id="ff697-153">After the nano editor opens, use the following XML as the contents of the file:</span><span class="sxs-lookup"><span data-stu-id="ff697-153">After the nano editor opens, use the following XML as the contents of the file:</span></span>

   ```bash
       nameNode=adl://home
       jobTracker=headnodehost:8050
       queueName=default
       examplesRoot=examples
       oozie.wf.application.path=${nameNode}/user/[domainuser]/examples/apps/map-reduce/workflow.xml
       hiveScript1=${nameNode}/user/${user.name}/countrowshive1.hql
       hiveScript2=${nameNode}/user/${user.name}/countrowshive2.hql
       oozie.use.system.libpath=true
       user.name=[domainuser]
       jdbcPrincipal=hive/hn0-<ClusterShortName>.<Domain>.com@<Domain>.COM
       jdbcURL=[jdbcurlvalue]
       hiveOutputDirectory1=${nameNode}/user/${user.name}/hiveresult1
       hiveOutputDirectory2=${nameNode}/user/${user.name}/hiveresult2
   ```
  
   <span data-ttu-id="ff697-154">a.</span><span class="sxs-lookup"><span data-stu-id="ff697-154">a.</span></span> <span data-ttu-id="ff697-155">Replace `domainuser` with your username for the domain.</span><span class="sxs-lookup"><span data-stu-id="ff697-155">Replace `domainuser` with your username for the domain.</span></span>  
   <span data-ttu-id="ff697-156">b.</span><span class="sxs-lookup"><span data-stu-id="ff697-156">b.</span></span> <span data-ttu-id="ff697-157">Replace `ClusterShortName` with the short name for the cluster.</span><span class="sxs-lookup"><span data-stu-id="ff697-157">Replace `ClusterShortName` with the short name for the cluster.</span></span> <span data-ttu-id="ff697-158">For example, if the cluster name is https:// *[example link]* sechadoopcontoso.azurehdisnight.net, the `clustershortname` is the first six characters of the cluster: **sechad**.</span><span class="sxs-lookup"><span data-stu-id="ff697-158">For example, if the cluster name is https:// *[example link]* sechadoopcontoso.azurehdisnight.net, the `clustershortname` is the first six characters of the cluster: **sechad**.</span></span>  
   <span data-ttu-id="ff697-159">c.</span><span class="sxs-lookup"><span data-stu-id="ff697-159">c.</span></span> <span data-ttu-id="ff697-160">Replace `jdbcurlvalue` with the JDBC URL from the Hive configuration.</span><span class="sxs-lookup"><span data-stu-id="ff697-160">Replace `jdbcurlvalue` with the JDBC URL from the Hive configuration.</span></span> <span data-ttu-id="ff697-161">An example is jdbc:hive2://headnodehost:10001/;transportMode=http.</span><span class="sxs-lookup"><span data-stu-id="ff697-161">An example is jdbc:hive2://headnodehost:10001/;transportMode=http.</span></span>      
   <span data-ttu-id="ff697-162">d.</span><span class="sxs-lookup"><span data-stu-id="ff697-162">d.</span></span> <span data-ttu-id="ff697-163">To save the file, select Ctrl+X, enter `Y`, and then select **Enter**.</span><span class="sxs-lookup"><span data-stu-id="ff697-163">To save the file, select Ctrl+X, enter `Y`, and then select **Enter**.</span></span>

   <span data-ttu-id="ff697-164">This properties file needs to be present locally when running Oozie jobs.</span><span class="sxs-lookup"><span data-stu-id="ff697-164">This properties file needs to be present locally when running Oozie jobs.</span></span>

## <a name="create-custom-hive-scripts-for-oozie-jobs"></a><span data-ttu-id="ff697-165">Create custom Hive scripts for Oozie jobs</span><span class="sxs-lookup"><span data-stu-id="ff697-165">Create custom Hive scripts for Oozie jobs</span></span>
<span data-ttu-id="ff697-166">You can create the two Hive scripts for Hive server 1 and Hive server 2 as shown in the following sections.</span><span class="sxs-lookup"><span data-stu-id="ff697-166">You can create the two Hive scripts for Hive server 1 and Hive server 2 as shown in the following sections.</span></span>
### <a name="hive-server-1-file"></a><span data-ttu-id="ff697-167">Hive server 1 file</span><span class="sxs-lookup"><span data-stu-id="ff697-167">Hive server 1 file</span></span>
1.  <span data-ttu-id="ff697-168">Create and edit a file for Hive server 1 actions:</span><span class="sxs-lookup"><span data-stu-id="ff697-168">Create and edit a file for Hive server 1 actions:</span></span>
    ```bash
    nano countrowshive1.hql
    ```

2.  <span data-ttu-id="ff697-169">Create the script:</span><span class="sxs-lookup"><span data-stu-id="ff697-169">Create the script:</span></span>
    ```sql
    INSERT OVERWRITE DIRECTORY '${hiveOutputDirectory1}' 
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' 
    select devicemake from hivesampletable limit 2;
    ```

3.  <span data-ttu-id="ff697-170">Save the file to Hadoop Distributed File System (HDFS):</span><span class="sxs-lookup"><span data-stu-id="ff697-170">Save the file to Hadoop Distributed File System (HDFS):</span></span>
    ```bash
    hdfs dfs -put countrowshive1.hql countrowshive1.hql
    ```

### <a name="hive-server-2-file"></a><span data-ttu-id="ff697-171">Hive server 2 file</span><span class="sxs-lookup"><span data-stu-id="ff697-171">Hive server 2 file</span></span>
1.  <span data-ttu-id="ff697-172">Create and edit a field for Hive server 2 actions:</span><span class="sxs-lookup"><span data-stu-id="ff697-172">Create and edit a field for Hive server 2 actions:</span></span>
    ```bash
    nano countrowshive2.hql
    ```

2.  <span data-ttu-id="ff697-173">Create the script:</span><span class="sxs-lookup"><span data-stu-id="ff697-173">Create the script:</span></span>
    ```sql
    INSERT OVERWRITE DIRECTORY '${hiveOutputDirectory1}' 
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' 
    select devicemodel from hivesampletable limit 2;
    ```

3.  <span data-ttu-id="ff697-174">Save the file to HDFS:</span><span class="sxs-lookup"><span data-stu-id="ff697-174">Save the file to HDFS:</span></span>
    ```bash
    hdfs dfs -put countrowshive2.hql countrowshive2.hql
    ```

## <a name="submit-oozie-jobs"></a><span data-ttu-id="ff697-175">Submit Oozie jobs</span><span class="sxs-lookup"><span data-stu-id="ff697-175">Submit Oozie jobs</span></span>
<span data-ttu-id="ff697-176">Submitting Oozie jobs for domain-joined clusters is like submitting Oozie jobs in nondomain-joined clusters.</span><span class="sxs-lookup"><span data-stu-id="ff697-176">Submitting Oozie jobs for domain-joined clusters is like submitting Oozie jobs in nondomain-joined clusters.</span></span>

<span data-ttu-id="ff697-177">For more information, see [Use Oozie with Hadoop to define and run a workflow on Linux-based Azure HDInsight](../hdinsight-use-oozie-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="ff697-177">For more information, see [Use Oozie with Hadoop to define and run a workflow on Linux-based Azure HDInsight](../hdinsight-use-oozie-linux-mac.md).</span></span>

## <a name="results-from-an-oozie-job-submission"></a><span data-ttu-id="ff697-178">Results from an Oozie job submission</span><span class="sxs-lookup"><span data-stu-id="ff697-178">Results from an Oozie job submission</span></span>
<span data-ttu-id="ff697-179">Oozie jobs are run for the user.</span><span class="sxs-lookup"><span data-stu-id="ff697-179">Oozie jobs are run for the user.</span></span> <span data-ttu-id="ff697-180">So both Apache YARN and Apache Ranger audit logs show the jobs being run as the impersonated user.</span><span class="sxs-lookup"><span data-stu-id="ff697-180">So both Apache YARN and Apache Ranger audit logs show the jobs being run as the impersonated user.</span></span> <span data-ttu-id="ff697-181">The command-line interface output of an Oozie job looks like the following code:</span><span class="sxs-lookup"><span data-stu-id="ff697-181">The command-line interface output of an Oozie job looks like the following code:</span></span>


```bash
    Job ID : 0000015-180626011240801-oozie-oozi-W
    ------------------------------------------------------------------------------------------------
    Workflow Name : map-reduce-wf
    App Path      : adl://home/user/alicetest/examples/apps/map-reduce/wf.xml
    Status        : SUCCEEDED
    Run           : 0
    User          : alicetest
    Group         : -
    Created       : 2018-06-26 19:25 GMT
    Started       : 2018-06-26 19:25 GMT
    Last Modified : 2018-06-26 19:30 GMT
    Ended         : 2018-06-26 19:30 GMT
    CoordAction ID: -
    
    Actions
    ------------------------------------------------------------------------------------------------
    ID                      Status  Ext ID          ExtStatus   ErrCode
    ------------------------------------------------------------------------------------------------
    0000015-180626011240801-oozie-oozi-W@:start:    OK  -           OK      -
    ------------------------------------------------------------------------------------------------
    0000015-180626011240801-oozie-oozi-W@mr-test    OK  job_1529975666160_0051  SUCCEEDED   -
    ------------------------------------------------------------------------------------------------
    0000015-180626011240801-oozie-oozi-W@myHive2    OK  job_1529975666160_0053  SUCCEEDED   -
    ------------------------------------------------------------------------------------------------
    0000015-180626011240801-oozie-oozi-W@myHive OK  job_1529975666160_0055  SUCCEEDED   -
    ------------------------------------------------------------------------------------------------
    0000015-180626011240801-oozie-oozi-W@end    OK  -           OK      -
    -----------------------------------------------------------------------------------------------
```

<span data-ttu-id="ff697-182">The Ranger audit logs for Hive server 2 actions show Oozie running the action for the user.</span><span class="sxs-lookup"><span data-stu-id="ff697-182">The Ranger audit logs for Hive server 2 actions show Oozie running the action for the user.</span></span> <span data-ttu-id="ff697-183">The Ranger and YARN views are visible only to the cluster admin.</span><span class="sxs-lookup"><span data-stu-id="ff697-183">The Ranger and YARN views are visible only to the cluster admin.</span></span>

## <a name="configure-user-authorization-in-oozie"></a><span data-ttu-id="ff697-184">Configure user authorization in Oozie</span><span class="sxs-lookup"><span data-stu-id="ff697-184">Configure user authorization in Oozie</span></span>
<span data-ttu-id="ff697-185">Oozie by itself has a user authorization configuration that can block users from stopping or deleting other users' jobs.</span><span class="sxs-lookup"><span data-stu-id="ff697-185">Oozie by itself has a user authorization configuration that can block users from stopping or deleting other users' jobs.</span></span> <span data-ttu-id="ff697-186">To enable this configuration, set the `oozie.service.AuthorizationService.security.enabled` to `true`.</span><span class="sxs-lookup"><span data-stu-id="ff697-186">To enable this configuration, set the `oozie.service.AuthorizationService.security.enabled` to `true`.</span></span> 

<span data-ttu-id="ff697-187">For more information, see [Oozie Installation and Configuration](https://oozie.apache.org/docs/3.2.0-incubating/AG_Install.html).</span><span class="sxs-lookup"><span data-stu-id="ff697-187">For more information, see [Oozie Installation and Configuration](https://oozie.apache.org/docs/3.2.0-incubating/AG_Install.html).</span></span>

<span data-ttu-id="ff697-188">For components like Hive server 1 where the Ranger plug-in isn't available or supported, only coarse-grained HDFS authorization is possible.</span><span class="sxs-lookup"><span data-stu-id="ff697-188">For components like Hive server 1 where the Ranger plug-in isn't available or supported, only coarse-grained HDFS authorization is possible.</span></span> <span data-ttu-id="ff697-189">Fine-grained authorization is available only through Ranger plug-ins.</span><span class="sxs-lookup"><span data-stu-id="ff697-189">Fine-grained authorization is available only through Ranger plug-ins.</span></span>

## <a name="get-the-oozie-web-ui"></a><span data-ttu-id="ff697-190">Get the Oozie web UI</span><span class="sxs-lookup"><span data-stu-id="ff697-190">Get the Oozie web UI</span></span>
<span data-ttu-id="ff697-191">The Oozie web UI provides a web-based view into the status of Oozie jobs on the cluster.</span><span class="sxs-lookup"><span data-stu-id="ff697-191">The Oozie web UI provides a web-based view into the status of Oozie jobs on the cluster.</span></span> <span data-ttu-id="ff697-192">To get the web UI, take the following steps in domain-joined clusters:</span><span class="sxs-lookup"><span data-stu-id="ff697-192">To get the web UI, take the following steps in domain-joined clusters:</span></span>

1. <span data-ttu-id="ff697-193">Add an [edge node](../hdinsight-apps-use-edge-node.md) and enable [SSH Kerberos authentication](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="ff697-193">Add an [edge node](../hdinsight-apps-use-edge-node.md) and enable [SSH Kerberos authentication](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="ff697-194">Follow the [Oozie web UI](../hdinsight-use-oozie-linux-mac.md) steps to enable SSH tunneling to the edge node and access the web UI.</span><span class="sxs-lookup"><span data-stu-id="ff697-194">Follow the [Oozie web UI](../hdinsight-use-oozie-linux-mac.md) steps to enable SSH tunneling to the edge node and access the web UI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff697-195">Next steps</span><span class="sxs-lookup"><span data-stu-id="ff697-195">Next steps</span></span>
* <span data-ttu-id="ff697-196">[Use Oozie with Hadoop to define and run a workflow on Linux-based Azure HDInsight](../hdinsight-use-oozie-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="ff697-196">[Use Oozie with Hadoop to define and run a workflow on Linux-based Azure HDInsight](../hdinsight-use-oozie-linux-mac.md).</span></span>
* <span data-ttu-id="ff697-197">[Use time-based Oozie coordinator](../hdinsight-use-oozie-coordinator-time.md).</span><span class="sxs-lookup"><span data-stu-id="ff697-197">[Use time-based Oozie coordinator](../hdinsight-use-oozie-coordinator-time.md).</span></span>
* <span data-ttu-id="ff697-198">[Connect to HDInsight (Hadoop) using SSH](../hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span><span class="sxs-lookup"><span data-stu-id="ff697-198">[Connect to HDInsight (Hadoop) using SSH](../hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>
