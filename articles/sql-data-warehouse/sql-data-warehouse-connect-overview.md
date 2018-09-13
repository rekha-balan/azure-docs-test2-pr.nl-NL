---
title: Connect to Azure SQL Data Warehouse | Microsoft Docs
description: How to find the server name and connection string for your to Azure SQL Data Warehouse
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: ''
ms.assetid: e52872ca-ae74-4e25-9c56-d49c85c8d0f0
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: barbkess
ms.openlocfilehash: dd758376c28a4941b04777e578244a6cb20d1055
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563576"
---
# <a name="connect-to-azure-sql-data-warehouse"></a>Connect to Azure SQL Data Warehouse
This article helps you get connected to SQL Data Warehouse for the first time.

## <a name="find-your-server-name"></a>Find your server name
The first step to connecting to SQL Data Warehouse is knowing how to find your server name.  For example, the server name in the following example is sample.database.windows.net. To find the fully qualified server name:

1. Go to the [Azure portal][Azure portal].
2. Click on **SQL databases** 
3. Click on the database you want to connect to.
4. Locate the full server name.
   
    ![Full server name][1]

## <a name="supported-drivers-and-connection-strings"></a>Supported drivers and connection strings
Azure SQL Data Warehouse supports [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP][PHP], and [JDBC][JDBC]. Click on one of the preceding drivers to find the latest version and documentation. To automatically generate the connection string for the driver that you are using from the Azure portal, you can click on the **Show database connection strings** from the preceding example.  Following are also some examples of what a connection string looks like for each driver.

> [!NOTE]
> Consider setting the connection timeout to 300 seconds to allow your connection to survive short periods of unavailability.
> 
> 

### <a name="adonet-connection-string-example"></a>ADO.NET connection string example
```C#
Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};User ID={your_user_name};Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
```

### <a name="odbc-connection-string-example"></a>ODBC connection string example
```C#
Driver={SQL Server Native Client 11.0};Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};Uid={your_user_name};Pwd={your_password_here};Encrypt=yes;TrustServerCertificate=no;Connection Timeout=30;
```

### <a name="php-connection-string-example"></a>PHP connection string example
```PHP
Server: {your_server}.database.windows.net,1433 \r\nSQL Database: {your_database}\r\nUser Name: {your_user_name}\r\n\r\nPHP Data Objects(PDO) Sample Code:\r\n\r\ntry {\r\n   $conn = new PDO ( \"sqlsrv:server = tcp:{your_server}.database.windows.net,1433; Database = {your_database}\", \"{your_user_name}\", \"{your_password_here}\");\r\n    $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );\r\n}\r\ncatch ( PDOException $e ) {\r\n   print( \"Error connecting to SQL Server.\" );\r\n   die(print_r($e));\r\n}\r\n\rSQL Server Extension Sample Code:\r\n\r\n$connectionInfo = array(\"UID\" => \"{your_user_name}\", \"pwd\" => \"{your_password_here}\", \"Database\" => \"{your_database}\", \"LoginTimeout\" => 30, \"Encrypt\" => 1, \"TrustServerCertificate\" => 0);\r\n$serverName = \"tcp:{your_server}.database.windows.net,1433\";\r\n$conn = sqlsrv_connect($serverName, $connectionInfo);
```

### <a name="jdbc-connection-string-example"></a>JDBC connection string example
```Java
jdbc:sqlserver://yourserver.database.windows.net:1433;database=yourdatabase;user={your_user_name};password={your_password_here};encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
```

## <a name="connection-settings"></a>Connection settings
SQL Data Warehouse standardizes some settings during connection and object creation. These settings cannot be overridden and include:

| Database Setting | Value |
|:--- |:--- |
| [ANSI_NULLS][ANSI_NULLS] |ON |
| [QUOTED_IDENTIFIERS][QUOTED_IDENTIFIERS] |ON |
| [DATEFORMAT][DATEFORMAT] |mdy |
| [DATEFIRST][DATEFIRST] |7 |

## <a name="next-steps"></a>Next steps
To connect and query with Visual Studio, see [Query with Visual Studio][Query with Visual Studio]. To learn more about authentication options, see [Authentication to Azure SQL Data Warehouse][Authentication to Azure SQL Data Warehouse].

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
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-connect-overview/get-server-name.png



