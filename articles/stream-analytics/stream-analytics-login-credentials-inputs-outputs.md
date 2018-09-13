---
title: 'Stream Analytics: Rotate log-in credentials for inputs and outputs | Microsoft Docs'
description: Learn how to update the credentials for Stream Analytics inputs and outputs.
keywords: login credentials
services: stream-analytics
documentationcenter: ''
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42ae83e1-cd33-49bb-a455-a39a7c151ea4
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: d6b0d6b0d319e5a1e4716c6c239d7d196c0cd386
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554711"
---
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a>Rotate login credentials for inputs and outputs in Stream Analytics Jobs
## <a name="abstract"></a>Abstract
Azure Stream Analytics today doesn’t allow replacing the credentials on an input/output while the job is running.

While Azure Stream Analytics does support resuming a job from last output, we wanted to share the entire process for minimizing the lag between the stopping and starting of the job and rotating the login credentials.

## <a name="part-1---prepare-the-new-set-of-credentials"></a>Part 1 - Prepare the new set of credentials:
This part is applicable to the following inputs/outputs:

* Blob Storage
* Event Hubs
* SQL Database
* Table Storage

For other inputs/outputs, proceed with Part 2.

### <a name="blob-storagetable-storage"></a>Blob storage/Table storage
1. Go to the Storage extention on the Azure Management portal:  
   ![graphic1][graphic1]
2. Locate the storage used by your job and go into it:  
   ![graphic2][graphic2]
3. Click the Manage Access Keys command:  
   ![graphic3][graphic3]
4. Between the Primary Access Key and the Secondary Access Key, **pick the one not used by your job**.
5. Hit regenerate:  
   ![graphic4][graphic4]
6. Copy the newly generated key:  
   ![graphic5][graphic5]
7. Continue to Part 2.

### <a name="event-hubs"></a>Event hubs
1. Go to the Service Bus extension on the Azure Management portal:  
   ![graphic6][graphic6]
2. Locate the Service Bus Namespace used by your job and go into it:  
   ![graphic7][graphic7]
3. If your job uses a shared access policy on the Service Bus Namespace, jump to step 6  
4. Go to the Event Hubs tab:  
   ![graphic8][graphic8]
5. Locate the Event Hub used by your job and go into it:  
   ![graphic9][graphic9]
6. Go to the Configure Tab:  
   ![graphic10][graphic10]
7. On the Policy Name drop-down, locate the shared access policy used by your job:  
   ![graphic11][graphic11]
8. Between the Primary Key and the Secondary Key, **pick the one not used by your job**.  
9. Hit regenerate:  
   ![graphic12][graphic12]
10. Copy the newly generated key:  
   ![graphic13][graphic13]
11. Continue to Part 2.  

### <a name="sql-database"></a>SQL Database
> [!NOTE]
> Note: you will need to connect to the SQL Database Service. We are going to show how to do this using the management experience on the Azure Management portal but you may choose to use some client-side tool such as SQL Server Management Studio as well.
>
> 

1. Go to the SQL Databases extension on the Azure Management portal:  
   ![graphic14][graphic14]
2. Locate the SQL Database used by your job and **click on the server** link on the same line:  
   ![graphic15][graphic15]
3. Click the Manage command:  
   ![graphic16][graphic16]
4. Type Database Master:  
   ![graphic17][graphic17]
5. Type in your User Name, Password, and click Log on:  
   ![graphic18][graphic18]
6. Click New Query:  
   ![graphic19][graphic19]
7. Type in the following query replacing <login_name> with your User Name and replacing <enterStrongPasswordHere> with your new password:  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. Click Run:  
   ![graphic20][graphic20]
9. Go back to step 2 and this time click the database:  
   ![graphic21][graphic21]
10. Click the Manage command:  
   ![graphic22][graphic22]
11. type in your User Name, Password, and click Logon:  
   ![graphic23][graphic23]
12. Click New Query:  
   ![graphic24][graphic24]
