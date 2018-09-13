---
title: Use an existing IoT hub with the Device Simulation solution - Azure | Microsoft Docs
description: This article describes how to configure the Device Simulation solution accelerator to use an existing IoT Hub.
author: dominicbetts
manager: timlt
ms.author: dobett
ms.service: iot-accelerators
services: iot-accelerators
ms.date: 07/06/2018
ms.topic: conceptual
ms.openlocfilehash: ee96173ca5f36dee0f08c38e4b6e29da6fee804e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856705"
---
# <a name="use-an-existing-iot-hub-with-the-device-simulation-solution-accelerator"></a><span data-ttu-id="25ba5-103">Use an existing IoT hub with the Device Simulation solution accelerator</span><span class="sxs-lookup"><span data-stu-id="25ba5-103">Use an existing IoT hub with the Device Simulation solution accelerator</span></span>

<span data-ttu-id="25ba5-104">When you provision the Device Simulation solution accelerator, you can choose to deploy an IoT hub in the solution accelerator's resource group to use in your simulation.</span><span class="sxs-lookup"><span data-stu-id="25ba5-104">When you provision the Device Simulation solution accelerator, you can choose to deploy an IoT hub in the solution accelerator's resource group to use in your simulation.</span></span>

<span data-ttu-id="25ba5-105">If you don't choose to deploy the optional IoT Hub, you must use your own hub for any simulations you run.</span><span class="sxs-lookup"><span data-stu-id="25ba5-105">If you don't choose to deploy the optional IoT Hub, you must use your own hub for any simulations you run.</span></span> <span data-ttu-id="25ba5-106">If you do choose to deploy the optional IoT Hub, you can choose to use this optional hub or your own hub.</span><span class="sxs-lookup"><span data-stu-id="25ba5-106">If you do choose to deploy the optional IoT Hub, you can choose to use this optional hub or your own hub.</span></span>

<span data-ttu-id="25ba5-107">If you don't have an IoT hub, you can always create a new one from the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="25ba5-107">If you don't have an IoT hub, you can always create a new one from the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="25ba5-108">To use a pre-existing IoT hub, you need a connection string for the **iothubowner** shared access policy.</span><span class="sxs-lookup"><span data-stu-id="25ba5-108">To use a pre-existing IoT hub, you need a connection string for the **iothubowner** shared access policy.</span></span> <span data-ttu-id="25ba5-109">You can get this connection string from the [Azure portal](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="25ba5-109">You can get this connection string from the [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="25ba5-110">On the hub's configuration page in the portal, click **Shared access policies**.</span><span class="sxs-lookup"><span data-stu-id="25ba5-110">On the hub's configuration page in the portal, click **Shared access policies**.</span></span>
1. <span data-ttu-id="25ba5-111">Click **iothubowner**.</span><span class="sxs-lookup"><span data-stu-id="25ba5-111">Click **iothubowner**.</span></span>
1. <span data-ttu-id="25ba5-112">Copy either the primary or secondary connection string.</span><span class="sxs-lookup"><span data-stu-id="25ba5-112">Copy either the primary or secondary connection string.</span></span>

<span data-ttu-id="25ba5-113">[![Get connection string](./media/iot-accelerators-device-simulation-choose-hub/connectionstring-inline.png)](./media/iot-accelerators-device-simulation-choose-hub/connectionstring-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="25ba5-113">[![Get connection string](./media/iot-accelerators-device-simulation-choose-hub/connectionstring-inline.png)](./media/iot-accelerators-device-simulation-choose-hub/connectionstring-expanded.png#lightbox)</span></span>

<span data-ttu-id="25ba5-114">USe the connection string you copied when you configure the simulation:</span><span class="sxs-lookup"><span data-stu-id="25ba5-114">USe the connection string you copied when you configure the simulation:</span></span>

<span data-ttu-id="25ba5-115">[![Configure simulation](./media/iot-accelerators-device-simulation-choose-hub/configuresimulation-inline.png)](./media/iot-accelerators-device-simulation-choose-hub/configuresimulation-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="25ba5-115">[![Configure simulation](./media/iot-accelerators-device-simulation-choose-hub/configuresimulation-inline.png)](./media/iot-accelerators-device-simulation-choose-hub/configuresimulation-expanded.png#lightbox)</span></span>

## <a name="next-steps"></a><span data-ttu-id="25ba5-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="25ba5-116">Next steps</span></span>

<span data-ttu-id="25ba5-117">In this how-to guide, you've learned how to use an existing IoT hub in a simulation.</span><span class="sxs-lookup"><span data-stu-id="25ba5-117">In this how-to guide, you've learned how to use an existing IoT hub in a simulation.</span></span> <span data-ttu-id="25ba5-118">Next, you may want to learn how to [Configure a custom device model](iot-accelerators-device-simulation-custom-model.md) for a simulation.</span><span class="sxs-lookup"><span data-stu-id="25ba5-118">Next, you may want to learn how to [Configure a custom device model](iot-accelerators-device-simulation-custom-model.md) for a simulation.</span></span>
