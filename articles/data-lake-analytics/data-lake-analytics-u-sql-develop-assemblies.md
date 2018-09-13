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
# <a name="develop-u-sql-assemblies-for-azure-data-lake-analytics-jobs"></a>Develop U-SQL assemblies for Azure Data Lake Analytics jobs
Learn how to turn code-behind into assemblies to be used and reused in Data Lake Analytics jobs. 

U-SQL makes it easy to add your own custom code in .Net languages, such as C#, VB.Net or F#. You can even deploy your own runtime to support other languages.

The easiest way to use custom code is to use the Data Lake Tools for Visual Studio’s code-behind capabilities. For more information, see [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md). There are a few drawbacks of using code-behind:

- The source code gets uploaded for every script submission.
- code-behind cannot be shared with other jobs.

To address these drawbacks, you can turn code-behind into assemblies, and register the assemblies to the Data Lake Analytics catalog.

## <a name="prerequisites"></a>Prerequisites
* Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed
* Microsoft Azure SDK for .NET version 2.5 or above.  Install it using the Web platform installer.
* A Data Lake Analytics account.  See [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).
* Go through the [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md) tutorial.
* Connect to Azure.
* Upload the source data, see [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md). 

## <a name="develop-assemblies-for-u-sql"></a>Develop assemblies for U-SQL

**To create and submit a U-SQL job**

1. From the **File** menu, click **New**, and then click **Project**.
2. Expand **Installed**, **Templates**, **Azure Data Lake**, **U-SQL(ADLA)**, select the **Class Library (For U-SQL Application)** template, and then click **OK**.
3. Write your code in Class1.cs.  The following is a code sample.

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
4. Click the **Build** menu, and then click **Build Solution** to create the dll.

## <a name="register-assemblies"></a>Register assemblies

See [Use Data Lake Analytics(U-SQL) catalog](data-lake-analytics-use-u-sql-catalog.md).


## <a name="use-the-assemblies"></a>Use the assemblies

See [Use the Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).

## <a name="see-also"></a>See also
* [Get started with Data Lake Analytics using PowerShell](data-lake-analytics-get-started-powershell.md)
* [Get started with Data Lake Analytics using the Azure portal](data-lake-analytics-get-started-portal.md)
* [Use Data Lake Tools for Visual Studio for developing U-SQL applications](data-lake-analytics-data-lake-tools-get-started.md)
* [Use Data Lake Analytics(U-SQL) catalog](data-lake-analytics-use-u-sql-catalog.md)
* [Use the Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md)