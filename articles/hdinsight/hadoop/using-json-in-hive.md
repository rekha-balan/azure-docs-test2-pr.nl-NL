---
title: Analyze and process JSON documents with Apache Hive in Azure HDInsight
description: Learn how to use JSON documents and analyze them by using apache Hive in Azure HDInsight
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 05/16/2018
ms.author: jasonh
ms.openlocfilehash: 5388d0d6c05cdfd60f3f840761a2cf87d4b6a41e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965449"
---
# <a name="process-and-analyze-json-documents-by-using-apache-hive-in-azure-hdinsight"></a><span data-ttu-id="4f34e-103">Process and analyze JSON documents by using Apache Hive in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="4f34e-103">Process and analyze JSON documents by using Apache Hive in Azure HDInsight</span></span>

<span data-ttu-id="4f34e-104">Learn how to process and analyze JavaScript Object Notation (JSON) files by using Apache Hive in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4f34e-104">Learn how to process and analyze JavaScript Object Notation (JSON) files by using Apache Hive in Azure HDInsight.</span></span> <span data-ttu-id="4f34e-105">This tutorial uses the following JSON document:</span><span class="sxs-lookup"><span data-stu-id="4f34e-105">This tutorial uses the following JSON document:</span></span>

```json
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
```

<span data-ttu-id="4f34e-106">The file can be found at **wasb://processjson@hditutorialdata.blob.core.windows.net/**.</span><span class="sxs-lookup"><span data-stu-id="4f34e-106">The file can be found at **wasb://processjson@hditutorialdata.blob.core.windows.net/**.</span></span> <span data-ttu-id="4f34e-107">For more information on how to use Azure Blob storage with HDInsight, see [Use HDFS-compatible Azure Blob storage with Hadoop in HDInsight](../hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="4f34e-107">For more information on how to use Azure Blob storage with HDInsight, see [Use HDFS-compatible Azure Blob storage with Hadoop in HDInsight](../hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="4f34e-108">You can copy the file to the default container of your cluster.</span><span class="sxs-lookup"><span data-stu-id="4f34e-108">You can copy the file to the default container of your cluster.</span></span>

