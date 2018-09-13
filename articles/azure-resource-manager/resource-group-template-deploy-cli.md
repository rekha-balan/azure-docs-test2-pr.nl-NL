---
title: Deploy resources with Azure CLI and template | Microsoft Docs
description: Use Azure Resource Manager and Azure CLI to deploy a resources to Azure. The resources are defined in a Resource Manager template.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 493b7932-8d1e-4499-912c-26098282ec95
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: tomfitz
ms.openlocfilehash: 0320aafd5eed1b3ef658d5f020fc37ba1dcff308
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551438"
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-cli"></a><span data-ttu-id="4a6e8-104">Deploy resources with Resource Manager templates and Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4a6e8-104">Deploy resources with Resource Manager templates and Azure CLI</span></span>
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-template-deploy.md)
> * [Azure CLI](resource-group-template-deploy-cli.md)
> * [Portal](resource-group-template-deploy-portal.md)
> * [REST API](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="4a6e8-109">This topic explains how to use [Azure CLI 2.0](/cli/azure/install-az-cli2) with Resource Manager templates to deploy your resources to Azure.</span><span class="sxs-lookup"><span data-stu-id="4a6e8-109">This topic explains how to use [Azure CLI 2.0](/cli/azure/install-az-cli2) with Resource Manager templates to deploy your resources to Azure.</span></span>  <span data-ttu-id="4a6e8-110">Your template can be either a local file or an external file that is available through a URI.</span><span class="sxs-lookup"><span data-stu-id="4a6e8-110">Your template can be either a local file or an external file that is available through a URI.</span></span> <span data-ttu-id="4a6e8-111">When your template resides in a storage account, you can restrict access to the template and provide a shared access signature (SAS) token during deployment.</span><span class="sxs-lookup"><span data-stu-id="4a6e8-111">When your template resides in a storage account, you can restrict access to the template and provide a shared access signature (SAS) token during deployment.</span></span>

## <a name="deploy"></a><span data-ttu-id="4a6e8-112">Deploy</span><span class="sxs-lookup"><span data-stu-id="4a6e8-112">Deploy</span></span>

* <span data-ttu-id="4a6e8-113">To quickly get started with deployment, use the following commands to deploy a local template with inline parameters:</span><span class="sxs-lookup"><span data-stu-id="4a6e8-113">To quickly get started with deployment, use the following commands to deploy a local template with inline parameters:</span></span>

  ```azurecli
  az login
  az account set --subscription {subscription-id}

  az group create --name ExampleGroup --location "Central US"
  az group deployment create \
      --name ExampleDeployment \
      --resource-group ExampleGroup \
      --template-file storage.json \
      --parameters '{"storageNamePrefix":{"value":"contoso"},"storageSKU":{"value":"Standard_GRS"}}'
  ```

  <span data-ttu-id="4a6e8-114">The deployment can take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="4a6e8-114">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="4a6e8-115">When it finishes, you see a message that includes the result:</span><span class="sxs-lookup"><span data-stu-id="4a6e8-115">When it finishes, you see a message that includes the result:</span></span>

  ```azurecli
  "provisioningState": "Succeeded",
  ```
  
* <span data-ttu-id="4a6e8-116">The `az account set` command is only needed if you want to use a subscription other than your default subscription.</span><span class="sxs-lookup"><span data-stu-id="4a6e8-116">The `az account set` command is only needed if you want to use a subscription other than your default subscription.</span></span> <span data-ttu-id="4a6e8-117">To see all your subscriptions and their IDs, use:</span><span class="sxs-lookup"><span data-stu-id="4a6e8-117">To see all your subscriptions and their IDs, use:</span></span>

  ```azurecli
  az account list
  ```

* <span data-ttu-id="4a6e8-118">To deploy an external template, use the **template-uri** parameter:</span><span class="sxs-lookup"><span data-stu-id="4a6e8-118">To deploy an external template, use the **template-uri** parameter:</span></span>
   
   ```azurecli
   az group deployment create \
       --name ExampleDeployment \
       --resource-group ExampleGroup \
       --template-uri "https://raw.githubusercontent.com/exampleuser/MyTemplates/master/storage.json" \
       --parameters '{"storageNamePrefix":{"value":"contoso"},"storageSKU":{"value":"Standard_GRS"}}'
   ```

* <span data-ttu-id="4a6e8-119">To pass the parameter values in a file, use:</span><span class="sxs-lookup"><span data-stu-id="4a6e8-119">To pass the parameter values in a file, use:</span></span>

   ```azurecli
   az group deployment create \
       --name ExampleDeployment \
       --resource-group ExampleGroup \
       --template-file storage.json \
       --parameters @storage.parameters.json
   ```

   <span data-ttu-id="4a6e8-120">The parameter file must be in the following format:</span><span class="sxs-lookup"><span data-stu-id="4a6e8-120">The parameter file must be in the following format:</span></span>

   ```json
   {
     "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
     "contentVersion": "1.0.0.0",
     "parameters": {
        "storageNamePrefix": {
            "value": "contoso"
        },
        "storageSKU": {
            "value": "Standard_GRS"
        }
     }
   }
   ```


[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

<span data-ttu-id="4a6e8-121">To use complete mode, use the mode parameter:</span><span class="sxs-lookup"><span data-stu-id="4a6e8-121">To use complete mode, use the mode parameter:</span></span>

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --mode Complete \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters '{"storageNamePrefix":{"value":"contoso"},"storageSKU":{"value":"Standard_GRS"}}'
```

## <a name="deploy-template-from-storage-with-sas-token"></a><span data-ttu-id="4a6e8-122">Deploy template from storage with SAS token</span><span class="sxs-lookup"><span data-stu-id="4a6e8-122">Deploy template from storage with SAS token</span></span>
<span data-ttu-id="4a6e8-123">You can add your templates to a storage account and link to them during deployment with a SAS token.</span><span class="sxs-lookup"><span data-stu-id="4a6e8-123">You can add your templates to a storage account and link to them during deployment with a SAS token.</span></span>

> [!IMPORTANT]
> By following the steps below, the blob containing the template is accessible to only the account owner. However, when you create a SAS token for the blob, the blob is accessible to anyone with that URI. If another user intercepts the URI, that user is able to access the template. Using a SAS token is a good way of limiting access to your templates, but you should not include sensitive data like passwords directly in the template.
> 
> 

### <a name="add-private-template-to-storage-account"></a><span data-ttu-id="4a6e8-128">Add private template to storage account</span><span class="sxs-lookup"><span data-stu-id="4a6e8-128">Add private template to storage account</span></span>
<span data-ttu-id="4a6e8-129">The following example sets up a private storage account container and uploads a template:</span><span class="sxs-lookup"><span data-stu-id="4a6e8-129">The following example sets up a private storage account container and uploads a template:</span></span>
   
```azurecli
az group create --name "ManageGroup" --location "South Central US"
az storage account create \
    --resource-group ManageGroup \
    --location "South Central US" \
    --sku Standard_LRS \
    --kind Storage \
    --name {your-unique-name}
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
az storage container create \
    --name templates \
    --public-access Off \
    --connection-string $connection
az storage blob upload \
    --container-name templates \
    --file vmlinux.json \
    --name vmlinux.json \
    --connection-string $connection
```

### <a name="provide-sas-token-during-deployment"></a><span data-ttu-id="4a6e8-130">Provide SAS token during deployment</span><span class="sxs-lookup"><span data-stu-id="4a6e8-130">Provide SAS token during deployment</span></span>
<span data-ttu-id="4a6e8-131">To deploy a private template in a storage account, generate a SAS token and include it in the URI for the template.</span><span class="sxs-lookup"><span data-stu-id="4a6e8-131">To deploy a private template in a storage account, generate a SAS token and include it in the URI for the template.</span></span> <span data-ttu-id="4a6e8-132">Set the expiry time to allow enough time to complete the deployment.</span><span class="sxs-lookup"><span data-stu-id="4a6e8-132">Set the expiry time to allow enough time to complete the deployment.</span></span>
   
```azurecli
seconds='@'$(( $(date +%s) + 1800 ))
expiretime=$(date +%Y-%m-%dT%H:%MZ --date=$seconds)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
token=$(az storage blob generate-sas \
    --container-name templates \
    --name vmlinux.json \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name vmlinux.json \
    --output tsv \
    --connection-string $connection)
az group deployment create --resource-group ExampleGroup --template-uri $url?$token
```

<span data-ttu-id="4a6e8-133">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="4a6e8-133">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="debug"></a><span data-ttu-id="4a6e8-134">Debug</span><span class="sxs-lookup"><span data-stu-id="4a6e8-134">Debug</span></span>

<span data-ttu-id="4a6e8-135">To see information about the operations for a failed deployment, use:</span><span class="sxs-lookup"><span data-stu-id="4a6e8-135">To see information about the operations for a failed deployment, use:</span></span>
   
```azurecli
az group deployment operation list --resource-group ExampleGroup --name vmlinux --query "[*].[properties.statusMessage]"
```

<span data-ttu-id="4a6e8-136">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="4a6e8-136">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="complete-deployment-script"></a><span data-ttu-id="4a6e8-137">Complete deployment script</span><span class="sxs-lookup"><span data-stu-id="4a6e8-137">Complete deployment script</span></span>

<span data-ttu-id="4a6e8-138">The following example shows the Azure CLI 2.0 script for deploying a template that is generated by the [export template](resource-manager-export-template.md) feature:</span><span class="sxs-lookup"><span data-stu-id="4a6e8-138">The following example shows the Azure CLI 2.0 script for deploying a template that is generated by the [export template](resource-manager-export-template.md) feature:</span></span>

```azurecli
#!/bin/bash
set -euo pipefail
IFS=$'\n\t'

# -e: immediately exit if any command has a non-zero exit status
# -o: prevents errors in a pipeline from being masked
# IFS new value is less likely to cause confusing bugs when looping arrays or arguments (e.g. $@)

usage() { echo "Usage: $0 -i <subscriptionId> -g <resourceGroupName> -n <deploymentName> -l <resourceGroupLocation>" 1>&2; exit 1; }

declare subscriptionId=""
declare resourceGroupName=""
declare deploymentName=""
declare resourceGroupLocation=""

# Initialize parameters specified from command line
while getopts ":i:g:n:l:" arg; do
    case "${arg}" in
        i)
            subscriptionId=${OPTARG}
            ;;
        g)
            resourceGroupName=${OPTARG}
            ;;
        n)
            deploymentName=${OPTARG}
            ;;
        l)
            resourceGroupLocation=${OPTARG}
            ;;
        esac