13. Type in the following query replacing <user_name> with a name by which you want to identify this login in the context of this database (you can provide the same value you gave for <login_name>, for example) and replacing <login_name> with your new user name:  
   `CREATE USER <user_name> FROM LOGIN <login_name>`
14. Click Run:  
   ![graphic25][graphic25]
15. You should now provide your new user with the same roles and privileges your original user had.
16. Continue to Part 2.

## <a name="part-2-stopping-the-stream-analytics-job"></a>Part 2: Stopping the Stream Analytics Job
1. Go to the Stream Analytics extension on the Azure Management portal:  
   ![graphic26][graphic26]
2. Locate your job and go into it:  
   ![graphic27][graphic27]
3. Go to the Inputs tab or the Outputs tab based on whether you are rotating the credentials on an Input or on an Output.  
   ![graphic28][graphic28]
4. Click the Stop command and confirm the job has stopped:  
   ![graphic29][graphic29] Wait for the job to stop.
5. Locate the input/output you want to rotate credentials on and go into it:  
   ![graphic30][graphic30]
6. Proceed to Part 3.

## <a name="part-3-editing-the-credentials-on-the-stream-analytics-job"></a>Part 3: Editing the credentials on the Stream Analytics Job
### <a name="blob-storagetable-storage"></a>Blob storage/Table storage
1. Find the Storage Account Key field and paste your newly generated key into it:  
   ![graphic31][graphic31]
2. Click the Save command and confirm saving your changes:  
   ![graphic32][graphic32]
3. A connection test will automatically start when you save your changes, make sure that is has successfully passed.
4. Proceed to Part 4.

### <a name="event-hubs"></a>Event hubs
1. Find the Event Hub Policy Key field and paste your newly generated key into it:  
   ![graphic33][graphic33]
2. Click the Save command and confirm saving your changes:  
   ![graphic34][graphic34]
3. A connection test will automatically start when you save your changes, make sure that it has successfully passed.
4. Proceed to Part 4.

### <a name="power-bi"></a>Power BI
1. Click the Renew authorization:  

   ![graphic35][graphic35]
2. You will get the following confirmation:  

   ![graphic36][graphic36]
3. Click the Save command and confirm saving your changes:  
   ![graphic37][graphic37]
4. A connection test will automatically start when you save your changes, make sure it has successfully passed.
5. Proceed to Part 4.

### <a name="sql-database"></a>SQL Database
1. Find the User Name and Password fields and paste your newly created set of credentials into them:  
   ![graphic38][graphic38]
2. Click the Save command and confirm saving your changes:  
   ![graphic39][graphic39]
3. A connection test will automatically start when you save your changes, make sure that it has successfully passed.  
4. Proceed to Part 4.

## <a name="part-4-starting-your-job-from-last-stopped-time"></a>Part 4: Starting your job from last stopped time
1. Navigate away from the Input/Output:  
   ![graphic40][graphic40]
2. Click the Start command:  
   ![graphic41][graphic41]
3. Pick the Last Stopped Time and click OK:  
   ![graphic42][graphic42]
4. Proceed to Part 5.  

## <a name="part-5-removing-the-old-set-of-credentials"></a>Part 5: Removing the old set of credentials
This part is applicable to the following inputs/outputs:

* Blob Storage
* Event Hubs
* SQL Database
* Table Storage

### <a name="blob-storagetable-storage"></a>Blob storage/Table storage
Repeat Part 1 for the Access Key that was previously used by your job to renew the now unused Access Key.

### <a name="event-hubs"></a>Event hubs
Repeat Part 1 for the Key that was previously used by your job to renew the now unused Key.

### <a name="sql-database"></a>SQL Database
1. Go back to the query window from Part 1 Step 7 and type in the following query, replacing <previous_login_name> with the User Name that was previously used by your job:  
   `DROP LOGIN <previous_login_name>`  
2. Click Run:  
   ![graphic43][graphic43]  

