---
title: Connect to Azure Stack with CLI | Microsoft Docs
description: Learn how to use the cross-platform command-line interface (CLI) to manage and deploy resources on Azure Stack
services: azure-stack
documentationcenter: ''
author: SnehaGunda
manager: byronr
editor: ''
ms.assetid: f576079c-5384-4c23-b5a4-9ae165d1e3c3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2016
ms.author: sngun
ms.openlocfilehash: 936bd7cd9fb953599579dc054a72d0a5470b5163
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670889"
---
# <a name="install-and-configure-azure-stack-cli"></a><span data-ttu-id="472a4-103">Install and configure Azure Stack CLI</span><span class="sxs-lookup"><span data-stu-id="472a4-103">Install and configure Azure Stack CLI</span></span>

<span data-ttu-id="472a4-104">In this document, we guide you through the process of using Azure Command-line Interface (CLI) to manage Azure Stack resources on Linux and Mac client platforms.</span><span class="sxs-lookup"><span data-stu-id="472a4-104">In this document, we guide you through the process of using Azure Command-line Interface (CLI) to manage Azure Stack resources on Linux and Mac client platforms.</span></span> <span data-ttu-id="472a4-105">The following steps required to connect to Azure Stack:</span><span class="sxs-lookup"><span data-stu-id="472a4-105">The following steps required to connect to Azure Stack:</span></span>

* [<span data-ttu-id="472a4-106">Install Node.js</span><span class="sxs-lookup"><span data-stu-id="472a4-106">Install Node.js</span></span>](#install-nodejs)
* [<span data-ttu-id="472a4-107">Install Azure Stack CLI</span><span class="sxs-lookup"><span data-stu-id="472a4-107">Install Azure Stack CLI</span></span>](#install-azure-stack-cli)
* [<span data-ttu-id="472a4-108">Connect to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="472a4-108">Connect to Azure Stack</span></span>](#connect-to-azure-stack)

## <a name="install-nodejs"></a><span data-ttu-id="472a4-109">Install Node.js</span><span class="sxs-lookup"><span data-stu-id="472a4-109">Install Node.js</span></span>
<span data-ttu-id="472a4-110">Azure Stack requires the **4.4.6** version of Node.js.</span><span class="sxs-lookup"><span data-stu-id="472a4-110">Azure Stack requires the **4.4.6** version of Node.js.</span></span> <span data-ttu-id="472a4-111">Navigate to https://nodejs.org/en/blog/release/v4.4.6/ and install the required version of Node.js for Windows, Mac OS or Linux machines.</span><span class="sxs-lookup"><span data-stu-id="472a4-111">Navigate to https://nodejs.org/en/blog/release/v4.4.6/ and install the required version of Node.js for Windows, Mac OS or Linux machines.</span></span>

## <a name="install-azure-stack-cli"></a><span data-ttu-id="472a4-112">Install Azure Stack CLI</span><span class="sxs-lookup"><span data-stu-id="472a4-112">Install Azure Stack CLI</span></span>
<span data-ttu-id="472a4-113">Azure Stack requires the **0.9.18** version of Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="472a4-113">Azure Stack requires the **0.9.18** version of Azure CLI.</span></span> <span data-ttu-id="472a4-114">Use the following command to install the required version of Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="472a4-114">Use the following command to install the required version of Azure CLI:</span></span>

```
npm install -g azure-cli@0.9.18
```

## <a name="connect-to-azure-stack"></a><span data-ttu-id="472a4-115">Connect to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="472a4-115">Connect to Azure Stack</span></span>
<span data-ttu-id="472a4-116">Use the following steps to connect to Azure Stack by using Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="472a4-116">Use the following steps to connect to Azure Stack by using Azure CLI:</span></span>

1. <span data-ttu-id="472a4-117">Open a PowerShell session and get the Active Directory Resource Id by running the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="472a4-117">Open a PowerShell session and get the Active Directory Resource Id by running the following PowerShell command:</span></span>

   ```
   PowerShell(Invoke-RestMethod -Uri https://management.local.azurestack.external/metadata/endpoints?api-version=2015-01-01 -Method Get).authentication.audiences[0]
   ```
   
2. <span data-ttu-id="472a4-118">Open a command prompt window and add the Azure Stack environment by using the following command, make sure to replace the `<Active directory resource ID>` with the value retrieved in the previous step:</span><span class="sxs-lookup"><span data-stu-id="472a4-118">Open a command prompt window and add the Azure Stack environment by using the following command, make sure to replace the `<Active directory resource ID>` with the value retrieved in the previous step:</span></span>

   ```
   azure account env add AzureStack --resource-manager-endpoint-url "https://management.local.azurestack.external" --management-endpoint-url "https://management.local.azurestack.external" --active-directory-endpoint-url  "https://login.windows.net" --portal-url "https://portal.local.azurestack.external" --gallery-endpoint-url "https://portal.local.azurestack.external/" --active-directory-resource-id "<Active directory resource ID>" --active-directory-graph-resource-id "https://graph.windows.net/"  
   ```

3. <span data-ttu-id="472a4-119">Disable the TLS certificate validation by running the following command:</span><span class="sxs-lookup"><span data-stu-id="472a4-119">Disable the TLS certificate validation by running the following command:</span></span>

   ```
   set NODE_TLS_REJECT_UNAUTHORIZED=0
   ```
   
4. <span data-ttu-id="472a4-120">Sign in to the Azure Stack administrator or user account by using the following command, make sure to replace the <username> and the <Password> with your Azure Stack administrator or user Active Directory account name.</span><span class="sxs-lookup"><span data-stu-id="472a4-120">Sign in to the Azure Stack administrator or user account by using the following command, make sure to replace the <username> and the <Password> with your Azure Stack administrator or user Active Directory account name.</span></span> 
   
   ```
   azure login -e AzureStack -u “<Active directory username>” -p "<Password>"
   ```
   <span data-ttu-id="472a4-121">For example, an Azure Stack service administrator can sign into their Azure Stack account as follows:</span><span class="sxs-lookup"><span data-stu-id="472a4-121">For example, an Azure Stack service administrator can sign into their Azure Stack account as follows:</span></span>
   
   ```
   azure login -e Azure -u "serviceadmin@contoso.onmicrosoft.com
   ```
   
5. <span data-ttu-id="472a4-122">Set the Azure configuration mode to Azure Resource Manager by using the following command:</span><span class="sxs-lookup"><span data-stu-id="472a4-122">Set the Azure configuration mode to Azure Resource Manager by using the following command:</span></span>

   ```
   azure config mode arm
   ```

6. <span data-ttu-id="472a4-123">After connecting, you can use the Azure CLI commands such as:</span><span class="sxs-lookup"><span data-stu-id="472a4-123">After connecting, you can use the Azure CLI commands such as:</span></span>

   ```
   # Get the list of subscriptions in the current account
   azure account list   

   # get the list of resources
   azure resource list
   ```

## <a name="next-steps"></a><span data-ttu-id="472a4-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="472a4-124">Next steps</span></span>

[<span data-ttu-id="472a4-125">Deploy templates with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="472a4-125">Deploy templates with Azure CLI</span></span>](azure-stack-deploy-template-command-line.md)

[<span data-ttu-id="472a4-126">Connect with PowerShell</span><span class="sxs-lookup"><span data-stu-id="472a4-126">Connect with PowerShell</span></span>](azure-stack-connect-powershell.md)

[<span data-ttu-id="472a4-127">Manage user permissions</span><span class="sxs-lookup"><span data-stu-id="472a4-127">Manage user permissions</span></span>](azure-stack-manage-permissions.md)

