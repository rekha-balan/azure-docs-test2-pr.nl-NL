---
title: Connnect a Raspberry Pi to your Azure IoT Central application (C#) | Microsoft Docs
description: As an device developer, how to connect a Raspberry Pi to your Azure IoT Central application using C#.
author: dominicbetts
ms.author: dobett
ms.date: 01/22/2018
ms.topic: conceptual
ms.service: iot-central
services: iot-central
manager: timlt
ms.openlocfilehash: 63843797cca7fe84cdb9ce91d2282b1c0c288f0c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864472"
---
# <a name="connect-a-raspberry-pi-to-your-azure-iot-central-application-c"></a><span data-ttu-id="8dad9-103">Connect a Raspberry Pi to your Azure IoT Central application (C#)</span><span class="sxs-lookup"><span data-stu-id="8dad9-103">Connect a Raspberry Pi to your Azure IoT Central application (C#)</span></span>

[!INCLUDE [howto-raspberrypi-selector](../../includes/iot-central-howto-raspberrypi-selector.md)]

<span data-ttu-id="8dad9-104">This article describes how, as a device developer, to connect a Raspberry Pi to your Microsoft Azure IoT Central application using the C# programming language.</span><span class="sxs-lookup"><span data-stu-id="8dad9-104">This article describes how, as a device developer, to connect a Raspberry Pi to your Microsoft Azure IoT Central application using the C# programming language.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8dad9-105">Before you begin</span><span class="sxs-lookup"><span data-stu-id="8dad9-105">Before you begin</span></span>

<span data-ttu-id="8dad9-106">To complete the steps in this article, you need the following:</span><span class="sxs-lookup"><span data-stu-id="8dad9-106">To complete the steps in this article, you need the following:</span></span>

* <span data-ttu-id="8dad9-107">[.NET Core 2](https://www.microsoft.com/net) installed on your development machine.</span><span class="sxs-lookup"><span data-stu-id="8dad9-107">[.NET Core 2](https://www.microsoft.com/net) installed on your development machine.</span></span> <span data-ttu-id="8dad9-108">You should also have a suitable code editor such as [Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="8dad9-108">You should also have a suitable code editor such as [Visual Studio Code](https://code.visualstudio.com/).</span></span>
* <span data-ttu-id="8dad9-109">An Azure IoT Central application created from the **Sample Devkits** application template.</span><span class="sxs-lookup"><span data-stu-id="8dad9-109">An Azure IoT Central application created from the **Sample Devkits** application template.</span></span> <span data-ttu-id="8dad9-110">For more information, see [Create your Azure IoT Central Application](howto-create-application.md).</span><span class="sxs-lookup"><span data-stu-id="8dad9-110">For more information, see [Create your Azure IoT Central Application](howto-create-application.md).</span></span>
* <span data-ttu-id="8dad9-111">A Raspberry Pi device running the Raspbian operating system.</span><span class="sxs-lookup"><span data-stu-id="8dad9-111">A Raspberry Pi device running the Raspbian operating system.</span></span>


## <a name="sample-devkits-application"></a><span data-ttu-id="8dad9-112">**Sample Devkits** application</span><span class="sxs-lookup"><span data-stu-id="8dad9-112">**Sample Devkits** application</span></span>

<span data-ttu-id="8dad9-113">An application created from the **Sample Devkits** application template includes a **Raspberry Pi** device template with the following characteristics:</span><span class="sxs-lookup"><span data-stu-id="8dad9-113">An application created from the **Sample Devkits** application template includes a **Raspberry Pi** device template with the following characteristics:</span></span> 

- <span data-ttu-id="8dad9-114">Telemetry which contains the measurements for the device **Humidity**, **Temperature**, **Pressure**, **Magnometer** (measured along X, Y, Z axis), **Accelorometer** (measured along X, Y, Z axis) and **Gyroscope** (measured along X, Y, Z axis).</span><span class="sxs-lookup"><span data-stu-id="8dad9-114">Telemetry which contains the measurements for the device **Humidity**, **Temperature**, **Pressure**, **Magnometer** (measured along X, Y, Z axis), **Accelorometer** (measured along X, Y, Z axis) and **Gyroscope** (measured along X, Y, Z axis).</span></span>
- <span data-ttu-id="8dad9-115">Settings showing **Voltage**, **Current**,**Fan Speed** and an **IR** toggle.</span><span class="sxs-lookup"><span data-stu-id="8dad9-115">Settings showing **Voltage**, **Current**,**Fan Speed** and an **IR** toggle.</span></span>
- <span data-ttu-id="8dad9-116">Properties containing device property **die number** and **location** cloud property.</span><span class="sxs-lookup"><span data-stu-id="8dad9-116">Properties containing device property **die number** and **location** cloud property.</span></span>


<span data-ttu-id="8dad9-117">For full details on the configuration of the device template refer to [Raspberry PI Device template details](howto-connect-raspberry-pi-csharp.md#raspberry-pi-device-template-details)</span><span class="sxs-lookup"><span data-stu-id="8dad9-117">For full details on the configuration of the device template refer to [Raspberry PI Device template details](howto-connect-raspberry-pi-csharp.md#raspberry-pi-device-template-details)</span></span>


## <a name="add-a-real-device"></a><span data-ttu-id="8dad9-118">Add a real device</span><span class="sxs-lookup"><span data-stu-id="8dad9-118">Add a real device</span></span>

<span data-ttu-id="8dad9-119">In your Azure IoT Central application, add a real device from the **Raspberry Pi** device template and make a note of the device connection string.</span><span class="sxs-lookup"><span data-stu-id="8dad9-119">In your Azure IoT Central application, add a real device from the **Raspberry Pi** device template and make a note of the device connection string.</span></span> <span data-ttu-id="8dad9-120">For more information, see [Add a real device to your Azure IoT Central application](tutorial-add-device.md).</span><span class="sxs-lookup"><span data-stu-id="8dad9-120">For more information, see [Add a real device to your Azure IoT Central application](tutorial-add-device.md).</span></span>

### <a name="create-your-net-application"></a><span data-ttu-id="8dad9-121">Create your .NET application</span><span class="sxs-lookup"><span data-stu-id="8dad9-121">Create your .NET application</span></span>

<span data-ttu-id="8dad9-122">You create and test the device application on your desktop machine.</span><span class="sxs-lookup"><span data-stu-id="8dad9-122">You create and test the device application on your desktop machine.</span></span>

<span data-ttu-id="8dad9-123">To complete the following steps, you can use Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="8dad9-123">To complete the following steps, you can use Visual Studio Code.</span></span> <span data-ttu-id="8dad9-124">For more information, see [Working with C#](https://code.visualstudio.com/docs/languages/csharp).</span><span class="sxs-lookup"><span data-stu-id="8dad9-124">For more information, see [Working with C#](https://code.visualstudio.com/docs/languages/csharp).</span></span>

> [!NOTE]
> <span data-ttu-id="8dad9-125">If you prefer, you can complete the following steps using a different code editor.</span><span class="sxs-lookup"><span data-stu-id="8dad9-125">If you prefer, you can complete the following steps using a different code editor.</span></span>

1. <span data-ttu-id="8dad9-126">To initialize your .NET project and add the required NuGet packages, run the following commands:</span><span class="sxs-lookup"><span data-stu-id="8dad9-126">To initialize your .NET project and add the required NuGet packages, run the following commands:</span></span>

  ```cmd/sh
  mkdir pisample
  cd pisample
  dotnet new console
  dotnet add package Microsoft.Azure.Devices.Client
  dotnet restore
  ```

1. <span data-ttu-id="8dad9-127">Open the `pisample` folder in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="8dad9-127">Open the `pisample` folder in Visual Studio Code.</span></span> <span data-ttu-id="8dad9-128">Then open the **pisample.csproj** project file.</span><span class="sxs-lookup"><span data-stu-id="8dad9-128">Then open the **pisample.csproj** project file.</span></span> <span data-ttu-id="8dad9-129">Add the `<RuntimeIdentifiers>` tag shown in the following snippet:</span><span class="sxs-lookup"><span data-stu-id="8dad9-129">Add the `<RuntimeIdentifiers>` tag shown in the following snippet:</span></span>

    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
      <PropertyGroup>
        <OutputType>Exe</OutputType>
        <TargetFramework>netcoreapp2.0</TargetFramework>
        <RuntimeIdentifiers>win-arm;linux-arm</RuntimeIdentifiers>
      </PropertyGroup>
      <ItemGroup>
        <PackageReference Include="Microsoft.Azure.Devices.Client" Version="1.5.2" />
      </ItemGroup>
    </Project>
    ```

    > [!NOTE]
    > <span data-ttu-id="8dad9-130">Your **Microsoft.Azure.Devices.Client** package version number may be higher than the one shown.</span><span class="sxs-lookup"><span data-stu-id="8dad9-130">Your **Microsoft.Azure.Devices.Client** package version number may be higher than the one shown.</span></span>

1. <span data-ttu-id="8dad9-131">Save **pisample.csproj**.</span><span class="sxs-lookup"><span data-stu-id="8dad9-131">Save **pisample.csproj**.</span></span> <span data-ttu-id="8dad9-132">If Visual Studio Code prompts you to execute the restore command, choose **Restore**.</span><span class="sxs-lookup"><span data-stu-id="8dad9-132">If Visual Studio Code prompts you to execute the restore command, choose **Restore**.</span></span>

1. <span data-ttu-id="8dad9-133">Open **Program.cs** and replace the contents with the following code:</span><span class="sxs-lookup"><span data-stu-id="8dad9-133">Open **Program.cs** and replace the contents with the following code:</span></span>

    ```csharp
    using System;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;

    using Microsoft.Azure.Devices.Client;
    using Microsoft.Azure.Devices.Shared;
    using Newtonsoft.Json;

    namespace pisample
    {
      class Program
      {
        static string DeviceConnectionString = "{your device connection string}";
        static DeviceClient Client = null;
        static TwinCollection reportedProperties = new TwinCollection();
        static CancellationTokenSource cts;
        static double baseTemperature = 60;
        static double basePressure = 500;
        static double baseHumidity = 50;
        static void Main(string[] args)
        {
          Console.WriteLine("Raspberry Pi Azure IoT Central example");

          try
          {
            InitClient();
            SendDeviceProperties();

            cts = new CancellationTokenSource();
            SendTelemetryAsync(cts.Token);

            Console.WriteLine("Wait for settings update...");
            Client.SetDesiredPropertyUpdateCallbackAsync(HandleSettingChanged, null).Wait();
            Console.ReadKey();
            cts.Cancel();
          }
          catch (Exception ex)
          {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
          }
        }

        public static void InitClient()
        {
          try
          {
            Console.WriteLine("Connecting to hub");
            Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
          }
          catch (Exception ex)
          {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
          }
        }

        public static async void SendDeviceProperties()
        {
          try
          {
            Console.WriteLine("Sending device properties:");
            Random random = new Random();
            TwinCollection telemetryConfig = new TwinCollection();
            reportedProperties["dieNumber"] = random.Next(1, 6);
            Console.WriteLine(JsonConvert.SerializeObject(reportedProperties));

            await Client.UpdateReportedPropertiesAsync(reportedProperties);
          }
          catch (Exception ex)
          {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
          }
        }

        private static async void SendTelemetryAsync(CancellationToken token)
        {
          try
          {
            Random rand = new Random();

            while (true)
            {
              double currentTemperature = baseTemperature + rand.NextDouble() * 20;
              double currentPressure = basePressure + rand.NextDouble() * 100;
              double currentHumidity = baseHumidity + rand.NextDouble() * 20;

              var telemetryDataPoint = new
              {
                humidity = currentHumidity,
                pressure = currentPressure,
                temp = currentTemperature
              };
              var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
              var message = new Message(Encoding.ASCII.GetBytes(messageString));

              token.ThrowIfCancellationRequested();
              await Client.SendEventAsync(message);

              Console.WriteLine("{0} > Sending telemetry: {1}", DateTime.Now, messageString);

              await Task.Delay(1000);
            }
          }
          catch (Exception ex)
          {
            Console.WriteLine();
            Console.WriteLine("Intentional shutdown: {0}", ex.Message);
          }
        }

        private static async Task HandleSettingChanged(TwinCollection desiredProperties, object userContext)
        {
          try
          {
            Console.WriteLine("Received settings change...");
            Console.WriteLine(JsonConvert.SerializeObject(desiredProperties));

            string setting = "fanSpeed";
            if (desiredProperties.Contains(setting))
            {
              // Act on setting change, then
              AcknowledgeSettingChange(desiredProperties, setting);
            }
            setting = "setVoltage";
            if (desiredProperties.Contains(setting))
            {
              // Act on setting change, then
              AcknowledgeSettingChange(desiredProperties, setting);
            }
            setting = "setCurrent";
            if (desiredProperties.Contains(setting))
            {
              // Act on setting change, then
              AcknowledgeSettingChange(desiredProperties, setting);
            }
            setting = "activateIR";
            if (desiredProperties.Contains(setting))
            {
              // Act on setting change, then
              AcknowledgeSettingChange(desiredProperties, setting);
            }
            await Client.UpdateReportedPropertiesAsync(reportedProperties);
          }

          catch (Exception ex)
          {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
          }
        }

        private static void AcknowledgeSettingChange(TwinCollection desiredProperties, string setting)
        {
          reportedProperties[setting] = new
          {
            value = desiredProperties[setting]["value"],
            status = "completed",
            desiredVersion = desiredProperties["$version"],
            message = "Processed"
          };
        }
      }
    }
    ```

    > [!NOTE]
    > <span data-ttu-id="8dad9-134">You update the placeholder `{your device connection string}` in the next step.</span><span class="sxs-lookup"><span data-stu-id="8dad9-134">You update the placeholder `{your device connection string}` in the next step.</span></span>

## <a name="run-your-net-application"></a><span data-ttu-id="8dad9-135">Run your .NET application</span><span class="sxs-lookup"><span data-stu-id="8dad9-135">Run your .NET application</span></span>

<span data-ttu-id="8dad9-136">Add your device-specific connection string to the code for the device to authenticate with Azure IoT Central.</span><span class="sxs-lookup"><span data-stu-id="8dad9-136">Add your device-specific connection string to the code for the device to authenticate with Azure IoT Central.</span></span> <span data-ttu-id="8dad9-137">You made a note of this connection string when you added your real device to your Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="8dad9-137">You made a note of this connection string when you added your real device to your Azure IoT Central application.</span></span>

1. <span data-ttu-id="8dad9-138">Replace `{your device connection string}` in the **Program.cs** file with the connection string you noted previously.</span><span class="sxs-lookup"><span data-stu-id="8dad9-138">Replace `{your device connection string}` in the **Program.cs** file with the connection string you noted previously.</span></span>

1. <span data-ttu-id="8dad9-139">Run the following command in your command-line environment:</span><span class="sxs-lookup"><span data-stu-id="8dad9-139">Run the following command in your command-line environment:</span></span>

  ```cmd/sh
  dotnet restore
  dotnet publish -r linux-arm
  ```

1. <span data-ttu-id="8dad9-140">Copy the `pisample\bin\Debug\netcoreapp2.0\linux-arm\publish` folder to your Raspberry Pi device.</span><span class="sxs-lookup"><span data-stu-id="8dad9-140">Copy the `pisample\bin\Debug\netcoreapp2.0\linux-arm\publish` folder to your Raspberry Pi device.</span></span> <span data-ttu-id="8dad9-141">You can use the **scp** command to copy the files, for example:</span><span class="sxs-lookup"><span data-stu-id="8dad9-141">You can use the **scp** command to copy the files, for example:</span></span>

    ```cmd/sh
    scp -r publish pi@192.168.0.40:publish
    ```

    <span data-ttu-id="8dad9-142">For more information, see [Raspberry Pi remote access](https://www.raspberrypi.org/documentation/remote-access/).</span><span class="sxs-lookup"><span data-stu-id="8dad9-142">For more information, see [Raspberry Pi remote access](https://www.raspberrypi.org/documentation/remote-access/).</span></span>

1. <span data-ttu-id="8dad9-143">Sign in to your Raspberry Pi device and run the following commands in a shell:</span><span class="sxs-lookup"><span data-stu-id="8dad9-143">Sign in to your Raspberry Pi device and run the following commands in a shell:</span></span>

    ```cmd/sh
    sudo apt-get update
    sudo apt-get install libc6 libcurl3 libgcc1 libgssapi-krb5-2 liblttng-ust0 libstdc++6 libunwind8 libuuid1 zlib1g
    ```

1. <span data-ttu-id="8dad9-144">On your Raspberry Pi, run the following commands:</span><span class="sxs-lookup"><span data-stu-id="8dad9-144">On your Raspberry Pi, run the following commands:</span></span>

    ```cmd/sh
    cd publish
    chmod 777 pisample
    ./pisample
    ```

    ![Program begins](./media/howto-connect-raspberry-pi-csharp/device_begin.png)

1. <span data-ttu-id="8dad9-146">In your Azure IoT Central application, you can see how the code running on the Raspberry Pi interacts with the application:</span><span class="sxs-lookup"><span data-stu-id="8dad9-146">In your Azure IoT Central application, you can see how the code running on the Raspberry Pi interacts with the application:</span></span>

    * <span data-ttu-id="8dad9-147">On the **Measurements** page for your real device, you can see the telemetry.</span><span class="sxs-lookup"><span data-stu-id="8dad9-147">On the **Measurements** page for your real device, you can see the telemetry.</span></span>
    * <span data-ttu-id="8dad9-148">On the **Properties** page, you can see the value of the reported **Die Number** property.</span><span class="sxs-lookup"><span data-stu-id="8dad9-148">On the **Properties** page, you can see the value of the reported **Die Number** property.</span></span>
    * <span data-ttu-id="8dad9-149">On the **Settings** page, you can change various settings on the Raspberry Pi such as voltage and fan speed.</span><span class="sxs-lookup"><span data-stu-id="8dad9-149">On the **Settings** page, you can change various settings on the Raspberry Pi such as voltage and fan speed.</span></span>

    <span data-ttu-id="8dad9-150">The following screenshot shows the Raspberry Pi receiving the setting change:</span><span class="sxs-lookup"><span data-stu-id="8dad9-150">The following screenshot shows the Raspberry Pi receiving the setting change:</span></span>

    ![Raspberry Pi receives setting change](./media/howto-connect-raspberry-pi-csharp/device_switch.png)


## <a name="raspberry-pi-device-template-details"></a><span data-ttu-id="8dad9-152">Raspberry PI Device template details</span><span class="sxs-lookup"><span data-stu-id="8dad9-152">Raspberry PI Device template details</span></span>

<span data-ttu-id="8dad9-153">An application created from the **Sample Devkits** application template includes a **Raspberry Pi** device template with the following characteristics:</span><span class="sxs-lookup"><span data-stu-id="8dad9-153">An application created from the **Sample Devkits** application template includes a **Raspberry Pi** device template with the following characteristics:</span></span>

### <a name="telemetry-measurements"></a><span data-ttu-id="8dad9-154">Telemetry measurements</span><span class="sxs-lookup"><span data-stu-id="8dad9-154">Telemetry measurements</span></span>

| <span data-ttu-id="8dad9-155">Field name</span><span class="sxs-lookup"><span data-stu-id="8dad9-155">Field name</span></span>     | <span data-ttu-id="8dad9-156">Units</span><span class="sxs-lookup"><span data-stu-id="8dad9-156">Units</span></span>  | <span data-ttu-id="8dad9-157">Minimum</span><span class="sxs-lookup"><span data-stu-id="8dad9-157">Minimum</span></span> | <span data-ttu-id="8dad9-158">Maximum</span><span class="sxs-lookup"><span data-stu-id="8dad9-158">Maximum</span></span> | <span data-ttu-id="8dad9-159">Decimal places</span><span class="sxs-lookup"><span data-stu-id="8dad9-159">Decimal places</span></span> |
| -------------- | ------ | ------- | ------- | -------------- |
| <span data-ttu-id="8dad9-160">humidity</span><span class="sxs-lookup"><span data-stu-id="8dad9-160">humidity</span></span>       | %      | <span data-ttu-id="8dad9-161">0</span><span class="sxs-lookup"><span data-stu-id="8dad9-161">0</span></span>       | <span data-ttu-id="8dad9-162">100</span><span class="sxs-lookup"><span data-stu-id="8dad9-162">100</span></span>     | <span data-ttu-id="8dad9-163">0</span><span class="sxs-lookup"><span data-stu-id="8dad9-163">0</span></span>              |
| <span data-ttu-id="8dad9-164">temp</span><span class="sxs-lookup"><span data-stu-id="8dad9-164">temp</span></span>           | <span data-ttu-id="8dad9-165">°C</span><span class="sxs-lookup"><span data-stu-id="8dad9-165">°C</span></span>     | <span data-ttu-id="8dad9-166">-40</span><span class="sxs-lookup"><span data-stu-id="8dad9-166">-40</span></span>     | <span data-ttu-id="8dad9-167">120</span><span class="sxs-lookup"><span data-stu-id="8dad9-167">120</span></span>     | <span data-ttu-id="8dad9-168">0</span><span class="sxs-lookup"><span data-stu-id="8dad9-168">0</span></span>              |
| <span data-ttu-id="8dad9-169">pressure</span><span class="sxs-lookup"><span data-stu-id="8dad9-169">pressure</span></span>       | <span data-ttu-id="8dad9-170">hPa</span><span class="sxs-lookup"><span data-stu-id="8dad9-170">hPa</span></span>    | <span data-ttu-id="8dad9-171">260</span><span class="sxs-lookup"><span data-stu-id="8dad9-171">260</span></span>     | <span data-ttu-id="8dad9-172">1260</span><span class="sxs-lookup"><span data-stu-id="8dad9-172">1260</span></span>    | <span data-ttu-id="8dad9-173">0</span><span class="sxs-lookup"><span data-stu-id="8dad9-173">0</span></span>              |
| <span data-ttu-id="8dad9-174">magnetometerX</span><span class="sxs-lookup"><span data-stu-id="8dad9-174">magnetometerX</span></span>  | <span data-ttu-id="8dad9-175">mgauss</span><span class="sxs-lookup"><span data-stu-id="8dad9-175">mgauss</span></span> | <span data-ttu-id="8dad9-176">-1000</span><span class="sxs-lookup"><span data-stu-id="8dad9-176">-1000</span></span>   | <span data-ttu-id="8dad9-177">1000</span><span class="sxs-lookup"><span data-stu-id="8dad9-177">1000</span></span>    | <span data-ttu-id="8dad9-178">0</span><span class="sxs-lookup"><span data-stu-id="8dad9-178">0</span></span>              |
| <span data-ttu-id="8dad9-179">magnetometerY</span><span class="sxs-lookup"><span data-stu-id="8dad9-179">magnetometerY</span></span>  | <span data-ttu-id="8dad9-180">mgauss</span><span class="sxs-lookup"><span data-stu-id="8dad9-180">mgauss</span></span> | <span data-ttu-id="8dad9-181">-1000</span><span class="sxs-lookup"><span data-stu-id="8dad9-181">-1000</span></span>   | <span data-ttu-id="8dad9-182">1000</span><span class="sxs-lookup"><span data-stu-id="8dad9-182">1000</span></span>    | <span data-ttu-id="8dad9-183">0</span><span class="sxs-lookup"><span data-stu-id="8dad9-183">0</span></span>              |
| <span data-ttu-id="8dad9-184">magnetometerZ</span><span class="sxs-lookup"><span data-stu-id="8dad9-184">magnetometerZ</span></span>  | <span data-ttu-id="8dad9-185">mgauss</span><span class="sxs-lookup"><span data-stu-id="8dad9-185">mgauss</span></span> | <span data-ttu-id="8dad9-186">-1000</span><span class="sxs-lookup"><span data-stu-id="8dad9-186">-1000</span></span>   | <span data-ttu-id="8dad9-187">1000</span><span class="sxs-lookup"><span data-stu-id="8dad9-187">1000</span></span>    | <span data-ttu-id="8dad9-188">0</span><span class="sxs-lookup"><span data-stu-id="8dad9-188">0</span></span>              |
| <span data-ttu-id="8dad9-189">accelerometerX</span><span class="sxs-lookup"><span data-stu-id="8dad9-189">accelerometerX</span></span> | <span data-ttu-id="8dad9-190">mg</span><span class="sxs-lookup"><span data-stu-id="8dad9-190">mg</span></span>     | <span data-ttu-id="8dad9-191">-2000</span><span class="sxs-lookup"><span data-stu-id="8dad9-191">-2000</span></span>   | <span data-ttu-id="8dad9-192">2000</span><span class="sxs-lookup"><span data-stu-id="8dad9-192">2000</span></span>    | <span data-ttu-id="8dad9-193">0</span><span class="sxs-lookup"><span data-stu-id="8dad9-193">0</span></span>              |
| <span data-ttu-id="8dad9-194">accelerometerY</span><span class="sxs-lookup"><span data-stu-id="8dad9-194">accelerometerY</span></span> | <span data-ttu-id="8dad9-195">mg</span><span class="sxs-lookup"><span data-stu-id="8dad9-195">mg</span></span>     | <span data-ttu-id="8dad9-196">-2000</span><span class="sxs-lookup"><span data-stu-id="8dad9-196">-2000</span></span>   | <span data-ttu-id="8dad9-197">2000</span><span class="sxs-lookup"><span data-stu-id="8dad9-197">2000</span></span>    | <span data-ttu-id="8dad9-198">0</span><span class="sxs-lookup"><span data-stu-id="8dad9-198">0</span></span>              |
| <span data-ttu-id="8dad9-199">accelerometerZ</span><span class="sxs-lookup"><span data-stu-id="8dad9-199">accelerometerZ</span></span> | <span data-ttu-id="8dad9-200">mg</span><span class="sxs-lookup"><span data-stu-id="8dad9-200">mg</span></span>     | <span data-ttu-id="8dad9-201">-2000</span><span class="sxs-lookup"><span data-stu-id="8dad9-201">-2000</span></span>   | <span data-ttu-id="8dad9-202">2000</span><span class="sxs-lookup"><span data-stu-id="8dad9-202">2000</span></span>    | <span data-ttu-id="8dad9-203">0</span><span class="sxs-lookup"><span data-stu-id="8dad9-203">0</span></span>              |
| <span data-ttu-id="8dad9-204">gyroscopeX</span><span class="sxs-lookup"><span data-stu-id="8dad9-204">gyroscopeX</span></span>     | <span data-ttu-id="8dad9-205">mdps</span><span class="sxs-lookup"><span data-stu-id="8dad9-205">mdps</span></span>   | <span data-ttu-id="8dad9-206">-2000</span><span class="sxs-lookup"><span data-stu-id="8dad9-206">-2000</span></span>   | <span data-ttu-id="8dad9-207">2000</span><span class="sxs-lookup"><span data-stu-id="8dad9-207">2000</span></span>    | <span data-ttu-id="8dad9-208">0</span><span class="sxs-lookup"><span data-stu-id="8dad9-208">0</span></span>              |
| <span data-ttu-id="8dad9-209">gyroscopeY</span><span class="sxs-lookup"><span data-stu-id="8dad9-209">gyroscopeY</span></span>     | <span data-ttu-id="8dad9-210">mdps</span><span class="sxs-lookup"><span data-stu-id="8dad9-210">mdps</span></span>   | <span data-ttu-id="8dad9-211">-2000</span><span class="sxs-lookup"><span data-stu-id="8dad9-211">-2000</span></span>   | <span data-ttu-id="8dad9-212">2000</span><span class="sxs-lookup"><span data-stu-id="8dad9-212">2000</span></span>    | <span data-ttu-id="8dad9-213">0</span><span class="sxs-lookup"><span data-stu-id="8dad9-213">0</span></span>              |
| <span data-ttu-id="8dad9-214">gyroscopeZ</span><span class="sxs-lookup"><span data-stu-id="8dad9-214">gyroscopeZ</span></span>     | <span data-ttu-id="8dad9-215">mdps</span><span class="sxs-lookup"><span data-stu-id="8dad9-215">mdps</span></span>   | <span data-ttu-id="8dad9-216">-2000</span><span class="sxs-lookup"><span data-stu-id="8dad9-216">-2000</span></span>   | <span data-ttu-id="8dad9-217">2000</span><span class="sxs-lookup"><span data-stu-id="8dad9-217">2000</span></span>    | <span data-ttu-id="8dad9-218">0</span><span class="sxs-lookup"><span data-stu-id="8dad9-218">0</span></span>              |

### <a name="settings"></a><span data-ttu-id="8dad9-219">Settings</span><span class="sxs-lookup"><span data-stu-id="8dad9-219">Settings</span></span>

<span data-ttu-id="8dad9-220">Numeric settings</span><span class="sxs-lookup"><span data-stu-id="8dad9-220">Numeric settings</span></span>

| <span data-ttu-id="8dad9-221">Display name</span><span class="sxs-lookup"><span data-stu-id="8dad9-221">Display name</span></span> | <span data-ttu-id="8dad9-222">Field name</span><span class="sxs-lookup"><span data-stu-id="8dad9-222">Field name</span></span> | <span data-ttu-id="8dad9-223">Units</span><span class="sxs-lookup"><span data-stu-id="8dad9-223">Units</span></span> | <span data-ttu-id="8dad9-224">Decimal places</span><span class="sxs-lookup"><span data-stu-id="8dad9-224">Decimal places</span></span> | <span data-ttu-id="8dad9-225">Minimum</span><span class="sxs-lookup"><span data-stu-id="8dad9-225">Minimum</span></span> | <span data-ttu-id="8dad9-226">Maximum</span><span class="sxs-lookup"><span data-stu-id="8dad9-226">Maximum</span></span> | <span data-ttu-id="8dad9-227">Initial</span><span class="sxs-lookup"><span data-stu-id="8dad9-227">Initial</span></span> |
| ------------ | ---------- | ----- | -------------- | ------- | ------- | ------- |
| <span data-ttu-id="8dad9-228">Voltage</span><span class="sxs-lookup"><span data-stu-id="8dad9-228">Voltage</span></span>      | <span data-ttu-id="8dad9-229">setVoltage</span><span class="sxs-lookup"><span data-stu-id="8dad9-229">setVoltage</span></span> | <span data-ttu-id="8dad9-230">Volts</span><span class="sxs-lookup"><span data-stu-id="8dad9-230">Volts</span></span> | <span data-ttu-id="8dad9-231">0</span><span class="sxs-lookup"><span data-stu-id="8dad9-231">0</span></span>              | <span data-ttu-id="8dad9-232">0</span><span class="sxs-lookup"><span data-stu-id="8dad9-232">0</span></span>       | <span data-ttu-id="8dad9-233">240</span><span class="sxs-lookup"><span data-stu-id="8dad9-233">240</span></span>     | <span data-ttu-id="8dad9-234">0</span><span class="sxs-lookup"><span data-stu-id="8dad9-234">0</span></span>       |
| <span data-ttu-id="8dad9-235">Current</span><span class="sxs-lookup"><span data-stu-id="8dad9-235">Current</span></span>      | <span data-ttu-id="8dad9-236">setCurrent</span><span class="sxs-lookup"><span data-stu-id="8dad9-236">setCurrent</span></span> | <span data-ttu-id="8dad9-237">Amps</span><span class="sxs-lookup"><span data-stu-id="8dad9-237">Amps</span></span>  | <span data-ttu-id="8dad9-238">0</span><span class="sxs-lookup"><span data-stu-id="8dad9-238">0</span></span>              | <span data-ttu-id="8dad9-239">0</span><span class="sxs-lookup"><span data-stu-id="8dad9-239">0</span></span>       | <span data-ttu-id="8dad9-240">100</span><span class="sxs-lookup"><span data-stu-id="8dad9-240">100</span></span>     | <span data-ttu-id="8dad9-241">0</span><span class="sxs-lookup"><span data-stu-id="8dad9-241">0</span></span>       |
| <span data-ttu-id="8dad9-242">Fan Speed</span><span class="sxs-lookup"><span data-stu-id="8dad9-242">Fan Speed</span></span>    | <span data-ttu-id="8dad9-243">fanSpeed</span><span class="sxs-lookup"><span data-stu-id="8dad9-243">fanSpeed</span></span>   | <span data-ttu-id="8dad9-244">RPM</span><span class="sxs-lookup"><span data-stu-id="8dad9-244">RPM</span></span>   | <span data-ttu-id="8dad9-245">0</span><span class="sxs-lookup"><span data-stu-id="8dad9-245">0</span></span>              | <span data-ttu-id="8dad9-246">0</span><span class="sxs-lookup"><span data-stu-id="8dad9-246">0</span></span>       | <span data-ttu-id="8dad9-247">1000</span><span class="sxs-lookup"><span data-stu-id="8dad9-247">1000</span></span>    | <span data-ttu-id="8dad9-248">0</span><span class="sxs-lookup"><span data-stu-id="8dad9-248">0</span></span>       |

<span data-ttu-id="8dad9-249">Toggle settings</span><span class="sxs-lookup"><span data-stu-id="8dad9-249">Toggle settings</span></span>

| <span data-ttu-id="8dad9-250">Display name</span><span class="sxs-lookup"><span data-stu-id="8dad9-250">Display name</span></span> | <span data-ttu-id="8dad9-251">Field name</span><span class="sxs-lookup"><span data-stu-id="8dad9-251">Field name</span></span> | <span data-ttu-id="8dad9-252">On text</span><span class="sxs-lookup"><span data-stu-id="8dad9-252">On text</span></span> | <span data-ttu-id="8dad9-253">Off text</span><span class="sxs-lookup"><span data-stu-id="8dad9-253">Off text</span></span> | <span data-ttu-id="8dad9-254">Initial</span><span class="sxs-lookup"><span data-stu-id="8dad9-254">Initial</span></span> |
| ------------ | ---------- | ------- | -------- | ------- |
| <span data-ttu-id="8dad9-255">IR</span><span class="sxs-lookup"><span data-stu-id="8dad9-255">IR</span></span>           | <span data-ttu-id="8dad9-256">activateIR</span><span class="sxs-lookup"><span data-stu-id="8dad9-256">activateIR</span></span> | <span data-ttu-id="8dad9-257">ON</span><span class="sxs-lookup"><span data-stu-id="8dad9-257">ON</span></span>      | <span data-ttu-id="8dad9-258">OFF</span><span class="sxs-lookup"><span data-stu-id="8dad9-258">OFF</span></span>      | <span data-ttu-id="8dad9-259">Off</span><span class="sxs-lookup"><span data-stu-id="8dad9-259">Off</span></span>     |

### <a name="properties"></a><span data-ttu-id="8dad9-260">Properties</span><span class="sxs-lookup"><span data-stu-id="8dad9-260">Properties</span></span>

| <span data-ttu-id="8dad9-261">Type</span><span class="sxs-lookup"><span data-stu-id="8dad9-261">Type</span></span>            | <span data-ttu-id="8dad9-262">Display name</span><span class="sxs-lookup"><span data-stu-id="8dad9-262">Display name</span></span> | <span data-ttu-id="8dad9-263">Field name</span><span class="sxs-lookup"><span data-stu-id="8dad9-263">Field name</span></span> | <span data-ttu-id="8dad9-264">Data type</span><span class="sxs-lookup"><span data-stu-id="8dad9-264">Data type</span></span> |
| --------------- | ------------ | ---------- | --------- |
| <span data-ttu-id="8dad9-265">Device property</span><span class="sxs-lookup"><span data-stu-id="8dad9-265">Device property</span></span> | <span data-ttu-id="8dad9-266">Die number</span><span class="sxs-lookup"><span data-stu-id="8dad9-266">Die number</span></span>   | <span data-ttu-id="8dad9-267">dieNumber</span><span class="sxs-lookup"><span data-stu-id="8dad9-267">dieNumber</span></span>  | <span data-ttu-id="8dad9-268">number</span><span class="sxs-lookup"><span data-stu-id="8dad9-268">number</span></span>    |
| <span data-ttu-id="8dad9-269">Text</span><span class="sxs-lookup"><span data-stu-id="8dad9-269">Text</span></span>            | <span data-ttu-id="8dad9-270">Location</span><span class="sxs-lookup"><span data-stu-id="8dad9-270">Location</span></span>     | <span data-ttu-id="8dad9-271">location</span><span class="sxs-lookup"><span data-stu-id="8dad9-271">location</span></span>   | <span data-ttu-id="8dad9-272">N/A</span><span class="sxs-lookup"><span data-stu-id="8dad9-272">N/A</span></span>       |

## <a name="next-steps"></a><span data-ttu-id="8dad9-273">Next steps</span><span class="sxs-lookup"><span data-stu-id="8dad9-273">Next steps</span></span>

<span data-ttu-id="8dad9-274">Now that you have learned how to connect a Raspberry Pi to your Azure IoT Central application, here are the suggested next steps:</span><span class="sxs-lookup"><span data-stu-id="8dad9-274">Now that you have learned how to connect a Raspberry Pi to your Azure IoT Central application, here are the suggested next steps:</span></span>

* [<span data-ttu-id="8dad9-275">Connect a generic Node.js client application to Azure IoT Central</span><span class="sxs-lookup"><span data-stu-id="8dad9-275">Connect a generic Node.js client application to Azure IoT Central</span></span>](howto-connect-nodejs.md)
