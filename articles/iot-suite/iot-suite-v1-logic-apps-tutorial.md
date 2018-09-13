---
title: Azure IoT Suite and Logic Apps | Microsoft Docs
description: A tutorial on how to hook up Logic Apps to Azure IoT Suite for business process.
services: ''
suite: iot-suite
documentationcenter: ''
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: 4629a7af-56ca-4b21-a769-5fa18bc3ab07
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/02/2017
ms.author: corywink
ms.openlocfilehash: 4a1db86f4b715533dfea545365eaf66de0574c5e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967324"
---
# <a name="tutorial-connect-logic-app-to-your-azure-iot-suite-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="cb14a-103">Tutorial: Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution</span><span class="sxs-lookup"><span data-stu-id="cb14a-103">Tutorial: Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution</span></span>
<span data-ttu-id="cb14a-104">The [Microsoft Azure IoT Suite][lnk-internetofthings] remote monitoring preconfigured solution is a great way to get started quickly with an end-to-end feature set that exemplifies an IoT solution.</span><span class="sxs-lookup"><span data-stu-id="cb14a-104">The [Microsoft Azure IoT Suite][lnk-internetofthings] remote monitoring preconfigured solution is a great way to get started quickly with an end-to-end feature set that exemplifies an IoT solution.</span></span> <span data-ttu-id="cb14a-105">This tutorial walks you through how to add Logic App to your Microsoft Azure IoT Suite remote monitoring preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="cb14a-105">This tutorial walks you through how to add Logic App to your Microsoft Azure IoT Suite remote monitoring preconfigured solution.</span></span> <span data-ttu-id="cb14a-106">These steps demonstrate how you can take your IoT solution even further by connecting it to a business process.</span><span class="sxs-lookup"><span data-stu-id="cb14a-106">These steps demonstrate how you can take your IoT solution even further by connecting it to a business process.</span></span>

<span data-ttu-id="cb14a-107">*If you’re looking for a walkthrough on how to provision a remote monitoring preconfigured solution, see [Tutorial: Get started with the IoT preconfigured solutions][lnk-getstarted].*</span><span class="sxs-lookup"><span data-stu-id="cb14a-107">*If you’re looking for a walkthrough on how to provision a remote monitoring preconfigured solution, see [Tutorial: Get started with the IoT preconfigured solutions][lnk-getstarted].*</span></span>

<span data-ttu-id="cb14a-108">Before you start this tutorial, you should:</span><span class="sxs-lookup"><span data-stu-id="cb14a-108">Before you start this tutorial, you should:</span></span>

