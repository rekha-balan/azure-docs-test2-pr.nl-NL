---
title: Geo-fenced push notifications with Azure Notification Hubs and Bing Spatial Data | Microsoft Docs
description: In this tutorial, you will learn how to deliver location-based push notifications with Azure Notification Hubs and Bing Spatial Data.
services: notification-hubs
documentationcenter: windows
keywords: push notification,push notification
author: dend
manager: yuaxu
editor: dend
ms.assetid: f41beea1-0d62-4418-9ffc-c9d70607a1b7
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/31/2016
ms.author: dendeli
ms.openlocfilehash: a0ca272a0d53feb57058b8f214dce48b9c0191ce
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554323"
---
# <a name="geo-fenced-push-notifications-with-azure-notification-hubs-and-bing-spatial-data"></a><span data-ttu-id="c384d-104">Geo-fenced push notifications with Azure Notification Hubs and Bing Spatial Data</span><span class="sxs-lookup"><span data-stu-id="c384d-104">Geo-fenced push notifications with Azure Notification Hubs and Bing Spatial Data</span></span>
> [!NOTE]
> <span data-ttu-id="c384d-105">To complete this tutorial, you must have an active Azure account.</span><span class="sxs-lookup"><span data-stu-id="c384d-105">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="c384d-106">If you don't have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="c384d-106">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c384d-107">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).</span><span class="sxs-lookup"><span data-stu-id="c384d-107">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).</span></span>
> 
> 

<span data-ttu-id="c384d-108">In this tutorial, you will learn how to deliver location-based push notifications with Azure Notification Hubs and Bing Spatial Data, leveraged from within a Universal Windows Platform application.</span><span class="sxs-lookup"><span data-stu-id="c384d-108">In this tutorial, you will learn how to deliver location-based push notifications with Azure Notification Hubs and Bing Spatial Data, leveraged from within a Universal Windows Platform application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c384d-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c384d-109">Prerequisites</span></span>
<span data-ttu-id="c384d-110">First and foremost, you need to make sure that you have all the software and service pre-requisites:</span><span class="sxs-lookup"><span data-stu-id="c384d-110">First and foremost, you need to make sure that you have all the software and service pre-requisites:</span></span>

* <span data-ttu-id="c384d-111">[Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) or later ([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) will do as well).</span><span class="sxs-lookup"><span data-stu-id="c384d-111">[Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) or later ([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) will do as well).</span></span> 
* <span data-ttu-id="c384d-112">Latest version of the [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c384d-112">Latest version of the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="c384d-113">[Bing Maps Dev Center account](https://www.bingmapsportal.com/) (you can create one for free and associate it with your Microsoft account).</span><span class="sxs-lookup"><span data-stu-id="c384d-113">[Bing Maps Dev Center account](https://www.bingmapsportal.com/) (you can create one for free and associate it with your Microsoft account).</span></span> 

## <a name="getting-started"></a><span data-ttu-id="c384d-114">Getting Started</span><span class="sxs-lookup"><span data-stu-id="c384d-114">Getting Started</span></span>
<span data-ttu-id="c384d-115">Let’s start by creating the project.</span><span class="sxs-lookup"><span data-stu-id="c384d-115">Let’s start by creating the project.</span></span> <span data-ttu-id="c384d-116">In Visual Studio, start a new project of type **Blank App (Universal Windows)**.</span><span class="sxs-lookup"><span data-stu-id="c384d-116">In Visual Studio, start a new project of type **Blank App (Universal Windows)**.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-geofence/notification-hubs-create-blank-app.png)

<span data-ttu-id="c384d-117">Once the project creation is complete, you should have the harness for the app itself.</span><span class="sxs-lookup"><span data-stu-id="c384d-117">Once the project creation is complete, you should have the harness for the app itself.</span></span> <span data-ttu-id="c384d-118">Now let’s set up everything for the geo-fencing infrastructure.</span><span class="sxs-lookup"><span data-stu-id="c384d-118">Now let’s set up everything for the geo-fencing infrastructure.</span></span> <span data-ttu-id="c384d-119">Because we are going to use Bing services for this, there is a public REST API endpoint that allows us to query specific location frames:</span><span class="sxs-lookup"><span data-stu-id="c384d-119">Because we are going to use Bing services for this, there is a public REST API endpoint that allows us to query specific location frames:</span></span>

    http://spatial.virtualearth.net/REST/v1/data/

<span data-ttu-id="c384d-120">You will need to specify the following parameters to get it working:</span><span class="sxs-lookup"><span data-stu-id="c384d-120">You will need to specify the following parameters to get it working:</span></span>

