---
title: Send notifications to specific devices (Universal Windows Platform) | Microsoft Docs
description: Use Azure Notification Hubs with tags in the registration to send breaking news to a Universal Windows Platform app.
services: notification-hubs
documentationcenter: windows
author: dimazaid
manager: kpiteira
editor: spelluru
ms.assetid: 994d2eed-f62e-433c-bf65-4afebf1c0561
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: tutorial
ms.custom: mvc
ms.date: 04/14/2018
ms.author: dimazaid
ms.openlocfilehash: b95f3f4b45b0a4e32c4ce08c58bedf68c9dc44c2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44809860"
---
# <a name="tutorial-push-notifications-to-specific-windows-devices-running-universal-windows-platform-applications"></a><span data-ttu-id="dec0b-103">Tutorial: Push notifications to specific Windows devices running Universal Windows Platform applications</span><span class="sxs-lookup"><span data-stu-id="dec0b-103">Tutorial: Push notifications to specific Windows devices running Universal Windows Platform applications</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="dec0b-104">Overview</span><span class="sxs-lookup"><span data-stu-id="dec0b-104">Overview</span></span>
<span data-ttu-id="dec0b-105">This tutorial shows you how to use Azure Notification Hubs to broadcast breaking news notifications to a Windows Store or Windows Phone 8.1 (non-Silverlight) applications.</span><span class="sxs-lookup"><span data-stu-id="dec0b-105">This tutorial shows you how to use Azure Notification Hubs to broadcast breaking news notifications to a Windows Store or Windows Phone 8.1 (non-Silverlight) applications.</span></span> <span data-ttu-id="dec0b-106">If you are targeting Windows Phone 8.1 Silverlight, see [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) version.</span><span class="sxs-lookup"><span data-stu-id="dec0b-106">If you are targeting Windows Phone 8.1 Silverlight, see [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) version.</span></span> 

<span data-ttu-id="dec0b-107">In this tutorial, you learn how to use Azure Notification Hubs to push notifications to specific Windows devices running Universal Windows Platform (UWP) application.</span><span class="sxs-lookup"><span data-stu-id="dec0b-107">In this tutorial, you learn how to use Azure Notification Hubs to push notifications to specific Windows devices running Universal Windows Platform (UWP) application.</span></span> <span data-ttu-id="dec0b-108">After you complete the tutorial, you can register for the breaking news categories that you are interested in, and you'll receive push notifications for those categories only.</span><span class="sxs-lookup"><span data-stu-id="dec0b-108">After you complete the tutorial, you can register for the breaking news categories that you are interested in, and you'll receive push notifications for those categories only.</span></span> 

