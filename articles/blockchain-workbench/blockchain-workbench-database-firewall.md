---
title: Configure the Azure Blockchain Workbench SQL DB firewall
description: Learn how to configure the Azure Blockchain Workbench SQL DB firewall.
services: azure-blockchain
keywords: ''
author: PatAltimore
ms.author: patricka
ms.date: 5/4/2018
ms.topic: article
ms.service: azure-blockchain
ms.reviewer: mmercuri
manager: femila
ms.openlocfilehash: afeea143f73fa4f7d3e373535007846a668616ab
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866995"
---
# <a name="configure-the-azure-blockchain-workbench-database-firewall"></a>Configure the Azure Blockchain Workbench database firewall

This article shows how to configure a firewall rule using the Azure portal. Firewall rules let external clients or applications connect to your Azure Blockchain Workbench database.

## <a name="connect-to-the-blockchain-workbench-database"></a>Connect to the Blockchain Workbench database

To connect to the database where you want to configure a rule:

1. Sign in to the Azure Portal with an account that has **Owner**     permissions for the Azure Blockchain Workbench resources.
2. In the left navigation pane, choose **Resource groups**.
3. Choose the name of the resource group for your Blockchain Workbench deployment.
4. Select **Type** to sort the list of resources, and then choose your **SQL server**.
5. The resource list example in the following screen capture shows two databases: *master* and *lsgn-sdk*. You configure the firewall rule on  *lsgn-sdk*.

![List Blockchain Workbench resources](media/blockchain-workbench-database-firewall/list-database-resources.png)

## <a name="create-a-database-firewall-rule"></a>Create a database firewall rule

To create a firewall rule:

1. Choose the link to the "lsgn-sdk" database.
2. On the menu bar, select **Set server firewall**.

   ![Set server firewall](media/blockchain-workbench-database-firewall/configure-server-firewall.png)

3. To create a rule for your organization:

   * Enter a **RULE NAME**
   * Enter an IP address for the **START IP** of the address range
   * Enter an IP address for the **END IP** of the address range

   ![Create firewall rule](media/blockchain-workbench-database-firewall/create-firewall-rule.png)

    > [!NOTE]
    > If you only want to add the IP address of your computer, choose **+ Add client IP**.
        
1. To save your firewall configuration, select **Save**.
2. Test the IP address range you configured for the database by connecting from an application or tool. For example, SQL Server Management Studio.

## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"]
> [Database views in Azure Blockchain Workbench](blockchain-workbench-database-views.md)