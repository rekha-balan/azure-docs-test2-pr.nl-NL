---
title: Visualize your Azure IoT Central data in a Power BI dashboard | Microsoft Docs
description: Use the Azure IoT Central Analytics Power BI solution template to visualize and analyze your IoT Central data.
ms.service: iot-central
services: iot-central
author: viv-liu
ms.author: viviali
ms.date: 07/16/2018
ms.topic: conceptual
ms.openlocfilehash: 5cb55e73b379b909811bde728d2ab39e29635bf5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871283"
---
# <a name="visualize-and-analyze-your-azure-iot-central-data-in-a-power-bi-dashboard"></a><span data-ttu-id="35114-103">Visualize and analyze your Azure IoT Central data in a Power BI dashboard</span><span class="sxs-lookup"><span data-stu-id="35114-103">Visualize and analyze your Azure IoT Central data in a Power BI dashboard</span></span>

![Power BI solution template pipeline](media/howto-connect-powerbi/iot-continuous-data-export.png)

<span data-ttu-id="35114-105">Use the Azure IoT Central Analytics Power BI solution template to create a powerful Power BI dashboard to monitor the performance of your IoT devices.</span><span class="sxs-lookup"><span data-stu-id="35114-105">Use the Azure IoT Central Analytics Power BI solution template to create a powerful Power BI dashboard to monitor the performance of your IoT devices.</span></span> <span data-ttu-id="35114-106">In your Power BI dashboard, you can:</span><span class="sxs-lookup"><span data-stu-id="35114-106">In your Power BI dashboard, you can:</span></span>
- <span data-ttu-id="35114-107">Track how much data your devices are sending over time</span><span class="sxs-lookup"><span data-stu-id="35114-107">Track how much data your devices are sending over time</span></span>
- <span data-ttu-id="35114-108">Compare data volume between telemetry, states, and events</span><span class="sxs-lookup"><span data-stu-id="35114-108">Compare data volume between telemetry, states, and events</span></span>
- <span data-ttu-id="35114-109">Identify devices that are reporting lots of measurements</span><span class="sxs-lookup"><span data-stu-id="35114-109">Identify devices that are reporting lots of measurements</span></span>
- <span data-ttu-id="35114-110">Observe historical trends of device measurements</span><span class="sxs-lookup"><span data-stu-id="35114-110">Observe historical trends of device measurements</span></span>
- <span data-ttu-id="35114-111">Identify problematic devices that send lots of critical events</span><span class="sxs-lookup"><span data-stu-id="35114-111">Identify problematic devices that send lots of critical events</span></span>

