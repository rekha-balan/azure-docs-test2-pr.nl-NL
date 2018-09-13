---
title: Connect to Azure SQL Data Warehouse | Microsoft Docs
description: Get connected to Azure SQL Data Warehouse.
services: sql-data-warehouse
author: kavithaj
manager: craigg
ms.service: sql-data-warehouse
ms.topic: conceptual
ms.component: consume
ms.date: 04/17/2018
ms.author: kavithaj
ms.reviewer: igorstan
ms.openlocfilehash: 0b2d8cec03c54ebd5bd780a2524da61d718a9673
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44783419"
---
# <a name="connect-to-azure-sql-data-warehouse"></a><span data-ttu-id="c1618-103">Connect to Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c1618-103">Connect to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="c1618-104">Get connected to Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c1618-104">Get connected to Azure SQL Data Warehouse.</span></span>

## <a name="find-your-server-name"></a><span data-ttu-id="c1618-105">Find your server name</span><span class="sxs-lookup"><span data-stu-id="c1618-105">Find your server name</span></span>
<span data-ttu-id="c1618-106">The server name in the following example is samplesvr.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="c1618-106">The server name in the following example is samplesvr.database.windows.net.</span></span> <span data-ttu-id="c1618-107">To find the fully qualified server name:</span><span class="sxs-lookup"><span data-stu-id="c1618-107">To find the fully qualified server name:</span></span>

