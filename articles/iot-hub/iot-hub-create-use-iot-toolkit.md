---
title: Create an Azure IoT Hub using Azure IoT Toolkit for VS Code | Microsoft Docs
description: How to use Azure IoT Toolkit for VS Code to create an IoT hub.
author: formulahendry
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.date: 07/30/2018
ms.author: junhan
ms.openlocfilehash: fd89c870794c8af8b8a889eafadc09461cc071e4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866122"
---
# <a name="create-an-iot-hub-using-the-azure-iot-toolkit-for-visual-studio-code"></a><span data-ttu-id="9db14-103">Create an IoT hub using the Azure IoT Toolkit for Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="9db14-103">Create an IoT hub using the Azure IoT Toolkit for Visual Studio Code</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="9db14-104">This article shows you how to use the [Azure IoT Toolkit for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit) to create an Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="9db14-104">This article shows you how to use the [Azure IoT Toolkit for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit) to create an Azure IoT hub.</span></span> 

<span data-ttu-id="9db14-105">To complete this article, you need the following:</span><span class="sxs-lookup"><span data-stu-id="9db14-105">To complete this article, you need the following:</span></span>

- <span data-ttu-id="9db14-106">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="9db14-106">An Azure subscription.</span></span> <span data-ttu-id="9db14-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="9db14-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

- [<span data-ttu-id="9db14-108">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="9db14-108">Visual Studio Code</span></span>](https://code.visualstudio.com/)

- [<span data-ttu-id="9db14-109">Azure IoT Toolkit</span><span class="sxs-lookup"><span data-stu-id="9db14-109">Azure IoT Toolkit</span></span>](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit)

## <a name="create-an-iot-hub"></a><span data-ttu-id="9db14-110">Create an IoT hub</span><span class="sxs-lookup"><span data-stu-id="9db14-110">Create an IoT hub</span></span>

1. <span data-ttu-id="9db14-111">In Visual Studio Code, open the **Explorer** view.</span><span class="sxs-lookup"><span data-stu-id="9db14-111">In Visual Studio Code, open the **Explorer** view.</span></span>

2. <span data-ttu-id="9db14-112">At the bottom of the Explorer, expand the **Azure IoT Hub Devices** section.</span><span class="sxs-lookup"><span data-stu-id="9db14-112">At the bottom of the Explorer, expand the **Azure IoT Hub Devices** section.</span></span> 

   ![Expand Azure IoT Hub Devices](./media/iot-hub-create-use-iot-toolkit/azure-iot-hub-devices.png)

3. <span data-ttu-id="9db14-114">Click on the **...** in the **Azure IoT Hub Devices** section header.</span><span class="sxs-lookup"><span data-stu-id="9db14-114">Click on the **...** in the **Azure IoT Hub Devices** section header.</span></span> <span data-ttu-id="9db14-115">If you don't see the ellipsis, hover over the header.</span><span class="sxs-lookup"><span data-stu-id="9db14-115">If you don't see the ellipsis, hover over the header.</span></span> 

4. <span data-ttu-id="9db14-116">Choose **Create IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="9db14-116">Choose **Create IoT Hub**.</span></span>

5. <span data-ttu-id="9db14-117">A pop-up will show in the bottom right corner to let you sign in to Azure for the first time.</span><span class="sxs-lookup"><span data-stu-id="9db14-117">A pop-up will show in the bottom right corner to let you sign in to Azure for the first time.</span></span>

6. <span data-ttu-id="9db14-118">Select Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="9db14-118">Select Azure subscription.</span></span> 

7. <span data-ttu-id="9db14-119">Select resource group.</span><span class="sxs-lookup"><span data-stu-id="9db14-119">Select resource group.</span></span>

8. <span data-ttu-id="9db14-120">Select location.</span><span class="sxs-lookup"><span data-stu-id="9db14-120">Select location.</span></span>

9. <span data-ttu-id="9db14-121">Select pricing tier.</span><span class="sxs-lookup"><span data-stu-id="9db14-121">Select pricing tier.</span></span>

10. <span data-ttu-id="9db14-122">Enter a globally unique name for your IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9db14-122">Enter a globally unique name for your IoT Hub.</span></span>

11. <span data-ttu-id="9db14-123">Wait a few minutes until the IoT Hub is created.</span><span class="sxs-lookup"><span data-stu-id="9db14-123">Wait a few minutes until the IoT Hub is created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9db14-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="9db14-124">Next steps</span></span>

<span data-ttu-id="9db14-125">Now you have deployed an IoT hub using the Azure IoT Toolkit for Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="9db14-125">Now you have deployed an IoT hub using the Azure IoT Toolkit for Visual Studio Code.</span></span> <span data-ttu-id="9db14-126">To explore further, check out the following articles:</span><span class="sxs-lookup"><span data-stu-id="9db14-126">To explore further, check out the following articles:</span></span>

* <span data-ttu-id="9db14-127">[Use the Azure IoT Toolkit extension for Visual Studio Code to send and receive messages between your device and an IoT Hub](iot-hub-vscode-iot-toolkit-cloud-device-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="9db14-127">[Use the Azure IoT Toolkit extension for Visual Studio Code to send and receive messages between your device and an IoT Hub](iot-hub-vscode-iot-toolkit-cloud-device-messaging.md).</span></span>

* [<span data-ttu-id="9db14-128">Use the Azure IoT Toolkit extension for Visual Studio Code for Azure IoT Hub device management</span><span class="sxs-lookup"><span data-stu-id="9db14-128">Use the Azure IoT Toolkit extension for Visual Studio Code for Azure IoT Hub device management</span></span>](iot-hub-device-management-iot-toolkit.md)

* <span data-ttu-id="9db14-129">[See the Azure IoT Toolkit wiki page](https://github.com/microsoft/vscode-azure-iot-toolkit/wiki).</span><span class="sxs-lookup"><span data-stu-id="9db14-129">[See the Azure IoT Toolkit wiki page](https://github.com/microsoft/vscode-azure-iot-toolkit/wiki).</span></span>
