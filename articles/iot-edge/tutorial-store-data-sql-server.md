---
title: Store data with Azure IoT Edge SQL module | Microsoft Docs
description: Learn how to store data locally on your IoT Edge device with a SQL Server module
services: iot-edge
author: kgremban
manager: timlt
ms.author: kgremban
ms.date: 08/30/2018
ms.topic: tutorial
ms.service: iot-edge
ms.custom: mvc
ms.openlocfilehash: 2b393a5b60ba534fba8115ab3ef0f35a26ad3ed4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865282"
---
# <a name="tutorial-store-data-at-the-edge-with-sql-server-databases"></a><span data-ttu-id="979f3-103">Tutorial: Store data at the edge with SQL Server databases</span><span class="sxs-lookup"><span data-stu-id="979f3-103">Tutorial: Store data at the edge with SQL Server databases</span></span>

<span data-ttu-id="979f3-104">Use Azure IoT Edge and SQL Server to store and query data at the edge.</span><span class="sxs-lookup"><span data-stu-id="979f3-104">Use Azure IoT Edge and SQL Server to store and query data at the edge.</span></span> <span data-ttu-id="979f3-105">Azure IoT Edge comes built-in with basic storage features that cache messages if a device goes offline and then forwards them when the connection is reestablished.</span><span class="sxs-lookup"><span data-stu-id="979f3-105">Azure IoT Edge comes built-in with basic storage features that cache messages if a device goes offline and then forwards them when the connection is reestablished.</span></span> <span data-ttu-id="979f3-106">However, you may want more advanced storage capabilities, like being able to query data locally.</span><span class="sxs-lookup"><span data-stu-id="979f3-106">However, you may want more advanced storage capabilities, like being able to query data locally.</span></span> <span data-ttu-id="979f3-107">By incorporating local databases, your IoT Edge devices can perform more complex computing without having to maintain a connection to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="979f3-107">By incorporating local databases, your IoT Edge devices can perform more complex computing without having to maintain a connection to IoT Hub.</span></span> <span data-ttu-id="979f3-108">For example, a field technician can visualize the last few days of sensor data on a machine locally, even though that data is only uploaded to the cloud once a month to help improve a machine learning model.</span><span class="sxs-lookup"><span data-stu-id="979f3-108">For example, a field technician can visualize the last few days of sensor data on a machine locally, even though that data is only uploaded to the cloud once a month to help improve a machine learning model.</span></span>

<span data-ttu-id="979f3-109">This article provides instructions for deploying a SQL Server database to an IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="979f3-109">This article provides instructions for deploying a SQL Server database to an IoT Edge device.</span></span> <span data-ttu-id="979f3-110">Azure Functions, running on the IoT Edge device, structures the incoming data then sends it to the database.</span><span class="sxs-lookup"><span data-stu-id="979f3-110">Azure Functions, running on the IoT Edge device, structures the incoming data then sends it to the database.</span></span> <span data-ttu-id="979f3-111">The steps in this article can also be applied to other databases that work in containers, like MySQL or PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="979f3-111">The steps in this article can also be applied to other databases that work in containers, like MySQL or PostgreSQL.</span></span>

<span data-ttu-id="979f3-112">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="979f3-112">In this tutorial, you learn how to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="979f3-113">Use Visual Studio Code to create an Azure Function</span><span class="sxs-lookup"><span data-stu-id="979f3-113">Use Visual Studio Code to create an Azure Function</span></span>
> * <span data-ttu-id="979f3-114">Deploy a SQL database to your IoT Edge device</span><span class="sxs-lookup"><span data-stu-id="979f3-114">Deploy a SQL database to your IoT Edge device</span></span>
> * <span data-ttu-id="979f3-115">Use Visual Studio Code to build modules and deploy them to your IoT Edge device</span><span class="sxs-lookup"><span data-stu-id="979f3-115">Use Visual Studio Code to build modules and deploy them to your IoT Edge device</span></span>
> * <span data-ttu-id="979f3-116">View generated data</span><span class="sxs-lookup"><span data-stu-id="979f3-116">View generated data</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="979f3-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="979f3-117">Prerequisites</span></span>

<span data-ttu-id="979f3-118">An Azure IoT Edge device:</span><span class="sxs-lookup"><span data-stu-id="979f3-118">An Azure IoT Edge device:</span></span>

