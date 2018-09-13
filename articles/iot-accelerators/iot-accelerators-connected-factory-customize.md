---
title: Customize the Connected Factory solution - Azure | Microsoft Docs
description: A description of how to customize the behavior of the Connected Factory solution accelerator.
author: dominicbetts
manager: timlt
ms.service: iot-accelerators
services: iot-accelerators
ms.devlang: csharp
ms.topic: conceptual
ms.date: 12/14/2017
ms.author: dobett
ms.openlocfilehash: e91f36c9d6f0cb3195e6903d55cd676f1e9ccf5a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855830"
---
# <a name="customize-how-the-connected-factory-solution-displays-data-from-your-opc-ua-servers"></a><span data-ttu-id="0a18a-103">Customize how the Connected Factory solution displays data from your OPC UA servers</span><span class="sxs-lookup"><span data-stu-id="0a18a-103">Customize how the Connected Factory solution displays data from your OPC UA servers</span></span>

<span data-ttu-id="0a18a-104">The Connected Factory solution aggregates and displays data from the OPC UA servers connected to the solution.</span><span class="sxs-lookup"><span data-stu-id="0a18a-104">The Connected Factory solution aggregates and displays data from the OPC UA servers connected to the solution.</span></span> <span data-ttu-id="0a18a-105">You can browse and send commands to the OPC UA servers in your solution.</span><span class="sxs-lookup"><span data-stu-id="0a18a-105">You can browse and send commands to the OPC UA servers in your solution.</span></span> <span data-ttu-id="0a18a-106">For more information about OPC UA, see the [Connected Factory FAQ](iot-accelerators-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="0a18a-106">For more information about OPC UA, see the [Connected Factory FAQ](iot-accelerators-faq-cf.md).</span></span>

<span data-ttu-id="0a18a-107">Examples of aggregated data in the solution include the Overall Equipment Efficiency (OEE) and Key Performance Indicators (KPIs) that you can view in the dashboard at the factory, line, and station levels.</span><span class="sxs-lookup"><span data-stu-id="0a18a-107">Examples of aggregated data in the solution include the Overall Equipment Efficiency (OEE) and Key Performance Indicators (KPIs) that you can view in the dashboard at the factory, line, and station levels.</span></span> <span data-ttu-id="0a18a-108">The following screenshot shows the OEE and KPI values for the **Assembly** station, on **Production line 1**, in the **Munich** factory:</span><span class="sxs-lookup"><span data-stu-id="0a18a-108">The following screenshot shows the OEE and KPI values for the **Assembly** station, on **Production line 1**, in the **Munich** factory:</span></span>

![Example of OEE and KPI values in the solution][img-oee-kpi]

<span data-ttu-id="0a18a-110">The solution enables you to view detailed information from specific data items from the OPC UA servers, called *stations*.</span><span class="sxs-lookup"><span data-stu-id="0a18a-110">The solution enables you to view detailed information from specific data items from the OPC UA servers, called *stations*.</span></span> <span data-ttu-id="0a18a-111">The following screenshot shows plots of the number of manufactured items from a specific station:</span><span class="sxs-lookup"><span data-stu-id="0a18a-111">The following screenshot shows plots of the number of manufactured items from a specific station:</span></span>

![Plots of number of manufactured items][img-manufactured-items]

<span data-ttu-id="0a18a-113">If you click one of the graphs, you can explore the data further using Time Series Insights (TSI):</span><span class="sxs-lookup"><span data-stu-id="0a18a-113">If you click one of the graphs, you can explore the data further using Time Series Insights (TSI):</span></span>

![Explore data using Time Series Insights][img-tsi]

<span data-ttu-id="0a18a-115">This article describes:</span><span class="sxs-lookup"><span data-stu-id="0a18a-115">This article describes:</span></span>

- <span data-ttu-id="0a18a-116">How the data is made available to the various views in the solution.</span><span class="sxs-lookup"><span data-stu-id="0a18a-116">How the data is made available to the various views in the solution.</span></span>
- <span data-ttu-id="0a18a-117">How you can customize the way the solution displays the data.</span><span class="sxs-lookup"><span data-stu-id="0a18a-117">How you can customize the way the solution displays the data.</span></span>

## <a name="data-sources"></a><span data-ttu-id="0a18a-118">Data sources</span><span class="sxs-lookup"><span data-stu-id="0a18a-118">Data sources</span></span>

<span data-ttu-id="0a18a-119">The Connected Factory solution displays data from the OPC UA servers connected to the solution.</span><span class="sxs-lookup"><span data-stu-id="0a18a-119">The Connected Factory solution displays data from the OPC UA servers connected to the solution.</span></span> <span data-ttu-id="0a18a-120">The default installation includes several OPC UA servers running a factory simulation.</span><span class="sxs-lookup"><span data-stu-id="0a18a-120">The default installation includes several OPC UA servers running a factory simulation.</span></span> <span data-ttu-id="0a18a-121">You can add your own OPC UA servers that [connect through a gateway][lnk-connect-cf] to your solution.</span><span class="sxs-lookup"><span data-stu-id="0a18a-121">You can add your own OPC UA servers that [connect through a gateway][lnk-connect-cf] to your solution.</span></span>

<span data-ttu-id="0a18a-122">You can browse the data items that a connected OPC UA server can send to your solution in the dashboard:</span><span class="sxs-lookup"><span data-stu-id="0a18a-122">You can browse the data items that a connected OPC UA server can send to your solution in the dashboard:</span></span>

1. <span data-ttu-id="0a18a-123">Choose **Browser** to navigate to the **Select an OPC UA server** view:</span><span class="sxs-lookup"><span data-stu-id="0a18a-123">Choose **Browser** to navigate to the **Select an OPC UA server** view:</span></span>

    ![Navigate to the Select an OPC UA server view][img-select-server]

1. <span data-ttu-id="0a18a-125">Select a server and click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="0a18a-125">Select a server and click **Connect**.</span></span> <span data-ttu-id="0a18a-126">Click **Proceed** when the security warning appears.</span><span class="sxs-lookup"><span data-stu-id="0a18a-126">Click **Proceed** when the security warning appears.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0a18a-127">This warning only appears once for each server and establishes a trust relationship between the solution dashboard and the server.</span><span class="sxs-lookup"><span data-stu-id="0a18a-127">This warning only appears once for each server and establishes a trust relationship between the solution dashboard and the server.</span></span>

1. <span data-ttu-id="0a18a-128">You can now browse the data items that the server can send to the solution.</span><span class="sxs-lookup"><span data-stu-id="0a18a-128">You can now browse the data items that the server can send to the solution.</span></span> <span data-ttu-id="0a18a-129">Items that are being sent to the solution have a check mark:</span><span class="sxs-lookup"><span data-stu-id="0a18a-129">Items that are being sent to the solution have a check mark:</span></span>

    ![Published items][img-published]

1. <span data-ttu-id="0a18a-131">If you are an *Administrator* in the solution, you can choose to publish a data item to make it available in the Connected Factory solution.</span><span class="sxs-lookup"><span data-stu-id="0a18a-131">If you are an *Administrator* in the solution, you can choose to publish a data item to make it available in the Connected Factory solution.</span></span> <span data-ttu-id="0a18a-132">As an Administrator, you can also change the value of data items and call methods in the OPC UA server.</span><span class="sxs-lookup"><span data-stu-id="0a18a-132">As an Administrator, you can also change the value of data items and call methods in the OPC UA server.</span></span>

## <a name="map-the-data"></a><span data-ttu-id="0a18a-133">Map the data</span><span class="sxs-lookup"><span data-stu-id="0a18a-133">Map the data</span></span>

<span data-ttu-id="0a18a-134">The Connected Factory solution maps and aggregates the published data items from the OPC UA server to the various views in the solution.</span><span class="sxs-lookup"><span data-stu-id="0a18a-134">The Connected Factory solution maps and aggregates the published data items from the OPC UA server to the various views in the solution.</span></span> <span data-ttu-id="0a18a-135">The Connected Factory solution deploys to your Azure account when you provision the solution.</span><span class="sxs-lookup"><span data-stu-id="0a18a-135">The Connected Factory solution deploys to your Azure account when you provision the solution.</span></span> <span data-ttu-id="0a18a-136">A JSON file in the Visual Studio Connected Factory solution stores this mapping information.</span><span class="sxs-lookup"><span data-stu-id="0a18a-136">A JSON file in the Visual Studio Connected Factory solution stores this mapping information.</span></span> <span data-ttu-id="0a18a-137">You can view and modify this JSON configuration file in the Connected Factory Visual Studio solution.</span><span class="sxs-lookup"><span data-stu-id="0a18a-137">You can view and modify this JSON configuration file in the Connected Factory Visual Studio solution.</span></span> <span data-ttu-id="0a18a-138">You can redeploy the solution after you make a change.</span><span class="sxs-lookup"><span data-stu-id="0a18a-138">You can redeploy the solution after you make a change.</span></span>

<span data-ttu-id="0a18a-139">You can use the configuration file to:</span><span class="sxs-lookup"><span data-stu-id="0a18a-139">You can use the configuration file to:</span></span>

- <span data-ttu-id="0a18a-140">Edit the existing simulated factories, production lines, and stations.</span><span class="sxs-lookup"><span data-stu-id="0a18a-140">Edit the existing simulated factories, production lines, and stations.</span></span>
- <span data-ttu-id="0a18a-141">Map data from real OPC UA servers that you connect to the solution.</span><span class="sxs-lookup"><span data-stu-id="0a18a-141">Map data from real OPC UA servers that you connect to the solution.</span></span>

<span data-ttu-id="0a18a-142">For more information about mapping and aggregating the data to meet your specific requirements, see [How to configure the Connected Factory solution accelerator ](iot-accelerators-connected-factory-configure.md).</span><span class="sxs-lookup"><span data-stu-id="0a18a-142">For more information about mapping and aggregating the data to meet your specific requirements, see [How to configure the Connected Factory solution accelerator ](iot-accelerators-connected-factory-configure.md).</span></span>

## <a name="deploy-the-changes"></a><span data-ttu-id="0a18a-143">Deploy the changes</span><span class="sxs-lookup"><span data-stu-id="0a18a-143">Deploy the changes</span></span>

<span data-ttu-id="0a18a-144">When you have finished making changes to the **ContosoTopologyDescription.json** file, you must redeploy the Connected Factory solution to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="0a18a-144">When you have finished making changes to the **ContosoTopologyDescription.json** file, you must redeploy the Connected Factory solution to your Azure account.</span></span>

<span data-ttu-id="0a18a-145">The **azure-iot-connected-factory** repository includes a **build.ps1** PowerShell script you can use to rebuild and deploy the solution.</span><span class="sxs-lookup"><span data-stu-id="0a18a-145">The **azure-iot-connected-factory** repository includes a **build.ps1** PowerShell script you can use to rebuild and deploy the solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a18a-146">Next Steps</span><span class="sxs-lookup"><span data-stu-id="0a18a-146">Next Steps</span></span>

<span data-ttu-id="0a18a-147">Learn more about the Connected Factory solution accelerator by reading the following articles:</span><span class="sxs-lookup"><span data-stu-id="0a18a-147">Learn more about the Connected Factory solution accelerator by reading the following articles:</span></span>

* <span data-ttu-id="0a18a-148">[Connected Factory solution accelerator walkthrough][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="0a18a-148">[Connected Factory solution accelerator walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="0a18a-149">[Deploy a gateway for Connected Factory][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="0a18a-149">[Deploy a gateway for Connected Factory][lnk-connect-cf]</span></span>
* <span data-ttu-id="0a18a-150">[Permissions on the azureiotsuite.com site][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="0a18a-150">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="0a18a-151">Connected Factory FAQ</span><span class="sxs-lookup"><span data-stu-id="0a18a-151">Connected Factory FAQ</span></span>](iot-accelerators-faq-cf.md)
* <span data-ttu-id="0a18a-152">[FAQ][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="0a18a-152">[FAQ][lnk-faq]</span></span>


[img-oee-kpi]: ./media/iot-accelerators-connected-factory-customize/oeenadkpi.png
[img-manufactured-items]: ./media/iot-accelerators-connected-factory-customize/manufactured.png
[img-tsi]: ./media/iot-accelerators-connected-factory-customize/tsi.png
[img-select-server]: ./media/iot-accelerators-connected-factory-customize/selectserver.png
[img-published]: ./media/iot-accelerators-connected-factory-customize/published.png


[lnk-rm-walkthrough]:iot-accelerators-connected-factory-sample-walkthrough.md
[lnk-connect-cf]:iot-accelerators-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-accelerators-permissions.md
[lnk-faq]: iot-accelerators-faq.md