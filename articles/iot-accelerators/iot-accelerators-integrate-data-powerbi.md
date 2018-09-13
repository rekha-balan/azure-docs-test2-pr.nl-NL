---
title: Visualize Remote Monitoring data using Power BI - Azure | Microsoft Docs
description: This tutorial uses Power BI Desktop and Cosmos DB to integerate data from a Remote Monitoring solution into a customized visualization. This way users can build their own custom dashboards and share them out to users not on the solution.
author: asdonald
manager: hegate
ms.author: asdonald
ms.service: iot-accelerators
services: iot-accelerators
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: ae039573cf202059114f23cca86207c117a35ead
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868022"
---
# <a name="visualize-remote-monitoring-data-using-power-bi"></a><span data-ttu-id="0f98b-104">Visualize Remote Monitoring data using Power BI</span><span class="sxs-lookup"><span data-stu-id="0f98b-104">Visualize Remote Monitoring data using Power BI</span></span>

<span data-ttu-id="0f98b-105">This tutorial will walk you through how to plug in your Remote Monitoring solution data from CosmosDB into Power BI.</span><span class="sxs-lookup"><span data-stu-id="0f98b-105">This tutorial will walk you through how to plug in your Remote Monitoring solution data from CosmosDB into Power BI.</span></span> <span data-ttu-id="0f98b-106">With this connection established, you can then create your own custom dashboards, and add them back onto your Remote Monitoring solution dashboard.</span><span class="sxs-lookup"><span data-stu-id="0f98b-106">With this connection established, you can then create your own custom dashboards, and add them back onto your Remote Monitoring solution dashboard.</span></span> <span data-ttu-id="0f98b-107">This workstream allows for more specialized graphs to be created, in addition to the ones out of the box.</span><span class="sxs-lookup"><span data-stu-id="0f98b-107">This workstream allows for more specialized graphs to be created, in addition to the ones out of the box.</span></span> <span data-ttu-id="0f98b-108">You can then use this tutorial to integrate with other data streams or build custom dashboards to be consumed outside of your Remote Monitoring Solution.</span><span class="sxs-lookup"><span data-stu-id="0f98b-108">You can then use this tutorial to integrate with other data streams or build custom dashboards to be consumed outside of your Remote Monitoring Solution.</span></span> <span data-ttu-id="0f98b-109">Building dashboards in Power BI means that you can also make each panel interact with one another as you select specific pieces.</span><span class="sxs-lookup"><span data-stu-id="0f98b-109">Building dashboards in Power BI means that you can also make each panel interact with one another as you select specific pieces.</span></span> <span data-ttu-id="0f98b-110">For example, you could have a filter that shows you only information about your simulated trucks and each piece of your dashboard would interact to show you only simulated truck information.</span><span class="sxs-lookup"><span data-stu-id="0f98b-110">For example, you could have a filter that shows you only information about your simulated trucks and each piece of your dashboard would interact to show you only simulated truck information.</span></span> <span data-ttu-id="0f98b-111">If you would like to use a tool other than Power BI, you can also extend these steps to use your visualization tool of choice and hook into the Cosmos Database, or custom database if you've set one up.</span><span class="sxs-lookup"><span data-stu-id="0f98b-111">If you would like to use a tool other than Power BI, you can also extend these steps to use your visualization tool of choice and hook into the Cosmos Database, or custom database if you've set one up.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0f98b-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0f98b-112">Prerequisites</span></span>

