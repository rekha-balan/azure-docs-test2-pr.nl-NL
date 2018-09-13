---
title: Accessing private Azure clouds with Visual Studio | Microsoft Docs
description: Learn how to access private cloud resources by using Visual Studio.
services: visual-studio-online
documentationcenter: na
author: TomArcher
manager: douge
editor: ''
ms.assetid: 9d733c8d-703b-44e7-a210-bb75874c45c8
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/19/2017
ms.author: tarcher
ms.openlocfilehash: 781f4b11a7345bb07ff2b5e88090b3bcdafc4b2f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549731"
---
# <a name="accessing-private-azure-clouds-with-visual-studio"></a>Accessing private Azure clouds with Visual Studio
By default, Visual Studio supports public Azure cloud REST endpoints. In this topic, you learn how to use your private cloud's certificate to access - and interact with - the private cloud from Visual Studio.

## <a name="to-access-a-private-azure-cloud-in-visual-studio"></a>To access a private Azure cloud in Visual Studio
1. In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885) for the private cloud, download your publish-settings file, or contact your administrator for a publish-settings file. On the public version of Azure, the link to download this is [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/). (The downloaded file should have an extension of `.publishsettings`)

1. Open Visual Studio

1. In **Server Explorer**, right-click the **Azure** node and, from the context menu, select **Manage and Filter Subscriptions**.
   
    ![Manage subscriptions command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790778.png)

1. In the **Manage Microsoft Azure Subscriptions** dialog, select the **Certificates** tab, and then select **Import**.
   
    ![Importing Azure certificates](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790779.png)

1. In the **Import Microsoft Azure Subscriptions** dialog, select **Browse**.

    ![Browse button on the Import Microsoft Azure Subscriptions dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/browse-button.png)

1. In the **Open** dialog, browse to the directory where you saved the publish-settings file, select the file, and then select **Open**.

    ![Select the publish-settings file](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/select-publish-settings-file.png)

1. When returned to the **Import Microsoft Azure Subscriptions** dialog, select **Import**.

    ![Import the publish-settings file](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790780.png)

    The certificates are imported from the publish-settings file into Visual Studio, and you can now interact with your private cloud resources.
   
## <a name="next-steps"></a>Next steps
- [Publishing to an Azure Cloud Service from Visual Studio](https://msdn.microsoft.com/library/azure/ee460772.aspx)
- [How to: Download and Import Publish Settings and Subscription Information](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)





