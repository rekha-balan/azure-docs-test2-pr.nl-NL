---
title: Manage Azure Data Lake Analytics using Python
description: This article describes how to use Python to manage Data Lake Analytics accounts, data sources, users, & jobs.
services: data-lake-analytics
ms.service: data-lake-analytics
author: matt1883
ms.author: saveenr
ms.reviewer: jasonwhowell
ms.assetid: d4213a19-4d0f-49c9-871c-9cd6ed7cf731
ms.topic: conceptual
ms.date: 06/08/2018
ms.openlocfilehash: f73ef118efbdfc94d8cb9b7d81717bd13511c785
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870287"
---
# <a name="manage-azure-data-lake-analytics-using-python"></a><span data-ttu-id="67894-103">Manage Azure Data Lake Analytics using Python</span><span class="sxs-lookup"><span data-stu-id="67894-103">Manage Azure Data Lake Analytics using Python</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="67894-104">This article describes how to manage Azure Data Lake Analytics accounts, data sources, users, and jobs by using Python.</span><span class="sxs-lookup"><span data-stu-id="67894-104">This article describes how to manage Azure Data Lake Analytics accounts, data sources, users, and jobs by using Python.</span></span>

## <a name="supported-python-versions"></a><span data-ttu-id="67894-105">Supported Python versions</span><span class="sxs-lookup"><span data-stu-id="67894-105">Supported Python versions</span></span>