* <span data-ttu-id="c384d-121">**Data Source ID** and **Data Source Name** – in Bing Maps API, data sources contain various bucketed metadata, such as locations and business hours of operation.</span><span class="sxs-lookup"><span data-stu-id="c384d-121">**Data Source ID** and **Data Source Name** – in Bing Maps API, data sources contain various bucketed metadata, such as locations and business hours of operation.</span></span> <span data-ttu-id="c384d-122">You can read more about those here.</span><span class="sxs-lookup"><span data-stu-id="c384d-122">You can read more about those here.</span></span> 
* <span data-ttu-id="c384d-123">**Entity Name** – the entity you want to use as a reference point for the notification.</span><span class="sxs-lookup"><span data-stu-id="c384d-123">**Entity Name** – the entity you want to use as a reference point for the notification.</span></span> 
* <span data-ttu-id="c384d-124">**Bing Maps API Key** – this is the key that you obtained earlier when you created the Bing Dev Center account.</span><span class="sxs-lookup"><span data-stu-id="c384d-124">**Bing Maps API Key** – this is the key that you obtained earlier when you created the Bing Dev Center account.</span></span>

<span data-ttu-id="c384d-125">Let’s do a deep-dive on the setup for each of the elements above.</span><span class="sxs-lookup"><span data-stu-id="c384d-125">Let’s do a deep-dive on the setup for each of the elements above.</span></span>

## <a name="setting-up-the-data-source"></a><span data-ttu-id="c384d-126">Setting up the data source</span><span class="sxs-lookup"><span data-stu-id="c384d-126">Setting up the data source</span></span>
<span data-ttu-id="c384d-127">You can do it in the Bing Maps Dev Center.</span><span class="sxs-lookup"><span data-stu-id="c384d-127">You can do it in the Bing Maps Dev Center.</span></span> <span data-ttu-id="c384d-128">Simply click on **Data sources** in the top navigation bar and select **Manage Data Sources**.</span><span class="sxs-lookup"><span data-stu-id="c384d-128">Simply click on **Data sources** in the top navigation bar and select **Manage Data Sources**.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-geofence/bing-maps-manage-data.png)

<span data-ttu-id="c384d-129">If you have not worked with Bing Maps API before, most likely there won’t be any data sources present, so you can just create a new one by clicking on Upload data to a data source.</span><span class="sxs-lookup"><span data-stu-id="c384d-129">If you have not worked with Bing Maps API before, most likely there won’t be any data sources present, so you can just create a new one by clicking on Upload data to a data source.</span></span> <span data-ttu-id="c384d-130">Make sure you fill out all the required fields:</span><span class="sxs-lookup"><span data-stu-id="c384d-130">Make sure you fill out all the required fields:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-geofence/bing-maps-create-data.png)

<span data-ttu-id="c384d-131">You might be wondering – what is the data file and what should you be uploading?</span><span class="sxs-lookup"><span data-stu-id="c384d-131">You might be wondering – what is the data file and what should you be uploading?</span></span> <span data-ttu-id="c384d-132">For the purposes of this test, we can just use the sample pipe-based that frames an area of the San Francisco waterfront:</span><span class="sxs-lookup"><span data-stu-id="c384d-132">For the purposes of this test, we can just use the sample pipe-based that frames an area of the San Francisco waterfront:</span></span>

    Bing Spatial Data Services, 1.0, TestBoundaries
    EntityID(Edm.String,primaryKey)|Name(Edm.String)|Longitude(Edm.Double)|Latitude(Edm.Double)|Boundary(Edm.Geography)
    1|SanFranciscoPier|||POLYGON ((-122.389825 37.776598,-122.389438 37.773087,-122.381885 37.771849,-122.382186 37.777022,-122.389825 37.776598))

<span data-ttu-id="c384d-133">The above represents this entity:</span><span class="sxs-lookup"><span data-stu-id="c384d-133">The above represents this entity:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-geofence/bing-maps-geofence.png)

<span data-ttu-id="c384d-134">Simply copy and paste the string above into a new file and save it as **NotificationHubsGeofence.pipe**, and upload it in the Bing Dev Center.</span><span class="sxs-lookup"><span data-stu-id="c384d-134">Simply copy and paste the string above into a new file and save it as **NotificationHubsGeofence.pipe**, and upload it in the Bing Dev Center.</span></span>

> [!NOTE]
> <span data-ttu-id="c384d-135">You might be prompted to specify a new key for the **Master Key** that is different from the **Query Key**.</span><span class="sxs-lookup"><span data-stu-id="c384d-135">You might be prompted to specify a new key for the **Master Key** that is different from the **Query Key**.</span></span> <span data-ttu-id="c384d-136">Simply create a new key through the dashboard and refresh the data source upload page.</span><span class="sxs-lookup"><span data-stu-id="c384d-136">Simply create a new key through the dashboard and refresh the data source upload page.</span></span>
> 
> 

<span data-ttu-id="c384d-137">Once you upload the data file, you will need to make sure that you publish the data source.</span><span class="sxs-lookup"><span data-stu-id="c384d-137">Once you upload the data file, you will need to make sure that you publish the data source.</span></span> 

