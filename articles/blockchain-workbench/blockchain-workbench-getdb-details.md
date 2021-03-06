---
title: Get Azure Blockchain Workbench database details
description: Learn how to get Azure Blockchain Workbench database and database server information.
services: azure-blockchain
keywords: ''
author: PatAltimore
ms.author: patricka
ms.date: 5/4/2018
ms.topic: article
ms.service: azure-blockchain
ms.reviewer: mmercuri
manager: femila
ms.openlocfilehash: 63b718bcb8722c5fd501891d162eadfae9fb8ec2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869728"
---
# <a name="get-information-about-your-azure-blockchain-workbench-database"></a>Get information about your Azure Blockchain Workbench database

This article shows how to get detailed information about your Azure Blockchain Workbench database.

## <a name="overview"></a>Overview

Information about applications, workflows, and smart contract execution is provided using database views in the Blockchain Workbench SQL DB. Developers can use this information when using tools such as Microsoft Excel, PowerBI, Visual Studio, and SQL Server Management Studio.

Before a developer can connect to the database, they need:

* External client access allowed in the database firewall. This article about configuring a database firewall article explains how to allow access.
* The database server name and database name.

## <a name="connect-to-the-blockchain-workbench-database"></a>Connect to the Blockchain Workbench database

To connect to the database:

1. Sign in to the Azure Portal with an account that has **Owner** permissions for the Azure Blockchain Workbench resources.
2. In the left navigation pane, choose **Resource groups**.
3. Choose the name of the resource group for your Blockchain Workbench deployment.
4. Select **Type** to sort the resource list, and then choose your **SQL server**. The sorted list in the next screen capture shows two SQL databases, "master" and one that uses "lhgn" as the **Resource prefix**.

   ![Sorted Blockchain Workbench resource list](media/blockchain-workbench-getdb-details/sorted-workbench-resource-list.png)

5. To see detailed information about the Blockchain Workbench database, select the link for the database with the **Resource prefix** you provided for deploying Blockchain Workbench.

   ![Database details](media/blockchain-workbench-getdb-details/workbench-db-details.png)

The database server name and database name let you connect to the Blockchain Workbench database using your development or reporting tool.

## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"]
> [Database views in Azure Blockchain Workbench](blockchain-workbench-database-views.md)