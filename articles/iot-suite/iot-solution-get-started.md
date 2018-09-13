---
title: 'MyDriving Azure IoT example: Quick start | Microsoft Docs'
description: Get started with an app that's a comprehensive demonstration of how to architect an IoT system by using Microsoft Azure, including Stream Analytics, Machine Learning, and Event Hubs.
services: ''
documentationcenter: .net
suite: ''
author: harikmenon
manager: douge
ms.assetid: f40ea71b-5721-4a6b-a886-53c2e9dffe8f
ms.service: multiple
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: dotnet
ms.topic: article
ms.date: 03/25/2016
ms.author: harikm
ms.openlocfilehash: f2fe8fd214283cf590d9bc3b2d45a91791414999
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669746"
---
# <a name="mydriving-iot-system-quick-start"></a><span data-ttu-id="8240e-103">MyDriving IoT system: Quick start</span><span class="sxs-lookup"><span data-stu-id="8240e-103">MyDriving IoT system: Quick start</span></span>
<span data-ttu-id="8240e-104">MyDriving is a system that demonstrates the design and implementation of a typical [Internet of Things](iot-suite-overview.md) (IoT) solution that gathers telemetry from devices, processes that data in the cloud, and applies machine learning to provide an adaptive response.</span><span class="sxs-lookup"><span data-stu-id="8240e-104">MyDriving is a system that demonstrates the design and implementation of a typical [Internet of Things](iot-suite-overview.md) (IoT) solution that gathers telemetry from devices, processes that data in the cloud, and applies machine learning to provide an adaptive response.</span></span> <span data-ttu-id="8240e-105">The demonstration logs data about your car trips, by using data from both your mobile phone and an adapter that collects information from your car’s control system.</span><span class="sxs-lookup"><span data-stu-id="8240e-105">The demonstration logs data about your car trips, by using data from both your mobile phone and an adapter that collects information from your car’s control system.</span></span> <span data-ttu-id="8240e-106">It uses this data to provide feedback on your driving style in comparison to other users.</span><span class="sxs-lookup"><span data-stu-id="8240e-106">It uses this data to provide feedback on your driving style in comparison to other users.</span></span>

<span data-ttu-id="8240e-107">The real purpose of MyDriving is to get you started in creating your own IoT solution.</span><span class="sxs-lookup"><span data-stu-id="8240e-107">The real purpose of MyDriving is to get you started in creating your own IoT solution.</span></span> <span data-ttu-id="8240e-108">But before that, let’s get you going with the MyDriving app itself--as a member of our test user team.</span><span class="sxs-lookup"><span data-stu-id="8240e-108">But before that, let’s get you going with the MyDriving app itself--as a member of our test user team.</span></span> <span data-ttu-id="8240e-109">This gives you an experience of the app and the system behind it as a consumer, before you delve into the architecture.</span><span class="sxs-lookup"><span data-stu-id="8240e-109">This gives you an experience of the app and the system behind it as a consumer, before you delve into the architecture.</span></span> <span data-ttu-id="8240e-110">It also introduces you to HockeyApp, a cool way of managing the alpha and beta distributions of your apps to test users.</span><span class="sxs-lookup"><span data-stu-id="8240e-110">It also introduces you to HockeyApp, a cool way of managing the alpha and beta distributions of your apps to test users.</span></span>

## <a name="use-the-mobile-experience"></a><span data-ttu-id="8240e-111">Use the mobile experience</span><span class="sxs-lookup"><span data-stu-id="8240e-111">Use the mobile experience</span></span>
<span data-ttu-id="8240e-112">You can use the MyDriving app if you have an Android, iOS, or Windows 10 device.</span><span class="sxs-lookup"><span data-stu-id="8240e-112">You can use the MyDriving app if you have an Android, iOS, or Windows 10 device.</span></span>

### <a name="android-and-windows-10-mobile-installation"></a><span data-ttu-id="8240e-113">Android and Windows 10 Mobile installation</span><span class="sxs-lookup"><span data-stu-id="8240e-113">Android and Windows 10 Mobile installation</span></span>
<span data-ttu-id="8240e-114">On your device:</span><span class="sxs-lookup"><span data-stu-id="8240e-114">On your device:</span></span>

