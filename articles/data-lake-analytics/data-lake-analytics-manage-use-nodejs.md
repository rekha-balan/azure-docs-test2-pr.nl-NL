---
title: Manage Azure Data Lake Analytics using Azure SDK for Node.js
description: This article describes how to use the Azure SDK for Node.js to manage Data Lake Analytics accounts, data sources, jobs & users.
services: data-lake-analytics
ms.service: data-lake-analytics
author: saveenr
ms.author: saveenr
ms.reviewer: jasonwhowell
ms.assetid: 9de1bcf4-b15b-4d0b-9284-8889ecf0c438
ms.topic: conceptual
ms.date: 12/05/2016
ms.openlocfilehash: 0603a60ea73d47dd6107ee80afc5c776ff8c83bc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44824114"
---
# <a name="manage-azure-data-lake-analytics-using-azure-sdk-for-nodejs"></a><span data-ttu-id="9fbf4-103">Manage Azure Data Lake Analytics using Azure SDK for Node.js</span><span class="sxs-lookup"><span data-stu-id="9fbf4-103">Manage Azure Data Lake Analytics using Azure SDK for Node.js</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="9fbf4-104">This article describes how to manage Azure Data Lake Analytics accounts, data sources, users, and jobs using an app written using the Azure SDK for Node.js.</span><span class="sxs-lookup"><span data-stu-id="9fbf4-104">This article describes how to manage Azure Data Lake Analytics accounts, data sources, users, and jobs using an app written using the Azure SDK for Node.js.</span></span> 

<span data-ttu-id="9fbf4-105">The following versions are supported:</span><span class="sxs-lookup"><span data-stu-id="9fbf4-105">The following versions are supported:</span></span>
* <span data-ttu-id="9fbf4-106">**Node.js version: 0.10.0 or higher**</span><span class="sxs-lookup"><span data-stu-id="9fbf4-106">**Node.js version: 0.10.0 or higher**</span></span>
* <span data-ttu-id="9fbf4-107">**REST API version for Account: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="9fbf4-107">**REST API version for Account: 2015-10-01-preview**</span></span>
* <span data-ttu-id="9fbf4-108">**REST API version for Catalog: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="9fbf4-108">**REST API version for Catalog: 2015-10-01-preview**</span></span>
* <span data-ttu-id="9fbf4-109">**REST API version for Job: 2016-03-20-preview**</span><span class="sxs-lookup"><span data-stu-id="9fbf4-109">**REST API version for Job: 2016-03-20-preview**</span></span>

## <a name="features"></a><span data-ttu-id="9fbf4-110">Features</span><span class="sxs-lookup"><span data-stu-id="9fbf4-110">Features</span></span>
* <span data-ttu-id="9fbf4-111">Account management: create, get, list, update, and delete.</span><span class="sxs-lookup"><span data-stu-id="9fbf4-111">Account management: create, get, list, update, and delete.</span></span>
* <span data-ttu-id="9fbf4-112">Job management: submit, get, list, and cancel.</span><span class="sxs-lookup"><span data-stu-id="9fbf4-112">Job management: submit, get, list, and cancel.</span></span>
* <span data-ttu-id="9fbf4-113">Catalog management: get and list.</span><span class="sxs-lookup"><span data-stu-id="9fbf4-113">Catalog management: get and list.</span></span>

## <a name="how-to-install"></a><span data-ttu-id="9fbf4-114">How to Install</span><span class="sxs-lookup"><span data-stu-id="9fbf4-114">How to Install</span></span>
```bash
npm install azure-arm-datalake-analytics
```

## <a name="authenticate-using-azure-active-directory"></a><span data-ttu-id="9fbf4-115">Authenticate using Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9fbf4-115">Authenticate using Azure Active Directory</span></span>
 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-the-data-lake-analytics-client"></a><span data-ttu-id="9fbf4-116">Create the Data Lake Analytics client</span><span class="sxs-lookup"><span data-stu-id="9fbf4-116">Create the Data Lake Analytics client</span></span>
```javascript
var adlaManagement = require("azure-arm-datalake-analytics");
var acccountClient = new adlaManagement.DataLakeAnalyticsAccountClient(credentials, 'your-subscription-id');
var jobClient = new adlaManagement.DataLakeAnalyticsJobClient(credentials, 'azuredatalakeanalytics.net');
var catalogClient = new adlaManagement.DataLakeAnalyticsCatalogClient(credentials, 'azuredatalakeanalytics.net');
```

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="9fbf4-117">Create a Data Lake Analytics account</span><span class="sxs-lookup"><span data-stu-id="9fbf4-117">Create a Data Lake Analytics account</span></span>
```javascript
var util = require('util');
var resourceGroupName = 'testrg';
var accountName = 'testadlaacct';
var location = 'eastus2';

// A Data Lake Store account must already have been created to create
// a Data Lake Analytics account. See the Data Lake Store readme for
// information on doing so. For now, we assume one exists already.
var datalakeStoreAccountName = 'existingadlsaccount';

// account object to create
var accountToCreate = {
  tags: {
    testtag1: 'testvalue1',
    testtag2: 'testvalue2'
  },
  name: accountName,
  location: location,
  properties: {
    defaultDataLakeStoreAccount: datalakeStoreAccountName,
    dataLakeStoreAccounts: [
      {
        name: datalakeStoreAccountName
      }
    ]
  }
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

## <a name="get-a-list-of-jobs"></a><span data-ttu-id="9fbf4-118">Get a list of jobs</span><span class="sxs-lookup"><span data-stu-id="9fbf4-118">Get a list of jobs</span></span>
```javascript
var util = require('util');
var accountName = 'testadlaacct';
jobClient.job.list(accountName, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="get-a-list-of-databases-in-the-data-lake-analytics-catalog"></a><span data-ttu-id="9fbf4-119">Get a list of databases in the Data Lake Analytics Catalog</span><span class="sxs-lookup"><span data-stu-id="9fbf4-119">Get a list of databases in the Data Lake Analytics Catalog</span></span>
```javascript
var util = require('util');
var accountName = 'testadlaacct';
catalogClient.catalog.listDatabases(accountName, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="see-also"></a><span data-ttu-id="9fbf4-120">See also</span><span class="sxs-lookup"><span data-stu-id="9fbf4-120">See also</span></span>
* [<span data-ttu-id="9fbf4-121">Microsoft Azure SDK for Node.js</span><span class="sxs-lookup"><span data-stu-id="9fbf4-121">Microsoft Azure SDK for Node.js</span></span>](https://github.com/azure/azure-sdk-for-node)
* [<span data-ttu-id="9fbf4-122">Microsoft Azure SDK for Node.js - Data Lake Store Management</span><span class="sxs-lookup"><span data-stu-id="9fbf4-122">Microsoft Azure SDK for Node.js - Data Lake Store Management</span></span>](https://github.com/Azure/azure-sdk-for-node/tree/autorest/lib/services/dataLake.Store)

