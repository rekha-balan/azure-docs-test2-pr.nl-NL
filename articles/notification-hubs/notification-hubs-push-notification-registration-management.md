---
title: Registration Management
description: This topic explains how to register devices with notification hubs in order to receive push notifications.
services: notification-hubs
documentationcenter: .net
author: dimazaid
manager: kpiteira
editor: spelluru
ms.assetid: fd0ee230-132c-4143-b4f9-65cef7f463a1
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 04/14/2018
ms.author: dimazaid
ms.openlocfilehash: 7f9052da066fcc0021151bf3b547484859cf216d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44790834"
---
# <a name="registration-management"></a><span data-ttu-id="c8b0e-103">Registration management</span><span class="sxs-lookup"><span data-stu-id="c8b0e-103">Registration management</span></span>
## <a name="overview"></a><span data-ttu-id="c8b0e-104">Overview</span><span class="sxs-lookup"><span data-stu-id="c8b0e-104">Overview</span></span>
<span data-ttu-id="c8b0e-105">This topic explains how to register devices with notification hubs in order to receive push notifications.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-105">This topic explains how to register devices with notification hubs in order to receive push notifications.</span></span> <span data-ttu-id="c8b0e-106">The topic describes registrations at a high level, then introduces the two main patterns for registering devices: registering from the device directly to the notification hub, and registering through an application backend.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-106">The topic describes registrations at a high level, then introduces the two main patterns for registering devices: registering from the device directly to the notification hub, and registering through an application backend.</span></span> 

## <a name="what-is-device-registration"></a><span data-ttu-id="c8b0e-107">What is device registration</span><span class="sxs-lookup"><span data-stu-id="c8b0e-107">What is device registration</span></span>
<span data-ttu-id="c8b0e-108">Device registration with a Notification Hub is accomplished using a **Registration** or **Installation**.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-108">Device registration with a Notification Hub is accomplished using a **Registration** or **Installation**.</span></span>

#### <a name="registrations"></a><span data-ttu-id="c8b0e-109">Registrations</span><span class="sxs-lookup"><span data-stu-id="c8b0e-109">Registrations</span></span>
<span data-ttu-id="c8b0e-110">A registration associates the Platform Notification Service (PNS) handle for a device with tags and possibly a template.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-110">A registration associates the Platform Notification Service (PNS) handle for a device with tags and possibly a template.</span></span> <span data-ttu-id="c8b0e-111">The PNS handle could be a ChannelURI, device token, or GCM registration id. Tags are used to route notifications to the correct set of device handles.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-111">The PNS handle could be a ChannelURI, device token, or GCM registration id. Tags are used to route notifications to the correct set of device handles.</span></span> <span data-ttu-id="c8b0e-112">For more information, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="c8b0e-112">For more information, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span> <span data-ttu-id="c8b0e-113">Templates are used to implement per-registration transformation.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-113">Templates are used to implement per-registration transformation.</span></span> <span data-ttu-id="c8b0e-114">For more information, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="c8b0e-114">For more information, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>

