---
title: Transform data with Databricks Notebook - Azure | Microsoft Docs
description: Learn how to process or transform data by running a Databricks notebook.
services: data-factory
documentationcenter: ''
author: douglaslMS
manager: craigg
ms.assetid: ''
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 03/15/2018
ms.author: douglasl
ms.openlocfilehash: 5f21f33678b8cf09d9dbd8966d42b1a5ebac9ffb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866361"
---
# <a name="transform-data-by-running-a-databricks-notebook"></a><span data-ttu-id="33432-103">Transform data by running a Databricks notebook</span><span class="sxs-lookup"><span data-stu-id="33432-103">Transform data by running a Databricks notebook</span></span>

<span data-ttu-id="33432-104">The Azure Databricks Notebook Activity in a [Data Factory pipeline](concepts-pipelines-activities.md) runs a Databricks notebook in your Azure Databricks workspace.</span><span class="sxs-lookup"><span data-stu-id="33432-104">The Azure Databricks Notebook Activity in a [Data Factory pipeline](concepts-pipelines-activities.md) runs a Databricks notebook in your Azure Databricks workspace.</span></span> <span data-ttu-id="33432-105">This article builds on the [data transformation activities](transform-data.md) article, which presents a general overview of data transformation and the supported transformation activities.</span><span class="sxs-lookup"><span data-stu-id="33432-105">This article builds on the [data transformation activities](transform-data.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span> <span data-ttu-id="33432-106">Azure Databricks is a managed platform for running Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="33432-106">Azure Databricks is a managed platform for running Apache Spark.</span></span>

## <a name="databricks-notebook-activity-definition"></a><span data-ttu-id="33432-107">Databricks Notebook activity definition</span><span class="sxs-lookup"><span data-stu-id="33432-107">Databricks Notebook activity definition</span></span>

<span data-ttu-id="33432-108">Here is the sample JSON definition of a Databricks Notebook Activity:</span><span class="sxs-lookup"><span data-stu-id="33432-108">Here is the sample JSON definition of a Databricks Notebook Activity:</span></span>

```json
{
    "activity": {
        "name": "MyActivity",
        "description": "MyActivity description",
        "type": "DatabricksNotebook",
        "linkedServiceName": {
            "referenceName": "MyDatabricksLinkedservice",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "notebookPath": "/Users/user@example.com/ScalaExampleNotebook",
            "baseParameters": {
                "inputpath": "input/folder1/",
                "outputpath": "output/"
            },
            "libraries": [
                {
                "jar": "dbfs:/docs/library.jar"
                }
            ]
        }
    }
}
```

## <a name="databricks-notebook-activity-properties"></a><span data-ttu-id="33432-109">Databricks Notebook activity properties</span><span class="sxs-lookup"><span data-stu-id="33432-109">Databricks Notebook activity properties</span></span>

<span data-ttu-id="33432-110">The following table describes the JSON properties used in the JSON definition:</span><span class="sxs-lookup"><span data-stu-id="33432-110">The following table describes the JSON properties used in the JSON definition:</span></span>

|<span data-ttu-id="33432-111">Property</span><span class="sxs-lookup"><span data-stu-id="33432-111">Property</span></span>|<span data-ttu-id="33432-112">Description</span><span class="sxs-lookup"><span data-stu-id="33432-112">Description</span></span>|<span data-ttu-id="33432-113">Required</span><span class="sxs-lookup"><span data-stu-id="33432-113">Required</span></span>|
|---|---|---|
|<span data-ttu-id="33432-114">name</span><span class="sxs-lookup"><span data-stu-id="33432-114">name</span></span>|<span data-ttu-id="33432-115">Name of the activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="33432-115">Name of the activity in the pipeline.</span></span>|<span data-ttu-id="33432-116">Yes</span><span class="sxs-lookup"><span data-stu-id="33432-116">Yes</span></span>|
|<span data-ttu-id="33432-117">description</span><span class="sxs-lookup"><span data-stu-id="33432-117">description</span></span>|<span data-ttu-id="33432-118">Text describing what the activity does.</span><span class="sxs-lookup"><span data-stu-id="33432-118">Text describing what the activity does.</span></span>|<span data-ttu-id="33432-119">No</span><span class="sxs-lookup"><span data-stu-id="33432-119">No</span></span>|
|<span data-ttu-id="33432-120">type</span><span class="sxs-lookup"><span data-stu-id="33432-120">type</span></span>|<span data-ttu-id="33432-121">For Databricks Notebook Activity, the activity type is DatabricksNotebook.</span><span class="sxs-lookup"><span data-stu-id="33432-121">For Databricks Notebook Activity, the activity type is DatabricksNotebook.</span></span>|<span data-ttu-id="33432-122">Yes</span><span class="sxs-lookup"><span data-stu-id="33432-122">Yes</span></span>|
|<span data-ttu-id="33432-123">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="33432-123">linkedServiceName</span></span>|<span data-ttu-id="33432-124">Name of the Databricks Linked Service on which the Databricks notebook runs.</span><span class="sxs-lookup"><span data-stu-id="33432-124">Name of the Databricks Linked Service on which the Databricks notebook runs.</span></span> <span data-ttu-id="33432-125">To learn about this linked service, see [Compute linked services](compute-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="33432-125">To learn about this linked service, see [Compute linked services](compute-linked-services.md) article.</span></span>|<span data-ttu-id="33432-126">Yes</span><span class="sxs-lookup"><span data-stu-id="33432-126">Yes</span></span>|
|<span data-ttu-id="33432-127">notebookPath</span><span class="sxs-lookup"><span data-stu-id="33432-127">notebookPath</span></span>|<span data-ttu-id="33432-128">The absolute path of the notebook to be run in the Databricks Workspace.</span><span class="sxs-lookup"><span data-stu-id="33432-128">The absolute path of the notebook to be run in the Databricks Workspace.</span></span> <span data-ttu-id="33432-129">This path must begin with a slash.</span><span class="sxs-lookup"><span data-stu-id="33432-129">This path must begin with a slash.</span></span>|<span data-ttu-id="33432-130">Yes</span><span class="sxs-lookup"><span data-stu-id="33432-130">Yes</span></span>|
|<span data-ttu-id="33432-131">baseParameters</span><span class="sxs-lookup"><span data-stu-id="33432-131">baseParameters</span></span>|<span data-ttu-id="33432-132">An array of Key-Value pairs.</span><span class="sxs-lookup"><span data-stu-id="33432-132">An array of Key-Value pairs.</span></span> <span data-ttu-id="33432-133">Base parameters can be used for each activity run.</span><span class="sxs-lookup"><span data-stu-id="33432-133">Base parameters can be used for each activity run.</span></span> <span data-ttu-id="33432-134">If the notebook takes a parameter that is not specified, the default value from the notebook will be used.</span><span class="sxs-lookup"><span data-stu-id="33432-134">If the notebook takes a parameter that is not specified, the default value from the notebook will be used.</span></span> <span data-ttu-id="33432-135">Find more on parameters in [Databricks Notebooks](https://docs.databricks.com/api/latest/jobs.html#jobsparampair).</span><span class="sxs-lookup"><span data-stu-id="33432-135">Find more on parameters in [Databricks Notebooks](https://docs.databricks.com/api/latest/jobs.html#jobsparampair).</span></span>|<span data-ttu-id="33432-136">No</span><span class="sxs-lookup"><span data-stu-id="33432-136">No</span></span>|
|<span data-ttu-id="33432-137">libraries</span><span class="sxs-lookup"><span data-stu-id="33432-137">libraries</span></span>|<span data-ttu-id="33432-138">A list of libraries to be installed on the cluster that will execute the job.</span><span class="sxs-lookup"><span data-stu-id="33432-138">A list of libraries to be installed on the cluster that will execute the job.</span></span> <span data-ttu-id="33432-139">It can be an array of \<string, object>.</span><span class="sxs-lookup"><span data-stu-id="33432-139">It can be an array of \<string, object>.</span></span>|<span data-ttu-id="33432-140">No</span><span class="sxs-lookup"><span data-stu-id="33432-140">No</span></span>|


## <a name="supported-libraries-for-databricks-activities"></a><span data-ttu-id="33432-141">Supported libraries for Databricks activities</span><span class="sxs-lookup"><span data-stu-id="33432-141">Supported libraries for Databricks activities</span></span>

<span data-ttu-id="33432-142">In the above Databricks activity definition, you specify these library types: *jar*, *egg*, *maven*, *pypi*, *cran*.</span><span class="sxs-lookup"><span data-stu-id="33432-142">In the above Databricks activity definition, you specify these library types: *jar*, *egg*, *maven*, *pypi*, *cran*.</span></span>

```json
{
    "libraries": [
        {
            "jar": "dbfs:/mnt/libraries/library.jar"
        },
        {
            "egg": "dbfs:/mnt/libraries/library.egg"
        },
        {
            "maven": {
                "coordinates": "org.jsoup:jsoup:1.7.2",
                "exclusions": [ "slf4j:slf4j" ]
            }
        },
        {
            "pypi": {
                "package": "simplejson",
                "repo": "http://my-pypi-mirror.com"
            }
        },
        {
            "cran": {
                "package": "ada",
                "repo": "http://cran.us.r-project.org"
            }
        }
    ]
}

```

<span data-ttu-id="33432-143">For more details, see the [Databricks documentation](https://docs.azuredatabricks.net/api/latest/libraries.html#managedlibrarieslibrary) for library types.</span><span class="sxs-lookup"><span data-stu-id="33432-143">For more details, see the [Databricks documentation](https://docs.azuredatabricks.net/api/latest/libraries.html#managedlibrarieslibrary) for library types.</span></span>

## <a name="how-to-upload-a-library-in-databricks"></a><span data-ttu-id="33432-144">How to upload a library in Databricks</span><span class="sxs-lookup"><span data-stu-id="33432-144">How to upload a library in Databricks</span></span>

#### <a name="using-databricks-workspace-uihttpsdocsazuredatabricksnetuser-guidelibrarieshtmlcreate-a-library"></a>[<span data-ttu-id="33432-145">Using Databricks workspace UI</span><span class="sxs-lookup"><span data-stu-id="33432-145">Using Databricks workspace UI</span></span>](https://docs.azuredatabricks.net/user-guide/libraries.html#create-a-library)

<span data-ttu-id="33432-146">To obtain the dbfs path of the library added using UI, you can use the [Databricks CLI (installation)](https://docs.azuredatabricks.net/user-guide/dev-tools/databricks-cli.html#install-the-cli).</span><span class="sxs-lookup"><span data-stu-id="33432-146">To obtain the dbfs path of the library added using UI, you can use the [Databricks CLI (installation)](https://docs.azuredatabricks.net/user-guide/dev-tools/databricks-cli.html#install-the-cli).</span></span> 

<span data-ttu-id="33432-147">Typically, the Jar libraries are stored under dbfs:/FileStore/jars while using the UI.</span><span class="sxs-lookup"><span data-stu-id="33432-147">Typically, the Jar libraries are stored under dbfs:/FileStore/jars while using the UI.</span></span> <span data-ttu-id="33432-148">You can list all through the CLI: *databricks fs ls dbfs:/FileStore/jars*.</span><span class="sxs-lookup"><span data-stu-id="33432-148">You can list all through the CLI: *databricks fs ls dbfs:/FileStore/jars*.</span></span>



#### <a name="copy-library-using-databricks-clihttpsdocsazuredatabricksnetuser-guidedev-toolsdatabricks-clihtmlcopy-a-file-to-dbfs"></a>[<span data-ttu-id="33432-149">Copy library using Databricks CLI</span><span class="sxs-lookup"><span data-stu-id="33432-149">Copy library using Databricks CLI</span></span>](https://docs.azuredatabricks.net/user-guide/dev-tools/databricks-cli.html#copy-a-file-to-dbfs)

<span data-ttu-id="33432-150">Example: *databricks fs cp SparkPi-assembly-0.1.jar dbfs:/FileStore/jars*</span><span class="sxs-lookup"><span data-stu-id="33432-150">Example: *databricks fs cp SparkPi-assembly-0.1.jar dbfs:/FileStore/jars*</span></span>
