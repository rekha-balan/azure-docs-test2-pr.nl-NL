---
title: Get started with Azure Data Lake Analytics using Python | Microsoft Docs
description: 'Learn how to use Python to create a Data Lake Store account, and submit jobs. '
services: data-lake-analytics
documentationcenter: ''
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/15/2016
ms.author: jgao
ms.openlocfilehash: 242df1dbb398c041c41c38e4e691915af3022dd8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553694"
---
# <a name="tutorial-get-started-with-azure-data-lake-analytics-using-python"></a><span data-ttu-id="67c26-103">Tutorial: get started with Azure Data Lake Analytics using Python</span><span class="sxs-lookup"><span data-stu-id="67c26-103">Tutorial: get started with Azure Data Lake Analytics using Python</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="67c26-104">Learn how to use Python to create Azure Data Lake Analytics accounts, define Data Lake Analytics jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs to Data Lake Analytic accounts.</span><span class="sxs-lookup"><span data-stu-id="67c26-104">Learn how to use Python to create Azure Data Lake Analytics accounts, define Data Lake Analytics jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs to Data Lake Analytic accounts.</span></span> <span data-ttu-id="67c26-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="67c26-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

<span data-ttu-id="67c26-106">In this tutorial, you develop a job that reads a tab separated values (TSV) file and converts it into a comma-separated-values (CSV) file.</span><span class="sxs-lookup"><span data-stu-id="67c26-106">In this tutorial, you develop a job that reads a tab separated values (TSV) file and converts it into a comma-separated-values (CSV) file.</span></span> <span data-ttu-id="67c26-107">To go through the same tutorial using other supported tools, click the tabs on the top of this section.</span><span class="sxs-lookup"><span data-stu-id="67c26-107">To go through the same tutorial using other supported tools, click the tabs on the top of this section.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="67c26-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="67c26-108">Prerequisites</span></span>

<span data-ttu-id="67c26-109">Before you begin this tutorial, you must have the following items:</span><span class="sxs-lookup"><span data-stu-id="67c26-109">Before you begin this tutorial, you must have the following items:</span></span>

