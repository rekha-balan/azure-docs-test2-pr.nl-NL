---
title: Configure SSL connectivity to securely connect to Azure Database for MySQL
description: Instructions for how to properly configure Azure Database for MySQL and associated applications to correctly use SSL connections
services: mysql
author: ajlam
ms.author: andrela
editor: jasonwhowell
manager: kfile
ms.service: mysql
ms.topic: article
ms.date: 02/28/2018
ms.openlocfilehash: f18510e83d4e7d6498f34012b68368552399c806
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856572"
---
# <a name="configure-ssl-connectivity-in-your-application-to-securely-connect-to-azure-database-for-mysql"></a><span data-ttu-id="b8fd0-103">Configure SSL connectivity in your application to securely connect to Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="b8fd0-103">Configure SSL connectivity in your application to securely connect to Azure Database for MySQL</span></span>
<span data-ttu-id="b8fd0-104">Azure Database for MySQL supports connecting your Azure Database for MySQL server to client applications using Secure Sockets Layer (SSL).</span><span class="sxs-lookup"><span data-stu-id="b8fd0-104">Azure Database for MySQL supports connecting your Azure Database for MySQL server to client applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="b8fd0-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in the middle" attacks by encrypting the data stream between the server and your application.</span><span class="sxs-lookup"><span data-stu-id="b8fd0-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in the middle" attacks by encrypting the data stream between the server and your application.</span></span>

## <a name="step-1-obtain-ssl-certificate"></a><span data-ttu-id="b8fd0-106">Step 1: Obtain SSL certificate</span><span class="sxs-lookup"><span data-stu-id="b8fd0-106">Step 1: Obtain SSL certificate</span></span>
<span data-ttu-id="b8fd0-107">Download the certificate needed to communicate over SSL with your Azure Database for MySQL server from [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) and save the certificate file to your local drive (this tutorial uses c:\ssl for example).</span><span class="sxs-lookup"><span data-stu-id="b8fd0-107">Download the certificate needed to communicate over SSL with your Azure Database for MySQL server from [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) and save the certificate file to your local drive (this tutorial uses c:\ssl for example).</span></span>
<span data-ttu-id="b8fd0-108">**For Microsoft Internet Explorer and Microsoft Edge:** After the download has completed, rename the certificate to BaltimoreCyberTrustRoot.crt.pem.</span><span class="sxs-lookup"><span data-stu-id="b8fd0-108">**For Microsoft Internet Explorer and Microsoft Edge:** After the download has completed, rename the certificate to BaltimoreCyberTrustRoot.crt.pem.</span></span>

## <a name="step-2-bind-ssl"></a><span data-ttu-id="b8fd0-109">Step 2: Bind SSL</span><span class="sxs-lookup"><span data-stu-id="b8fd0-109">Step 2: Bind SSL</span></span>
### <a name="connecting-to-server-using-the-mysql-workbench-over-ssl"></a><span data-ttu-id="b8fd0-110">Connecting to server using the MySQL Workbench over SSL</span><span class="sxs-lookup"><span data-stu-id="b8fd0-110">Connecting to server using the MySQL Workbench over SSL</span></span>
<span data-ttu-id="b8fd0-111">Configure the MySQL Workbench to connect securely over SSL.</span><span class="sxs-lookup"><span data-stu-id="b8fd0-111">Configure the MySQL Workbench to connect securely over SSL.</span></span> <span data-ttu-id="b8fd0-112">From the Setup New Connection dialogue, navigate to the **SSL** tab. In the **SSL CA File:** field, enter the file location of the **BaltimoreCyberTrustRoot.crt.pem**.</span><span class="sxs-lookup"><span data-stu-id="b8fd0-112">From the Setup New Connection dialogue, navigate to the **SSL** tab. In the **SSL CA File:** field, enter the file location of the **BaltimoreCyberTrustRoot.crt.pem**.</span></span> 
<span data-ttu-id="b8fd0-113">![save customized tile](./media/howto-configure-ssl/mysql-workbench-ssl.png) For existing connections, you can bind SSL by right-clicking on the connection icon and choose edit.</span><span class="sxs-lookup"><span data-stu-id="b8fd0-113">![save customized tile](./media/howto-configure-ssl/mysql-workbench-ssl.png) For existing connections, you can bind SSL by right-clicking on the connection icon and choose edit.</span></span> <span data-ttu-id="b8fd0-114">Then navigate to the **SSL** tab and bind the cert file.</span><span class="sxs-lookup"><span data-stu-id="b8fd0-114">Then navigate to the **SSL** tab and bind the cert file.</span></span>

