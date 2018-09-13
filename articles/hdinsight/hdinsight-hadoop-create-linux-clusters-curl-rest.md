---
title: Create Azure HDInsight (Hadoop) using cURL and REST | Microsoft Docs
description: Learn how to create HDInsight clusters using cURL, Azure Resource Manager templates, and the Azure REST API. You can specify the cluster type (Hadoop, HBase, or Storm,) or use scripts to install custom components.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 98be5893-2c6f-4dfa-95ec-d4d8b5b7dcb5
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/17/2017
ms.author: larryfr
ms.openlocfilehash: c3440ac34a195bfc831ee2fa2ff916b16e92a2ac
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669815"
---
# <a name="create-hdinsight-clusters-using-curl-and-the-azure-rest-api"></a><span data-ttu-id="82c0f-104">Create HDInsight clusters using cURL and the Azure REST API</span><span class="sxs-lookup"><span data-stu-id="82c0f-104">Create HDInsight clusters using cURL and the Azure REST API</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="82c0f-105">Learn how to create an HDInsight cluster using an Azure Resource Manager template and the Azure REST API.</span><span class="sxs-lookup"><span data-stu-id="82c0f-105">Learn how to create an HDInsight cluster using an Azure Resource Manager template and the Azure REST API.</span></span>

<span data-ttu-id="82c0f-106">The Azure REST API allows you to perform management operations on services hosted in the Azure platform, including the creation of new resources such as HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="82c0f-106">The Azure REST API allows you to perform management operations on services hosted in the Azure platform, including the creation of new resources such as HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="82c0f-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="82c0f-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="82c0f-108">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="82c0f-108">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82c0f-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="82c0f-109">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="82c0f-110">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="82c0f-110">**An Azure subscription**.</span></span> <span data-ttu-id="82c0f-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="82c0f-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="82c0f-112">**Azure CLI 2.0** (preview).</span><span class="sxs-lookup"><span data-stu-id="82c0f-112">**Azure CLI 2.0** (preview).</span></span> <span data-ttu-id="82c0f-113">The Azure CLI is used to create a service principal, which is then used to generate authentication tokens for requests to the Azure REST API.</span><span class="sxs-lookup"><span data-stu-id="82c0f-113">The Azure CLI is used to create a service principal, which is then used to generate authentication tokens for requests to the Azure REST API.</span></span> <span data-ttu-id="82c0f-114">For more information on the Azure CLI 2.0 preview, see [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="82c0f-114">For more information on the Azure CLI 2.0 preview, see [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

* <span data-ttu-id="82c0f-115">**cURL**.</span><span class="sxs-lookup"><span data-stu-id="82c0f-115">**cURL**.</span></span> <span data-ttu-id="82c0f-116">This utility is available through your package management system, or can be downloaded from [http://curl.haxx.se/](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="82c0f-116">This utility is available through your package management system, or can be downloaded from [http://curl.haxx.se/](http://curl.haxx.se/).</span></span>

  > [!NOTE]
  > <span data-ttu-id="82c0f-117">If you are using PowerShell to run the commands in this document, you must first remove the `curl` alias that it creates by default.</span><span class="sxs-lookup"><span data-stu-id="82c0f-117">If you are using PowerShell to run the commands in this document, you must first remove the `curl` alias that it creates by default.</span></span> <span data-ttu-id="82c0f-118">This alias uses Invoke-WebRequest instead of cURL.</span><span class="sxs-lookup"><span data-stu-id="82c0f-118">This alias uses Invoke-WebRequest instead of cURL.</span></span> <span data-ttu-id="82c0f-119">If you do not remove this alias, you may receive errors with some of the commands used in this document.</span><span class="sxs-lookup"><span data-stu-id="82c0f-119">If you do not remove this alias, you may receive errors with some of the commands used in this document.</span></span>
  >
  > <span data-ttu-id="82c0f-120">To remove this alias, use the following command from the PowerShell prompt:</span><span class="sxs-lookup"><span data-stu-id="82c0f-120">To remove this alias, use the following command from the PowerShell prompt:</span></span>
  >
  > `Remove-item alias:curl`
  >
  > <span data-ttu-id="82c0f-121">Once the alias has been removed, you should be able to use the version of cURL that you have installed on your system.</span><span class="sxs-lookup"><span data-stu-id="82c0f-121">Once the alias has been removed, you should be able to use the version of cURL that you have installed on your system.</span></span>

### <a name="access-control-requirements"></a><span data-ttu-id="82c0f-122">Access control requirements</span><span class="sxs-lookup"><span data-stu-id="82c0f-122">Access control requirements</span></span>

[!INCLUDE [access-control](../../includes/hdinsight-access-control-requirements.md)]

## <a name="create-a-template"></a><span data-ttu-id="82c0f-123">Create a template</span><span class="sxs-lookup"><span data-stu-id="82c0f-123">Create a template</span></span>

<span data-ttu-id="82c0f-124">Azure Resource Manager templates are JSON documents that describe a **resource group** and all resources in it (such as HDInsight.) This template-based approach allows you to define the resources that you need for HDInsight in one template.</span><span class="sxs-lookup"><span data-stu-id="82c0f-124">Azure Resource Manager templates are JSON documents that describe a **resource group** and all resources in it (such as HDInsight.) This template-based approach allows you to define the resources that you need for HDInsight in one template.</span></span>

<span data-ttu-id="82c0f-125">The following is a merger of the template and parameters files from [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), which creates a Linux-based cluster using a password to secure the SSH user account.</span><span class="sxs-lookup"><span data-stu-id="82c0f-125">The following is a merger of the template and parameters files from [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), which creates a Linux-based cluster using a password to secure the SSH user account.</span></span>

   ```json
   {
       "properties": {
           "template": {
               "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
               "contentVersion": "1.0.0.0",
               "parameters": {
                   "location": {
                       "type": "string",
                       "allowedValues": ["Central US",
                       "East Asia",
                       "East US",
                       "Japan East",
                       "Japan West",
                       "North Europe",
                       "South Central US",
                       "Southeast Asia",
                       "West Europe",
                       "West US"],
                       "metadata": {
                           "description": "The location where all azure resources are deployed."
                       }
                   },
                   "clusterType": {
                       "type": "string",
                       "allowedValues": ["hadoop",
                       "hbase",
                       "storm",
                       "spark"],
                       "metadata": {
                           "description": "The type of the HDInsight cluster to create."
                       }
                   },
                   "clusterName": {
                       "type": "string",
                       "metadata": {
                           "description": "The name of the HDInsight cluster to create."
                       }
                   },
                   "clusterLoginUserName": {
                       "type": "string",
                       "metadata": {
                           "description": "These credentials can be used to submit jobs to the cluster and to log into cluster dashboards."
                       }
                   },
                   "clusterLoginPassword": {
                       "type": "securestring",
                       "metadata": {
                           "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
                       }
                   },
                   "sshUserName": {
                       "type": "string",
                       "metadata": {
                           "description": "These credentials can be used to remotely access the cluster."
                       }
                   },
                   "sshPassword": {
                       "type": "securestring",
                       "metadata": {
                           "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
                       }
                   },
                   "clusterStorageAccountName": {
                       "type": "string",
                       "metadata": {
                           "description": "The name of the storage account to be created and be used as the cluster's storage."
                       }
                   },
                   "clusterWorkerNodeCount": {
                       "type": "int",
                       "defaultValue": 4,
                       "metadata": {
                           "description": "The number of nodes in the HDInsight cluster."
                       }
                   }
               },
               "variables": {
                   "defaultApiVersion": "2015-05-01-preview",
                   "clusterApiVersion": "2015-03-01-preview"
               },
               "resources": [{
                   "name": "[parameters('clusterStorageAccountName')]",
                   "type": "Microsoft.Storage/storageAccounts",
                   "location": "[parameters('location')]",
                   "apiVersion": "[variables('defaultApiVersion')]",
                   "dependsOn": [],
                   "tags": {

                   },
                   "properties": {
                       "accountType": "Standard_LRS"
                   }
               },
               {
                   "name": "[parameters('clusterName')]",
                   "type": "Microsoft.HDInsight/clusters",
                   "location": "[parameters('location')]",
                   "apiVersion": "[variables('clusterApiVersion')]",
                   "dependsOn": ["[concat('Microsoft.Storage/storageAccounts/',parameters('clusterStorageAccountName'))]"],
                   "tags": {

                   },
                   "properties": {
                       "clusterVersion": "3.5",
                       "osType": "Linux",
                       "clusterDefinition": {
                           "kind": "[parameters('clusterType')]",
                           "configurations": {
                               "gateway": {
                                   "restAuthCredential.isEnabled": true,
                                   "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                                   "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                               }
                           }
                       },
                       "storageProfile": {
                           "storageaccounts": [{
                               "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                               "isDefault": true,
                               "container": "[parameters('clusterName')]",
                               "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), variables('defaultApiVersion')).key1]"
                           }]
                       },
                       "computeProfile": {
                           "roles": [{
                               "name": "headnode",
                               "targetInstanceCount": "2",
                               "hardwareProfile": {
                                   "vmSize": "Standard_D3"
                               },
                               "osProfile": {
                                   "linuxOperatingSystemProfile": {
                                       "username": "[parameters('sshUserName')]",
                                       "password": "[parameters('sshPassword')]"
                                   }
                               }
                           },
                           {
                               "name": "workernode",
                               "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                               "hardwareProfile": {
                                   "vmSize": "Standard_D3"
                               },
                               "osProfile": {
                                   "linuxOperatingSystemProfile": {
                                       "username": "[parameters('sshUserName')]",
                                       "password": "[parameters('sshPassword')]"
                                   }
                               }
                           }]
                       }
                   }
               }],
               "outputs": {
                   "cluster": {
                       "type": "object",
                       "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                   }
               }
           },
           "mode": "incremental",
           "Parameters": {
               "location": {
                   "value": "North Europe"
               },
               "clusterName": {
                   "value": "newclustername"
               },
               "clusterType": {
                   "value": "hadoop"
               },
               "clusterStorageAccountName": {
                   "value": "newstoragename"
               },
               "clusterLoginUserName": {
                   "value": "admin"
               },
               "clusterLoginPassword": {
                   "value": "changeme"
               },
               "sshUserName": {
                   "value": "sshuser"
               },
               "sshPassword": {
                   "value": "changeme"
               }
           }
       }
   }
   ```

<span data-ttu-id="82c0f-126">This example is used in the steps in this document.</span><span class="sxs-lookup"><span data-stu-id="82c0f-126">This example is used in the steps in this document.</span></span> <span data-ttu-id="82c0f-127">Replace the example *values* in the **Parameters** section with the values for your cluster.</span><span class="sxs-lookup"><span data-stu-id="82c0f-127">Replace the example *values* in the **Parameters** section with the values for your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="82c0f-128">The template uses the default number of worker nodes (4) for an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="82c0f-128">The template uses the default number of worker nodes (4) for an HDInsight cluster.</span></span> <span data-ttu-id="82c0f-129">If you plan on more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14 GB ram.</span><span class="sxs-lookup"><span data-stu-id="82c0f-129">If you plan on more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14 GB ram.</span></span>
>
> <span data-ttu-id="82c0f-130">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="82c0f-130">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="log-in-to-your-azure-subscription"></a><span data-ttu-id="82c0f-131">Log in to your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="82c0f-131">Log in to your Azure subscription</span></span>

<span data-ttu-id="82c0f-132">Follow the steps documented in [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) and connect to your subscription using the `az login` command.</span><span class="sxs-lookup"><span data-stu-id="82c0f-132">Follow the steps documented in [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) and connect to your subscription using the `az login` command.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="82c0f-133">Create a service principal</span><span class="sxs-lookup"><span data-stu-id="82c0f-133">Create a service principal</span></span>

> [!NOTE]
> <span data-ttu-id="82c0f-134">These steps are an abridged version of the *Create service principal with password* section of the [Use Azure CLI to create a service principal to access resources](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) document.</span><span class="sxs-lookup"><span data-stu-id="82c0f-134">These steps are an abridged version of the *Create service principal with password* section of the [Use Azure CLI to create a service principal to access resources](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) document.</span></span> <span data-ttu-id="82c0f-135">These steps create a service principal that is used to authenticate to the Azure REST API.</span><span class="sxs-lookup"><span data-stu-id="82c0f-135">These steps create a service principal that is used to authenticate to the Azure REST API.</span></span>

1. <span data-ttu-id="82c0f-136">From a command line, use the following command to list your Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="82c0f-136">From a command line, use the following command to list your Azure subscriptions.</span></span>

   ```bash
   az account list --query '[].{Subscription_ID:id,Tenant_ID:tenantId,Name:name}'  --output table
   ```

    <span data-ttu-id="82c0f-137">In the list, select the subscription that you want to use and note the **Subscription_ID** and __Tenant_ID__ columns.</span><span class="sxs-lookup"><span data-stu-id="82c0f-137">In the list, select the subscription that you want to use and note the **Subscription_ID** and __Tenant_ID__ columns.</span></span> <span data-ttu-id="82c0f-138">Save these values.</span><span class="sxs-lookup"><span data-stu-id="82c0f-138">Save these values.</span></span>

2. <span data-ttu-id="82c0f-139">Use the following command to create an application in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="82c0f-139">Use the following command to create an application in Azure Active Directory.</span></span>

   ```bash
   az ad app create --display-name "exampleapp" --homepage "https://www.contoso.org" --identifier-uris "https://www.contoso.org/example" --password <Your password> --query 'appId'
   ```

    <span data-ttu-id="82c0f-140">Replace the values for the `--display-name`, `--homepage`, and `--identifier-uris` with your own values.</span><span class="sxs-lookup"><span data-stu-id="82c0f-140">Replace the values for the `--display-name`, `--homepage`, and `--identifier-uris` with your own values.</span></span> <span data-ttu-id="82c0f-141">Provide a password for the new Active Directory entry.</span><span class="sxs-lookup"><span data-stu-id="82c0f-141">Provide a password for the new Active Directory entry.</span></span>

   > [!NOTE]
   > <span data-ttu-id="82c0f-142">The `--home-page` and `--identifier-uris` values don't need to reference an actual web page hosted on the internet.</span><span class="sxs-lookup"><span data-stu-id="82c0f-142">The `--home-page` and `--identifier-uris` values don't need to reference an actual web page hosted on the internet.</span></span> <span data-ttu-id="82c0f-143">They must be unique URIs.</span><span class="sxs-lookup"><span data-stu-id="82c0f-143">They must be unique URIs.</span></span>

   <span data-ttu-id="82c0f-144">The value returned from this command is the __App ID__ for the new application.</span><span class="sxs-lookup"><span data-stu-id="82c0f-144">The value returned from this command is the __App ID__ for the new application.</span></span> <span data-ttu-id="82c0f-145">Save this value.</span><span class="sxs-lookup"><span data-stu-id="82c0f-145">Save this value.</span></span>

3. <span data-ttu-id="82c0f-146">Use the following command to create a service principal using the **App ID**.</span><span class="sxs-lookup"><span data-stu-id="82c0f-146">Use the following command to create a service principal using the **App ID**.</span></span>

   ```bash
   az ad sp create --id <App ID> --query 'objectId'
   ```

     <span data-ttu-id="82c0f-147">The value returned from this command is the __Object ID__.</span><span class="sxs-lookup"><span data-stu-id="82c0f-147">The value returned from this command is the __Object ID__.</span></span> <span data-ttu-id="82c0f-148">Save this value.</span><span class="sxs-lookup"><span data-stu-id="82c0f-148">Save this value.</span></span>

4. <span data-ttu-id="82c0f-149">Assign the **Owner** role to the service principal using the **Object ID** value.</span><span class="sxs-lookup"><span data-stu-id="82c0f-149">Assign the **Owner** role to the service principal using the **Object ID** value.</span></span> <span data-ttu-id="82c0f-150">Use the **subscription ID** you obtained earlier.</span><span class="sxs-lookup"><span data-stu-id="82c0f-150">Use the **subscription ID** you obtained earlier.</span></span>

   ```bash
   az role assignment create --assignee <Object ID> --role Owner --scope /subscriptions/<Subscription ID>/
   ```

## <a name="get-an-authentication-token"></a><span data-ttu-id="82c0f-151">Get an authentication token</span><span class="sxs-lookup"><span data-stu-id="82c0f-151">Get an authentication token</span></span>

<span data-ttu-id="82c0f-152">Use the following command to retrieve an authentication token:</span><span class="sxs-lookup"><span data-stu-id="82c0f-152">Use the following command to retrieve an authentication token:</span></span>

    curl -X "POST" "https://login.microsoftonline.com/TenantID/oauth2/token" \
    -H "Cookie: flight-uxoptin=true; stsservicecookie=ests; x-ms-gateway-slice=productionb; stsservicecookie=ests" \
    -H "Content-Type: application/x-www-form-urlencoded" \
    --data-urlencode "client_id=AppID" \
    --data-urlencode "grant_type=client_credentials" \
    --data-urlencode "client_secret=password" \
    --data-urlencode "resource=https://management.azure.com/"

    Replace **TenantID**, **AppID**, and **password** with the values obtained or used previously.

    If this request is successful, you receive a 200 series response and the response body contains a JSON document.

    The JSON document returned by this request contains an element named **access_token**. The value of **access_token** is used to authentication requests to the REST API.

   ```json
   {
       "token_type":"Bearer",
       "expires_in":"3599",
       "expires_on":"1463409994",
       "not_before":"1463406094",
       "resource":"https://management.azure.com/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWoNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuYXp1cmUuY29tLyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI2Ny8iLCJpYXQiOjE0NjM0MDYwOTQsIm5iZiI6MTQ2MzQwNjA5NCwiZXhwIjoxNDYzNDA5OTk5LCJhcHBpZCI6IjBlYzcyMzM0LTZkMDMtNDhmYi04OWU1LTU2NTJiODBiZDliYiIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0Ny8iLCJvaWQiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJzdWIiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJ0aWQiOiI3MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDciLCJ2ZXIiOiIxLjAifQ.nJVERbeDHLGHn7ZsbVGBJyHOu2PYhG5dji6F63gu8XN2Cvol3J1HO1uB4H3nCSt9DTu_jMHqAur_NNyobgNM21GojbEZAvd0I9NY0UDumBEvDZfMKneqp7a_cgAU7IYRcTPneSxbD6wo-8gIgfN9KDql98b0uEzixIVIWra2Q1bUUYETYqyaJNdS4RUmlJKNNpENllAyHQLv7hXnap1IuzP-f5CNIbbj9UgXxLiOtW5JhUAwWLZ3-WMhNRpUO2SIB7W7tQ0AbjXw3aUYr7el066J51z5tC1AK9UC-mD_fO_HUP6ZmPzu5gLA6DxkIIYP3grPnRVoUDltHQvwgONDOw"
   }
   ```

## <a name="create-a-resource-group"></a><span data-ttu-id="82c0f-153">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="82c0f-153">Create a resource group</span></span>

<span data-ttu-id="82c0f-154">Use the following to create a resource group.</span><span class="sxs-lookup"><span data-stu-id="82c0f-154">Use the following to create a resource group.</span></span>

* <span data-ttu-id="82c0f-155">Replace **SubscriptionID** with the subscription ID received while creating the service principal.</span><span class="sxs-lookup"><span data-stu-id="82c0f-155">Replace **SubscriptionID** with the subscription ID received while creating the service principal.</span></span>
* <span data-ttu-id="82c0f-156">Replace **AccessToken** with the access token received in the previous step.</span><span class="sxs-lookup"><span data-stu-id="82c0f-156">Replace **AccessToken** with the access token received in the previous step.</span></span>
* <span data-ttu-id="82c0f-157">Replace **DataCenterLocation** with the data center you wish to create the resource group, and resources, in.</span><span class="sxs-lookup"><span data-stu-id="82c0f-157">Replace **DataCenterLocation** with the data center you wish to create the resource group, and resources, in.</span></span> <span data-ttu-id="82c0f-158">For example, 'South Central US'.</span><span class="sxs-lookup"><span data-stu-id="82c0f-158">For example, 'South Central US'.</span></span>
* <span data-ttu-id="82c0f-159">Replace **ResourceGroupName** with the name you wish to use for this group:</span><span class="sxs-lookup"><span data-stu-id="82c0f-159">Replace **ResourceGroupName** with the name you wish to use for this group:</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/SubscriptionID/resourcegroups/ResourceGroupName?api-version=2015-01-01" \
    -H "Authorization: Bearer AccessToken" \
    -H "Content-Type: application/json" \
    -d $'{
"location": "DataCenterLocation"
}'
```

<span data-ttu-id="82c0f-160">If this request is successful, you receive a 200 series response and the response body contains a JSON document containing information about the group.</span><span class="sxs-lookup"><span data-stu-id="82c0f-160">If this request is successful, you receive a 200 series response and the response body contains a JSON document containing information about the group.</span></span> <span data-ttu-id="82c0f-161">The `"provisioningState"` element contains a value of `"Succeeded"`.</span><span class="sxs-lookup"><span data-stu-id="82c0f-161">The `"provisioningState"` element contains a value of `"Succeeded"`.</span></span>

## <a name="create-a-deployment"></a><span data-ttu-id="82c0f-162">Create a deployment</span><span class="sxs-lookup"><span data-stu-id="82c0f-162">Create a deployment</span></span>

<span data-ttu-id="82c0f-163">Use the following command to deploy the template to the resource group.</span><span class="sxs-lookup"><span data-stu-id="82c0f-163">Use the following command to deploy the template to the resource group.</span></span>

* <span data-ttu-id="82c0f-164">Replace **SubscriptionID** and **AccessToken** with the values used previously.</span><span class="sxs-lookup"><span data-stu-id="82c0f-164">Replace **SubscriptionID** and **AccessToken** with the values used previously.</span></span>
* <span data-ttu-id="82c0f-165">Replace **ResourceGroupName** with the resource group name you created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="82c0f-165">Replace **ResourceGroupName** with the resource group name you created in the previous section.</span></span>
* <span data-ttu-id="82c0f-166">Replace **DeploymentName** with the name you wish to use for this deployment.</span><span class="sxs-lookup"><span data-stu-id="82c0f-166">Replace **DeploymentName** with the name you wish to use for this deployment.</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/SubscriptionID/resourcegroups/ResourceGroupName/providers/microsoft.resources/deployments/DeploymentName?api-version=2015-01-01" \
-H "Authorization: Bearer AccessToken" \
-H "Content-Type: application/json" \
-d "{set your body string to the template and parameters}"
```

> [!NOTE]
> <span data-ttu-id="82c0f-167">If you saved the teplate to a file, you can use the following command instead of `-d "{ template and parameters}"`:</span><span class="sxs-lookup"><span data-stu-id="82c0f-167">If you saved the teplate to a file, you can use the following command instead of `-d "{ template and parameters}"`:</span></span>
>
> `--data-binary "@/path/to/file.json"`

<span data-ttu-id="82c0f-168">If this request is successful, you receive a 200 series response and the response body contains a JSON document containing information about the deployment operation.</span><span class="sxs-lookup"><span data-stu-id="82c0f-168">If this request is successful, you receive a 200 series response and the response body contains a JSON document containing information about the deployment operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="82c0f-169">The deployment has been submitted, but has not completed at this time.</span><span class="sxs-lookup"><span data-stu-id="82c0f-169">The deployment has been submitted, but has not completed at this time.</span></span> <span data-ttu-id="82c0f-170">It can take several minutes, usually around 15, for the deployment to complete.</span><span class="sxs-lookup"><span data-stu-id="82c0f-170">It can take several minutes, usually around 15, for the deployment to complete.</span></span>

## <a name="check-the-status-of-a-deployment"></a><span data-ttu-id="82c0f-171">Check the status of a deployment</span><span class="sxs-lookup"><span data-stu-id="82c0f-171">Check the status of a deployment</span></span>

<span data-ttu-id="82c0f-172">To check the status of the deployment, use the following command:</span><span class="sxs-lookup"><span data-stu-id="82c0f-172">To check the status of the deployment, use the following command:</span></span>

* <span data-ttu-id="82c0f-173">Replace **SubscriptionID** and **AccessToken** with the values used previously.</span><span class="sxs-lookup"><span data-stu-id="82c0f-173">Replace **SubscriptionID** and **AccessToken** with the values used previously.</span></span>
* <span data-ttu-id="82c0f-174">Replace **ResourceGroupName** with the resource group name you created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="82c0f-174">Replace **ResourceGroupName** with the resource group name you created in the previous section.</span></span>

```bash
curl -X "GET" "https://management.azure.com/subscriptions/SubscriptionID/resourcegroups/ResourceGroupName/providers/microsoft.resources/deployments/DeploymentName?api-version=2015-01-01" \
-H "Authorization: Bearer AccessToken" \
-H "Content-Type: application/json"
```

<span data-ttu-id="82c0f-175">This command returns a JSON document containing information about the deployment operation.</span><span class="sxs-lookup"><span data-stu-id="82c0f-175">This command returns a JSON document containing information about the deployment operation.</span></span> <span data-ttu-id="82c0f-176">The `"provisioningState"` element contains the status of the deployment.</span><span class="sxs-lookup"><span data-stu-id="82c0f-176">The `"provisioningState"` element contains the status of the deployment.</span></span> <span data-ttu-id="82c0f-177">If this contains a value of `"Succeeded"`, then the deployment has completed successfully.</span><span class="sxs-lookup"><span data-stu-id="82c0f-177">If this contains a value of `"Succeeded"`, then the deployment has completed successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82c0f-178">Next steps</span><span class="sxs-lookup"><span data-stu-id="82c0f-178">Next steps</span></span>

<span data-ttu-id="82c0f-179">Now that you have successfully created an HDInsight cluster, use the following to learn how to work with your cluster.</span><span class="sxs-lookup"><span data-stu-id="82c0f-179">Now that you have successfully created an HDInsight cluster, use the following to learn how to work with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="82c0f-180">Hadoop clusters</span><span class="sxs-lookup"><span data-stu-id="82c0f-180">Hadoop clusters</span></span>

* [<span data-ttu-id="82c0f-181">Use Hive with HDInsight</span><span class="sxs-lookup"><span data-stu-id="82c0f-181">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="82c0f-182">Use Pig with HDInsight</span><span class="sxs-lookup"><span data-stu-id="82c0f-182">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="82c0f-183">Use MapReduce with HDInsight</span><span class="sxs-lookup"><span data-stu-id="82c0f-183">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="82c0f-184">HBase clusters</span><span class="sxs-lookup"><span data-stu-id="82c0f-184">HBase clusters</span></span>

* [<span data-ttu-id="82c0f-185">Get started with HBase on HDInsight</span><span class="sxs-lookup"><span data-stu-id="82c0f-185">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="82c0f-186">Develop Java applications for HBase on HDInsight</span><span class="sxs-lookup"><span data-stu-id="82c0f-186">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="82c0f-187">Storm clusters</span><span class="sxs-lookup"><span data-stu-id="82c0f-187">Storm clusters</span></span>

* [<span data-ttu-id="82c0f-188">Develop Java topologies for Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="82c0f-188">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="82c0f-189">Use Python components in Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="82c0f-189">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="82c0f-190">Deploy and monitor topologies with Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="82c0f-190">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