* <span data-ttu-id="979f3-119">You can use your development machine or a virtual machine as an Edge device by following the steps in the quickstart for [Linux](quickstart-linux.md) or [Windows devices](quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="979f3-119">You can use your development machine or a virtual machine as an Edge device by following the steps in the quickstart for [Linux](quickstart-linux.md) or [Windows devices](quickstart.md).</span></span>

<span data-ttu-id="979f3-120">Cloud resources:</span><span class="sxs-lookup"><span data-stu-id="979f3-120">Cloud resources:</span></span>

* <span data-ttu-id="979f3-121">A standard-tier [IoT Hub](../iot-hub/iot-hub-create-through-portal.md) in Azure.</span><span class="sxs-lookup"><span data-stu-id="979f3-121">A standard-tier [IoT Hub](../iot-hub/iot-hub-create-through-portal.md) in Azure.</span></span> 

<span data-ttu-id="979f3-122">Development resources:</span><span class="sxs-lookup"><span data-stu-id="979f3-122">Development resources:</span></span>

* <span data-ttu-id="979f3-123">[Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="979f3-123">[Visual Studio Code](https://code.visualstudio.com/).</span></span> 
* <span data-ttu-id="979f3-124">[C# for Visual Studio Code (powered by OmniSharp)](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) extension for Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="979f3-124">[C# for Visual Studio Code (powered by OmniSharp)](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) extension for Visual Studio Code.</span></span> 
* <span data-ttu-id="979f3-125">[Azure IoT Edge](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-edge) extension for Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="979f3-125">[Azure IoT Edge](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-edge) extension for Visual Studio Code.</span></span> 
* <span data-ttu-id="979f3-126">[.NET Core 2.1 SDK](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="979f3-126">[.NET Core 2.1 SDK](https://www.microsoft.com/net/download).</span></span> 
* <span data-ttu-id="979f3-127">[Docker CE](https://docs.docker.com/install/).</span><span class="sxs-lookup"><span data-stu-id="979f3-127">[Docker CE](https://docs.docker.com/install/).</span></span> 

## <a name="create-a-container-registry"></a><span data-ttu-id="979f3-128">Create a container registry</span><span class="sxs-lookup"><span data-stu-id="979f3-128">Create a container registry</span></span>
<span data-ttu-id="979f3-129">In this tutorial, you use the Azure IoT Edge extension for VS Code to build a module and create a **container image** from the files.</span><span class="sxs-lookup"><span data-stu-id="979f3-129">In this tutorial, you use the Azure IoT Edge extension for VS Code to build a module and create a **container image** from the files.</span></span> <span data-ttu-id="979f3-130">Then you push this image to a **registry** that stores and manages your images.</span><span class="sxs-lookup"><span data-stu-id="979f3-130">Then you push this image to a **registry** that stores and manages your images.</span></span> <span data-ttu-id="979f3-131">Finally, you deploy your image from your registry to run on your IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="979f3-131">Finally, you deploy your image from your registry to run on your IoT Edge device.</span></span>  

<span data-ttu-id="979f3-132">You can use any Docker-compatible registry for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="979f3-132">You can use any Docker-compatible registry for this tutorial.</span></span> <span data-ttu-id="979f3-133">Two popular Docker registry services available in the cloud are [Azure Container Registry](https://docs.microsoft.com/azure/container-registry/) and [Docker Hub](https://docs.docker.com/docker-hub/repos/#viewing-repository-tags).</span><span class="sxs-lookup"><span data-stu-id="979f3-133">Two popular Docker registry services available in the cloud are [Azure Container Registry](https://docs.microsoft.com/azure/container-registry/) and [Docker Hub](https://docs.docker.com/docker-hub/repos/#viewing-repository-tags).</span></span> <span data-ttu-id="979f3-134">This tutorial uses Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="979f3-134">This tutorial uses Azure Container Registry.</span></span> 

1. <span data-ttu-id="979f3-135">In the [Azure portal](https://portal.azure.com), select **Create a resource** > **Containers** > **Container Registry**.</span><span class="sxs-lookup"><span data-stu-id="979f3-135">In the [Azure portal](https://portal.azure.com), select **Create a resource** > **Containers** > **Container Registry**.</span></span>

    ![create container registry](./media/tutorial-deploy-function/create-container-registry.png)

2. <span data-ttu-id="979f3-137">Give your registry a name, and choose a subscription.</span><span class="sxs-lookup"><span data-stu-id="979f3-137">Give your registry a name, and choose a subscription.</span></span>
3. <span data-ttu-id="979f3-138">For the resource group, it is recommended that you use the same resource group name that contains your IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="979f3-138">For the resource group, it is recommended that you use the same resource group name that contains your IoT Hub.</span></span> <span data-ttu-id="979f3-139">By keeping all the resources together in the same group, you can manage them together.</span><span class="sxs-lookup"><span data-stu-id="979f3-139">By keeping all the resources together in the same group, you can manage them together.</span></span> <span data-ttu-id="979f3-140">For example, deleting the resource group used for testing deletes all test resources contained in the group.</span><span class="sxs-lookup"><span data-stu-id="979f3-140">For example, deleting the resource group used for testing deletes all test resources contained in the group.</span></span> 
4. <span data-ttu-id="979f3-141">Set the SKU to **Basic**, and toggle **Admin user** to **Enable**.</span><span class="sxs-lookup"><span data-stu-id="979f3-141">Set the SKU to **Basic**, and toggle **Admin user** to **Enable**.</span></span> 
5. <span data-ttu-id="979f3-142">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="979f3-142">Click **Create**.</span></span>
6. <span data-ttu-id="979f3-143">Once your container registry is created, navigate to it and select **Access keys**.</span><span class="sxs-lookup"><span data-stu-id="979f3-143">Once your container registry is created, navigate to it and select **Access keys**.</span></span> 
7. <span data-ttu-id="979f3-144">Copy the values for **Login server**, **Username**, and **Password**.</span><span class="sxs-lookup"><span data-stu-id="979f3-144">Copy the values for **Login server**, **Username**, and **Password**.</span></span> <span data-ttu-id="979f3-145">You'll use these values later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="979f3-145">You'll use these values later in the tutorial.</span></span> 

## <a name="create-a-function-project"></a><span data-ttu-id="979f3-146">Create a function project</span><span class="sxs-lookup"><span data-stu-id="979f3-146">Create a function project</span></span>

<span data-ttu-id="979f3-147">To send data into a database, you need a module that can structure the data properly and then stores it in a table.</span><span class="sxs-lookup"><span data-stu-id="979f3-147">To send data into a database, you need a module that can structure the data properly and then stores it in a table.</span></span> 

<span data-ttu-id="979f3-148">The following steps show you how to create an IoT Edge function using Visual Studio Code and the Azure IoT Edge extension.</span><span class="sxs-lookup"><span data-stu-id="979f3-148">The following steps show you how to create an IoT Edge function using Visual Studio Code and the Azure IoT Edge extension.</span></span>

1. <span data-ttu-id="979f3-149">Open Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="979f3-149">Open Visual Studio Code.</span></span>
2. <span data-ttu-id="979f3-150">Open the VS Code integrated terminal by selecting **View** > **Terminal**.</span><span class="sxs-lookup"><span data-stu-id="979f3-150">Open the VS Code integrated terminal by selecting **View** > **Terminal**.</span></span>
3. <span data-ttu-id="979f3-151">Open the VS Code command palette by selecting **View** > **Command palette**.</span><span class="sxs-lookup"><span data-stu-id="979f3-151">Open the VS Code command palette by selecting **View** > **Command palette**.</span></span>
4. <span data-ttu-id="979f3-152">In the command palette, type and run the command **Azure: Sign in** and follow the instructions to sign in your Azure account.</span><span class="sxs-lookup"><span data-stu-id="979f3-152">In the command palette, type and run the command **Azure: Sign in** and follow the instructions to sign in your Azure account.</span></span> <span data-ttu-id="979f3-153">If you've already signed in, you can skip this step.</span><span class="sxs-lookup"><span data-stu-id="979f3-153">If you've already signed in, you can skip this step.</span></span>
3. <span data-ttu-id="979f3-154">In the command palette, type and run the command **Azure IoT Edge: New IoT Edge solution**.</span><span class="sxs-lookup"><span data-stu-id="979f3-154">In the command palette, type and run the command **Azure IoT Edge: New IoT Edge solution**.</span></span> <span data-ttu-id="979f3-155">In the command palette, provide the following information to create your solution:</span><span class="sxs-lookup"><span data-stu-id="979f3-155">In the command palette, provide the following information to create your solution:</span></span> 
   1. <span data-ttu-id="979f3-156">Select the folder where you want to create the solution.</span><span class="sxs-lookup"><span data-stu-id="979f3-156">Select the folder where you want to create the solution.</span></span> 
   2. <span data-ttu-id="979f3-157">Provide a name for your solution or accept the default **EdgeSolution**.</span><span class="sxs-lookup"><span data-stu-id="979f3-157">Provide a name for your solution or accept the default **EdgeSolution**.</span></span>
   3. <span data-ttu-id="979f3-158">Choose **Azure Functions - C#** as the module template.</span><span class="sxs-lookup"><span data-stu-id="979f3-158">Choose **Azure Functions - C#** as the module template.</span></span> 
   4. <span data-ttu-id="979f3-159">Name your module **sqlFunction**.</span><span class="sxs-lookup"><span data-stu-id="979f3-159">Name your module **sqlFunction**.</span></span> 
   5. <span data-ttu-id="979f3-160">Specify the Azure Container Registry that you created in the previous section as the image repository for your first module.</span><span class="sxs-lookup"><span data-stu-id="979f3-160">Specify the Azure Container Registry that you created in the previous section as the image repository for your first module.</span></span> <span data-ttu-id="979f3-161">Replace **localhost:5000** with the login server value that you copied.</span><span class="sxs-lookup"><span data-stu-id="979f3-161">Replace **localhost:5000** with the login server value that you copied.</span></span> <span data-ttu-id="979f3-162">The final string looks like **\<registry name\>.azurecr.io/sqlFunction**.</span><span class="sxs-lookup"><span data-stu-id="979f3-162">The final string looks like **\<registry name\>.azurecr.io/sqlFunction**.</span></span>

4. <span data-ttu-id="979f3-163">The VS Code window loads your IoT Edge solution workspace.</span><span class="sxs-lookup"><span data-stu-id="979f3-163">The VS Code window loads your IoT Edge solution workspace.</span></span> <span data-ttu-id="979f3-164">There is a **modules** folder, a **.vscode** folder, and a deployment manifest template file.</span><span class="sxs-lookup"><span data-stu-id="979f3-164">There is a **modules** folder, a **.vscode** folder, and a deployment manifest template file.</span></span> <span data-ttu-id="979f3-165">Open **modules** > **sqlFunction** > **EdgeHubTrigger-Csharp** > **run.csx**.</span><span class="sxs-lookup"><span data-stu-id="979f3-165">Open **modules** > **sqlFunction** > **EdgeHubTrigger-Csharp** > **run.csx**.</span></span>

5. <span data-ttu-id="979f3-166">Replace the contents of the file with the following code:</span><span class="sxs-lookup"><span data-stu-id="979f3-166">Replace the contents of the file with the following code:</span></span>

   ```csharp
   #r "Microsoft.Azure.Devices.Client"
   #r "Newtonsoft.Json"
   #r "System.Data.SqlClient"

   using System.IO;
   using Microsoft.Azure.Devices.Client;
   using Newtonsoft.Json;
   using Sql = System.Data.SqlClient;
   using System.Threading.Tasks;

   // Filter messages based on the temperature value in the body of the message and the temperature threshold value.
   public static async Task Run(Message messageReceived, IAsyncCollector<Message> output, TraceWriter log)
   {
       const int temperatureThreshold = 25;
       byte[] messageBytes = messageReceived.GetBytes();
       var messageString = System.Text.Encoding.UTF8.GetString(messageBytes);

       if (!string.IsNullOrEmpty(messageString))
       {
           // Get the body of the message and deserialize it
           var messageBody = JsonConvert.DeserializeObject<MessageBody>(messageString);

           //Store the data in SQL db
           const string str = "<sql connection string>";
           using (Sql.SqlConnection conn = new Sql.SqlConnection(str))
           {
           conn.Open();
           var insertMachineTemperature = "INSERT INTO MeasurementsDB.dbo.TemperatureMeasurements VALUES (CONVERT(DATETIME2,'" + messageBody.timeCreated + "', 127), 'machine', " + messageBody.machine.temperature + ");";
           var insertAmbientTemperature = "INSERT INTO MeasurementsDB.dbo.TemperatureMeasurements VALUES (CONVERT(DATETIME2,'" + messageBody.timeCreated + "', 127), 'ambient', " + messageBody.ambient.temperature + ");"; 
               using (Sql.SqlCommand cmd = new Sql.SqlCommand(insertMachineTemperature + "\n" + insertAmbientTemperature, conn))
               {
               //Execute the command and log the # rows affected.
               var rows = await cmd.ExecuteNonQueryAsync();
               log.Info($"{rows} rows were updated");
               }
           }

           if (messageBody != null && messageBody.machine.temperature > temperatureThreshold)
           {
               // Send the message to the output as the temperature value is greater than the threshold
               var filteredMessage = new Message(messageBytes);
               // Copy the properties of the original message into the new Message object
               foreach (KeyValuePair<string, string> prop in messageReceived.Properties)
               {
                   filteredMessage.Properties.Add(prop.Key, prop.Value);
               }
               // Add a new property to the message to indicate it is an alert
               filteredMessage.Properties.Add("MessageType", "Alert");
               // Send the message        
               await output.AddAsync(filteredMessage);
               log.Info("Received and transferred a message with temperature above the threshold");
           }
       }
   }

   //Define the expected schema for the body of incoming messages
   class MessageBody
   {
       public Machine machine {get;set;}
       public Ambient ambient {get; set;}
       public string timeCreated {get; set;}
   }
   class Machine
   {
      public double temperature {get; set;}
      public double pressure {get; set;}         
   }
   class Ambient
   {
      public double temperature {get; set;}
      public int humidity {get; set;}         
   }
   ```

6. <span data-ttu-id="979f3-167">In line 24, replace the string **\<sql connection string\>** with the following string.</span><span class="sxs-lookup"><span data-stu-id="979f3-167">In line 24, replace the string **\<sql connection string\>** with the following string.</span></span> <span data-ttu-id="979f3-168">The **Data Source** property references the SQL Server container name, which you will create with the name **SQL** in the next section.</span><span class="sxs-lookup"><span data-stu-id="979f3-168">The **Data Source** property references the SQL Server container name, which you will create with the name **SQL** in the next section.</span></span> 

   ```C#
   Data Source=tcp:sql,1433;Initial Catalog=MeasurementsDB;User Id=SA;Password=Strong!Passw0rd;TrustServerCertificate=False;Connection Timeout=30;
   ```

7. <span data-ttu-id="979f3-169">Save the **run.csx** file.</span><span class="sxs-lookup"><span data-stu-id="979f3-169">Save the **run.csx** file.</span></span> 

## <a name="add-a-sql-server-container"></a><span data-ttu-id="979f3-170">Add a SQL Server container</span><span class="sxs-lookup"><span data-stu-id="979f3-170">Add a SQL Server container</span></span>

<span data-ttu-id="979f3-171">A [Deployment manifest](module-composition.md) declares which modules the IoT Edge runtime will install on your IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="979f3-171">A [Deployment manifest](module-composition.md) declares which modules the IoT Edge runtime will install on your IoT Edge device.</span></span> <span data-ttu-id="979f3-172">You added the code to make a customized Function module in the previous section, but the SQL Server module is already built.</span><span class="sxs-lookup"><span data-stu-id="979f3-172">You added the code to make a customized Function module in the previous section, but the SQL Server module is already built.</span></span> <span data-ttu-id="979f3-173">You just need to tell the IoT Edge runtime to include it, then configure it on your device.</span><span class="sxs-lookup"><span data-stu-id="979f3-173">You just need to tell the IoT Edge runtime to include it, then configure it on your device.</span></span> 

1. <span data-ttu-id="979f3-174">In the Visual Studio Code explorer, open the **deployment.template.json** file.</span><span class="sxs-lookup"><span data-stu-id="979f3-174">In the Visual Studio Code explorer, open the **deployment.template.json** file.</span></span> 
2. <span data-ttu-id="979f3-175">Find the **moduleContent.$edgeAgent.properties.desired.modules** section.</span><span class="sxs-lookup"><span data-stu-id="979f3-175">Find the **moduleContent.$edgeAgent.properties.desired.modules** section.</span></span> <span data-ttu-id="979f3-176">There should be two modules listed: **tempSensor**, which generates simulated data, and your **sqlFunction** module.</span><span class="sxs-lookup"><span data-stu-id="979f3-176">There should be two modules listed: **tempSensor**, which generates simulated data, and your **sqlFunction** module.</span></span>
3. <span data-ttu-id="979f3-177">If you're using Windows containers, modify the **sqlFunction.settings.image** section.</span><span class="sxs-lookup"><span data-stu-id="979f3-177">If you're using Windows containers, modify the **sqlFunction.settings.image** section.</span></span>
    ```json
    "image": "${MODULES.sqlFunction.windows-amd64}"
    ```
4. <span data-ttu-id="979f3-178">Add the following code to declare a third module.</span><span class="sxs-lookup"><span data-stu-id="979f3-178">Add the following code to declare a third module.</span></span> <span data-ttu-id="979f3-179">Add a comma after the sqlFunction section and insert:</span><span class="sxs-lookup"><span data-stu-id="979f3-179">Add a comma after the sqlFunction section and insert:</span></span>

   ```json
   "sql": {
       "version": "1.0",
       "type": "docker",
       "status": "running",
       "restartPolicy": "always",
       "settings": {
           "image": "",
           "createOptions": ""
       }
   }
   ```

   <span data-ttu-id="979f3-180">Here's an example if there is any confusion with adding a JSON element.</span><span class="sxs-lookup"><span data-stu-id="979f3-180">Here's an example if there is any confusion with adding a JSON element.</span></span> ![Add sql server container](./media/tutorial-store-data-sql-server/view_json_sql.png)

5. <span data-ttu-id="979f3-182">Depending on the type of Docker containers on your IoT Edge device, update the **sql.settings** parameters with the following code:</span><span class="sxs-lookup"><span data-stu-id="979f3-182">Depending on the type of Docker containers on your IoT Edge device, update the **sql.settings** parameters with the following code:</span></span>

   * <span data-ttu-id="979f3-183">Windows containers:</span><span class="sxs-lookup"><span data-stu-id="979f3-183">Windows containers:</span></span>

      ```json
      "image": "microsoft/mssql-server-windows-developer",
      "createOptions": "{\"Env\": [\"ACCEPT_EULA=Y\",\"SA_PASSWORD=Strong!Passw0rd\"],\"HostConfig\": {\"Mounts\": [{\"Target\": \"C:\\\\mssql\",\"Source\": \"sqlVolume\",\"Type\": \"volume\"}],\"PortBindings\": {\"1433/tcp\": [{\"HostPort\": \"1401\"}]}}}"
      ```

   * <span data-ttu-id="979f3-184">Linux containers:</span><span class="sxs-lookup"><span data-stu-id="979f3-184">Linux containers:</span></span>

      ```json
      "image": "microsoft/mssql-server-linux:2017-latest",
      "createOptions": "{\"Env\": [\"ACCEPT_EULA=Y\",\"MSSQL_SA_PASSWORD=Strong!Passw0rd\"],\"HostConfig\": {\"Mounts\": [{\"Target\": \"/var/opt/mssql\",\"Source\": \"sqlVolume\",\"Type\": \"volume\"}],\"PortBindings\": {\"1433/tcp\": [{\"HostPort\": \"1401\"}]}}}"
      ```

   >[!Tip]
   ><span data-ttu-id="979f3-185">Any time that you create a SQL Server container in a production environment, you should [change the default system administrator password](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker#change-the-sa-password).</span><span class="sxs-lookup"><span data-stu-id="979f3-185">Any time that you create a SQL Server container in a production environment, you should [change the default system administrator password](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker#change-the-sa-password).</span></span>

6. <span data-ttu-id="979f3-186">Save the **deployment.template.json** file.</span><span class="sxs-lookup"><span data-stu-id="979f3-186">Save the **deployment.template.json** file.</span></span>

## <a name="build-your-iot-edge-solution"></a><span data-ttu-id="979f3-187">Build your IoT Edge solution</span><span class="sxs-lookup"><span data-stu-id="979f3-187">Build your IoT Edge solution</span></span>

<span data-ttu-id="979f3-188">In the previous sections, you created a solution with one module, and then added another to the deployment manifest template.</span><span class="sxs-lookup"><span data-stu-id="979f3-188">In the previous sections, you created a solution with one module, and then added another to the deployment manifest template.</span></span> <span data-ttu-id="979f3-189">Now, you need to build the solution, create container images for the modules, and push the images to your container registry.</span><span class="sxs-lookup"><span data-stu-id="979f3-189">Now, you need to build the solution, create container images for the modules, and push the images to your container registry.</span></span> 

1. <span data-ttu-id="979f3-190">In the .env file, give the IoT Edge runtime your registry credentials so that it can access your module images.</span><span class="sxs-lookup"><span data-stu-id="979f3-190">In the .env file, give the IoT Edge runtime your registry credentials so that it can access your module images.</span></span> <span data-ttu-id="979f3-191">Find the **CONTAINER_REGISTRY_USERNAME** and **CONTAINER_REGISTRY_PASSWORD** sections and insert your credentials after the equals symbol:</span><span class="sxs-lookup"><span data-stu-id="979f3-191">Find the **CONTAINER_REGISTRY_USERNAME** and **CONTAINER_REGISTRY_PASSWORD** sections and insert your credentials after the equals symbol:</span></span> 

   ```env
   CONTAINER_REGISTRY_USERNAME_yourContainerReg=<username>
   CONTAINER_REGISTRY_PASSWORD_yourContainerReg=<password>
   ```
2. <span data-ttu-id="979f3-192">Save the .env file.</span><span class="sxs-lookup"><span data-stu-id="979f3-192">Save the .env file.</span></span>
3. <span data-ttu-id="979f3-193">Sign in to your container registry in Visual Studio Code so that you can push your images to your registry.</span><span class="sxs-lookup"><span data-stu-id="979f3-193">Sign in to your container registry in Visual Studio Code so that you can push your images to your registry.</span></span> <span data-ttu-id="979f3-194">Use the same credentials that you added to the .env file.</span><span class="sxs-lookup"><span data-stu-id="979f3-194">Use the same credentials that you added to the .env file.</span></span> <span data-ttu-id="979f3-195">Enter the following command in the integrated terminal:</span><span class="sxs-lookup"><span data-stu-id="979f3-195">Enter the following command in the integrated terminal:</span></span>

    ```csh/sh
    docker login -u <ACR username> <ACR login server>
    ```
    <span data-ttu-id="979f3-196">You will be prompted for the password.</span><span class="sxs-lookup"><span data-stu-id="979f3-196">You will be prompted for the password.</span></span> <span data-ttu-id="979f3-197">Paste your password into the prompt and press **Enter**.</span><span class="sxs-lookup"><span data-stu-id="979f3-197">Paste your password into the prompt and press **Enter**.</span></span>

    ```csh/sh
    Password: <paste in the ACR password and press enter>
    Login Succeeded
    ```

4. <span data-ttu-id="979f3-198">In the VS Code explorer, right-click the **deployment.template.json** file and select **Build and Push IoT Edge solution**.</span><span class="sxs-lookup"><span data-stu-id="979f3-198">In the VS Code explorer, right-click the **deployment.template.json** file and select **Build and Push IoT Edge solution**.</span></span> 

## <a name="deploy-the-solution-to-a-device"></a><span data-ttu-id="979f3-199">Deploy the solution to a device</span><span class="sxs-lookup"><span data-stu-id="979f3-199">Deploy the solution to a device</span></span>

<span data-ttu-id="979f3-200">You can set modules on a device through the IoT Hub, but you can also access your IoT Hub and devices through Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="979f3-200">You can set modules on a device through the IoT Hub, but you can also access your IoT Hub and devices through Visual Studio Code.</span></span> <span data-ttu-id="979f3-201">In this section, you set up access to your IoT Hub then use VS Code to deploy your solution to your IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="979f3-201">In this section, you set up access to your IoT Hub then use VS Code to deploy your solution to your IoT Edge device.</span></span> 

1. <span data-ttu-id="979f3-202">In the VS Code command palette, select **Azure IoT Hub: Select IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="979f3-202">In the VS Code command palette, select **Azure IoT Hub: Select IoT Hub**.</span></span>
2. <span data-ttu-id="979f3-203">Follow the prompts to sign in to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="979f3-203">Follow the prompts to sign in to your Azure account.</span></span> 
3. <span data-ttu-id="979f3-204">In the command palette, select your Azure subscription then select your IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="979f3-204">In the command palette, select your Azure subscription then select your IoT Hub.</span></span> 
4. <span data-ttu-id="979f3-205">In the VS Code explorer, expand the **Azure IoT Hub Devices** section.</span><span class="sxs-lookup"><span data-stu-id="979f3-205">In the VS Code explorer, expand the **Azure IoT Hub Devices** section.</span></span> 
5. <span data-ttu-id="979f3-206">Right-click on the device that you want to target with your deployment and select **Create deployment for single device**.</span><span class="sxs-lookup"><span data-stu-id="979f3-206">Right-click on the device that you want to target with your deployment and select **Create deployment for single device**.</span></span> 
6. <span data-ttu-id="979f3-207">In the file explorer, navigate to the **config** folder inside your solution and choose **deployment.json**.</span><span class="sxs-lookup"><span data-stu-id="979f3-207">In the file explorer, navigate to the **config** folder inside your solution and choose **deployment.json**.</span></span> <span data-ttu-id="979f3-208">Click **Select Edge deployment manifest**.</span><span class="sxs-lookup"><span data-stu-id="979f3-208">Click **Select Edge deployment manifest**.</span></span> 

<span data-ttu-id="979f3-209">If the deployment is successful, and confirmation message is printed in the VS Code output.</span><span class="sxs-lookup"><span data-stu-id="979f3-209">If the deployment is successful, and confirmation message is printed in the VS Code output.</span></span> <span data-ttu-id="979f3-210">You can also check to see that all the modules are up and running on your device.</span><span class="sxs-lookup"><span data-stu-id="979f3-210">You can also check to see that all the modules are up and running on your device.</span></span> 

<span data-ttu-id="979f3-211">On your IoT Edge device, run the following command to see the status of the modules.</span><span class="sxs-lookup"><span data-stu-id="979f3-211">On your IoT Edge device, run the following command to see the status of the modules.</span></span> <span data-ttu-id="979f3-212">It may take a few minutes.</span><span class="sxs-lookup"><span data-stu-id="979f3-212">It may take a few minutes.</span></span>

   ```PowerShell
   iotedge list
   ```

## <a name="create-the-sql-database"></a><span data-ttu-id="979f3-213">Create the SQL database</span><span class="sxs-lookup"><span data-stu-id="979f3-213">Create the SQL database</span></span>

<span data-ttu-id="979f3-214">When you apply the deployment manifest to your device, you get three modules running.</span><span class="sxs-lookup"><span data-stu-id="979f3-214">When you apply the deployment manifest to your device, you get three modules running.</span></span> <span data-ttu-id="979f3-215">The tempSensor module generates simulated environment data.</span><span class="sxs-lookup"><span data-stu-id="979f3-215">The tempSensor module generates simulated environment data.</span></span> <span data-ttu-id="979f3-216">The sqlFunction module takes the data and formats it for a database.</span><span class="sxs-lookup"><span data-stu-id="979f3-216">The sqlFunction module takes the data and formats it for a database.</span></span> 

<span data-ttu-id="979f3-217">This section guides you through setting up the SQL database to store the temperature data.</span><span class="sxs-lookup"><span data-stu-id="979f3-217">This section guides you through setting up the SQL database to store the temperature data.</span></span> 

1. <span data-ttu-id="979f3-218">In a command-line too, connect to your database.</span><span class="sxs-lookup"><span data-stu-id="979f3-218">In a command-line too, connect to your database.</span></span> 
   * <span data-ttu-id="979f3-219">Windows container:</span><span class="sxs-lookup"><span data-stu-id="979f3-219">Windows container:</span></span>
   
      ```cmd
      docker exec -it sql cmd
      ```
    
   * <span data-ttu-id="979f3-220">Linux container:</span><span class="sxs-lookup"><span data-stu-id="979f3-220">Linux container:</span></span> 

      ```bash
      docker exec -it sql bash
      ```

2. <span data-ttu-id="979f3-221">Open the SQL command tool.</span><span class="sxs-lookup"><span data-stu-id="979f3-221">Open the SQL command tool.</span></span>
   * <span data-ttu-id="979f3-222">Windows container:</span><span class="sxs-lookup"><span data-stu-id="979f3-222">Windows container:</span></span>

      ```cmd
      sqlcmd -S localhost -U SA -P "Strong!Passw0rd"
      ```

   * <span data-ttu-id="979f3-223">Linux container:</span><span class="sxs-lookup"><span data-stu-id="979f3-223">Linux container:</span></span> 

      ```bash
      /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P 'Strong!Passw0rd'
      ```

3. <span data-ttu-id="979f3-224">Create your database:</span><span class="sxs-lookup"><span data-stu-id="979f3-224">Create your database:</span></span> 

   * <span data-ttu-id="979f3-225">Windows container</span><span class="sxs-lookup"><span data-stu-id="979f3-225">Windows container</span></span>
      ```sql
      CREATE DATABASE MeasurementsDB
      ON
      (NAME = MeasurementsDB, FILENAME = 'C:\mssql\measurementsdb.mdf')
      GO
      ```

   * <span data-ttu-id="979f3-226">Linux container</span><span class="sxs-lookup"><span data-stu-id="979f3-226">Linux container</span></span>
      ```sql
      CREATE DATABASE MeasurementsDB
      ON
      (NAME = MeasurementsDB, FILENAME = '/var/opt/mssql/measurementsdb.mdf')
      GO
      ```

4. <span data-ttu-id="979f3-227">Define your table.</span><span class="sxs-lookup"><span data-stu-id="979f3-227">Define your table.</span></span>

   ```sql
   CREATE TABLE MeasurementsDB.dbo.TemperatureMeasurements (measurementTime DATETIME2, location NVARCHAR(50), temperature FLOAT)
   GO
   ```

<span data-ttu-id="979f3-228">You can customize your SQL Server docker file to automatically set up your SQL Server to be deployed on multiple IoT Edge devices.</span><span class="sxs-lookup"><span data-stu-id="979f3-228">You can customize your SQL Server docker file to automatically set up your SQL Server to be deployed on multiple IoT Edge devices.</span></span> <span data-ttu-id="979f3-229">For more information, see the [Microsoft SQL Server container demo project](https://github.com/twright-msft/mssql-node-docker-demo-app).</span><span class="sxs-lookup"><span data-stu-id="979f3-229">For more information, see the [Microsoft SQL Server container demo project](https://github.com/twright-msft/mssql-node-docker-demo-app).</span></span> 

## <a name="view-the-local-data"></a><span data-ttu-id="979f3-230">View the local data</span><span class="sxs-lookup"><span data-stu-id="979f3-230">View the local data</span></span>

<span data-ttu-id="979f3-231">Once your table is created, the sqlFunction module starts storing data in a local SQL Server 2017 database on your IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="979f3-231">Once your table is created, the sqlFunction module starts storing data in a local SQL Server 2017 database on your IoT Edge device.</span></span> 

<span data-ttu-id="979f3-232">From inside the SQL command tool, run the following command to view your formatted table data:</span><span class="sxs-lookup"><span data-stu-id="979f3-232">From inside the SQL command tool, run the following command to view your formatted table data:</span></span> 

   ```sql
   SELECT * FROM MeasurementsDB.dbo.TemperatureMeasurements
   GO
   ```

   ![View local data](./media/tutorial-store-data-sql-server/view-data.png)



## <a name="clean-up-resources"></a><span data-ttu-id="979f3-234">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="979f3-234">Clean up resources</span></span>

<span data-ttu-id="979f3-235">If you plan to continue to the next recommended article, you can keep the resources and configurations that you created and reuse them.</span><span class="sxs-lookup"><span data-stu-id="979f3-235">If you plan to continue to the next recommended article, you can keep the resources and configurations that you created and reuse them.</span></span> <span data-ttu-id="979f3-236">You can also keep using the same IoT Edge device as a test device.</span><span class="sxs-lookup"><span data-stu-id="979f3-236">You can also keep using the same IoT Edge device as a test device.</span></span> 

<span data-ttu-id="979f3-237">Otherwise, you can delete the local configurations and the Azure resources that you created in this article to avoid charges.</span><span class="sxs-lookup"><span data-stu-id="979f3-237">Otherwise, you can delete the local configurations and the Azure resources that you created in this article to avoid charges.</span></span> 

[!INCLUDE [iot-edge-clean-up-cloud-resources](../../includes/iot-edge-clean-up-cloud-resources.md)]

[!INCLUDE [iot-edge-clean-up-local-resources](../../includes/iot-edge-clean-up-local-resources.md)]



## <a name="next-steps"></a><span data-ttu-id="979f3-238">Next steps</span><span class="sxs-lookup"><span data-stu-id="979f3-238">Next steps</span></span>

<span data-ttu-id="979f3-239">In this tutorial, you created an Azure Functions module that contains code to filter raw data generated by your IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="979f3-239">In this tutorial, you created an Azure Functions module that contains code to filter raw data generated by your IoT Edge device.</span></span> <span data-ttu-id="979f3-240">When you're ready to build your own modules, you can learn more about how to [Develop Azure Functions with Azure IoT Edge for Visual Studio Code](how-to-develop-csharp-function.md).</span><span class="sxs-lookup"><span data-stu-id="979f3-240">When you're ready to build your own modules, you can learn more about how to [Develop Azure Functions with Azure IoT Edge for Visual Studio Code](how-to-develop-csharp-function.md).</span></span> 

<span data-ttu-id="979f3-241">Continue on to the next tutorials to learn about other ways that Azure IoT Edge can help you turn data into business insights at the edge.</span><span class="sxs-lookup"><span data-stu-id="979f3-241">Continue on to the next tutorials to learn about other ways that Azure IoT Edge can help you turn data into business insights at the edge.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="979f3-242">Find averages using a floating window in Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="979f3-242">Find averages using a floating window in Azure Stream Analytics</span></span>](tutorial-deploy-stream-analytics.md)