### <a name="connecting-to-server-using-the-mysql-cli-over-ssl"></a><span data-ttu-id="b8fd0-115">Connecting to server using the MySQL CLI over SSL</span><span class="sxs-lookup"><span data-stu-id="b8fd0-115">Connecting to server using the MySQL CLI over SSL</span></span>
<span data-ttu-id="b8fd0-116">Another way to bind the SSL certificate is to use the MySQL command-line interface by executing the following command:</span><span class="sxs-lookup"><span data-stu-id="b8fd0-116">Another way to bind the SSL certificate is to use the MySQL command-line interface by executing the following command:</span></span>
```dos
mysql.exe -h mydemoserver.mysql.database.azure.com -u Username@mydemoserver -p --ssl-ca=c:\ssl\BaltimoreCyberTrustRoot.crt.pem
```

## <a name="step-3--enforcing-ssl-connections-in-azure"></a><span data-ttu-id="b8fd0-117">Step 3:  Enforcing SSL connections in Azure</span><span class="sxs-lookup"><span data-stu-id="b8fd0-117">Step 3:  Enforcing SSL connections in Azure</span></span> 
### <a name="using-the-azure-portal"></a><span data-ttu-id="b8fd0-118">Using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="b8fd0-118">Using the Azure portal</span></span>
<span data-ttu-id="b8fd0-119">Using the Azure portal, visit your Azure Database for MySQL server, and then click **Connection security**.</span><span class="sxs-lookup"><span data-stu-id="b8fd0-119">Using the Azure portal, visit your Azure Database for MySQL server, and then click **Connection security**.</span></span> <span data-ttu-id="b8fd0-120">Use the toggle button to enable or disable the **Enforce SSL connection** setting, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="b8fd0-120">Use the toggle button to enable or disable the **Enforce SSL connection** setting, and then click **Save**.</span></span> <span data-ttu-id="b8fd0-121">Microsoft recommends to always enable the **Enforce SSL connection** setting for enhanced security.</span><span class="sxs-lookup"><span data-stu-id="b8fd0-121">Microsoft recommends to always enable the **Enforce SSL connection** setting for enhanced security.</span></span>
<span data-ttu-id="b8fd0-122">![enable-ssl](./media/howto-configure-ssl/enable-ssl.png)</span><span class="sxs-lookup"><span data-stu-id="b8fd0-122">![enable-ssl](./media/howto-configure-ssl/enable-ssl.png)</span></span>

### <a name="using-azure-cli"></a><span data-ttu-id="b8fd0-123">Using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b8fd0-123">Using Azure CLI</span></span>
<span data-ttu-id="b8fd0-124">You can enable or disable the **ssl-enforcement** parameter by using Enabled or Disabled values respectively in Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="b8fd0-124">You can enable or disable the **ssl-enforcement** parameter by using Enabled or Disabled values respectively in Azure CLI.</span></span>
```azurecli-interactive
az mysql server update --resource-group myresource --name mydemoserver --ssl-enforcement Enabled
```