1. <span data-ttu-id="c1618-108">Go to the [Azure portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="c1618-108">Go to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="c1618-109">Click on **SQL data warehouses**.</span><span class="sxs-lookup"><span data-stu-id="c1618-109">Click on **SQL data warehouses**.</span></span>
3. <span data-ttu-id="c1618-110">Click on the data warehouse you want to connect to.</span><span class="sxs-lookup"><span data-stu-id="c1618-110">Click on the data warehouse you want to connect to.</span></span>
4. <span data-ttu-id="c1618-111">Locate the full server name.</span><span class="sxs-lookup"><span data-stu-id="c1618-111">Locate the full server name.</span></span>
   
    ![Full server name][1]

## <a name="supported-drivers-and-connection-strings"></a><span data-ttu-id="c1618-113">Supported drivers and connection strings</span><span class="sxs-lookup"><span data-stu-id="c1618-113">Supported drivers and connection strings</span></span>
<span data-ttu-id="c1618-114">Azure SQL Data Warehouse supports [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP][PHP], and [JDBC][JDBC].</span><span class="sxs-lookup"><span data-stu-id="c1618-114">Azure SQL Data Warehouse supports [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP][PHP], and [JDBC][JDBC].</span></span> <span data-ttu-id="c1618-115">To find the latest version and documentation, click on one of the preceding drivers.</span><span class="sxs-lookup"><span data-stu-id="c1618-115">To find the latest version and documentation, click on one of the preceding drivers.</span></span> <span data-ttu-id="c1618-116">To automatically generate the connection string for the driver that you are using from the Azure portal, click on the **Show database connection strings** from the preceding example.</span><span class="sxs-lookup"><span data-stu-id="c1618-116">To automatically generate the connection string for the driver that you are using from the Azure portal, click on the **Show database connection strings** from the preceding example.</span></span> <span data-ttu-id="c1618-117">Following are also some examples of what a connection string looks like for each driver.</span><span class="sxs-lookup"><span data-stu-id="c1618-117">Following are also some examples of what a connection string looks like for each driver.</span></span>

> [!NOTE]
> <span data-ttu-id="c1618-118">Consider setting the connection timeout to 300 seconds to allow your connection to survive short periods of unavailability.</span><span class="sxs-lookup"><span data-stu-id="c1618-118">Consider setting the connection timeout to 300 seconds to allow your connection to survive short periods of unavailability.</span></span>
> 
> 

### <a name="adonet-connection-string-example"></a><span data-ttu-id="c1618-119">ADO.NET connection string example</span><span class="sxs-lookup"><span data-stu-id="c1618-119">ADO.NET connection string example</span></span>
```csharp
Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};User ID={your_user_name};Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
```

### <a name="odbc-connection-string-example"></a><span data-ttu-id="c1618-120">ODBC connection string example</span><span class="sxs-lookup"><span data-stu-id="c1618-120">ODBC connection string example</span></span>
```csharp
Driver={SQL Server Native Client 11.0};Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};Uid={your_user_name};Pwd={your_password_here};Encrypt=yes;TrustServerCertificate=no;Connection Timeout=30;
```

### <a name="php-connection-string-example"></a><span data-ttu-id="c1618-121">PHP connection string example</span><span class="sxs-lookup"><span data-stu-id="c1618-121">PHP connection string example</span></span>
```PHP
Server: {your_server}.database.windows.net,1433 \r\nSQL Database: {your_database}\r\nUser Name: {your_user_name}\r\n\r\nPHP Data Objects(PDO) Sample Code:\r\n\r\ntry {\r\n   $conn = new PDO ( \"sqlsrv:server = tcp:{your_server}.database.windows.net,1433; Database = {your_database}\", \"{your_user_name}\", \"{your_password_here}\");\r\n    $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );\r\n}\r\ncatch ( PDOException $e ) {\r\n   print( \"Error connecting to SQL Server.\" );\r\n   die(print_r($e));\r\n}\r\n\rSQL Server Extension Sample Code:\r\n\r\n$connectionInfo = array(\"UID\" => \"{your_user_name}\", \"pwd\" => \"{your_password_here}\", \"Database\" => \"{your_database}\", \"LoginTimeout\" => 30, \"Encrypt\" => 1, \"TrustServerCertificate\" => 0);\r\n$serverName = \"tcp:{your_server}.database.windows.net,1433\";\r\n$conn = sqlsrv_connect($serverName, $connectionInfo);
```

### <a name="jdbc-connection-string-example"></a><span data-ttu-id="c1618-122">JDBC connection string example</span><span class="sxs-lookup"><span data-stu-id="c1618-122">JDBC connection string example</span></span>
```Java
jdbc:sqlserver://yourserver.database.windows.net:1433;database=yourdatabase;user={your_user_name};password={your_password_here};encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
```

## <a name="connection-settings"></a><span data-ttu-id="c1618-123">Connection settings</span><span class="sxs-lookup"><span data-stu-id="c1618-123">Connection settings</span></span>
<span data-ttu-id="c1618-124">SQL Data Warehouse standardizes some settings during connection and object creation.</span><span class="sxs-lookup"><span data-stu-id="c1618-124">SQL Data Warehouse standardizes some settings during connection and object creation.</span></span> <span data-ttu-id="c1618-125">These settings cannot be overridden and include:</span><span class="sxs-lookup"><span data-stu-id="c1618-125">These settings cannot be overridden and include:</span></span>

| <span data-ttu-id="c1618-126">Database Setting</span><span class="sxs-lookup"><span data-stu-id="c1618-126">Database Setting</span></span> | <span data-ttu-id="c1618-127">Value</span><span class="sxs-lookup"><span data-stu-id="c1618-127">Value</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1618-128">[ANSI_NULLS][ANSI_NULLS]</span><span class="sxs-lookup"><span data-stu-id="c1618-128">[ANSI_NULLS][ANSI_NULLS]</span></span> |<span data-ttu-id="c1618-129">ON</span><span class="sxs-lookup"><span data-stu-id="c1618-129">ON</span></span> |
| <span data-ttu-id="c1618-130">[QUOTED_IDENTIFIERS][QUOTED_IDENTIFIERS]</span><span class="sxs-lookup"><span data-stu-id="c1618-130">[QUOTED_IDENTIFIERS][QUOTED_IDENTIFIERS]</span></span> |<span data-ttu-id="c1618-131">ON</span><span class="sxs-lookup"><span data-stu-id="c1618-131">ON</span></span> |
| <span data-ttu-id="c1618-132">[DATEFORMAT][DATEFORMAT]</span><span class="sxs-lookup"><span data-stu-id="c1618-132">[DATEFORMAT][DATEFORMAT]</span></span> |<span data-ttu-id="c1618-133">mdy</span><span class="sxs-lookup"><span data-stu-id="c1618-133">mdy</span></span> |
| <span data-ttu-id="c1618-134">[DATEFIRST][DATEFIRST]</span><span class="sxs-lookup"><span data-stu-id="c1618-134">[DATEFIRST][DATEFIRST]</span></span> |<span data-ttu-id="c1618-135">7</span><span class="sxs-lookup"><span data-stu-id="c1618-135">7</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c1618-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="c1618-136">Next steps</span></span>
<span data-ttu-id="c1618-137">To connect and query with Visual Studio, see [Query with Visual Studio][Query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="c1618-137">To connect and query with Visual Studio, see [Query with Visual Studio][Query with Visual Studio].</span></span> <span data-ttu-id="c1618-138">To learn more about authentication options, see [Authentication to Azure SQL Data Warehouse][Authentication to Azure SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="c1618-138">To learn more about authentication options, see [Authentication to Azure SQL Data Warehouse][Authentication to Azure SQL Data Warehouse].</span></span>

<!--Articles-->
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[Authentication to Azure SQL Data Warehouse]: ./sql-data-warehouse-authentication.md

<!--MSDN references-->
[ADO.NET]: https://msdn.microsoft.com/library/e80y5yhx(v=vs.110).aspx
[ODBC]: https://msdn.microsoft.com/library/jj730314.aspx
[PHP]: https://msdn.microsoft.com/library/cc296172.aspx?f=255&MSPPError=-2147217396
[JDBC]: https://msdn.microsoft.com/library/mt484311(v=sql.110).aspx
[ANSI_NULLS]: https://msdn.microsoft.com/library/ms188048.aspx
[QUOTED_IDENTIFIERS]: https://msdn.microsoft.com/library/ms174393.aspx
[DATEFORMAT]: https://msdn.microsoft.com/library/ms189491.aspx
[DATEFIRST]: https://msdn.microsoft.com/library/ms181598.aspx

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->
[1]: media/sql-data-warehouse-connect-overview/server-connect.PNG


