---
title: How to manage secrets when working with an Azure Dev Space | Microsoft Docs
titleSuffix: Azure Dev Spaces
services: azure-dev-spaces
ms.service: azure-dev-spaces
ms.component: azds-kubernetes
author: ghogen
ms.author: ghogen
ms.date: 05/11/2018
ms.topic: article
ms.technology: azds-kubernetes
description: Rapid Kubernetes development with containers and microservices on Azure
keywords: Docker, Kubernetes, Azure, AKS, Azure Container Service, containers
manager: douge
ms.openlocfilehash: 352e43633ea1464eb7e28fa698d1ae77d5ac52bd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864663"
---
# <a name="how-to-manage-secrets-when-working-with-an-azure-dev-space"></a><span data-ttu-id="a7fec-104">How to manage secrets when working with an Azure Dev Space</span><span class="sxs-lookup"><span data-stu-id="a7fec-104">How to manage secrets when working with an Azure Dev Space</span></span>

<span data-ttu-id="a7fec-105">Your services might require certain passwords, connection strings, and other secrets, such as for databases or other secure Azure services.</span><span class="sxs-lookup"><span data-stu-id="a7fec-105">Your services might require certain passwords, connection strings, and other secrets, such as for databases or other secure Azure services.</span></span> <span data-ttu-id="a7fec-106">By setting the values of these secrets in configuration files, you can make them available in your code as environment variables.</span><span class="sxs-lookup"><span data-stu-id="a7fec-106">By setting the values of these secrets in configuration files, you can make them available in your code as environment variables.</span></span>  <span data-ttu-id="a7fec-107">These must be handled with care to avoid compromising the security of the secrets.</span><span class="sxs-lookup"><span data-stu-id="a7fec-107">These must be handled with care to avoid compromising the security of the secrets.</span></span>

<span data-ttu-id="a7fec-108">Azure Dev Spaces provides two recommended options for storing secrets: in the values.dev.yaml file, and inline directly in azds.yaml.</span><span class="sxs-lookup"><span data-stu-id="a7fec-108">Azure Dev Spaces provides two recommended options for storing secrets: in the values.dev.yaml file, and inline directly in azds.yaml.</span></span> <span data-ttu-id="a7fec-109">It's not recommended to store secrets in values.yaml.</span><span class="sxs-lookup"><span data-stu-id="a7fec-109">It's not recommended to store secrets in values.yaml.</span></span>
 
## <a name="method-1-valuesdevyaml"></a><span data-ttu-id="a7fec-110">Method 1: values.dev.yaml</span><span class="sxs-lookup"><span data-stu-id="a7fec-110">Method 1: values.dev.yaml</span></span>
1. <span data-ttu-id="a7fec-111">Open VS Code with your project that is enabled for Azure Dev Spaces.</span><span class="sxs-lookup"><span data-stu-id="a7fec-111">Open VS Code with your project that is enabled for Azure Dev Spaces.</span></span>
2. <span data-ttu-id="a7fec-112">Add a file named _values.dev.yaml_ in the same folder as existing _values.yaml_ and define your secret key and values, as in the following example:</span><span class="sxs-lookup"><span data-stu-id="a7fec-112">Add a file named _values.dev.yaml_ in the same folder as existing _values.yaml_ and define your secret key and values, as in the following example:</span></span>

    ```yaml
    secrets:
      redis:
        port: "6380"
        host: "contosodevredis.redis.cache.windows.net"
        key: "secretkeyhere"
    ```
     
3. <span data-ttu-id="a7fec-113">Update _azds.yaml_ to tell Azure Dev Spaces to use your new _values.dev.yaml_ file.</span><span class="sxs-lookup"><span data-stu-id="a7fec-113">Update _azds.yaml_ to tell Azure Dev Spaces to use your new _values.dev.yaml_ file.</span></span> <span data-ttu-id="a7fec-114">To do this, add this configuration under the configurations.develop.container section:</span><span class="sxs-lookup"><span data-stu-id="a7fec-114">To do this, add this configuration under the configurations.develop.container section:</span></span>

    ```yaml
           container:
             values:
             - "charts/webfrontend/values.dev.yaml"
    ```
 
4. <span data-ttu-id="a7fec-115">Modify your service code to refer to these secrets as environment variables, as in the following example:</span><span class="sxs-lookup"><span data-stu-id="a7fec-115">Modify your service code to refer to these secrets as environment variables, as in the following example:</span></span>

    ```
    var redisPort = process.env.REDIS_PORT
    var host = process.env.REDIS_HOST
    var theKey = process.env.REDIS_KEY
    ```
    
5. <span data-ttu-id="a7fec-116">Update the services running in your cluster with these changes.</span><span class="sxs-lookup"><span data-stu-id="a7fec-116">Update the services running in your cluster with these changes.</span></span> <span data-ttu-id="a7fec-117">On the command line, run the command:</span><span class="sxs-lookup"><span data-stu-id="a7fec-117">On the command line, run the command:</span></span>

    ```
    azds up
    ```
 