<span data-ttu-id="dec0b-109">Broadcast scenarios are enabled by including one or more *tags* when you create a registration in the notification hub.</span><span class="sxs-lookup"><span data-stu-id="dec0b-109">Broadcast scenarios are enabled by including one or more *tags* when you create a registration in the notification hub.</span></span> <span data-ttu-id="dec0b-110">When notifications are sent to a tag, all devices that have registered for the tag receive the notification.</span><span class="sxs-lookup"><span data-stu-id="dec0b-110">When notifications are sent to a tag, all devices that have registered for the tag receive the notification.</span></span> <span data-ttu-id="dec0b-111">For more information about tags, see [Tags in Registrations](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="dec0b-111">For more information about tags, see [Tags in Registrations](notification-hubs-tags-segment-push-message.md).</span></span>

> [!NOTE]
> <span data-ttu-id="dec0b-112">Windows Store and Windows Phone project versions 8.1 and earlier are not supported in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="dec0b-112">Windows Store and Windows Phone project versions 8.1 and earlier are not supported in Visual Studio 2017.</span></span> <span data-ttu-id="dec0b-113">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="dec0b-113">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span> 

<span data-ttu-id="dec0b-114">In this tutorial, you take the following steps:</span><span class="sxs-lookup"><span data-stu-id="dec0b-114">In this tutorial, you take the following steps:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dec0b-115">Add category selection to the mobile app</span><span class="sxs-lookup"><span data-stu-id="dec0b-115">Add category selection to the mobile app</span></span>
> * <span data-ttu-id="dec0b-116">Register for notifications</span><span class="sxs-lookup"><span data-stu-id="dec0b-116">Register for notifications</span></span>
> * <span data-ttu-id="dec0b-117">Send tagged notification</span><span class="sxs-lookup"><span data-stu-id="dec0b-117">Send tagged notification</span></span>
> * <span data-ttu-id="dec0b-118">Run the app and generate notifications</span><span class="sxs-lookup"><span data-stu-id="dec0b-118">Run the app and generate notifications</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dec0b-119">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="dec0b-119">Prerequisites</span></span>
<span data-ttu-id="dec0b-120">Complete the [Tutorial: Send notifications to Universal Windows Platform apps by using Azure Notification Hubs][get-started] before starting this tutorial.</span><span class="sxs-lookup"><span data-stu-id="dec0b-120">Complete the [Tutorial: Send notifications to Universal Windows Platform apps by using Azure Notification Hubs][get-started] before starting this tutorial.</span></span>  

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="dec0b-121">Add category selection to the app</span><span class="sxs-lookup"><span data-stu-id="dec0b-121">Add category selection to the app</span></span>
<span data-ttu-id="dec0b-122">The first step is to add UI elements to your existing main page so that users can select categories to register.</span><span class="sxs-lookup"><span data-stu-id="dec0b-122">The first step is to add UI elements to your existing main page so that users can select categories to register.</span></span> <span data-ttu-id="dec0b-123">The selected categories are stored on the device.</span><span class="sxs-lookup"><span data-stu-id="dec0b-123">The selected categories are stored on the device.</span></span> <span data-ttu-id="dec0b-124">When the app starts, a device registration is created in your notification hub, with the selected categories as tags.</span><span class="sxs-lookup"><span data-stu-id="dec0b-124">When the app starts, a device registration is created in your notification hub, with the selected categories as tags.</span></span>

1. <span data-ttu-id="dec0b-125">Open the MainPage.xaml project file, and then copy the following code in the **Grid** element:</span><span class="sxs-lookup"><span data-stu-id="dec0b-125">Open the MainPage.xaml project file, and then copy the following code in the **Grid** element:</span></span>
   
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition/>
                <ColumnDefinition/>
            </Grid.ColumnDefinitions>
            <TextBlock Grid.Row="0" Grid.Column="0" Grid.ColumnSpan="2"  TextWrapping="Wrap" Text="Breaking News" FontSize="42" VerticalAlignment="Top" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="World" Name="WorldToggle" Grid.Row="1" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Politics" Name="PoliticsToggle" Grid.Row="2" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Business" Name="BusinessToggle" Grid.Row="3" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Technology" Name="TechnologyToggle" Grid.Row="1" Grid.Column="1" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Science" Name="ScienceToggle" Grid.Row="2" Grid.Column="1" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Sports" Name="SportsToggle" Grid.Row="3" Grid.Column="1" HorizontalAlignment="Center"/>
            <Button Name="SubscribeButton" Content="Subscribe" HorizontalAlignment="Center" Grid.Row="4" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click"/>
        </Grid>

2. <span data-ttu-id="dec0b-126">In **Solution Explorer**, right-click the project, add a new class: **Notifications**.</span><span class="sxs-lookup"><span data-stu-id="dec0b-126">In **Solution Explorer**, right-click the project, add a new class: **Notifications**.</span></span> <span data-ttu-id="dec0b-127">Add the **public** modifier to the class definition, and then add the following **using** statements to the new code file:</span><span class="sxs-lookup"><span data-stu-id="dec0b-127">Add the **public** modifier to the class definition, and then add the following **using** statements to the new code file:</span></span>

    ```csharp   
    using Windows.Networking.PushNotifications;
    using Microsoft.WindowsAzure.Messaging;
    using Windows.Storage;
    using System.Threading.Tasks;
    ```

3. <span data-ttu-id="dec0b-128">Copy the following code to the new **Notifications** class:</span><span class="sxs-lookup"><span data-stu-id="dec0b-128">Copy the following code to the new **Notifications** class:</span></span>
   
    ```csharp
    private NotificationHub hub;

    public Notifications(string hubName, string listenConnectionString)
    {
        hub = new NotificationHub(hubName, listenConnectionString);
    }

    public async Task<Registration> StoreCategoriesAndSubscribe(IEnumerable<string> categories)
    {
        ApplicationData.Current.LocalSettings.Values["categories"] = string.Join(",", categories);
        return await SubscribeToCategories(categories);
    }

    public IEnumerable<string> RetrieveCategories()
    {
        var categories = (string) ApplicationData.Current.LocalSettings.Values["categories"];
        return categories != null ? categories.Split(','): new string[0];
    }

    public async Task<Registration> SubscribeToCategories(IEnumerable<string> categories = null)
    {
        var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

        if (categories == null)
        {
            categories = RetrieveCategories();
        }

        // Using a template registration to support notifications across platforms.
        // Any template notifications that contain messageParam and a corresponding tag expression
        // will be delivered for this registration.

        const string templateBodyWNS = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(messageParam)</text></binding></visual></toast>";

        return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "simpleWNSTemplateExample",
                categories);
    }
    ```
   
    <span data-ttu-id="dec0b-129">This class uses the local storage to store the categories of news that this device must receive.</span><span class="sxs-lookup"><span data-stu-id="dec0b-129">This class uses the local storage to store the categories of news that this device must receive.</span></span> <span data-ttu-id="dec0b-130">Instead of calling the *RegisterNativeAsync* method, call *RegisterTemplateAsync* to register for the categories by using a template registration.</span><span class="sxs-lookup"><span data-stu-id="dec0b-130">Instead of calling the *RegisterNativeAsync* method, call *RegisterTemplateAsync* to register for the categories by using a template registration.</span></span> 
   
    <span data-ttu-id="dec0b-131">If you want to register more than one template (for example, one for toast notifications and one for tiles), provide a template name (for example, "simpleWNSTemplateExample").</span><span class="sxs-lookup"><span data-stu-id="dec0b-131">If you want to register more than one template (for example, one for toast notifications and one for tiles), provide a template name (for example, "simpleWNSTemplateExample").</span></span> <span data-ttu-id="dec0b-132">You name the templates so that you can update or delete them.</span><span class="sxs-lookup"><span data-stu-id="dec0b-132">You name the templates so that you can update or delete them.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="dec0b-133">If a device registers multiple templates with the same tag, an incoming message that targets the tag causes multiple notifications to be delivered to the device (one for each template).</span><span class="sxs-lookup"><span data-stu-id="dec0b-133">If a device registers multiple templates with the same tag, an incoming message that targets the tag causes multiple notifications to be delivered to the device (one for each template).</span></span> <span data-ttu-id="dec0b-134">This behavior is useful when the same logical message must result in multiple visual notifications (for example, showing both a badge and a toast in a Windows Store application).</span><span class="sxs-lookup"><span data-stu-id="dec0b-134">This behavior is useful when the same logical message must result in multiple visual notifications (for example, showing both a badge and a toast in a Windows Store application).</span></span>
   
    <span data-ttu-id="dec0b-135">For more information, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="dec0b-135">For more information, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>

4. <span data-ttu-id="dec0b-136">In the App.xaml.cs project file, add the following property to the **App** class:</span><span class="sxs-lookup"><span data-stu-id="dec0b-136">In the App.xaml.cs project file, add the following property to the **App** class:</span></span>

    ```csharp   
    public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
    ```
   
    <span data-ttu-id="dec0b-137">You use this property to create and access a **Notifications** instance.</span><span class="sxs-lookup"><span data-stu-id="dec0b-137">You use this property to create and access a **Notifications** instance.</span></span>
   
    <span data-ttu-id="dec0b-138">In the code, replace the `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and the connection string for *DefaultListenSharedAccessSignature*, which you obtained earlier.</span><span class="sxs-lookup"><span data-stu-id="dec0b-138">In the code, replace the `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and the connection string for *DefaultListenSharedAccessSignature*, which you obtained earlier.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="dec0b-139">Because credentials that are distributed with a client app are not usually secure, distribute only the key for *listen* access with your client app.</span><span class="sxs-lookup"><span data-stu-id="dec0b-139">Because credentials that are distributed with a client app are not usually secure, distribute only the key for *listen* access with your client app.</span></span> <span data-ttu-id="dec0b-140">With listen access, your app can register for notifications, but existing registrations cannot be modified, and notifications cannot be sent.</span><span class="sxs-lookup"><span data-stu-id="dec0b-140">With listen access, your app can register for notifications, but existing registrations cannot be modified, and notifications cannot be sent.</span></span> <span data-ttu-id="dec0b-141">The full access key is used in a secured back-end service for sending notifications and changing existing registrations.</span><span class="sxs-lookup"><span data-stu-id="dec0b-141">The full access key is used in a secured back-end service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
5. <span data-ttu-id="dec0b-142">In the MainPage.xaml.cs project file, add the following line:</span><span class="sxs-lookup"><span data-stu-id="dec0b-142">In the MainPage.xaml.cs project file, add the following line:</span></span>
   
    ```csharp
    using Windows.UI.Popups;
    ```

6. <span data-ttu-id="dec0b-143">In the MainPage.xaml.cs project file, add the following method:</span><span class="sxs-lookup"><span data-stu-id="dec0b-143">In the MainPage.xaml.cs project file, add the following method:</span></span>
   
    ```csharp
    private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
    {
        var categories = new HashSet<string>();
        if (WorldToggle.IsOn) categories.Add("World");
        if (PoliticsToggle.IsOn) categories.Add("Politics");
        if (BusinessToggle.IsOn) categories.Add("Business");
        if (TechnologyToggle.IsOn) categories.Add("Technology");
        if (ScienceToggle.IsOn) categories.Add("Science");
        if (SportsToggle.IsOn) categories.Add("Sports");

        var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(categories);

        var dialog = new MessageDialog("Subscribed to: " + string.Join(",", categories) + " on registration Id: " + result.RegistrationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
    ```

    <span data-ttu-id="dec0b-144">This method creates a list of categories and uses the **Notifications** class to store the list in the local storage.</span><span class="sxs-lookup"><span data-stu-id="dec0b-144">This method creates a list of categories and uses the **Notifications** class to store the list in the local storage.</span></span> <span data-ttu-id="dec0b-145">It also registers the corresponding tags with your notification hub.</span><span class="sxs-lookup"><span data-stu-id="dec0b-145">It also registers the corresponding tags with your notification hub.</span></span> <span data-ttu-id="dec0b-146">When the categories are changed, the registration is re-created with the new categories.</span><span class="sxs-lookup"><span data-stu-id="dec0b-146">When the categories are changed, the registration is re-created with the new categories.</span></span>

<span data-ttu-id="dec0b-147">Your app can now store a set of categories in local storage on the device.</span><span class="sxs-lookup"><span data-stu-id="dec0b-147">Your app can now store a set of categories in local storage on the device.</span></span> <span data-ttu-id="dec0b-148">The app registers with the notification hub whenever users change the category selection.</span><span class="sxs-lookup"><span data-stu-id="dec0b-148">The app registers with the notification hub whenever users change the category selection.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="dec0b-149">Register for notifications</span><span class="sxs-lookup"><span data-stu-id="dec0b-149">Register for notifications</span></span>
<span data-ttu-id="dec0b-150">In this section, you register with the notification hub on startup by using the categories that you've stored in local storage.</span><span class="sxs-lookup"><span data-stu-id="dec0b-150">In this section, you register with the notification hub on startup by using the categories that you've stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="dec0b-151">Because the channel URI that's assigned by the Windows Notification Service (WNS) can change at any time, you should register for notifications frequently to avoid notification failures.</span><span class="sxs-lookup"><span data-stu-id="dec0b-151">Because the channel URI that's assigned by the Windows Notification Service (WNS) can change at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="dec0b-152">This example registers for notification every time that the app starts.</span><span class="sxs-lookup"><span data-stu-id="dec0b-152">This example registers for notification every time that the app starts.</span></span> <span data-ttu-id="dec0b-153">For apps that you run frequently (more than once a day), you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span><span class="sxs-lookup"><span data-stu-id="dec0b-153">For apps that you run frequently (more than once a day), you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
> 
> 

1. <span data-ttu-id="dec0b-154">To use the `notifications` class to subscribe based on categories, open the App.xaml.cs file, and then update the **InitNotificationsAsync** method.</span><span class="sxs-lookup"><span data-stu-id="dec0b-154">To use the `notifications` class to subscribe based on categories, open the App.xaml.cs file, and then update the **InitNotificationsAsync** method.</span></span>
   
    ```csharp
    // *** Remove or comment out these lines *** 
    //var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
    //var hub = new NotificationHub("your hub name", "your listen connection string");
    //var result = await hub.RegisterNativeAsync(channel.Uri);

    var result = await notifications.SubscribeToCategories();
   ```
    <span data-ttu-id="dec0b-155">This process ensures that when the app starts, it retrieves the categories from local storage and requests registration of these categories.</span><span class="sxs-lookup"><span data-stu-id="dec0b-155">This process ensures that when the app starts, it retrieves the categories from local storage and requests registration of these categories.</span></span> <span data-ttu-id="dec0b-156">You created the **InitNotificationsAsync** method as part of the [Get started with Notification Hubs][get-started] tutorial.</span><span class="sxs-lookup"><span data-stu-id="dec0b-156">You created the **InitNotificationsAsync** method as part of the [Get started with Notification Hubs][get-started] tutorial.</span></span>
2. <span data-ttu-id="dec0b-157">In the MainPage.xaml.cs project file, add the following code to the *OnNavigatedTo* method:</span><span class="sxs-lookup"><span data-stu-id="dec0b-157">In the MainPage.xaml.cs project file, add the following code to the *OnNavigatedTo* method:</span></span>
   
    ```csharp
    protected override void OnNavigatedTo(NavigationEventArgs e)
    {
        var categories = ((App)Application.Current).notifications.RetrieveCategories();

        if (categories.Contains("World")) WorldToggle.IsOn = true;
        if (categories.Contains("Politics")) PoliticsToggle.IsOn = true;
        if (categories.Contains("Business")) BusinessToggle.IsOn = true;
        if (categories.Contains("Technology")) TechnologyToggle.IsOn = true;
        if (categories.Contains("Science")) ScienceToggle.IsOn = true;
        if (categories.Contains("Sports")) SportsToggle.IsOn = true;
    }
    ```

    <span data-ttu-id="dec0b-158">This code updates the main page, based on the status of previously saved categories.</span><span class="sxs-lookup"><span data-stu-id="dec0b-158">This code updates the main page, based on the status of previously saved categories.</span></span>

<span data-ttu-id="dec0b-159">The app is now complete.</span><span class="sxs-lookup"><span data-stu-id="dec0b-159">The app is now complete.</span></span> <span data-ttu-id="dec0b-160">It can store a set of categories in the device local storage that's used to register with the notification hub when users change the category selection.</span><span class="sxs-lookup"><span data-stu-id="dec0b-160">It can store a set of categories in the device local storage that's used to register with the notification hub when users change the category selection.</span></span> <span data-ttu-id="dec0b-161">In the next section, you define a back end that can send category notifications to this app.</span><span class="sxs-lookup"><span data-stu-id="dec0b-161">In the next section, you define a back end that can send category notifications to this app.</span></span>

## <a name="send-tagged-notifications"></a><span data-ttu-id="dec0b-162">Send tagged notifications</span><span class="sxs-lookup"><span data-stu-id="dec0b-162">Send tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="dec0b-163">Run the app and generate notifications</span><span class="sxs-lookup"><span data-stu-id="dec0b-163">Run the app and generate notifications</span></span>
1. <span data-ttu-id="dec0b-164">In Visual Studio, select **F5** to compile and start the app.</span><span class="sxs-lookup"><span data-stu-id="dec0b-164">In Visual Studio, select **F5** to compile and start the app.</span></span> <span data-ttu-id="dec0b-165">The app UI provides a set of toggles that lets you choose the categories to subscribe to.</span><span class="sxs-lookup"><span data-stu-id="dec0b-165">The app UI provides a set of toggles that lets you choose the categories to subscribe to.</span></span> 
   
    ![Breaking News app][1]

2. <span data-ttu-id="dec0b-167">Enable one or more category toggles, and then click **Subscribe**.</span><span class="sxs-lookup"><span data-stu-id="dec0b-167">Enable one or more category toggles, and then click **Subscribe**.</span></span>
   
    <span data-ttu-id="dec0b-168">The app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span><span class="sxs-lookup"><span data-stu-id="dec0b-168">The app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span> <span data-ttu-id="dec0b-169">The registered categories are returned and displayed in a dialog box.</span><span class="sxs-lookup"><span data-stu-id="dec0b-169">The registered categories are returned and displayed in a dialog box.</span></span>
   
    ![Category toggles and Subscribe button][19]

3. <span data-ttu-id="dec0b-171">Send a new notification from the back end in one of the following ways:</span><span class="sxs-lookup"><span data-stu-id="dec0b-171">Send a new notification from the back end in one of the following ways:</span></span>

   * <span data-ttu-id="dec0b-172">**Console app**: Start the console app.</span><span class="sxs-lookup"><span data-stu-id="dec0b-172">**Console app**: Start the console app.</span></span>
   * <span data-ttu-id="dec0b-173">**Java/PHP**: Run your app or script.</span><span class="sxs-lookup"><span data-stu-id="dec0b-173">**Java/PHP**: Run your app or script.</span></span>
     
     <span data-ttu-id="dec0b-174">Notifications for the selected categories appear as toast notifications.</span><span class="sxs-lookup"><span data-stu-id="dec0b-174">Notifications for the selected categories appear as toast notifications.</span></span>
     
     ![Toast notifications][14]

## <a name="next-steps"></a><span data-ttu-id="dec0b-176">Next steps</span><span class="sxs-lookup"><span data-stu-id="dec0b-176">Next steps</span></span>
<span data-ttu-id="dec0b-177">In this article, you learned how to broadcast breaking news by category.</span><span class="sxs-lookup"><span data-stu-id="dec0b-177">In this article, you learned how to broadcast breaking news by category.</span></span> <span data-ttu-id="dec0b-178">The backend application pushes tagged notifications to devices that have registered to receive notifications for that tag.</span><span class="sxs-lookup"><span data-stu-id="dec0b-178">The backend application pushes tagged notifications to devices that have registered to receive notifications for that tag.</span></span> <span data-ttu-id="dec0b-179">To learn how to push notifications to specific users irrespective of what device they use, advance to the following tutorial:</span><span class="sxs-lookup"><span data-stu-id="dec0b-179">To learn how to push notifications to specific users irrespective of what device they use, advance to the following tutorial:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dec0b-180">Push localized notifications</span><span class="sxs-lookup"><span data-stu-id="dec0b-180">Push localized notifications</span></span>](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)

<!-- Anchors. -->
[Add category selection to the app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run the app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-breakingnews-win1.png

[14]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-toast-2.png


[19]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-reg-2.png

<!-- URLs.-->
[get-started]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[Use Notification Hubs to broadcast localized breaking news]: notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md
[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