<span data-ttu-id="c384d-138">Go to **Manage Data Sources**, just like we did above, find your data source in the list and click on **Publish** in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="c384d-138">Go to **Manage Data Sources**, just like we did above, find your data source in the list and click on **Publish** in the **Actions** column.</span></span> <span data-ttu-id="c384d-139">In a bit, you should see your data source in the **Published Data Sources** tab:</span><span class="sxs-lookup"><span data-stu-id="c384d-139">In a bit, you should see your data source in the **Published Data Sources** tab:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-geofence/bing-maps-published-data.png)

<span data-ttu-id="c384d-140">If you click **Edit**, you will be able to see at a glance what locations we introduced in it:</span><span class="sxs-lookup"><span data-stu-id="c384d-140">If you click **Edit**, you will be able to see at a glance what locations we introduced in it:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-geofence/bing-maps-data-details.png)

<span data-ttu-id="c384d-141">At this point, the portal does not show you the boundaries for the geofence that we created – all we need is a confirmation that the location specified is in the right vicinity.</span><span class="sxs-lookup"><span data-stu-id="c384d-141">At this point, the portal does not show you the boundaries for the geofence that we created – all we need is a confirmation that the location specified is in the right vicinity.</span></span>

<span data-ttu-id="c384d-142">Now you have all the requirements for the data source.</span><span class="sxs-lookup"><span data-stu-id="c384d-142">Now you have all the requirements for the data source.</span></span> <span data-ttu-id="c384d-143">To get the details on the request URL for the API call, in the Bing Maps Dev Center, click **Data sources** and select **Data Source Information**.</span><span class="sxs-lookup"><span data-stu-id="c384d-143">To get the details on the request URL for the API call, in the Bing Maps Dev Center, click **Data sources** and select **Data Source Information**.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-geofence/bing-maps-data-info.png)

<span data-ttu-id="c384d-144">The **Query URL** is what we’re after here.</span><span class="sxs-lookup"><span data-stu-id="c384d-144">The **Query URL** is what we’re after here.</span></span> <span data-ttu-id="c384d-145">This is the endpoint against which we can execute queries to check whether the device is currently within the boundaries of a location or not.</span><span class="sxs-lookup"><span data-stu-id="c384d-145">This is the endpoint against which we can execute queries to check whether the device is currently within the boundaries of a location or not.</span></span> <span data-ttu-id="c384d-146">To perform this check, we simply need to execute a GET call against the query URL, with the following parameters appended:</span><span class="sxs-lookup"><span data-stu-id="c384d-146">To perform this check, we simply need to execute a GET call against the query URL, with the following parameters appended:</span></span>

    ?spatialFilter=intersects(%27POINT%20LONGITUDE%20LATITUDE)%27)&$format=json&key=QUERY_KEY

<span data-ttu-id="c384d-147">That way you're specifying a target point that we obtain from the device and Bing Maps will automatically perform the calculations to see whether it is within the geofence.</span><span class="sxs-lookup"><span data-stu-id="c384d-147">That way you're specifying a target point that we obtain from the device and Bing Maps will automatically perform the calculations to see whether it is within the geofence.</span></span> <span data-ttu-id="c384d-148">Once you execute the request through a browser (or cURL), you will get standard a JSON response:</span><span class="sxs-lookup"><span data-stu-id="c384d-148">Once you execute the request through a browser (or cURL), you will get standard a JSON response:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-geofence/bing-maps-json.png)

<span data-ttu-id="c384d-149">This response only happens when the point is actually within the designated boundaries.</span><span class="sxs-lookup"><span data-stu-id="c384d-149">This response only happens when the point is actually within the designated boundaries.</span></span> <span data-ttu-id="c384d-150">If it is not, you will get an empty **results** bucket:</span><span class="sxs-lookup"><span data-stu-id="c384d-150">If it is not, you will get an empty **results** bucket:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-geofence/bing-maps-nores.png)

## <a name="setting-up-the-uwp-application"></a><span data-ttu-id="c384d-151">Setting up the UWP application</span><span class="sxs-lookup"><span data-stu-id="c384d-151">Setting up the UWP application</span></span>
<span data-ttu-id="c384d-152">Now that we have the data source ready, we can start working on the UWP application that we bootstrapped earlier.</span><span class="sxs-lookup"><span data-stu-id="c384d-152">Now that we have the data source ready, we can start working on the UWP application that we bootstrapped earlier.</span></span>

<span data-ttu-id="c384d-153">First and foremost, we must enable location services for our application.</span><span class="sxs-lookup"><span data-stu-id="c384d-153">First and foremost, we must enable location services for our application.</span></span> <span data-ttu-id="c384d-154">To do this, double-click on `Package.appxmanifest` file in **Solution Explorer**.</span><span class="sxs-lookup"><span data-stu-id="c384d-154">To do this, double-click on `Package.appxmanifest` file in **Solution Explorer**.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-geofence/vs-package-manifest.png)

