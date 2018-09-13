---
title: Install Visual Studio and connect to Azure Stack | Microsoft Docs
description: Learn the steps required to install Visual Studio and connect to Azure Stack
services: azure-stack
documentationcenter: ''
author: heathl17
manager: byronr
editor: ''
ms.assetid: 2022dbe5-47fd-457d-9af3-6c01688171d7
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2016
ms.author: sngun
ms.openlocfilehash: 785cfcac1220a258905bae6ece58a0dda9f1be7c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550184"
---
# <a name="install-visual-studio-and-connect-to-azure-stack"></a>Install Visual Studio and connect to Azure Stack

Use Visual Studio to author and deploy Azure Resource Manager [templates](azure-stack-arm-templates.md) in Azure Stack. You can use the steps described in this article to install Visual Studio either on [MAS-CON01](azure-stack-connect-azure-stack.md#connect-with-remote-desktop) computer, Azure Stack host computer or on a Windows-based external client if you are connected through [VPN](azure-stack-connect-azure-stack.md#connect-with-vpn). These steps perform a new installation of Visual Studio 2015 Community Edition. Read more about [coexistence](https://msdn.microsoft.com/library/ms246609.aspx) between other Visual Studio versions.

## <a name="install-visual-studio"></a>Install Visual Studio
1. Download and run the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).             
2. Search for **Visual Studio Community 2015 with Microsoft Azure SDK - 2.9.6**, click **Add**, and **Install**.

    ![Screenshot of WebPI install steps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-install-visual-studio/image1.png) 

3. Uninstall the **Microsoft Azure PowerShell** that is installed as part of the Azure SDK.

    ![Screenshot of add/remove programs interface for Azure PowerShell](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-install-visual-studio/image2.png) 

4. [Install PowerShell for Azure Stack](azure-stack-powershell-install.md)

5. Restart the operating system after the installation completes.

## <a name="connect-to-azure-stack"></a>Connect to Azure Stack

1. Launch Visual Studio.

2. From the **View** menu, select **Cloud Explorer**.

3. In the new pane, select **Add Account** and sign in with your Azure Active Directory credentials.  
    ![Screenshot of Cloud Explorer once logged in and connected to Azure Stack](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-install-visual-studio/image6.png)

Once logged in, you can [deploy templates](azure-stack-deploy-template-visual-studio.md) or browse available resource types and resource groups to create your own templates.  

## <a name="next-steps"></a>Next Steps

 - [Develop templates for Azure Stack](azure-stack-develop-templates.md)