## <a name="step-4-verify-the-ssl-connection"></a><span data-ttu-id="b8fd0-125">Step 4: Verify the SSL connection</span><span class="sxs-lookup"><span data-stu-id="b8fd0-125">Step 4: Verify the SSL connection</span></span>
<span data-ttu-id="b8fd0-126">Execute the mysql **status** command to verify that you have connected to your MySQL server using SSL:</span><span class="sxs-lookup"><span data-stu-id="b8fd0-126">Execute the mysql **status** command to verify that you have connected to your MySQL server using SSL:</span></span>
```dos
mysql> status
```
<span data-ttu-id="b8fd0-127">Confirm the connection is encrypted by reviewing the output, which should show:  **SSL: Cipher in use is AES256-SHA**</span><span class="sxs-lookup"><span data-stu-id="b8fd0-127">Confirm the connection is encrypted by reviewing the output, which should show:  **SSL: Cipher in use is AES256-SHA**</span></span> 

## <a name="sample-code"></a><span data-ttu-id="b8fd0-128">Sample code</span><span class="sxs-lookup"><span data-stu-id="b8fd0-128">Sample code</span></span>
<span data-ttu-id="b8fd0-129">To establish a secure connection to Azure Database for MySQL over SSL from your application, refer to the following code samples:</span><span class="sxs-lookup"><span data-stu-id="b8fd0-129">To establish a secure connection to Azure Database for MySQL over SSL from your application, refer to the following code samples:</span></span>

