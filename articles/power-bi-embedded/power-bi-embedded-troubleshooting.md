---
title: Microsoft Power BI Embedded Preview troubleshooting
description: Microsoft Power BI Embedded Preview troubleshooting
services: power-bi-embedded
documentationcenter: ''
author: guyinacube
manager: erikre
editor: ''
tags: ''
ms.assetid: c8aee652-ed8b-4c66-9c63-f798b7a655b4
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: f406d23e578acc825514aa5bd9eabcbf160bf9ec
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669799"
---
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a>Microsoft Power BI Embedded Preview troubleshooting
This article provides answers for how  to troubleshoot **Power BI Embedded**.

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a>Setting SQL Server connection strings
To set a SQL Server connecting string, you need to follow a specific format. Below is an example connection string for SQL Server.

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

To learn more about SQL Server connection strings, see the following articles:

* [SQL Server Connection Strings](https://msdn.microsoft.com/library/jj653752.aspx)
* [SqlConnection.ConnectionString](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a>Setting credentials
In the case where you have credentials for a development or staging environment, such as user name and password, you might need to update credentials that match a production solution.

## <a name="see-also"></a>See Also
* [Get started with sample](power-bi-embedded-get-started-sample.md)
* [What is Power BI Embedded](power-bi-embedded-what-is-power-bi-embedded.md)

