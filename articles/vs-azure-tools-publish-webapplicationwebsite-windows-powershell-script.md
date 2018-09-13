---
title: Publish-WebApplicationWebSite (Windows PowerShell script) | Microsoft Docs
description: Learn how to publish a web project to an Azure website. This script creates the required resources in your Azure subscription if they don't exist.
services: visual-studio-online
documentationcenter: na
author: TomArcher
manager: douge
editor: ''
ms.assetid: 63cfaa2d-f04d-40dc-8677-345385c278d5
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: tarcher
ms.openlocfilehash: ed1a5bdd0a7fb84579b248fdbb3b295c9d904ee5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549611"
---
# <a name="publish-webapplicationwebsite-windows-powershell-script"></a>Publish-WebApplicationWebSite (Windows PowerShell script)
## <a name="syntax"></a>Syntax
Publishes a web project to an Azure website. The script creates the required resources in your Azure subscription if they don't exist.

    Publish-WebApplicationWebSite
    –Configuration <configuration>
    -SubscriptionName <subscriptionName>
    -WebDeployPackage <packageName>
    -DatabaseServerPassword @{Name = "name"; Password = "password"}
    -SendHostMessagesToOutput
    -Verbose


## <a name="configuration"></a>Configuration
The path to the JSON configuration file that describes the details of the deployment.

| Parameter | Default value |
| --- | --- |
| Aliases |none |
| Required? |true |
| Position |named |
| Default value |none |
| Accept pipeline input? |false |
| Accept wildcard characters? |false |

## <a name="subscriptionname"></a>SubscriptionName
The name of the Azure subscription that you want to create the website in.

| Parameter | Default value |
| --- | --- |
| Aliases |none |
| Required? |false |
| Position |named |
| Default value |none |
| Accept pipeline input? |false |
| Accept wildcard characters? |false |

## <a name="webdeploypackage"></a>WebDeployPackage
The path to the web deployment package to publish to the website. You can create this package by using the Publish Web wizard in Visual Studio. For more information, see [Get started with Azure Cloud Services and ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).

| Parameter | Default value |
| --- | --- |
| Aliases |none |
| Required? |false |
| Position |named |
| Default value |none |
| Accept pipeline input? |false |
| Accept wildcard characters? |false |

## <a name="databaseserverpassword"></a>DatabaseServerPassword
The username and password for the SQL database in Azure.

| Parameter | Default value |
| --- | --- |
| Aliases |none |
| Required? |false |
| Position |named |
| Default value |none |
| Accept pipeline input? |false |
| Accept wildcard characters? |false |

## <a name="sendhostmessagestooutput"></a>SendHostMessagesToOutput
If true, print messages from the script to the output stream.

| Parameter | Default value |
| --- | --- |
| Aliases |none |
| Required? |false |
| Position |named |
| Default value |false |
| Accept pipeline input? |false |
| Accept wildcard characters? |false |

## <a name="remarks"></a>Remarks
For a complete explanation of how to use the script to create Dev and Test environments, see [Using Windows PowerShell Scripts to Publish to Dev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).

The JSON configuration file specifies the details of what is to be deployed. It includes the information that you specified when you created the project, such as the name and username for the website. It also includes the database to provision, if any. The following code shows an example JSON configuration file:

    {
        "environmentSettings": {
            "webSite": {
                "name": "WebApplication10554",
                "location": "West US"
            },
            "databases": [
                {
                    "connectionStringName": "DefaultConnection",
                    "databaseName": "WebApplication10554_db",
                    "serverName": "iss00brc88",
                    "user": "sqluser2",
                    "password": "",
                    "edition": "",
                    "size": "",
                    "collation": "",
                    "location": "West US"
                }
            ]
        }
    }

You can edit the JSON configuration file to change what is deployed. A webSite section is required, but the database section is optional.

## <a name="next-steps"></a>Next steps
For more information, see [Publish-WebApplicationVM (Windows PowerShell script)](vs-azure-tools-publish-webapplicationvm.md)

