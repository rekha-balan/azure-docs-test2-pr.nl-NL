---
title: 'REST API: Filesystem operations on Azure Data Lake Storage Gen1 | Microsoft Docs'
description: Use WebHDFS REST APIs to perform filesystem operations on Azure Data Lake Storage Gen1
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: conceptual
ms.date: 05/29/2018
ms.author: nitinme
ms.openlocfilehash: 62ecf3b1983853629f6bc5fd594231188aa67bcd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870065"
---
# <a name="filesystem-operations-on-azure-data-lake-storage-gen1-using-rest-api"></a><span data-ttu-id="0727e-103">Filesystem operations on Azure Data Lake Storage Gen1 using REST API</span><span class="sxs-lookup"><span data-stu-id="0727e-103">Filesystem operations on Azure Data Lake Storage Gen1 using REST API</span></span>
> [!div class="op_single_selector"]
> * [.NET SDK](data-lake-store-data-operations-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-data-operations-rest-api.md)
> * [Python](data-lake-store-data-operations-python.md)
>
> 

<span data-ttu-id="0727e-108">In this article, you learn how to use WebHDFS REST APIs and Data Lake Storage Gen1 REST APIs to perform filesystem operations on Azure Data Lake Storage Gen1.</span><span class="sxs-lookup"><span data-stu-id="0727e-108">In this article, you learn how to use WebHDFS REST APIs and Data Lake Storage Gen1 REST APIs to perform filesystem operations on Azure Data Lake Storage Gen1.</span></span> <span data-ttu-id="0727e-109">For instructions on how to perform account management operations on Data Lake Storage Gen1 using REST API, see [Account management operations on Data Lake Storage Gen1 using REST API](data-lake-store-get-started-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="0727e-109">For instructions on how to perform account management operations on Data Lake Storage Gen1 using REST API, see [Account management operations on Data Lake Storage Gen1 using REST API](data-lake-store-get-started-rest-api.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0727e-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0727e-110">Prerequisites</span></span>
* <span data-ttu-id="0727e-111">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="0727e-111">**An Azure subscription**.</span></span> <span data-ttu-id="0727e-112">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0727e-112">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="0727e-113">**Azure Data Lake Storage Gen1 account**.</span><span class="sxs-lookup"><span data-stu-id="0727e-113">**Azure Data Lake Storage Gen1 account**.</span></span> <span data-ttu-id="0727e-114">Follow the instructions at [Get started with Azure Data Lake Storage Gen1 using the Azure portal](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0727e-114">Follow the instructions at [Get started with Azure Data Lake Storage Gen1 using the Azure portal](data-lake-store-get-started-portal.md).</span></span>

* <span data-ttu-id="0727e-115">**[cURL](http://curl.haxx.se/)**.</span><span class="sxs-lookup"><span data-stu-id="0727e-115">**[cURL](http://curl.haxx.se/)**.</span></span> <span data-ttu-id="0727e-116">This article uses cURL to demonstrate how to make REST API calls against a Data Lake Storage Gen1 account.</span><span class="sxs-lookup"><span data-stu-id="0727e-116">This article uses cURL to demonstrate how to make REST API calls against a Data Lake Storage Gen1 account.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="0727e-117">How do I authenticate using Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0727e-117">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="0727e-118">You can use two approaches to authenticate using Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0727e-118">You can use two approaches to authenticate using Azure Active Directory.</span></span>

* <span data-ttu-id="0727e-119">For end-user authentication for your application (interactive), see [End-user authentication with Data Lake Storage Gen1 using .NET SDK](data-lake-store-end-user-authenticate-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="0727e-119">For end-user authentication for your application (interactive), see [End-user authentication with Data Lake Storage Gen1 using .NET SDK](data-lake-store-end-user-authenticate-rest-api.md).</span></span>
* <span data-ttu-id="0727e-120">For service-to-service authentication for your application (non-interactive), see [Service-to-service authentication with Data Lake Storage Gen1 using .NET SDK](data-lake-store-service-to-service-authenticate-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="0727e-120">For service-to-service authentication for your application (non-interactive), see [Service-to-service authentication with Data Lake Storage Gen1 using .NET SDK](data-lake-store-service-to-service-authenticate-rest-api.md).</span></span>


## <a name="create-folders"></a><span data-ttu-id="0727e-121">Create folders</span><span class="sxs-lookup"><span data-stu-id="0727e-121">Create folders</span></span>
<span data-ttu-id="0727e-122">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span><span class="sxs-lookup"><span data-stu-id="0727e-122">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span></span>

<span data-ttu-id="0727e-123">Use the following cURL command.</span><span class="sxs-lookup"><span data-stu-id="0727e-123">Use the following cURL command.</span></span> <span data-ttu-id="0727e-124">Replace **\<yourstorename>** with your Data Lake Storage Gen1 account name.</span><span class="sxs-lookup"><span data-stu-id="0727e-124">Replace **\<yourstorename>** with your Data Lake Storage Gen1 account name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/?op=MKDIRS'

<span data-ttu-id="0727e-125">In the preceding command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span><span class="sxs-lookup"><span data-stu-id="0727e-125">In the preceding command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span></span> <span data-ttu-id="0727e-126">This command creates a directory called **mytempdir** under the root folder of your Data Lake Storage Gen1 account.</span><span class="sxs-lookup"><span data-stu-id="0727e-126">This command creates a directory called **mytempdir** under the root folder of your Data Lake Storage Gen1 account.</span></span>

<span data-ttu-id="0727e-127">If the operation completes successfully, you should see a response like the following snippet:</span><span class="sxs-lookup"><span data-stu-id="0727e-127">If the operation completes successfully, you should see a response like the following snippet:</span></span>

    {"boolean":true}

## <a name="list-folders"></a><span data-ttu-id="0727e-128">List folders</span><span class="sxs-lookup"><span data-stu-id="0727e-128">List folders</span></span>
<span data-ttu-id="0727e-129">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span><span class="sxs-lookup"><span data-stu-id="0727e-129">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span></span>

<span data-ttu-id="0727e-130">Use the following cURL command.</span><span class="sxs-lookup"><span data-stu-id="0727e-130">Use the following cURL command.</span></span> <span data-ttu-id="0727e-131">Replace **\<yourstorename>** with your Data Lake Storage Gen1 account name.</span><span class="sxs-lookup"><span data-stu-id="0727e-131">Replace **\<yourstorename>** with your Data Lake Storage Gen1 account name.</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS'

<span data-ttu-id="0727e-132">In the preceding command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span><span class="sxs-lookup"><span data-stu-id="0727e-132">In the preceding command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span></span>

<span data-ttu-id="0727e-133">If the operation completes successfully, you should see a response like the following snippet:</span><span class="sxs-lookup"><span data-stu-id="0727e-133">If the operation completes successfully, you should see a response like the following snippet:</span></span>

    {
    "FileStatuses": {
        "FileStatus": [{
            "length": 0,
            "pathSuffix": "mytempdir",
            "type": "DIRECTORY",
            "blockSize": 268435456,
            "accessTime": 1458324719512,
            "modificationTime": 1458324719512,
            "replication": 0,
            "permission": "777",
            "owner": "<GUID>",
            "group": "<GUID>"
        }]
    }
    }

## <a name="upload-data"></a><span data-ttu-id="0727e-134">Upload data</span><span class="sxs-lookup"><span data-stu-id="0727e-134">Upload data</span></span>
<span data-ttu-id="0727e-135">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span><span class="sxs-lookup"><span data-stu-id="0727e-135">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span></span>

<span data-ttu-id="0727e-136">Use the following cURL command.</span><span class="sxs-lookup"><span data-stu-id="0727e-136">Use the following cURL command.</span></span> <span data-ttu-id="0727e-137">Replace **\<yourstorename>** with your Data Lake Storage Gen1 account name.</span><span class="sxs-lookup"><span data-stu-id="0727e-137">Replace **\<yourstorename>** with your Data Lake Storage Gen1 account name.</span></span>

    curl -i -X PUT -L -T 'C:\temp\list.txt' -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE'

<span data-ttu-id="0727e-138">In the preceding syntax **-T** parameter is the location of the file you are uploading.</span><span class="sxs-lookup"><span data-stu-id="0727e-138">In the preceding syntax **-T** parameter is the location of the file you are uploading.</span></span>

<span data-ttu-id="0727e-139">The output is similar to the following snippet:</span><span class="sxs-lookup"><span data-stu-id="0727e-139">The output is similar to the following snippet:</span></span>
   
    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE&write=true
    ...
    Content-Length: 0

    HTTP/1.1 100 Continue

    HTTP/1.1 201 Created
    ...

## <a name="read-data"></a><span data-ttu-id="0727e-140">Read data</span><span class="sxs-lookup"><span data-stu-id="0727e-140">Read data</span></span>
<span data-ttu-id="0727e-141">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span><span class="sxs-lookup"><span data-stu-id="0727e-141">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span></span>

<span data-ttu-id="0727e-142">Reading data from a Data Lake Storage Gen1 account is a two-step process.</span><span class="sxs-lookup"><span data-stu-id="0727e-142">Reading data from a Data Lake Storage Gen1 account is a two-step process.</span></span>

* <span data-ttu-id="0727e-143">You first submit a GET request against the endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span><span class="sxs-lookup"><span data-stu-id="0727e-143">You first submit a GET request against the endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span></span> <span data-ttu-id="0727e-144">This call returns a location to submit the next GET request to.</span><span class="sxs-lookup"><span data-stu-id="0727e-144">This call returns a location to submit the next GET request to.</span></span>
* <span data-ttu-id="0727e-145">You then submit the GET request against the endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span><span class="sxs-lookup"><span data-stu-id="0727e-145">You then submit the GET request against the endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span></span> <span data-ttu-id="0727e-146">This call displays the contents of the file.</span><span class="sxs-lookup"><span data-stu-id="0727e-146">This call displays the contents of the file.</span></span>

<span data-ttu-id="0727e-147">However, because there is no difference in the input parameters between the first and the second step, you can use the `-L` parameter to submit the first request.</span><span class="sxs-lookup"><span data-stu-id="0727e-147">However, because there is no difference in the input parameters between the first and the second step, you can use the `-L` parameter to submit the first request.</span></span> <span data-ttu-id="0727e-148">`-L` option essentially combines two requests into one and makes cURL redo the request on the new location.</span><span class="sxs-lookup"><span data-stu-id="0727e-148">`-L` option essentially combines two requests into one and makes cURL redo the request on the new location.</span></span> <span data-ttu-id="0727e-149">Finally, the output from all the request calls is displayed, like shown in the following snippet.</span><span class="sxs-lookup"><span data-stu-id="0727e-149">Finally, the output from all the request calls is displayed, like shown in the following snippet.</span></span> <span data-ttu-id="0727e-150">Replace **\<yourstorename>** with your Data Lake Storage Gen1 account name.</span><span class="sxs-lookup"><span data-stu-id="0727e-150">Replace **\<yourstorename>** with your Data Lake Storage Gen1 account name.</span></span>

    curl -i -L GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN'

<span data-ttu-id="0727e-151">You should see an output similar to the following snippet:</span><span class="sxs-lookup"><span data-stu-id="0727e-151">You should see an output similar to the following snippet:</span></span>

    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/somerandomfile.txt?op=OPEN&read=true
    ...

    HTTP/1.1 200 OK
    ...

    Hello, Data Lake Store user!

## <a name="rename-a-file"></a><span data-ttu-id="0727e-152">Rename a file</span><span class="sxs-lookup"><span data-stu-id="0727e-152">Rename a file</span></span>
<span data-ttu-id="0727e-153">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span><span class="sxs-lookup"><span data-stu-id="0727e-153">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span></span>

<span data-ttu-id="0727e-154">Use the following cURL command to rename a file.</span><span class="sxs-lookup"><span data-stu-id="0727e-154">Use the following cURL command to rename a file.</span></span> <span data-ttu-id="0727e-155">Replace **\<yourstorename>** with your Data Lake Storage Gen1 account name.</span><span class="sxs-lookup"><span data-stu-id="0727e-155">Replace **\<yourstorename>** with your Data Lake Storage Gen1 account name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=RENAME&destination=/mytempdir/myinputfile1.txt'

<span data-ttu-id="0727e-156">You should see an output similar to the  following snippet:</span><span class="sxs-lookup"><span data-stu-id="0727e-156">You should see an output similar to the  following snippet:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-file"></a><span data-ttu-id="0727e-157">Delete a file</span><span class="sxs-lookup"><span data-stu-id="0727e-157">Delete a file</span></span>
<span data-ttu-id="0727e-158">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span><span class="sxs-lookup"><span data-stu-id="0727e-158">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span></span>

<span data-ttu-id="0727e-159">Use the following cURL command to delete a file.</span><span class="sxs-lookup"><span data-stu-id="0727e-159">Use the following cURL command to delete a file.</span></span> <span data-ttu-id="0727e-160">Replace **\<yourstorename>** with your Data Lake Storage Gen1 account name.</span><span class="sxs-lookup"><span data-stu-id="0727e-160">Replace **\<yourstorename>** with your Data Lake Storage Gen1 account name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile1.txt?op=DELETE'

<span data-ttu-id="0727e-161">You should see an output like the following:</span><span class="sxs-lookup"><span data-stu-id="0727e-161">You should see an output like the following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="next-steps"></a><span data-ttu-id="0727e-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="0727e-162">Next steps</span></span>
* <span data-ttu-id="0727e-163">[Account management operations on Data Lake Storage Gen1 using REST API](data-lake-store-get-started-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="0727e-163">[Account management operations on Data Lake Storage Gen1 using REST API](data-lake-store-get-started-rest-api.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="0727e-164">See also</span><span class="sxs-lookup"><span data-stu-id="0727e-164">See also</span></span>
* [<span data-ttu-id="0727e-165">Azure Data Lake Storage Gen1 REST API Reference</span><span class="sxs-lookup"><span data-stu-id="0727e-165">Azure Data Lake Storage Gen1 REST API Reference</span></span>](https://docs.microsoft.com/rest/api/datalakestore/)
* [<span data-ttu-id="0727e-166">Open Source Big Data applications compatible with Azure Data Lake Storage Gen1</span><span class="sxs-lookup"><span data-stu-id="0727e-166">Open Source Big Data applications compatible with Azure Data Lake Storage Gen1</span></span>](data-lake-store-compatible-oss-other-applications.md)