### <a name="php"></a><span data-ttu-id="b8fd0-130">PHP</span><span class="sxs-lookup"><span data-stu-id="b8fd0-130">PHP</span></span>
```php
$conn = mysqli_init();
mysqli_ssl_set($conn,NULL,NULL, "/var/www/html/BaltimoreCyberTrustRoot.crt.pem", NULL, NULL) ; 
mysqli_real_connect($conn, 'mydemoserver.mysql.database.azure.com', 'myadmin@mydemoserver', 'yourpassword', 'quickstartdb', 3306, MYSQLI_CLIENT_SSL, MYSQLI_CLIENT_SSL_DONT_VERIFY_SERVER_CERT);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}
```
### <a name="python-mysqlconnector-python"></a><span data-ttu-id="b8fd0-131">Python (MySQLConnector Python)</span><span class="sxs-lookup"><span data-stu-id="b8fd0-131">Python (MySQLConnector Python)</span></span>
```python
try:
    conn=mysql.connector.connect(user='myadmin@mydemoserver', 
        password='yourpassword', 
        database='quickstartdb', 
        host='mydemoserver.mysql.database.azure.com', 
        ssl_ca='/var/www/html/BaltimoreCyberTrustRoot.crt.pem')
except mysql.connector.Error as err:
    print(err)
```
### <a name="python-pymysql"></a><span data-ttu-id="b8fd0-132">Python (PyMySQL)</span><span class="sxs-lookup"><span data-stu-id="b8fd0-132">Python (PyMySQL)</span></span>
```python
conn = pymysql.connect(user = 'myadmin@mydemoserver', 
        password = 'yourpassword', 
        database = 'quickstartdb', 
        host = 'mydemoserver.mysql.database.azure.com', 
        ssl = {'ssl': {'ca': '/var/www/html/BaltimoreCyberTrustRoot.crt.pem'}})
```
### <a name="ruby"></a><span data-ttu-id="b8fd0-133">Ruby</span><span class="sxs-lookup"><span data-stu-id="b8fd0-133">Ruby</span></span>
```ruby
client = Mysql2::Client.new(
        :host     => 'mydemoserver.mysql.database.azure.com', 
        :username => 'myadmin@mydemoserver',      
        :password => 'yourpassword',    
        :database => 'quickstartdb',
        :ssl_ca => '/var/www/html/BaltimoreCyberTrustRoot.crt.pem'
    )
```
### <a name="golang"></a><span data-ttu-id="b8fd0-134">Golang</span><span class="sxs-lookup"><span data-stu-id="b8fd0-134">Golang</span></span>
```go
rootCertPool := x509.NewCertPool()
pem, _ := ioutil.ReadFile("/var/www/html/BaltimoreCyberTrustRoot.crt.pem")
if ok := rootCertPool.AppendCertsFromPEM(pem); !ok {
    log.Fatal("Failed to append PEM.")
}
mysql.RegisterTLSConfig("custom", &tls.Config{RootCAs: rootCertPool})
var connectionString string
connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true&tls=custom",'myadmin@mydemoserver' , 'yourpassword', 'mydemoserver.mysql.database.azure.com', 'quickstartdb')   
db, _ := sql.Open("mysql", connectionString)
```
### <a name="javajdbc"></a><span data-ttu-id="b8fd0-135">JAVA(JDBC)</span><span class="sxs-lookup"><span data-stu-id="b8fd0-135">JAVA(JDBC)</span></span>
```java
# generate truststore and keystore in code
String importCert = " -import "+
    " -alias mysqlServerCACert "+
    " -file " + ssl_ca +
    " -keystore truststore "+
    " -trustcacerts " + 
    " -storepass password -noprompt ";
String genKey = " -genkey -keyalg rsa " +
    " -alias mysqlClientCertificate -keystore keystore " +
    " -storepass password123 -keypass password " + 
    " -dname CN=MS ";
sun.security.tools.keytool.Main.main(importCert.trim().split("\\s+"));
sun.security.tools.keytool.Main.main(genKey.trim().split("\\s+"));

# use the generated keystore and truststore 
System.setProperty("javax.net.ssl.keyStore","path_to_keystore_file");
System.setProperty("javax.net.ssl.keyStorePassword","password");
System.setProperty("javax.net.ssl.trustStore","path_to_truststore_file");
System.setProperty("javax.net.ssl.trustStorePassword","password");

url = String.format("jdbc:mysql://%s/%s?serverTimezone=UTC&useSSL=true", 'mydemoserver.mysql.database.azure.com', 'quickstartdb');
properties.setProperty("user", 'myadmin@mydemoserver');
properties.setProperty("password", 'yourpassword');
conn = DriverManager.getConnection(url, properties);
```
### <a name="javamariadb"></a><span data-ttu-id="b8fd0-136">JAVA(MariaDB)</span><span class="sxs-lookup"><span data-stu-id="b8fd0-136">JAVA(MariaDB)</span></span>
```java
# generate truststore and keystore in code
String importCert = " -import "+
    " -alias mysqlServerCACert "+
    " -file " + ssl_ca +
    " -keystore truststore "+
    " -trustcacerts " + 
    " -storepass password -noprompt ";
String genKey = " -genkey -keyalg rsa " +
    " -alias mysqlClientCertificate -keystore keystore " +
    " -storepass password123 -keypass password " + 
    " -dname CN=MS ";
sun.security.tools.keytool.Main.main(importCert.trim().split("\\s+"));
sun.security.tools.keytool.Main.main(genKey.trim().split("\\s+"));

# use the generated keystore and truststore 
System.setProperty("javax.net.ssl.keyStore","path_to_keystore_file");
System.setProperty("javax.net.ssl.keyStorePassword","password");
System.setProperty("javax.net.ssl.trustStore","path_to_truststore_file");
System.setProperty("javax.net.ssl.trustStorePassword","password");

url = String.format("jdbc:mariadb://%s/%s?useSSL=true&trustServerCertificate=true", 'mydemoserver.mysql.database.azure.com', 'quickstartdb');
properties.setProperty("user", 'myadmin@mydemoserver');
properties.setProperty("password", 'yourpassword');
conn = DriverManager.getConnection(url, properties);
```

## <a name="next-steps"></a><span data-ttu-id="b8fd0-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="b8fd0-137">Next steps</span></span>
<span data-ttu-id="b8fd0-138">Review various application connectivity options following [Connection libraries for Azure Database for MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="b8fd0-138">Review various application connectivity options following [Connection libraries for Azure Database for MySQL](concepts-connection-libraries.md)</span></span>