<span data-ttu-id="c384d-155">In the package properties tab that just opened, click on **Capabilities** and make sure that you select **Location**:</span><span class="sxs-lookup"><span data-stu-id="c384d-155">In the package properties tab that just opened, click on **Capabilities** and make sure that you select **Location**:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-geofence/vs-package-location.png)

<span data-ttu-id="c384d-156">As the location capability is declared, create a new folder in your solution named `Core`, and add a new file within it, called `LocationHelper.cs`:</span><span class="sxs-lookup"><span data-stu-id="c384d-156">As the location capability is declared, create a new folder in your solution named `Core`, and add a new file within it, called `LocationHelper.cs`:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-geofence/vs-location-helper.png)

<span data-ttu-id="c384d-157">The `LocationHelper` class itself is fairly basic at this point – all it does is allow us to obtain the user location through the system API:</span><span class="sxs-lookup"><span data-stu-id="c384d-157">The `LocationHelper` class itself is fairly basic at this point – all it does is allow us to obtain the user location through the system API:</span></span>

    using System;
    using System.Threading.Tasks;
    using Windows.Devices.Geolocation;

    namespace NotificationHubs.Geofence.Core
    {
        public class LocationHelper
        {
            private static readonly uint AppDesiredAccuracyInMeters = 10;

            public async static Task<Geoposition> GetCurrentLocation()
            {
                var accessStatus = await Geolocator.RequestAccessAsync();
                switch (accessStatus)
                {
                    case GeolocationAccessStatus.Allowed:
                        {
                            Geolocator geolocator = new Geolocator { DesiredAccuracyInMeters = AppDesiredAccuracyInMeters };

                            return await geolocator.GetGeopositionAsync();
                        }
                    default:
                        {
                            return null;
                        }
                }
            }

        }
    }

<span data-ttu-id="c384d-158">You can read more about getting the user’s location in UWP apps in the official [MSDN document](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).</span><span class="sxs-lookup"><span data-stu-id="c384d-158">You can read more about getting the user’s location in UWP apps in the official [MSDN document](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).</span></span>

<span data-ttu-id="c384d-159">To check that the location acquisition is actually working, open the code side of your main page (`MainPage.xaml.cs`).</span><span class="sxs-lookup"><span data-stu-id="c384d-159">To check that the location acquisition is actually working, open the code side of your main page (`MainPage.xaml.cs`).</span></span> <span data-ttu-id="c384d-160">Create a new event handler for the `Loaded` event in the `MainPage` constructor:</span><span class="sxs-lookup"><span data-stu-id="c384d-160">Create a new event handler for the `Loaded` event in the `MainPage` constructor:</span></span>

    public MainPage()
    {
        this.InitializeComponent();
        this.Loaded += MainPage_Loaded;
    }

<span data-ttu-id="c384d-161">The implementation of the event handler is as follows:</span><span class="sxs-lookup"><span data-stu-id="c384d-161">The implementation of the event handler is as follows:</span></span>

    private async void MainPage_Loaded(object sender, RoutedEventArgs e)
    {
        var location = await LocationHelper.GetCurrentLocation();

        if (location != null)
        {
            Debug.WriteLine(string.Concat(location.Coordinate.Longitude,
                " ", location.Coordinate.Latitude));
        }
    }

<span data-ttu-id="c384d-162">Notice that we declared the handler as async because `GetCurrentLocation` is awaitable, and therefore requires to be executed in an async context.</span><span class="sxs-lookup"><span data-stu-id="c384d-162">Notice that we declared the handler as async because `GetCurrentLocation` is awaitable, and therefore requires to be executed in an async context.</span></span> <span data-ttu-id="c384d-163">Also, because under certain circumstances we might end up with a null location (e.g. the location services are disabled or the application was denied permissions to access location), we need to make sure that it is properly handled with a null check.</span><span class="sxs-lookup"><span data-stu-id="c384d-163">Also, because under certain circumstances we might end up with a null location (e.g. the location services are disabled or the application was denied permissions to access location), we need to make sure that it is properly handled with a null check.</span></span>

<span data-ttu-id="c384d-164">Run the application.</span><span class="sxs-lookup"><span data-stu-id="c384d-164">Run the application.</span></span> <span data-ttu-id="c384d-165">Make sure you allow location access:</span><span class="sxs-lookup"><span data-stu-id="c384d-165">Make sure you allow location access:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-geofence/notification-hubs-location-access.png)

<span data-ttu-id="c384d-166">Once the application launches, you should be able to see the coordinates in the **Output** window:</span><span class="sxs-lookup"><span data-stu-id="c384d-166">Once the application launches, you should be able to see the coordinates in the **Output** window:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-geofence/notification-hubs-location-output.png)