- <span data-ttu-id="67c26-110">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="67c26-110">**An Azure subscription**.</span></span> <span data-ttu-id="67c26-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="67c26-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="67c26-112">**An Azure Active Directory Application**.</span><span class="sxs-lookup"><span data-stu-id="67c26-112">**An Azure Active Directory Application**.</span></span> <span data-ttu-id="67c26-113">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67c26-113">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="67c26-114">There are different approaches to authenticate with Azure AD, which are end-user authentication or service-to-service authentication.</span><span class="sxs-lookup"><span data-stu-id="67c26-114">There are different approaches to authenticate with Azure AD, which are end-user authentication or service-to-service authentication.</span></span> <span data-ttu-id="67c26-115">For instructions and more information on how to authenticate, see [Authenticate with Data Lake Store using Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="67c26-115">For instructions and more information on how to authenticate, see [Authenticate with Data Lake Store using Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span>
- <span data-ttu-id="67c26-116">**[Python](https://www.python.org/downloads/)**.</span><span class="sxs-lookup"><span data-stu-id="67c26-116">**[Python](https://www.python.org/downloads/)**.</span></span> <span data-ttu-id="67c26-117">You must use the 64-bit version.</span><span class="sxs-lookup"><span data-stu-id="67c26-117">You must use the 64-bit version.</span></span> <span data-ttu-id="67c26-118">This article uses Python version 3.5.2.</span><span class="sxs-lookup"><span data-stu-id="67c26-118">This article uses Python version 3.5.2.</span></span>


## <a name="install-azure-python-sdk"></a><span data-ttu-id="67c26-119">Install Azure Python SDK</span><span class="sxs-lookup"><span data-stu-id="67c26-119">Install Azure Python SDK</span></span>

<span data-ttu-id="67c26-120">To work with Data Lake Store using Python, you need to install three modules.</span><span class="sxs-lookup"><span data-stu-id="67c26-120">To work with Data Lake Store using Python, you need to install three modules.</span></span>

<span data-ttu-id="67c26-121">The azure-mgmt-datalake-store module includes the Azure Data Lake Store account management operations.</span><span class="sxs-lookup"><span data-stu-id="67c26-121">The azure-mgmt-datalake-store module includes the Azure Data Lake Store account management operations.</span></span> <span data-ttu-id="67c26-122">The azure-mgmt-resource module includes other Azure modules for Active Directory, etc. The azure-datalake-store module includes the Azure Data Lake Store filesystem operations.</span><span class="sxs-lookup"><span data-stu-id="67c26-122">The azure-mgmt-resource module includes other Azure modules for Active Directory, etc. The azure-datalake-store module includes the Azure Data Lake Store filesystem operations.</span></span> <span data-ttu-id="67c26-123">The azure-datalake-analytics module includes the Azure Data Lake Analytics operations.</span><span class="sxs-lookup"><span data-stu-id="67c26-123">The azure-datalake-analytics module includes the Azure Data Lake Analytics operations.</span></span> <span data-ttu-id="67c26-124">Use the following commands to install the modules.</span><span class="sxs-lookup"><span data-stu-id="67c26-124">Use the following commands to install the modules.</span></span>

    pip install azure-mgmt-resource
    pip install azure-mgmt-datalake-store
    pip install azure-mgmt-datalake-analytics
    pip install azure-datalake-store

## <a name="create-a-python-application"></a><span data-ttu-id="67c26-125">Create a Python application</span><span class="sxs-lookup"><span data-stu-id="67c26-125">Create a Python application</span></span>

1. <span data-ttu-id="67c26-126">Use the IDE of your choice to create a new Python application, for example, mysample.py.</span><span class="sxs-lookup"><span data-stu-id="67c26-126">Use the IDE of your choice to create a new Python application, for example, mysample.py.</span></span>

2. <span data-ttu-id="67c26-127">Add the following lines to import the required modules</span><span class="sxs-lookup"><span data-stu-id="67c26-127">Add the following lines to import the required modules</span></span>

        ## Use this only for Azure AD service-to-service authentication
        from azure.common.credentials import ServicePrincipalCredentials

        ## Use this only for Azure AD end-user authentication
        from azure.common.credentials import UserPassCredentials

        ## Required for Azure Resource Manager
        from azure.mgmt.resource.resources import ResourceManagementClient
        from azure.mgmt.resource.resources.models import ResourceGroup

        ## Required for Azure Data Lake Store account management
        from azure.mgmt.datalake.store import DataLakeStoreAccountManagementClient
        from azure.mgmt.datalake.store.models import DataLakeStoreAccount

        ## Required for Azure Data Lake Store filesystem management
        from azure.datalake.store import core, lib, multithread

        ## Required for Azure Data Lake Analytics account management
        from azure.mgmt.datalake.analytics.account.models import DataLakeAnalyticsAccount, DataLakeAnalyticsAccountProperties, DataLakeStoreAccountInfo

        ## Required for Azure Data Lake Analytics job management
        from azure.mgmt.datalake.analytics.job import DataLakeAnalyticsJobManagementClient
        from azure.mgmt.datalake.analytics.job.models import JobInformation, JobState, USqlJobProperties

        ## Required for Azure Data Lake Analytics catalog management
        from azure.mgmt.datalake.analytics.catalog import DataLakeAnalyticsCatalogManagementClient

        ## Use these as needed for your application
        import logging, getpass, pprint, uuid, time

3. <span data-ttu-id="67c26-128">Save changes to the Python application file.</span><span class="sxs-lookup"><span data-stu-id="67c26-128">Save changes to the Python application file.</span></span>

## <a name="authentication"></a><span data-ttu-id="67c26-129">Authentication</span><span class="sxs-lookup"><span data-stu-id="67c26-129">Authentication</span></span>

<span data-ttu-id="67c26-130">Use one of the following methods to authenticate:</span><span class="sxs-lookup"><span data-stu-id="67c26-130">Use one of the following methods to authenticate:</span></span>

### <a name="end-user-authentication-for-account-management"></a><span data-ttu-id="67c26-131">End-user authentication for account management</span><span class="sxs-lookup"><span data-stu-id="67c26-131">End-user authentication for account management</span></span>

<span data-ttu-id="67c26-132">Use this method to authenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span><span class="sxs-lookup"><span data-stu-id="67c26-132">Use this method to authenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="67c26-133">You must provide username and password for an Azure AD user.</span><span class="sxs-lookup"><span data-stu-id="67c26-133">You must provide username and password for an Azure AD user.</span></span> <span data-ttu-id="67c26-134">The user account cannot be configured for multi-factor authentication, and the account can't be a Microsoft account / Live ID, for example, @outlook.com, and @live.com.</span><span class="sxs-lookup"><span data-stu-id="67c26-134">The user account cannot be configured for multi-factor authentication, and the account can't be a Microsoft account / Live ID, for example, @outlook.com, and @live.com.</span></span>

    user = input('Enter the user to authenticate with that has permission to subscription: ')
    password = getpass.getpass()

    credentials = UserPassCredentials(user, password)

### <a name="service-to-service-authentication-with-client-secret-for-account-management"></a><span data-ttu-id="67c26-135">Service-to-service authentication with client secret for account management</span><span class="sxs-lookup"><span data-stu-id="67c26-135">Service-to-service authentication with client secret for account management</span></span>

<span data-ttu-id="67c26-136">Use this method to authenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span><span class="sxs-lookup"><span data-stu-id="67c26-136">Use this method to authenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="67c26-137">The following snippet can be used to authenticate your application non-interactively, using the client secret for an application / service principal.</span><span class="sxs-lookup"><span data-stu-id="67c26-137">The following snippet can be used to authenticate your application non-interactively, using the client secret for an application / service principal.</span></span> <span data-ttu-id="67c26-138">Use this with an existing Azure AD "Web App" application.</span><span class="sxs-lookup"><span data-stu-id="67c26-138">Use this with an existing Azure AD "Web App" application.</span></span>

    credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')

## <a name="create-resource-management-group"></a><span data-ttu-id="67c26-139">Create Resource Management group</span><span class="sxs-lookup"><span data-stu-id="67c26-139">Create Resource Management group</span></span>

<span data-ttu-id="67c26-140">Use the following code snippet to create an Azure Resource Group:</span><span class="sxs-lookup"><span data-stu-id="67c26-140">Use the following code snippet to create an Azure Resource Group:</span></span>

    ## Declare variables
    subscriptionId= '<Azure Subscription ID>'
    resourceGroup = '<Azure Resource Group Name>'
    location = '<Location>' # i.e. 'eastus2'

    ## Create management client object
    resourceClient = ResourceManagementClient(
        credentials,
        subscriptionId
    )

    ## Create an Azure Resource Group
    armGroupResult = resourceClient.resource_groups.create_or_update(
        resourceGroup,
        ResourceGroup(
            location=location
        )
    )


## <a name="create-data-lake-store-account"></a><span data-ttu-id="67c26-141">Create Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="67c26-141">Create Data Lake Store account</span></span>

<span data-ttu-id="67c26-142">Each Data Lake Analytics account requires a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="67c26-142">Each Data Lake Analytics account requires a Data Lake Store account.</span></span> <span data-ttu-id="67c26-143">For instructions, see [Create a Data Lake Store account](../data-lake-store/data-lake-store-get-started-portal.md#create-an-azure-data-lake-store-account).</span><span class="sxs-lookup"><span data-stu-id="67c26-143">For instructions, see [Create a Data Lake Store account](../data-lake-store/data-lake-store-get-started-portal.md#create-an-azure-data-lake-store-account).</span></span>



## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="67c26-144">Create Data Lake Analytics account</span><span class="sxs-lookup"><span data-stu-id="67c26-144">Create Data Lake Analytics account</span></span>

    ## Declare variables
    subscriptionId= '<Azure Subscription ID>'
    resourceGroup = '<Azure Resource Group Name>'
    location = '<Location>' # i.e. 'eastus2'
    adlsAccountName = '<Azure Data Lake Store Account Name>'
    adlaAccountName = '<Azure Data Lake Analytics Account Name>'

    ## Create management client object
    adlaAcctClient = DataLakeAnalyticsAccountManagementClient(
        credentials,
        subscriptionId
    )

    ## Create an Azure Data Lake Analytics account
    adlaAcctResult = adlaAcctClient.account.create(
        resourceGroup,
        adlaAccountName,
        DataLakeAnalyticsAccount(
            location=location,
            default_data_lake_store_account=adlsAccountName,
            data_lake_store_accounts=[DataLakeStoreAccountInfo(name=adlsAccountName)]
        )
    ).wait()


##<a name="submit-data-lake-analytics-jobs"></a><span data-ttu-id="67c26-145">Submit Data Lake Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="67c26-145">Submit Data Lake Analytics jobs</span></span>

<span data-ttu-id="67c26-146">The Data Lake Analytics jobs are written in the U-SQL language.</span><span class="sxs-lookup"><span data-stu-id="67c26-146">The Data Lake Analytics jobs are written in the U-SQL language.</span></span> <span data-ttu-id="67c26-147">To learn more about U-SQL, see [Get started with U-SQL language](data-lake-analytics-u-sql-get-started.md) and [U-SQL language reference](http://go.microsoft.com/fwlink/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="67c26-147">To learn more about U-SQL, see [Get started with U-SQL language](data-lake-analytics-u-sql-get-started.md) and [U-SQL language reference](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>

    ## Declare variables
    adlsAccountName = '<Azure Data Lake Store Account Name>'

    ## Create management client object
    adlaJobClient = DataLakeAnalyticsJobManagementClient(
        credentials,
        'azuredatalakeanalytics.net'
    )

    ## Submit a U-SQL job
    jobId = str(uuid.uuid4())
    jobResult = adlaJobClient.job.create(
        adlaAccountName,
        jobId,
        JobInformation(
            name='Sample Job',
            type='USql',
            properties=USqlJobProperties(
                script='DROP DATABASE IF EXISTS FOO; CREATE DATABASE FOO;'
            )
        )
    )

    ## Print the job result
    while(jobResult.state != JobState.ended):
        print('Job is not yet done, waiting for 3 seconds. Current state: ' + jobResult.state.value)
        time.sleep(3)
        jobResult = adlaJobClient.job.get(adlaAccountName, jobId)
        
    print ('Job finished with result: ' + jobResult.result.value)

## <a name="next-steps"></a><span data-ttu-id="67c26-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="67c26-148">Next steps</span></span>

- <span data-ttu-id="67c26-149">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span><span class="sxs-lookup"><span data-stu-id="67c26-149">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span></span>
- <span data-ttu-id="67c26-150">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="67c26-150">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
- <span data-ttu-id="67c26-151">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="67c26-151">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="67c26-152">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="67c26-152">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
- <span data-ttu-id="67c26-153">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="67c26-153">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
- <span data-ttu-id="67c26-154">To get an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="67c26-154">To get an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

