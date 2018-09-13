---
title: Connect to Azure Analysis Services with Excel | Microsoft Docs
description: Learn how to connect to an Azure Analysis Services server by using Excel.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: 807496584acb3f93fccd3495de005792b769b37f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44775521"
---
# <a name="connect-with-excel"></a>Connect with Excel

Once you've created a server, and deployed a tabular model to it, clients can connect and begin exploring data. 

## <a name="before-you-begin"></a>Before you begin
The account you log in with must belong to a model database role with at least read permissions. To learn more, see [Authentication and user permissions](analysis-services-manage-users.md). 

## <a name="connect-in-excel"></a>Connect in Excel

Connecting to a server in Excel is supported by using Get Data in Excel 2016. Connecting by using the Import Table Wizard in Power Pivot is not supported. 

**To connect in Excel 2016**

1. In Excel 2016, on the **Data** ribbon, click **Get External Data** > **From Other Sources** > **From Analysis Services**.

2. In the Data Connection Wizard, in **Server name**, enter the server name including protocol and URI. For example, asazure://westcentralus.asazure.windows.net/advworks. Then, in **Logon credentials**, select **Use the following User Name and Password**, and then type the organizational user name, for example nancy@adventureworks.com, and password.

    > [!IMPORTANT]
    > If you log in with a Microsoft Account, Live ID, Yahoo, Gmail, etc., or you are required to sign in with multi-factor authentication, leave the password field blank. You are prompted for a password after clicking Next. 

    ![Connect from Excel logon](./media/analysis-services-connect-excel/aas-connect-excel-logon.png)

3. In **Select Database and Table**, select the database and model or perspective, and then click **Finish**.
   
    ![Connect from Excel select model](./media/analysis-services-connect-excel/aas-connect-excel-select.png)


## <a name="see-also"></a>See also
[Client libraries](analysis-services-data-providers.md)   
[Manage your server](analysis-services-manage.md)     