* <span data-ttu-id="cb14a-109">Provision the remote monitoring preconfigured solution in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="cb14a-109">Provision the remote monitoring preconfigured solution in your Azure subscription.</span></span>
* <span data-ttu-id="cb14a-110">Create a SendGrid account to enable you to send an email that triggers your business process.</span><span class="sxs-lookup"><span data-stu-id="cb14a-110">Create a SendGrid account to enable you to send an email that triggers your business process.</span></span> <span data-ttu-id="cb14a-111">You can sign up for a free trial account at [SendGrid](https://sendgrid.com/) by clicking **Try for Free**.</span><span class="sxs-lookup"><span data-stu-id="cb14a-111">You can sign up for a free trial account at [SendGrid](https://sendgrid.com/) by clicking **Try for Free**.</span></span> <span data-ttu-id="cb14a-112">After you have registered for your free trial account, you need to create an [API key](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) in SendGrid that grants permissions to send mail.</span><span class="sxs-lookup"><span data-stu-id="cb14a-112">After you have registered for your free trial account, you need to create an [API key](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) in SendGrid that grants permissions to send mail.</span></span> <span data-ttu-id="cb14a-113">You need this API key later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="cb14a-113">You need this API key later in the tutorial.</span></span>

<span data-ttu-id="cb14a-114">To complete this tutorial, you need Visual Studio 2015 or Visual Studio 2017 to modify the actions in the preconfigured solution back end.</span><span class="sxs-lookup"><span data-stu-id="cb14a-114">To complete this tutorial, you need Visual Studio 2015 or Visual Studio 2017 to modify the actions in the preconfigured solution back end.</span></span>

<span data-ttu-id="cb14a-115">Assuming you’ve already provisioned your remote monitoring preconfigured solution, navigate to the resource group for that solution in the [Azure portal][lnk-azureportal].</span><span class="sxs-lookup"><span data-stu-id="cb14a-115">Assuming you’ve already provisioned your remote monitoring preconfigured solution, navigate to the resource group for that solution in the [Azure portal][lnk-azureportal].</span></span> <span data-ttu-id="cb14a-116">The resource group has the same name as the solution name you chose when you provisioned your remote monitoring solution.</span><span class="sxs-lookup"><span data-stu-id="cb14a-116">The resource group has the same name as the solution name you chose when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="cb14a-117">In the resource group, you can see all the provisioned Azure resources for your solution.</span><span class="sxs-lookup"><span data-stu-id="cb14a-117">In the resource group, you can see all the provisioned Azure resources for your solution.</span></span> <span data-ttu-id="cb14a-118">The following screenshot shows an example **Resource group** blade for a remote monitoring preconfigured solution:</span><span class="sxs-lookup"><span data-stu-id="cb14a-118">The following screenshot shows an example **Resource group** blade for a remote monitoring preconfigured solution:</span></span>

![](media/iot-suite-v1-logic-apps-tutorial/resourcegroup.png)

<span data-ttu-id="cb14a-119">To begin, set up the logic app to use with the preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="cb14a-119">To begin, set up the logic app to use with the preconfigured solution.</span></span>

## <a name="set-up-the-logic-app"></a><span data-ttu-id="cb14a-120">Set up the Logic App</span><span class="sxs-lookup"><span data-stu-id="cb14a-120">Set up the Logic App</span></span>
1. <span data-ttu-id="cb14a-121">Click **Add** at the top of your resource group blade in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cb14a-121">Click **Add** at the top of your resource group blade in the Azure portal.</span></span>
2. <span data-ttu-id="cb14a-122">Search for **Logic App**, select it and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="cb14a-122">Search for **Logic App**, select it and then click **Create**.</span></span>
3. <span data-ttu-id="cb14a-123">Fill out the **Name** and use the same **Subscription** and **Resource group** that you used when you provisioned your remote monitoring solution.</span><span class="sxs-lookup"><span data-stu-id="cb14a-123">Fill out the **Name** and use the same **Subscription** and **Resource group** that you used when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="cb14a-124">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="cb14a-124">Click **Create**.</span></span>
   
    ![](media/iot-suite-v1-logic-apps-tutorial/createlogicapp.png)
4. <span data-ttu-id="cb14a-125">When your deployment completes, you can see the Logic App is listed as a resource in your resource group.</span><span class="sxs-lookup"><span data-stu-id="cb14a-125">When your deployment completes, you can see the Logic App is listed as a resource in your resource group.</span></span>
5. <span data-ttu-id="cb14a-126">Click the Logic App to navigate to the Logic App blade, select the **Blank Logic App** template to open the **Logic Apps Designer**.</span><span class="sxs-lookup"><span data-stu-id="cb14a-126">Click the Logic App to navigate to the Logic App blade, select the **Blank Logic App** template to open the **Logic Apps Designer**.</span></span>
   
    ![](media/iot-suite-v1-logic-apps-tutorial/logicappsdesigner.png)
6. <span data-ttu-id="cb14a-127">Select **Request**.</span><span class="sxs-lookup"><span data-stu-id="cb14a-127">Select **Request**.</span></span> <span data-ttu-id="cb14a-128">This action specifies that an incoming HTTP request with a specific JSON formatted payload acts as a trigger.</span><span class="sxs-lookup"><span data-stu-id="cb14a-128">This action specifies that an incoming HTTP request with a specific JSON formatted payload acts as a trigger.</span></span>
7. <span data-ttu-id="cb14a-129">Paste the following code into the Request Body JSON Schema:</span><span class="sxs-lookup"><span data-stu-id="cb14a-129">Paste the following code into the Request Body JSON Schema:</span></span>
   
    ```json
    {
      "$schema": "http://json-schema.org/draft-04/schema#",
      "id": "/",
      "properties": {
        "DeviceId": {
          "id": "DeviceId",
          "type": "string"
        },
        "measuredValue": {
          "id": "measuredValue",
          "type": "integer"
        },
        "measurementName": {
          "id": "measurementName",
          "type": "string"
        }
      },
      "required": [
        "DeviceId",
        "measurementName",
        "measuredValue"
      ],
      "type": "object"
    }
    ```
   
   > [!NOTE]
   > <span data-ttu-id="cb14a-130">You can copy the URL for the HTTP post after you save the logic app, but first you must add an action.</span><span class="sxs-lookup"><span data-stu-id="cb14a-130">You can copy the URL for the HTTP post after you save the logic app, but first you must add an action.</span></span>
   > 
   > 
8. <span data-ttu-id="cb14a-131">Click **+ New step** under your manual trigger.</span><span class="sxs-lookup"><span data-stu-id="cb14a-131">Click **+ New step** under your manual trigger.</span></span> <span data-ttu-id="cb14a-132">Then click **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="cb14a-132">Then click **Add an action**.</span></span>
   
    ![](media/iot-suite-v1-logic-apps-tutorial/logicappcode.png)
9. <span data-ttu-id="cb14a-133">Search for **SendGrid - Send email** and click it.</span><span class="sxs-lookup"><span data-stu-id="cb14a-133">Search for **SendGrid - Send email** and click it.</span></span>
   
    ![](media/iot-suite-v1-logic-apps-tutorial/logicappaction.png)
10. <span data-ttu-id="cb14a-134">Enter a name for the connection, such as **SendGridConnection**, enter the **SendGrid API Key** you created when you set up your SendGrid account, and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="cb14a-134">Enter a name for the connection, such as **SendGridConnection**, enter the **SendGrid API Key** you created when you set up your SendGrid account, and click **Create**.</span></span>
    
    ![](media/iot-suite-v1-logic-apps-tutorial/sendgridconnection.png)
11. <span data-ttu-id="cb14a-135">Add email addresses you own to both the **From** and **To** fields.</span><span class="sxs-lookup"><span data-stu-id="cb14a-135">Add email addresses you own to both the **From** and **To** fields.</span></span> <span data-ttu-id="cb14a-136">Add **Remote monitoring alert [DeviceId]** to the **Subject** field.</span><span class="sxs-lookup"><span data-stu-id="cb14a-136">Add **Remote monitoring alert [DeviceId]** to the **Subject** field.</span></span> <span data-ttu-id="cb14a-137">In the **Email Body** field, add **Device [DeviceId] has reported [measurementName] with value [measuredValue].**</span><span class="sxs-lookup"><span data-stu-id="cb14a-137">In the **Email Body** field, add **Device [DeviceId] has reported [measurementName] with value [measuredValue].**</span></span> <span data-ttu-id="cb14a-138">You can add **[DeviceId]**, **[measurementName]**, and **[measuredValue]** by clicking in the **You can insert data from previous steps** section.</span><span class="sxs-lookup"><span data-stu-id="cb14a-138">You can add **[DeviceId]**, **[measurementName]**, and **[measuredValue]** by clicking in the **You can insert data from previous steps** section.</span></span>
    
    ![](media/iot-suite-v1-logic-apps-tutorial/sendgridaction.png)
12. <span data-ttu-id="cb14a-139">Click **Save** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="cb14a-139">Click **Save** in the top menu.</span></span>
13. <span data-ttu-id="cb14a-140">Click the **Request** trigger and copy the **Http Post to this URL** value.</span><span class="sxs-lookup"><span data-stu-id="cb14a-140">Click the **Request** trigger and copy the **Http Post to this URL** value.</span></span> <span data-ttu-id="cb14a-141">You need this URL later in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="cb14a-141">You need this URL later in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="cb14a-142">Logic Apps enable you to run [many different types of action][lnk-logic-apps-actions] including actions in Office 365.</span><span class="sxs-lookup"><span data-stu-id="cb14a-142">Logic Apps enable you to run [many different types of action][lnk-logic-apps-actions] including actions in Office 365.</span></span> 
> 
> 

## <a name="set-up-the-eventprocessor-web-job"></a><span data-ttu-id="cb14a-143">Set up the EventProcessor Web Job</span><span class="sxs-lookup"><span data-stu-id="cb14a-143">Set up the EventProcessor Web Job</span></span>
<span data-ttu-id="cb14a-144">In this section, you connect your preconfigured solution to the Logic App you created.</span><span class="sxs-lookup"><span data-stu-id="cb14a-144">In this section, you connect your preconfigured solution to the Logic App you created.</span></span> <span data-ttu-id="cb14a-145">To complete this task, you add the URL to trigger the Logic App to the action that fires when a device sensor value exceeds a threshold.</span><span class="sxs-lookup"><span data-stu-id="cb14a-145">To complete this task, you add the URL to trigger the Logic App to the action that fires when a device sensor value exceeds a threshold.</span></span>

1. <span data-ttu-id="cb14a-146">Use your git client to clone the latest version of the [azure-iot-remote-monitoring github repository][lnk-rmgithub].</span><span class="sxs-lookup"><span data-stu-id="cb14a-146">Use your git client to clone the latest version of the [azure-iot-remote-monitoring github repository][lnk-rmgithub].</span></span> <span data-ttu-id="cb14a-147">For example:</span><span class="sxs-lookup"><span data-stu-id="cb14a-147">For example:</span></span>
   
    ```cmd
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```
2. <span data-ttu-id="cb14a-148">In Visual Studio, open the **RemoteMonitoring.sln** from the local copy of the repository.</span><span class="sxs-lookup"><span data-stu-id="cb14a-148">In Visual Studio, open the **RemoteMonitoring.sln** from the local copy of the repository.</span></span>
3. <span data-ttu-id="cb14a-149">Open the **ActionRepository.cs** file in the **Infrastructure\\Repository** folder.</span><span class="sxs-lookup"><span data-stu-id="cb14a-149">Open the **ActionRepository.cs** file in the **Infrastructure\\Repository** folder.</span></span>
4. <span data-ttu-id="cb14a-150">Update the **actionIds** dictionary with the **Http Post to this URL** you noted from your Logic App as follows:</span><span class="sxs-lookup"><span data-stu-id="cb14a-150">Update the **actionIds** dictionary with the **Http Post to this URL** you noted from your Logic App as follows:</span></span>
   
    ```csharp
    private Dictionary<string,string> actionIds = new Dictionary<string, string>()
    {
        { "Send Message", "<Http Post to this URL>" },
        { "Raise Alarm", "<Http Post to this URL>" }
    };
    ```
5. <span data-ttu-id="cb14a-151">Save the changes in solution and exit Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cb14a-151">Save the changes in solution and exit Visual Studio.</span></span>

## <a name="deploy-from-the-command-line"></a><span data-ttu-id="cb14a-152">Deploy from the command line</span><span class="sxs-lookup"><span data-stu-id="cb14a-152">Deploy from the command line</span></span>
<span data-ttu-id="cb14a-153">In this section, you deploy your updated version of the remote monitoring solution to replace the version currently running in Azure.</span><span class="sxs-lookup"><span data-stu-id="cb14a-153">In this section, you deploy your updated version of the remote monitoring solution to replace the version currently running in Azure.</span></span>

1. <span data-ttu-id="cb14a-154">Following the [dev set-up][lnk-devsetup] instructions to set up your environment for deployment.</span><span class="sxs-lookup"><span data-stu-id="cb14a-154">Following the [dev set-up][lnk-devsetup] instructions to set up your environment for deployment.</span></span>
2. <span data-ttu-id="cb14a-155">To deploy locally, follow the [local deployment][lnk-localdeploy] instructions.</span><span class="sxs-lookup"><span data-stu-id="cb14a-155">To deploy locally, follow the [local deployment][lnk-localdeploy] instructions.</span></span>
3. <span data-ttu-id="cb14a-156">To deploy to the cloud and update your existing cloud deployment, follow the [cloud deployment][lnk-clouddeploy] instructions.</span><span class="sxs-lookup"><span data-stu-id="cb14a-156">To deploy to the cloud and update your existing cloud deployment, follow the [cloud deployment][lnk-clouddeploy] instructions.</span></span> <span data-ttu-id="cb14a-157">Use the name of your original deployment as the deployment name.</span><span class="sxs-lookup"><span data-stu-id="cb14a-157">Use the name of your original deployment as the deployment name.</span></span> <span data-ttu-id="cb14a-158">For example if the original deployment was called **demologicapp**, use the following command:</span><span class="sxs-lookup"><span data-stu-id="cb14a-158">For example if the original deployment was called **demologicapp**, use the following command:</span></span>
   
   ```cmd
   build.cmd cloud release demologicapp
   ```
   
   <span data-ttu-id="cb14a-159">When the build script runs, be sure to use the same Azure account, subscription, region, and Active Directory instance you used when you provisioned the solution.</span><span class="sxs-lookup"><span data-stu-id="cb14a-159">When the build script runs, be sure to use the same Azure account, subscription, region, and Active Directory instance you used when you provisioned the solution.</span></span>

## <a name="see-your-logic-app-in-action"></a><span data-ttu-id="cb14a-160">See your Logic App in action</span><span class="sxs-lookup"><span data-stu-id="cb14a-160">See your Logic App in action</span></span>
<span data-ttu-id="cb14a-161">The remote monitoring preconfigured solution has two rules set up by default when you provision a solution.</span><span class="sxs-lookup"><span data-stu-id="cb14a-161">The remote monitoring preconfigured solution has two rules set up by default when you provision a solution.</span></span> <span data-ttu-id="cb14a-162">Both rules are on the **SampleDevice001** device:</span><span class="sxs-lookup"><span data-stu-id="cb14a-162">Both rules are on the **SampleDevice001** device:</span></span>

* <span data-ttu-id="cb14a-163">Temperature > 38.00</span><span class="sxs-lookup"><span data-stu-id="cb14a-163">Temperature > 38.00</span></span>
* <span data-ttu-id="cb14a-164">Humidity > 48.00</span><span class="sxs-lookup"><span data-stu-id="cb14a-164">Humidity > 48.00</span></span>

<span data-ttu-id="cb14a-165">The temperature rule triggers the **Raise Alarm** action and the Humidity rule triggers the **SendMessage** action.</span><span class="sxs-lookup"><span data-stu-id="cb14a-165">The temperature rule triggers the **Raise Alarm** action and the Humidity rule triggers the **SendMessage** action.</span></span> <span data-ttu-id="cb14a-166">Assuming you used the same URL for both actions the **ActionRepository** class, your logic app triggers for either rule.</span><span class="sxs-lookup"><span data-stu-id="cb14a-166">Assuming you used the same URL for both actions the **ActionRepository** class, your logic app triggers for either rule.</span></span> <span data-ttu-id="cb14a-167">Both rules use SendGrid to send an email to the **To** address with details of the alert.</span><span class="sxs-lookup"><span data-stu-id="cb14a-167">Both rules use SendGrid to send an email to the **To** address with details of the alert.</span></span>

> [!NOTE]
> <span data-ttu-id="cb14a-168">The Logic App continues to trigger every time the threshold is met.</span><span class="sxs-lookup"><span data-stu-id="cb14a-168">The Logic App continues to trigger every time the threshold is met.</span></span> <span data-ttu-id="cb14a-169">To avoid unnecessary emails, you can either disable the rules in your solution portal or disable the Logic App in the [Azure portal][lnk-azureportal].</span><span class="sxs-lookup"><span data-stu-id="cb14a-169">To avoid unnecessary emails, you can either disable the rules in your solution portal or disable the Logic App in the [Azure portal][lnk-azureportal].</span></span>
> 
> 

<span data-ttu-id="cb14a-170">In addition to receiving emails, you can also see when the Logic App runs in the portal:</span><span class="sxs-lookup"><span data-stu-id="cb14a-170">In addition to receiving emails, you can also see when the Logic App runs in the portal:</span></span>

![](media/iot-suite-v1-logic-apps-tutorial/logicapprun.png)

## <a name="next-steps"></a><span data-ttu-id="cb14a-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="cb14a-171">Next steps</span></span>
<span data-ttu-id="cb14a-172">Now that you've used a Logic App to connect the preconfigured solution to a business process, you can learn more about the options for customizing the preconfigured solutions:</span><span class="sxs-lookup"><span data-stu-id="cb14a-172">Now that you've used a Logic App to connect the preconfigured solution to a business process, you can learn more about the options for customizing the preconfigured solutions:</span></span>

* <span data-ttu-id="cb14a-173">[Use dynamic telemetry with the remote monitoring preconfigured solution][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="cb14a-173">[Use dynamic telemetry with the remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="cb14a-174">[Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="cb14a-174">[Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo]</span></span>

[lnk-dynamic]: iot-suite-v1-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-v1-remote-monitoring-device-info.md

[lnk-internetofthings]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-getstarted]: iot-suite-v1-getstarted-preconfigured-solutions.md
[lnk-azureportal]: https://portal.azure.com
[lnk-logic-apps-actions]: ../connectors/apis-list.md
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-devsetup]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/dev-setup.md
[lnk-localdeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/local-deployment.md
[lnk-clouddeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
