---
title: Create a custom rule in Azure IoT Suite | Microsoft Docs
description: How to create a custom rule in an IoT Suite preconfigured solution.
services: ''
suite: iot-suite
documentationcenter: ''
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: 562799dc-06ea-4cdd-b822-80d1f70d2f09
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: dobett
ms.openlocfilehash: 900f0b4c38f08d1e3017954db01cf32362765578
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549088"
---
# <a name="create-a-custom-rule-in-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="72774-103">Create a custom rule in the remote monitoring preconfigured solution</span><span class="sxs-lookup"><span data-stu-id="72774-103">Create a custom rule in the remote monitoring preconfigured solution</span></span>

## <a name="introduction"></a><span data-ttu-id="72774-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="72774-104">Introduction</span></span>

<span data-ttu-id="72774-105">In the preconfigured solutions, you can configure [rules that trigger when a telemetry value for a device reaches a specific threshold][lnk-builtin-rule].</span><span class="sxs-lookup"><span data-stu-id="72774-105">In the preconfigured solutions, you can configure [rules that trigger when a telemetry value for a device reaches a specific threshold][lnk-builtin-rule].</span></span> <span data-ttu-id="72774-106">[Use dynamic telemetry with the remote monitoring preconfigured solution][lnk-dynamic-telemetry] describes how you can add custom telemetry values, such as *ExternalTemperature* to your solution.</span><span class="sxs-lookup"><span data-stu-id="72774-106">[Use dynamic telemetry with the remote monitoring preconfigured solution][lnk-dynamic-telemetry] describes how you can add custom telemetry values, such as *ExternalTemperature* to your solution.</span></span> <span data-ttu-id="72774-107">This article shows you how to create custom rule for dynamic telemetry types in your solution.</span><span class="sxs-lookup"><span data-stu-id="72774-107">This article shows you how to create custom rule for dynamic telemetry types in your solution.</span></span>

<span data-ttu-id="72774-108">This tutorial uses a simple Node.js simulated device to generate dynamic telemetry to send to the preconfigured solution back end.</span><span class="sxs-lookup"><span data-stu-id="72774-108">This tutorial uses a simple Node.js simulated device to generate dynamic telemetry to send to the preconfigured solution back end.</span></span> <span data-ttu-id="72774-109">You then add custom rules in the **RemoteMonitoring** Visual Studio solution and deploy this customized back end to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="72774-109">You then add custom rules in the **RemoteMonitoring** Visual Studio solution and deploy this customized back end to your Azure subscription.</span></span>

