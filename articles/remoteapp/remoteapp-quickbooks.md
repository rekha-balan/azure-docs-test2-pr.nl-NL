---
title: Deploy QuickBooks in Azure RemoteApp | Microsoft Docs
description: Learn how to share QuickBooks with Azure RemoteApp.
services: remoteapp
documentationcenter: ''
author: ericorman
manager: mbaldwin
ms.assetid: c5d00753-77c0-4f0d-a5df-9451b46a31d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 4b7c17446efe025b02001f926ea5d43591c971e3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553391"
---
# <a name="how-do-you-deploy-quickbooks-in-azure-remoteapp"></a>How do you deploy QuickBooks in Azure RemoteApp?
> [!IMPORTANT]
> Azure RemoteApp is being discontinued on August 31, 2017. Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.
> 
> 

Use the following information to share QuickBooks as an app in Azure RemoteApp.

You can share QuickBooks 2015 Enterprise with Azure RemoteApp in either a hybrid or cloud collection. The company file must reside on a VM that is running QuickBooks database server that is separate from the Azure RemoteApp servers. Never store the company file on your Azure RemoteApp image - data loss is expected if you do this. Only QuickBooks Enterprise supports hosting the QuickBooks file on an external share with QuickBooks database server accessible via standard Windows networking.   

> [!IMPORTANT]
> The QuickBooks database server that is hosting the company file must reside on a separate VM within the same VNET as the Azure RemoteApp collection.  
> 
> 

## <a name="steps-to-deploy-quickbooks"></a>Steps to deploy QuickBooks
1. Create an Azure VM and install QuickBooks, QuickBooks database server, and place the company file on a Azure VM.  Make sure to properly configure firewall rules.
2. Install QuickBooks on a [custom image](remoteapp-imageoptions.md) and create an [Azure RemoteApp collection](remoteapp-collections.md), either cloud or hybrid, within the exact same VNET where the VM hosting the QuickBooks database server with company files resides. 
3. [Publish](remoteapp-publish.md) QuickBooks app to users
4. Launch the Azure RemoteApp-hosted QuickBooks client, navigate using standard Windows networking to the VM hosting the QuickBooks database server and open the company file. 

## <a name="documentation-references"></a>Documentation references
* QuickBooks [supported configurations](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)
* QuickBooks [deployment options](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)

You can also check out my Ignite presentation, [Fundamentals of Microsoft Azure RemoteApp Management and Administration](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) - fast-forward to 1:02:45 to get to the QuickBooks part.

## <a name="deployment-architecture"></a>Deployment architecture
![QuickBooks + Azure RemoteApp deployment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-quickbooks/ra-quickbooks.png)