<span data-ttu-id="c384d-167">Now you know that location acquisition works – feel free to remove the test event handler for Loaded because we won’t be using it anymore.</span><span class="sxs-lookup"><span data-stu-id="c384d-167">Now you know that location acquisition works – feel free to remove the test event handler for Loaded because we won’t be using it anymore.</span></span>

<span data-ttu-id="c384d-168">The next step is to capture location changes.</span><span class="sxs-lookup"><span data-stu-id="c384d-168">The next step is to capture location changes.</span></span> <span data-ttu-id="c384d-169">For that, let’s go back to the `LocationHelper` class and add the event handler for `PositionChanged`:</span><span class="sxs-lookup"><span data-stu-id="c384d-169">For that, let’s go back to the `LocationHelper` class and add the event handler for `PositionChanged`:</span></span>

    geolocator.PositionChanged += Geolocator_PositionChanged;

<span data-ttu-id="c384d-170">The implementation will show the location coordinates in the **Output** window:</span><span class="sxs-lookup"><span data-stu-id="c384d-170">The implementation will show the location coordinates in the **Output** window:</span></span>

    private static async void Geolocator_PositionChanged(Geolocator sender, PositionChangedEventArgs args)
    {
        await CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            Debug.WriteLine(string.Concat(args.Position.Coordinate.Longitude, " ", args.Position.Coordinate.Latitude));
        });
    }

