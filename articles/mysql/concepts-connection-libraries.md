---
title: Connection libraries for Azure Database for MySQL
description: This article lists each library or driver that client programs can use when connecting to Azure Database for MySQL.
services: mysql
author: ajlam
ms.author: andrela
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.topic: article
ms.date: 02/28/2018
ms.openlocfilehash: 3f49065d4f66f55ed728626764d9cac2aa5c3c69
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865898"
---
# <a name="connection-libraries-for-azure-database-for-mysql"></a>Connection libraries for Azure Database for MySQL
This article lists each library or driver that client programs can use when connecting to Azure Database for MySQL.

## <a name="client-interfaces"></a>Client interfaces
MySQL offers standard database driver connectivity for using MySQL with applications and tools that are compatible with industry standards ODBC and JDBC. Any system that works with ODBC or JDBC can use MySQL.

| **Language** | **Platform** | **Additional Resource** | **Download** |
| :----------- | :------------| :-----------------------| :------------|
| PHP | Windows, Linux | [MySQL native driver for PHP - mysqlnd](https://dev.mysql.com/downloads/connector/php-mysqlnd/) | [Download](http://php.net/downloads.php) |
| ODBC | Windows, Linux, Mac OS X, and Unix platforms | [MySQL Connector/ODBC Developer Guide](https://dev.mysql.com/doc/connector-odbc/en/) | [Download](https://dev.mysql.com/downloads/connector/odbc/) |
| ADO.NET | Windows | [MySQL Connector/Net Developer Guide](https://dev.mysql.com/doc/connector-net/en/) | [Download](https://dev.mysql.com/downloads/connector/net/) |
| JDBC | Platform independent | [MySQL Connector/J 5.1 Developer Guide](https://dev.mysql.com/doc/connector-j/5.1/en/) | [Download](https://dev.mysql.com/downloads/connector/j/) |
| Node.js | Windows, Linux, Mac OS X | [sidorares/node-mysql2](https://github.com/sidorares/node-mysql2/tree/master/documentation) | [Download](https://github.com/sidorares/node-mysql2) |
| Python | Windows, Linux, Mac OS X | [MySQL Connector/Python Developer Guide](https://dev.mysql.com/doc/connector-python/en/) | [Download](https://dev.mysql.com/downloads/connector/python/) |
| C++ | Windows, Linux, Mac OS X | [MySQL Connector/C++ Developer Guide](https://dev.mysql.com/doc/connector-cpp/en/) | [Download](https://dev.mysql.com/downloads/connector/python/) |
| C | Windows, Linux, Mac OS X | [MySQL Connector/C Developer Guide](https://dev.mysql.com/doc/connector-c/en/) | [Download](https://dev.mysql.com/downloads/connector/c/)
| Perl | Windows, Linux, Mac OS X, and Unix platforms | [DBD::MySQL](https://metacpan.org/pod/DBD::mysql) | [Download](https://metacpan.org/pod/DBD::mysql) |


## <a name="next-steps"></a>Next steps
Read these quickstarts on how to connect to and query Azure Database for MySQL by using your language of choice:

[PHP](./connect-php.md) | [Java](./connect-java.md) |  [.NET (C#)](./connect-csharp.md) | [Python](./connect-python.md) | [Node.JS](./connect-nodejs.md) | [Ruby](./connect-ruby.md) | [C++](connect-cpp.md) | [Go](./connect-go.md)