done
shift $((OPTIND-1))

#Prompt for parameters is some required parameters are missing
if [[ -z "$subscriptionId" ]]; then
    echo "Subscription Id:"
    read subscriptionId
    [[ "${subscriptionId:?}" ]]
fi

if [[ -z "$resourceGroupName" ]]; then
    echo "ResourceGroupName:"
    read resourceGroupName
    [[ "${resourceGroupName:?}" ]]
fi

if [[ -z "$deploymentName" ]]; then
    echo "DeploymentName:"
    read deploymentName
fi

if [[ -z "$resourceGroupLocation" ]]; then
    echo "Enter a location below to create a new resource group else skip this"
    echo "ResourceGroupLocation:"
    read resourceGroupLocation
fi

#templateFile Path - template file to be used
templateFilePath="template.json"

if [ ! -f "$templateFilePath" ]; then
    echo "$templateFilePath not found"
    exit 1
fi

#parameter file path
parametersFilePath="parameters.json"

if [ ! -f "$parametersFilePath" ]; then
    echo "$parametersFilePath not found"
    exit 1
fi

if [ -z "$subscriptionId" ] || [ -z "$resourceGroupName" ] || [ -z "$deploymentName" ]; then
    echo "Either one of subscriptionId, resourceGroupName, deploymentName is empty"
    usage