## <a name="setting-up-the-backend"></a><span data-ttu-id="c384d-171">Setting up the backend</span><span class="sxs-lookup"><span data-stu-id="c384d-171">Setting up the backend</span></span>
<span data-ttu-id="c384d-172">Download the [.NET Backend Sample from GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span><span class="sxs-lookup"><span data-stu-id="c384d-172">Download the [.NET Backend Sample from GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> <span data-ttu-id="c384d-173">Once the download completes, open the `NotifyUsers` folder, and subsequently – the `NotifyUsers.sln` file.</span><span class="sxs-lookup"><span data-stu-id="c384d-173">Once the download completes, open the `NotifyUsers` folder, and subsequently – the `NotifyUsers.sln` file.</span></span>

<span data-ttu-id="c384d-174">Set the `AppBackend` project as the **StartUp Project** and launch it.</span><span class="sxs-lookup"><span data-stu-id="c384d-174">Set the `AppBackend` project as the **StartUp Project** and launch it.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-geofence/vs-startup-project.png)

<span data-ttu-id="c384d-175">The project is already configured to send push notifications to target devices, so we’ll need to do only two things – swap out the right connection string for the notification hub and add boundary identification to send the notification only when the user is within the geofence.</span><span class="sxs-lookup"><span data-stu-id="c384d-175">The project is already configured to send push notifications to target devices, so we’ll need to do only two things – swap out the right connection string for the notification hub and add boundary identification to send the notification only when the user is within the geofence.</span></span>

<span data-ttu-id="c384d-176">To configure the connection string, in the `Models` folder open `Notifications.cs`.</span><span class="sxs-lookup"><span data-stu-id="c384d-176">To configure the connection string, in the `Models` folder open `Notifications.cs`.</span></span> <span data-ttu-id="c384d-177">The `NotificationHubClient.CreateClientFromConnectionString` function should contain the information about your notification hub that you can get in the [Azure Portal](https://portal.azure.com) (look inside the **Access Policies** blade in **Settings**).</span><span class="sxs-lookup"><span data-stu-id="c384d-177">The `NotificationHubClient.CreateClientFromConnectionString` function should contain the information about your notification hub that you can get in the [Azure Portal](https://portal.azure.com) (look inside the **Access Policies** blade in **Settings**).</span></span> <span data-ttu-id="c384d-178">Save the updated configuration file.</span><span class="sxs-lookup"><span data-stu-id="c384d-178">Save the updated configuration file.</span></span>

<span data-ttu-id="c384d-179">Now we need to create a model for the Bing Maps API result.</span><span class="sxs-lookup"><span data-stu-id="c384d-179">Now we need to create a model for the Bing Maps API result.</span></span> <span data-ttu-id="c384d-180">The easiest way to do that is right-click on the `Models` folder, **Add** > **Class**.</span><span class="sxs-lookup"><span data-stu-id="c384d-180">The easiest way to do that is right-click on the `Models` folder, **Add** > **Class**.</span></span> <span data-ttu-id="c384d-181">Name it `GeofenceBoundary.cs`.</span><span class="sxs-lookup"><span data-stu-id="c384d-181">Name it `GeofenceBoundary.cs`.</span></span> <span data-ttu-id="c384d-182">Once done, copy the JSON from the API response that we discussed in the first section and in Visual Studio use **Edit** > **Paste Special** > **Paste JSON as Classes**.</span><span class="sxs-lookup"><span data-stu-id="c384d-182">Once done, copy the JSON from the API response that we discussed in the first section and in Visual Studio use **Edit** > **Paste Special** > **Paste JSON as Classes**.</span></span> 

<span data-ttu-id="c384d-183">That way we ensure that the object will be deserialized exactly as it was intended.</span><span class="sxs-lookup"><span data-stu-id="c384d-183">That way we ensure that the object will be deserialized exactly as it was intended.</span></span> <span data-ttu-id="c384d-184">Your resulting class set should resemble this:</span><span class="sxs-lookup"><span data-stu-id="c384d-184">Your resulting class set should resemble this:</span></span>

    namespace AppBackend.Models
    {
        public class Rootobject
        {
            public D d { get; set; }
        }

        public class D
        {
            public string __copyright { get; set; }
            public Result[] results { get; set; }
        }

        public class Result
        {
            public __Metadata __metadata { get; set; }
            public string EntityID { get; set; }
            public string Name { get; set; }
            public float Longitude { get; set; }
            public float Latitude { get; set; }
            public string Boundary { get; set; }
            public string Confidence { get; set; }
            public string Locality { get; set; }
            public string AddressLine { get; set; }
            public string AdminDistrict { get; set; }
            public string CountryRegion { get; set; }
            public string PostalCode { get; set; }
        }

        public class __Metadata
        {
            public string uri { get; set; }
        }
    }

<span data-ttu-id="c384d-185">Next, open `Controllers` > `NotificationsController.cs`.</span><span class="sxs-lookup"><span data-stu-id="c384d-185">Next, open `Controllers` > `NotificationsController.cs`.</span></span> <span data-ttu-id="c384d-186">We need to tweak the Post call to account for the target longitude and latitude.</span><span class="sxs-lookup"><span data-stu-id="c384d-186">We need to tweak the Post call to account for the target longitude and latitude.</span></span> <span data-ttu-id="c384d-187">For that, simply add two strings to the function signature – `latitude` and `longitude`.</span><span class="sxs-lookup"><span data-stu-id="c384d-187">For that, simply add two strings to the function signature – `latitude` and `longitude`.</span></span>

    public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag, string latitude, string longitude)

<span data-ttu-id="c384d-188">Create a new class within the project called `ApiHelper.cs` – we’ll use it to connect to Bing to check point boundary intersections.</span><span class="sxs-lookup"><span data-stu-id="c384d-188">Create a new class within the project called `ApiHelper.cs` – we’ll use it to connect to Bing to check point boundary intersections.</span></span> <span data-ttu-id="c384d-189">Implement a `IsPointWithinBounds` function, like this:</span><span class="sxs-lookup"><span data-stu-id="c384d-189">Implement a `IsPointWithinBounds` function, like this:</span></span>

    public class ApiHelper
    {
        public static readonly string ApiEndpoint = "{YOUR_QUERY_ENDPOINT}?spatialFilter=intersects(%27POINT%20({0}%20{1})%27)&$format=json&key={2}";
        public static readonly string ApiKey = "{YOUR_API_KEY}";

        public static bool IsPointWithinBounds(string longitude,string latitude)
        {
            var json = new WebClient().DownloadString(string.Format(ApiEndpoint, longitude, latitude, ApiKey));
            var result = JsonConvert.DeserializeObject<Rootobject>(json);
            if (result.d.results != null && result.d.results.Count() > 0)
            {
                return true;
            }
            else
            {
                return false;
            }
        }
    }

> [!NOTE]
> <span data-ttu-id="c384d-190">Make sure to substitute the API endpoint with the query URL that you obtained earlier from the Bing Dev Center (same applies to the API key).</span><span class="sxs-lookup"><span data-stu-id="c384d-190">Make sure to substitute the API endpoint with the query URL that you obtained earlier from the Bing Dev Center (same applies to the API key).</span></span> 
> 
> 

<span data-ttu-id="c384d-191">If there are results to the query, that means that the specified point is within the boundaries of the geofence, so we return `true`.</span><span class="sxs-lookup"><span data-stu-id="c384d-191">If there are results to the query, that means that the specified point is within the boundaries of the geofence, so we return `true`.</span></span> <span data-ttu-id="c384d-192">If there are no results, Bing is telling us that the point is outside the lookup frame, so we return `false`.</span><span class="sxs-lookup"><span data-stu-id="c384d-192">If there are no results, Bing is telling us that the point is outside the lookup frame, so we return `false`.</span></span>

<span data-ttu-id="c384d-193">Back in `NotificationsController.cs`, create a check right before the switch statement:</span><span class="sxs-lookup"><span data-stu-id="c384d-193">Back in `NotificationsController.cs`, create a check right before the switch statement:</span></span>

    if (ApiHelper.IsPointWithinBounds(longitude, latitude))
    {
        switch (pns.ToLower())
        {
            case "wns":
                //// Windows 8.1 / Windows Phone 8.1
                var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
                            "From " + user + ": " + message + "</text></binding></visual></toast>";
                outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

                // Windows 10 specific Action Center support
                toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
                            "From " + user + ": " + message + "</text></binding></visual></toast>";
                outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

                break;
        }
    }

<span data-ttu-id="c384d-194">That way, the notification is only sent when the point is within the boundaries.</span><span class="sxs-lookup"><span data-stu-id="c384d-194">That way, the notification is only sent when the point is within the boundaries.</span></span>

## <a name="testing-push-notifications-in-the-uwp-app"></a><span data-ttu-id="c384d-195">Testing push notifications in the UWP app</span><span class="sxs-lookup"><span data-stu-id="c384d-195">Testing push notifications in the UWP app</span></span>
<span data-ttu-id="c384d-196">Going back to the UWP app, we should now be able to test notifications.</span><span class="sxs-lookup"><span data-stu-id="c384d-196">Going back to the UWP app, we should now be able to test notifications.</span></span> <span data-ttu-id="c384d-197">Within the `LocationHelper` class, create a new function – `SendLocationToBackend`:</span><span class="sxs-lookup"><span data-stu-id="c384d-197">Within the `LocationHelper` class, create a new function – `SendLocationToBackend`:</span></span>

    public static async Task SendLocationToBackend(string pns, string userTag, string message, string latitude, string longitude)
    {
        var POST_URL = "http://localhost:8741/api/notifications?pns=" +
            pns + "&to_tag=" + userTag + "&latitude=" + latitude + "&longitude=" + longitude;

        using (var httpClient = new HttpClient())
        {
            try
            {
                await httpClient.PostAsync(POST_URL, new StringContent("\"" + message + "\"",
                    System.Text.Encoding.UTF8, "application/json"));
            }
            catch (Exception ex)
            {
                Debug.WriteLine(ex.Message);
            }
        }
    }

> [!NOTE]
> <span data-ttu-id="c384d-198">Swap the `POST_URL` to the location of your deployed web application that we created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="c384d-198">Swap the `POST_URL` to the location of your deployed web application that we created in the previous section.</span></span> <span data-ttu-id="c384d-199">For now, it’s OK to run it locally, but as you work on deploying a public version, you will need to host it with an external provider.</span><span class="sxs-lookup"><span data-stu-id="c384d-199">For now, it’s OK to run it locally, but as you work on deploying a public version, you will need to host it with an external provider.</span></span>
> 
> 

<span data-ttu-id="c384d-200">Let’s now make sure that we register the UWP app for push notifications.</span><span class="sxs-lookup"><span data-stu-id="c384d-200">Let’s now make sure that we register the UWP app for push notifications.</span></span> <span data-ttu-id="c384d-201">In Visual Studio, click on **Project** > **Store** > **Associate app with the store**.</span><span class="sxs-lookup"><span data-stu-id="c384d-201">In Visual Studio, click on **Project** > **Store** > **Associate app with the store**.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-geofence/vs-associate-with-store.png)

