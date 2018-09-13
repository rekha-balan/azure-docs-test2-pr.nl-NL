---
title: Develop U-SQL user-defined operators for Azure Data Lake Analytics jobs | Microsoft Docs
description: 'Learn how to develop user-defined operators to be used and reused in Data Lake Analytics jobs. '
services: data-lake-analytics
documentationcenter: ''
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: e5189e4e-9438-46d1-8686-ed4836bf3356
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 3fef47dcec418c8e206f1385ca7bd70bacf937c4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563566"
---
# <a name="develop-u-sql-user-defined-operators-for-azure-data-lake-analytics-jobs"></a><span data-ttu-id="37a8f-103">Develop U-SQL user-defined operators for Azure Data Lake Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="37a8f-103">Develop U-SQL user-defined operators for Azure Data Lake Analytics jobs</span></span>
<span data-ttu-id="37a8f-104">Learn how to develop user-defined operators to be used and reused in Data Lake Analytics jobs.</span><span class="sxs-lookup"><span data-stu-id="37a8f-104">Learn how to develop user-defined operators to be used and reused in Data Lake Analytics jobs.</span></span> <span data-ttu-id="37a8f-105">You will develop a custom operator to convert country names.</span><span class="sxs-lookup"><span data-stu-id="37a8f-105">You will develop a custom operator to convert country names.</span></span>

