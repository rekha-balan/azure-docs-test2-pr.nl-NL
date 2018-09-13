---
title: Connect a Raspberry Pi to Azure IoT Suite | Microsoft Docs
description: Tutorials using Node.js or C to help you learn how to use the Microsoft Azure IoT Starter Kit for the Raspberry Pi 3 and the IoT Suite remote monitoring solution. You can chose a tutorial that simulates telemetry, or that uses real sensors, or that enables remote firmware updates.
services: ''
suite: iot-suite
documentationcenter: ''
author: dominicbetts
manager: timlt
editor: ''
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/02/2017
ms.author: dobett
ms.openlocfilehash: d9e737fcaaabd2088d2920b69fca96d6058f4b4a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866517"
---
# <a name="connect-your-microsoft-azure-iot-raspberry-pi-3-starter-kit-to-the-remote-monitoring-solution"></a><span data-ttu-id="a8d3a-104">Connect your Microsoft Azure IoT Raspberry Pi 3 Starter Kit to the remote monitoring solution</span><span class="sxs-lookup"><span data-stu-id="a8d3a-104">Connect your Microsoft Azure IoT Raspberry Pi 3 Starter Kit to the remote monitoring solution</span></span>

<span data-ttu-id="a8d3a-105">The tutorials in this section help you learn how to connect a Raspberry Pi 3 device to the remote monitoring solution.</span><span class="sxs-lookup"><span data-stu-id="a8d3a-105">The tutorials in this section help you learn how to connect a Raspberry Pi 3 device to the remote monitoring solution.</span></span> <span data-ttu-id="a8d3a-106">Choose the tutorial appropriate to your preferred programming language and the whether you have the sensor hardware available to use with your Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="a8d3a-106">Choose the tutorial appropriate to your preferred programming language and the whether you have the sensor hardware available to use with your Raspberry Pi.</span></span>

## <a name="the-tutorials"></a><span data-ttu-id="a8d3a-107">The tutorials</span><span class="sxs-lookup"><span data-stu-id="a8d3a-107">The tutorials</span></span>

| <span data-ttu-id="a8d3a-108">Tutorial</span><span class="sxs-lookup"><span data-stu-id="a8d3a-108">Tutorial</span></span> | <span data-ttu-id="a8d3a-109">Notes</span><span class="sxs-lookup"><span data-stu-id="a8d3a-109">Notes</span></span> | <span data-ttu-id="a8d3a-110">Languages</span><span class="sxs-lookup"><span data-stu-id="a8d3a-110">Languages</span></span> |
| -------- | ----- | --------- |
| <span data-ttu-id="a8d3a-111">Simulated telemetry (Basic)</span><span class="sxs-lookup"><span data-stu-id="a8d3a-111">Simulated telemetry (Basic)</span></span>| <span data-ttu-id="a8d3a-112">Simulates sensor data.</span><span class="sxs-lookup"><span data-stu-id="a8d3a-112">Simulates sensor data.</span></span> <span data-ttu-id="a8d3a-113">Uses a standalone Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="a8d3a-113">Uses a standalone Raspberry Pi.</span></span> | <span data-ttu-id="a8d3a-114">[C][lnk-c-simulator], [Node.js][lnk-node-simulator]</span><span class="sxs-lookup"><span data-stu-id="a8d3a-114">[C][lnk-c-simulator], [Node.js][lnk-node-simulator]</span></span> |
| <span data-ttu-id="a8d3a-115">Real sensor (Intermediate)</span><span class="sxs-lookup"><span data-stu-id="a8d3a-115">Real sensor (Intermediate)</span></span> | <span data-ttu-id="a8d3a-116">Uses data from a BME280 sensor connected to your Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="a8d3a-116">Uses data from a BME280 sensor connected to your Raspberry Pi.</span></span> | <span data-ttu-id="a8d3a-117">[C][lnk-c-basic], [Node.js][lnk-node-basic]</span><span class="sxs-lookup"><span data-stu-id="a8d3a-117">[C][lnk-c-basic], [Node.js][lnk-node-basic]</span></span> |
| <span data-ttu-id="a8d3a-118">Implement firmware update (Advanced)</span><span class="sxs-lookup"><span data-stu-id="a8d3a-118">Implement firmware update (Advanced)</span></span>| <span data-ttu-id="a8d3a-119">Uses data from a BME280 sensor connected to your Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="a8d3a-119">Uses data from a BME280 sensor connected to your Raspberry Pi.</span></span> <span data-ttu-id="a8d3a-120">Enables remote firmware updates on your Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="a8d3a-120">Enables remote firmware updates on your Raspberry Pi.</span></span> | <span data-ttu-id="a8d3a-121">[C][lnk-c-advanced], [Node.js][lnk-node-advanced]</span><span class="sxs-lookup"><span data-stu-id="a8d3a-121">[C][lnk-c-advanced], [Node.js][lnk-node-advanced]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a8d3a-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="a8d3a-122">Next steps</span></span>

<span data-ttu-id="a8d3a-123">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="a8d3a-123">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[lnk-node-simulator]: iot-suite-v1-raspberry-pi-kit-node-get-started-simulator.md
[lnk-node-basic]: iot-suite-v1-raspberry-pi-kit-node-get-started-basic.md
[lnk-node-advanced]: iot-suite-v1-raspberry-pi-kit-node-get-started-advanced.md
[lnk-c-simulator]: iot-suite-v1-raspberry-pi-kit-c-get-started-simulator.md
[lnk-c-basic]: iot-suite-v1-raspberry-pi-kit-c-get-started-basic.md
[lnk-c-advanced]: iot-suite-v1-raspberry-pi-kit-c-get-started-advanced.md