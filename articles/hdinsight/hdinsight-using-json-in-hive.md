---
title: Analyze and Process JSON documents with Hive in HDInsight | Microsoft Docs
description: Learn how to use JSON documents and analyze them using Hive in HDInsight.
services: hdinsight
documentationcenter: ''
author: rashimg
manager: mwinkle
editor: cgronlun
ms.assetid: e17794e8-faae-4264-9434-67f61ea78f13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/22/2015
ms.author: rashimg
ms.openlocfilehash: 7b95133c83914c09faae893aca0c313520110a42
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540806"
---
# <a name="process-and-analyze-json-documents-using-hive-in-hdinsight"></a><span data-ttu-id="943b8-103">Process and analyze JSON documents using Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="943b8-103">Process and analyze JSON documents using Hive in HDInsight</span></span>
<span data-ttu-id="943b8-104">Learn how to process and analyze JSON files using Hive in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="943b8-104">Learn how to process and analyze JSON files using Hive in HDInsight.</span></span> <span data-ttu-id="943b8-105">The following JSON document will be used in the tutorial</span><span class="sxs-lookup"><span data-stu-id="943b8-105">The following JSON document will be used in the tutorial</span></span>

    {
        "StudentId": "trgfg-5454-fdfdg-4346",
        "Grade": 7,
        "StudentDetails": [
            {
                "FirstName": "Peggy",
                "LastName": "Williams",
                "YearJoined": 2012
            }
        ],
        "StudentClassCollection": [
            {
                "ClassId": "89084343",
                "ClassParticipation": "Satisfied",
                "ClassParticipationRank": "High",
                "Score": 93,
                "PerformedActivity": false
            },
            {
                "ClassId": "78547522",
                "ClassParticipation": "NotSatisfied",
                "ClassParticipationRank": "None",
                "Score": 74,
                "PerformedActivity": false
            },
            {
                "ClassId": "78675563",
                "ClassParticipation": "Satisfied",
                "ClassParticipationRank": "Low",
                "Score": 83,
                "PerformedActivity": true
            }
        ]
    }

<span data-ttu-id="943b8-106">The file can be found at wasbs://processjson@hditutorialdata.blob.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="943b8-106">The file can be found at wasbs://processjson@hditutorialdata.blob.core.windows.net/.</span></span> <span data-ttu-id="943b8-107">For more information on using Azure Blob storage with HDInsight, see [Use HDFS-compatible Azure Blob storage with Hadoop in HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="943b8-107">For more information on using Azure Blob storage with HDInsight, see [Use HDFS-compatible Azure Blob storage with Hadoop in HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="943b8-108">You can copy the file to the default container of your cluster if you want.</span><span class="sxs-lookup"><span data-stu-id="943b8-108">You can copy the file to the default container of your cluster if you want.</span></span>