You should get the following confirmation: 

    Command(s) completed successfully.

## <a name="get-help"></a>Get help
For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Next steps
* [Introduction to Azure Stream Analytics](stream-analytics-introduction.md)
* [Get started using Azure Stream Analytics](stream-analytics-get-started.md)
* [Scale Azure Stream Analytics jobs](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[graphic1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/1-stream-analytics-login-credentials-inputs-outputs.png
[graphic2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/2-stream-analytics-login-credentials-inputs-outputs.png
[graphic3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/3-stream-analytics-login-credentials-inputs-outputs.png
[graphic4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/4-stream-analytics-login-credentials-inputs-outputs.png
[graphic5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/5-stream-analytics-login-credentials-inputs-outputs.png
[graphic6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/6-stream-analytics-login-credentials-inputs-outputs.png
[graphic7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/7-stream-analytics-login-credentials-inputs-outputs.png
[graphic8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/8-stream-analytics-login-credentials-inputs-outputs.png
[graphic9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/9-stream-analytics-login-credentials-inputs-outputs.png
[graphic10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/10-stream-analytics-login-credentials-inputs-outputs.png
[graphic11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/11-stream-analytics-login-credentials-inputs-outputs.png
[graphic12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/12-stream-analytics-login-credentials-inputs-outputs.png
[graphic13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/13-stream-analytics-login-credentials-inputs-outputs.png
[graphic14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/14-stream-analytics-login-credentials-inputs-outputs.png
[graphic15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/15-stream-analytics-login-credentials-inputs-outputs.png
[graphic16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/16-stream-analytics-login-credentials-inputs-outputs.png
[graphic17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/17-stream-analytics-login-credentials-inputs-outputs.png
[graphic18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/18-stream-analytics-login-credentials-inputs-outputs.png
[graphic19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/19-stream-analytics-login-credentials-inputs-outputs.png
[graphic20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/20-stream-analytics-login-credentials-inputs-outputs.png
[graphic21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/21-stream-analytics-login-credentials-inputs-outputs.png
[graphic22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/22-stream-analytics-login-credentials-inputs-outputs.png
[graphic23]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/23-stream-analytics-login-credentials-inputs-outputs.png
[graphic24]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/24-stream-analytics-login-credentials-inputs-outputs.png
[graphic25]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/25-stream-analytics-login-credentials-inputs-outputs.png
[graphic26]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/26-stream-analytics-login-credentials-inputs-outputs.png
[graphic27]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/27-stream-analytics-login-credentials-inputs-outputs.png
[graphic28]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/28-stream-analytics-login-credentials-inputs-outputs.png
[graphic29]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/29-stream-analytics-login-credentials-inputs-outputs.png
[graphic30]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/30-stream-analytics-login-credentials-inputs-outputs.png
[graphic31]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/31-stream-analytics-login-credentials-inputs-outputs.png
[graphic32]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/32-stream-analytics-login-credentials-inputs-outputs.png
[graphic33]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/33-stream-analytics-login-credentials-inputs-outputs.png
[graphic34]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/34-stream-analytics-login-credentials-inputs-outputs.png
[graphic35]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/35-stream-analytics-login-credentials-inputs-outputs.png
[graphic36]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/36-stream-analytics-login-credentials-inputs-outputs.png
[graphic37]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/37-stream-analytics-login-credentials-inputs-outputs.png
[graphic38]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/38-stream-analytics-login-credentials-inputs-outputs.png
[graphic39]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/39-stream-analytics-login-credentials-inputs-outputs.png
[graphic40]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/40-stream-analytics-login-credentials-inputs-outputs.png
[graphic41]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/41-stream-analytics-login-credentials-inputs-outputs.png
[graphic42]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/42-stream-analytics-login-credentials-inputs-outputs.png
[graphic43]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-login-credentials-inputs-outputs/43-stream-analytics-login-credentials-inputs-outputs.png












































