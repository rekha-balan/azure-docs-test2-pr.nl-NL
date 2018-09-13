---
title: Develop U-SQL assemblies for Azure Data Lake Analytics jobs | Microsoft Docs
description: 'Learn how to develop assemblies to be used and reused in Data Lake Analytics jobs. '
services: data-lake-analytics
documentationcenter: ''
author: jejiang
manager: jhubbard
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/30/2016
ms.author: jejiang
ms.openlocfilehash: 98b04d28d1b905dad19ad6cf608733c6554f01cf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554206"
---
# <a name="develop-u-sql-assemblies-for-azure-data-lake-analytics-jobs"></a><span data-ttu-id="39e39-103">Develop U-SQL assemblies for Azure Data Lake Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="39e39-103">Develop U-SQL assemblies for Azure Data Lake Analytics jobs</span></span>
<span data-ttu-id="39e39-104">Learn how to turn code-behind into assemblies to be used and reused in Data Lake Analytics jobs.</span><span class="sxs-lookup"><span data-stu-id="39e39-104">Learn how to turn code-behind into assemblies to be used and reused in Data Lake Analytics jobs.</span></span> 

<span data-ttu-id="39e39-105">U-SQL makes it easy to add your own custom code in .Net languages, such as C#, VB.Net or F#.</span><span class="sxs-lookup"><span data-stu-id="39e39-105">U-SQL makes it easy to add your own custom code in .Net languages, such as C#, VB.Net or F#.</span></span> <span data-ttu-id="39e39-106">You can even deploy your own runtime to support other languages.</span><span class="sxs-lookup"><span data-stu-id="39e39-106">You can even deploy your own runtime to support other languages.</span></span>

