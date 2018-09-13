---
title: Schedule jobs with Azure IoT Hub (Java) | Microsoft Docs
description: How to schedule an Azure IoT Hub job to invoke a direct method and set a desired property on multiple devices. You use the Azure IoT device SDK for Java to implement the simulated device apps and the Azure IoT service SDK for Java to implement a service app to run the job.
author: dominicbetts
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.devlang: java
ms.topic: conceptual
ms.date: 07/10/2017
ms.author: dobett
ms.openlocfilehash: 3161715ac2ff212e2de8a27ff8f8eb53fb858b92
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856532"
---
# <a name="schedule-and-broadcast-jobs-java"></a><span data-ttu-id="b7123-104">Schedule and broadcast jobs (Java)</span><span class="sxs-lookup"><span data-stu-id="b7123-104">Schedule and broadcast jobs (Java)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="b7123-105">Use Azure IoT Hub to schedule and track jobs that update millions of devices.</span><span class="sxs-lookup"><span data-stu-id="b7123-105">Use Azure IoT Hub to schedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="b7123-106">Use jobs to:</span><span class="sxs-lookup"><span data-stu-id="b7123-106">Use jobs to:</span></span>

* <span data-ttu-id="b7123-107">Update desired properties</span><span class="sxs-lookup"><span data-stu-id="b7123-107">Update desired properties</span></span>
* <span data-ttu-id="b7123-108">Update tags</span><span class="sxs-lookup"><span data-stu-id="b7123-108">Update tags</span></span>
* <span data-ttu-id="b7123-109">Invoke direct methods</span><span class="sxs-lookup"><span data-stu-id="b7123-109">Invoke direct methods</span></span>

<span data-ttu-id="b7123-110">A job wraps one of these actions and tracks the execution against a set of devices.</span><span class="sxs-lookup"><span data-stu-id="b7123-110">A job wraps one of these actions and tracks the execution against a set of devices.</span></span> <span data-ttu-id="b7123-111">A device twin query defines the set of devices the job executes against.</span><span class="sxs-lookup"><span data-stu-id="b7123-111">A device twin query defines the set of devices the job executes against.</span></span> <span data-ttu-id="b7123-112">For example, a back-end app can use a job to invoke a direct method on 10,000 devices that reboots the devices.</span><span class="sxs-lookup"><span data-stu-id="b7123-112">For example, a back-end app can use a job to invoke a direct method on 10,000 devices that reboots the devices.</span></span> <span data-ttu-id="b7123-113">You specify the set of devices with a device twin query and schedule the job to run at a future time.</span><span class="sxs-lookup"><span data-stu-id="b7123-113">You specify the set of devices with a device twin query and schedule the job to run at a future time.</span></span> <span data-ttu-id="b7123-114">The job tracks progress as each of the devices receive and execute the reboot direct method.</span><span class="sxs-lookup"><span data-stu-id="b7123-114">The job tracks progress as each of the devices receive and execute the reboot direct method.</span></span>

