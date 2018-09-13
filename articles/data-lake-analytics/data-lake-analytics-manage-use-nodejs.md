---
title: Manage Azure Data Lake Analytics using Azure SDK for Node.js | Microsoft Docs
description: Learn how to manage Data Lake Analytics accounts, data sources, jobs and users using Azure SDK for Node.js
services: data-lake-analytics
documentationcenter: ''
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 9de1bcf4-b15b-4d0b-9284-8889ecf0c438
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: e6440522ced33a48925cfabc64da055b8700b253
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662268"
---
# <a name="manage-azure-data-lake-analytics-using-azure-sdk-for-nodejs"></a><span data-ttu-id="d975b-103">Manage Azure Data Lake Analytics using Azure SDK for Node.js</span><span class="sxs-lookup"><span data-stu-id="d975b-103">Manage Azure Data Lake Analytics using Azure SDK for Node.js</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="d975b-104">The Azure SDK for Node.js can be used for managing Azure Data Lake Analytics accounts, jobs and catalogs.</span><span class="sxs-lookup"><span data-stu-id="d975b-104">The Azure SDK for Node.js can be used for managing Azure Data Lake Analytics accounts, jobs and catalogs.</span></span> <span data-ttu-id="d975b-105">To see management topic using other tools, click the tab select above.</span><span class="sxs-lookup"><span data-stu-id="d975b-105">To see management topic using other tools, click the tab select above.</span></span>

<span data-ttu-id="d975b-106">Right now it supports:</span><span class="sxs-lookup"><span data-stu-id="d975b-106">Right now it supports:</span></span>

* <span data-ttu-id="d975b-107">**Node.js version: 0.10.0 or higher**</span><span class="sxs-lookup"><span data-stu-id="d975b-107">**Node.js version: 0.10.0 or higher**</span></span>
* <span data-ttu-id="d975b-108">**REST API version for Account: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="d975b-108">**REST API version for Account: 2015-10-01-preview**</span></span>
* <span data-ttu-id="d975b-109">**REST API version for Catalog: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="d975b-109">**REST API version for Catalog: 2015-10-01-preview**</span></span>
* <span data-ttu-id="d975b-110">**REST API version for Job: 2016-03-20-preview**</span><span class="sxs-lookup"><span data-stu-id="d975b-110">**REST API version for Job: 2016-03-20-preview**</span></span>

## <a name="features"></a><span data-ttu-id="d975b-111">Features</span><span class="sxs-lookup"><span data-stu-id="d975b-111">Features</span></span>
* <span data-ttu-id="d975b-112">Account management: create, get, list, update, and delete.</span><span class="sxs-lookup"><span data-stu-id="d975b-112">Account management: create, get, list, update, and delete.</span></span>
* <span data-ttu-id="d975b-113">Job management: submit, get, list, cancel.</span><span class="sxs-lookup"><span data-stu-id="d975b-113">Job management: submit, get, list, cancel.</span></span>
* <span data-ttu-id="d975b-114">Catalog management: get, list, create (secrets), update (secrets), delete (secrets).</span><span class="sxs-lookup"><span data-stu-id="d975b-114">Catalog management: get, list, create (secrets), update (secrets), delete (secrets).</span></span>

## <a name="how-to-install"></a><span data-ttu-id="d975b-115">How to Install</span><span class="sxs-lookup"><span data-stu-id="d975b-115">How to Install</span></span>
```bash
npm install azure-arm-datalake-analytics
```

## <a name="authenticate-using-azure-active-directory"></a><span data-ttu-id="d975b-116">Authenticate using Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d975b-116">Authenticate using Azure Active Directory</span></span>
 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-the-data-lake-analytics-client"></a><span data-ttu-id="d975b-117">Create the Data Lake Analytics client</span><span class="sxs-lookup"><span data-stu-id="d975b-117">Create the Data Lake Analytics client</span></span>
```javascript
var adlaManagement = require("azure-arm-datalake-analytics");
var acccountClient = new adlaManagement.DataLakeAnalyticsAccountClient(credentials, 'your-subscription-id');
var jobClient = new adlaManagement.DataLakeAnalyticsJobClient(credentials, 'azuredatalakeanalytics.net');
var catalogClient = new adlaManagement.DataLakeAnalyticsCatalogClient(credentials, 'azuredatalakeanalytics.net');
```

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="d975b-118">Create a Data Lake Analytics account</span><span class="sxs-lookup"><span data-stu-id="d975b-118">Create a Data Lake Analytics account</span></span>
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

## <a name="get-a-list-of-jobs"></a><span data-ttu-id="d975b-119">Get a list of jobs</span><span class="sxs-lookup"><span data-stu-id="d975b-119">Get a list of jobs</span></span>
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

## <a name="get-a-list-of-databases-in-the-data-lake-analytics-catalog"></a><span data-ttu-id="d975b-120">Get a list of databases in the Data Lake Analytics Catalog</span><span class="sxs-lookup"><span data-stu-id="d975b-120">Get a list of databases in the Data Lake Analytics Catalog</span></span>
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

## <a name="see-also"></a><span data-ttu-id="d975b-121">See also</span><span class="sxs-lookup"><span data-stu-id="d975b-121">See also</span></span>
* [<span data-ttu-id="d975b-122">Microsoft Azure SDK for Node.js</span><span class="sxs-lookup"><span data-stu-id="d975b-122">Microsoft Azure SDK for Node.js</span></span>](https://github.com/azure/azure-sdk-for-node)
* [<span data-ttu-id="d975b-123">Microsoft Azure SDK for Node.js - Data Lake Store Management</span><span class="sxs-lookup"><span data-stu-id="d975b-123">Microsoft Azure SDK for Node.js - Data Lake Store Management</span></span>](https://github.com/Azure/azure-sdk-for-node/tree/autorest/lib/services/dataLake.Store)

