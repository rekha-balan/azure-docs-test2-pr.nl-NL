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
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a><span data-ttu-id="970ca-103">Microsoft Power BI Embedded Preview troubleshooting</span><span class="sxs-lookup"><span data-stu-id="970ca-103">Microsoft Power BI Embedded Preview troubleshooting</span></span>
<span data-ttu-id="970ca-104">This article provides answers for how  to troubleshoot **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="970ca-104">This article provides answers for how  to troubleshoot **Power BI Embedded**.</span></span>

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a><span data-ttu-id="970ca-105">Setting SQL Server connection strings</span><span class="sxs-lookup"><span data-stu-id="970ca-105">Setting SQL Server connection strings</span></span>
<span data-ttu-id="970ca-106">To set a SQL Server connecting string, you need to follow a specific format.</span><span class="sxs-lookup"><span data-stu-id="970ca-106">To set a SQL Server connecting string, you need to follow a specific format.</span></span> <span data-ttu-id="970ca-107">Below is an example connection string for SQL Server.</span><span class="sxs-lookup"><span data-stu-id="970ca-107">Below is an example connection string for SQL Server.</span></span>

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

<span data-ttu-id="970ca-108">To learn more about SQL Server connection strings, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="970ca-108">To learn more about SQL Server connection strings, see the following articles:</span></span>

* [<span data-ttu-id="970ca-109">SQL Server Connection Strings</span><span class="sxs-lookup"><span data-stu-id="970ca-109">SQL Server Connection Strings</span></span>](https://msdn.microsoft.com/library/jj653752.aspx)
* [<span data-ttu-id="970ca-110">SqlConnection.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="970ca-110">SqlConnection.ConnectionString</span></span>](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a><span data-ttu-id="970ca-111">Setting credentials</span><span class="sxs-lookup"><span data-stu-id="970ca-111">Setting credentials</span></span>
<span data-ttu-id="970ca-112">In the case where you have credentials for a development or staging environment, such as user name and password, you might need to update credentials that match a production solution.</span><span class="sxs-lookup"><span data-stu-id="970ca-112">In the case where you have credentials for a development or staging environment, such as user name and password, you might need to update credentials that match a production solution.</span></span>

## <a name="see-also"></a><span data-ttu-id="970ca-113">See Also</span><span class="sxs-lookup"><span data-stu-id="970ca-113">See Also</span></span>
* [<span data-ttu-id="970ca-114">Get started with sample</span><span class="sxs-lookup"><span data-stu-id="970ca-114">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)
* [<span data-ttu-id="970ca-115">What is Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="970ca-115">What is Power BI Embedded</span></span>](power-bi-embedded-what-is-power-bi-embedded.md)

