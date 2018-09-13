---
title: Get started with Azure Data Lake Analytics using .NET SDK | Microsoft Docs
description: 'Learn how to use the .NET SDK to create Data Lake Analytics accounts, create Data Lake Analytics jobs, and submit jobs written in U-SQL. '
services: data-lake-analytics
documentationcenter: ''
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 1dfcbc3d-235d-4074-bc2a-e96def8298b6
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/26/2016
ms.author: edmaca
ms.openlocfilehash: 9c82ab54138dd376fff81258b6f368fb84ed14fd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550216"
---
# <a name="tutorial-get-started-with-azure-data-lake-analytics-using-net-sdk"></a><span data-ttu-id="8813f-103">Tutorial: get started with Azure Data Lake Analytics using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="8813f-103">Tutorial: get started with Azure Data Lake Analytics using .NET SDK</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="8813f-104">Learn how to use the Azure .NET SDK to submit jobs written in [U-SQL](data-lake-analytics-u-sql-get-started.md) to Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="8813f-104">Learn how to use the Azure .NET SDK to submit jobs written in [U-SQL](data-lake-analytics-u-sql-get-started.md) to Data Lake Analytics.</span></span> <span data-ttu-id="8813f-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8813f-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

<span data-ttu-id="8813f-106">In this tutorial, you will develop a C# console application to submit a U-SQL job that reads a tab separated values (TSV) file and converts it into a comma separated values (CSV) file.</span><span class="sxs-lookup"><span data-stu-id="8813f-106">In this tutorial, you will develop a C# console application to submit a U-SQL job that reads a tab separated values (TSV) file and converts it into a comma separated values (CSV) file.</span></span> <span data-ttu-id="8813f-107">To go through the same tutorial using other supported tools, click the tabs on the top of this article.</span><span class="sxs-lookup"><span data-stu-id="8813f-107">To go through the same tutorial using other supported tools, click the tabs on the top of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8813f-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8813f-108">Prerequisites</span></span>
<span data-ttu-id="8813f-109">Before you begin this tutorial, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="8813f-109">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="8813f-110">**Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed**.</span><span class="sxs-lookup"><span data-stu-id="8813f-110">**Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed**.</span></span>
* <span data-ttu-id="8813f-111">**Microsoft Azure SDK for .NET version 2.5 or above**.</span><span class="sxs-lookup"><span data-stu-id="8813f-111">**Microsoft Azure SDK for .NET version 2.5 or above**.</span></span>  <span data-ttu-id="8813f-112">Install it using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="8813f-112">Install it using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="8813f-113">**An Azure Data Lake Analytics account**.</span><span class="sxs-lookup"><span data-stu-id="8813f-113">**An Azure Data Lake Analytics account**.</span></span> <span data-ttu-id="8813f-114">See [Manage Data Lake Analytics using Azure .NET SDK](data-lake-analytics-manage-use-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="8813f-114">See [Manage Data Lake Analytics using Azure .NET SDK](data-lake-analytics-manage-use-dotnet-sdk.md).</span></span>

## <a name="create-console-application"></a><span data-ttu-id="8813f-115">Create console application</span><span class="sxs-lookup"><span data-stu-id="8813f-115">Create console application</span></span>
<span data-ttu-id="8813f-116">In this tutorial, you process some search logs.</span><span class="sxs-lookup"><span data-stu-id="8813f-116">In this tutorial, you process some search logs.</span></span>  <span data-ttu-id="8813f-117">The search log can be stored in either Data Lake store or Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="8813f-117">The search log can be stored in either Data Lake store or Azure Blob storage.</span></span> 

<span data-ttu-id="8813f-118">A sample search log can be found in a public Azure Blob container.</span><span class="sxs-lookup"><span data-stu-id="8813f-118">A sample search log can be found in a public Azure Blob container.</span></span> <span data-ttu-id="8813f-119">In the application, you will download the file to your workstation, and then upload the file to the default Data Lake Store account of your Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="8813f-119">In the application, you will download the file to your workstation, and then upload the file to the default Data Lake Store account of your Data Lake Analytics account.</span></span>

<span data-ttu-id="8813f-120">**To create a U-SQL script**</span><span class="sxs-lookup"><span data-stu-id="8813f-120">**To create a U-SQL script**</span></span>

<span data-ttu-id="8813f-121">Data Lake Analytics jobs are written in the U-SQL language.</span><span class="sxs-lookup"><span data-stu-id="8813f-121">Data Lake Analytics jobs are written in the U-SQL language.</span></span> <span data-ttu-id="8813f-122">To learn more about U-SQL, see [Get started with U-SQL language](data-lake-analytics-u-sql-get-started.md) and [U-SQL language reference](http://go.microsoft.com/fwlink/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="8813f-122">To learn more about U-SQL, see [Get started with U-SQL language](data-lake-analytics-u-sql-get-started.md) and [U-SQL language reference](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>

<span data-ttu-id="8813f-123">Create a **SampleUSQLScript.txt** file with the following U-SQL script, and place the file in the \**C:\temp\** path.</span><span class="sxs-lookup"><span data-stu-id="8813f-123">Create a **SampleUSQLScript.txt** file with the following U-SQL script, and place the file in the \**C:\temp\** path.</span></span>  <span data-ttu-id="8813f-124">The path is hardcoded in the .NET application that you create in the next procedure.</span><span class="sxs-lookup"><span data-stu-id="8813f-124">The path is hardcoded in the .NET application that you create in the next procedure.</span></span>  

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM "/Samples/Data/SearchLog.tsv"
        USING Extractors.Tsv();

    OUTPUT @searchlog   
        TO "/Output/SearchLog-from-Data-Lake.csv"
    USING Outputters.Csv();

<span data-ttu-id="8813f-125">This U-SQL script reads the source data file using **Extractors.Tsv()**, and then creates a csv file using **Outputters.Csv()**.</span><span class="sxs-lookup"><span data-stu-id="8813f-125">This U-SQL script reads the source data file using **Extractors.Tsv()**, and then creates a csv file using **Outputters.Csv()**.</span></span> 

<span data-ttu-id="8813f-126">In the C# program, you need to prepare the **/Samples/Data/SearchLog.tsv** file, and the **/Output/** folder.</span><span class="sxs-lookup"><span data-stu-id="8813f-126">In the C# program, you need to prepare the **/Samples/Data/SearchLog.tsv** file, and the **/Output/** folder.</span></span>    

<span data-ttu-id="8813f-127">It is simpler to use relative paths for files stored in default data Lake accounts.</span><span class="sxs-lookup"><span data-stu-id="8813f-127">It is simpler to use relative paths for files stored in default data Lake accounts.</span></span> <span data-ttu-id="8813f-128">You can also use absolute paths.</span><span class="sxs-lookup"><span data-stu-id="8813f-128">You can also use absolute paths.</span></span>  <span data-ttu-id="8813f-129">For example</span><span class="sxs-lookup"><span data-stu-id="8813f-129">For example</span></span> 

    adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv

<span data-ttu-id="8813f-130">You must use absolute paths to access  files in linked Storage accounts.</span><span class="sxs-lookup"><span data-stu-id="8813f-130">You must use absolute paths to access  files in linked Storage accounts.</span></span>  <span data-ttu-id="8813f-131">The syntax for files stored in the linked Azure Storage account is:</span><span class="sxs-lookup"><span data-stu-id="8813f-131">The syntax for files stored in the linked Azure Storage account is:</span></span>

    wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv

> [!NOTE]
> <span data-ttu-id="8813f-132">There is currently a known issue with the Azure Data Lake Service.</span><span class="sxs-lookup"><span data-stu-id="8813f-132">There is currently a known issue with the Azure Data Lake Service.</span></span>  <span data-ttu-id="8813f-133">If the sample app is interrupted or encounters an error, you may need to manually delete the Data Lake Store & Data Lake Analytics accounts that the script creates.</span><span class="sxs-lookup"><span data-stu-id="8813f-133">If the sample app is interrupted or encounters an error, you may need to manually delete the Data Lake Store & Data Lake Analytics accounts that the script creates.</span></span>  <span data-ttu-id="8813f-134">If you're not familiar with the Azure portal, the [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md) guide will get you started.</span><span class="sxs-lookup"><span data-stu-id="8813f-134">If you're not familiar with the Azure portal, the [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md) guide will get you started.</span></span>       
> 
> 

<span data-ttu-id="8813f-135">**To create an application**</span><span class="sxs-lookup"><span data-stu-id="8813f-135">**To create an application**</span></span>

1. <span data-ttu-id="8813f-136">Open Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8813f-136">Open Visual Studio.</span></span>
2. <span data-ttu-id="8813f-137">Create a C# console application.</span><span class="sxs-lookup"><span data-stu-id="8813f-137">Create a C# console application.</span></span>
3. <span data-ttu-id="8813f-138">Open NuGet Package Management console, and run the following commands:</span><span class="sxs-lookup"><span data-stu-id="8813f-138">Open NuGet Package Management console, and run the following commands:</span></span>
   
        Install-Package Microsoft.Azure.Management.DataLake.Analytics -Pre
        Install-Package Microsoft.Azure.Management.DataLake.Store -Pre
        Install-Package Microsoft.Azure.Management.DataLake.StoreUploader -Pre
        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
        Install-Package WindowsAzure.Storage
4. <span data-ttu-id="8813f-139">In Program.cs, paste the following code:</span><span class="sxs-lookup"><span data-stu-id="8813f-139">In Program.cs, paste the following code:</span></span>
   
        using System;
        using System.IO;
        using System.Collections.Generic;
        using System.Threading;
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Azure.Management.DataLake.Store;
        using Microsoft.Azure.Management.DataLake.StoreUploader;
        using Microsoft.Azure.Management.DataLake.Analytics;
        using Microsoft.Azure.Management.DataLake.Analytics.Models;
        using Microsoft.WindowsAzure.Storage.Blob;
   
        namespace SdkSample
        {
          class Program
          {
            private const string SUBSCRIPTIONID = "<Enter Your Azure Subscription ID>";
            private const string CLIENTID = "1950a258-227b-4e31-a9cf-717495945fc2";
            private const string DOMAINNAME = "common"; // Replace this string with the user's Azure Active Directory tenant ID or domain name, if needed.
   
            private static string _adlaAccountName = "<Enter an Existing Data Lake Analytics Account Name>";
            private static string _adlsAccountName = "<Enter the default Data Lake Store Account Name>";
   
            private static DataLakeAnalyticsAccountManagementClient _adlaClient;
            private static DataLakeStoreFileSystemManagementClient _adlsFileSystemClient;
            private static DataLakeAnalyticsJobManagementClient _adlaJobClient;
   
            private static void Main(string[] args)
            {
                string localFolderPath = @"c:\temp\";
   
                // Connect to Azure
                var creds = AuthenticateAzure(DOMAINNAME, CLIENTID);
   
                SetupClients(creds, SUBSCRIPTIONID);
   
                // Transfer the source file from a public Azure Blob container to Data Lake Store.
                CloudBlockBlob blob = new CloudBlockBlob(new Uri("https://adltutorials.blob.core.windows.net/adls-sample-data/SearchLog.tsv"));
                blob.DownloadToFile(localFolderPath + "SearchLog.tsv", FileMode.Create); // from WASB
                UploadFile(localFolderPath + "SearchLog.tsv", "/Samples/Data/SearchLog.tsv"); // to ADLS
                WaitForNewline("Source data file prepared.", "Submitting a job.");

                // Submit the job
                Guid jobId = SubmitJobByPath(localFolderPath + "SampleUSQLScript.txt", "My First ADLA Job");
                WaitForNewline("Job submitted.", "Waiting for job completion.");

                // Wait for job completion
                WaitForJob(jobId);
                WaitForNewline("Job completed.", "Downloading job output.");

                // Download job output
                DownloadFile(@"/Output/SearchLog-from-Data-Lake.csv", localFolderPath + "SearchLog-from-Data-Lake.csv");

                  WaitForNewline("Job output downloaded. You can now exit.");
            }

            public static ServiceClientCredentials AuthenticateAzure(
                string domainName,
                string nativeClientAppCLIENTID)
            {
                // User login via interactive popup
                SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
                // Use the client ID of an existing AAD "Native Client" application.
                var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(nativeClientAppCLIENTID, new Uri("urn:ietf:wg:oauth:2.0:oob"));
                return UserTokenProvider.LoginWithPromptAsync(domainName, activeDirectoryClientSettings).Result;
            }

            public static void SetupClients(ServiceClientCredentials tokenCreds, string subscriptionId)
            {
                _adlaClient = new DataLakeAnalyticsAccountManagementClient(tokenCreds);
                _adlaClient.SubscriptionId = subscriptionId;

                _adlaJobClient = new DataLakeAnalyticsJobManagementClient(tokenCreds);

                _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(tokenCreds);
            }

            public static void UploadFile(string srcFilePath, string destFilePath, bool force = true)
            {
                var parameters = new UploadParameters(srcFilePath, destFilePath, _adlsAccountName, isOverwrite: force);
                var frontend = new DataLakeStoreFrontEndAdapter(_adlsAccountName, _adlsFileSystemClient);
                var uploader = new DataLakeStoreUploader(parameters, frontend);
                uploader.Execute();
            }

            public static void DownloadFile(string srcPath, string destPath)
            {
                var stream = _adlsFileSystemClient.FileSystem.Open(_adlsAccountName, srcPath);
                var fileStream = new FileStream(destPath, FileMode.Create);

                stream.CopyTo(fileStream);
                fileStream.Close();
                stream.Close();
            }

            // Helper function to show status and wait for user input
            public static void WaitForNewline(string reason, string nextAction = "")
            {
                Console.WriteLine(reason + "\r\nPress ENTER to continue...");

                Console.ReadLine();

                if (!String.IsNullOrWhiteSpace(nextAction))
                    Console.WriteLine(nextAction);
            }

            // List all Data Lake Analytics accounts within the subscription
            public static List<DataLakeAnalyticsAccount> ListADLAAccounts()
            {
                var response = _adlaClient.Account.List();
                var accounts = new List<DataLakeAnalyticsAccount>(response);

                while (response.NextPageLink != null)
                {
                    response = _adlaClient.Account.ListNext(response.NextPageLink);
                    accounts.AddRange(response);
                }

                Console.WriteLine("You have %i Data Lake Analytics account(s).", accounts.Count);
                for (int i = 0; i < accounts.Count; i++)
                {
                    Console.WriteLine(accounts[i].Name);
                }

                return accounts;
            }

            public static Guid SubmitJobByPath(string scriptPath, string jobName)
            {
                var script = File.ReadAllText(scriptPath);

                var jobId = Guid.NewGuid();
                var properties = new USqlJobProperties(script);
                var parameters = new JobInformation(jobName, JobType.USql, properties, priority: 1, degreeOfParallelism: 1, jobId: jobId);
                var jobInfo = _adlaJobClient.Job.Create(_adlaAccountName, jobId, parameters);

                return jobId;
            }

            public static JobResult WaitForJob(Guid jobId)
            {
                var jobInfo = _adlaJobClient.Job.Get(_adlaAccountName, jobId);
                while (jobInfo.State != JobState.Ended)
                {
                    jobInfo = _adlaJobClient.Job.Get(_adlaAccountName, jobId);
                }
                return jobInfo.Result.Value;
            }
          }
        }

5. <span data-ttu-id="8813f-140">Press **F5** to run the application.</span><span class="sxs-lookup"><span data-stu-id="8813f-140">Press **F5** to run the application.</span></span> <span data-ttu-id="8813f-141">The output is like:</span><span class="sxs-lookup"><span data-stu-id="8813f-141">The output is like:</span></span>
   
    ![Azure Data Lake Analytics job U-SQL .NET SDK output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-get-started-net-sdk/data-lake-analytics-dotnet-job-output.png)
6. <span data-ttu-id="8813f-143">Check the output file.</span><span class="sxs-lookup"><span data-stu-id="8813f-143">Check the output file.</span></span>  <span data-ttu-id="8813f-144">The default path and file name is c:\Temp\SearchLog-from-Data-Lake.csv.</span><span class="sxs-lookup"><span data-stu-id="8813f-144">The default path and file name is c:\Temp\SearchLog-from-Data-Lake.csv.</span></span>

## <a name="see-also"></a><span data-ttu-id="8813f-145">See also</span><span class="sxs-lookup"><span data-stu-id="8813f-145">See also</span></span>
* <span data-ttu-id="8813f-146">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span><span class="sxs-lookup"><span data-stu-id="8813f-146">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span></span>
* <span data-ttu-id="8813f-147">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="8813f-147">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="8813f-148">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8813f-148">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="8813f-149">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md), and [U-SQL language reference](http://go.microsoft.com/fwlink/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="8813f-149">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md), and [U-SQL language reference](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>
* <span data-ttu-id="8813f-150">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8813f-150">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="8813f-151">To get an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8813f-151">To get an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>