<span data-ttu-id="39e39-107">The easiest way to use custom code is to use the Data Lake Tools for Visual Studio’s code-behind capabilities.</span><span class="sxs-lookup"><span data-stu-id="39e39-107">The easiest way to use custom code is to use the Data Lake Tools for Visual Studio’s code-behind capabilities.</span></span> <span data-ttu-id="39e39-108">For more information, see [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="39e39-108">For more information, see [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="39e39-109">There are a few drawbacks of using code-behind:</span><span class="sxs-lookup"><span data-stu-id="39e39-109">There are a few drawbacks of using code-behind:</span></span>

- <span data-ttu-id="39e39-110">The source code gets uploaded for every script submission.</span><span class="sxs-lookup"><span data-stu-id="39e39-110">The source code gets uploaded for every script submission.</span></span>
- <span data-ttu-id="39e39-111">code-behind cannot be shared with other jobs.</span><span class="sxs-lookup"><span data-stu-id="39e39-111">code-behind cannot be shared with other jobs.</span></span>

<span data-ttu-id="39e39-112">To address these drawbacks, you can turn code-behind into assemblies, and register the assemblies to the Data Lake Analytics catalog.</span><span class="sxs-lookup"><span data-stu-id="39e39-112">To address these drawbacks, you can turn code-behind into assemblies, and register the assemblies to the Data Lake Analytics catalog.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39e39-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="39e39-113">Prerequisites</span></span>
* <span data-ttu-id="39e39-114">Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed</span><span class="sxs-lookup"><span data-stu-id="39e39-114">Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed</span></span>
* <span data-ttu-id="39e39-115">Microsoft Azure SDK for .NET version 2.5 or above.</span><span class="sxs-lookup"><span data-stu-id="39e39-115">Microsoft Azure SDK for .NET version 2.5 or above.</span></span>  <span data-ttu-id="39e39-116">Install it using the Web platform installer.</span><span class="sxs-lookup"><span data-stu-id="39e39-116">Install it using the Web platform installer.</span></span>
* <span data-ttu-id="39e39-117">A Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="39e39-117">A Data Lake Analytics account.</span></span>  <span data-ttu-id="39e39-118">See [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="39e39-118">See [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="39e39-119">Go through the [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="39e39-119">Go through the [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md) tutorial.</span></span>
* <span data-ttu-id="39e39-120">Connect to Azure.</span><span class="sxs-lookup"><span data-stu-id="39e39-120">Connect to Azure.</span></span>
* <span data-ttu-id="39e39-121">Upload the source data, see [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="39e39-121">Upload the source data, see [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md).</span></span> 

## <a name="develop-assemblies-for-u-sql"></a><span data-ttu-id="39e39-122">Develop assemblies for U-SQL</span><span class="sxs-lookup"><span data-stu-id="39e39-122">Develop assemblies for U-SQL</span></span>

<span data-ttu-id="39e39-123">**To create and submit a U-SQL job**</span><span class="sxs-lookup"><span data-stu-id="39e39-123">**To create and submit a U-SQL job**</span></span>

1. <span data-ttu-id="39e39-124">From the **File** menu, click **New**, and then click **Project**.</span><span class="sxs-lookup"><span data-stu-id="39e39-124">From the **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="39e39-125">Expand **Installed**, **Templates**, **Azure Data Lake**, **U-SQL(ADLA)**, select the **Class Library (For U-SQL Application)** template, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="39e39-125">Expand **Installed**, **Templates**, **Azure Data Lake**, **U-SQL(ADLA)**, select the **Class Library (For U-SQL Application)** template, and then click **OK**.</span></span>
3. <span data-ttu-id="39e39-126">Write your code in Class1.cs.</span><span class="sxs-lookup"><span data-stu-id="39e39-126">Write your code in Class1.cs.</span></span>  <span data-ttu-id="39e39-127">The following is a code sample.</span><span class="sxs-lookup"><span data-stu-id="39e39-127">The following is a code sample.</span></span>

        using Microsoft.Analytics.Interfaces;

        namespace USQLApplication_codebehind
        {
            [SqlUserDefinedProcessor]
            public class MyProcessor : IProcessor
            {
                public override IRow Process(IRow input, IUpdatableRow output)
                {
                    output.Set(0, input.Get<string>(0));
                    output.Set(0, input.Get<string>(0));
                    return output.AsReadOnly();
                }
            }
        }
4. <span data-ttu-id="39e39-128">Click the **Build** menu, and then click **Build Solution** to create the dll.</span><span class="sxs-lookup"><span data-stu-id="39e39-128">Click the **Build** menu, and then click **Build Solution** to create the dll.</span></span>

## <a name="register-assemblies"></a><span data-ttu-id="39e39-129">Register assemblies</span><span class="sxs-lookup"><span data-stu-id="39e39-129">Register assemblies</span></span>

<span data-ttu-id="39e39-130">See [Use Data Lake Analytics(U-SQL) catalog](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="39e39-130">See [Use Data Lake Analytics(U-SQL) catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>


## <a name="use-the-assemblies"></a><span data-ttu-id="39e39-131">Use the assemblies</span><span class="sxs-lookup"><span data-stu-id="39e39-131">Use the assemblies</span></span>

<span data-ttu-id="39e39-132">See [Use the Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="39e39-132">See [Use the Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="39e39-133">See also</span><span class="sxs-lookup"><span data-stu-id="39e39-133">See also</span></span>
* [<span data-ttu-id="39e39-134">Get started with Data Lake Analytics using PowerShell</span><span class="sxs-lookup"><span data-stu-id="39e39-134">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="39e39-135">Get started with Data Lake Analytics using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="39e39-135">Get started with Data Lake Analytics using the Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="39e39-136">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span><span class="sxs-lookup"><span data-stu-id="39e39-136">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="39e39-137">Use Data Lake Analytics(U-SQL) catalog</span><span class="sxs-lookup"><span data-stu-id="39e39-137">Use Data Lake Analytics(U-SQL) catalog</span></span>](data-lake-analytics-use-u-sql-catalog.md)
* [<span data-ttu-id="39e39-138">Use the Azure Data Lake Tools for Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="39e39-138">Use the Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)