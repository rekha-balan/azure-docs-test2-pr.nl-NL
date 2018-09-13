---
title: Use Azure Stream Analytics with SQL Data Warehouse | Microsoft Docs
description: Tips for using Azure Stream Analytics with Azure SQL Data Warehouse for developing solutions.
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: barbkess
editor: ''
ms.assetid: 8aeb2247-20c5-4a29-b327-30a8ce09dfdc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 99adddc04c5c0826fc4e57ded81729c3ed127d9d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563586"
---
# <a name="use-azure-stream-analytics-with-sql-data-warehouse"></a>Use Azure Stream Analytics with SQL Data Warehouse
Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable complex event processing over streaming data in the cloud. You can learn the basics by reading [Introduction to Azure Stream Analytics][Introduction to Azure Stream Analytics]. You can then learn how to create an end-to-end solution with Stream Analytics by following the [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.

In this article, you will learn how to use your Azure SQL Data Warehouse database as an output sink for your Steam Analytics jobs.

## <a name="prerequisites"></a>Prerequisites
First, run through the following steps in the [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.  

1. Create an Event Hub input
2. Configure and start event generator application
3. Provision a Stream Analytics job
4. Specify job input and query

Then, create an Azure SQL Data Warehouse database

## <a name="specify-job-output-azure-sql-data-warehouse-database"></a>Specify job output: Azure SQL Data Warehouse database
### <a name="step-1"></a>Step 1
In your Stream Analytics job click **OUTPUT** from the top of the page, and then click **ADD OUTPUT**.

### <a name="step-2"></a>Step 2
Select SQL Database and click next.

![][add-output]

### <a name="step-3"></a>Step 3
Enter the following values on the next page:

* *Output Alias*: Enter a friendly name for this job output.
* *Subscription*:
  * If your SQL Data Warehouse database is in the same subscription as the Stream Analytics job, select Use SQL Database from Current Subscription.
  * If your database is in a different subscription, select Use SQL Database from Another Subscription.
* *Database*: Specify the name of a destination database.
* *Server Name*: Specify the server name for the database you just specified. You can use the Azure Classic Portal to find this.

![][server-name]

* *User Name*: Specify the user name of an account that has write permissions for the database.
* *Password*: Provide the password for the specified user account.
* *Table*: Specify the name of the target table in the database.

![][add-database]

### <a name="step-4"></a>Step 4
Click the check button to add this job output and to verify that Stream Analytics can successfully connect to the database.

![][test-connection]

When the connection to the database succeeds, you will see a notification at the bottom of the portal. You can click Test Connection at the bottom to test the connection to the database.

## <a name="next-steps"></a>Next steps
For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].

For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].

<!--Image references-->

[add-output]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-integrate-azure-stream-analytics/add-output.png
[server-name]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-integrate-azure-stream-analytics/dw-server-name.png
[add-database]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-integrate-azure-stream-analytics/add-database.png
[test-connection]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-integrate-azure-stream-analytics/test-connection.png

<!--Article references-->

[Introduction to Azure Stream Analytics]: ../stream-analytics/stream-analytics-introduction.md
[Get started using Azure Stream Analytics]: ../stream-analytics/stream-analytics-get-started.md
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Stream Analytics documentation]: http://azure.microsoft.com/documentation/services/stream-analytics/




