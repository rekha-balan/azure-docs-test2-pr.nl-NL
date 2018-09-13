---
title: Create an IoT Hub using Azure CLI | Microsoft Docs
description: How to create an Azure IoT hub using Azure CLI.
author: robinsh
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.date: 08/23/2018
ms.author: robinsh
ms.openlocfilehash: 95741b1a00c47468c7189e0103608c1dd7fa1d90
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44811316"
---
# <a name="create-an-iot-hub-using-azure-cli"></a><span data-ttu-id="4edf1-103">Create an IoT hub using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4edf1-103">Create an IoT hub using Azure CLI</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="4edf1-104">This article shows you how to create an IoT hub using Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="4edf1-104">This article shows you how to create an IoT hub using Azure CLI.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4edf1-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4edf1-105">Prerequisites</span></span>

<span data-ttu-id="4edf1-106">To complete this how-to, you need an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="4edf1-106">To complete this how-to, you need an Azure subscription.</span></span> <span data-ttu-id="4edf1-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="4edf1-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="4edf1-108">Sign in and set your Azure account</span><span class="sxs-lookup"><span data-stu-id="4edf1-108">Sign in and set your Azure account</span></span>

<span data-ttu-id="4edf1-109">If you are running Azure CLI locally instead of using Cloud Shell, you need to sign in to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="4edf1-109">If you are running Azure CLI locally instead of using Cloud Shell, you need to sign in to your Azure account.</span></span>

<span data-ttu-id="4edf1-110">At the command prompt, run the [login command](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli):</span><span class="sxs-lookup"><span data-stu-id="4edf1-110">At the command prompt, run the [login command](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli):</span></span>

    ```azurecli
    az login
    ```

<span data-ttu-id="4edf1-111">Follow the instructions to authenticate using the code and sign in to your Azure account through a web browser.</span><span class="sxs-lookup"><span data-stu-id="4edf1-111">Follow the instructions to authenticate using the code and sign in to your Azure account through a web browser.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="4edf1-112">Create an IoT Hub</span><span class="sxs-lookup"><span data-stu-id="4edf1-112">Create an IoT Hub</span></span>

<span data-ttu-id="4edf1-113">Use the Azure CLI to create a resource group and then add an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4edf1-113">Use the Azure CLI to create a resource group and then add an IoT hub.</span></span>

1. <span data-ttu-id="4edf1-114">When you create an IoT hub, you must create it in a resource group.</span><span class="sxs-lookup"><span data-stu-id="4edf1-114">When you create an IoT hub, you must create it in a resource group.</span></span> <span data-ttu-id="4edf1-115">Either use an existing resource group, or run the following [command to create a resource group](https://docs.microsoft.com/cli/azure/resource):</span><span class="sxs-lookup"><span data-stu-id="4edf1-115">Either use an existing resource group, or run the following [command to create a resource group](https://docs.microsoft.com/cli/azure/resource):</span></span>
    
   ```azurecli
   az group create --name {your resource group name} --location westus
   ```

   > [!TIP]
   > <span data-ttu-id="4edf1-116">The previous example creates the resource group in the West US location.</span><span class="sxs-lookup"><span data-stu-id="4edf1-116">The previous example creates the resource group in the West US location.</span></span> <span data-ttu-id="4edf1-117">You can view a list of available locations by running this command:</span><span class="sxs-lookup"><span data-stu-id="4edf1-117">You can view a list of available locations by running this command:</span></span> 
   >
   >``` bash
   >az account list-locations -o table
   >```
   >

2. <span data-ttu-id="4edf1-118">Run the following [command to create an IoT hub](https://docs.microsoft.com/cli/azure/iot/hub#az-iot-hub-create) in your resource group, using a globally unique name for your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="4edf1-118">Run the following [command to create an IoT hub](https://docs.microsoft.com/cli/azure/iot/hub#az-iot-hub-create) in your resource group, using a globally unique name for your IoT hub:</span></span>
    
   ```azurecli
   az iot hub create --name {your iot hub name} \
      --resource-group {your resource group name} --sku S1
   ```

   [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


<span data-ttu-id="4edf1-119">The previous command creates an IoT hub in the S1 pricing tier for which you are billed.</span><span class="sxs-lookup"><span data-stu-id="4edf1-119">The previous command creates an IoT hub in the S1 pricing tier for which you are billed.</span></span> <span data-ttu-id="4edf1-120">For more information, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="4edf1-120">For more information, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

## <a name="remove-an-iot-hub"></a><span data-ttu-id="4edf1-121">Remove an IoT Hub</span><span class="sxs-lookup"><span data-stu-id="4edf1-121">Remove an IoT Hub</span></span>

<span data-ttu-id="4edf1-122">You can use Azure CLI to [delete an individual resource](https://docs.microsoft.com/cli/azure/resource), such as an IoT hub, or delete a resource group and all its resources, including any IoT hubs.</span><span class="sxs-lookup"><span data-stu-id="4edf1-122">You can use Azure CLI to [delete an individual resource](https://docs.microsoft.com/cli/azure/resource), such as an IoT hub, or delete a resource group and all its resources, including any IoT hubs.</span></span>

<span data-ttu-id="4edf1-123">To [delete an IoT hub](https://docs.microsoft.com/cli/azure/iot/hub#az-iot-hub-delete), run the following command:</span><span class="sxs-lookup"><span data-stu-id="4edf1-123">To [delete an IoT hub](https://docs.microsoft.com/cli/azure/iot/hub#az-iot-hub-delete), run the following command:</span></span>

```azurecli
az iot hub delete --name {your iot hub name} -\
  -resource-group {your resource group name}
```

<span data-ttu-id="4edf1-124">To [delete a resource group](https://docs.microsoft.com/cli/azure/group#az-group-delete) and all its resources, run the following command:</span><span class="sxs-lookup"><span data-stu-id="4edf1-124">To [delete a resource group](https://docs.microsoft.com/cli/azure/group#az-group-delete) and all its resources, run the following command:</span></span>

```azurecli
az group delete --name {your resource group name}
```

## <a name="next-steps"></a><span data-ttu-id="4edf1-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="4edf1-125">Next steps</span></span>

<span data-ttu-id="4edf1-126">To learn more about using an IoT hub, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="4edf1-126">To learn more about using an IoT hub, see the following articles:</span></span>

* [<span data-ttu-id="4edf1-127">IoT Hub developer guide</span><span class="sxs-lookup"><span data-stu-id="4edf1-127">IoT Hub developer guide</span></span>](iot-hub-devguide.md)
* [<span data-ttu-id="4edf1-128">Using the Azure portal to manage IoT Hub</span><span class="sxs-lookup"><span data-stu-id="4edf1-128">Using the Azure portal to manage IoT Hub</span></span>](iot-hub-create-through-portal.md)
