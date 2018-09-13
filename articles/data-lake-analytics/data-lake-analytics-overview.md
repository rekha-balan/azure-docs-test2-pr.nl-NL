---
title: Overview of Microsoft Azure Data Lake Analytics | Microsoft Docs
description: Data Lake Analytics is an Azure Big Data service that lets you use data to drive your business using insights gained from your data in the cloud, regardless its size or where it is.
services: data-lake-analytics
documentationcenter: ''
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 1e1d443a-48a2-47fb-bc00-bf88274222de
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/28/2017
ms.author: edmaca
ms.openlocfilehash: b74c0c5c9c5bd2b643dcbe7798af226b3434bb72
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564498"
---
# <a name="overview-of-microsoft-azure-data-lake-analytics"></a>Overview of Microsoft Azure Data Lake Analytics
## <a name="what-is-azure-data-lake-analytics"></a>What is Azure Data Lake Analytics?
Azure Data Lake Analytics ia an on-demand analytics job service to simplify big data analytics. Focus on writing, running, and managing jobs rather than on operating distributed infrastructure. Instead of deploying, configuring, and tuning hardware, you write queries to transform your data and extract valuable insights. The analytics service can handle jobs of any scale instantly by setting the dial for how much power you need. You only pay for your job when it is running, making it cost-effective. The analytics service supports Azure Active Directory letting you manage access and roles, integrated with your on-premises identity system. It also includes U-SQL, a language that unifies the benefits of SQL with the expressive power of user code. U-SQL’s scalable distributed runtime enables you to efficiently analyze data in the store and across SQL Servers in Azure, Azure SQL Database, and Azure SQL Data Warehouse.

## <a name="key-capabilities"></a>Key capabilities
* **Dynamic scaling**
  
    Data Lake Analytics is architected for cloud scale and performance.  It dynamically provisions resources and lets you do analytics on terabytes or even exabytes of data. When the job completes, it winds down resources automatically, and you pay only for the processing power used. As you increase or decrease the size of data stored or the amount of compute used, you don’t have to rewrite code. You can focus on your business logic only and not on how you process and store large datasets.
* **Develop faster, debug, and optimize smarter using familiar tools**
  
    Data Lake Analytics has deep integration with Visual Studio, so that you can use familiar tools to run, debug, and tune your code. Visualizations of your U-SQL jobs let you see how your code runs at scale, so you can easily identify performance bottlenecks and optimize costs.
* **U-SQL: simple and familiar, powerful, and extensible**
  
    Data Lake Analytics includes U-SQL, a query language that extends the familiar, simple, declarative nature of SQL with the expressive power of C#. The U-SQL language is built on the same distributed runtime that powers the big data systems inside Microsoft. Millions of SQL and .NET developers can now process and analyze their data with the skills they already have.
* **Integrates seamlessly with your IT investments**
  
    Data Lake Analytics can use your existing IT investments for identity, management, security, and data warehousing. This simplifies data governance and makes it easy to extend your current data applications. Data Lake Analytics is integrated with Active Directory for user management and permissions and comes with built-in monitoring and auditing.
* **Affordable and cost effective**
  
    Data Lake Analytics is a cost-effective solution for running big data workloads. You pay on a per-job basis when data is processed. No hardware, licenses, or service-specific support agreements are required. The system automatically scales up or down as the job starts and completes, meaning that you never pay for more than what you need.
* **Works with all your Azure Data**
  
    Data Lake Analytics is optimized to work with Azure Data Lake - providing the highest level of performance, throughput, and parallelization for your big data workloads.  Data Lake Analytics can also work with Azure Blob storage and Azure SQL database.

## <a name="see-also"></a>See also
* Get started
  
  * [Get started with Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md)
  * [Get started with Data Lake Analytics using Azure PowerShell](data-lake-analytics-get-started-powershell.md)
  * [Get started with Data Lake Analytics using Azure .NET SDK](data-lake-analytics-get-started-net-sdk.md)
  * [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
  * [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md)
* U-SQL & development
  
  * [Use U-SQL window functions for Azure Data Lake Analytics jobs](data-lake-analytics-use-window-functions.md)
  * [Develop U-SQL user-defined operators for Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-user-defined-operators.md)
* Management
  
  * [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md)
  * [Manage Azure Data Lake Analytics using Azure PowerShell](data-lake-analytics-manage-use-powershell.md)
  * [Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
  * [Accessing Diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)
* End-to-end tutorial
  
  * [Use Azure Data Lake Analytics interactive tutorials](data-lake-analytics-use-interactive-tutorials.md)
  * [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md)
* Let us know what you think
  
  <!-- Fixing broken links for Azure content migration from ACOM to DOCS. I can't find a suitable substitute for what appears to be a link that is no longer available. I am commenting out for now. The author can investigate in the future. Hyperlink text: Comment on our documentation backlog. Referenced file: data-lake-analytics-documentation-backlog.md -->
  * [Submit a feature request](http://aka.ms/adlafeedback)
  * [Get help in the forums](http://aka.ms/adlaforums)

