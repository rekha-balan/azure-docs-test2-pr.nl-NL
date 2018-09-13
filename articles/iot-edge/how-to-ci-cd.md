---
title: Azure IoT Edge continuous integration and continuous deployment | Microsoft Docs
description: Overview of the continuous integration and continuous deployment for Azure IoT Edge
author: shizn
manager: ''
ms.author: xshi
ms.date: 06/27/2018
ms.topic: conceptual
ms.service: iot-edge
services: iot-edge
ms.openlocfilehash: 5099ca70503ba2ed4ae8f4969a9199816c4986fb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871429"
---
# <a name="continuous-integration-and-continuous-deployment-to-azure-iot-edge"></a><span data-ttu-id="a18c5-103">Continuous integration and continuous deployment to Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="a18c5-103">Continuous integration and continuous deployment to Azure IoT Edge</span></span>

<span data-ttu-id="a18c5-104">This article demonstrates how you can use the continuous integration and continuous deployment features of Azure DevOps Services and Microsoft Team Foundation Server (TFS) to build, test, and deploy applications quickly and efficiently to your Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="a18c5-104">This article demonstrates how you can use the continuous integration and continuous deployment features of Azure DevOps Services and Microsoft Team Foundation Server (TFS) to build, test, and deploy applications quickly and efficiently to your Azure IoT Edge.</span></span> 

<span data-ttu-id="a18c5-105">In this article, you will learn how to:</span><span class="sxs-lookup"><span data-stu-id="a18c5-105">In this article, you will learn how to:</span></span>
* <span data-ttu-id="a18c5-106">Create and check in a sample IoT Edge solution containing unit tests.</span><span class="sxs-lookup"><span data-stu-id="a18c5-106">Create and check in a sample IoT Edge solution containing unit tests.</span></span>
* <span data-ttu-id="a18c5-107">Install Azure IoT Edge extension for your Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="a18c5-107">Install Azure IoT Edge extension for your Azure DevOps.</span></span>
* <span data-ttu-id="a18c5-108">Configure continuous integration (CI) to build the solution and run the unit tests.</span><span class="sxs-lookup"><span data-stu-id="a18c5-108">Configure continuous integration (CI) to build the solution and run the unit tests.</span></span>
* <span data-ttu-id="a18c5-109">Configure continuous deployment (CD) to deploy the solution and view responses.</span><span class="sxs-lookup"><span data-stu-id="a18c5-109">Configure continuous deployment (CD) to deploy the solution and view responses.</span></span>

<span data-ttu-id="a18c5-110">It will take 30 minutes to complete the steps in this article.</span><span class="sxs-lookup"><span data-stu-id="a18c5-110">It will take 30 minutes to complete the steps in this article.</span></span>

![CI and CD](./media/how-to-ci-cd/cd.png)

## <a name="create-a-sample-azure-iot-edge-solution-using-visual-studio-code"></a><span data-ttu-id="a18c5-112">Create a sample Azure IoT Edge solution using Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="a18c5-112">Create a sample Azure IoT Edge solution using Visual Studio Code</span></span>

