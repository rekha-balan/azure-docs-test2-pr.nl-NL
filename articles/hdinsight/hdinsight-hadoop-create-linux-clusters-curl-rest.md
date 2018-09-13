---
title: Create Hadoop clusters using Azure REST API - Azure
description: Learn how to create HDInsight clusters by submitting Azure Resource Manager templates to the Azure REST API.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 05/02/2018
ms.author: jasonh
ms.openlocfilehash: 32c9edcbbe7a5b319240f1e8af3b9d399b493d6b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44775001"
---
# <a name="create-hadoop-clusters-using-the-azure-rest-api"></a><span data-ttu-id="68998-103">Create Hadoop clusters using the Azure REST API</span><span class="sxs-lookup"><span data-stu-id="68998-103">Create Hadoop clusters using the Azure REST API</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="68998-104">Learn how to create an HDInsight cluster using an Azure Resource Manager template and the Azure REST API.</span><span class="sxs-lookup"><span data-stu-id="68998-104">Learn how to create an HDInsight cluster using an Azure Resource Manager template and the Azure REST API.</span></span>

<span data-ttu-id="68998-105">The Azure REST API allows you to perform management operations on services hosted in the Azure platform, including the creation of new resources such as HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="68998-105">The Azure REST API allows you to perform management operations on services hosted in the Azure platform, including the creation of new resources such as HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="68998-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="68998-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="68998-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="68998-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!NOTE]
> <span data-ttu-id="68998-108">The steps in this document use the [curl (https://curl.haxx.se/)](https://curl.haxx.se/) utility to communicate with the Azure REST API.</span><span class="sxs-lookup"><span data-stu-id="68998-108">The steps in this document use the [curl (https://curl.haxx.se/)](https://curl.haxx.se/) utility to communicate with the Azure REST API.</span></span>

## <a name="create-a-template"></a><span data-ttu-id="68998-109">Create a template</span><span class="sxs-lookup"><span data-stu-id="68998-109">Create a template</span></span>

<span data-ttu-id="68998-110">Azure Resource Manager templates are JSON documents that describe a **resource group** and all resources in it (such as HDInsight.) This template-based approach allows you to define the resources that you need for HDInsight in one template.</span><span class="sxs-lookup"><span data-stu-id="68998-110">Azure Resource Manager templates are JSON documents that describe a **resource group** and all resources in it (such as HDInsight.) This template-based approach allows you to define the resources that you need for HDInsight in one template.</span></span>

<span data-ttu-id="68998-111">The following JSON document is a merger of the template and parameters files from [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), which creates a Linux-based cluster using a password to secure the SSH user account.</span><span class="sxs-lookup"><span data-stu-id="68998-111">The following JSON document is a merger of the template and parameters files from [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), which creates a Linux-based cluster using a password to secure the SSH user account.</span></span>

   ```json
   {
       "properties": {
           "template": {
               "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
               "contentVersion": "1.0.0.0",
               "parameters": {
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
                   "location": "[resourceGroup().location]",
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
                   "location": "[resourceGroup().location]",
                   "apiVersion": "[variables('clusterApiVersion')]",
                   "dependsOn": ["[concat('Microsoft.Storage/storageAccounts/',parameters('clusterStorageAccountName'))]"],
                   "tags": {

                   },
                   "properties": {
                       "clusterVersion": "3.6",
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

<span data-ttu-id="68998-112">This example is used in the steps in this document.</span><span class="sxs-lookup"><span data-stu-id="68998-112">This example is used in the steps in this document.</span></span> <span data-ttu-id="68998-113">Replace the example *values* in the **Parameters** section with the values for your cluster.</span><span class="sxs-lookup"><span data-stu-id="68998-113">Replace the example *values* in the **Parameters** section with the values for your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="68998-114">The template uses the default number of worker nodes (4) for an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="68998-114">The template uses the default number of worker nodes (4) for an HDInsight cluster.</span></span> <span data-ttu-id="68998-115">If you plan on more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14-GB ram.</span><span class="sxs-lookup"><span data-stu-id="68998-115">If you plan on more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14-GB ram.</span></span>
>
> <span data-ttu-id="68998-116">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="68998-116">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="log-in-to-your-azure-subscription"></a><span data-ttu-id="68998-117">Log in to your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="68998-117">Log in to your Azure subscription</span></span>

<span data-ttu-id="68998-118">Follow the steps documented in [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) and connect to your subscription using the `az login` command.</span><span class="sxs-lookup"><span data-stu-id="68998-118">Follow the steps documented in [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) and connect to your subscription using the `az login` command.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="68998-119">Create a service principal</span><span class="sxs-lookup"><span data-stu-id="68998-119">Create a service principal</span></span>

> [!NOTE]
> <span data-ttu-id="68998-120">These steps are an abridged version of the *Create service principal with password* section of the [Use Azure CLI to create a service principal to access resources](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md) document.</span><span class="sxs-lookup"><span data-stu-id="68998-120">These steps are an abridged version of the *Create service principal with password* section of the [Use Azure CLI to create a service principal to access resources](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md) document.</span></span> <span data-ttu-id="68998-121">These steps create a service principal that is used to authenticate to the Azure REST API.</span><span class="sxs-lookup"><span data-stu-id="68998-121">These steps create a service principal that is used to authenticate to the Azure REST API.</span></span>

1. <span data-ttu-id="68998-122">From a command line, use the following command to list your Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="68998-122">From a command line, use the following command to list your Azure subscriptions.</span></span>

   ```bash
   az account list --query '[].{Subscription_ID:id,Tenant_ID:tenantId,Name:name}'  --output table
   ```

    <span data-ttu-id="68998-123">In the list, select the subscription that you want to use and note the **Subscription_ID** and __Tenant_ID__ columns.</span><span class="sxs-lookup"><span data-stu-id="68998-123">In the list, select the subscription that you want to use and note the **Subscription_ID** and __Tenant_ID__ columns.</span></span> <span data-ttu-id="68998-124">Save these values.</span><span class="sxs-lookup"><span data-stu-id="68998-124">Save these values.</span></span>

2. <span data-ttu-id="68998-125">Use the following command to create an application in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="68998-125">Use the following command to create an application in Azure Active Directory.</span></span>

   ```bash
   az ad app create --display-name "exampleapp" --homepage "https://www.contoso.org" --identifier-uris "https://www.contoso.org/example" --password <Your password> --query 'appId'
   ```

    <span data-ttu-id="68998-126">Replace the values for the `--display-name`, `--homepage`, and `--identifier-uris` with your own values.</span><span class="sxs-lookup"><span data-stu-id="68998-126">Replace the values for the `--display-name`, `--homepage`, and `--identifier-uris` with your own values.</span></span> <span data-ttu-id="68998-127">Provide a password for the new Active Directory entry.</span><span class="sxs-lookup"><span data-stu-id="68998-127">Provide a password for the new Active Directory entry.</span></span>

   > [!NOTE]
   > <span data-ttu-id="68998-128">The `--home-page` and `--identifier-uris` values don't need to reference an actual web page hosted on the internet.</span><span class="sxs-lookup"><span data-stu-id="68998-128">The `--home-page` and `--identifier-uris` values don't need to reference an actual web page hosted on the internet.</span></span> <span data-ttu-id="68998-129">They must be unique URIs.</span><span class="sxs-lookup"><span data-stu-id="68998-129">They must be unique URIs.</span></span>

   <span data-ttu-id="68998-130">The value returned from this command is the __App ID__ for the new application.</span><span class="sxs-lookup"><span data-stu-id="68998-130">The value returned from this command is the __App ID__ for the new application.</span></span> <span data-ttu-id="68998-131">Save this value.</span><span class="sxs-lookup"><span data-stu-id="68998-131">Save this value.</span></span>

3. <span data-ttu-id="68998-132">Use the following command to create a service principal using the **App ID**.</span><span class="sxs-lookup"><span data-stu-id="68998-132">Use the following command to create a service principal using the **App ID**.</span></span>

   ```bash
   az ad sp create --id <App ID> --query 'objectId'
   ```

     <span data-ttu-id="68998-133">The value returned from this command is the __Object ID__.</span><span class="sxs-lookup"><span data-stu-id="68998-133">The value returned from this command is the __Object ID__.</span></span> <span data-ttu-id="68998-134">Save this value.</span><span class="sxs-lookup"><span data-stu-id="68998-134">Save this value.</span></span>

4. <span data-ttu-id="68998-135">Assign the **Owner** role to the service principal using the **Object ID** value.</span><span class="sxs-lookup"><span data-stu-id="68998-135">Assign the **Owner** role to the service principal using the **Object ID** value.</span></span> <span data-ttu-id="68998-136">Use the **subscription ID** you obtained earlier.</span><span class="sxs-lookup"><span data-stu-id="68998-136">Use the **subscription ID** you obtained earlier.</span></span>

   ```bash
   az role assignment create --assignee <Object ID> --role Owner --scope /subscriptions/<Subscription ID>/
   ```

## <a name="get-an-authentication-token"></a><span data-ttu-id="68998-137">Get an authentication token</span><span class="sxs-lookup"><span data-stu-id="68998-137">Get an authentication token</span></span>

<span data-ttu-id="68998-138">Use the following command to retrieve an authentication token:</span><span class="sxs-lookup"><span data-stu-id="68998-138">Use the following command to retrieve an authentication token:</span></span>

```bash
curl -X "POST" "https://login.microsoftonline.com/$TENANTID/oauth2/token" \
-H "Cookie: flight-uxoptin=true; stsservicecookie=ests; x-ms-gateway-slice=productionb; stsservicecookie=ests" \
-H "Content-Type: application/x-www-form-urlencoded" \
--data-urlencode "client_id=$APPID" \
--data-urlencode "grant_type=client_credentials" \
--data-urlencode "client_secret=$PASSWORD" \
--data-urlencode "resource=https://management.azure.com/"
```

<span data-ttu-id="68998-139">Set `$TENANTID`, `$APPID`, and `$PASSWORD` to the values obtained or used previously.</span><span class="sxs-lookup"><span data-stu-id="68998-139">Set `$TENANTID`, `$APPID`, and `$PASSWORD` to the values obtained or used previously.</span></span>

<span data-ttu-id="68998-140">If this request is successful, you receive a 200 series response and the response body contains a JSON document.</span><span class="sxs-lookup"><span data-stu-id="68998-140">If this request is successful, you receive a 200 series response and the response body contains a JSON document.</span></span>

<span data-ttu-id="68998-141">The JSON document returned by this request contains an element named **access_token**.</span><span class="sxs-lookup"><span data-stu-id="68998-141">The JSON document returned by this request contains an element named **access_token**.</span></span> <span data-ttu-id="68998-142">The value of **access_token** is used to authentication requests to the REST API.</span><span class="sxs-lookup"><span data-stu-id="68998-142">The value of **access_token** is used to authentication requests to the REST API.</span></span>

```json
{
    "token_type":"Bearer",
    "expires_in":"3599",
    "expires_on":"1463409994",
    "not_before":"1463406094",
    "resource":"https://management.azure.com/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWoNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuYXp1cmUuY29tLyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI2Ny8iLCJpYXQiOjE0NjM0MDYwOTQsIm5iZiI6MTQ2MzQwNjA5NCwiZXhwIjoxNDYzNDA5OTk5LCJhcHBpZCI6IjBlYzcyMzM0LTZkMDMtNDhmYi04OWU1LTU2NTJiODBiZDliYiIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0Ny8iLCJvaWQiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJzdWIiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJ0aWQiOiI3MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDciLCJ2ZXIiOiIxLjAifQ.nJVERbeDHLGHn7ZsbVGBJyHOu2PYhG5dji6F63gu8XN2Cvol3J1HO1uB4H3nCSt9DTu_jMHqAur_NNyobgNM21GojbEZAvd0I9NY0UDumBEvDZfMKneqp7a_cgAU7IYRcTPneSxbD6wo-8gIgfN9KDql98b0uEzixIVIWra2Q1bUUYETYqyaJNdS4RUmlJKNNpENllAyHQLv7hXnap1IuzP-f5CNIbbj9UgXxLiOtW5JhUAwWLZ3-WMhNRpUO2SIB7W7tQ0AbjXw3aUYr7el066J51z5tC1AK9UC-mD_fO_HUP6ZmPzu5gLA6DxkIIYP3grPnRVoUDltHQvwgONDOw"
}
```

## <a name="create-a-resource-group"></a><span data-ttu-id="68998-143">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="68998-143">Create a resource group</span></span>

<span data-ttu-id="68998-144">Use the following to create a resource group.</span><span class="sxs-lookup"><span data-stu-id="68998-144">Use the following to create a resource group.</span></span>

* <span data-ttu-id="68998-145">Set `$SUBSCRIPTIONID` to the subscription ID received while creating the service principal.</span><span class="sxs-lookup"><span data-stu-id="68998-145">Set `$SUBSCRIPTIONID` to the subscription ID received while creating the service principal.</span></span>
* <span data-ttu-id="68998-146">Set `$ACCESSTOKEN` to the access token received in the previous step.</span><span class="sxs-lookup"><span data-stu-id="68998-146">Set `$ACCESSTOKEN` to the access token received in the previous step.</span></span>
* <span data-ttu-id="68998-147">Replace `DATACENTERLOCATION` with the data center you wish to create the resource group, and resources, in.</span><span class="sxs-lookup"><span data-stu-id="68998-147">Replace `DATACENTERLOCATION` with the data center you wish to create the resource group, and resources, in.</span></span> <span data-ttu-id="68998-148">For example, 'South Central US'.</span><span class="sxs-lookup"><span data-stu-id="68998-148">For example, 'South Central US'.</span></span>
* <span data-ttu-id="68998-149">Set `$RESOURCEGROUPNAME` to the name you wish to use for this group:</span><span class="sxs-lookup"><span data-stu-id="68998-149">Set `$RESOURCEGROUPNAME` to the name you wish to use for this group:</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME?api-version=2015-01-01" \
    -H "Authorization: Bearer $ACCESSTOKEN" \
    -H "Content-Type: application/json" \
    -d $'{
"location": "DATACENTERLOCATION"
}'
```

<span data-ttu-id="68998-150">If this request is successful, you receive a 200 series response and the response body contains a JSON document containing information about the group.</span><span class="sxs-lookup"><span data-stu-id="68998-150">If this request is successful, you receive a 200 series response and the response body contains a JSON document containing information about the group.</span></span> <span data-ttu-id="68998-151">The `"provisioningState"` element contains a value of `"Succeeded"`.</span><span class="sxs-lookup"><span data-stu-id="68998-151">The `"provisioningState"` element contains a value of `"Succeeded"`.</span></span>

## <a name="create-a-deployment"></a><span data-ttu-id="68998-152">Create a deployment</span><span class="sxs-lookup"><span data-stu-id="68998-152">Create a deployment</span></span>

<span data-ttu-id="68998-153">Use the following command to deploy the template to the resource group.</span><span class="sxs-lookup"><span data-stu-id="68998-153">Use the following command to deploy the template to the resource group.</span></span>

* <span data-ttu-id="68998-154">Set `$DEPLOYMENTNAME` to the name you wish to use for this deployment.</span><span class="sxs-lookup"><span data-stu-id="68998-154">Set `$DEPLOYMENTNAME` to the name you wish to use for this deployment.</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json" \
-d "{set your body string to the template and parameters}"
```

> [!NOTE]
> <span data-ttu-id="68998-155">If you saved the template to a file, you can use the following command instead of `-d "{ template and parameters}"`:</span><span class="sxs-lookup"><span data-stu-id="68998-155">If you saved the template to a file, you can use the following command instead of `-d "{ template and parameters}"`:</span></span>
>
> `--data-binary "@/path/to/file.json"`

<span data-ttu-id="68998-156">If this request is successful, you receive a 200 series response and the response body contains a JSON document containing information about the deployment operation.</span><span class="sxs-lookup"><span data-stu-id="68998-156">If this request is successful, you receive a 200 series response and the response body contains a JSON document containing information about the deployment operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="68998-157">The deployment has been submitted, but has not completed.</span><span class="sxs-lookup"><span data-stu-id="68998-157">The deployment has been submitted, but has not completed.</span></span> <span data-ttu-id="68998-158">It can take several minutes, usually around 15, for the deployment to complete.</span><span class="sxs-lookup"><span data-stu-id="68998-158">It can take several minutes, usually around 15, for the deployment to complete.</span></span>

## <a name="check-the-status-of-a-deployment"></a><span data-ttu-id="68998-159">Check the status of a deployment</span><span class="sxs-lookup"><span data-stu-id="68998-159">Check the status of a deployment</span></span>

<span data-ttu-id="68998-160">To check the status of the deployment, use the following command:</span><span class="sxs-lookup"><span data-stu-id="68998-160">To check the status of the deployment, use the following command:</span></span>

```bash
curl -X "GET" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json"
```

<span data-ttu-id="68998-161">This command returns a JSON document containing information about the deployment operation.</span><span class="sxs-lookup"><span data-stu-id="68998-161">This command returns a JSON document containing information about the deployment operation.</span></span> <span data-ttu-id="68998-162">The `"provisioningState"` element contains the status of the deployment.</span><span class="sxs-lookup"><span data-stu-id="68998-162">The `"provisioningState"` element contains the status of the deployment.</span></span> <span data-ttu-id="68998-163">If this element contains a value of `"Succeeded"`, then the deployment has completed successfully.</span><span class="sxs-lookup"><span data-stu-id="68998-163">If this element contains a value of `"Succeeded"`, then the deployment has completed successfully.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="68998-164">Troubleshoot</span><span class="sxs-lookup"><span data-stu-id="68998-164">Troubleshoot</span></span>

<span data-ttu-id="68998-165">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="68998-165">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="68998-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="68998-166">Next steps</span></span>

<span data-ttu-id="68998-167">Now that you have successfully created an HDInsight cluster, use the following to learn how to work with your cluster.</span><span class="sxs-lookup"><span data-stu-id="68998-167">Now that you have successfully created an HDInsight cluster, use the following to learn how to work with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="68998-168">Hadoop clusters</span><span class="sxs-lookup"><span data-stu-id="68998-168">Hadoop clusters</span></span>

* [<span data-ttu-id="68998-169">Use Hive with HDInsight</span><span class="sxs-lookup"><span data-stu-id="68998-169">Use Hive with HDInsight</span></span>](hadoop/hdinsight-use-hive.md)
* [<span data-ttu-id="68998-170">Use Pig with HDInsight</span><span class="sxs-lookup"><span data-stu-id="68998-170">Use Pig with HDInsight</span></span>](hadoop/hdinsight-use-pig.md)
* [<span data-ttu-id="68998-171">Use MapReduce with HDInsight</span><span class="sxs-lookup"><span data-stu-id="68998-171">Use MapReduce with HDInsight</span></span>](hadoop/hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="68998-172">HBase clusters</span><span class="sxs-lookup"><span data-stu-id="68998-172">HBase clusters</span></span>

* [<span data-ttu-id="68998-173">Get started with HBase on HDInsight</span><span class="sxs-lookup"><span data-stu-id="68998-173">Get started with HBase on HDInsight</span></span>](hbase/apache-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="68998-174">Develop Java applications for HBase on HDInsight</span><span class="sxs-lookup"><span data-stu-id="68998-174">Develop Java applications for HBase on HDInsight</span></span>](hbase/apache-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="68998-175">Storm clusters</span><span class="sxs-lookup"><span data-stu-id="68998-175">Storm clusters</span></span>

* [<span data-ttu-id="68998-176">Develop Java topologies for Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="68998-176">Develop Java topologies for Storm on HDInsight</span></span>](storm/apache-storm-develop-java-topology.md)
* [<span data-ttu-id="68998-177">Use Python components in Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="68998-177">Use Python components in Storm on HDInsight</span></span>](storm/apache-storm-develop-python-topology.md)
* [<span data-ttu-id="68998-178">Deploy and monitor topologies with Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="68998-178">Deploy and monitor topologies with Storm on HDInsight</span></span>](storm/apache-storm-deploy-monitor-topology-linux.md)