#### <a name="installations"></a><span data-ttu-id="c8b0e-115">Installations</span><span class="sxs-lookup"><span data-stu-id="c8b0e-115">Installations</span></span>
<span data-ttu-id="c8b0e-116">An Installation is an enhanced registration that includes a bag of push related properties.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-116">An Installation is an enhanced registration that includes a bag of push related properties.</span></span> <span data-ttu-id="c8b0e-117">It is the latest and best approach to registering your devices.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-117">It is the latest and best approach to registering your devices.</span></span> <span data-ttu-id="c8b0e-118">However, it is not supported by client-side .NET SDK ([Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) as of yet.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-118">However, it is not supported by client-side .NET SDK ([Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) as of yet.</span></span>  <span data-ttu-id="c8b0e-119">This means if you are registering from the client device itself, you would have to use the [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx) approach to support installations.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-119">This means if you are registering from the client device itself, you would have to use the [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx) approach to support installations.</span></span> <span data-ttu-id="c8b0e-120">If you are using a backend service, you should be able to use [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="c8b0e-120">If you are using a backend service, you should be able to use [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="c8b0e-121">The following are some key advantages to using installations:</span><span class="sxs-lookup"><span data-stu-id="c8b0e-121">The following are some key advantages to using installations:</span></span>

* <span data-ttu-id="c8b0e-122">Creating or updating an installation is fully idempotent.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-122">Creating or updating an installation is fully idempotent.</span></span> <span data-ttu-id="c8b0e-123">So you can retry it without any concerns about duplicate registrations.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-123">So you can retry it without any concerns about duplicate registrations.</span></span>
* <span data-ttu-id="c8b0e-124">The installation model makes it easy to do individual pushes - targeting specific device.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-124">The installation model makes it easy to do individual pushes - targeting specific device.</span></span> <span data-ttu-id="c8b0e-125">A system tag **"$InstallationId:[installationId]"** is automatically added with each installation based registration.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-125">A system tag **"$InstallationId:[installationId]"** is automatically added with each installation based registration.</span></span> <span data-ttu-id="c8b0e-126">So you can call a send to this tag to target a specific device without having to do any additional coding.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-126">So you can call a send to this tag to target a specific device without having to do any additional coding.</span></span>
* <span data-ttu-id="c8b0e-127">Using installations also enables you to do partial registration updates.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-127">Using installations also enables you to do partial registration updates.</span></span> <span data-ttu-id="c8b0e-128">The partial update of an installation is requested with a PATCH method using the [JSON-Patch standard](https://tools.ietf.org/html/rfc6902).</span><span class="sxs-lookup"><span data-stu-id="c8b0e-128">The partial update of an installation is requested with a PATCH method using the [JSON-Patch standard](https://tools.ietf.org/html/rfc6902).</span></span> <span data-ttu-id="c8b0e-129">This is useful when you want to update tags on the registration.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-129">This is useful when you want to update tags on the registration.</span></span> <span data-ttu-id="c8b0e-130">You don't have to pull down the entire registration and then resend all the previous tags again.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-130">You don't have to pull down the entire registration and then resend all the previous tags again.</span></span>

<span data-ttu-id="c8b0e-131">An installation can contain the following properties.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-131">An installation can contain the following properties.</span></span> <span data-ttu-id="c8b0e-132">For a complete listing of the installation properties, see [Create or Overwrite an Installation with REST API](https://msdn.microsoft.com/library/azure/mt621153.aspx) or [Installation Properties](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx).</span><span class="sxs-lookup"><span data-stu-id="c8b0e-132">For a complete listing of the installation properties, see [Create or Overwrite an Installation with REST API](https://msdn.microsoft.com/library/azure/mt621153.aspx) or [Installation Properties](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx).</span></span>

    // Example installation format to show some supported properties
    {,
        installationId: "",
        expirationTime: "",
        tags: [],
        platform: "",
        pushChannel: "",
        ………
        templates: {
            "templateName1" : {
                body: "",
                tags: [] },
            "templateName2" : {
                body: "",
                // Headers are for Windows Store only
                headers: {
                    "X-WNS-Type": "wns/tile" }
                tags: [] }
        },
        secondaryTiles: {
            "tileId1": {
                pushChannel: "",
                tags: [],
                templates: {
                    "otherTemplate": {
                        bodyTemplate: "",
                        headers: {
                            ... }
                        tags: [] }
                }
            }
        }
    }



<span data-ttu-id="c8b0e-133">It is important to note that registrations and installations by default no longer expire.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-133">It is important to note that registrations and installations by default no longer expire.</span></span>

<span data-ttu-id="c8b0e-134">Registrations and installations must contain a valid PNS handle for each device/channel.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-134">Registrations and installations must contain a valid PNS handle for each device/channel.</span></span> <span data-ttu-id="c8b0e-135">Because PNS handles can only be obtained in a client app on the device, one pattern is to register directly on that device with the client app.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-135">Because PNS handles can only be obtained in a client app on the device, one pattern is to register directly on that device with the client app.</span></span> <span data-ttu-id="c8b0e-136">On the other hand, security considerations and business logic related to tags might require you to manage device registration in the app back-end.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-136">On the other hand, security considerations and business logic related to tags might require you to manage device registration in the app back-end.</span></span> 

#### <a name="templates"></a><span data-ttu-id="c8b0e-137">Templates</span><span class="sxs-lookup"><span data-stu-id="c8b0e-137">Templates</span></span>
<span data-ttu-id="c8b0e-138">If you want to use [Templates](notification-hubs-templates-cross-platform-push-messages.md), the device installation also holds all templates associated with that device in a JSON format (see sample above).</span><span class="sxs-lookup"><span data-stu-id="c8b0e-138">If you want to use [Templates](notification-hubs-templates-cross-platform-push-messages.md), the device installation also holds all templates associated with that device in a JSON format (see sample above).</span></span> <span data-ttu-id="c8b0e-139">The template names help target different templates for the same device.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-139">The template names help target different templates for the same device.</span></span>

<span data-ttu-id="c8b0e-140">Each template name maps to a template body and an optional set of tags.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-140">Each template name maps to a template body and an optional set of tags.</span></span> <span data-ttu-id="c8b0e-141">Moreover, each platform can have additional template properties.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-141">Moreover, each platform can have additional template properties.</span></span> <span data-ttu-id="c8b0e-142">For Windows Store (using WNS) and Windows Phone 8 (using MPNS), an additional set of headers can be part of the template.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-142">For Windows Store (using WNS) and Windows Phone 8 (using MPNS), an additional set of headers can be part of the template.</span></span> <span data-ttu-id="c8b0e-143">In the case of APNs, you can set an expiry property to either a constant or to a template expression.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-143">In the case of APNs, you can set an expiry property to either a constant or to a template expression.</span></span> <span data-ttu-id="c8b0e-144">For a complete listing of the installation properties see, [Create or Overwrite an Installation with REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) topic.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-144">For a complete listing of the installation properties see, [Create or Overwrite an Installation with REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) topic.</span></span>

#### <a name="secondary-tiles-for-windows-store-apps"></a><span data-ttu-id="c8b0e-145">Secondary Tiles for Windows Store Apps</span><span class="sxs-lookup"><span data-stu-id="c8b0e-145">Secondary Tiles for Windows Store Apps</span></span>
<span data-ttu-id="c8b0e-146">For Windows Store client applications, sending notifications to secondary tiles is the same as sending them to the primary one.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-146">For Windows Store client applications, sending notifications to secondary tiles is the same as sending them to the primary one.</span></span> <span data-ttu-id="c8b0e-147">This is also supported in installations.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-147">This is also supported in installations.</span></span> <span data-ttu-id="c8b0e-148">Secondary tiles have a different ChannelUri, which the SDK on your client app handles transparently.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-148">Secondary tiles have a different ChannelUri, which the SDK on your client app handles transparently.</span></span>

<span data-ttu-id="c8b0e-149">The SecondaryTiles dictionary uses the same TileId that is used to create the SecondaryTiles object in your Windows Store app.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-149">The SecondaryTiles dictionary uses the same TileId that is used to create the SecondaryTiles object in your Windows Store app.</span></span>
<span data-ttu-id="c8b0e-150">As with the primary ChannelUri, ChannelUris of secondary tiles can change at any moment.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-150">As with the primary ChannelUri, ChannelUris of secondary tiles can change at any moment.</span></span> <span data-ttu-id="c8b0e-151">In order to keep the installations in the notification hub updated, the device must refresh them with the current ChannelUris of the secondary tiles.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-151">In order to keep the installations in the notification hub updated, the device must refresh them with the current ChannelUris of the secondary tiles.</span></span>

## <a name="registration-management-from-the-device"></a><span data-ttu-id="c8b0e-152">Registration management from the device</span><span class="sxs-lookup"><span data-stu-id="c8b0e-152">Registration management from the device</span></span>
<span data-ttu-id="c8b0e-153">When managing device registration from client apps, the backend is only responsible for sending notifications.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-153">When managing device registration from client apps, the backend is only responsible for sending notifications.</span></span> <span data-ttu-id="c8b0e-154">Client apps keep PNS handles up-to-date, and register tags.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-154">Client apps keep PNS handles up-to-date, and register tags.</span></span> <span data-ttu-id="c8b0e-155">The following picture illustrates this pattern.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-155">The following picture illustrates this pattern.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-device.png)

<span data-ttu-id="c8b0e-156">The device first retrieves the PNS handle from the PNS, then registers with the notification hub directly.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-156">The device first retrieves the PNS handle from the PNS, then registers with the notification hub directly.</span></span> <span data-ttu-id="c8b0e-157">After the registration is successful, the app backend can send a notification targeting that registration.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-157">After the registration is successful, the app backend can send a notification targeting that registration.</span></span> <span data-ttu-id="c8b0e-158">For more information about how to send notifications, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="c8b0e-158">For more information about how to send notifications, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>
<span data-ttu-id="c8b0e-159">In this case, you use only Listen rights to access your notification hubs from the device.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-159">In this case, you use only Listen rights to access your notification hubs from the device.</span></span> <span data-ttu-id="c8b0e-160">For more information, see [Security](notification-hubs-push-notification-security.md).</span><span class="sxs-lookup"><span data-stu-id="c8b0e-160">For more information, see [Security](notification-hubs-push-notification-security.md).</span></span>

<span data-ttu-id="c8b0e-161">Registering from the device is the simplest method, but it has some drawbacks.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-161">Registering from the device is the simplest method, but it has some drawbacks.</span></span>
<span data-ttu-id="c8b0e-162">The first drawback is that a client app can only update its tags when the app is active.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-162">The first drawback is that a client app can only update its tags when the app is active.</span></span> <span data-ttu-id="c8b0e-163">For example, if a user has two devices that register tags related to sport teams, when the first device registers for an additional tag (for example, Seahawks), the second device will not receive the notifications about the Seahawks until the app on the second device is executed a second time.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-163">For example, if a user has two devices that register tags related to sport teams, when the first device registers for an additional tag (for example, Seahawks), the second device will not receive the notifications about the Seahawks until the app on the second device is executed a second time.</span></span> <span data-ttu-id="c8b0e-164">More generally, when tags are affected by multiple devices, managing tags from the backend is a desirable option.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-164">More generally, when tags are affected by multiple devices, managing tags from the backend is a desirable option.</span></span>
<span data-ttu-id="c8b0e-165">The second drawback of registration management from the client app is that, since apps can be hacked, securing the registration to specific tags requires extra care, as explained in the section “Tag-level security.”</span><span class="sxs-lookup"><span data-stu-id="c8b0e-165">The second drawback of registration management from the client app is that, since apps can be hacked, securing the registration to specific tags requires extra care, as explained in the section “Tag-level security.”</span></span>

#### <a name="example-code-to-register-with-a-notification-hub-from-a-device-using-an-installation"></a><span data-ttu-id="c8b0e-166">Example code to register with a notification hub from a device using an installation</span><span class="sxs-lookup"><span data-stu-id="c8b0e-166">Example code to register with a notification hub from a device using an installation</span></span>
<span data-ttu-id="c8b0e-167">At this time, this is only supported using the [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx).</span><span class="sxs-lookup"><span data-stu-id="c8b0e-167">At this time, this is only supported using the [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx).</span></span>

<span data-ttu-id="c8b0e-168">You can also use the PATCH method using the [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating the installation.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-168">You can also use the PATCH method using the [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating the installation.</span></span>

    class DeviceInstallation
    {
        public string installationId { get; set; }
        public string platform { get; set; }
        public string pushChannel { get; set; }
        public string[] tags { get; set; }
    }

    private async Task<HttpStatusCode> CreateOrUpdateInstallationAsync(DeviceInstallation deviceInstallation,
         string hubName, string listenConnectionString)
    {
        if (deviceInstallation.installationId == null)
            return HttpStatusCode.BadRequest;

        // Parse connection string (https://msdn.microsoft.com/library/azure/dn495627.aspx)
        ConnectionStringUtility connectionSaSUtil = new ConnectionStringUtility(listenConnectionString);
        string hubResource = "installations/" + deviceInstallation.installationId + "?";
        string apiVersion = "api-version=2015-04";

        // Determine the targetUri that we will sign
        string uri = connectionSaSUtil.Endpoint + hubName + "/" + hubResource + apiVersion;

        //=== Generate SaS Security Token for Authorization header ===
        // See, https://msdn.microsoft.com/library/azure/dn495627.aspx
        string SasToken = connectionSaSUtil.getSaSToken(uri, 60);

        using (var httpClient = new HttpClient())
        {
            string json = JsonConvert.SerializeObject(deviceInstallation);

            httpClient.DefaultRequestHeaders.Add("Authorization", SasToken);

            var response = await httpClient.PutAsync(uri, new StringContent(json, System.Text.Encoding.UTF8, "application/json"));
            return response.StatusCode;
        }
    }

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    string installationId = null;
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a installation id in application data, create and store as application data.
    if (!settings.ContainsKey("__NHInstallationId"))
    {
        installationId = Guid.NewGuid().ToString();
        settings.Add("__NHInstallationId", installationId);
    }

    installationId = (string)settings["__NHInstallationId"];

    var deviceInstallation = new DeviceInstallation
    {
        installationId = installationId,
        platform = "wns",
        pushChannel = channel.Uri,
        //tags = tags.ToArray<string>()
    };

    var statusCode = await CreateOrUpdateInstallationAsync(deviceInstallation, 
                        "<HUBNAME>", "<SHARED LISTEN CONNECTION STRING>");

    if (statusCode != HttpStatusCode.Accepted)
    {
        var dialog = new MessageDialog(statusCode.ToString(), "Registration failed. Installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
    else
    {
        var dialog = new MessageDialog("Registration successful using installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }



#### <a name="example-code-to-register-with-a-notification-hub-from-a-device-using-a-registration"></a><span data-ttu-id="c8b0e-169">Example code to register with a notification hub from a device using a registration</span><span class="sxs-lookup"><span data-stu-id="c8b0e-169">Example code to register with a notification hub from a device using a registration</span></span>
<span data-ttu-id="c8b0e-170">These methods create or update a registration for the device on which they are called.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-170">These methods create or update a registration for the device on which they are called.</span></span> <span data-ttu-id="c8b0e-171">This means that in order to update the handle or the tags, you must overwrite the entire registration.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-171">This means that in order to update the handle or the tags, you must overwrite the entire registration.</span></span> <span data-ttu-id="c8b0e-172">Remember that registrations are transient, so you should always have a reliable store with the current tags that a specific device needs.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-172">Remember that registrations are transient, so you should always have a reliable store with the current tags that a specific device needs.</span></span>

    // Initialize the Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // The Device id from the PNS
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // If you are registering from the client itself, then store this registration id in device
    // storage. Then when the app starts, you can check if a registration id already exists or not before
    // creating.
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a registration id in application data, store in application data.
    if (!settings.ContainsKey("__NHRegistrationId"))
    {
        // make sure there are no existing registrations for this push handle (used for iOS and Android)    
        string newRegistrationId = null;
        var registrations = await hub.GetRegistrationsByChannelAsync(pushChannel.Uri, 100);
        foreach (RegistrationDescription registration in registrations)
        {
            if (newRegistrationId == null)
            {
                newRegistrationId = registration.RegistrationId;
            }
            else
            {
                await hub.DeleteRegistrationAsync(registration);
            }
        }

        newRegistrationId = await hub.CreateRegistrationIdAsync();

        settings.Add("__NHRegistrationId", newRegistrationId);
    }

    string regId = (string)settings["__NHRegistrationId"];

    RegistrationDescription registration = new WindowsRegistrationDescription(pushChannel.Uri);
    registration.RegistrationId = regId;
    registration.Tags = new HashSet<string>(YourTags);

    try
    {
        await hub.CreateOrUpdateRegistrationAsync(registration);
    }
    catch (Microsoft.WindowsAzure.Messaging.RegistrationGoneException e)
    {
        settings.Remove("__NHRegistrationId");
    }


## <a name="registration-management-from-a-backend"></a><span data-ttu-id="c8b0e-173">Registration management from a backend</span><span class="sxs-lookup"><span data-stu-id="c8b0e-173">Registration management from a backend</span></span>
<span data-ttu-id="c8b0e-174">Managing registrations from the backend requires writing additional code.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-174">Managing registrations from the backend requires writing additional code.</span></span> <span data-ttu-id="c8b0e-175">The app from the device must provide the updated PNS handle to the backend every time the app starts (along with tags and templates), and the backend must update this handle on the notification hub.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-175">The app from the device must provide the updated PNS handle to the backend every time the app starts (along with tags and templates), and the backend must update this handle on the notification hub.</span></span> <span data-ttu-id="c8b0e-176">The following picture illustrates this design.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-176">The following picture illustrates this design.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-backend.png)

<span data-ttu-id="c8b0e-177">The advantages of managing registrations from the backend include the ability to modify tags to registrations even when the corresponding app on the device is inactive, and to authenticate the client app before adding a tag to its registration.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-177">The advantages of managing registrations from the backend include the ability to modify tags to registrations even when the corresponding app on the device is inactive, and to authenticate the client app before adding a tag to its registration.</span></span>

#### <a name="example-code-to-register-with-a-notification-hub-from-a-backend-using-an-installation"></a><span data-ttu-id="c8b0e-178">Example code to register with a notification hub from a backend using an installation</span><span class="sxs-lookup"><span data-stu-id="c8b0e-178">Example code to register with a notification hub from a backend using an installation</span></span>
<span data-ttu-id="c8b0e-179">The client device still gets its PNS handle and relevant installation properties as before and calls a custom API on the backend that can perform the registration and authorize tags etc. The backend can leverage the [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="c8b0e-179">The client device still gets its PNS handle and relevant installation properties as before and calls a custom API on the backend that can perform the registration and authorize tags etc. The backend can leverage the [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="c8b0e-180">You can also use the PATCH method using the [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating the installation.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-180">You can also use the PATCH method using the [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating the installation.</span></span>

    // Initialize the Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // Custom API on the backend
    public async Task<HttpResponseMessage> Put(DeviceInstallation deviceUpdate)
    {

        Installation installation = new Installation();
        installation.InstallationId = deviceUpdate.InstallationId;
        installation.PushChannel = deviceUpdate.Handle;
        installation.Tags = deviceUpdate.Tags;

        switch (deviceUpdate.Platform)
        {
            case "mpns":
                installation.Platform = NotificationPlatform.Mpns;
                break;
            case "wns":
                installation.Platform = NotificationPlatform.Wns;
                break;
            case "apns":
                installation.Platform = NotificationPlatform.Apns;
                break;
            case "gcm":
                installation.Platform = NotificationPlatform.Gcm;
                break;
            default:
                throw new HttpResponseException(HttpStatusCode.BadRequest);
        }


        // In the backend we can control if a user is allowed to add tags
        //installation.Tags = new List<string>(deviceUpdate.Tags);
        //installation.Tags.Add("username:" + username);

        await hub.CreateOrUpdateInstallationAsync(installation);

        return Request.CreateResponse(HttpStatusCode.OK);
    }


#### <a name="example-code-to-register-with-a-notification-hub-from-a-device-using-a-registration-id"></a><span data-ttu-id="c8b0e-181">Example code to register with a notification hub from a device using a registration ID</span><span class="sxs-lookup"><span data-stu-id="c8b0e-181">Example code to register with a notification hub from a device using a registration ID</span></span>
<span data-ttu-id="c8b0e-182">From your app backend, you can perform basic CRUDS operations on registrations.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-182">From your app backend, you can perform basic CRUDS operations on registrations.</span></span> <span data-ttu-id="c8b0e-183">For example:</span><span class="sxs-lookup"><span data-stu-id="c8b0e-183">For example:</span></span>

    var hub = NotificationHubClient.CreateClientFromConnectionString("{connectionString}", "hubName");

    // create a registration description object of the correct type, e.g.
    var reg = new WindowsRegistrationDescription(channelUri, tags);

    // Create
    await hub.CreateRegistrationAsync(reg);

    // Get by id
    var r = await hub.GetRegistrationAsync<RegistrationDescription>("id");

    // update
    r.Tags.Add("myTag");

    // update on hub
    await hub.UpdateRegistrationAsync(r);

    // delete
    await hub.DeleteRegistrationAsync(r);


<span data-ttu-id="c8b0e-184">The backend must handle concurrency between registration updates.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-184">The backend must handle concurrency between registration updates.</span></span> <span data-ttu-id="c8b0e-185">Service Bus offers optimistic concurrency control for registration management.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-185">Service Bus offers optimistic concurrency control for registration management.</span></span> <span data-ttu-id="c8b0e-186">At the HTTP level, this is implemented with the use of ETag on registration management operations.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-186">At the HTTP level, this is implemented with the use of ETag on registration management operations.</span></span> <span data-ttu-id="c8b0e-187">This feature is transparently used by Microsoft SDKs, which throw an exception if an update is rejected for concurrency reasons.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-187">This feature is transparently used by Microsoft SDKs, which throw an exception if an update is rejected for concurrency reasons.</span></span> <span data-ttu-id="c8b0e-188">The app backend is responsible for handling these exceptions and retrying the update if necessary.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-188">The app backend is responsible for handling these exceptions and retrying the update if necessary.</span></span>

