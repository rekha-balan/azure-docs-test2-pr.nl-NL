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
# <a name="connect-to-azure-government-with-azure-command-line-interface-cli"></a><span data-ttu-id="16cc7-103">Connect to Azure Government with Azure Command Line Interface (CLI)</span><span class="sxs-lookup"><span data-stu-id="16cc7-103">Connect to Azure Government with Azure Command Line Interface (CLI)</span></span>
<span data-ttu-id="16cc7-104">To use Azure CLI, you need to connect to Azure Government instead of Azure public.</span><span class="sxs-lookup"><span data-stu-id="16cc7-104">To use Azure CLI, you need to connect to Azure Government instead of Azure public.</span></span> <span data-ttu-id="16cc7-105">The Azure CLI can be used to manage a large subscription through script or to access features that are not currently available in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="16cc7-105">The Azure CLI can be used to manage a large subscription through script or to access features that are not currently available in the Azure portal.</span></span> <span data-ttu-id="16cc7-106">If you have used Azure CLI in Azure Public, it is mostly the same.</span><span class="sxs-lookup"><span data-stu-id="16cc7-106">If you have used Azure CLI in Azure Public, it is mostly the same.</span></span>  

## <a name="azure-cli-20"></a><span data-ttu-id="16cc7-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="16cc7-107">Azure CLI 2.0</span></span>
<span data-ttu-id="16cc7-108">There are multiple ways to [install the Azure CLI v2](https://docs.microsoft.com/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="16cc7-108">There are multiple ways to [install the Azure CLI v2](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>  

<span data-ttu-id="16cc7-109">To connect to Azure Government, you set the cloud:</span><span class="sxs-lookup"><span data-stu-id="16cc7-109">To connect to Azure Government, you set the cloud:</span></span>

```
az cloud set --name AzureUSGovernment
```

<span data-ttu-id="16cc7-110">After the cloud has been set, you can continue logging in:</span><span class="sxs-lookup"><span data-stu-id="16cc7-110">After the cloud has been set, you can continue logging in:</span></span>

```
az login --username your-user-name@your-gov-tenant.onmicrosoft.com
```

<span data-ttu-id="16cc7-111">To confirm the cloud has correctly been set to AzureUSGovernment, run this command:</span><span class="sxs-lookup"><span data-stu-id="16cc7-111">To confirm the cloud has correctly been set to AzureUSGovernment, run this command:</span></span>

```
az cloud list
```

<span data-ttu-id="16cc7-112">or</span><span class="sxs-lookup"><span data-stu-id="16cc7-112">or</span></span>

```
az cloud list --output table
```

<span data-ttu-id="16cc7-113">and verify that the `isActive` flag is set to `true` for the AzureUSGovernment item.</span><span class="sxs-lookup"><span data-stu-id="16cc7-113">and verify that the `isActive` flag is set to `true` for the AzureUSGovernment item.</span></span>

## <a name="azure-cli-10"></a><span data-ttu-id="16cc7-114">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="16cc7-114">Azure CLI 1.0</span></span>
<span data-ttu-id="16cc7-115">There are multiple ways to [install the Azure CLI v1](https://docs.microsoft.com/azure/xplat-cli-install).</span><span class="sxs-lookup"><span data-stu-id="16cc7-115">There are multiple ways to [install the Azure CLI v1](https://docs.microsoft.com/azure/xplat-cli-install).</span></span> <span data-ttu-id="16cc7-116">If you already have Node installed, the easiest way is to install the npm package:</span><span class="sxs-lookup"><span data-stu-id="16cc7-116">If you already have Node installed, the easiest way is to install the npm package:</span></span>

<span data-ttu-id="16cc7-117">To install the CLI from an npm package, make sure you have downloaded and installed the [latest Node.js and npm](https://nodejs.org/en/download/package-manager/).</span><span class="sxs-lookup"><span data-stu-id="16cc7-117">To install the CLI from an npm package, make sure you have downloaded and installed the [latest Node.js and npm](https://nodejs.org/en/download/package-manager/).</span></span> <span data-ttu-id="16cc7-118">Then, run **npm install** to install the azure-cli package:</span><span class="sxs-lookup"><span data-stu-id="16cc7-118">Then, run **npm install** to install the azure-cli package:</span></span>

```bash
npm install -g azure-cli
```

<span data-ttu-id="16cc7-119">On Linux distributions, you might need to use **sudo** to successfully run the **npm** command, as follows:</span><span class="sxs-lookup"><span data-stu-id="16cc7-119">On Linux distributions, you might need to use **sudo** to successfully run the **npm** command, as follows:</span></span>

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> <span data-ttu-id="16cc7-120">If you need to install or update Node.js and npm on your Linux distribution or OS, we recommend that you install the most recent Node.js LTS version (4.x).</span><span class="sxs-lookup"><span data-stu-id="16cc7-120">If you need to install or update Node.js and npm on your Linux distribution or OS, we recommend that you install the most recent Node.js LTS version (4.x).</span></span> <span data-ttu-id="16cc7-121">If you use an older version, you might get installation errors.</span><span class="sxs-lookup"><span data-stu-id="16cc7-121">If you use an older version, you might get installation errors.</span></span>


<span data-ttu-id="16cc7-122">Once you have the Azure CLI installed, you need to log in to Azure Government:</span><span class="sxs-lookup"><span data-stu-id="16cc7-122">Once you have the Azure CLI installed, you need to log in to Azure Government:</span></span>

```
azure login --username your-user-name@your-gov-tenant.onmicrosoft.com  --environment AzureUSGovernment
```

<span data-ttu-id="16cc7-123">Once you are logged in, you can run Azure CLI commands as you normally would:</span><span class="sxs-lookup"><span data-stu-id="16cc7-123">Once you are logged in, you can run Azure CLI commands as you normally would:</span></span>

```
azure webapp list my-resource-group
```
