---
title: Connect applications to Azure Database for MySQL
description: This document lists the currently supported connection strings for applications to connect with Azure Database for MySQL, including ADO.NET (C#), JDBC, Node.js, ODBC, PHP, Python, and Ruby.
services: mysql
author: ajlam
ms.author: andrela
editor: jasonwhowell
manager: kfile
ms.service: mysql
ms.topic: article
ms.date: 02/28/2018
ms.openlocfilehash: 06bd91adb0a86198f7709d0989624657ce00dfa9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866784"
---
# <a name="how-to-connect-applications-to-azure-database-for-mysql"></a>How to connect applications to Azure Database for MySQL
This topic lists the connection string types that are supported by Azure Database for MySQL, together with templates and examples. You might have different parameters and settings in your connection string.

- To obtain the certificate, see [How to configure SSL](./howto-configure-ssl.md).
- {your_host} = <servername>.mysql.database.azure.com
- {your_user}@{servername} = userID format for authentication correctly.  If you only use the userID, the authentication will fail.

## <a name="adonet"></a>ADO.NET
```ado.net
Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password};[SslMode=Required;]
```

In this example, the server name is `mydemoserver`, the database name is `wpdb`, the user name is `WPAdmin`, and the password is `mypassword!2`. As a result, the connection string should be:

```ado.net
Server= "mydemoserver.mysql.database.azure.com"; Port=3306; Database= "wpdb"; Uid= "WPAdmin@mydemoserver"; Pwd="mypassword!2"; SslMode=Required;
```

## <a name="jdbc"></a>JDBC
```jdbc
String url ="jdbc:mysql://%s:%s/%s[?verifyServerCertificate=true&useSSL=true&requireSSL=true]",{your_host},{your_port},{your_database}"; myDbConn = DriverManager.getConnection(url, {username@servername}, {your_password}";
```

## <a name="nodejs"></a>Node.js
```node.js
var conn = mysql.createConnection({host: {your_host}, user: {username@servername}, password: {your_password}, database: {your_database}, Port: {your_port}[, ssl:{ca:fs.readFileSync({ca-cert filename})}}]);
```

## <a name="odbc"></a>ODBC
```odbc
DRIVER={MySQL ODBC 5.3 UNICODE Driver};Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password}; [sslca={ca-cert filename}; sslverify=1; Option=3;]
```

## <a name="php"></a>PHP
```php
$con=mysqli_init(); [mysqli_ssl_set($con, NULL, NULL, {ca-cert filename}, NULL, NULL);] mysqli_real_connect($con, {your_host}, {username@servername}, {your_password}, {your_database}, {your_port});
```

## <a name="python"></a>Python
```python
cnx = mysql.connector.connect(user={username@servername}, password={your_password}, host={your_host}, port={your_port}, database={your_database}[, ssl_ca={ca-cert filename}, ssl_verify_cert=true])
```

## <a name="ruby"></a>Ruby
```ruby
client = Mysql2::Client.new(username: {username@servername}, password: {your_password}, database: {your_database}, host: {your_host}, port: {your_port}[, sslca:{ca-cert filename}, sslverify:false, sslcipher:'AES256-SHA'])
```

## <a name="get-the-connection-string-details-from-the-azure-portal"></a>Get the connection string details from the Azure portal
In the [Azure portal](https://portal.azure.com), go to your Azure Database for MySQL server, and then click **Connection strings** to get the string list for your instance: ![The Connection strings pane in the Azure portal](./media/howto-connection-strings/connection-strings-on-portal.png)

The string provides details such as the driver, server, and other database connection parameters. Modify these examples to use your own parameters, such as database name, password, and so on. You can then use this string to connect to the server from your code and applications.

## <a name="next-steps"></a>Next steps
- For more information about connection libraries, see [Concepts - Connection libraries](./concepts-connection-libraries.md).
