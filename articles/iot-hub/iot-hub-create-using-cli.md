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
# <a name="create-an-iot-hub-using-azure-cli"></a>Create an IoT hub using Azure CLI

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

This article shows you how to create an IoT hub using Azure CLI.

## <a name="prerequisites"></a>Prerequisites

To complete this how-to, you need an Azure subscription. If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="sign-in-and-set-your-azure-account"></a>Sign in and set your Azure account

If you are running Azure CLI locally instead of using Cloud Shell, you need to sign in to your Azure account.

At the command prompt, run the [login command](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli):

    ```azurecli
    az login
    ```

Follow the instructions to authenticate using the code and sign in to your Azure account through a web browser.

## <a name="create-an-iot-hub"></a>Create an IoT Hub

Use the Azure CLI to create a resource group and then add an IoT hub.

1. When you create an IoT hub, you must create it in a resource group. Either use an existing resource group, or run the following [command to create a resource group](https://docs.microsoft.com/cli/azure/resource):
    
   ```azurecli
   az group create --name {your resource group name} --location westus
   ```

   > [!TIP]
   > The previous example creates the resource group in the West US location. You can view a list of available locations by running this command: 
   >
   >``` bash
   >az account list-locations -o table
   >```
   >

2. Run the following [command to create an IoT hub](https://docs.microsoft.com/cli/azure/iot/hub#az-iot-hub-create) in your resource group, using a globally unique name for your IoT hub:
    
   ```azurecli
   az iot hub create --name {your iot hub name} \
      --resource-group {your resource group name} --sku S1
   ```

   [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


The previous command creates an IoT hub in the S1 pricing tier for which you are billed. For more information, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).

## <a name="remove-an-iot-hub"></a>Remove an IoT Hub

You can use Azure CLI to [delete an individual resource](https://docs.microsoft.com/cli/azure/resource), such as an IoT hub, or delete a resource group and all its resources, including any IoT hubs.

To [delete an IoT hub](https://docs.microsoft.com/cli/azure/iot/hub#az-iot-hub-delete), run the following command:

```azurecli
az iot hub delete --name {your iot hub name} -\
  -resource-group {your resource group name}
```

To [delete a resource group](https://docs.microsoft.com/cli/azure/group#az-group-delete) and all its resources, run the following command:

```azurecli
az group delete --name {your resource group name}
```

## <a name="next-steps"></a>Next steps

To learn more about using an IoT hub, see the following articles:

* [IoT Hub developer guide](iot-hub-devguide.md)
* [Using the Azure portal to manage IoT Hub](iot-hub-create-through-portal.md)