<span data-ttu-id="a18c5-113">In this section, you will create a sample IoT Edge solution containing unit tests that you can execute as part of the build process.</span><span class="sxs-lookup"><span data-stu-id="a18c5-113">In this section, you will create a sample IoT Edge solution containing unit tests that you can execute as part of the build process.</span></span> <span data-ttu-id="a18c5-114">Before following the guidance in this section, complete the steps in [Develop an IoT Edge solution with multiple modules in Visual Studio Code](tutorial-multiple-modules-in-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="a18c5-114">Before following the guidance in this section, complete the steps in [Develop an IoT Edge solution with multiple modules in Visual Studio Code](tutorial-multiple-modules-in-vscode.md).</span></span>

1. <span data-ttu-id="a18c5-115">In VS Code command palette, type and run the command **Edge: New IoT Edge solution**.</span><span class="sxs-lookup"><span data-stu-id="a18c5-115">In VS Code command palette, type and run the command **Edge: New IoT Edge solution**.</span></span> <span data-ttu-id="a18c5-116">Then select your workspace folder, provide the solution name (The default name is **EdgeSolution**), and create a C# Module (**FilterModule**) as the first user module in this solution.</span><span class="sxs-lookup"><span data-stu-id="a18c5-116">Then select your workspace folder, provide the solution name (The default name is **EdgeSolution**), and create a C# Module (**FilterModule**) as the first user module in this solution.</span></span> <span data-ttu-id="a18c5-117">You also need to specify the Docker image repository for your first module.</span><span class="sxs-lookup"><span data-stu-id="a18c5-117">You also need to specify the Docker image repository for your first module.</span></span> <span data-ttu-id="a18c5-118">The default image repository is based on a local Docker registry (`localhost:5000/filtermodule`).</span><span class="sxs-lookup"><span data-stu-id="a18c5-118">The default image repository is based on a local Docker registry (`localhost:5000/filtermodule`).</span></span> <span data-ttu-id="a18c5-119">You need to change it to Azure Container Registry(`<your container registry address>/filtermodule`) or Docker Hub for further continuous integration.</span><span class="sxs-lookup"><span data-stu-id="a18c5-119">You need to change it to Azure Container Registry(`<your container registry address>/filtermodule`) or Docker Hub for further continuous integration.</span></span>

    ![Setup ACR](./media/how-to-ci-cd/acr.png)

2. <span data-ttu-id="a18c5-121">The VS Code window will load your IoT Edge solution workspace.</span><span class="sxs-lookup"><span data-stu-id="a18c5-121">The VS Code window will load your IoT Edge solution workspace.</span></span> <span data-ttu-id="a18c5-122">You can optionally type and run **Edge: Add IoT Edge module** to add more modules.</span><span class="sxs-lookup"><span data-stu-id="a18c5-122">You can optionally type and run **Edge: Add IoT Edge module** to add more modules.</span></span> <span data-ttu-id="a18c5-123">There is a `modules` folder, a `.vscode` folder, and a deployment manifest template file in the root folder.</span><span class="sxs-lookup"><span data-stu-id="a18c5-123">There is a `modules` folder, a `.vscode` folder, and a deployment manifest template file in the root folder.</span></span> <span data-ttu-id="a18c5-124">All user module codes will be subfolders under the folder `modules`.</span><span class="sxs-lookup"><span data-stu-id="a18c5-124">All user module codes will be subfolders under the folder `modules`.</span></span> <span data-ttu-id="a18c5-125">The `deployment.template.json` is the deployment manifest template.</span><span class="sxs-lookup"><span data-stu-id="a18c5-125">The `deployment.template.json` is the deployment manifest template.</span></span> <span data-ttu-id="a18c5-126">Some of the parameters in this file will be parsed from the `module.json`, which exists in every module folder.</span><span class="sxs-lookup"><span data-stu-id="a18c5-126">Some of the parameters in this file will be parsed from the `module.json`, which exists in every module folder.</span></span>

3. <span data-ttu-id="a18c5-127">Now your sample IoT Edge solution is ready.</span><span class="sxs-lookup"><span data-stu-id="a18c5-127">Now your sample IoT Edge solution is ready.</span></span> <span data-ttu-id="a18c5-128">The default C# module acts as a pipe message module.</span><span class="sxs-lookup"><span data-stu-id="a18c5-128">The default C# module acts as a pipe message module.</span></span> <span data-ttu-id="a18c5-129">In the `deployment.template.json`, you will see this solution contains two modules.</span><span class="sxs-lookup"><span data-stu-id="a18c5-129">In the `deployment.template.json`, you will see this solution contains two modules.</span></span> <span data-ttu-id="a18c5-130">The message will be generated from the `tempSensor` module, and will be directly piped via `FilterModule`, then sent to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a18c5-130">The message will be generated from the `tempSensor` module, and will be directly piped via `FilterModule`, then sent to your IoT hub.</span></span> <span data-ttu-id="a18c5-131">Replace the entire **Program.cs** file with below content.</span><span class="sxs-lookup"><span data-stu-id="a18c5-131">Replace the entire **Program.cs** file with below content.</span></span> <span data-ttu-id="a18c5-132">For more information about this code snippet, you can refer to [Create an IoT Edge C# module project](https://docs.microsoft.com/azure/iot-edge/tutorial-csharp-module#create-an-iot-edge-module-project).</span><span class="sxs-lookup"><span data-stu-id="a18c5-132">For more information about this code snippet, you can refer to [Create an IoT Edge C# module project](https://docs.microsoft.com/azure/iot-edge/tutorial-csharp-module#create-an-iot-edge-module-project).</span></span>

    ```csharp
    namespace FilterModule
    {
        using System;
        using System.IO;
        using System.Runtime.InteropServices;
        using System.Runtime.Loader;
        using System.Security.Cryptography.X509Certificates;
        using System.Text;
        using System.Threading;
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Client.Transport.Mqtt;
        using System.Collections.Generic;     // for KeyValuePair<>
        using Microsoft.Azure.Devices.Shared; // for TwinCollection
        using Newtonsoft.Json;                // for JsonConvert

        public class MessageBody
        {
            public Machine machine { get; set; }
            public Ambient ambient { get; set; }
            public string timeCreated { get; set; }
        }
        public class Machine
        {
            public double temperature { get; set; }
            public double pressure { get; set; }
        }
        public class Ambient
        {
            public double temperature { get; set; }
            public int humidity { get; set; }
        }

        public class Program
        {
            static int counter;
            static int temperatureThreshold { get; set; } = 25;

            static void Main(string[] args)
            {
                Init().Wait();

                // Wait until the app unloads or is cancelled
                var cts = new CancellationTokenSource();
                AssemblyLoadContext.Default.Unloading += (ctx) => cts.Cancel();
                Console.CancelKeyPress += (sender, cpe) => cts.Cancel();
                WhenCancelled(cts.Token).Wait();
            }

            /// <summary>
            /// Handles cleanup operations when app is cancelled or unloads
            /// </summary>
            public static Task WhenCancelled(CancellationToken cancellationToken)
            {
                var tcs = new TaskCompletionSource<bool>();
                cancellationToken.Register(s => ((TaskCompletionSource<bool>)s).SetResult(true), tcs);
                return tcs.Task;
            }

            /// <summary>
            /// Initializes the ModuleClient and sets up the callback to receive
            /// messages containing temperature information
            /// </summary>
            static async Task Init()
            {
                MqttTransportSettings mqttSetting = new MqttTransportSettings(TransportType.Mqtt_Tcp_Only);
                ITransportSettings[] settings = { mqttSetting };

                // Open a connection to the Edge runtime
                ModuleClient ioTHubModuleClient = await ModuleClient.CreateFromEnvironmentAsync(settings);
                await ioTHubModuleClient.OpenAsync();
                Console.WriteLine("IoT Hub module client initialized.");

                // Register callback to be called when a message is received by the module
                await ioTHubModuleClient.SetInputMessageHandlerAsync("input1", FilterMessage, ioTHubModuleClient);
            }

            /// <summary>
            /// This method is called whenever the module is sent a message from the EdgeHub. 
            /// It just pipe the messages without any change.
            /// It prints all the incoming messages.
            /// </summary>
            static async Task<MessageResponse> FilterMessage(Message message, object userContext)
            {
                int counterValue = Interlocked.Increment(ref counter);

                var moduleClient = userContext as ModuleClient;
                if (moduleClient == null)
                {
                    throw new InvalidOperationException("UserContext doesn't contain " + "expected values");
                }

                byte[] messageBytes = message.GetBytes();
                string messageString = Encoding.UTF8.GetString(messageBytes);
                Console.WriteLine($"Received message: {counterValue}, Body: [{messageString}]");

                var filteredMessage = filter(message);

                if (filteredMessage != null && !string.IsNullOrEmpty(messageString))
                {
                    var pipeMessage = new Message(messageBytes);
                    foreach (var prop in message.Properties)
                    {
                        pipeMessage.Properties.Add(prop.Key, prop.Value);
                    }
                    await moduleClient.SendEventAsync("output1", pipeMessage);
                    Console.WriteLine("Received message sent");
                }
                return MessageResponse.Completed;
            }

            public static Message filter(Message message)
            {
                var counterValue = Interlocked.Increment(ref counter);

                var messageBytes = message.GetBytes();
                var messageString = Encoding.UTF8.GetString(messageBytes);
                Console.WriteLine($"Received message {counterValue}: [{messageString}]");

                // Get message body
                var messageBody = JsonConvert.DeserializeObject<MessageBody>(messageString);

                if (messageBody != null && messageBody.machine.temperature > temperatureThreshold)
                {
                    Console.WriteLine($"Machine temperature {messageBody.machine.temperature} " +
                        $"exceeds threshold {temperatureThreshold}");
                    var filteredMessage = new Message(messageBytes);
                    foreach (KeyValuePair<string, string> prop in message.Properties)
                    {
                        filteredMessage.Properties.Add(prop.Key, prop.Value);
                    }

                    filteredMessage.Properties.Add("MessageType", "Alert");
                    return filteredMessage;
                }
                return null;
            }
        }
    }
    ```

4. <span data-ttu-id="a18c5-133">Create a .Net Core unit test project.</span><span class="sxs-lookup"><span data-stu-id="a18c5-133">Create a .Net Core unit test project.</span></span> <span data-ttu-id="a18c5-134">In VS Code file explorer, create a new folder **tests\FilterModuleTest** in your workspace.</span><span class="sxs-lookup"><span data-stu-id="a18c5-134">In VS Code file explorer, create a new folder **tests\FilterModuleTest** in your workspace.</span></span> <span data-ttu-id="a18c5-135">Then in VS Code integrated terminal (**Ctrl + \`**), run following commands to create a xunit test project and add reference to the **FilterModule** project.</span><span class="sxs-lookup"><span data-stu-id="a18c5-135">Then in VS Code integrated terminal (**Ctrl + \`**), run following commands to create a xunit test project and add reference to the **FilterModule** project.</span></span>

    ```cmd
    cd tests\FilterModuleTest
    dotnet new xunit
    dotnet add reference ../../modules/FilterModule/FilterModule.csproj
    ```

    ![Folder Structure](./media/how-to-ci-cd/add-test-project.png)

5. <span data-ttu-id="a18c5-137">In the **FilterModuleTest** folder, update the file name of **UnitTest1.cs** to **FilterModuleTest.cs**.</span><span class="sxs-lookup"><span data-stu-id="a18c5-137">In the **FilterModuleTest** folder, update the file name of **UnitTest1.cs** to **FilterModuleTest.cs**.</span></span> <span data-ttu-id="a18c5-138">Select and open **FilterModuleTest.cs**, replace the entire code with below code snippet, which contains the unit tests against the FilterModule project.</span><span class="sxs-lookup"><span data-stu-id="a18c5-138">Select and open **FilterModuleTest.cs**, replace the entire code with below code snippet, which contains the unit tests against the FilterModule project.</span></span>

    ```csharp
    using Xunit;
    using FilterModule;
    using Newtonsoft.Json;
    using System;
    using System.IO;
    using System.Runtime.InteropServices;
    using System.Runtime.Loader;
    using System.Security.Cryptography.X509Certificates;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.Azure.Devices.Client;
    using Microsoft.Azure.Devices.Client.Transport.Mqtt;

    namespace FilterModuleTest
    {
        public class FilterModuleTest
        {
            [Fact]
            public void filterLessThanThresholdTest()
            {
                var source = createMessage(25 - 1);
                var result = Program.filter(source);
                Assert.True(result == null);
            }

            [Fact]
            public void filterMoreThanThresholdAlertPropertyTest()
            {
                var source = createMessage(25 + 1);
                var result = Program.filter(source);
                Assert.True(result.Properties["MessageType"] == "Alert");
            }

            [Fact]
            public void filterMoreThanThresholdCopyPropertyTest()
            {
                var source = createMessage(25 + 1);
                source.Properties.Add("customTestKey", "customTestValue");
                var result = Program.filter(source);
                Assert.True(result.Properties["customTestKey"] == "customTestValue");
            }

            private Message createMessage(int temperature)
            {
                var messageBody = createMessageBody(temperature);
                var messageString = JsonConvert.SerializeObject(messageBody);
                var messageBytes = Encoding.UTF8.GetBytes(messageString);
                return new Message(messageBytes);
            }

            private MessageBody createMessageBody(int temperature)
            {
                var messageBody = new MessageBody
                {
                    machine = new Machine
                    {
                        temperature = temperature,
                        pressure = 0
                    },
                    ambient = new Ambient
                    {
                        temperature = 0,
                        humidity = 0
                    },
                    timeCreated = string.Format("{0:O}", DateTime.Now)
                };

                return messageBody;
            }
        }
    }
    ```

6. <span data-ttu-id="a18c5-139">In integrated terminal, you can enter following commands to run unit tests locally.</span><span class="sxs-lookup"><span data-stu-id="a18c5-139">In integrated terminal, you can enter following commands to run unit tests locally.</span></span> 
    ```cmd
    dotnet test
    ```

    ![Unit Test](./media/how-to-ci-cd/unit-test.png)

7. <span data-ttu-id="a18c5-141">Save these projects, then check it into your Azure DevOps or TFS repository.</span><span class="sxs-lookup"><span data-stu-id="a18c5-141">Save these projects, then check it into your Azure DevOps or TFS repository.</span></span>
    

> [!NOTE]
> <span data-ttu-id="a18c5-142">For more information about using Azure Repos, see [Share your code with Visual Studio and Azure Repos](https://docs.microsoft.com/azure/devops/repos/git/share-your-code-in-git-vs?view=vsts).</span><span class="sxs-lookup"><span data-stu-id="a18c5-142">For more information about using Azure Repos, see [Share your code with Visual Studio and Azure Repos](https://docs.microsoft.com/azure/devops/repos/git/share-your-code-in-git-vs?view=vsts).</span></span>


## <a name="configure-continuous-integration"></a><span data-ttu-id="a18c5-143">Configure continuous integration</span><span class="sxs-lookup"><span data-stu-id="a18c5-143">Configure continuous integration</span></span>
<span data-ttu-id="a18c5-144">In this section, you will create a build pipeline that is configured to run automatically when you check in any changes to the sample IoT Edge solution, and it will automatically execute the unit tests it contains.</span><span class="sxs-lookup"><span data-stu-id="a18c5-144">In this section, you will create a build pipeline that is configured to run automatically when you check in any changes to the sample IoT Edge solution, and it will automatically execute the unit tests it contains.</span></span>

1. <span data-ttu-id="a18c5-145">Sign into your Azure DevOps organization (**https://**_your-account_**.visualstudio.com**) and open the project where you checked in the sample app.</span><span class="sxs-lookup"><span data-stu-id="a18c5-145">Sign into your Azure DevOps organization (**https://**_your-account_**.visualstudio.com**) and open the project where you checked in the sample app.</span></span>

    ![Check-in code](./media/how-to-ci-cd/init-project.png)

1. <span data-ttu-id="a18c5-147">Visit [Azure IoT Edge For Azure DevOps](https://marketplace.visualstudio.com/items?itemName=vsc-iot.iot-edge-build-deploy) on Azure DevOps Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a18c5-147">Visit [Azure IoT Edge For Azure DevOps](https://marketplace.visualstudio.com/items?itemName=vsc-iot.iot-edge-build-deploy) on Azure DevOps Marketplace.</span></span> <span data-ttu-id="a18c5-148">Click **Get it free** and follow the wizard to install this extension to your Azure DevOps organization or download to your TFS.</span><span class="sxs-lookup"><span data-stu-id="a18c5-148">Click **Get it free** and follow the wizard to install this extension to your Azure DevOps organization or download to your TFS.</span></span>

    ![Install extension](./media/how-to-ci-cd/install-extension.png)

1. <span data-ttu-id="a18c5-150">In your Azure DevOps, open the **Build &amp; Release** hub and, in the **Builds** tab, choose **+ New pipeline**.</span><span class="sxs-lookup"><span data-stu-id="a18c5-150">In your Azure DevOps, open the **Build &amp; Release** hub and, in the **Builds** tab, choose **+ New pipeline**.</span></span> <span data-ttu-id="a18c5-151">Or, if you already have build pipelines, choose the **+ New** button.</span><span class="sxs-lookup"><span data-stu-id="a18c5-151">Or, if you already have build pipelines, choose the **+ New** button.</span></span> 

    ![New build](./media/how-to-ci-cd/add-new-build.png)

1. <span data-ttu-id="a18c5-153">If prompted, select the **Azure DevOps Git** source type; then select the project, repository, and branch where your code is located.</span><span class="sxs-lookup"><span data-stu-id="a18c5-153">If prompted, select the **Azure DevOps Git** source type; then select the project, repository, and branch where your code is located.</span></span> <span data-ttu-id="a18c5-154">Choose **Continue**.</span><span class="sxs-lookup"><span data-stu-id="a18c5-154">Choose **Continue**.</span></span>

    ![Select Azure DevOps git](./media/how-to-ci-cd/select-vsts-git.png)

1. <span data-ttu-id="a18c5-156">In **Select a template** window, choose **start with an Empty process**.</span><span class="sxs-lookup"><span data-stu-id="a18c5-156">In **Select a template** window, choose **start with an Empty process**.</span></span>

    ![Start empty](./media/how-to-ci-cd/start-with-empty.png)

1. <span data-ttu-id="a18c5-158">Click **+** on the right side of **Phase 1** to add a task to the phase.</span><span class="sxs-lookup"><span data-stu-id="a18c5-158">Click **+** on the right side of **Phase 1** to add a task to the phase.</span></span> <span data-ttu-id="a18c5-159">Then search and select **.Net Core**, and click **Add** to add this task to the phase.</span><span class="sxs-lookup"><span data-stu-id="a18c5-159">Then search and select **.Net Core**, and click **Add** to add this task to the phase.</span></span>

    ![Dotnet test](./media/how-to-ci-cd/add-dot-net-core.png)

1. <span data-ttu-id="a18c5-161">Update the **Display name** to **dotnet test**, and in the **Command** dropdown list, select **test**.</span><span class="sxs-lookup"><span data-stu-id="a18c5-161">Update the **Display name** to **dotnet test**, and in the **Command** dropdown list, select **test**.</span></span> <span data-ttu-id="a18c5-162">Add below path to the **Path to project(s)**.</span><span class="sxs-lookup"><span data-stu-id="a18c5-162">Add below path to the **Path to project(s)**.</span></span>

    ```
    tests/FilterModuleTest/*.csproj
    ```

    ![Configure dotnet test](./media/how-to-ci-cd/dotnet-test.png)

1. <span data-ttu-id="a18c5-164">Click **+** on the right side of **Phase 1** to add a task to the phase.</span><span class="sxs-lookup"><span data-stu-id="a18c5-164">Click **+** on the right side of **Phase 1** to add a task to the phase.</span></span> <span data-ttu-id="a18c5-165">Then search and select **Azure IoT Edge**, and click **Add** button **twice** to add these tasks to the phase.</span><span class="sxs-lookup"><span data-stu-id="a18c5-165">Then search and select **Azure IoT Edge**, and click **Add** button **twice** to add these tasks to the phase.</span></span>

    ![IoT Edge](./media/how-to-ci-cd/add-azure-iot-edge.png)

1. <span data-ttu-id="a18c5-167">In the first Azure IoT Edge task, update the **Display name** to **Module Build and Push**, and in the **Action** dropdown list, select **Build and Push**.</span><span class="sxs-lookup"><span data-stu-id="a18c5-167">In the first Azure IoT Edge task, update the **Display name** to **Module Build and Push**, and in the **Action** dropdown list, select **Build and Push**.</span></span> <span data-ttu-id="a18c5-168">In the **Module.json File** textbox, add below path to it.</span><span class="sxs-lookup"><span data-stu-id="a18c5-168">In the **Module.json File** textbox, add below path to it.</span></span> <span data-ttu-id="a18c5-169">Then choose **Container Registry Type**, make sure you configure and select the same registry in your code.</span><span class="sxs-lookup"><span data-stu-id="a18c5-169">Then choose **Container Registry Type**, make sure you configure and select the same registry in your code.</span></span> <span data-ttu-id="a18c5-170">This task will build and push all your modules in the solution and publish to the container registry you specified.</span><span class="sxs-lookup"><span data-stu-id="a18c5-170">This task will build and push all your modules in the solution and publish to the container registry you specified.</span></span> <span data-ttu-id="a18c5-171">If your modules will be pushed to different registries, you can have multiple **Module Build and Push** tasks.</span><span class="sxs-lookup"><span data-stu-id="a18c5-171">If your modules will be pushed to different registries, you can have multiple **Module Build and Push** tasks.</span></span>

    ```
    **/module.json
    ```

    ![Module Build and Push](./media/how-to-ci-cd/module-build-push.png)

1. <span data-ttu-id="a18c5-173">In the second Azure IoT Edge task, update the **Display name** to **Deploy to IoT Edge device**, and in the **Action** dropdown list, select **Deploy to IoT Edge device**.</span><span class="sxs-lookup"><span data-stu-id="a18c5-173">In the second Azure IoT Edge task, update the **Display name** to **Deploy to IoT Edge device**, and in the **Action** dropdown list, select **Deploy to IoT Edge device**.</span></span> <span data-ttu-id="a18c5-174">Select your Azure subscription and input your IoT Hub name.</span><span class="sxs-lookup"><span data-stu-id="a18c5-174">Select your Azure subscription and input your IoT Hub name.</span></span> <span data-ttu-id="a18c5-175">You can specify an IoT Edge deployment ID and the deployment priority.</span><span class="sxs-lookup"><span data-stu-id="a18c5-175">You can specify an IoT Edge deployment ID and the deployment priority.</span></span> <span data-ttu-id="a18c5-176">You can also choose to deploy to single or multiple devices.</span><span class="sxs-lookup"><span data-stu-id="a18c5-176">You can also choose to deploy to single or multiple devices.</span></span> <span data-ttu-id="a18c5-177">If you are deploying to multiple devices, you need to specify the device target condition.</span><span class="sxs-lookup"><span data-stu-id="a18c5-177">If you are deploying to multiple devices, you need to specify the device target condition.</span></span> <span data-ttu-id="a18c5-178">For example, if you want to use device Tags as the condition, you need to update your corresponding devices Tags before the deployment.</span><span class="sxs-lookup"><span data-stu-id="a18c5-178">For example, if you want to use device Tags as the condition, you need to update your corresponding devices Tags before the deployment.</span></span> 

    ![Deploy to Edge](./media/how-to-ci-cd/deploy-to-edge.png)

1. <span data-ttu-id="a18c5-180">Click the **Process** and make sure your **Agent queue** is **Hosted Linux Preview**.</span><span class="sxs-lookup"><span data-stu-id="a18c5-180">Click the **Process** and make sure your **Agent queue** is **Hosted Linux Preview**.</span></span>

    ![Configure](./media/how-to-ci-cd/configure-env.png)

1. <span data-ttu-id="a18c5-182">Open the **Triggers** tab and turn on the **Continuous integration** trigger.</span><span class="sxs-lookup"><span data-stu-id="a18c5-182">Open the **Triggers** tab and turn on the **Continuous integration** trigger.</span></span> <span data-ttu-id="a18c5-183">Make sure the branch containing your code is included.</span><span class="sxs-lookup"><span data-stu-id="a18c5-183">Make sure the branch containing your code is included.</span></span>

    ![Trigger](./media/how-to-ci-cd/configure-trigger.png)

1. <span data-ttu-id="a18c5-185">Save the new build pipeline and queue a new build.</span><span class="sxs-lookup"><span data-stu-id="a18c5-185">Save the new build pipeline and queue a new build.</span></span> <span data-ttu-id="a18c5-186">Click the **Save & queue** button.</span><span class="sxs-lookup"><span data-stu-id="a18c5-186">Click the **Save & queue** button.</span></span>

1. <span data-ttu-id="a18c5-187">Choose the link to the build in the message bar that appears.</span><span class="sxs-lookup"><span data-stu-id="a18c5-187">Choose the link to the build in the message bar that appears.</span></span> <span data-ttu-id="a18c5-188">Or go to build pipeline to see the latest queued build job.</span><span class="sxs-lookup"><span data-stu-id="a18c5-188">Or go to build pipeline to see the latest queued build job.</span></span>

    ![Build](./media/how-to-ci-cd/build-def.png)

1. <span data-ttu-id="a18c5-190">After the build has finished, you see the summary for each task and the results in the live log file.</span><span class="sxs-lookup"><span data-stu-id="a18c5-190">After the build has finished, you see the summary for each task and the results in the live log file.</span></span> 
    
    ![Complete](./media/how-to-ci-cd/complete.png)

1. <span data-ttu-id="a18c5-192">You can go back to VS Code and check the IoT Hub device explorer.</span><span class="sxs-lookup"><span data-stu-id="a18c5-192">You can go back to VS Code and check the IoT Hub device explorer.</span></span> <span data-ttu-id="a18c5-193">The Edge device with the module should start running (Make sure you've added registry credentials to Edge runtime).</span><span class="sxs-lookup"><span data-stu-id="a18c5-193">The Edge device with the module should start running (Make sure you've added registry credentials to Edge runtime).</span></span>

    ![Edge running](./media/how-to-ci-cd/edge-running.png)

## <a name="continuous-deployment-to-iot-edge-devices"></a><span data-ttu-id="a18c5-195">Continuous deployment to IoT Edge devices</span><span class="sxs-lookup"><span data-stu-id="a18c5-195">Continuous deployment to IoT Edge devices</span></span>

<span data-ttu-id="a18c5-196">To enable continuous deployment, basically you need to set up CI jobs with proper IoT Edge devices, enabling the **Triggers** for your branches in your project.</span><span class="sxs-lookup"><span data-stu-id="a18c5-196">To enable continuous deployment, basically you need to set up CI jobs with proper IoT Edge devices, enabling the **Triggers** for your branches in your project.</span></span> <span data-ttu-id="a18c5-197">In a classic DevOps practice, a project contains two main branches.</span><span class="sxs-lookup"><span data-stu-id="a18c5-197">In a classic DevOps practice, a project contains two main branches.</span></span> <span data-ttu-id="a18c5-198">The master branch should be the stable version of the code, and the develop branch contains the latest code changes.</span><span class="sxs-lookup"><span data-stu-id="a18c5-198">The master branch should be the stable version of the code, and the develop branch contains the latest code changes.</span></span> <span data-ttu-id="a18c5-199">Every developer in the team should fork develop branch to his or her own feature branch when starting updating the code, which means all commits happens on feature branches off the develop branch.</span><span class="sxs-lookup"><span data-stu-id="a18c5-199">Every developer in the team should fork develop branch to his or her own feature branch when starting updating the code, which means all commits happens on feature branches off the develop branch.</span></span> <span data-ttu-id="a18c5-200">And every pushed commit should be tested via the CI system.</span><span class="sxs-lookup"><span data-stu-id="a18c5-200">And every pushed commit should be tested via the CI system.</span></span> <span data-ttu-id="a18c5-201">After fully tested the code locally, the feature branch should be merged to the develop branch via a pull request.</span><span class="sxs-lookup"><span data-stu-id="a18c5-201">After fully tested the code locally, the feature branch should be merged to the develop branch via a pull request.</span></span> <span data-ttu-id="a18c5-202">When the code on developer branch is tested via CI system, it can be merged to master branch via a pull request.</span><span class="sxs-lookup"><span data-stu-id="a18c5-202">When the code on developer branch is tested via CI system, it can be merged to master branch via a pull request.</span></span>

<span data-ttu-id="a18c5-203">So, when deploying to IoT Edge devices, there are three main environments.</span><span class="sxs-lookup"><span data-stu-id="a18c5-203">So, when deploying to IoT Edge devices, there are three main environments.</span></span>
- <span data-ttu-id="a18c5-204">On feature branch, you can use simulated IoT Edge device on your development machine or deploy to a physical IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="a18c5-204">On feature branch, you can use simulated IoT Edge device on your development machine or deploy to a physical IoT Edge device.</span></span>
- <span data-ttu-id="a18c5-205">On develop branch, you should deploy to a physical IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="a18c5-205">On develop branch, you should deploy to a physical IoT Edge device.</span></span>
- <span data-ttu-id="a18c5-206">On master branch, the target IoT Edge devices should be the production devices.</span><span class="sxs-lookup"><span data-stu-id="a18c5-206">On master branch, the target IoT Edge devices should be the production devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a18c5-207">Next steps</span><span class="sxs-lookup"><span data-stu-id="a18c5-207">Next steps</span></span>

* <span data-ttu-id="a18c5-208">Understand the IoT Edge deployment in [Understand IoT Edge deployments for single devices or at scale](module-deployment-monitoring.md)</span><span class="sxs-lookup"><span data-stu-id="a18c5-208">Understand the IoT Edge deployment in [Understand IoT Edge deployments for single devices or at scale](module-deployment-monitoring.md)</span></span>
* <span data-ttu-id="a18c5-209">Walk through the steps to create, update, or delete a deployment in [Deploy and monitor IoT Edge modules at scale](how-to-deploy-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="a18c5-209">Walk through the steps to create, update, or delete a deployment in [Deploy and monitor IoT Edge modules at scale](how-to-deploy-monitor.md).</span></span>