<span data-ttu-id="37a8f-106">For the instructions of developing general-purpose assemblies for U-SQL, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md)</span><span class="sxs-lookup"><span data-stu-id="37a8f-106">For the instructions of developing general-purpose assemblies for U-SQL, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37a8f-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="37a8f-107">Prerequisites</span></span>
* <span data-ttu-id="37a8f-108">Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed</span><span class="sxs-lookup"><span data-stu-id="37a8f-108">Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed</span></span>
* <span data-ttu-id="37a8f-109">Microsoft Azure SDK for .NET version 2.5 or above.</span><span class="sxs-lookup"><span data-stu-id="37a8f-109">Microsoft Azure SDK for .NET version 2.5 or above.</span></span>  <span data-ttu-id="37a8f-110">Install it using the Web platform installer.</span><span class="sxs-lookup"><span data-stu-id="37a8f-110">Install it using the Web platform installer.</span></span>
* <span data-ttu-id="37a8f-111">A Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="37a8f-111">A Data Lake Analytics account.</span></span>  <span data-ttu-id="37a8f-112">See [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="37a8f-112">See [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="37a8f-113">Go through the [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="37a8f-113">Go through the [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md) tutorial.</span></span>
* <span data-ttu-id="37a8f-114">Connect to Azure.</span><span class="sxs-lookup"><span data-stu-id="37a8f-114">Connect to Azure.</span></span>
* <span data-ttu-id="37a8f-115">Upload the source data, see [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="37a8f-115">Upload the source data, see [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md).</span></span> 

## <a name="define-and-use-user-defined-operator-in-u-sql"></a><span data-ttu-id="37a8f-116">Define and use user-defined operator in U-SQL</span><span class="sxs-lookup"><span data-stu-id="37a8f-116">Define and use user-defined operator in U-SQL</span></span>
<span data-ttu-id="37a8f-117">**To create and submit a U-SQL job**</span><span class="sxs-lookup"><span data-stu-id="37a8f-117">**To create and submit a U-SQL job**</span></span>

1. <span data-ttu-id="37a8f-118">From the **File** menu, click **New**, and then click **Project**.</span><span class="sxs-lookup"><span data-stu-id="37a8f-118">From the **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="37a8f-119">Select the **U-SQL Project** type.</span><span class="sxs-lookup"><span data-stu-id="37a8f-119">Select the **U-SQL Project** type.</span></span>

    ![new U-SQL Visual Studio project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. <span data-ttu-id="37a8f-121">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="37a8f-121">Click **OK**.</span></span> <span data-ttu-id="37a8f-122">Visual studio creates a solution with a Script.usql file.</span><span class="sxs-lookup"><span data-stu-id="37a8f-122">Visual studio creates a solution with a Script.usql file.</span></span>
4. <span data-ttu-id="37a8f-123">From **Solution Explorer**, expand Script.usql, and then double-click **Script.usql.cs**.</span><span class="sxs-lookup"><span data-stu-id="37a8f-123">From **Solution Explorer**, expand Script.usql, and then double-click **Script.usql.cs**.</span></span>
5. <span data-ttu-id="37a8f-124">Paste the following code into the file:</span><span class="sxs-lookup"><span data-stu-id="37a8f-124">Paste the following code into the file:</span></span>

        using Microsoft.Analytics.Interfaces;
        using System.Collections.Generic;

        namespace USQL_UDO
        {
            public class CountryName : IProcessor
            {
                private static IDictionary<string, string> CountryTranslation = new Dictionary<string, string>
                {
                    {
                        "Deutschland", "Germany"
                    },
                    {
                        "Schwiiz", "Switzerland"
                    },
                    {
                        "UK", "United Kingdom"
                    },
                    {
                        "USA", "United States of America"
                    },
                    {
                        "中国", "PR China"
                    }
                };

                public override IRow Process(IRow input, IUpdatableRow output)
                {

                    string UserID = input.Get<string>("UserID");
                    string Name = input.Get<string>("Name");
                    string Address = input.Get<string>("Address");
                    string City = input.Get<string>("City");
                    string State = input.Get<string>("State");
                    string PostalCode = input.Get<string>("PostalCode");
                    string Country = input.Get<string>("Country");
                    string Phone = input.Get<string>("Phone");

                    if (CountryTranslation.Keys.Contains(Country))
                    {
                        Country = CountryTranslation[Country];
                    }
                    output.Set<string>(0, UserID);
                    output.Set<string>(1, Name);
                    output.Set<string>(2, Address);
                    output.Set<string>(3, City);
                    output.Set<string>(4, State);
                    output.Set<string>(5, PostalCode);
                    output.Set<string>(6, Country);
                    output.Set<string>(7, Phone);

                    return output.AsReadOnly();
                }
            }
        }
6. <span data-ttu-id="37a8f-125">Open Script.usql, and paste the following U-SQL script:</span><span class="sxs-lookup"><span data-stu-id="37a8f-125">Open Script.usql, and paste the following U-SQL script:</span></span>

        @drivers =
            EXTRACT UserID      string,
                    Name        string,
                    Address     string,
                    City        string,
                    State       string,
                    PostalCode  string,
                    Country     string,
                    Phone       string
            FROM "/Samples/Data/AmbulanceData/Drivers.txt"
            USING Extractors.Tsv(Encoding.Unicode);

        @drivers_CountryName =
            PROCESS @drivers
            PRODUCE UserID string,
                    Name string,
                    Address string,
                    City string,
                    State string,
                    PostalCode string,
                    Country string,
                    Phone string
            USING new USQL_UDO.CountryName();    

        OUTPUT @drivers_CountryName
            TO "/Samples/Outputs/Drivers.csv"
            USING Outputters.Csv(Encoding.Unicode);
7. <span data-ttu-id="37a8f-126">From **Solution Explorer**, right-click **Script.usql**, and then click **Build Script**.</span><span class="sxs-lookup"><span data-stu-id="37a8f-126">From **Solution Explorer**, right-click **Script.usql**, and then click **Build Script**.</span></span>
8. <span data-ttu-id="37a8f-127">From **Solution Explorer**, right-click **Script.usql**, and then click **Submit Script**.</span><span class="sxs-lookup"><span data-stu-id="37a8f-127">From **Solution Explorer**, right-click **Script.usql**, and then click **Submit Script**.</span></span>
9. <span data-ttu-id="37a8f-128">If you haven't connect to your Azure subscription, you will be prompt to enter your Azure account credentials.</span><span class="sxs-lookup"><span data-stu-id="37a8f-128">If you haven't connect to your Azure subscription, you will be prompt to enter your Azure account credentials.</span></span>
10. <span data-ttu-id="37a8f-129">Click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="37a8f-129">Click **Submit**.</span></span> <span data-ttu-id="37a8f-130">Submission results and job link are available in the Results window when the submission is completed.</span><span class="sxs-lookup"><span data-stu-id="37a8f-130">Submission results and job link are available in the Results window when the submission is completed.</span></span>
11. <span data-ttu-id="37a8f-131">You must click the Refresh button to see the latest job status and refresh the screen.</span><span class="sxs-lookup"><span data-stu-id="37a8f-131">You must click the Refresh button to see the latest job status and refresh the screen.</span></span>

<span data-ttu-id="37a8f-132">**To see the job output**</span><span class="sxs-lookup"><span data-stu-id="37a8f-132">**To see the job output**</span></span>

1. <span data-ttu-id="37a8f-133">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click the Default Storage, and then click **Explorer**.</span><span class="sxs-lookup"><span data-stu-id="37a8f-133">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click the Default Storage, and then click **Explorer**.</span></span>
2. <span data-ttu-id="37a8f-134">Expand Samples, expand Outputs, and then double-click **Drivers.csv**.</span><span class="sxs-lookup"><span data-stu-id="37a8f-134">Expand Samples, expand Outputs, and then double-click **Drivers.csv**.</span></span>

## <a name="see-also"></a><span data-ttu-id="37a8f-135">See also</span><span class="sxs-lookup"><span data-stu-id="37a8f-135">See also</span></span>
* [<span data-ttu-id="37a8f-136">Get started with Data Lake Analytics using PowerShell</span><span class="sxs-lookup"><span data-stu-id="37a8f-136">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="37a8f-137">Get started with Data Lake Analytics using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="37a8f-137">Get started with Data Lake Analytics using the Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="37a8f-138">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span><span class="sxs-lookup"><span data-stu-id="37a8f-138">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)