<span data-ttu-id="4f34e-109">In this tutorial, you use the Hive console.</span><span class="sxs-lookup"><span data-stu-id="4f34e-109">In this tutorial, you use the Hive console.</span></span> <span data-ttu-id="4f34e-110">For instructions on how to open the Hive console, see [Use Hive with Hadoop on HDInsight with Remote Desktop](apache-hadoop-use-hive-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="4f34e-110">For instructions on how to open the Hive console, see [Use Hive with Hadoop on HDInsight with Remote Desktop](apache-hadoop-use-hive-remote-desktop.md).</span></span>

## <a name="flatten-json-documents"></a><span data-ttu-id="4f34e-111">Flatten JSON documents</span><span class="sxs-lookup"><span data-stu-id="4f34e-111">Flatten JSON documents</span></span>
<span data-ttu-id="4f34e-112">The methods listed in the next section require that the JSON document be composed of a single row.</span><span class="sxs-lookup"><span data-stu-id="4f34e-112">The methods listed in the next section require that the JSON document be composed of a single row.</span></span> <span data-ttu-id="4f34e-113">So, you must flatten the JSON document to a string.</span><span class="sxs-lookup"><span data-stu-id="4f34e-113">So, you must flatten the JSON document to a string.</span></span> <span data-ttu-id="4f34e-114">If your JSON document is already flattened, you can skip this step and go straight to the next section on analyzing JSON data.</span><span class="sxs-lookup"><span data-stu-id="4f34e-114">If your JSON document is already flattened, you can skip this step and go straight to the next section on analyzing JSON data.</span></span> <span data-ttu-id="4f34e-115">To flatten the JSON document, run the following script:</span><span class="sxs-lookup"><span data-stu-id="4f34e-115">To flatten the JSON document, run the following script:</span></span>

```sql
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
```

<span data-ttu-id="4f34e-116">The raw JSON file is located at **wasb://processjson@hditutorialdata.blob.core.windows.net/**.</span><span class="sxs-lookup"><span data-stu-id="4f34e-116">The raw JSON file is located at **wasb://processjson@hditutorialdata.blob.core.windows.net/**.</span></span> <span data-ttu-id="4f34e-117">The **StudentsRaw** Hive table points to the raw JSON document that is not flattened.</span><span class="sxs-lookup"><span data-stu-id="4f34e-117">The **StudentsRaw** Hive table points to the raw JSON document that is not flattened.</span></span>

<span data-ttu-id="4f34e-118">The **StudentsOneLine** Hive table stores the data in the HDInsight default file system under the **/json/students/** path.</span><span class="sxs-lookup"><span data-stu-id="4f34e-118">The **StudentsOneLine** Hive table stores the data in the HDInsight default file system under the **/json/students/** path.</span></span>

<span data-ttu-id="4f34e-119">The **INSERT** statement populates the **StudentOneLine** table with the flattened JSON data.</span><span class="sxs-lookup"><span data-stu-id="4f34e-119">The **INSERT** statement populates the **StudentOneLine** table with the flattened JSON data.</span></span>

<span data-ttu-id="4f34e-120">The **SELECT** statement only returns one row.</span><span class="sxs-lookup"><span data-stu-id="4f34e-120">The **SELECT** statement only returns one row.</span></span>

<span data-ttu-id="4f34e-121">Here is the output of the **SELECT** statement:</span><span class="sxs-lookup"><span data-stu-id="4f34e-121">Here is the output of the **SELECT** statement:</span></span>

![Flattening the JSON document][image-hdi-hivejson-flatten]

## <a name="analyze-json-documents-in-hive"></a><span data-ttu-id="4f34e-123">Analyze JSON documents in Hive</span><span class="sxs-lookup"><span data-stu-id="4f34e-123">Analyze JSON documents in Hive</span></span>
<span data-ttu-id="4f34e-124">Hive provides three different mechanisms to run queries on JSON documents, or you can write your own:</span><span class="sxs-lookup"><span data-stu-id="4f34e-124">Hive provides three different mechanisms to run queries on JSON documents, or you can write your own:</span></span>

* <span data-ttu-id="4f34e-125">Use the get_json_object user-defined function (UDF).</span><span class="sxs-lookup"><span data-stu-id="4f34e-125">Use the get_json_object user-defined function (UDF).</span></span>
* <span data-ttu-id="4f34e-126">Use the json_tuple UDF.</span><span class="sxs-lookup"><span data-stu-id="4f34e-126">Use the json_tuple UDF.</span></span>
* <span data-ttu-id="4f34e-127">Use the custom Serializer/Deserializer (SerDe).</span><span class="sxs-lookup"><span data-stu-id="4f34e-127">Use the custom Serializer/Deserializer (SerDe).</span></span>
* <span data-ttu-id="4f34e-128">Write your own UDF by using Python or other languages.</span><span class="sxs-lookup"><span data-stu-id="4f34e-128">Write your own UDF by using Python or other languages.</span></span> <span data-ttu-id="4f34e-129">For more information on how to run your own Python code with Hive, see [Python UDF with Apache Hive and Pig][hdinsight-python].</span><span class="sxs-lookup"><span data-stu-id="4f34e-129">For more information on how to run your own Python code with Hive, see [Python UDF with Apache Hive and Pig][hdinsight-python].</span></span>

### <a name="use-the-getjsonobject-udf"></a><span data-ttu-id="4f34e-130">Use the get_json_object UDF</span><span class="sxs-lookup"><span data-stu-id="4f34e-130">Use the get_json_object UDF</span></span>
<span data-ttu-id="4f34e-131">Hive provides a built-in UDF called [get_json_object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object) that can perform JSON querying during runtime.</span><span class="sxs-lookup"><span data-stu-id="4f34e-131">Hive provides a built-in UDF called [get_json_object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object) that can perform JSON querying during runtime.</span></span> <span data-ttu-id="4f34e-132">This method takes two arguments--the table name and method name, which has the flattened JSON document and the JSON field that needs to be parsed.</span><span class="sxs-lookup"><span data-stu-id="4f34e-132">This method takes two arguments--the table name and method name, which has the flattened JSON document and the JSON field that needs to be parsed.</span></span> <span data-ttu-id="4f34e-133">Let’s look at an example to see how this UDF works.</span><span class="sxs-lookup"><span data-stu-id="4f34e-133">Let’s look at an example to see how this UDF works.</span></span>

<span data-ttu-id="4f34e-134">The following query returns the first name and last name for each student:</span><span class="sxs-lookup"><span data-stu-id="4f34e-134">The following query returns the first name and last name for each student:</span></span>

```sql
SELECT
  GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.FirstName'),
  GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.LastName')
FROM StudentsOneLine;
```

<span data-ttu-id="4f34e-135">Here is the output when you run this query in the console window:</span><span class="sxs-lookup"><span data-stu-id="4f34e-135">Here is the output when you run this query in the console window:</span></span>

![get_json_object UDF][image-hdi-hivejson-getjsonobject]

<span data-ttu-id="4f34e-137">There are limitations of the get_json_object UDF:</span><span class="sxs-lookup"><span data-stu-id="4f34e-137">There are limitations of the get_json_object UDF:</span></span>

* <span data-ttu-id="4f34e-138">Because each field in the query requires reparsing of the query, it affects the performance.</span><span class="sxs-lookup"><span data-stu-id="4f34e-138">Because each field in the query requires reparsing of the query, it affects the performance.</span></span>
* <span data-ttu-id="4f34e-139">**GET\_JSON_OBJECT()** returns the string representation of an array.</span><span class="sxs-lookup"><span data-stu-id="4f34e-139">**GET\_JSON_OBJECT()** returns the string representation of an array.</span></span> <span data-ttu-id="4f34e-140">To convert this array to a Hive array, you have to use regular expressions to replace the square brackets "[" and "]", and then you also have to call split to get the array.</span><span class="sxs-lookup"><span data-stu-id="4f34e-140">To convert this array to a Hive array, you have to use regular expressions to replace the square brackets "[" and "]", and then you also have to call split to get the array.</span></span>

<span data-ttu-id="4f34e-141">This is why the Hive wiki recommends that you use json_tuple.</span><span class="sxs-lookup"><span data-stu-id="4f34e-141">This is why the Hive wiki recommends that you use json_tuple.</span></span>  

### <a name="use-the-jsontuple-udf"></a><span data-ttu-id="4f34e-142">Use the json_tuple UDF</span><span class="sxs-lookup"><span data-stu-id="4f34e-142">Use the json_tuple UDF</span></span>
<span data-ttu-id="4f34e-143">Another UDF provided by Hive is called [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), which performs better than [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object).</span><span class="sxs-lookup"><span data-stu-id="4f34e-143">Another UDF provided by Hive is called [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), which performs better than [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object).</span></span> <span data-ttu-id="4f34e-144">This method takes a set of keys and a JSON string, and returns a tuple of values by using one function.</span><span class="sxs-lookup"><span data-stu-id="4f34e-144">This method takes a set of keys and a JSON string, and returns a tuple of values by using one function.</span></span> <span data-ttu-id="4f34e-145">The following query returns the student ID and the grade from the JSON document:</span><span class="sxs-lookup"><span data-stu-id="4f34e-145">The following query returns the student ID and the grade from the JSON document:</span></span>

```sql
SELECT q1.StudentId, q1.Grade
FROM StudentsOneLine jt
LATERAL VIEW JSON_TUPLE(jt.json_body, 'StudentId', 'Grade') q1
  AS StudentId, Grade;
```

<span data-ttu-id="4f34e-146">The output of this script in the Hive console:</span><span class="sxs-lookup"><span data-stu-id="4f34e-146">The output of this script in the Hive console:</span></span>

![json_tuple UDF][image-hdi-hivejson-jsontuple]

<span data-ttu-id="4f34e-148">The json_tuple UDF uses the [lateral view](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) syntax in Hive, which enables json\_tuple to create a virtual table by applying the UDT function to each row of the original table.</span><span class="sxs-lookup"><span data-stu-id="4f34e-148">The json_tuple UDF uses the [lateral view](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) syntax in Hive, which enables json\_tuple to create a virtual table by applying the UDT function to each row of the original table.</span></span> <span data-ttu-id="4f34e-149">Complex JSONs become too unwieldy because of the repeated use of **LATERAL VIEW**.</span><span class="sxs-lookup"><span data-stu-id="4f34e-149">Complex JSONs become too unwieldy because of the repeated use of **LATERAL VIEW**.</span></span> <span data-ttu-id="4f34e-150">Furthermore, **JSON_TUPLE** cannot handle nested JSONs.</span><span class="sxs-lookup"><span data-stu-id="4f34e-150">Furthermore, **JSON_TUPLE** cannot handle nested JSONs.</span></span>

### <a name="use-a-custom-serde"></a><span data-ttu-id="4f34e-151">Use a custom SerDe</span><span class="sxs-lookup"><span data-stu-id="4f34e-151">Use a custom SerDe</span></span>
<span data-ttu-id="4f34e-152">SerDe is the best choice for parsing nested JSON documents.</span><span class="sxs-lookup"><span data-stu-id="4f34e-152">SerDe is the best choice for parsing nested JSON documents.</span></span> <span data-ttu-id="4f34e-153">It lets you define the JSON schema, and then you can use the schema to parse the documents.</span><span class="sxs-lookup"><span data-stu-id="4f34e-153">It lets you define the JSON schema, and then you can use the schema to parse the documents.</span></span> <span data-ttu-id="4f34e-154">For instructions, see [How to use a custom JSON SerDe with Microsoft Azure HDInsight](https://blogs.msdn.microsoft.com/bigdatasupport/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="4f34e-154">For instructions, see [How to use a custom JSON SerDe with Microsoft Azure HDInsight](https://blogs.msdn.microsoft.com/bigdatasupport/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight/).</span></span>

## <a name="summary"></a><span data-ttu-id="4f34e-155">Summary</span><span class="sxs-lookup"><span data-stu-id="4f34e-155">Summary</span></span>
<span data-ttu-id="4f34e-156">In conclusion, the type of JSON operator in Hive that you choose depends on your scenario.</span><span class="sxs-lookup"><span data-stu-id="4f34e-156">In conclusion, the type of JSON operator in Hive that you choose depends on your scenario.</span></span> <span data-ttu-id="4f34e-157">If you have a simple JSON document and you have only one field to look up on, you can choose to use the Hive UDF get_json_object.</span><span class="sxs-lookup"><span data-stu-id="4f34e-157">If you have a simple JSON document and you have only one field to look up on, you can choose to use the Hive UDF get_json_object.</span></span> <span data-ttu-id="4f34e-158">If you have more than one key to look up on, then you can use json_tuple.</span><span class="sxs-lookup"><span data-stu-id="4f34e-158">If you have more than one key to look up on, then you can use json_tuple.</span></span> <span data-ttu-id="4f34e-159">If you have a nested document, then you should use the JSON SerDe.</span><span class="sxs-lookup"><span data-stu-id="4f34e-159">If you have a nested document, then you should use the JSON SerDe.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f34e-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="4f34e-160">Next steps</span></span>

<span data-ttu-id="4f34e-161">For related articles, see:</span><span class="sxs-lookup"><span data-stu-id="4f34e-161">For related articles, see:</span></span>

* [<span data-ttu-id="4f34e-162">Use Hive and HiveQL with Hadoop in HDInsight to analyze a sample Apache log4j file</span><span class="sxs-lookup"><span data-stu-id="4f34e-162">Use Hive and HiveQL with Hadoop in HDInsight to analyze a sample Apache log4j file</span></span>](../hdinsight-use-hive.md)
* [<span data-ttu-id="4f34e-163">Analyze flight delay data by using Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="4f34e-163">Analyze flight delay data by using Hive in HDInsight</span></span>](../hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="4f34e-164">Analyze Twitter data by using Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="4f34e-164">Analyze Twitter data by using Hive in HDInsight</span></span>](../hdinsight-analyze-twitter-data.md)

[hdinsight-python]:python-udf-hdinsight.md

[image-hdi-hivejson-flatten]: ./media/using-json-in-hive/flatten.png
[image-hdi-hivejson-getjsonobject]: ./media/using-json-in-hive/getjsonobject.png
[image-hdi-hivejson-jsontuple]: ./media/using-json-in-hive/jsontuple.png
[image-hdi-hivejson-jdk]: ./media/hdinsight-using-json-in-hive/jdk.png
[image-hdi-hivejson-maven]: ./media/hdinsight-using-json-in-hive/maven.png
[image-hdi-hivejson-serde]: ./media/hdinsight-using-json-in-hive/serde.png
[image-hdi-hivejson-addjar]: ./media/hdinsight-using-json-in-hive/addjar.png
[image-hdi-hivejson-serde_query1]: ./media/hdinsight-using-json-in-hive/serde_query1.png
[image-hdi-hivejson-serde_query2]: ./media/hdinsight-using-json-in-hive/serde_query2.png
[image-hdi-hivejson-serde_query3]: ./media/hdinsight-using-json-in-hive/serde_query3.png
[image-hdi-hivejson-serde_result]: ./media/hdinsight-using-json-in-hive/serde_result.png