<span data-ttu-id="72774-110">To complete this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="72774-110">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="72774-111">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="72774-111">An active Azure subscription.</span></span> <span data-ttu-id="72774-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="72774-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="72774-113">For details, see [Azure Free Trial][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="72774-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="72774-114">[Node.js][lnk-node] version 0.12.x or later to create a simulated device.</span><span class="sxs-lookup"><span data-stu-id="72774-114">[Node.js][lnk-node] version 0.12.x or later to create a simulated device.</span></span>
* <span data-ttu-id="72774-115">Visual Studio 2015 or Visual Studio 2017 to modify the preconfigured solution back end with your new rules.</span><span class="sxs-lookup"><span data-stu-id="72774-115">Visual Studio 2015 or Visual Studio 2017 to modify the preconfigured solution back end with your new rules.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

<span data-ttu-id="72774-116">Make a note of the solution name you chose for your deployment.</span><span class="sxs-lookup"><span data-stu-id="72774-116">Make a note of the solution name you chose for your deployment.</span></span> <span data-ttu-id="72774-117">You need this solution name later in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="72774-117">You need this solution name later in this tutorial.</span></span>

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

<span data-ttu-id="72774-118">You can stop the Node.js console app when you have verified that it is sending **ExternalTemperature** telemetry to the preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="72774-118">You can stop the Node.js console app when you have verified that it is sending **ExternalTemperature** telemetry to the preconfigured solution.</span></span> <span data-ttu-id="72774-119">Keep the console window open because you run this Node.js console app again after you add the custom rule to the solution.</span><span class="sxs-lookup"><span data-stu-id="72774-119">Keep the console window open because you run this Node.js console app again after you add the custom rule to the solution.</span></span>

## <a name="rule-storage-locations"></a><span data-ttu-id="72774-120">Rule storage locations</span><span class="sxs-lookup"><span data-stu-id="72774-120">Rule storage locations</span></span>

<span data-ttu-id="72774-121">Information about rules is persisted in two locations:</span><span class="sxs-lookup"><span data-stu-id="72774-121">Information about rules is persisted in two locations:</span></span>

* <span data-ttu-id="72774-122">**DeviceRulesNormalizedTable** table – This table stores a normalized reference to the rules defined by the solution portal.</span><span class="sxs-lookup"><span data-stu-id="72774-122">**DeviceRulesNormalizedTable** table – This table stores a normalized reference to the rules defined by the solution portal.</span></span> <span data-ttu-id="72774-123">When the solution portal displays device rules, it queries this table for the rule definitions.</span><span class="sxs-lookup"><span data-stu-id="72774-123">When the solution portal displays device rules, it queries this table for the rule definitions.</span></span>
* <span data-ttu-id="72774-124">**DeviceRules** blob – This blob stores all the rules defined for all registered devices and is defined as a reference input to the Azure Stream Analytics jobs.</span><span class="sxs-lookup"><span data-stu-id="72774-124">**DeviceRules** blob – This blob stores all the rules defined for all registered devices and is defined as a reference input to the Azure Stream Analytics jobs.</span></span>
 
<span data-ttu-id="72774-125">When you update an existing rule or define a new rule in the solution portal, both the table and blob are updated to reflect the changes.</span><span class="sxs-lookup"><span data-stu-id="72774-125">When you update an existing rule or define a new rule in the solution portal, both the table and blob are updated to reflect the changes.</span></span> <span data-ttu-id="72774-126">The rule definition displayed in the portal comes from the table store, and the rule definition referenced by the Stream Analytics jobs comes from the blob.</span><span class="sxs-lookup"><span data-stu-id="72774-126">The rule definition displayed in the portal comes from the table store, and the rule definition referenced by the Stream Analytics jobs comes from the blob.</span></span> 

## <a name="update-the-remotemonitoring-visual-studio-solution"></a><span data-ttu-id="72774-127">Update the RemoteMonitoring Visual Studio solution</span><span class="sxs-lookup"><span data-stu-id="72774-127">Update the RemoteMonitoring Visual Studio solution</span></span>

<span data-ttu-id="72774-128">The following steps show you how to modify the RemoteMonitoring Visual Studio solution to include a new rule that uses the **ExternalTemperature** telemetry sent from the simulated device:</span><span class="sxs-lookup"><span data-stu-id="72774-128">The following steps show you how to modify the RemoteMonitoring Visual Studio solution to include a new rule that uses the **ExternalTemperature** telemetry sent from the simulated device:</span></span>

1. <span data-ttu-id="72774-129">If you have not already done so, clone the **azure-iot-remote-monitoring** repository to a suitable location on your local machine using the following Git command:</span><span class="sxs-lookup"><span data-stu-id="72774-129">If you have not already done so, clone the **azure-iot-remote-monitoring** repository to a suitable location on your local machine using the following Git command:</span></span>

    ```
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```

2. <span data-ttu-id="72774-130">In Visual Studio, open the RemoteMonitoring.sln file from your local copy of the **azure-iot-remote-monitoring** repository.</span><span class="sxs-lookup"><span data-stu-id="72774-130">In Visual Studio, open the RemoteMonitoring.sln file from your local copy of the **azure-iot-remote-monitoring** repository.</span></span>

3. <span data-ttu-id="72774-131">Open the file Infrastructure\Models\DeviceRuleBlobEntity.cs and add an **ExternalTemperature** property as follows:</span><span class="sxs-lookup"><span data-stu-id="72774-131">Open the file Infrastructure\Models\DeviceRuleBlobEntity.cs and add an **ExternalTemperature** property as follows:</span></span>

    ```csharp
    public double? Temperature { get; set; }
    public double? Humidity { get; set; }
    public double? ExternalTemperature { get; set; }
    ```

4. <span data-ttu-id="72774-132">In the same file, add an **ExternalTemperatureRuleOutput** property as follows:</span><span class="sxs-lookup"><span data-stu-id="72774-132">In the same file, add an **ExternalTemperatureRuleOutput** property as follows:</span></span>

    ```csharp
    public string TemperatureRuleOutput { get; set; }
    public string HumidityRuleOutput { get; set; }
    public string ExternalTemperatureRuleOutput { get; set; }
    ```

5. <span data-ttu-id="72774-133">Open the file Infrastructure\Models\DeviceRuleDataFields.cs and add the following **ExternalTemperature** property after the existing **Humidity** property:</span><span class="sxs-lookup"><span data-stu-id="72774-133">Open the file Infrastructure\Models\DeviceRuleDataFields.cs and add the following **ExternalTemperature** property after the existing **Humidity** property:</span></span>

    ```csharp
    public static string ExternalTemperature
    {
        get { return "ExternalTemperature"; }
    }
    ```

6. <span data-ttu-id="72774-134">In the same file, update the **_availableDataFields** method to include **ExternalTemperature** as follows:</span><span class="sxs-lookup"><span data-stu-id="72774-134">In the same file, update the **_availableDataFields** method to include **ExternalTemperature** as follows:</span></span>

    ```csharp
    private static List<string> _availableDataFields = new List<string>
    {                    
        Temperature, Humidity, ExternalTemperature
    };
    ```

7. <span data-ttu-id="72774-135">Open the file Infrastructure\Repository\DeviceRulesRepository.cs and modify the **BuildBlobEntityListFromTableRows** method as follows:</span><span class="sxs-lookup"><span data-stu-id="72774-135">Open the file Infrastructure\Repository\DeviceRulesRepository.cs and modify the **BuildBlobEntityListFromTableRows** method as follows:</span></span>

    ```csharp
    else if (rule.DataField == DeviceRuleDataFields.Humidity)
    {
        entity.Humidity = rule.Threshold;
        entity.HumidityRuleOutput = rule.RuleOutput;
    }
    else if (rule.DataField == DeviceRuleDataFields.ExternalTemperature)
    {
      entity.ExternalTemperature = rule.Threshold;
      entity.ExternalTemperatureRuleOutput = rule.RuleOutput;
    }
    ```

## <a name="rebuild-and-redeploy-the-solution"></a><span data-ttu-id="72774-136">Rebuild and redeploy the solution.</span><span class="sxs-lookup"><span data-stu-id="72774-136">Rebuild and redeploy the solution.</span></span>

<span data-ttu-id="72774-137">You can now deploy the updated solution to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="72774-137">You can now deploy the updated solution to your Azure subscription.</span></span>

1. <span data-ttu-id="72774-138">Open an elevated command prompt and navigate to the root of your local copy of the azure-iot-remote-monitoring repository.</span><span class="sxs-lookup"><span data-stu-id="72774-138">Open an elevated command prompt and navigate to the root of your local copy of the azure-iot-remote-monitoring repository.</span></span>

2. <span data-ttu-id="72774-139">To deploy your updated solution, run the following command substituting **{deployment name}** with the name of your preconfigured solution deployment that you noted previously:</span><span class="sxs-lookup"><span data-stu-id="72774-139">To deploy your updated solution, run the following command substituting **{deployment name}** with the name of your preconfigured solution deployment that you noted previously:</span></span>

    ```
    build.cmd cloud release {deployment name}
    ```

## <a name="update-the-stream-analytics-job"></a><span data-ttu-id="72774-140">Update the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="72774-140">Update the Stream Analytics job</span></span>

<span data-ttu-id="72774-141">When the deployment is complete, you can update the Stream Analytics job to use the new rule definitions.</span><span class="sxs-lookup"><span data-stu-id="72774-141">When the deployment is complete, you can update the Stream Analytics job to use the new rule definitions.</span></span>

1. <span data-ttu-id="72774-142">In the Azure portal, navigate to the resource group that contains your preconfigured solution resources.</span><span class="sxs-lookup"><span data-stu-id="72774-142">In the Azure portal, navigate to the resource group that contains your preconfigured solution resources.</span></span> <span data-ttu-id="72774-143">This resource group has the same name you specified for the solution during the deployment.</span><span class="sxs-lookup"><span data-stu-id="72774-143">This resource group has the same name you specified for the solution during the deployment.</span></span>

2. <span data-ttu-id="72774-144">Navigate to the {deployment name}-Rules Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="72774-144">Navigate to the {deployment name}-Rules Stream Analytics job.</span></span> 

3. <span data-ttu-id="72774-145">Click **Stop** to stop the Stream Analytics job from running.</span><span class="sxs-lookup"><span data-stu-id="72774-145">Click **Stop** to stop the Stream Analytics job from running.</span></span> <span data-ttu-id="72774-146">(You must wait for the streaming job to stop before you can edit the query).</span><span class="sxs-lookup"><span data-stu-id="72774-146">(You must wait for the streaming job to stop before you can edit the query).</span></span>

4. <span data-ttu-id="72774-147">Click **Query**.</span><span class="sxs-lookup"><span data-stu-id="72774-147">Click **Query**.</span></span> <span data-ttu-id="72774-148">Edit the query to include the **SELECT** statement for **ExternalTemperature**.</span><span class="sxs-lookup"><span data-stu-id="72774-148">Edit the query to include the **SELECT** statement for **ExternalTemperature**.</span></span> <span data-ttu-id="72774-149">The following sample shows the complete query with the new **SELECT** statement:</span><span class="sxs-lookup"><span data-stu-id="72774-149">The following sample shows the complete query with the new **SELECT** statement:</span></span>

    ```
    WITH AlarmsData AS 
    (
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'Temperature' as ReadingType,
         Stream.Temperature as Reading,
         Ref.Temperature as Threshold,
         Ref.TemperatureRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature
     
    UNION ALL
     
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'Humidity' as ReadingType,
         Stream.Humidity as Reading,
         Ref.Humidity as Threshold,
         Ref.HumidityRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
     
    UNION ALL
     
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'ExternalTemperature' as ReadingType,
         Stream.ExternalTemperature as Reading,
         Ref.ExternalTemperature as Threshold,
         Ref.ExternalTemperatureRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.ExternalTemperature IS NOT null AND Stream.ExternalTemperature > Ref.ExternalTemperature
    )
     
    SELECT *
    INTO DeviceRulesMonitoring
    FROM AlarmsData
     
    SELECT *
    INTO DeviceRulesHub
    FROM AlarmsData
    ```

5. <span data-ttu-id="72774-150">Click **Save** to change the updated rule query.</span><span class="sxs-lookup"><span data-stu-id="72774-150">Click **Save** to change the updated rule query.</span></span>

6. <span data-ttu-id="72774-151">Click **Start** to start the Stream Analytics job running again.</span><span class="sxs-lookup"><span data-stu-id="72774-151">Click **Start** to start the Stream Analytics job running again.</span></span>

## <a name="add-your-new-rule-in-the-dashboard"></a><span data-ttu-id="72774-152">Add your new rule in the dashboard</span><span class="sxs-lookup"><span data-stu-id="72774-152">Add your new rule in the dashboard</span></span>

<span data-ttu-id="72774-153">You can now add the **ExternalTemperature** rule to a device in the solution dashboard.</span><span class="sxs-lookup"><span data-stu-id="72774-153">You can now add the **ExternalTemperature** rule to a device in the solution dashboard.</span></span>

1. <span data-ttu-id="72774-154">Navigate to the solution portal.</span><span class="sxs-lookup"><span data-stu-id="72774-154">Navigate to the solution portal.</span></span>

2. <span data-ttu-id="72774-155">Navigate to the **Devices** panel.</span><span class="sxs-lookup"><span data-stu-id="72774-155">Navigate to the **Devices** panel.</span></span>

3. <span data-ttu-id="72774-156">Locate the custom device you created that sends **ExternalTemperature** telemetry and on the **Device Details** panel, click **Add Rule**.</span><span class="sxs-lookup"><span data-stu-id="72774-156">Locate the custom device you created that sends **ExternalTemperature** telemetry and on the **Device Details** panel, click **Add Rule**.</span></span>

4. <span data-ttu-id="72774-157">Select **ExternalTemperature** in **Data Field**.</span><span class="sxs-lookup"><span data-stu-id="72774-157">Select **ExternalTemperature** in **Data Field**.</span></span>

5. <span data-ttu-id="72774-158">Set **Threshold** to 56.</span><span class="sxs-lookup"><span data-stu-id="72774-158">Set **Threshold** to 56.</span></span> <span data-ttu-id="72774-159">Then click **Save and view rules**.</span><span class="sxs-lookup"><span data-stu-id="72774-159">Then click **Save and view rules**.</span></span>

6. <span data-ttu-id="72774-160">Return to the dashboard to view the alarm history.</span><span class="sxs-lookup"><span data-stu-id="72774-160">Return to the dashboard to view the alarm history.</span></span>

7. <span data-ttu-id="72774-161">In the console window you left open, start the Node.js console app to begin sending **ExternalTemperature** telemetry data.</span><span class="sxs-lookup"><span data-stu-id="72774-161">In the console window you left open, start the Node.js console app to begin sending **ExternalTemperature** telemetry data.</span></span>

8. <span data-ttu-id="72774-162">Notice that the **Alarm History** table shows new alarms when the new rule is triggered.</span><span class="sxs-lookup"><span data-stu-id="72774-162">Notice that the **Alarm History** table shows new alarms when the new rule is triggered.</span></span>
 
## <a name="additional-information"></a><span data-ttu-id="72774-163">Additional information</span><span class="sxs-lookup"><span data-stu-id="72774-163">Additional information</span></span>

<span data-ttu-id="72774-164">Changing the operator **>** is more complex and goes beyond the steps outlined in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="72774-164">Changing the operator **>** is more complex and goes beyond the steps outlined in this tutorial.</span></span> <span data-ttu-id="72774-165">While you can change the Stream Analytics job to use whatever operator you like, reflecting that operator in the solution portal is a more complex task.</span><span class="sxs-lookup"><span data-stu-id="72774-165">While you can change the Stream Analytics job to use whatever operator you like, reflecting that operator in the solution portal is a more complex task.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="72774-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="72774-166">Next steps</span></span>
<span data-ttu-id="72774-167">Now that you've seen how to create custom rules, you can learn more about the preconfigured solutions:</span><span class="sxs-lookup"><span data-stu-id="72774-167">Now that you've seen how to create custom rules, you can learn more about the preconfigured solutions:</span></span>

- <span data-ttu-id="72774-168">[Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logic-app]</span><span class="sxs-lookup"><span data-stu-id="72774-168">[Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logic-app]</span></span>
- <span data-ttu-id="72774-169">[Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="72774-169">[Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
[lnk-builtin-rule]: iot-suite-getstarted-preconfigured-solutions.md#view-alarms
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md
[lnk-logic-app]: iot-suite-logic-apps-tutorial.md