- <span data-ttu-id="0f98b-113">You must have a Remote Monitoring solution currently running</span><span class="sxs-lookup"><span data-stu-id="0f98b-113">You must have a Remote Monitoring solution currently running</span></span>
- <span data-ttu-id="0f98b-114">You must have access to [Azure Portal](https://portal.azure.com) and your subscription on which the IoT Hub and Solution are running</span><span class="sxs-lookup"><span data-stu-id="0f98b-114">You must have access to [Azure Portal](https://portal.azure.com) and your subscription on which the IoT Hub and Solution are running</span></span>
- <span data-ttu-id="0f98b-115">You must have [Power BI desktop](https://powerbi.microsoft.com) installed, any version will do</span><span class="sxs-lookup"><span data-stu-id="0f98b-115">You must have [Power BI desktop](https://powerbi.microsoft.com) installed, any version will do</span></span>


## <a name="information-needed-from-azure-portal"></a><span data-ttu-id="0f98b-116">Information Needed from Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0f98b-116">Information Needed from Azure Portal</span></span>

1. <span data-ttu-id="0f98b-117">Navigate to [Azure Portal](https://portal.azure.com) and log in if needed</span><span class="sxs-lookup"><span data-stu-id="0f98b-117">Navigate to [Azure Portal](https://portal.azure.com) and log in if needed</span></span>

2. <span data-ttu-id="0f98b-118">On the left-hand panel, click Resource groups</span><span class="sxs-lookup"><span data-stu-id="0f98b-118">On the left-hand panel, click Resource groups</span></span>

    ![Side Panel Nav](./media/iot-accelerators-integrate-data-powerbi/side_panel.png)

3. <span data-ttu-id="0f98b-120">Navigate to the Resource Group of which your Iot Solution is running on and click to be taken to that Resource Group's Overview page.</span><span class="sxs-lookup"><span data-stu-id="0f98b-120">Navigate to the Resource Group of which your Iot Solution is running on and click to be taken to that Resource Group's Overview page.</span></span> 

4. <span data-ttu-id="0f98b-121">On that overview page click the item, which has type "Azure Cosmos DB Account", you will then be taken to the overview page of the Cosmos DB stream for that IoT Solution.</span><span class="sxs-lookup"><span data-stu-id="0f98b-121">On that overview page click the item, which has type "Azure Cosmos DB Account", you will then be taken to the overview page of the Cosmos DB stream for that IoT Solution.</span></span>

    ![Resource Group](./media/iot-accelerators-integrate-data-powerbi/resource_groups.png)

5. <span data-ttu-id="0f98b-123">On the panel to the left, click the "Keys" section and take note of the following values to be used in PowerBi:</span><span class="sxs-lookup"><span data-stu-id="0f98b-123">On the panel to the left, click the "Keys" section and take note of the following values to be used in PowerBi:</span></span>

    - <span data-ttu-id="0f98b-124">URI</span><span class="sxs-lookup"><span data-stu-id="0f98b-124">URI</span></span>
    - <span data-ttu-id="0f98b-125">Primary Key</span><span class="sxs-lookup"><span data-stu-id="0f98b-125">Primary Key</span></span>

    ![keys](./media/iot-accelerators-integrate-data-powerbi/keys.png)

## <a name="setting-up-the-stream-in-power-bi"></a><span data-ttu-id="0f98b-127">Setting up the Stream in Power BI</span><span class="sxs-lookup"><span data-stu-id="0f98b-127">Setting up the Stream in Power BI</span></span>
  
1. <span data-ttu-id="0f98b-128">Open up the Power BI desktop app and click "Get Data" from the top left corner.</span><span class="sxs-lookup"><span data-stu-id="0f98b-128">Open up the Power BI desktop app and click "Get Data" from the top left corner.</span></span> 

    ![Get Data](./media/iot-accelerators-integrate-data-powerbi/get_data.png)

2. <span data-ttu-id="0f98b-130">When asked to enter data, choose to Search for "Azure Cosmos DB" and select this connector.</span><span class="sxs-lookup"><span data-stu-id="0f98b-130">When asked to enter data, choose to Search for "Azure Cosmos DB" and select this connector.</span></span> <span data-ttu-id="0f98b-131">This connector essentially pulls data straight from the cosmos database of your Azure IoT Solution</span><span class="sxs-lookup"><span data-stu-id="0f98b-131">This connector essentially pulls data straight from the cosmos database of your Azure IoT Solution</span></span>
  
    ![Cosmos DB](./media/iot-accelerators-integrate-data-powerbi/cosmos_db.png)
  
3. <span data-ttu-id="0f98b-133">Enter the information, which you have recorded above:</span><span class="sxs-lookup"><span data-stu-id="0f98b-133">Enter the information, which you have recorded above:</span></span>

    * <span data-ttu-id="0f98b-134">URI</span><span class="sxs-lookup"><span data-stu-id="0f98b-134">URI</span></span>
    * <span data-ttu-id="0f98b-135">Primary Key</span><span class="sxs-lookup"><span data-stu-id="0f98b-135">Primary Key</span></span>

4. <span data-ttu-id="0f98b-136">Select all the tables to be imported into Power BI.</span><span class="sxs-lookup"><span data-stu-id="0f98b-136">Select all the tables to be imported into Power BI.</span></span> <span data-ttu-id="0f98b-137">This action will kick off the loading of the data.</span><span class="sxs-lookup"><span data-stu-id="0f98b-137">This action will kick off the loading of the data.</span></span> <span data-ttu-id="0f98b-138">The longer your solution has been running, the longer it can take for the data to load (up to a few hours).</span><span class="sxs-lookup"><span data-stu-id="0f98b-138">The longer your solution has been running, the longer it can take for the data to load (up to a few hours).</span></span> 

    ![Import Tables](./media/iot-accelerators-integrate-data-powerbi/import_tables.png)

5. <span data-ttu-id="0f98b-140">Once the data has finished loading, click "Edit Queries" on the top row of Power BI and expand all the tables by clicking the arrows in the yellow bar for each table.</span><span class="sxs-lookup"><span data-stu-id="0f98b-140">Once the data has finished loading, click "Edit Queries" on the top row of Power BI and expand all the tables by clicking the arrows in the yellow bar for each table.</span></span> <span data-ttu-id="0f98b-141">This will essentially expand to show all the columns.</span><span class="sxs-lookup"><span data-stu-id="0f98b-141">This will essentially expand to show all the columns.</span></span> <span data-ttu-id="0f98b-142">You will notice how data for things such as humidity, speed time, etc. are not of the correct type.</span><span class="sxs-lookup"><span data-stu-id="0f98b-142">You will notice how data for things such as humidity, speed time, etc. are not of the correct type.</span></span>

    ![New Column](./media/iot-accelerators-integrate-data-powerbi/new_column.png)
  
    <span data-ttu-id="0f98b-144">For example, the data coming into Power BI was changed into UNIX time when it came in through the connector.</span><span class="sxs-lookup"><span data-stu-id="0f98b-144">For example, the data coming into Power BI was changed into UNIX time when it came in through the connector.</span></span> <span data-ttu-id="0f98b-145">To adjust for this conversion, going forward you can create a new column and use this equation to get it into date time format:</span><span class="sxs-lookup"><span data-stu-id="0f98b-145">To adjust for this conversion, going forward you can create a new column and use this equation to get it into date time format:</span></span> 

    ```text
    #datetime(1970, 1, 1, 0, 0, 0) + #duration(0, 0, 0, [Document.device.msg.received]/1000)
    ```

    ![Updated Table](./media/iot-accelerators-integrate-data-powerbi/updated_table.png)
  
    <span data-ttu-id="0f98b-147">Document.device.msg.received is just one of the columns with UNIX formatting and can be substituted with others that need conversion.</span><span class="sxs-lookup"><span data-stu-id="0f98b-147">Document.device.msg.received is just one of the columns with UNIX formatting and can be substituted with others that need conversion.</span></span> 
  
    <span data-ttu-id="0f98b-148">Other data points were converted to type String can be changed into Doubles or Int where appropriate using the same steps as above.</span><span class="sxs-lookup"><span data-stu-id="0f98b-148">Other data points were converted to type String can be changed into Doubles or Int where appropriate using the same steps as above.</span></span>

## <a name="creating-a-dashboard"></a><span data-ttu-id="0f98b-149">Creating a dashboard</span><span class="sxs-lookup"><span data-stu-id="0f98b-149">Creating a dashboard</span></span>

<span data-ttu-id="0f98b-150">Once the stream has been connected, you are ready to create your personalized dashboards!</span><span class="sxs-lookup"><span data-stu-id="0f98b-150">Once the stream has been connected, you are ready to create your personalized dashboards!</span></span> <span data-ttu-id="0f98b-151">The dashboard below is an example of taking the telemetry being immmited by our simulated devices, and showing different pivots around it such as:</span><span class="sxs-lookup"><span data-stu-id="0f98b-151">The dashboard below is an example of taking the telemetry being immmited by our simulated devices, and showing different pivots around it such as:</span></span> 

* <span data-ttu-id="0f98b-152">Device Location on a map (right)</span><span class="sxs-lookup"><span data-stu-id="0f98b-152">Device Location on a map (right)</span></span>
* <span data-ttu-id="0f98b-153">Devices with their status and severity.</span><span class="sxs-lookup"><span data-stu-id="0f98b-153">Devices with their status and severity.</span></span> <span data-ttu-id="0f98b-154">(top left)</span><span class="sxs-lookup"><span data-stu-id="0f98b-154">(top left)</span></span>
* <span data-ttu-id="0f98b-155">Devices with rules in place, and if there are any alarms going off for them (bottom left)</span><span class="sxs-lookup"><span data-stu-id="0f98b-155">Devices with rules in place, and if there are any alarms going off for them (bottom left)</span></span>

![PowerBi Visualization](./media/iot-accelerators-integrate-data-powerbi/visual_data.png)

## <a name="publishing-the-dashboard-and-refreshing-the-data"></a><span data-ttu-id="0f98b-157">Publishing the dashboard and refreshing the data</span><span class="sxs-lookup"><span data-stu-id="0f98b-157">Publishing the dashboard and refreshing the data</span></span>

<span data-ttu-id="0f98b-158">After you have successfully created your dashboards, we recommend that you [publish your Power BI dashboards](https://docs.microsoft.com/power-bi/desktop-upload-desktop-files) to share with others.</span><span class="sxs-lookup"><span data-stu-id="0f98b-158">After you have successfully created your dashboards, we recommend that you [publish your Power BI dashboards](https://docs.microsoft.com/power-bi/desktop-upload-desktop-files) to share with others.</span></span>

<span data-ttu-id="0f98b-159">You'll also want to [refresh the data](https://docs.microsoft.com/power-bi/refresh-data) on the published dashboard to make sure that you have the latest data set.</span><span class="sxs-lookup"><span data-stu-id="0f98b-159">You'll also want to [refresh the data](https://docs.microsoft.com/power-bi/refresh-data) on the published dashboard to make sure that you have the latest data set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f98b-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="0f98b-160">Next steps</span></span>

<span data-ttu-id="0f98b-161">In this article, you learned about how to visualize remote monitoring data using Power BI</span><span class="sxs-lookup"><span data-stu-id="0f98b-161">In this article, you learned about how to visualize remote monitoring data using Power BI</span></span>

<span data-ttu-id="0f98b-162">For more information about customizing the Remote Monitoring solution, see:</span><span class="sxs-lookup"><span data-stu-id="0f98b-162">For more information about customizing the Remote Monitoring solution, see:</span></span>

* [<span data-ttu-id="0f98b-163">Customizing the Remote Monitoring Solution UI</span><span class="sxs-lookup"><span data-stu-id="0f98b-163">Customizing the Remote Monitoring Solution UI</span></span>](iot-accelerators-remote-monitoring-customize.md)
* [<span data-ttu-id="0f98b-164">Developer Reference Guide</span><span class="sxs-lookup"><span data-stu-id="0f98b-164">Developer Reference Guide</span></span>](https://github.com/Azure/azure-iot-pcs-remote-monitoring-dotnet/wiki/Developer-Reference-Guide)
* [<span data-ttu-id="0f98b-165">Developer Troubleshooting Guide</span><span class="sxs-lookup"><span data-stu-id="0f98b-165">Developer Troubleshooting Guide</span></span>](https://github.com/Azure/azure-iot-pcs-remote-monitoring-dotnet/wiki/Developer-Troubleshooting-Guide)

