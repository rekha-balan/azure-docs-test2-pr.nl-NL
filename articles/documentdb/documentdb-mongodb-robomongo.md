---
title: Use Robomongo for MongoDB with Azure DocumentDB | Microsoft Docs
description: 'Learn how to use Robomongo with a DocumentDB: API for MongoDB account'
keywords: robomongo
services: documentdb
author: AndrewHoh
manager: jhubbard
editor: ''
documentationcenter: ''
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: anhoh
ms.openlocfilehash: 060ad7d47541f5a8a9a23cbe67146112dad66fc8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554056"
---
# <a name="use-robomongo-with-a-documentdb-api-for-mongodb-account"></a>Use Robomongo with a DocumentDB: API for MongoDB account
To connect to an Azure DocumentDB: API for MongoDB account using Robomongo, you must:

* Download and install [Robomongo](https://robomongo.org/)
* Have your DocumentDB: API for MongoDB account [connection string](documentdb-connect-mongodb-account.md) information

## <a name="connect-using-robomongo"></a>Connect using Robomongo
To add your DocumentDB: API for MongoDB account to the Robomongo MongoDB Connections, perform the following steps.

1. Retrieve your DocumentDB: API for MongoDB account connection information using the instructions [here](documentdb-connect-mongodb-account.md).

    ![Screen shot of the connection string blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-mongodb-robomongo/connectionstringblade.png)
2. Run *Robomongo.exe*

3. Click the connection button under **File** to manage your connections. Then, click **Create** in the **MongoDB Connections** window, which will open up the **Connection Settings** window.

4. In the **Connection Settings** window, choose a name. Then, find the **Host** and **Port** from your connection information in Step 1 and enter them into **Address** and **Port**, respectively.

    ![Screen shot of the Robomongo Manage Connections](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-mongodb-robomongo/manageconnections.png)
5. On the **Authentication** tab, click **Perform authentication**. Then, enter your Database (default is *Admin*), **User Name** and **Password**.
Both **User Name** and **Password** can be found in your connection information in Step 1.

    ![Screen shot of the Robomongo Authentication Tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-mongodb-robomongo/authentication.png)
6. On the **SSL** tab, check **Use SSL protocol**, then change the **Authentication Method** to **Self-signed Certificate**.

    ![Screen shot of the Robomongo SSL Tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-mongodb-robomongo/SSL.png)
7. Finally, click **Test** to verify that you are able to connect, then **Save**.

## <a name="next-steps"></a>Next steps
* Explore DocumentDB: API for MongoDB [samples](documentdb-mongodb-samples.md).




