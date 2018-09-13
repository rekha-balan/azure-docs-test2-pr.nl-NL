---
title: Use the REST API to get started with Data Lake Store | Microsoft Docs
description: Use WebHDFS REST APIs to perform operations on Data Lake Store
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57ac6501-cb71-4f75-82c2-acc07c562889
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/03/2017
ms.author: nitinme
ms.openlocfilehash: 650ff05715c8c0d915c82f9de49756530b8f3138
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552164"
---
# <a name="get-started-with-azure-data-lake-store-using-rest-apis"></a><span data-ttu-id="202f0-103">Get started with Azure Data Lake Store using REST APIs</span><span class="sxs-lookup"><span data-stu-id="202f0-103">Get started with Azure Data Lake Store using REST APIs</span></span>
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI](data-lake-store-get-started-cli.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="202f0-113">In this article, you will learn how to use WebHDFS REST APIs and Data Lake Store REST APIs to perform account management as well as filesystem operations on Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="202f0-113">In this article, you will learn how to use WebHDFS REST APIs and Data Lake Store REST APIs to perform account management as well as filesystem operations on Azure Data Lake Store.</span></span> <span data-ttu-id="202f0-114">Azure Data Lake Store exposes its own REST APIs for account management operations.</span><span class="sxs-lookup"><span data-stu-id="202f0-114">Azure Data Lake Store exposes its own REST APIs for account management operations.</span></span> <span data-ttu-id="202f0-115">However, because Data Lake Store is compatible with HDFS and Hadoop ecosystem, it supports using WebHDFS REST APIs for filesystem operations.</span><span class="sxs-lookup"><span data-stu-id="202f0-115">However, because Data Lake Store is compatible with HDFS and Hadoop ecosystem, it supports using WebHDFS REST APIs for filesystem operations.</span></span>

> [!NOTE]
> For detailed information on the REST API support for Data Lake Store, see [Azure Data Lake Store REST API Reference](https://msdn.microsoft.com/library/mt693424.aspx).
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="202f0-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="202f0-117">Prerequisites</span></span>
* <span data-ttu-id="202f0-118">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="202f0-118">**An Azure subscription**.</span></span> <span data-ttu-id="202f0-119">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="202f0-119">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="202f0-120">**Create an Azure Active Directory Application**.</span><span class="sxs-lookup"><span data-stu-id="202f0-120">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="202f0-121">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="202f0-121">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="202f0-122">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span><span class="sxs-lookup"><span data-stu-id="202f0-122">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="202f0-123">For instructions and more information on how to authenticate, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="202f0-123">For instructions and more information on how to authenticate, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="202f0-124">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="202f0-124">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="202f0-125">This article uses cURL to demonstrate how to make REST API calls against a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="202f0-125">This article uses cURL to demonstrate how to make REST API calls against a Data Lake Store account.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="202f0-126">How do I authenticate using Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="202f0-126">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="202f0-127">You can use two approaches to authenticate using Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="202f0-127">You can use two approaches to authenticate using Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="202f0-128">End-user authentication (interactive)</span><span class="sxs-lookup"><span data-stu-id="202f0-128">End-user authentication (interactive)</span></span>
<span data-ttu-id="202f0-129">In this scenario, the application prompts the user to log in and all the operations are performed in the context of the user.</span><span class="sxs-lookup"><span data-stu-id="202f0-129">In this scenario, the application prompts the user to log in and all the operations are performed in the context of the user.</span></span> <span data-ttu-id="202f0-130">Perform the following steps for interactive authentication.</span><span class="sxs-lookup"><span data-stu-id="202f0-130">Perform the following steps for interactive authentication.</span></span>

1. <span data-ttu-id="202f0-131">Through your application, redirect the user to the following URL:</span><span class="sxs-lookup"><span data-stu-id="202f0-131">Through your application, redirect the user to the following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<CLIENT-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > \<REDIRECT-URI> needs to be encoded for use in a URL. So, for https://localhost, use `https%3A%2F%2Flocalhost`)
   > 
   > 
   
    <span data-ttu-id="202f0-134">For the purpose of this tutorial, you can replace the placeholder values in the URL above and paste it in a web browser's address bar.</span><span class="sxs-lookup"><span data-stu-id="202f0-134">For the purpose of this tutorial, you can replace the placeholder values in the URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="202f0-135">You will be redirected to authenticate using your Azure login.</span><span class="sxs-lookup"><span data-stu-id="202f0-135">You will be redirected to authenticate using your Azure login.</span></span> <span data-ttu-id="202f0-136">Once you successfully log in, the response is displayed in the browser's address bar.</span><span class="sxs-lookup"><span data-stu-id="202f0-136">Once you successfully log in, the response is displayed in the browser's address bar.</span></span> <span data-ttu-id="202f0-137">The response will be in the following format:</span><span class="sxs-lookup"><span data-stu-id="202f0-137">The response will be in the following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="202f0-138">Capture the authorization code from the response.</span><span class="sxs-lookup"><span data-stu-id="202f0-138">Capture the authorization code from the response.</span></span> <span data-ttu-id="202f0-139">For this tutorial, you can copy the authorization code from the address bar of the web browser and pass it in the POST request to the token endpoint, as shown below:</span><span class="sxs-lookup"><span data-stu-id="202f0-139">For this tutorial, you can copy the authorization code from the address bar of the web browser and pass it in the POST request to the token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<CLIENT-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > In this case, the \<REDIRECT-URI> need not be encoded.
   > 
   > 
3. <span data-ttu-id="202f0-141">The response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span><span class="sxs-lookup"><span data-stu-id="202f0-141">The response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="202f0-142">Your application uses the access token when accessing Azure Data Lake Store and the refresh token to get another access token when an access token expires.</span><span class="sxs-lookup"><span data-stu-id="202f0-142">Your application uses the access token when accessing Azure Data Lake Store and the refresh token to get another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="202f0-143">When the access token expires, you can request a new access token using the refresh token, as shown below:</span><span class="sxs-lookup"><span data-stu-id="202f0-143">When the access token expires, you can request a new access token using the refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<CLIENT-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="202f0-144">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span><span class="sxs-lookup"><span data-stu-id="202f0-144">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="202f0-145">Service-to-service authentication (non-interactive)</span><span class="sxs-lookup"><span data-stu-id="202f0-145">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="202f0-146">In this scenario, the the application provides its own credentials to perform the operations.</span><span class="sxs-lookup"><span data-stu-id="202f0-146">In this scenario, the the application provides its own credentials to perform the operations.</span></span> <span data-ttu-id="202f0-147">For this, you must issue a POST request like the one shown below.</span><span class="sxs-lookup"><span data-stu-id="202f0-147">For this, you must issue a POST request like the one shown below.</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="202f0-148">The output of this request will include an authorization token (denoted by `access-token` in the output below) that you will subsequently pass with your REST API calls.</span><span class="sxs-lookup"><span data-stu-id="202f0-148">The output of this request will include an authorization token (denoted by `access-token` in the output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="202f0-149">Save this authentication token in a text file; you will need this later in this article.</span><span class="sxs-lookup"><span data-stu-id="202f0-149">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="202f0-150">This article uses the **non-interactive** approach.</span><span class="sxs-lookup"><span data-stu-id="202f0-150">This article uses the **non-interactive** approach.</span></span> <span data-ttu-id="202f0-151">For more information on non-interactive (service-to-service calls), see [Service to service calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span><span class="sxs-lookup"><span data-stu-id="202f0-151">For more information on non-interactive (service-to-service calls), see [Service to service calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="202f0-152">Create a Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="202f0-152">Create a Data Lake Store account</span></span>
<span data-ttu-id="202f0-153">This operation is based on the REST API call defined [here](https://msdn.microsoft.com/library/mt694078.aspx).</span><span class="sxs-lookup"><span data-stu-id="202f0-153">This operation is based on the REST API call defined [here](https://msdn.microsoft.com/library/mt694078.aspx).</span></span>

<span data-ttu-id="202f0-154">Use the following cURL command.</span><span class="sxs-lookup"><span data-stu-id="202f0-154">Use the following cURL command.</span></span> <span data-ttu-id="202f0-155">Replace **\<yourstorename>** with your Data Lake Store name.</span><span class="sxs-lookup"><span data-stu-id="202f0-155">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview -d@"C:\temp\input.json"

<span data-ttu-id="202f0-156">In the above command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span><span class="sxs-lookup"><span data-stu-id="202f0-156">In the above command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span></span> <span data-ttu-id="202f0-157">The request payload for this command is contained in the **input.json** file that is provided for the `-d` parameter above.</span><span class="sxs-lookup"><span data-stu-id="202f0-157">The request payload for this command is contained in the **input.json** file that is provided for the `-d` parameter above.</span></span> <span data-ttu-id="202f0-158">The contents of the input.json file resemble the following:</span><span class="sxs-lookup"><span data-stu-id="202f0-158">The contents of the input.json file resemble the following:</span></span>

    {
    "location": "eastus2",
    "tags": {
        "department": "finance"
        },
    "properties": {}
    }    

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="202f0-159">Create folders in a Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="202f0-159">Create folders in a Data Lake Store account</span></span>
<span data-ttu-id="202f0-160">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span><span class="sxs-lookup"><span data-stu-id="202f0-160">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span></span>

<span data-ttu-id="202f0-161">Use the following cURL command.</span><span class="sxs-lookup"><span data-stu-id="202f0-161">Use the following cURL command.</span></span> <span data-ttu-id="202f0-162">Replace **\<yourstorename>** with your Data Lake Store name.</span><span class="sxs-lookup"><span data-stu-id="202f0-162">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/?op=MKDIRS

<span data-ttu-id="202f0-163">In the above command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span><span class="sxs-lookup"><span data-stu-id="202f0-163">In the above command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span></span> <span data-ttu-id="202f0-164">This command creates a directory called **mytempdir** under the root folder of your Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="202f0-164">This command creates a directory called **mytempdir** under the root folder of your Data Lake Store account.</span></span>

<span data-ttu-id="202f0-165">You should see a response like this if the operation completes successfully:</span><span class="sxs-lookup"><span data-stu-id="202f0-165">You should see a response like this if the operation completes successfully:</span></span>

    {"boolean":true}

## <a name="list-folders-in-a-data-lake-store-account"></a><span data-ttu-id="202f0-166">List folders in a Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="202f0-166">List folders in a Data Lake Store account</span></span>
<span data-ttu-id="202f0-167">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span><span class="sxs-lookup"><span data-stu-id="202f0-167">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span></span>

<span data-ttu-id="202f0-168">Use the following cURL command.</span><span class="sxs-lookup"><span data-stu-id="202f0-168">Use the following cURL command.</span></span> <span data-ttu-id="202f0-169">Replace **\<yourstorename>** with your Data Lake Store name.</span><span class="sxs-lookup"><span data-stu-id="202f0-169">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS

<span data-ttu-id="202f0-170">In the above command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span><span class="sxs-lookup"><span data-stu-id="202f0-170">In the above command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span></span>

<span data-ttu-id="202f0-171">You should see a response like this if the operation completes successfully:</span><span class="sxs-lookup"><span data-stu-id="202f0-171">You should see a response like this if the operation completes successfully:</span></span>

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
            "owner": "NotSupportYet",
            "group": "NotSupportYet"
        }]
    }
    }

## <a name="upload-data-into-a-data-lake-store-account"></a><span data-ttu-id="202f0-172">Upload data into a Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="202f0-172">Upload data into a Data Lake Store account</span></span>
<span data-ttu-id="202f0-173">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span><span class="sxs-lookup"><span data-stu-id="202f0-173">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span></span>

<span data-ttu-id="202f0-174">Uploading data using the WebHDFS REST API is a two-step process, as explained below.</span><span class="sxs-lookup"><span data-stu-id="202f0-174">Uploading data using the WebHDFS REST API is a two-step process, as explained below.</span></span>

1. <span data-ttu-id="202f0-175">Submit a HTTP PUT request without sending the file data to be uploaded.</span><span class="sxs-lookup"><span data-stu-id="202f0-175">Submit a HTTP PUT request without sending the file data to be uploaded.</span></span> <span data-ttu-id="202f0-176">In the following command, replace **\<yourstorename>** with your Data Lake Store name.</span><span class="sxs-lookup"><span data-stu-id="202f0-176">In the following command, replace **\<yourstorename>** with your Data Lake Store name.</span></span>
   
        curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/?op=CREATE
   
    <span data-ttu-id="202f0-177">The output for this command will be contain a temporary redirect URL, like the one shown below.</span><span class="sxs-lookup"><span data-stu-id="202f0-177">The output for this command will be contain a temporary redirect URL, like the one shown below.</span></span>
   
        HTTP/1.1 100 Continue
   
        HTTP/1.1 307 Temporary Redirect
        ...
        ...
        Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/somerandomfile.txt?op=CREATE&write=true
        ...
        ...
2. <span data-ttu-id="202f0-178">You must now submit another HTTP PUT request against the URL listed for the **Location** property in the response.</span><span class="sxs-lookup"><span data-stu-id="202f0-178">You must now submit another HTTP PUT request against the URL listed for the **Location** property in the response.</span></span> <span data-ttu-id="202f0-179">Replace **\<yourstorename>** with your Data Lake Store name.</span><span class="sxs-lookup"><span data-stu-id="202f0-179">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>
   
        curl -i -X PUT -T myinputfile.txt -H "Authorization: Bearer <REDACTED>" https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=CREATE&write=true
   
    <span data-ttu-id="202f0-180">The output will be similar to the following:</span><span class="sxs-lookup"><span data-stu-id="202f0-180">The output will be similar to the following:</span></span>
   
        HTTP/1.1 100 Continue
   
        HTTP/1.1 201 Created
        ...
        ...

## <a name="read-data-from-a-data-lake-store-account"></a><span data-ttu-id="202f0-181">Read data from a Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="202f0-181">Read data from a Data Lake Store account</span></span>
<span data-ttu-id="202f0-182">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span><span class="sxs-lookup"><span data-stu-id="202f0-182">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span></span>

<span data-ttu-id="202f0-183">Reading data from a Data Lake Store account is a two-step process.</span><span class="sxs-lookup"><span data-stu-id="202f0-183">Reading data from a Data Lake Store account is a two-step process.</span></span>

* <span data-ttu-id="202f0-184">You first submit a GET request against the endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span><span class="sxs-lookup"><span data-stu-id="202f0-184">You first submit a GET request against the endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span></span> <span data-ttu-id="202f0-185">This will return a location to submit the next GET request to.</span><span class="sxs-lookup"><span data-stu-id="202f0-185">This will return a location to submit the next GET request to.</span></span>
* <span data-ttu-id="202f0-186">You then submit the GET request against the endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span><span class="sxs-lookup"><span data-stu-id="202f0-186">You then submit the GET request against the endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span></span> <span data-ttu-id="202f0-187">This will display the contents of the file.</span><span class="sxs-lookup"><span data-stu-id="202f0-187">This will display the contents of the file.</span></span>

<span data-ttu-id="202f0-188">However, because there is no difference in the input parameters between the first and the second step, you can use the `-L` parameter to submit the first request.</span><span class="sxs-lookup"><span data-stu-id="202f0-188">However, because there is no difference in the input parameters between the first and the second step, you can use the `-L` parameter to submit the first request.</span></span> <span data-ttu-id="202f0-189">`-L` option essentially combines two requests into one and will make cURL redo the request on the new location.</span><span class="sxs-lookup"><span data-stu-id="202f0-189">`-L` option essentially combines two requests into one and will make cURL redo the request on the new location.</span></span> <span data-ttu-id="202f0-190">Finally, the output from all the request calls is displayed, like shown below.</span><span class="sxs-lookup"><span data-stu-id="202f0-190">Finally, the output from all the request calls is displayed, like shown below.</span></span> <span data-ttu-id="202f0-191">Replace **\<yourstorename>** with your Data Lake Store name.</span><span class="sxs-lookup"><span data-stu-id="202f0-191">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -L GET -H "Authorization: Bearer <REDACTED>" https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN

<span data-ttu-id="202f0-192">You should see an output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="202f0-192">You should see an output similar to the following:</span></span>

    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/somerandomfile.txt?op=OPEN&read=true
    ...

    HTTP/1.1 200 OK
    ...

    Hello, Data Lake Store user!

## <a name="rename-a-file-in-a-data-lake-store-account"></a><span data-ttu-id="202f0-193">Rename a file in a Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="202f0-193">Rename a file in a Data Lake Store account</span></span>
<span data-ttu-id="202f0-194">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span><span class="sxs-lookup"><span data-stu-id="202f0-194">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span></span>

<span data-ttu-id="202f0-195">Use the following cURL command to rename a file.</span><span class="sxs-lookup"><span data-stu-id="202f0-195">Use the following cURL command to rename a file.</span></span> <span data-ttu-id="202f0-196">Replace **\<yourstorename>** with your Data Lake Store name.</span><span class="sxs-lookup"><span data-stu-id="202f0-196">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=RENAME&destination=/mytempdir/myinputfile1.txt

<span data-ttu-id="202f0-197">You should see an output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="202f0-197">You should see an output similar to the following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-file-from-a-data-lake-store-account"></a><span data-ttu-id="202f0-198">Delete a file from a Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="202f0-198">Delete a file from a Data Lake Store account</span></span>
<span data-ttu-id="202f0-199">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span><span class="sxs-lookup"><span data-stu-id="202f0-199">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span></span>

<span data-ttu-id="202f0-200">Use the following cURL command to delete a file.</span><span class="sxs-lookup"><span data-stu-id="202f0-200">Use the following cURL command to delete a file.</span></span> <span data-ttu-id="202f0-201">Replace **\<yourstorename>** with your Data Lake Store name.</span><span class="sxs-lookup"><span data-stu-id="202f0-201">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile1.txt?op=DELETE

<span data-ttu-id="202f0-202">You should see an output like the following:</span><span class="sxs-lookup"><span data-stu-id="202f0-202">You should see an output like the following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="202f0-203">Delete a Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="202f0-203">Delete a Data Lake Store account</span></span>
<span data-ttu-id="202f0-204">This operation is based on the REST API call defined [here](https://msdn.microsoft.com/library/mt694075.aspx).</span><span class="sxs-lookup"><span data-stu-id="202f0-204">This operation is based on the REST API call defined [here](https://msdn.microsoft.com/library/mt694075.aspx).</span></span>

<span data-ttu-id="202f0-205">Use the following cURL command to delete a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="202f0-205">Use the following cURL command to delete a Data Lake Store account.</span></span> <span data-ttu-id="202f0-206">Replace **\<yourstorename>** with your Data Lake Store name.</span><span class="sxs-lookup"><span data-stu-id="202f0-206">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview

<span data-ttu-id="202f0-207">You should see an output like the following:</span><span class="sxs-lookup"><span data-stu-id="202f0-207">You should see an output like the following:</span></span>

    HTTP/1.1 200 OK
    ...
    ...

## <a name="see-also"></a><span data-ttu-id="202f0-208">See also</span><span class="sxs-lookup"><span data-stu-id="202f0-208">See also</span></span>
* [<span data-ttu-id="202f0-209">Open Source Big Data applications compatible with Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="202f0-209">Open Source Big Data applications compatible with Azure Data Lake Store</span></span>](data-lake-store-compatible-oss-other-applications.md)