<span data-ttu-id="35114-112">This solution template sets up the pipeline that takes the data in your Azure Blob storage account from [continuous data export](howto-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="35114-112">This solution template sets up the pipeline that takes the data in your Azure Blob storage account from [continuous data export](howto-export-data.md).</span></span> <span data-ttu-id="35114-113">This data flows through to Azure Functions, Azure Data Factory, and Azure SQL Database which process and transform the data to be visualized and analyzed in a Power BI report that you can download as a PBIX file.</span><span class="sxs-lookup"><span data-stu-id="35114-113">This data flows through to Azure Functions, Azure Data Factory, and Azure SQL Database which process and transform the data to be visualized and analyzed in a Power BI report that you can download as a PBIX file.</span></span> <span data-ttu-id="35114-114">All of these resources are created in your Azure subscription, so you can customize each component to suit your needs.</span><span class="sxs-lookup"><span data-stu-id="35114-114">All of these resources are created in your Azure subscription, so you can customize each component to suit your needs.</span></span> <span data-ttu-id="35114-115">This solution template is completely open-sourced, so you can learn more about the architecture and extend the solution by visiting the [Github repo](https://aka.ms/iotcentralgithubpowerbisolutiontemplate).</span><span class="sxs-lookup"><span data-stu-id="35114-115">This solution template is completely open-sourced, so you can learn more about the architecture and extend the solution by visiting the [Github repo](https://aka.ms/iotcentralgithubpowerbisolutiontemplate).</span></span>

<span data-ttu-id="35114-116">**[Get the Azure IoT Central Analytics solution template from Microsoft AppSource.](https://aka.ms/iotcentralpowerbisolutiontemplate)**</span><span class="sxs-lookup"><span data-stu-id="35114-116">**[Get the Azure IoT Central Analytics solution template from Microsoft AppSource.](https://aka.ms/iotcentralpowerbisolutiontemplate)**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35114-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="35114-117">Prerequisites</span></span>
<span data-ttu-id="35114-118">Setting up the template requires the following:</span><span class="sxs-lookup"><span data-stu-id="35114-118">Setting up the template requires the following:</span></span>
- <span data-ttu-id="35114-119">Access to an Azure subscription</span><span class="sxs-lookup"><span data-stu-id="35114-119">Access to an Azure subscription</span></span>
- <span data-ttu-id="35114-120">Exported data using [continuous data export](howto-export-data.md) from your IoT Central app.</span><span class="sxs-lookup"><span data-stu-id="35114-120">Exported data using [continuous data export](howto-export-data.md) from your IoT Central app.</span></span> <span data-ttu-id="35114-121">We recommend you turn on measurements, devices, and device template streams to get the most out of the Power BI dashboard.</span><span class="sxs-lookup"><span data-stu-id="35114-121">We recommend you turn on measurements, devices, and device template streams to get the most out of the Power BI dashboard.</span></span>
- <span data-ttu-id="35114-122">Power BI Desktop (latest version)</span><span class="sxs-lookup"><span data-stu-id="35114-122">Power BI Desktop (latest version)</span></span>
- <span data-ttu-id="35114-123">Power BI Pro (if you want to share the dashboard with others)</span><span class="sxs-lookup"><span data-stu-id="35114-123">Power BI Pro (if you want to share the dashboard with others)</span></span>

## <a name="reports"></a><span data-ttu-id="35114-124">Reports</span><span class="sxs-lookup"><span data-stu-id="35114-124">Reports</span></span>

<span data-ttu-id="35114-125">Two reports are generated automatically.</span><span class="sxs-lookup"><span data-stu-id="35114-125">Two reports are generated automatically.</span></span> 

<span data-ttu-id="35114-126">The first report shows a historical view of measurements reported by devices, and breaks down the different types of measurements and devices that have sent the highest number of measurements.</span><span class="sxs-lookup"><span data-stu-id="35114-126">The first report shows a historical view of measurements reported by devices, and breaks down the different types of measurements and devices that have sent the highest number of measurements.</span></span>

![Power BI report page 1](media/howto-connect-powerbi/template-page1-hasdata.PNG)

<span data-ttu-id="35114-128">The second report dives deeper into events and shows a historical view of errors and warnings reported.</span><span class="sxs-lookup"><span data-stu-id="35114-128">The second report dives deeper into events and shows a historical view of errors and warnings reported.</span></span> <span data-ttu-id="35114-129">It also shows which devices are reporting the highest number of events all up, as well as specifically error events and warning events.</span><span class="sxs-lookup"><span data-stu-id="35114-129">It also shows which devices are reporting the highest number of events all up, as well as specifically error events and warning events.</span></span>

![Power BI report page 2](media/howto-connect-powerbi/template-page2-hasdata.PNG)

## <a name="resources"></a><span data-ttu-id="35114-131">Resources</span><span class="sxs-lookup"><span data-stu-id="35114-131">Resources</span></span>

<span data-ttu-id="35114-132">Visit AppSource to get the [Azure IoT Central Analytics solution template](https://aka.ms/iotcentralpowerbisolutiontemplate).</span><span class="sxs-lookup"><span data-stu-id="35114-132">Visit AppSource to get the [Azure IoT Central Analytics solution template](https://aka.ms/iotcentralpowerbisolutiontemplate).</span></span>

<span data-ttu-id="35114-133">Visit the [Github repo](https://aka.ms/iotcentralgithubpowerbisolutiontemplate) to learn more about the architecture and extend the solution.</span><span class="sxs-lookup"><span data-stu-id="35114-133">Visit the [Github repo](https://aka.ms/iotcentralgithubpowerbisolutiontemplate) to learn more about the architecture and extend the solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35114-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="35114-134">Next steps</span></span>

<span data-ttu-id="35114-135">Now that you have learned how to visualize your data in Power BI, here is the suggested next step:</span><span class="sxs-lookup"><span data-stu-id="35114-135">Now that you have learned how to visualize your data in Power BI, here is the suggested next step:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="35114-136">How to manage devices</span><span class="sxs-lookup"><span data-stu-id="35114-136">How to manage devices</span></span>](howto-manage-devices.md)