<span data-ttu-id="b7123-115">To learn more about each of these capabilities, see:</span><span class="sxs-lookup"><span data-stu-id="b7123-115">To learn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="b7123-116">Device twin and properties: [Get started with device twins](iot-hub-java-java-twin-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="b7123-116">Device twin and properties: [Get started with device twins](iot-hub-java-java-twin-getstarted.md)</span></span>
* <span data-ttu-id="b7123-117">Direct methods: [IoT Hub developer guide - direct methods](iot-hub-devguide-direct-methods.md) and [Tutorial: Use direct methods](quickstart-control-device-java.md)</span><span class="sxs-lookup"><span data-stu-id="b7123-117">Direct methods: [IoT Hub developer guide - direct methods](iot-hub-devguide-direct-methods.md) and [Tutorial: Use direct methods](quickstart-control-device-java.md)</span></span>

[!INCLUDE [iot-hub-basic](../../includes/iot-hub-basic-whole.md)]

<span data-ttu-id="b7123-118">This tutorial shows you how to:</span><span class="sxs-lookup"><span data-stu-id="b7123-118">This tutorial shows you how to:</span></span>

* <span data-ttu-id="b7123-119">Create a device app that implements a direct method called **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="b7123-119">Create a device app that implements a direct method called **lockDoor**.</span></span> <span data-ttu-id="b7123-120">The device app also receives desired property changes from the back-end app.</span><span class="sxs-lookup"><span data-stu-id="b7123-120">The device app also receives desired property changes from the back-end app.</span></span>
* <span data-ttu-id="b7123-121">Create a back-end app that creates a job to call the **lockDoor** direct method on multiple devices.</span><span class="sxs-lookup"><span data-stu-id="b7123-121">Create a back-end app that creates a job to call the **lockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="b7123-122">Another job sends desired property updates to multiple devices.</span><span class="sxs-lookup"><span data-stu-id="b7123-122">Another job sends desired property updates to multiple devices.</span></span>

<span data-ttu-id="b7123-123">At the end of this tutorial, you have a java console device app and a java console back-end app:</span><span class="sxs-lookup"><span data-stu-id="b7123-123">At the end of this tutorial, you have a java console device app and a java console back-end app:</span></span>

<span data-ttu-id="b7123-124">**simulated-device** that connects to your IoT hub, implements the **lockDoor** direct method, and handles desired property changes.</span><span class="sxs-lookup"><span data-stu-id="b7123-124">**simulated-device** that connects to your IoT hub, implements the **lockDoor** direct method, and handles desired property changes.</span></span>

<span data-ttu-id="b7123-125">**schedule-jobs** that use jobs to call the **lockDoor** direct method and update the device twin desired properties on multiple devices.</span><span class="sxs-lookup"><span data-stu-id="b7123-125">**schedule-jobs** that use jobs to call the **lockDoor** direct method and update the device twin desired properties on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="b7123-126">The article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span><span class="sxs-lookup"><span data-stu-id="b7123-126">The article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7123-127">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b7123-127">Prerequisites</span></span>

<span data-ttu-id="b7123-128">To complete this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="b7123-128">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="b7123-129">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="b7123-129">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="b7123-130">Maven 3</span><span class="sxs-lookup"><span data-stu-id="b7123-130">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="b7123-131">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="b7123-131">An active Azure account.</span></span> <span data-ttu-id="b7123-132">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="b7123-132">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="b7123-133">You can also use the [IoT extension for Azure CLI 2.0](https://github.com/Azure/azure-iot-cli-extension) tool to add a device to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="b7123-133">You can also use the [IoT extension for Azure CLI 2.0](https://github.com/Azure/azure-iot-cli-extension) tool to add a device to your IoT hub.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="b7123-134">Create the service app</span><span class="sxs-lookup"><span data-stu-id="b7123-134">Create the service app</span></span>

<span data-ttu-id="b7123-135">In this section, you create a Java console app that uses jobs to:</span><span class="sxs-lookup"><span data-stu-id="b7123-135">In this section, you create a Java console app that uses jobs to:</span></span>

* <span data-ttu-id="b7123-136">Call the **lockDoor** direct method on multiple devices.</span><span class="sxs-lookup"><span data-stu-id="b7123-136">Call the **lockDoor** direct method on multiple devices.</span></span>
* <span data-ttu-id="b7123-137">Send desired properties to multiple devices.</span><span class="sxs-lookup"><span data-stu-id="b7123-137">Send desired properties to multiple devices.</span></span>

<span data-ttu-id="b7123-138">To create the app:</span><span class="sxs-lookup"><span data-stu-id="b7123-138">To create the app:</span></span>

1. <span data-ttu-id="b7123-139">On your development machine, create an empty folder called `iot-java-schedule-jobs`.</span><span class="sxs-lookup"><span data-stu-id="b7123-139">On your development machine, create an empty folder called `iot-java-schedule-jobs`.</span></span>

1. <span data-ttu-id="b7123-140">In the `iot-java-schedule-jobs` folder, create a Maven project called **schedule-jobs** using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="b7123-140">In the `iot-java-schedule-jobs` folder, create a Maven project called **schedule-jobs** using the following command at your command prompt.</span></span> <span data-ttu-id="b7123-141">Note this is a single, long command:</span><span class="sxs-lookup"><span data-stu-id="b7123-141">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=schedule-jobs -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="b7123-142">At your command prompt, navigate to the `schedule-jobs` folder.</span><span class="sxs-lookup"><span data-stu-id="b7123-142">At your command prompt, navigate to the `schedule-jobs` folder.</span></span>

1. <span data-ttu-id="b7123-143">Using a text editor, open the `pom.xml` file in the `schedule-jobs` folder and add the following dependency to the **dependencies** node.</span><span class="sxs-lookup"><span data-stu-id="b7123-143">Using a text editor, open the `pom.xml` file in the `schedule-jobs` folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="b7123-144">This dependency enables you to use the **iot-service-client** package in your app to communicate with your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="b7123-144">This dependency enables you to use the **iot-service-client** package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="b7123-145">You can check for the latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="b7123-145">You can check for the latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="b7123-146">Add the following **build** node after the **dependencies** node.</span><span class="sxs-lookup"><span data-stu-id="b7123-146">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="b7123-147">This configuration instructs Maven to use Java 1.8 to build the app:</span><span class="sxs-lookup"><span data-stu-id="b7123-147">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. <span data-ttu-id="b7123-148">Save and close the `pom.xml` file.</span><span class="sxs-lookup"><span data-stu-id="b7123-148">Save and close the `pom.xml` file.</span></span>

1. <span data-ttu-id="b7123-149">Using a text editor, open the `schedule-jobs\src\main\java\com\mycompany\app\App.java` file.</span><span class="sxs-lookup"><span data-stu-id="b7123-149">Using a text editor, open the `schedule-jobs\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="b7123-150">Add the following **import** statements to the file:</span><span class="sxs-lookup"><span data-stu-id="b7123-150">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwinDevice;
    import com.microsoft.azure.sdk.iot.service.devicetwin.Pair;
    import com.microsoft.azure.sdk.iot.service.devicetwin.Query;
    import com.microsoft.azure.sdk.iot.service.devicetwin.SqlQuery;
    import com.microsoft.azure.sdk.iot.service.jobs.JobClient;
    import com.microsoft.azure.sdk.iot.service.jobs.JobResult;
    import com.microsoft.azure.sdk.iot.service.jobs.JobStatus;

    import java.util.Date;
    import java.time.Instant;
    import java.util.HashSet;
    import java.util.Set;
    import java.util.UUID;
    ```

1. <span data-ttu-id="b7123-151">Add the following class-level variables to the **App** class.</span><span class="sxs-lookup"><span data-stu-id="b7123-151">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="b7123-152">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in the *Create an IoT Hub* section:</span><span class="sxs-lookup"><span data-stu-id="b7123-152">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in the *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    // How long the job is permitted to run without
    // completing its work on the set of devices
    private static final long maxExecutionTimeInSeconds = 30;
    ```

1. <span data-ttu-id="b7123-153">Add the following method to the **App** class to schedule a job to update the **Building** and **Floor** desired properties in the device twin:</span><span class="sxs-lookup"><span data-stu-id="b7123-153">Add the following method to the **App** class to schedule a job to update the **Building** and **Floor** desired properties in the device twin:</span></span>

    ```java
    private static JobResult scheduleJobSetDesiredProperties(JobClient jobClient, String jobId) {
      DeviceTwinDevice twin = new DeviceTwinDevice(deviceId);
      Set<Pair> desiredProperties = new HashSet<Pair>();
      desiredProperties.add(new Pair("Building", 43));
      desiredProperties.add(new Pair("Floor", 3));
      twin.setDesiredProperties(desiredProperties);
      // Optimistic concurrency control
      twin.setETag("*");

      // Schedule the update twin job to run now
      // against a single device
      System.out.println("Schedule job " + jobId + " for device " + deviceId);
      try {
        JobResult jobResult = jobClient.scheduleUpdateTwin(jobId, 
          "deviceId='" + deviceId + "'",
          twin,
          new Date(),
          maxExecutionTimeInSeconds);
        return jobResult;
      } catch (Exception e) {
        System.out.println("Exception scheduling desired properties job: " + jobId);
        System.out.println(e.getMessage());
        return null;
      }
    }
    ```

1. <span data-ttu-id="b7123-154">To schedule a job to call the **lockDoor** method, add the following method to the **App** class:</span><span class="sxs-lookup"><span data-stu-id="b7123-154">To schedule a job to call the **lockDoor** method, add the following method to the **App** class:</span></span>

    ```java
    private static JobResult scheduleJobCallDirectMethod(JobClient jobClient, String jobId) {
      // Schedule a job now to call the lockDoor direct method
      // against a single device. Response and connection
      // timeouts are set to 5 seconds.
      System.out.println("Schedule job " + jobId + " for device " + deviceId);
      try {
        JobResult jobResult = jobClient.scheduleDeviceMethod(jobId,
          "deviceId='" + deviceId + "'",
          "lockDoor",
          5L, 5L, null,
          new Date(),
          maxExecutionTimeInSeconds);
        return jobResult;
      } catch (Exception e) {
        System.out.println("Exception scheduling direct method job: " + jobId);
        System.out.println(e.getMessage());
        return null;
      }
    };
    ```

1. <span data-ttu-id="b7123-155">To monitor a job, add the following method to the **App** class:</span><span class="sxs-lookup"><span data-stu-id="b7123-155">To monitor a job, add the following method to the **App** class:</span></span>

    ```java
    private static void monitorJob(JobClient jobClient, String jobId) {
      try {
        JobResult jobResult = jobClient.getJob(jobId);
        if(jobResult == null)
        {
          System.out.println("No JobResult for: " + jobId);
          return;
        }
        // Check the job result until it's completed
        while(jobResult.getJobStatus() != JobStatus.completed)
        {
          Thread.sleep(100);
          jobResult = jobClient.getJob(jobId);
          System.out.println("Status " + jobResult.getJobStatus() + " for job " + jobId);
        }
        System.out.println("Final status " + jobResult.getJobStatus() + " for job " + jobId);
      } catch (Exception e) {
        System.out.println("Exception monitoring job: " + jobId);
        System.out.println(e.getMessage());
        return;
      }
    }
    ```

1. <span data-ttu-id="b7123-156">To query for the details of the jobs you ran, add the following method:</span><span class="sxs-lookup"><span data-stu-id="b7123-156">To query for the details of the jobs you ran, add the following method:</span></span>

    ```java
    private static void queryDeviceJobs(JobClient jobClient, String start) throws Exception {
      System.out.println("\nQuery device jobs since " + start);

      // Create a jobs query using the time the jobs started
      Query deviceJobQuery = jobClient
          .queryDeviceJob(SqlQuery.createSqlQuery("*", SqlQuery.FromType.JOBS, "devices.jobs.startTimeUtc > '" + start + "'", null).getQuery());

      // Iterate over the list of jobs and print the details
      while (jobClient.hasNextJob(deviceJobQuery)) {
        System.out.println(jobClient.getNextJob(deviceJobQuery));
      }
    }
    ```

1. <span data-ttu-id="b7123-157">Update the **main** method signature to include the following `throws` clause:</span><span class="sxs-lookup"><span data-stu-id="b7123-157">Update the **main** method signature to include the following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws Exception
    ```

1. <span data-ttu-id="b7123-158">To run and monitor two jobs sequentially, add the following code to the **main** method:</span><span class="sxs-lookup"><span data-stu-id="b7123-158">To run and monitor two jobs sequentially, add the following code to the **main** method:</span></span>

    ```java
    // Record the start time
    String start = Instant.now().toString();

    // Create JobClient
    JobClient jobClient = JobClient.createFromConnectionString(iotHubConnectionString);
    System.out.println("JobClient created with success");

    // Schedule twin job desired properties
    // Maximum concurrent jobs is 1 for Free and S1 tiers
    String desiredPropertiesJobId = "DPCMD" + UUID.randomUUID();
    scheduleJobSetDesiredProperties(jobClient, desiredPropertiesJobId);
    monitorJob(jobClient, desiredPropertiesJobId);

    // Schedule twin job direct method
    String directMethodJobId = "DMCMD" + UUID.randomUUID();
    scheduleJobCallDirectMethod(jobClient, directMethodJobId);
    monitorJob(jobClient, directMethodJobId);

    // Run a query to show the job detail
    queryDeviceJobs(jobClient, start);

    System.out.println("Shutting down schedule-jobs app");
    ```

1. <span data-ttu-id="b7123-159">Save and close the `schedule-jobs\src\main\java\com\mycompany\app\App.java` file</span><span class="sxs-lookup"><span data-stu-id="b7123-159">Save and close the `schedule-jobs\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="b7123-160">Build the **schedule-jobs** app and correct any errors.</span><span class="sxs-lookup"><span data-stu-id="b7123-160">Build the **schedule-jobs** app and correct any errors.</span></span> <span data-ttu-id="b7123-161">At your command prompt, navigate to the `schedule-jobs` folder and run the following command:</span><span class="sxs-lookup"><span data-stu-id="b7123-161">At your command prompt, navigate to the `schedule-jobs` folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="b7123-162">Create a device app</span><span class="sxs-lookup"><span data-stu-id="b7123-162">Create a device app</span></span>

<span data-ttu-id="b7123-163">In this section, you create a Java console app that handles the desired properties sent from IoT Hub and implements the direct method call.</span><span class="sxs-lookup"><span data-stu-id="b7123-163">In this section, you create a Java console app that handles the desired properties sent from IoT Hub and implements the direct method call.</span></span>

1. <span data-ttu-id="b7123-164">In the `iot-java-schedule-jobs` folder, create a Maven project called **simulated-device** using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="b7123-164">In the `iot-java-schedule-jobs` folder, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="b7123-165">Note this is a single, long command:</span><span class="sxs-lookup"><span data-stu-id="b7123-165">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="b7123-166">At your command prompt, navigate to the `simulated-device` folder.</span><span class="sxs-lookup"><span data-stu-id="b7123-166">At your command prompt, navigate to the `simulated-device` folder.</span></span>

1. <span data-ttu-id="b7123-167">Using a text editor, open the `pom.xml` file in the `simulated-device` folder and add the following dependencies to the **dependencies** node.</span><span class="sxs-lookup"><span data-stu-id="b7123-167">Using a text editor, open the `pom.xml` file in the `simulated-device` folder and add the following dependencies to the **dependencies** node.</span></span> <span data-ttu-id="b7123-168">This dependency enables you to use the **iot-device-client** package in your app to communicate with your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="b7123-168">This dependency enables you to use the **iot-device-client** package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="b7123-169">You can check for the latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="b7123-169">You can check for the latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="b7123-170">Add the following **build** node after the **dependencies** node.</span><span class="sxs-lookup"><span data-stu-id="b7123-170">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="b7123-171">This configuration instructs Maven to use Java 1.8 to build the app:</span><span class="sxs-lookup"><span data-stu-id="b7123-171">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. <span data-ttu-id="b7123-172">Save and close the `pom.xml` file.</span><span class="sxs-lookup"><span data-stu-id="b7123-172">Save and close the `pom.xml` file.</span></span>

1. <span data-ttu-id="b7123-173">Using a text editor, open the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span><span class="sxs-lookup"><span data-stu-id="b7123-173">Using a text editor, open the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="b7123-174">Add the following **import** statements to the file:</span><span class="sxs-lookup"><span data-stu-id="b7123-174">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="b7123-175">Add the following class-level variables to the **App** class.</span><span class="sxs-lookup"><span data-stu-id="b7123-175">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="b7123-176">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with the device key value you generated in the *Create a device identity* section:</span><span class="sxs-lookup"><span data-stu-id="b7123-176">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with the device key value you generated in the *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="b7123-177">This sample app uses the **protocol** variable when it instantiates a **DeviceClient** object.</span><span class="sxs-lookup"><span data-stu-id="b7123-177">This sample app uses the **protocol** variable when it instantiates a **DeviceClient** object.</span></span>

1. <span data-ttu-id="b7123-178">To print device twin notifications to the console, add the following nested class to the **App** class:</span><span class="sxs-lookup"><span data-stu-id="b7123-178">To print device twin notifications to the console, add the following nested class to the **App** class:</span></span>

    ```java
    // Handler for device twin operation notifications from IoT Hub
    protected static class DeviceTwinStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded to device twin operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="b7123-179">To print direct method notifications to the console, add the following nested class to the **App** class:</span><span class="sxs-lookup"><span data-stu-id="b7123-179">To print direct method notifications to the console, add the following nested class to the **App** class:</span></span>

    ```java
    // Handler for direct method notifications from IoT Hub
    protected static class DirectMethodStatusCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded to direct method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="b7123-180">To handle direct method calls from IoT Hub, add the following nested class to the **App** class:</span><span class="sxs-lookup"><span data-stu-id="b7123-180">To handle direct method calls from IoT Hub, add the following nested class to the **App** class:</span></span>

    ```java
    // Handler for direct method calls from IoT Hub
    protected static class DirectMethodCallback
        implements DeviceMethodCallback {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context) {
        DeviceMethodData deviceMethodData;
        switch (methodName) {
          case "lockDoor": {
            System.out.println("Executing direct method: " + methodName);
            deviceMethodData = new DeviceMethodData(METHOD_SUCCESS, "Executed direct method " + methodName);
            break;
          }
          default: {
            deviceMethodData = new DeviceMethodData(METHOD_NOT_DEFINED, "Not defined direct method " + methodName);
          }
        }
        // Notify IoT Hub of result
        return deviceMethodData;
      }
    }
    ```

1. <span data-ttu-id="b7123-181">Update the **main** method signature to include the following `throws` clause:</span><span class="sxs-lookup"><span data-stu-id="b7123-181">Update the **main** method signature to include the following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="b7123-182">Add the following code to the **main** method to:</span><span class="sxs-lookup"><span data-stu-id="b7123-182">Add the following code to the **main** method to:</span></span>
    * <span data-ttu-id="b7123-183">Create a device client to communicate with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b7123-183">Create a device client to communicate with IoT Hub.</span></span>
    * <span data-ttu-id="b7123-184">Create a **Device** object to store the device twin properties.</span><span class="sxs-lookup"><span data-stu-id="b7123-184">Create a **Device** object to store the device twin properties.</span></span>

    ```java
    // Create a device client
    DeviceClient client = new DeviceClient(connString, protocol);

    // An object to manage device twin desired and reported properties
    Device dataCollector = new Device() {
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context)
      {
        System.out.println("Received desired property change: " + propertyKey + " " + propertyValue);
      }
    };
    ```

1. <span data-ttu-id="b7123-185">To start the device client services, add the following code to the **main** method:</span><span class="sxs-lookup"><span data-stu-id="b7123-185">To start the device client services, add the following code to the **main** method:</span></span>

    ```java
    try {
      // Open the DeviceClient
      // Start the device twin services
      // Subscribe to direct method calls
      client.open();
      client.startDeviceTwin(new DeviceTwinStatusCallBack(), null, dataCollector, null);
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
    } catch (Exception e) {
      System.out.println("Exception, shutting down \n" + " Cause: " + e.getCause() + " \n" + e.getMessage());
      dataCollector.clean();
      client.closeNow();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="b7123-186">To wait for the user to press the **Enter** key before shutting down, add the following code to the end of the **main** method:</span><span class="sxs-lookup"><span data-stu-id="b7123-186">To wait for the user to press the **Enter** key before shutting down, add the following code to the end of the **main** method:</span></span>

    ```java
    // Close the app
    System.out.println("Press any key to exit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    dataCollector.clean();
    client.closeNow();
    scanner.close();
    ```

1. <span data-ttu-id="b7123-187">Save and close the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span><span class="sxs-lookup"><span data-stu-id="b7123-187">Save and close the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="b7123-188">Build the **simulated-device** app and correct any errors.</span><span class="sxs-lookup"><span data-stu-id="b7123-188">Build the **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="b7123-189">At your command prompt, navigate to the `simulated-device` folder and run the following command:</span><span class="sxs-lookup"><span data-stu-id="b7123-189">At your command prompt, navigate to the `simulated-device` folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-the-apps"></a><span data-ttu-id="b7123-190">Run the apps</span><span class="sxs-lookup"><span data-stu-id="b7123-190">Run the apps</span></span>

<span data-ttu-id="b7123-191">You are now ready to run the console apps.</span><span class="sxs-lookup"><span data-stu-id="b7123-191">You are now ready to run the console apps.</span></span>

1. <span data-ttu-id="b7123-192">At a command prompt in the `simulated-device` folder, run the following command to start the device app listening for desired property changes and direct method calls:</span><span class="sxs-lookup"><span data-stu-id="b7123-192">At a command prompt in the `simulated-device` folder, run the following command to start the device app listening for desired property changes and direct method calls:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![The device client starts](media/iot-hub-java-java-schedule-jobs/device-app-1.png)

1. <span data-ttu-id="b7123-194">At a command prompt in the `schedule-jobs` folder, run the following command to run the **schedule-jobs** service app to run two jobs.</span><span class="sxs-lookup"><span data-stu-id="b7123-194">At a command prompt in the `schedule-jobs` folder, run the following command to run the **schedule-jobs** service app to run two jobs.</span></span> <span data-ttu-id="b7123-195">The first sets the desired property values, the second calls the direct method:</span><span class="sxs-lookup"><span data-stu-id="b7123-195">The first sets the desired property values, the second calls the direct method:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT Hub service app creates two jobs](media/iot-hub-java-java-schedule-jobs/service-app-1.png)