6. <span data-ttu-id="a7fec-118">(Optional) From the command line, check that these secrets have been created:</span><span class="sxs-lookup"><span data-stu-id="a7fec-118">(Optional) From the command line, check that these secrets have been created:</span></span>

      ```
      kubectl get secret --namespace default -o yaml 
      ```

7. <span data-ttu-id="a7fec-119">Make sure that you add _values.dev.yaml_ to the _.gitignore_ file to avoid committing secrets in source control.</span><span class="sxs-lookup"><span data-stu-id="a7fec-119">Make sure that you add _values.dev.yaml_ to the _.gitignore_ file to avoid committing secrets in source control.</span></span>
 
 
## <a name="method-2-inline-directly-in-azdsyaml"></a><span data-ttu-id="a7fec-120">Method 2: Inline directly in azds.yaml</span><span class="sxs-lookup"><span data-stu-id="a7fec-120">Method 2: Inline directly in azds.yaml</span></span>
1.  <span data-ttu-id="a7fec-121">In _azds.yaml_, set secrets under the yaml section configurations/develop/install.</span><span class="sxs-lookup"><span data-stu-id="a7fec-121">In _azds.yaml_, set secrets under the yaml section configurations/develop/install.</span></span> <span data-ttu-id="a7fec-122">Although you can enter secret values directly there, it's not recommended because _azds.yaml_ is checked into source control.</span><span class="sxs-lookup"><span data-stu-id="a7fec-122">Although you can enter secret values directly there, it's not recommended because _azds.yaml_ is checked into source control.</span></span> <span data-ttu-id="a7fec-123">Instead, add placeholders using the "$PLACEHOLDER" syntax.</span><span class="sxs-lookup"><span data-stu-id="a7fec-123">Instead, add placeholders using the "$PLACEHOLDER" syntax.</span></span>

    ```yaml
    configurations:
      develop:
        ...
        install:
          set:
            secrets:
              redis:
                port: "$REDIS_PORT_DEV"
                host: "$REDIS_HOST_DEV"
                key: "$REDIS_KEY_DEV"
    ```
     
2.  <span data-ttu-id="a7fec-124">Create a _.env_ file in the same folder as _azds.yaml_.</span><span class="sxs-lookup"><span data-stu-id="a7fec-124">Create a _.env_ file in the same folder as _azds.yaml_.</span></span> <span data-ttu-id="a7fec-125">Enter secrets using standard key=value notation.</span><span class="sxs-lookup"><span data-stu-id="a7fec-125">Enter secrets using standard key=value notation.</span></span> <span data-ttu-id="a7fec-126">Don’t commit the _.env_ file to source control.</span><span class="sxs-lookup"><span data-stu-id="a7fec-126">Don’t commit the _.env_ file to source control.</span></span> <span data-ttu-id="a7fec-127">(To omit from source control in git-based version control systems, add it to the _.gitignore_ file.) The following example shows an _.env_ file:</span><span class="sxs-lookup"><span data-stu-id="a7fec-127">(To omit from source control in git-based version control systems, add it to the _.gitignore_ file.) The following example shows an _.env_ file:</span></span>

    ```
    REDIS_PORT_DEV=3333
    REDIS_HOST_DEV=myredishost
    REDIS_KEY_DEV=myrediskey
    ```
2.  <span data-ttu-id="a7fec-128">Modify your service source code to reference these secrets in code, as in the following example:</span><span class="sxs-lookup"><span data-stu-id="a7fec-128">Modify your service source code to reference these secrets in code, as in the following example:</span></span>

    ```
    var redisPort = process.env.REDIS_PORT
    var host = process.env.REDIS_HOST
    var theKey = process.env.REDIS_KEY
    ```
 
3.  <span data-ttu-id="a7fec-129">Update the services running in your cluster with these changes.</span><span class="sxs-lookup"><span data-stu-id="a7fec-129">Update the services running in your cluster with these changes.</span></span> <span data-ttu-id="a7fec-130">On the command line, run the command:</span><span class="sxs-lookup"><span data-stu-id="a7fec-130">On the command line, run the command:</span></span>

    ```
    azds up
    ```

4.  <span data-ttu-id="a7fec-131">(optional) View secrets from kubectl:</span><span class="sxs-lookup"><span data-stu-id="a7fec-131">(optional) View secrets from kubectl:</span></span>

    ```
    kubectl get secret --namespace default -o yaml
    ```

## <a name="next-steps"></a><span data-ttu-id="a7fec-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="a7fec-132">Next steps</span></span>

<span data-ttu-id="a7fec-133">With these methods, you can now securely connect to a database, a Redis cache, or access secure Azure services.</span><span class="sxs-lookup"><span data-stu-id="a7fec-133">With these methods, you can now securely connect to a database, a Redis cache, or access secure Azure services.</span></span>
 