<span data-ttu-id="c384d-202">Once you sign in to your developer account, make sure you select an existing app or create a new one and associate the package with it.</span><span class="sxs-lookup"><span data-stu-id="c384d-202">Once you sign in to your developer account, make sure you select an existing app or create a new one and associate the package with it.</span></span> 

<span data-ttu-id="c384d-203">Go to the Dev Center and open the app that you just created.</span><span class="sxs-lookup"><span data-stu-id="c384d-203">Go to the Dev Center and open the app that you just created.</span></span> <span data-ttu-id="c384d-204">Click **Services** > **Push Notifications** > **Live Services site**.</span><span class="sxs-lookup"><span data-stu-id="c384d-204">Click **Services** > **Push Notifications** > **Live Services site**.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-geofence/ms-live-services.png)

<span data-ttu-id="c384d-205">On the site, take note of the **Application Secret** and the **Package SID**.</span><span class="sxs-lookup"><span data-stu-id="c384d-205">On the site, take note of the **Application Secret** and the **Package SID**.</span></span> <span data-ttu-id="c384d-206">You will need both in the Azure Portal – open your notification hub, click on **Settings** > **Notification Services** > **Windows (WNS)** and enter the information in the required fields.</span><span class="sxs-lookup"><span data-stu-id="c384d-206">You will need both in the Azure Portal – open your notification hub, click on **Settings** > **Notification Services** > **Windows (WNS)** and enter the information in the required fields.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-geofence/notification-hubs-wns.png)

<span data-ttu-id="c384d-207">Click on **Save**.</span><span class="sxs-lookup"><span data-stu-id="c384d-207">Click on **Save**.</span></span>

<span data-ttu-id="c384d-208">Right click on **References** in **Solution Explorer** and select **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="c384d-208">Right click on **References** in **Solution Explorer** and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="c384d-209">We will need to add a reference to the **Microsoft Azure Service Bus managed library** – simply search for `WindowsAzure.Messaging.Managed` and add it to your project.</span><span class="sxs-lookup"><span data-stu-id="c384d-209">We will need to add a reference to the **Microsoft Azure Service Bus managed library** – simply search for `WindowsAzure.Messaging.Managed` and add it to your project.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-geofence/vs-nuget.png)

