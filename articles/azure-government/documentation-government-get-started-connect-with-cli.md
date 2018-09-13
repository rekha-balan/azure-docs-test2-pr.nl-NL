---
title: Connect to Azure Government with Azure CLI | Microsoft Docs
description: Information on managing your subscription in Azure Government by connecting with the Azure CLI
services: azure-government
cloud: gov
documentationcenter: ''
author: zakramer
manager: liki
ms.assetid: c7cbe993-375e-4aed-9aa5-2f4b2111f71c
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 03/19/2017
ms.author: zakramer
ms.openlocfilehash: 49c5d5a835ae5749e79de70e3b4e2e9418a333a8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563735"
---
# <a name="connect-to-azure-government-with-azure-command-line-interface-cli"></a>Connect to Azure Government with Azure Command Line Interface (CLI)
To use Azure CLI, you need to connect to Azure Government instead of Azure public. The Azure CLI can be used to manage a large subscription through script or to access features that are not currently available in the Azure portal. If you have used Azure CLI in Azure Public, it is mostly the same.  

## <a name="azure-cli-20"></a>Azure CLI 2.0
There are multiple ways to [install the Azure CLI v2](https://docs.microsoft.com/cli/azure/install-az-cli2).  

To connect to Azure Government, you set the cloud:

```
az cloud set --name AzureUSGovernment
```

After the cloud has been set, you can continue logging in:

```
az login --username your-user-name@your-gov-tenant.onmicrosoft.com
```

To confirm the cloud has correctly been set to AzureUSGovernment, run this command:

```
az cloud list
```

or

```
az cloud list --output table
```

and verify that the `isActive` flag is set to `true` for the AzureUSGovernment item.

## <a name="azure-cli-10"></a>Azure CLI 1.0
There are multiple ways to [install the Azure CLI v1](https://docs.microsoft.com/azure/xplat-cli-install). If you already have Node installed, the easiest way is to install the npm package:

To install the CLI from an npm package, make sure you have downloaded and installed the [latest Node.js and npm](https://nodejs.org/en/download/package-manager/). Then, run **npm install** to install the azure-cli package:

```bash
npm install -g azure-cli
```

On Linux distributions, you might need to use **sudo** to successfully run the **npm** command, as follows:

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> If you need to install or update Node.js and npm on your Linux distribution or OS, we recommend that you install the most recent Node.js LTS version (4.x). If you use an older version, you might get installation errors.


Once you have the Azure CLI installed, you need to log in to Azure Government:

```
azure login --username your-user-name@your-gov-tenant.onmicrosoft.com  --environment AzureUSGovernment
```

Once you are logged in, you can run Azure CLI commands as you normally would:

```
azure webapp list my-resource-group
```
