---
title: Deploy templates with the command line in Azure Stack | Microsoft Docs
description: Learn how to use the cross-platform command line interface (CLI) to deploy templates from inside the ClientVM or after using the VPN to connect to Azure Stack.
services: azure-stack
documentationcenter: ''
author: heathl17
manager: byronr
editor: ''
ms.assetid: 9584177f-4af3-4834-864d-930b09ae0995
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/12/2016
ms.author: helaw
ms.openlocfilehash: 030e5ec3dea1ae498daf1936a9d92e9d11001704
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551648"
---
# <a name="deploy-templates-in-azure-stack-using-the-command-line"></a><span data-ttu-id="a46d4-103">Deploy templates in Azure Stack using the command line</span><span class="sxs-lookup"><span data-stu-id="a46d4-103">Deploy templates in Azure Stack using the command line</span></span>
<span data-ttu-id="a46d4-104">Use the command line to deploy Azure Resource Manager templates to the Azure Stack POC.</span><span class="sxs-lookup"><span data-stu-id="a46d4-104">Use the command line to deploy Azure Resource Manager templates to the Azure Stack POC.</span></span> <span data-ttu-id="a46d4-105">Azure Resource Manager templates deploy and provision all the resources for your application in a single, coordinated operation.</span><span class="sxs-lookup"><span data-stu-id="a46d4-105">Azure Resource Manager templates deploy and provision all the resources for your application in a single, coordinated operation.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a46d4-106">Before you begin</span><span class="sxs-lookup"><span data-stu-id="a46d4-106">Before you begin</span></span>
 - <span data-ttu-id="a46d4-107">[Install and connect](azure-stack-connect-cli.md) to Azure Stack with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a46d4-107">[Install and connect](azure-stack-connect-cli.md) to Azure Stack with Azure CLI</span></span>
 - <span data-ttu-id="a46d4-108">Download the files *azuredeploy.json* and *azuredeploy.parameters.json* from the [create storage account example template](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-create-storage-account).</span><span class="sxs-lookup"><span data-stu-id="a46d4-108">Download the files *azuredeploy.json* and *azuredeploy.parameters.json* from the [create storage account example template](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-create-storage-account).</span></span>
 
## <a name="deploy-template"></a><span data-ttu-id="a46d4-109">Deploy template</span><span class="sxs-lookup"><span data-stu-id="a46d4-109">Deploy template</span></span>
<span data-ttu-id="a46d4-110">Navigate to the folder where these files were downloaded and run the following command to deploy the template:</span><span class="sxs-lookup"><span data-stu-id="a46d4-110">Navigate to the folder where these files were downloaded and run the following command to deploy the template:</span></span>

    azure group create "cliRG" "local" –f azuredeploy.json –d "testDeploy" –e azuredeploy.parameters.json

<span data-ttu-id="a46d4-111">This command deploys the template to the resource group **cliRG** in the Azure Stack POC’s default location.</span><span class="sxs-lookup"><span data-stu-id="a46d4-111">This command deploys the template to the resource group **cliRG** in the Azure Stack POC’s default location.</span></span>

## <a name="validate-template-deployment"></a><span data-ttu-id="a46d4-112">Validate template deployment</span><span class="sxs-lookup"><span data-stu-id="a46d4-112">Validate template deployment</span></span>
<span data-ttu-id="a46d4-113">To see this resource group and storage account, use the following commands:</span><span class="sxs-lookup"><span data-stu-id="a46d4-113">To see this resource group and storage account, use the following commands:</span></span>

    azure group list

    azure storage account list

## <a name="next-steps"></a><span data-ttu-id="a46d4-114">Next steps</span><span class="sxs-lookup"><span data-stu-id="a46d4-114">Next steps</span></span>
[<span data-ttu-id="a46d4-115">Manage user permissions</span><span class="sxs-lookup"><span data-stu-id="a46d4-115">Manage user permissions</span></span>](azure-stack-manage-permissions.md)

