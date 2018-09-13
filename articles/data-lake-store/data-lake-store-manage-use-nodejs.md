---
title: Get started with Azure Data Lake Store using Azure SDK for Node.js | Microsoft Docs
description: Learn how to use Node.js to work with Data Lake Store accounts and the file system.
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 2fee173c-69ae-4e1d-8773-48618cda9e16
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/31/2017
ms.author: nitinme
ms.openlocfilehash: 091ab246826c96b9d816c87b27014c1e54039429
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549260"
---
# <a name="get-started-with-azure-data-lake-store-using-azure-sdk-for-nodejs"></a><span data-ttu-id="785b3-103">Get started with Azure Data Lake Store using Azure SDK for Node.js</span><span class="sxs-lookup"><span data-stu-id="785b3-103">Get started with Azure Data Lake Store using Azure SDK for Node.js</span></span>
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI](data-lake-store-get-started-cli.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
> 

> [!NOTE]
> For uploading and downloading large amount of data (large files, a large number of files, or both), we recommend that you use the [Python SDK](data-lake-store-get-started-python.md), the [.NET SDK](data-lake-store-get-started-net-sdk.md), or [Azure PowerShell](data-lake-store-get-started-powershell.md). These options have better performance as they use multiple threads to parallelize the data movement.
> 
> 

<span data-ttu-id="785b3-114">Learn how to use the Azure SDK for Node.js to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="785b3-114">Learn how to use the Azure SDK for Node.js to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span> <span data-ttu-id="785b3-115">Currently, the SDK supports</span><span class="sxs-lookup"><span data-stu-id="785b3-115">Currently, the SDK supports</span></span>

* <span data-ttu-id="785b3-116">**Node.js version: 0.10.0 or higher**</span><span class="sxs-lookup"><span data-stu-id="785b3-116">**Node.js version: 0.10.0 or higher**</span></span>
* <span data-ttu-id="785b3-117">**REST API version for Account: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="785b3-117">**REST API version for Account: 2015-10-01-preview**</span></span>
* <span data-ttu-id="785b3-118">**REST API version for FileSystem: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="785b3-118">**REST API version for FileSystem: 2015-10-01-preview**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="785b3-119">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="785b3-119">Prerequisites</span></span>
<span data-ttu-id="785b3-120">Before you begin this article, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="785b3-120">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="785b3-121">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="785b3-121">**An Azure subscription**.</span></span> <span data-ttu-id="785b3-122">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="785b3-122">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="785b3-123">**Create an Azure Active Directory Application**.</span><span class="sxs-lookup"><span data-stu-id="785b3-123">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="785b3-124">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="785b3-124">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="785b3-125">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span><span class="sxs-lookup"><span data-stu-id="785b3-125">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="785b3-126">For instructions and more information on how to authenticate, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="785b3-126">For instructions and more information on how to authenticate, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="how-to-install"></a><span data-ttu-id="785b3-127">How to Install</span><span class="sxs-lookup"><span data-stu-id="785b3-127">How to Install</span></span>
```bash
npm install azure-arm-datalake-store
```

## <a name="authenticate-using-azure-active-directory"></a><span data-ttu-id="785b3-128">Authenticate using Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="785b3-128">Authenticate using Azure Active Directory</span></span>
<span data-ttu-id="785b3-129">The snippets below show two separate ways of authenticating with Data Lake Store using Azure AD.</span><span class="sxs-lookup"><span data-stu-id="785b3-129">The snippets below show two separate ways of authenticating with Data Lake Store using Azure AD.</span></span> <span data-ttu-id="785b3-130">For a detailed discussion on various methods to use for authentication with Data Lake Store, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="785b3-130">For a detailed discussion on various methods to use for authentication with Data Lake Store, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="785b3-131">The snippet below also requires inputs like Azure AD domain name, client ID for an Azure AD app, etc. All these details can be retrieved from an Azure AD application that you must created, the details of which are also included in link above.</span><span class="sxs-lookup"><span data-stu-id="785b3-131">The snippet below also requires inputs like Azure AD domain name, client ID for an Azure AD app, etc. All these details can be retrieved from an Azure AD application that you must created, the details of which are also included in link above.</span></span>

 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-the-data-lake-store-clients"></a><span data-ttu-id="785b3-132">Create the Data Lake Store Clients</span><span class="sxs-lookup"><span data-stu-id="785b3-132">Create the Data Lake Store Clients</span></span>
```javascript
var adlsManagement = require("azure-arm-datalake-store");
var acccountClient = new adlsManagement.DataLakeStoreAccountClient(credentials, "your-subscription-id");
var filesystemClient = new adlsManagement.DataLakeStoreFileSystemClient(credentials);
```

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="785b3-133">Create a Data Lake Store Account</span><span class="sxs-lookup"><span data-stu-id="785b3-133">Create a Data Lake Store Account</span></span>
```javascript
var util = require('util');
var resourceGroupName = 'testrg';
var accountName = 'testadlsacct';
var location = 'eastus2';

// account object to create
var accountToCreate = {
  tags: {
    testtag1: 'testvalue1',
    testtag2: 'testvalue2'
  },
  name: accountName,
  location: location
};

client.account.create(resourceGroupName, accountName, accountToCreate, function (err, result, request, response) {
  if (err) {
    console.log(err);
    /*err has reference to the actual request and response, so you can see what was sent and received on the wire.
      The structure of err looks like this:
      err: {
        code: 'Error Code',
        message: 'Error Message',
        body: 'The response body if any',
        request: reference to a stripped version of http request
        response: reference to a stripped version of the response
      }
    */
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="create-a-file-with-content"></a><span data-ttu-id="785b3-134">Create a file with content</span><span class="sxs-lookup"><span data-stu-id="785b3-134">Create a file with content</span></span>
```javascript
var util = require('util');
var accountName = 'testadlsacct';
var fileToCreate = '/myfolder/myfile.txt';
var options = {
  streamContents: new Buffer('some string content')
}

filesystemClient.fileSystem.listFileStatus(accountName, fileToCreate, options, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    // no result is returned, only a 201 response for success.
    console.log('response is: ' + util.inspect(response, {depth: null}));
  }
});
```

## <a name="get-a-list-of-files-and-folders"></a><span data-ttu-id="785b3-135">Get a list of files and folders</span><span class="sxs-lookup"><span data-stu-id="785b3-135">Get a list of files and folders</span></span>
```javascript
var util = require('util');
var accountName = 'testadlsacct';
var pathToEnumerate = '/myfolder';
filesystemClient.fileSystem.listFileStatus(accountName, pathToEnumerate, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="see-also"></a><span data-ttu-id="785b3-136">See also</span><span class="sxs-lookup"><span data-stu-id="785b3-136">See also</span></span>
* [<span data-ttu-id="785b3-137">Microsoft Azure SDK for Node.js</span><span class="sxs-lookup"><span data-stu-id="785b3-137">Microsoft Azure SDK for Node.js</span></span>](https://github.com/azure/azure-sdk-for-node)
* [<span data-ttu-id="785b3-138">Microsoft Azure SDK for Node.js - Data Lake Analytics Management</span><span class="sxs-lookup"><span data-stu-id="785b3-138">Microsoft Azure SDK for Node.js - Data Lake Analytics Management</span></span>](https://www.npmjs.com/package/azure-arm-datalake-analytics)