* <span data-ttu-id="67894-106">Use a 64-bit version of Python.</span><span class="sxs-lookup"><span data-stu-id="67894-106">Use a 64-bit version of Python.</span></span>
* <span data-ttu-id="67894-107">You can use the standard Python distribution found at **[Python.org downloads](https://www.python.org/downloads/)**.</span><span class="sxs-lookup"><span data-stu-id="67894-107">You can use the standard Python distribution found at **[Python.org downloads](https://www.python.org/downloads/)**.</span></span> 
* <span data-ttu-id="67894-108">Many developers find it convenient to use the **[Anaconda Python distribution](https://www.anaconda.com/download/)**.</span><span class="sxs-lookup"><span data-stu-id="67894-108">Many developers find it convenient to use the **[Anaconda Python distribution](https://www.anaconda.com/download/)**.</span></span>  
* <span data-ttu-id="67894-109">This article was written using Python version 3.6 from the standard Python distribution</span><span class="sxs-lookup"><span data-stu-id="67894-109">This article was written using Python version 3.6 from the standard Python distribution</span></span>

## <a name="install-azure-python-sdk"></a><span data-ttu-id="67894-110">Install Azure Python SDK</span><span class="sxs-lookup"><span data-stu-id="67894-110">Install Azure Python SDK</span></span>

<span data-ttu-id="67894-111">Install the following modules:</span><span class="sxs-lookup"><span data-stu-id="67894-111">Install the following modules:</span></span>

* <span data-ttu-id="67894-112">The **azure-mgmt-resource** module includes other Azure modules for Active Directory, etc.</span><span class="sxs-lookup"><span data-stu-id="67894-112">The **azure-mgmt-resource** module includes other Azure modules for Active Directory, etc.</span></span>
* <span data-ttu-id="67894-113">The **azure-datalake-store** module includes the Azure Data Lake Store filesystem operations.</span><span class="sxs-lookup"><span data-stu-id="67894-113">The **azure-datalake-store** module includes the Azure Data Lake Store filesystem operations.</span></span> 
* <span data-ttu-id="67894-114">The **azure-mgmt-datalake-store** module includes the Azure Data Lake Store account management operations.</span><span class="sxs-lookup"><span data-stu-id="67894-114">The **azure-mgmt-datalake-store** module includes the Azure Data Lake Store account management operations.</span></span>
* <span data-ttu-id="67894-115">The **azure-mgmt-datalake-analytics** module includes the Azure Data Lake Analytics operations.</span><span class="sxs-lookup"><span data-stu-id="67894-115">The **azure-mgmt-datalake-analytics** module includes the Azure Data Lake Analytics operations.</span></span> 

<span data-ttu-id="67894-116">First, ensure you have the latest `pip` by running the following command:</span><span class="sxs-lookup"><span data-stu-id="67894-116">First, ensure you have the latest `pip` by running the following command:</span></span>

```
python -m pip install --upgrade pip
```

<span data-ttu-id="67894-117">This document was written using `pip version 9.0.1`.</span><span class="sxs-lookup"><span data-stu-id="67894-117">This document was written using `pip version 9.0.1`.</span></span>

<span data-ttu-id="67894-118">Use the following `pip` commands to install the modules from the commandline:</span><span class="sxs-lookup"><span data-stu-id="67894-118">Use the following `pip` commands to install the modules from the commandline:</span></span>

```
pip install azure-mgmt-resource
pip install azure-datalake-store
pip install azure-mgmt-datalake-store
pip install azure-mgmt-datalake-analytics
```

## <a name="create-a-new-python-script"></a><span data-ttu-id="67894-119">Create a new Python script</span><span class="sxs-lookup"><span data-stu-id="67894-119">Create a new Python script</span></span>

<span data-ttu-id="67894-120">Paste the following code into the script:</span><span class="sxs-lookup"><span data-stu-id="67894-120">Paste the following code into the script:</span></span>

```python
## Use this only for Azure AD service-to-service authentication
#from azure.common.credentials import ServicePrincipalCredentials

## Use this only for Azure AD end-user authentication
#from azure.common.credentials import UserPassCredentials

## Required for Azure Resource Manager
from azure.mgmt.resource.resources import ResourceManagementClient
from azure.mgmt.resource.resources.models import ResourceGroup

## Required for Azure Data Lake Store account management
from azure.mgmt.datalake.store import DataLakeStoreAccountManagementClient
from azure.mgmt.datalake.store.models import DataLakeStoreAccount

## Required for Azure Data Lake Store filesystem management
from azure.datalake.store import core, lib, multithread

## Required for Azure Data Lake Analytics account management
from azure.mgmt.datalake.analytics.account import DataLakeAnalyticsAccountManagementClient
from azure.mgmt.datalake.analytics.account.models import DataLakeAnalyticsAccount, DataLakeStoreAccountInfo

## Required for Azure Data Lake Analytics job management
from azure.mgmt.datalake.analytics.job import DataLakeAnalyticsJobManagementClient
from azure.mgmt.datalake.analytics.job.models import JobInformation, JobState, USqlJobProperties

## Required for Azure Data Lake Analytics catalog management
from azure.mgmt.datalake.analytics.catalog import DataLakeAnalyticsCatalogManagementClient

## Use these as needed for your application
import logging, getpass, pprint, uuid, time
```

<span data-ttu-id="67894-121">Run this script to verify that the modules can be imported.</span><span class="sxs-lookup"><span data-stu-id="67894-121">Run this script to verify that the modules can be imported.</span></span>

## <a name="authentication"></a><span data-ttu-id="67894-122">Authentication</span><span class="sxs-lookup"><span data-stu-id="67894-122">Authentication</span></span>

### <a name="interactive-user-authentication-with-a-pop-up"></a><span data-ttu-id="67894-123">Interactive user authentication with a pop-up</span><span class="sxs-lookup"><span data-stu-id="67894-123">Interactive user authentication with a pop-up</span></span>

<span data-ttu-id="67894-124">This method is not supported.</span><span class="sxs-lookup"><span data-stu-id="67894-124">This method is not supported.</span></span>

### <a name="interactive-user-authentication-with-a-device-code"></a><span data-ttu-id="67894-125">Interactive user authentication with a device code</span><span class="sxs-lookup"><span data-stu-id="67894-125">Interactive user authentication with a device code</span></span>

```python
user = input('Enter the user to authenticate with that has permission to subscription: ')
password = getpass.getpass()
credentials = UserPassCredentials(user, password)
```

### <a name="noninteractive-authentication-with-spi-and-a-secret"></a><span data-ttu-id="67894-126">Noninteractive authentication with SPI and a secret</span><span class="sxs-lookup"><span data-stu-id="67894-126">Noninteractive authentication with SPI and a secret</span></span>

```python
credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')
```

### <a name="noninteractive-authentication-with-api-and-a-certificate"></a><span data-ttu-id="67894-127">Noninteractive authentication with API and a certificate</span><span class="sxs-lookup"><span data-stu-id="67894-127">Noninteractive authentication with API and a certificate</span></span>

<span data-ttu-id="67894-128">This method is not supported.</span><span class="sxs-lookup"><span data-stu-id="67894-128">This method is not supported.</span></span>

## <a name="common-script-variables"></a><span data-ttu-id="67894-129">Common script variables</span><span class="sxs-lookup"><span data-stu-id="67894-129">Common script variables</span></span>

<span data-ttu-id="67894-130">These variables are used in the samples.</span><span class="sxs-lookup"><span data-stu-id="67894-130">These variables are used in the samples.</span></span>

```python
subid= '<Azure Subscription ID>'
rg = '<Azure Resource Group Name>'
location = '<Location>' # i.e. 'eastus2'
adls = '<Azure Data Lake Store Account Name>'
adla = '<Azure Data Lake Analytics Account Name>'
```

## <a name="create-the-clients"></a><span data-ttu-id="67894-131">Create the clients</span><span class="sxs-lookup"><span data-stu-id="67894-131">Create the clients</span></span>

```python
resourceClient = ResourceManagementClient(credentials, subid)
adlaAcctClient = DataLakeAnalyticsAccountManagementClient(credentials, subid)
adlaJobClient = DataLakeAnalyticsJobManagementClient( credentials, 'azuredatalakeanalytics.net')
```

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="67894-132">Create an Azure Resource Group</span><span class="sxs-lookup"><span data-stu-id="67894-132">Create an Azure Resource Group</span></span>

```python
armGroupResult = resourceClient.resource_groups.create_or_update( rg, ResourceGroup( location=location ) )
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="67894-133">Create Data Lake Analytics account</span><span class="sxs-lookup"><span data-stu-id="67894-133">Create Data Lake Analytics account</span></span>

<span data-ttu-id="67894-134">First create a store account.</span><span class="sxs-lookup"><span data-stu-id="67894-134">First create a store account.</span></span>

```python
adlsAcctResult = adlsAcctClient.account.create(
    rg,
    adls,
    DataLakeStoreAccount(
        location=location)
    )
).wait()
```
<span data-ttu-id="67894-135">Then create an ADLA account that uses that store.</span><span class="sxs-lookup"><span data-stu-id="67894-135">Then create an ADLA account that uses that store.</span></span>

```python
adlaAcctResult = adlaAcctClient.account.create(
    rg,
    adla,
    DataLakeAnalyticsAccount(
        location=location,
        default_data_lake_store_account=adls,
        data_lake_store_accounts=[DataLakeStoreAccountInfo(name=adls)]
    )
).wait()
```

## <a name="submit-a-job"></a><span data-ttu-id="67894-136">Submit a job</span><span class="sxs-lookup"><span data-stu-id="67894-136">Submit a job</span></span>

```python
script = """
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    TO "/data.csv"
    USING Outputters.Csv();
"""

jobId = str(uuid.uuid4())
jobResult = adlaJobClient.job.create(
    adla,
    jobId,
    JobInformation(
        name='Sample Job',
        type='USql',
        properties=USqlJobProperties(script=script)
    )
)
```

## <a name="wait-for-a-job-to-end"></a><span data-ttu-id="67894-137">Wait for a job to end</span><span class="sxs-lookup"><span data-stu-id="67894-137">Wait for a job to end</span></span>

```python
jobResult = adlaJobClient.job.get(adla, jobId)
while(jobResult.state != JobState.ended):
    print('Job is not yet done, waiting for 3 seconds. Current state: ' + jobResult.state.value)
    time.sleep(3)
    jobResult = adlaJobClient.job.get(adla, jobId)

print ('Job finished with result: ' + jobResult.result.value)
```

## <a name="list-pipelines-and-recurrences"></a><span data-ttu-id="67894-138">List pipelines and recurrences</span><span class="sxs-lookup"><span data-stu-id="67894-138">List pipelines and recurrences</span></span>
<span data-ttu-id="67894-139">Depending whether your jobs have pipeline or recurrence metadata attached, you can list pipelines and recurrences.</span><span class="sxs-lookup"><span data-stu-id="67894-139">Depending whether your jobs have pipeline or recurrence metadata attached, you can list pipelines and recurrences.</span></span>

```python
pipelines = adlaJobClient.pipeline.list(adla)
for p in pipelines:
    print('Pipeline: ' + p.name + ' ' + p.pipelineId)

recurrences = adlaJobClient.recurrence.list(adla)
for r in recurrences:
    print('Recurrence: ' + r.name + ' ' + r.recurrenceId)
```

## <a name="manage-compute-policies"></a><span data-ttu-id="67894-140">Manage compute policies</span><span class="sxs-lookup"><span data-stu-id="67894-140">Manage compute policies</span></span>

<span data-ttu-id="67894-141">The DataLakeAnalyticsAccountManagementClient object provides methods for managing the compute policies for a Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="67894-141">The DataLakeAnalyticsAccountManagementClient object provides methods for managing the compute policies for a Data Lake Analytics account.</span></span>

### <a name="list-compute-policies"></a><span data-ttu-id="67894-142">List compute policies</span><span class="sxs-lookup"><span data-stu-id="67894-142">List compute policies</span></span>

<span data-ttu-id="67894-143">The following code retrieves a list of compute policies for a Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="67894-143">The following code retrieves a list of compute policies for a Data Lake Analytics account.</span></span>

```python
policies = adlaAccountClient.computePolicies.listByAccount(rg, adla)
for p in policies:
    print('Name: ' + p.name + 'Type: ' + p.objectType + 'Max AUs / job: ' + p.maxDegreeOfParallelismPerJob + 'Min priority / job: ' + p.minPriorityPerJob)
```

### <a name="create-a-new-compute-policy"></a><span data-ttu-id="67894-144">Create a new compute policy</span><span class="sxs-lookup"><span data-stu-id="67894-144">Create a new compute policy</span></span>

<span data-ttu-id="67894-145">The following code creates a new compute policy for a Data Lake Analytics account, setting the maximum AUs available to the specified user to 50, and the minimum job priority to 250.</span><span class="sxs-lookup"><span data-stu-id="67894-145">The following code creates a new compute policy for a Data Lake Analytics account, setting the maximum AUs available to the specified user to 50, and the minimum job priority to 250.</span></span>

```python
userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde"
newPolicyParams = ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250)
adlaAccountClient.computePolicies.createOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams)
```

## <a name="next-steps"></a><span data-ttu-id="67894-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="67894-146">Next steps</span></span>

- <span data-ttu-id="67894-147">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span><span class="sxs-lookup"><span data-stu-id="67894-147">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span></span>
- <span data-ttu-id="67894-148">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="67894-148">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
- <span data-ttu-id="67894-149">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="67894-149">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>