fi

#login to azure using your credentials
az account show 1> /dev/null

if [ $? != 0 ];
then
    az login
fi

#set the default subscription id
az account set --name $subscriptionId

set +e

#Check for existing RG
az group show $resourceGroupName 1> /dev/null

if [ $? != 0 ]; then
    echo "Resource group with name" $resourceGroupName "could not be found. Creating new resource group.."
    set -e
    (
        set -x
        az resource group create --name $resourceGroupName --location $resourceGroupLocation 1> /dev/null
    )
    else
    echo "Using existing resource group..."
fi

#Start deployment
echo "Starting deployment..."
(
    set -x
    az resource group deployment create --name $deploymentName --resource-group $resourceGroupName --template-file $templateFilePath --parameters $parametersFilePath
)

if [ $?  == 0 ];
 then
    echo "Template has been successfully deployed"
fi
```

## <a name="next-steps"></a><span data-ttu-id="4a6e8-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="4a6e8-139">Next steps</span></span>
* <span data-ttu-id="4a6e8-140">For an example of deploying resources through the .NET client library, see [Deploy resources using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4a6e8-140">For an example of deploying resources through the .NET client library, see [Deploy resources using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="4a6e8-141">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="4a6e8-141">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="4a6e8-142">For guidance on deploying your solution to different environments, see [Development and test environments in Microsoft Azure](solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="4a6e8-142">For guidance on deploying your solution to different environments, see [Development and test environments in Microsoft Azure](solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="4a6e8-143">For details about using a KeyVault reference to pass secure values, see [Pass secure values during deployment](resource-manager-keyvault-parameter.md).</span><span class="sxs-lookup"><span data-stu-id="4a6e8-143">For details about using a KeyVault reference to pass secure values, see [Pass secure values during deployment](resource-manager-keyvault-parameter.md).</span></span>
* <span data-ttu-id="4a6e8-144">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="4a6e8-144">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="4a6e8-145">For a four part series about automating deployment, see [Automating application deployments to Azure Virtual Machines](../virtual-machines/windows/dotnet-core-1-landing.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4a6e8-145">For a four part series about automating deployment, see [Automating application deployments to Azure Virtual Machines](../virtual-machines/windows/dotnet-core-1-landing.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="4a6e8-146">This series covers application architecture, access and security, availability and scale, and application deployment.</span><span class="sxs-lookup"><span data-stu-id="4a6e8-146">This series covers application architecture, access and security, availability and scale, and application deployment.</span></span>