<span data-ttu-id="c384d-210">For testing purposes, we can create the `MainPage_Loaded` event handler once again, and add this code snippet to it:</span><span class="sxs-lookup"><span data-stu-id="c384d-210">For testing purposes, we can create the `MainPage_Loaded` event handler once again, and add this code snippet to it:</span></span>

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    var hub = new NotificationHub("HUB_NAME", "HUB_LISTEN_CONNECTION_STRING");
    var result = await hub.RegisterNativeAsync(channel.Uri);

    // Displays the registration ID so you know it was successful
    if (result.RegistrationId != null)
    {
        Debug.WriteLine("Reg successful.");
    }

<span data-ttu-id="c384d-211">The above registers the app with the notification hub.</span><span class="sxs-lookup"><span data-stu-id="c384d-211">The above registers the app with the notification hub.</span></span> <span data-ttu-id="c384d-212">You are ready to go!</span><span class="sxs-lookup"><span data-stu-id="c384d-212">You are ready to go!</span></span> 

<span data-ttu-id="c384d-213">In `LocationHelper`, inside the `Geolocator_PositionChanged` handler, you can add a piece of test code that will forcefully put the location inside the geofence:</span><span class="sxs-lookup"><span data-stu-id="c384d-213">In `LocationHelper`, inside the `Geolocator_PositionChanged` handler, you can add a piece of test code that will forcefully put the location inside the geofence:</span></span>

    await LocationHelper.SendLocationToBackend("wns", "TEST_USER", "TEST", "37.7746", "-122.3858");

<span data-ttu-id="c384d-214">Because we are not passing the real coordinates (which might not be within the boundaries at the moment) and are using predefined test values, we will see a notification show up on update:</span><span class="sxs-lookup"><span data-stu-id="c384d-214">Because we are not passing the real coordinates (which might not be within the boundaries at the moment) and are using predefined test values, we will see a notification show up on update:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-geofence/notification-hubs-test-notification.png)

## <a name="whats-next"></a><span data-ttu-id="c384d-215">What’s next?</span><span class="sxs-lookup"><span data-stu-id="c384d-215">What’s next?</span></span>
<span data-ttu-id="c384d-216">There are a couple of steps that you might need to follow in addition to the above to make sure that the solution is production-ready.</span><span class="sxs-lookup"><span data-stu-id="c384d-216">There are a couple of steps that you might need to follow in addition to the above to make sure that the solution is production-ready.</span></span>

<span data-ttu-id="c384d-217">First and foremost, you might need to ensure that geofences are dynamic.</span><span class="sxs-lookup"><span data-stu-id="c384d-217">First and foremost, you might need to ensure that geofences are dynamic.</span></span> <span data-ttu-id="c384d-218">This will require some extra work with the Bing API in order to be able to upload new boundaries within the existing data source.</span><span class="sxs-lookup"><span data-stu-id="c384d-218">This will require some extra work with the Bing API in order to be able to upload new boundaries within the existing data source.</span></span> <span data-ttu-id="c384d-219">Consult the [Bing Spatial Data Services API documentation](https://msdn.microsoft.com/library/ff701734.aspx) for more details on the subject.</span><span class="sxs-lookup"><span data-stu-id="c384d-219">Consult the [Bing Spatial Data Services API documentation](https://msdn.microsoft.com/library/ff701734.aspx) for more details on the subject.</span></span>

<span data-ttu-id="c384d-220">Second, as you are working to ensure that the delivery is done to the right participants, you might want to target them via [tagging](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="c384d-220">Second, as you are working to ensure that the delivery is done to the right participants, you might want to target them via [tagging](notification-hubs-tags-segment-push-message.md).</span></span>

<span data-ttu-id="c384d-221">The solution shown above describes a scenario in which you might have a wide variety of target platforms, so we did not limit the geofencing to system-specific capabilities.</span><span class="sxs-lookup"><span data-stu-id="c384d-221">The solution shown above describes a scenario in which you might have a wide variety of target platforms, so we did not limit the geofencing to system-specific capabilities.</span></span> <span data-ttu-id="c384d-222">That said, the Universal Windows Platform offers capabilities to [detect geofences right out-of-the-box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span><span class="sxs-lookup"><span data-stu-id="c384d-222">That said, the Universal Windows Platform offers capabilities to [detect geofences right out-of-the-box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span></span>

<span data-ttu-id="c384d-223">For more details regarding Notification Hubs capabilities, check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/).</span><span class="sxs-lookup"><span data-stu-id="c384d-223">For more details regarding Notification Hubs capabilities, check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/).</span></span>





















