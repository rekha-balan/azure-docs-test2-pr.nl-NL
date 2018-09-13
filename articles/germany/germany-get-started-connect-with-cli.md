---
title: Connect to Azure Germany by using Azure CLI | Microsoft Docs
description: Information on managing your subscription in Azure Germany by using Azure CLI
services: germany
cloud: na
documentationcenter: na
author: gitralf
manager: rainerst
ms.assetid: na
ms.service: germany
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/13/2017
ms.author: ralfwi
ms.openlocfilehash: 51021bc01256ac0d1319ca90fd81baa8e509f28d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857185"
---
# <a name="connect-to-azure-germany-by-using-azure-cli"></a><span data-ttu-id="a0eee-103">Connect to Azure Germany by using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a0eee-103">Connect to Azure Germany by using Azure CLI</span></span>
<span data-ttu-id="a0eee-104">To use the Azure command-line interface (Azure CLI), you need to connect to Azure Germany instead of global Azure.</span><span class="sxs-lookup"><span data-stu-id="a0eee-104">To use the Azure command-line interface (Azure CLI), you need to connect to Azure Germany instead of global Azure.</span></span> <span data-ttu-id="a0eee-105">You can use Azure CLI to manage a large subscription through scripts or to access features that are not currently available in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a0eee-105">You can use Azure CLI to manage a large subscription through scripts or to access features that are not currently available in the Azure portal.</span></span> <span data-ttu-id="a0eee-106">If you have used Azure CLI in global Azure, it's mostly the same.</span><span class="sxs-lookup"><span data-stu-id="a0eee-106">If you have used Azure CLI in global Azure, it's mostly the same.</span></span>  

## <a name="azure-cli-20"></a><span data-ttu-id="a0eee-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a0eee-107">Azure CLI 2.0</span></span>
<span data-ttu-id="a0eee-108">There are multiple ways to [install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="a0eee-108">There are multiple ways to [install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>  

<span data-ttu-id="a0eee-109">To connect to Azure Germany, set the cloud:</span><span class="sxs-lookup"><span data-stu-id="a0eee-109">To connect to Azure Germany, set the cloud:</span></span>

```
az cloud set --name AzureGermanCloud
```

<span data-ttu-id="a0eee-110">After the cloud is set, you can log in:</span><span class="sxs-lookup"><span data-stu-id="a0eee-110">After the cloud is set, you can log in:</span></span>

```
az login --username your-user-name@your-tenant.onmicrosoft.de
```

<span data-ttu-id="a0eee-111">To confirm that the cloud is correctly set to AzureGermanCloud, run either of the following commands and then verify that the `isActive` flag is set to `true` for the AzureGermanCloud item:</span><span class="sxs-lookup"><span data-stu-id="a0eee-111">To confirm that the cloud is correctly set to AzureGermanCloud, run either of the following commands and then verify that the `isActive` flag is set to `true` for the AzureGermanCloud item:</span></span>

```
az cloud list
```

```
az cloud list --output table
```

## <a name="azure-cli-10"></a><span data-ttu-id="a0eee-112">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a0eee-112">Azure CLI 1.0</span></span>
<span data-ttu-id="a0eee-113">There are multiple ways to [install Azure CLI 1.0](../xplat-cli-install.md).</span><span class="sxs-lookup"><span data-stu-id="a0eee-113">There are multiple ways to [install Azure CLI 1.0](../xplat-cli-install.md).</span></span> <span data-ttu-id="a0eee-114">If you already have Node installed, the easiest way is to install the npm package.</span><span class="sxs-lookup"><span data-stu-id="a0eee-114">If you already have Node installed, the easiest way is to install the npm package.</span></span>

<span data-ttu-id="a0eee-115">To install CLI from an npm package, make sure you have downloaded and installed the [latest Node.js and npm](https://nodejs.org/en/download/package-manager/).</span><span class="sxs-lookup"><span data-stu-id="a0eee-115">To install CLI from an npm package, make sure you have downloaded and installed the [latest Node.js and npm](https://nodejs.org/en/download/package-manager/).</span></span> <span data-ttu-id="a0eee-116">Then, run **npm install** to install the azure-cli package:</span><span class="sxs-lookup"><span data-stu-id="a0eee-116">Then, run **npm install** to install the azure-cli package:</span></span>

```bash
npm install -g azure-cli
```

<span data-ttu-id="a0eee-117">On Linux distributions, you might need to use **sudo** to successfully run the **npm** command, as follows:</span><span class="sxs-lookup"><span data-stu-id="a0eee-117">On Linux distributions, you might need to use **sudo** to successfully run the **npm** command, as follows:</span></span>

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> <span data-ttu-id="a0eee-118">If you need to install or update Node.js and npm on your Linux distribution or OS, we recommend that you install the most recent Node.js LTS version (4.x).</span><span class="sxs-lookup"><span data-stu-id="a0eee-118">If you need to install or update Node.js and npm on your Linux distribution or OS, we recommend that you install the most recent Node.js LTS version (4.x).</span></span> <span data-ttu-id="a0eee-119">If you use an older version, you might get installation errors.</span><span class="sxs-lookup"><span data-stu-id="a0eee-119">If you use an older version, you might get installation errors.</span></span>


<span data-ttu-id="a0eee-120">After Azure CLI is installed, log in to Azure Germany:</span><span class="sxs-lookup"><span data-stu-id="a0eee-120">After Azure CLI is installed, log in to Azure Germany:</span></span>

```
azure login --username your-user-name@your-tenant.onmicrosoft.de  --environment AzureGermanCloud
```

<span data-ttu-id="a0eee-121">After you're logged in, you can run Azure CLI commands as you normally would:</span><span class="sxs-lookup"><span data-stu-id="a0eee-121">After you're logged in, you can run Azure CLI commands as you normally would:</span></span>

```
azure webapp list my-resource-group
```

## <a name="next-steps"></a><span data-ttu-id="a0eee-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="a0eee-122">Next steps</span></span>
<span data-ttu-id="a0eee-123">For more information about connecting to Azure Germany, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="a0eee-123">For more information about connecting to Azure Germany, see the following resources:</span></span>

* [<span data-ttu-id="a0eee-124">Connect to Azure Germany by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0eee-124">Connect to Azure Germany by using PowerShell</span></span>](./germany-get-started-connect-with-ps.md)
* [<span data-ttu-id="a0eee-125">Connect to Azure Germany by using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a0eee-125">Connect to Azure Germany by using Visual Studio</span></span>](./germany-get-started-connect-with-vs.md)
* [<span data-ttu-id="a0eee-126">Connect to Azure Germany by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="a0eee-126">Connect to Azure Germany by using the Azure portal</span></span>](./germany-get-started-connect-with-portal.md)