<span data-ttu-id="943b8-109">In this tutorial, you will use the Hive console.</span><span class="sxs-lookup"><span data-stu-id="943b8-109">In this tutorial, you will use the Hive console.</span></span>  <span data-ttu-id="943b8-110">For instructions of opening the Hive console, see [Use Hive with Hadoop on HDInsight with Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="943b8-110">For instructions of opening the Hive console, see [Use Hive with Hadoop on HDInsight with Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md).</span></span>

## <a name="flatten-json-documents"></a><span data-ttu-id="943b8-111">Flatten JSON documents</span><span class="sxs-lookup"><span data-stu-id="943b8-111">Flatten JSON documents</span></span>
<span data-ttu-id="943b8-112">The methods listed in the next section require the JSON document in a single row.</span><span class="sxs-lookup"><span data-stu-id="943b8-112">The methods listed in the next section require the JSON document in a single row.</span></span> <span data-ttu-id="943b8-113">So you must flatten the JSON document to a string.</span><span class="sxs-lookup"><span data-stu-id="943b8-113">So you must flatten the JSON document to a string.</span></span> <span data-ttu-id="943b8-114">If your JSON document is already flattened, you can skip this step and go straight to the next section on Analyzing JSON data.</span><span class="sxs-lookup"><span data-stu-id="943b8-114">If your JSON document is already flattened, you can skip this step and go straight to the next section on Analyzing JSON data.</span></span>

    DROP TABLE IF EXISTS StudentsRaw;
    CREATE EXTERNAL TABLE StudentsRaw (textcol string) STORED AS TEXTFILE LOCATION "wasb://processjson@hditutorialdata.blob.core.windows.net/";

    DROP TABLE IF EXISTS StudentsOneLine;
    CREATE EXTERNAL TABLE StudentsOneLine
    (
      json_body string
    )
    STORED AS TEXTFILE LOCATION '/json/students';

    INSERT OVERWRITE TABLE StudentsOneLine
    SELECT CONCAT_WS(' ',COLLECT_LIST(textcol)) AS singlelineJSON
          FROM (SELECT INPUT__FILE__NAME,BLOCK__OFFSET__INSIDE__FILE, textcol FROM StudentsRaw DISTRIBUTE BY INPUT__FILE__NAME SORT BY BLOCK__OFFSET__INSIDE__FILE) x
          GROUP BY INPUT__FILE__NAME;

    SELECT * FROM StudentsOneLine

<span data-ttu-id="943b8-115">The raw JSON file is located at **wasbs://processjson@hditutorialdata.blob.core.windows.net/**.</span><span class="sxs-lookup"><span data-stu-id="943b8-115">The raw JSON file is located at **wasbs://processjson@hditutorialdata.blob.core.windows.net/**.</span></span> <span data-ttu-id="943b8-116">The *StudentsRaw* Hive table points to the raw un-flattened JSON document.</span><span class="sxs-lookup"><span data-stu-id="943b8-116">The *StudentsRaw* Hive table points to the raw un-flattened JSON document.</span></span>

<span data-ttu-id="943b8-117">The *StudentsOneLine* Hive table will store the data in the HDInsight default file system under the */json/students/* path.</span><span class="sxs-lookup"><span data-stu-id="943b8-117">The *StudentsOneLine* Hive table will store the data in the HDInsight default file system under the */json/students/* path.</span></span>

<span data-ttu-id="943b8-118">The INSERT statement populate the StudentOneLine table with the flattened JSON data.</span><span class="sxs-lookup"><span data-stu-id="943b8-118">The INSERT statement populate the StudentOneLine table with the flattened JSON data.</span></span>

<span data-ttu-id="943b8-119">The SELECT statement shall only return 1 row.</span><span class="sxs-lookup"><span data-stu-id="943b8-119">The SELECT statement shall only return 1 row.</span></span>

<span data-ttu-id="943b8-120">Here is the output of the SELECT statement:</span><span class="sxs-lookup"><span data-stu-id="943b8-120">Here is the output of the SELECT statement:</span></span>

![Flattening of the JSON document.][image-hdi-hivejson-flatten]

## <a name="analyze-json-documents-in-hive"></a><span data-ttu-id="943b8-122">Analyze JSON documents in Hive</span><span class="sxs-lookup"><span data-stu-id="943b8-122">Analyze JSON documents in Hive</span></span>
<span data-ttu-id="943b8-123">Hive provides three different mechanisms to run queries on JSON documents:</span><span class="sxs-lookup"><span data-stu-id="943b8-123">Hive provides three different mechanisms to run queries on JSON documents:</span></span>

* <span data-ttu-id="943b8-124">use the GET\_JSON\_OBJECT UDF (User Defined Function)</span><span class="sxs-lookup"><span data-stu-id="943b8-124">use the GET\_JSON\_OBJECT UDF (User Defined Function)</span></span>
* <span data-ttu-id="943b8-125">use the JSON_TUPLE UDF</span><span class="sxs-lookup"><span data-stu-id="943b8-125">use the JSON_TUPLE UDF</span></span>
* <span data-ttu-id="943b8-126">use custom SerDe</span><span class="sxs-lookup"><span data-stu-id="943b8-126">use custom SerDe</span></span>
* <span data-ttu-id="943b8-127">write you own UDF using Python or other languages.</span><span class="sxs-lookup"><span data-stu-id="943b8-127">write you own UDF using Python or other languages.</span></span> <span data-ttu-id="943b8-128">See [this article][hdinsight-python] on running your own Python code with Hive.</span><span class="sxs-lookup"><span data-stu-id="943b8-128">See [this article][hdinsight-python] on running your own Python code with Hive.</span></span>

### <a name="use-the-getjsonobject-udf"></a><span data-ttu-id="943b8-129">Use the GET\_JSON_OBJECT UDF</span><span class="sxs-lookup"><span data-stu-id="943b8-129">Use the GET\_JSON_OBJECT UDF</span></span>
<span data-ttu-id="943b8-130">Hive provides a built-in UDF called [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object) which can perform JSON querying during run time.</span><span class="sxs-lookup"><span data-stu-id="943b8-130">Hive provides a built-in UDF called [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object) which can perform JSON querying during run time.</span></span> <span data-ttu-id="943b8-131">This method takes two arguments – the table name and method name which has the flattened JSON document and the JSON field that needs to be parsed.</span><span class="sxs-lookup"><span data-stu-id="943b8-131">This method takes two arguments – the table name and method name which has the flattened JSON document and the JSON field that needs to be parsed.</span></span> <span data-ttu-id="943b8-132">Let’s look at an example to see how this UDF works.</span><span class="sxs-lookup"><span data-stu-id="943b8-132">Let’s look at an example to see how this UDF works.</span></span>

<span data-ttu-id="943b8-133">Get the first name and last name for each student</span><span class="sxs-lookup"><span data-stu-id="943b8-133">Get the first name and last name for each student</span></span>

    SELECT
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.FirstName'),
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.LastName')
    FROM StudentsOneLine;

<span data-ttu-id="943b8-134">Here is the output when running this query in console window.</span><span class="sxs-lookup"><span data-stu-id="943b8-134">Here is the output when running this query in console window.</span></span>

![get_json_object UDF][image-hdi-hivejson-getjsonobject]

<span data-ttu-id="943b8-136">There are a few limitations of the get-json_object UDF.</span><span class="sxs-lookup"><span data-stu-id="943b8-136">There are a few limitations of the get-json_object UDF.</span></span>

* <span data-ttu-id="943b8-137">Because each field in the query requires re-parsing the query, it affects the performance.</span><span class="sxs-lookup"><span data-stu-id="943b8-137">Because each field in the query requires re-parsing the query, it affects the performance.</span></span>
* <span data-ttu-id="943b8-138">GET\_JSON_OBJECT() returns the string representation of an array.</span><span class="sxs-lookup"><span data-stu-id="943b8-138">GET\_JSON_OBJECT() returns the string representation of an array.</span></span> <span data-ttu-id="943b8-139">To convert this to a Hive array, you will have to use regular expressions to replace the square brackets ‘[‘ and ‘]’ and then also call split to get the array.</span><span class="sxs-lookup"><span data-stu-id="943b8-139">To convert this to a Hive array, you will have to use regular expressions to replace the square brackets ‘[‘ and ‘]’ and then also call split to get the array.</span></span>

<span data-ttu-id="943b8-140">This is why the Hive wiki recommends using json_tuple.</span><span class="sxs-lookup"><span data-stu-id="943b8-140">This is why the Hive wiki recommends using json_tuple.</span></span>  

### <a name="use-the-jsontuple-udf"></a><span data-ttu-id="943b8-141">Use the JSON_TUPLE UDF</span><span class="sxs-lookup"><span data-stu-id="943b8-141">Use the JSON_TUPLE UDF</span></span>
<span data-ttu-id="943b8-142">Another UDF provided by Hive is called [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple) which performs better than [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object).</span><span class="sxs-lookup"><span data-stu-id="943b8-142">Another UDF provided by Hive is called [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple) which performs better than [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object).</span></span> <span data-ttu-id="943b8-143">This method takes a set of keys and a JSON string, and returns a tuple of values using one function.</span><span class="sxs-lookup"><span data-stu-id="943b8-143">This method takes a set of keys and a JSON string, and returns a tuple of values using one function.</span></span> <span data-ttu-id="943b8-144">The following query returns the student id and the grade from the JSON document:</span><span class="sxs-lookup"><span data-stu-id="943b8-144">The following query returns the student id and the grade from the JSON document:</span></span>

    SELECT q1.StudentId, q1.Grade
      FROM StudentsOneLine jt
      LATERAL VIEW JSON_TUPLE(jt.json_body, 'StudentId', 'Grade') q1
        AS StudentId, Grade;

<span data-ttu-id="943b8-145">The output of this script in the Hive console:</span><span class="sxs-lookup"><span data-stu-id="943b8-145">The output of this script in the Hive console:</span></span>

![json_tuple UDF][image-hdi-hivejson-jsontuple]

<span data-ttu-id="943b8-147">JSON\_TUPLE uses the [lateral view](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) syntax in Hive which allows json\_tuple to create a virtual table by applying the UDT function to each row of the original table.</span><span class="sxs-lookup"><span data-stu-id="943b8-147">JSON\_TUPLE uses the [lateral view](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) syntax in Hive which allows json\_tuple to create a virtual table by applying the UDT function to each row of the original table.</span></span>  <span data-ttu-id="943b8-148">Complex JSONs become too unwieldy because of the repeated use of LATERAL VIEW.</span><span class="sxs-lookup"><span data-stu-id="943b8-148">Complex JSONs become too unwieldy because of the repeated use of LATERAL VIEW.</span></span> <span data-ttu-id="943b8-149">Furthermore, JSON_TUPLE cannot handle nested JSONs.</span><span class="sxs-lookup"><span data-stu-id="943b8-149">Furthermore, JSON_TUPLE cannot handle nested JSONs.</span></span>

### <a name="use-custom-serde"></a><span data-ttu-id="943b8-150">Use custom SerDe</span><span class="sxs-lookup"><span data-stu-id="943b8-150">Use custom SerDe</span></span>
<span data-ttu-id="943b8-151">SerDe is the best choice for parsing nested JSON documents, it allows you to define the JSON schema, and use the schema to parse the documents.</span><span class="sxs-lookup"><span data-stu-id="943b8-151">SerDe is the best choice for parsing nested JSON documents, it allows you to define the JSON schema, and use the schema to parse the documents.</span></span> <span data-ttu-id="943b8-152">In this tutorial, you will use one of the more popular SerDe that has been developed by [rcongiu](https://github.com/rcongiu).</span><span class="sxs-lookup"><span data-stu-id="943b8-152">In this tutorial, you will use one of the more popular SerDe that has been developed by [rcongiu](https://github.com/rcongiu).</span></span>

<span data-ttu-id="943b8-153">**To use the custom SerDe:**</span><span class="sxs-lookup"><span data-stu-id="943b8-153">**To use the custom SerDe:**</span></span>

1. <span data-ttu-id="943b8-154">Install [Java SE Development Kit 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR).</span><span class="sxs-lookup"><span data-stu-id="943b8-154">Install [Java SE Development Kit 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR).</span></span> <span data-ttu-id="943b8-155">Choose the Windows X64 version of the JDK if you are going to be using the Windows deployment of HDInsight</span><span class="sxs-lookup"><span data-stu-id="943b8-155">Choose the Windows X64 version of the JDK if you are going to be using the Windows deployment of HDInsight</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="943b8-156">JDK 1.8 doesn't work with this SerDe.</span><span class="sxs-lookup"><span data-stu-id="943b8-156">JDK 1.8 doesn't work with this SerDe.</span></span>
   > 
   > 
   
    <span data-ttu-id="943b8-157">After the installation is completed, add a new user environment variable:</span><span class="sxs-lookup"><span data-stu-id="943b8-157">After the installation is completed, add a new user environment variable:</span></span>
   
   1. <span data-ttu-id="943b8-158">Open **View advanced system settings** from the Windows screen.</span><span class="sxs-lookup"><span data-stu-id="943b8-158">Open **View advanced system settings** from the Windows screen.</span></span>
   2. <span data-ttu-id="943b8-159">Click **Environment Variables**.</span><span class="sxs-lookup"><span data-stu-id="943b8-159">Click **Environment Variables**.</span></span>  
   3. <span data-ttu-id="943b8-160">Add a new **JAVA_HOME** environment variable is pointing to **C:\Program Files\Java\jdk1.7.0_55** or wherever your JDK is installed.</span><span class="sxs-lookup"><span data-stu-id="943b8-160">Add a new **JAVA_HOME** environment variable is pointing to **C:\Program Files\Java\jdk1.7.0_55** or wherever your JDK is installed.</span></span>
      
      ![Setting up correct config values for JDK][image-hdi-hivejson-jdk]
2. <span data-ttu-id="943b8-162">Install [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span><span class="sxs-lookup"><span data-stu-id="943b8-162">Install [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span></span>
   
    <span data-ttu-id="943b8-163">Add the bin folder to your path by going to Control Panel-->Edit the System Variables for your account Environment variables.</span><span class="sxs-lookup"><span data-stu-id="943b8-163">Add the bin folder to your path by going to Control Panel-->Edit the System Variables for your account Environment variables.</span></span> <span data-ttu-id="943b8-164">The screenshot below shows you how to do this.</span><span class="sxs-lookup"><span data-stu-id="943b8-164">The screenshot below shows you how to do this.</span></span>
   
    ![Setting up Maven][image-hdi-hivejson-maven]
3. <span data-ttu-id="943b8-166">Clone the project from [Hive-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) github site.</span><span class="sxs-lookup"><span data-stu-id="943b8-166">Clone the project from [Hive-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) github site.</span></span> <span data-ttu-id="943b8-167">You can do this by clicking on the “Download Zip” button as shown in the screenshot below.</span><span class="sxs-lookup"><span data-stu-id="943b8-167">You can do this by clicking on the “Download Zip” button as shown in the screenshot below.</span></span>
   
    ![Cloning the project][image-hdi-hivejson-serde]

<span data-ttu-id="943b8-169">4: Go to the folder where you have downloaded this package and  type “mvn package”.</span><span class="sxs-lookup"><span data-stu-id="943b8-169">4: Go to the folder where you have downloaded this package and  type “mvn package”.</span></span> <span data-ttu-id="943b8-170">This should create the necessary jar files that you can then copy over to the cluster.</span><span class="sxs-lookup"><span data-stu-id="943b8-170">This should create the necessary jar files that you can then copy over to the cluster.</span></span>

<span data-ttu-id="943b8-171">5: Go to the target folder under the root folder where you downloaded the package.</span><span class="sxs-lookup"><span data-stu-id="943b8-171">5: Go to the target folder under the root folder where you downloaded the package.</span></span> <span data-ttu-id="943b8-172">Upload the json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar file to head-node of your cluster.</span><span class="sxs-lookup"><span data-stu-id="943b8-172">Upload the json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar file to head-node of your cluster.</span></span> <span data-ttu-id="943b8-173">I usually put it under the hive binary folder: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin or something similar.</span><span class="sxs-lookup"><span data-stu-id="943b8-173">I usually put it under the hive binary folder: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin or something similar.</span></span>

<span data-ttu-id="943b8-174">6: In the hive prompt, type “add jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar”.</span><span class="sxs-lookup"><span data-stu-id="943b8-174">6: In the hive prompt, type “add jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar”.</span></span> <span data-ttu-id="943b8-175">Since in my case, the jar is in the C:\apps\dist\hive-0.13.x\bin folder, I can directly add the jar with the name as shown below:</span><span class="sxs-lookup"><span data-stu-id="943b8-175">Since in my case, the jar is in the C:\apps\dist\hive-0.13.x\bin folder, I can directly add the jar with the name as shown below:</span></span>

    add jar json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar;

   ![Adding JAR to your project][image-hdi-hivejson-addjar]

<span data-ttu-id="943b8-177">Now, you are ready to use the SerDe to run queries against the JSON document.</span><span class="sxs-lookup"><span data-stu-id="943b8-177">Now, you are ready to use the SerDe to run queries against the JSON document.</span></span>

<span data-ttu-id="943b8-178">The following statement create a table with a defined schema</span><span class="sxs-lookup"><span data-stu-id="943b8-178">The following statement create a table with a defined schema</span></span>

    DROP TABLE json_table;
    CREATE EXTERNAL TABLE json_table (
      StudentId string,
      Grade int,
      StudentDetails array<struct<
          FirstName:string,
          LastName:string,
          YearJoined:int
          >
      >,
      StudentClassCollection array<struct<
          ClassId:string,
          ClassParticipation:string,
          ClassParticipationRank:string,
          Score:int,
          PerformedActivity:boolean
          >
      >
    ) ROW FORMAT SERDE 'org.openx.data.jsonserde.JsonSerDe'
    LOCATION '/json/students';

<span data-ttu-id="943b8-179">To list the first name and last name of the student</span><span class="sxs-lookup"><span data-stu-id="943b8-179">To list the first name and last name of the student</span></span>

    SELECT StudentDetails.FirstName, StudentDetails.LastName FROM json_table;

<span data-ttu-id="943b8-180">Here is the result from the Hive console.</span><span class="sxs-lookup"><span data-stu-id="943b8-180">Here is the result from the Hive console.</span></span>

![SerDe Query 1][image-hdi-hivejson-serde_query1]

<span data-ttu-id="943b8-182">To calculate the sum of scores of the JSON document</span><span class="sxs-lookup"><span data-stu-id="943b8-182">To calculate the sum of scores of the JSON document</span></span>

    SELECT SUM(scores)
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as scores;

<span data-ttu-id="943b8-183">The query above uses [lateral view explode](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) UDF to expand the array of scores so that they can be summed.</span><span class="sxs-lookup"><span data-stu-id="943b8-183">The query above uses [lateral view explode](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) UDF to expand the array of scores so that they can be summed.</span></span>

<span data-ttu-id="943b8-184">Here is the output from the Hive console.</span><span class="sxs-lookup"><span data-stu-id="943b8-184">Here is the output from the Hive console.</span></span>

![SerDe Query 2][image-hdi-hivejson-serde_query2]

<span data-ttu-id="943b8-186">To find which subjects a given student has scored more than 80 points SELECT</span><span class="sxs-lookup"><span data-stu-id="943b8-186">To find which subjects a given student has scored more than 80 points SELECT</span></span>  
      <span data-ttu-id="943b8-187">jt.StudentClassCollection.ClassId FROM json_table jt lateral view explode(jt.StudentClassCollection.Score) collection as score  where score > 80;</span><span class="sxs-lookup"><span data-stu-id="943b8-187">jt.StudentClassCollection.ClassId FROM json_table jt lateral view explode(jt.StudentClassCollection.Score) collection as score  where score > 80;</span></span>

<span data-ttu-id="943b8-188">The query above returns a Hive array unlike get\_json\_object which returns a string.</span><span class="sxs-lookup"><span data-stu-id="943b8-188">The query above returns a Hive array unlike get\_json\_object which returns a string.</span></span>

![SerDe Query 3][image-hdi-hivejson-serde_query3]

<span data-ttu-id="943b8-190">If you want to skil malformed JSON, then as explained in the [wiki page](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) of this SerDe you can achieve that by typing the code below:</span><span class="sxs-lookup"><span data-stu-id="943b8-190">If you want to skil malformed JSON, then as explained in the [wiki page](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) of this SerDe you can achieve that by typing the code below:</span></span>  

    ALTER TABLE json_table SET SERDEPROPERTIES ( "ignore.malformed.json" = "true");




## <a name="summary"></a><span data-ttu-id="943b8-191">Summary</span><span class="sxs-lookup"><span data-stu-id="943b8-191">Summary</span></span>
<span data-ttu-id="943b8-192">In conclusion, the type of JSON operator in Hive that you choose depends on your scenario.</span><span class="sxs-lookup"><span data-stu-id="943b8-192">In conclusion, the type of JSON operator in Hive that you choose depends on your scenario.</span></span> <span data-ttu-id="943b8-193">If you have a simple JSON document and you only have one field to look up on – you can choose to use the Hive UDF get\_json\_object.</span><span class="sxs-lookup"><span data-stu-id="943b8-193">If you have a simple JSON document and you only have one field to look up on – you can choose to use the Hive UDF get\_json\_object.</span></span> <span data-ttu-id="943b8-194">If you have more than one keys to look up on then you can use json_tuple.</span><span class="sxs-lookup"><span data-stu-id="943b8-194">If you have more than one keys to look up on then you can use json_tuple.</span></span> <span data-ttu-id="943b8-195">If you have a nested document, then you should use the JSON SerDe.</span><span class="sxs-lookup"><span data-stu-id="943b8-195">If you have a nested document, then you should use the JSON SerDe.</span></span>

<span data-ttu-id="943b8-196">For other related articles, see</span><span class="sxs-lookup"><span data-stu-id="943b8-196">For other related articles, see</span></span>

* [<span data-ttu-id="943b8-197">Use Hive and HiveQL with Hadoop in HDInsight to analyze a sample Apache log4j file</span><span class="sxs-lookup"><span data-stu-id="943b8-197">Use Hive and HiveQL with Hadoop in HDInsight to analyze a sample Apache log4j file</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="943b8-198">Analyze flight delay data by using Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="943b8-198">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="943b8-199">Analyze Twitter data using Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="943b8-199">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="943b8-200">Run a Hadoop job using DocumentDB and HDInsight</span><span class="sxs-lookup"><span data-stu-id="943b8-200">Run a Hadoop job using DocumentDB and HDInsight</span></span>](../documentdb/documentdb-run-hadoop-with-hdinsight.md)

[hdinsight-python]: hdinsight-python.md

[image-hdi-hivejson-flatten]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-using-json-in-hive/flatten.png
[image-hdi-hivejson-getjsonobject]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-using-json-in-hive/getjsonobject.png
[image-hdi-hivejson-jsontuple]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-using-json-in-hive/jsontuple.png
[image-hdi-hivejson-jdk]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-using-json-in-hive/jdk.png
[image-hdi-hivejson-maven]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-using-json-in-hive/maven.png
[image-hdi-hivejson-serde]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-using-json-in-hive/serde.png
[image-hdi-hivejson-addjar]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-using-json-in-hive/addjar.png
[image-hdi-hivejson-serde_query1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-using-json-in-hive/serde_query1.png
[image-hdi-hivejson-serde_query2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-using-json-in-hive/serde_query2.png
[image-hdi-hivejson-serde_query3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-using-json-in-hive/serde_query3.png
[image-hdi-hivejson-serde_result]: ./media/hdinsight-using-json-in-hive/serde_result.png










