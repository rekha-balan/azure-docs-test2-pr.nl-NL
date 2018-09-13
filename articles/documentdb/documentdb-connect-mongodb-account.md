---
title: MongoDB connection string for DocumentDB account | Microsoft Docs
description: Learn how to connect your MongoDB app to an Azure DocumentDB account using a MongoDB connection string.
keywords: mongodb connection string
services: documentdb
author: AndrewHoh
manager: jhubbard
editor: ''
documentationcenter: ''
ms.assetid: e36f7375-9329-403b-afd1-4ab49894f75e
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: anhoh
ms.openlocfilehash: 372d328eb6c5d370faf486b78873173c6b3b90b7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553482"
---
# <a name="connect-an-application-to-documentdb-api-for-mongodb"></a>Connect an application to DocumentDB: API for MongoDB
Learn how to connect your MongoDB app to an Azure DocumentDB account using a MongoDB connection string. By connecting your MongoDB app to an Azure DocumentDB database, you can use a DocumentDB database as the data store for your MongoDB app. 

This tutorial provides two ways to retrieve connection string information:

- [The Quick start method](#QuickstartConnection), for use with .NET, Node.js, MongoDB Shell, Java, and Python drivers.
- [The custom connection string method](#GetCustomConnection), for use with other drivers.

## <a name="prerequisites"></a>Prerequisites

- An Azure account. If you don't have an Azure account, create a [free Azure account](https://azure.microsoft.com/free/) now. 
- A DocumentDB account. For instructions, see [Create a DocumentDB account for use with MongoDB apps](documentdb-create-mongodb-account.md).

## <a id="QuickstartConnection"></a>Get the MongoDB connection string using the Quick start
1. In an internet browser, sign in to the [Azure Portal](https://portal.azure.com).
2. In the **NoSQL (DocumentDB)** blade, select the DocumentDB: API for MongoDB account. 
3. In the **Left Navigation** bar of the account blade, click **Quick start**. 
4. Choose your platform (*.NET driver*, *Node.js driver*, *MongoDB Shell*, *Java driver*, *Python driver*). If you don't see your driver or tool listed, don't worry, we continuously document more connection code snippets. Please comment below on what you'd like to see and read [Get the account's connection string information](#GetCustomConnection) to learn how to craft your own connection.
5. Copy and paste the code snippet into your MongoDB app, and you are ready to go.

    ![Screen shot of the quick start blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-connect-mongodb-account/QuickStartBlade.png)

## <a id="GetCustomConnection"></a> Get the MongoDB connection string to customize
1. In an internet browser, sign in to the [Azure Portal](https://portal.azure.com).
2. In the **NoSQL (DocumentDB)** blade, select the DocumentDB: API for MongoDB account. 
3. In the **Left Navigation** bar of the account blade, click **Connection String**. 
4. The **Connection String Information** blade opens and has all the information necessary to connect to the account using a driver for MongoDB, including a pre-constructed connection string.

    ![Screen shot of the connection string blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a>Connection string requirements
> [!Important]
> DocumentDB has strict security requirements and standards. DocumentDB accounts require authentication and secure communication via **SSL**.
>
>

It is important to note that DocumentDB supports the standard MongoDB connection string URI format, with a couple of specific requirements: DocumentDB accounts require authentication and secure communication via SSL.  Thus, the connection string format is:

    mongodb://username:password@host:port/[database]?ssl=true

Where the values of this string are available in the Connection String blade shown above.

* Username (required)
  * DocumentDB account name
* Password (required)
  * DocumentDB account password
* Host (required)
  * FQDN of DocumentDB account
* Port (required)
  * 10250
* Database (optional)
  * The default database used by the connection (if no database is provided, the default database is "test")
* ssl=true (required)

For example, consider the account shown in the Connection String Information above.  A valid connection string is:

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10250/mydatabase?ssl=true

## <a name="next-steps"></a>Next steps
* Learn how to [use MongoChef](documentdb-mongodb-mongochef.md) with a DocumentDB: API for MongoDB account.
* Explore DocumentDB: API for MongoDB [samples](documentdb-mongodb-samples.md).


