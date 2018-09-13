---
title: Publish-WebApplicationVM | Microsoft Docs
description: Learn how to deploy a web application to a virtual machine. This script creates the required resources in your Azure subscription if they don't exist.
services: visual-studio-online
author: ghogen
manager: douge
assetId: de4cec95-f73f-44d9-babd-9f47f2633cdb
ms.prod: visual-studio-dev15
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 11/11/2016
ms.author: ghogen
ms.openlocfilehash: c2dc6057eeb4eba1306309785e13192674bc43c6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44804250"
---
# <a name="publish-webapplicationvm-windows-powershell-script"></a>Publish-WebApplicationVM (Windows PowerShell script)
Deploys a web application to a virtual machine. The script creates the required resources in your Azure subscription if they don't exist.

```
Publish-WebApplicationVM
–Configuration <configuration>
-SubscriptionName <subscriptionName>
-WebDeployPackage <packageName>
-VMPassword @{Name = "name"; Password = "password")
-DatabaseServerPassword @{Name = "name"; Password = "password"}
-SendHostMessagesToOutput
-Verbose
```

### <a name="configuration"></a>Configuration
The path to the JSON configuration file that describes the details of the deployment.

| Aliases | none |
| --- | --- |
| Required? |true |
| Position |named |
| Default value |none |
| Accept pipeline input? |false |
| Accept wildcard characters? |false |

### <a name="subscriptionname"></a>SubscriptionName
The name of the Azure subscription in which you want to create the virtual machine.

| Aliases | none |
| --- | --- |
| Required? |false |
| Position |named |
| Default value |Uses the first subscription in the subscription file |
| Accept pipeline input? |false |
| Accept wildcard characters? |false |

### <a name="webdeploypackage"></a>WebDeployPackage
The path to the web deployment package to publish to the virtual machine. You can create this package by using the Publish Web wizard in Visual Studio. See [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).

| Aliases | none |
| --- | --- |
| Required? |false |
| Position |named |
| Default value |none |
| Accept pipeline input? |false |
| Accept wildcard characters? |false |

### <a name="allowuntrusted"></a>AllowUntrusted
If true, allow the use of certificates that aren't signed by a trusted root authority.

| Aliases | none |
| --- | --- |
| Required? |false |
| Position |named |
| Default value |false |
| Accept pipeline input? |false |
| Accept wildcard characters? |false |

### <a name="vmpassword"></a>VMPassword
The credentials for the virtual machine account. Example: -VMPassword @{Name = "admin"; Password = "password"}

| Aliases | none |
| --- | --- |
| Required? |false |
| Position |named |
| Default value |none |
| Accept pipeline input? |false |
| Accept wildcard characters? |false |

### <a name="databaseserverpassword"></a>DatabaseServerPassword
The credentials for the SQL database in Azure. Example: -DatabaseServerPassword @{Name = "admin"; Password = "password"}

| Aliases | none |
| --- | --- |
| Required? |false |
| Position |named |
| Default value |none |
| Accept pipeline input? |false |
| Accept wildcard characters? |false |

### <a name="sendhostmessagestooutput"></a>SendHostMessagesToOutput
If true, print messages from the script to the output stream.

| Aliases | none |
| --- | --- |
| Required? |false |
| Position |named |
| Default value |false |
| Accept pipeline input? |false |
| Accept wildcard characters? |false |

## <a name="remarks"></a>Remarks
For a complete explanation of how to use the script to create Dev and Test environments, see [Using Windows PowerShell Scripts to Publish to Dev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).

The JSON configuration file specifies the details of what is to be deployed. It includes the information that you specified when you created the project, such as the name, affinity group, VHD image, and size of the virtual machine. It also includes the endpoints on the virtual machine, the databases to provision, if any, and web deployment parameters. The following code shows an example JSON configuration file:

```
{
    "environmentSettings": {
        "cloudService": {
            "name": "myvmname",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myvmname",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201404.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [
                    {
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [
            {
                "connectionStringName": "",
                "databaseName": "",
                "serverName": "",
                "user": "",
                "password": ""
            }
        ],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

You can edit the JSON configuration file to change what is provisioned. A virtual machine and a cloud service are required, but the database section is optional.