1. <span data-ttu-id="8240e-115">Allow development apps:</span><span class="sxs-lookup"><span data-stu-id="8240e-115">Allow development apps:</span></span>
   
   * <span data-ttu-id="8240e-116">Android: In **Settings** > **Security**, allow apps from **Unknown sources**.</span><span class="sxs-lookup"><span data-stu-id="8240e-116">Android: In **Settings** > **Security**, allow apps from **Unknown sources**.</span></span>
   * <span data-ttu-id="8240e-117">Windows 10: In **Settings** > **Updates** > **For Developers**, set **Developer mode**.</span><span class="sxs-lookup"><span data-stu-id="8240e-117">Windows 10: In **Settings** > **Updates** > **For Developers**, set **Developer mode**.</span></span>
2. <span data-ttu-id="8240e-118">Join our beta test team by signing up with, or signing in to, [HockeyApp](https://rink.hockeyapp.net).</span><span class="sxs-lookup"><span data-stu-id="8240e-118">Join our beta test team by signing up with, or signing in to, [HockeyApp](https://rink.hockeyapp.net).</span></span> <span data-ttu-id="8240e-119">HockeyApp makes it easy to distribute early releases of your app to test users.</span><span class="sxs-lookup"><span data-stu-id="8240e-119">HockeyApp makes it easy to distribute early releases of your app to test users.</span></span>
   
   <span data-ttu-id="8240e-120">If you’re using Windows 10, use the Edge browser.</span><span class="sxs-lookup"><span data-stu-id="8240e-120">If you’re using Windows 10, use the Edge browser.</span></span>
   
   <span data-ttu-id="8240e-121">If you were a Build 2016 attendee, sign in with the same Microsoft account email that you registered for the conference, by using one of the Microsoft buttons.</span><span class="sxs-lookup"><span data-stu-id="8240e-121">If you were a Build 2016 attendee, sign in with the same Microsoft account email that you registered for the conference, by using one of the Microsoft buttons.</span></span> <span data-ttu-id="8240e-122">You’re already signed up with HockeyApp.</span><span class="sxs-lookup"><span data-stu-id="8240e-122">You’re already signed up with HockeyApp.</span></span>
   
   ![HockeyApp sign-in screen](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-solution-get-started/image1.png)
3. <span data-ttu-id="8240e-124">Download and install the app from here:</span><span class="sxs-lookup"><span data-stu-id="8240e-124">Download and install the app from here:</span></span>
   
   * [<span data-ttu-id="8240e-125">Android</span><span class="sxs-lookup"><span data-stu-id="8240e-125">Android</span></span>](http://rink.io/spMyDrivingAndroid)
   * [<span data-ttu-id="8240e-126">Windows 10</span><span class="sxs-lookup"><span data-stu-id="8240e-126">Windows 10</span></span>](http://rink.io/spMyDrivingUWP)
   
   <span data-ttu-id="8240e-127">There are two items.</span><span class="sxs-lookup"><span data-stu-id="8240e-127">There are two items.</span></span> <span data-ttu-id="8240e-128">Install the certificate in **Trusted People**.</span><span class="sxs-lookup"><span data-stu-id="8240e-128">Install the certificate in **Trusted People**.</span></span> <span data-ttu-id="8240e-129">Then install the app.</span><span class="sxs-lookup"><span data-stu-id="8240e-129">Then install the app.</span></span>

<span data-ttu-id="8240e-130">*Any issues starting the app on Windows 10 Mobile?*</span><span class="sxs-lookup"><span data-stu-id="8240e-130">*Any issues starting the app on Windows 10 Mobile?*</span></span> <span data-ttu-id="8240e-131">Your phone might be an update or two behind.</span><span class="sxs-lookup"><span data-stu-id="8240e-131">Your phone might be an update or two behind.</span></span> <span data-ttu-id="8240e-132">Make sure you've got the latest updates, or install:</span><span class="sxs-lookup"><span data-stu-id="8240e-132">Make sure you've got the latest updates, or install:</span></span>

* [<span data-ttu-id="8240e-133">Microsoft.NET.Native.Framework.1.2.appx</span><span class="sxs-lookup"><span data-stu-id="8240e-133">Microsoft.NET.Native.Framework.1.2.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Framework.1.2.appx) 
* [<span data-ttu-id="8240e-134">Microsoft.NET.Native.Runtime.1.1.appx</span><span class="sxs-lookup"><span data-stu-id="8240e-134">Microsoft.NET.Native.Runtime.1.1.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Runtime.1.1.appx) 
* [<span data-ttu-id="8240e-135">Microsoft.VCLibs.ARM.14.00.appx</span><span class="sxs-lookup"><span data-stu-id="8240e-135">Microsoft.VCLibs.ARM.14.00.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.VCLibs.ARM.14.00.appx)

### <a name="ios-installation"></a><span data-ttu-id="8240e-136">iOS installation</span><span class="sxs-lookup"><span data-stu-id="8240e-136">iOS installation</span></span>
<span data-ttu-id="8240e-137">If you attended Build 2016, download the app as a member of our test team on HockeyApp:</span><span class="sxs-lookup"><span data-stu-id="8240e-137">If you attended Build 2016, download the app as a member of our test team on HockeyApp:</span></span>

1. <span data-ttu-id="8240e-138">On your iOS device, sign in to [HockeyApp](https://rink.hockeyapp.net).</span><span class="sxs-lookup"><span data-stu-id="8240e-138">On your iOS device, sign in to [HockeyApp](https://rink.hockeyapp.net).</span></span>
   <span data-ttu-id="8240e-139">Use one of the Microsoft sign-in buttons, and sign in with the same Microsoft account email that you registered with the conference.</span><span class="sxs-lookup"><span data-stu-id="8240e-139">Use one of the Microsoft sign-in buttons, and sign in with the same Microsoft account email that you registered with the conference.</span></span> <span data-ttu-id="8240e-140">(Don’t use the email and password fields.)</span><span class="sxs-lookup"><span data-stu-id="8240e-140">(Don’t use the email and password fields.)</span></span>
   
   ![HockeyApp sign-in screen](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-solution-get-started/image1.png)
2. <span data-ttu-id="8240e-142">In the HockeyApp dashboard, select MyDriving and download it.</span><span class="sxs-lookup"><span data-stu-id="8240e-142">In the HockeyApp dashboard, select MyDriving and download it.</span></span>
3. <span data-ttu-id="8240e-143">Authorize the beta release from HockeyApp:</span><span class="sxs-lookup"><span data-stu-id="8240e-143">Authorize the beta release from HockeyApp:</span></span>
   
   <span data-ttu-id="8240e-144">a.</span><span class="sxs-lookup"><span data-stu-id="8240e-144">a.</span></span> <span data-ttu-id="8240e-145">Go to **Settings** > **General** > **Profiles and Device Management.**</span><span class="sxs-lookup"><span data-stu-id="8240e-145">Go to **Settings** > **General** > **Profiles and Device Management.**</span></span>
   
   <span data-ttu-id="8240e-146">b.</span><span class="sxs-lookup"><span data-stu-id="8240e-146">b.</span></span> <span data-ttu-id="8240e-147">Trust the **Bit Stadium GmbH** certificate.</span><span class="sxs-lookup"><span data-stu-id="8240e-147">Trust the **Bit Stadium GmbH** certificate.</span></span>

<span data-ttu-id="8240e-148">If you didn’t attend Build 2016, you can build and deploy the app yourself:</span><span class="sxs-lookup"><span data-stu-id="8240e-148">If you didn’t attend Build 2016, you can build and deploy the app yourself:</span></span>

1. <span data-ttu-id="8240e-149">Download the code [from GitHub].</span><span class="sxs-lookup"><span data-stu-id="8240e-149">Download the code [from GitHub].</span></span>
2. <span data-ttu-id="8240e-150">Build and deploy by [using Xamarin].</span><span class="sxs-lookup"><span data-stu-id="8240e-150">Build and deploy by [using Xamarin].</span></span>

<span data-ttu-id="8240e-151">Find more details in the [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span><span class="sxs-lookup"><span data-stu-id="8240e-151">Find more details in the [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="get-an-obd-adapter-optional"></a><span data-ttu-id="8240e-152">Get an OBD adapter (optional)</span><span class="sxs-lookup"><span data-stu-id="8240e-152">Get an OBD adapter (optional)</span></span>
<span data-ttu-id="8240e-153">This is the part that makes this a real Internet of Things system!</span><span class="sxs-lookup"><span data-stu-id="8240e-153">This is the part that makes this a real Internet of Things system!</span></span> <span data-ttu-id="8240e-154">You can use the app without one, but it’s more fun with the real thing, and they aren’t expensive.</span><span class="sxs-lookup"><span data-stu-id="8240e-154">You can use the app without one, but it’s more fun with the real thing, and they aren’t expensive.</span></span>

<span data-ttu-id="8240e-155">On-board diagnostics (OBD) is the feature of your car that the garage uses to tune up your car and diagnose odd noises and warning lamps.</span><span class="sxs-lookup"><span data-stu-id="8240e-155">On-board diagnostics (OBD) is the feature of your car that the garage uses to tune up your car and diagnose odd noises and warning lamps.</span></span> <span data-ttu-id="8240e-156">Unless your car is of great antiquity, you’ll find a socket somewhere in the cabin, typically behind a flap under the dashboard.</span><span class="sxs-lookup"><span data-stu-id="8240e-156">Unless your car is of great antiquity, you’ll find a socket somewhere in the cabin, typically behind a flap under the dashboard.</span></span> <span data-ttu-id="8240e-157">With the right connector, you can get metrics of the engine’s performance and make certain adjustments.</span><span class="sxs-lookup"><span data-stu-id="8240e-157">With the right connector, you can get metrics of the engine’s performance and make certain adjustments.</span></span> <span data-ttu-id="8240e-158">An OBD connector can be purchased cheaply from the usual places.</span><span class="sxs-lookup"><span data-stu-id="8240e-158">An OBD connector can be purchased cheaply from the usual places.</span></span> <span data-ttu-id="8240e-159">It connects by using Bluetooth or Wi-Fi to an app on your phone.</span><span class="sxs-lookup"><span data-stu-id="8240e-159">It connects by using Bluetooth or Wi-Fi to an app on your phone.</span></span>

<span data-ttu-id="8240e-160">In this case, we’re going to connect your car to the cloud.</span><span class="sxs-lookup"><span data-stu-id="8240e-160">In this case, we’re going to connect your car to the cloud.</span></span> <span data-ttu-id="8240e-161">The direct connection from the OBD is to your phone, but our app works as a relay.</span><span class="sxs-lookup"><span data-stu-id="8240e-161">The direct connection from the OBD is to your phone, but our app works as a relay.</span></span> <span data-ttu-id="8240e-162">Your car's telemetry is sent straight to the MyDriving IoT hub, where it's processed to log your road trips and assess your driving style.</span><span class="sxs-lookup"><span data-stu-id="8240e-162">Your car's telemetry is sent straight to the MyDriving IoT hub, where it's processed to log your road trips and assess your driving style.</span></span>

<span data-ttu-id="8240e-163">To connect an OBD device:</span><span class="sxs-lookup"><span data-stu-id="8240e-163">To connect an OBD device:</span></span>

1. <span data-ttu-id="8240e-164">Check that your car has an OBD socket.</span><span class="sxs-lookup"><span data-stu-id="8240e-164">Check that your car has an OBD socket.</span></span>
2. <span data-ttu-id="8240e-165">Obtain an OBD adapter:</span><span class="sxs-lookup"><span data-stu-id="8240e-165">Obtain an OBD adapter:</span></span>
   
   * <span data-ttu-id="8240e-166">If you're using an Android or Windows phone, you need a Bluetooth-enabled OBD II adapter.</span><span class="sxs-lookup"><span data-stu-id="8240e-166">If you're using an Android or Windows phone, you need a Bluetooth-enabled OBD II adapter.</span></span> <span data-ttu-id="8240e-167">We used [BAFX Products 34t5 Bluetooth OBDII Scan Tool].</span><span class="sxs-lookup"><span data-stu-id="8240e-167">We used [BAFX Products 34t5 Bluetooth OBDII Scan Tool].</span></span>
   * <span data-ttu-id="8240e-168">If you're using an iOS phone, you need a Wi-Fi-enabled OBD adapter.</span><span class="sxs-lookup"><span data-stu-id="8240e-168">If you're using an iOS phone, you need a Wi-Fi-enabled OBD adapter.</span></span> <span data-ttu-id="8240e-169">We used [ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner].</span><span class="sxs-lookup"><span data-stu-id="8240e-169">We used [ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner].</span></span>
3. <span data-ttu-id="8240e-170">Follow the instructions that come with your OBD adapter to connect it to your phone.</span><span class="sxs-lookup"><span data-stu-id="8240e-170">Follow the instructions that come with your OBD adapter to connect it to your phone.</span></span> <span data-ttu-id="8240e-171">Keep the following in mind:</span><span class="sxs-lookup"><span data-stu-id="8240e-171">Keep the following in mind:</span></span>
   
   * <span data-ttu-id="8240e-172">A Bluetooth adapter must be paired with the phone, on the **Settings** page.</span><span class="sxs-lookup"><span data-stu-id="8240e-172">A Bluetooth adapter must be paired with the phone, on the **Settings** page.</span></span>
   * <span data-ttu-id="8240e-173">A Wi-Fi adapter must have an address in the range 192.168.xxx.xxx.</span><span class="sxs-lookup"><span data-stu-id="8240e-173">A Wi-Fi adapter must have an address in the range 192.168.xxx.xxx.</span></span>
4. <span data-ttu-id="8240e-174">If you have several cars, you can get a separate adapter for each (maximum of three).</span><span class="sxs-lookup"><span data-stu-id="8240e-174">If you have several cars, you can get a separate adapter for each (maximum of three).</span></span>

<span data-ttu-id="8240e-175">If you don’t have an OBD adapter, the app will still send location and speed data from the phone's GPS receiver to the back end and will ask if you want to simulate an OBD.</span><span class="sxs-lookup"><span data-stu-id="8240e-175">If you don’t have an OBD adapter, the app will still send location and speed data from the phone's GPS receiver to the back end and will ask if you want to simulate an OBD.</span></span>

<span data-ttu-id="8240e-176">You can find out more about how the app uses data from the OBD adapter and about options for creating your own OBD device in section 2.1, "IoT Devices," in the [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span><span class="sxs-lookup"><span data-stu-id="8240e-176">You can find out more about how the app uses data from the OBD adapter and about options for creating your own OBD device in section 2.1, "IoT Devices," in the [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="use-the-app"></a><span data-ttu-id="8240e-177">Use the app</span><span class="sxs-lookup"><span data-stu-id="8240e-177">Use the app</span></span>
<span data-ttu-id="8240e-178">Start the app.</span><span class="sxs-lookup"><span data-stu-id="8240e-178">Start the app.</span></span> <span data-ttu-id="8240e-179">There’s an initial Quickstart to walk you through how it works.</span><span class="sxs-lookup"><span data-stu-id="8240e-179">There’s an initial Quickstart to walk you through how it works.</span></span>

### <a name="track-your-trips"></a><span data-ttu-id="8240e-180">Track your trips</span><span class="sxs-lookup"><span data-stu-id="8240e-180">Track your trips</span></span>
<span data-ttu-id="8240e-181">Tap the record button (big red circle at the bottom of the screen) to start a trip, and tap again to end.</span><span class="sxs-lookup"><span data-stu-id="8240e-181">Tap the record button (big red circle at the bottom of the screen) to start a trip, and tap again to end.</span></span>

![Illustration of the record button for trip tracking](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-solution-get-started/image2.png)

<span data-ttu-id="8240e-183">Each time you start a trip, if there’s no OBD device, you’ll be asked if you want to use the simulator.</span><span class="sxs-lookup"><span data-stu-id="8240e-183">Each time you start a trip, if there’s no OBD device, you’ll be asked if you want to use the simulator.</span></span>

<span data-ttu-id="8240e-184">At the end of a trip, tap the stop button, and you get a summary.</span><span class="sxs-lookup"><span data-stu-id="8240e-184">At the end of a trip, tap the stop button, and you get a summary.</span></span>

![Example of a trip summary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-solution-get-started/image3.png)

### <a name="review-your-trips"></a><span data-ttu-id="8240e-186">Review your trips</span><span class="sxs-lookup"><span data-stu-id="8240e-186">Review your trips</span></span>
![Example of a past trip](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-solution-get-started/image4.png)

### <a name="review-your-profile"></a><span data-ttu-id="8240e-188">Review your profile</span><span class="sxs-lookup"><span data-stu-id="8240e-188">Review your profile</span></span>
![Example of a driving-style profile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-solution-get-started/image5.png)

## <a name="send-us-your-test-feedback"></a><span data-ttu-id="8240e-190">Send us your test feedback</span><span class="sxs-lookup"><span data-stu-id="8240e-190">Send us your test feedback</span></span>
<span data-ttu-id="8240e-191">Because we created MyDriving to help jumpstart your own IoT systems, we certainly want to hear from you about how well it works.</span><span class="sxs-lookup"><span data-stu-id="8240e-191">Because we created MyDriving to help jumpstart your own IoT systems, we certainly want to hear from you about how well it works.</span></span> <span data-ttu-id="8240e-192">Let us know if:</span><span class="sxs-lookup"><span data-stu-id="8240e-192">Let us know if:</span></span>

* <span data-ttu-id="8240e-193">You run into difficulties or challenges.</span><span class="sxs-lookup"><span data-stu-id="8240e-193">You run into difficulties or challenges.</span></span>
* <span data-ttu-id="8240e-194">There is an extension point that would make it more suitable to your scenario.</span><span class="sxs-lookup"><span data-stu-id="8240e-194">There is an extension point that would make it more suitable to your scenario.</span></span>
* <span data-ttu-id="8240e-195">You find a more efficient way to accomplish certain needs.</span><span class="sxs-lookup"><span data-stu-id="8240e-195">You find a more efficient way to accomplish certain needs.</span></span>
* <span data-ttu-id="8240e-196">You have any other suggestions for improving MyDriving or this documentation.</span><span class="sxs-lookup"><span data-stu-id="8240e-196">You have any other suggestions for improving MyDriving or this documentation.</span></span>

<span data-ttu-id="8240e-197">Within the MyDriving app itself, you can use the built-in HockeyApp feedback mechanism: on iOS and Android, just give your phone a shake, or use the **Feedback** menu command.</span><span class="sxs-lookup"><span data-stu-id="8240e-197">Within the MyDriving app itself, you can use the built-in HockeyApp feedback mechanism: on iOS and Android, just give your phone a shake, or use the **Feedback** menu command.</span></span> <span data-ttu-id="8240e-198">This will automatically attach a screenshot, so that we’ll know what you’re talking about.</span><span class="sxs-lookup"><span data-stu-id="8240e-198">This will automatically attach a screenshot, so that we’ll know what you’re talking about.</span></span> <span data-ttu-id="8240e-199">And if there are any unfortunate crashes, HockeyApp collects the crash logs to tell us about them.</span><span class="sxs-lookup"><span data-stu-id="8240e-199">And if there are any unfortunate crashes, HockeyApp collects the crash logs to tell us about them.</span></span> <span data-ttu-id="8240e-200">You can also give feedback through the [HockeyApp portal].</span><span class="sxs-lookup"><span data-stu-id="8240e-200">You can also give feedback through the [HockeyApp portal].</span></span>

<span data-ttu-id="8240e-201">You can also file an [issue on GitHub], or leave a comment below (en-us edition).</span><span class="sxs-lookup"><span data-stu-id="8240e-201">You can also file an [issue on GitHub], or leave a comment below (en-us edition).</span></span>

<span data-ttu-id="8240e-202">We look forward to hearing from you!</span><span class="sxs-lookup"><span data-stu-id="8240e-202">We look forward to hearing from you!</span></span>

## <a name="next-steps"></a><span data-ttu-id="8240e-203">Next steps</span><span class="sxs-lookup"><span data-stu-id="8240e-203">Next steps</span></span>
* <span data-ttu-id="8240e-204">Explore the [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) to understand how we’ve designed and built the entire MyDriving system.</span><span class="sxs-lookup"><span data-stu-id="8240e-204">Explore the [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) to understand how we’ve designed and built the entire MyDriving system.</span></span>
* <span data-ttu-id="8240e-205">[Create and deploy a system of your own](iot-solution-build-system.md) by using our Azure Resource Manager scripts.</span><span class="sxs-lookup"><span data-stu-id="8240e-205">[Create and deploy a system of your own](iot-solution-build-system.md) by using our Azure Resource Manager scripts.</span></span> <span data-ttu-id="8240e-206">The [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) also guides you through areas where you’ll make the most customizations.</span><span class="sxs-lookup"><span data-stu-id="8240e-206">The [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) also guides you through areas where you’ll make the most customizations.</span></span>

[from GitHub]: https://github.com/Azure-Samples/MyDriving
[using Xamarin]: https://developer.xamarin.com/guides/ios/getting_started/installation/
[BAFX Products 34t5 Bluetooth OBDII Scan Tool]: http://www.amazon.com/gp/product/B005NLQAHS
[ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP
[HockeyApp portal]: https://rink.hockeyapp.org
[issue on GitHub]: https://github.com/Azure-Samples/MyDriving/issues






