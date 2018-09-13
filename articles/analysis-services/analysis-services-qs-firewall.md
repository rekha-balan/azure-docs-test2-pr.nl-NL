---
title: Quickstart - Configure a firewall for an Analysis Services server in Azure | Microsoft Docs
description: Learn how to configure a firewall for an Analysis Services server instance in Azure.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: quickstart
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: c16a189e72edd94cf6fc60580d89dd4cfd1742e8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870281"
---
# <a name="quickstart-configure-server-firewall---portal"></a>Quickstart: Configure server firewall - Portal

This quickstart helps you configure a firewall for your Azure Analysis Services server. Enabling a firewall and configuring IP address ranges for only those computers accessing your server are an important part of securing your server and data.

## <a name="prerequisites"></a>Prerequisites

- An Analysis Services server in your subscription. To learn more, see [Quickstart: Create a server - Portal](analysis-services-create-server.md) or [Quickstart: Create a server - PowerShell](analysis-services-create-powershell.md)
- One or more IP address ranges for client computers (if needed).

## <a name="log-in-to-the-azure-portal"></a>Log in to the Azure portal 

[Log in to the portal](https://portal.azure.com)

## <a name="configure-a-firewall"></a>Configure a firewall

1. Click on your server to open the Overview page. 
2. In **SETTINGS** > **Firewall** > **Enable firewall**, click **On**.
3. To allow DirectQuery access from Power BI service, in **Allow accesss from Power BI**, click **On**.  
4. (Optional) Specify one or more IP address ranges. Enter a name, starting, and ending IP address for each range. 
5. Click **Save**.

     ![Firewall settings](./media/analysis-services-qs-firewall/aas-qs-firewall.png)

## <a name="clean-up-resources"></a>Clean up resources

When no longer needed, delete IP address ranges, or disable the firewall.

## <a name="next-steps"></a>Next steps
In this quickstart, you learned how to configure a firewall for your server. Now that you have server, and secured it with a firewall, you can add a basic sample data model to it from the portal. Having a sample model is helpful to learn about configuring model database roles and testing client connections. To learn more, continue to the tutorial for adding a sample model.

> [!div class="nextstepaction"]
> [Tutorial: Add a sample model to your server](analysis-services-create-sample-model.md)