1. <span data-ttu-id="b7123-197">The device app handles the desired property change and the direct method call:</span><span class="sxs-lookup"><span data-stu-id="b7123-197">The device app handles the desired property change and the direct method call:</span></span>

    ![The device client responds to the changes](media/iot-hub-java-java-schedule-jobs/device-app-2.png)

## <a name="next-steps"></a><span data-ttu-id="b7123-199">Next steps</span><span class="sxs-lookup"><span data-stu-id="b7123-199">Next steps</span></span>

<span data-ttu-id="b7123-200">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span><span class="sxs-lookup"><span data-stu-id="b7123-200">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="b7123-201">You created a back-end app to run two jobs.</span><span class="sxs-lookup"><span data-stu-id="b7123-201">You created a back-end app to run two jobs.</span></span> <span data-ttu-id="b7123-202">The first job set desired property values, and the second job called a direct method.</span><span class="sxs-lookup"><span data-stu-id="b7123-202">The first job set desired property values, and the second job called a direct method.</span></span>

<span data-ttu-id="b7123-203">Use the following resources to learn how to:</span><span class="sxs-lookup"><span data-stu-id="b7123-203">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="b7123-204">Send telemetry from devices with the [Get started with IoT Hub](quickstart-send-telemetry-java.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="b7123-204">Send telemetry from devices with the [Get started with IoT Hub](quickstart-send-telemetry-java.md) tutorial.</span></span>
* <span data-ttu-id="b7123-205">Control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods](quickstart-control-device-java.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="b7123-205">Control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods](quickstart-control-device-java.md) tutorial.</span></span>
