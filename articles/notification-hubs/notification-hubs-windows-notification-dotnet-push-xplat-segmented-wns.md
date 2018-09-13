---
title: Use Notification Hubs to send breaking news (Windows Universal)
description: Use Azure Notification Hubs with tags in the registration to send breaking news to a universal Windows app.
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: ''
ms.assetid: 994d2eed-f62e-433c-bf65-4afebf1c0561
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 0ac6af8d4d981042fe1f8f6f91e931845507f6f0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555994"
---
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="472f1-103">Use Notification Hubs to send breaking news</span><span class="sxs-lookup"><span data-stu-id="472f1-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="472f1-104">Overview</span><span class="sxs-lookup"><span data-stu-id="472f1-104">Overview</span></span>
<span data-ttu-id="472f1-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to a Windows Store or Windows Phone 8.1 (non-Silverlight) app.</span><span class="sxs-lookup"><span data-stu-id="472f1-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to a Windows Store or Windows Phone 8.1 (non-Silverlight) app.</span></span> <span data-ttu-id="472f1-106">If you are targeting Windows Phone 8.1 Silverlight, please refer to the [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) version.</span><span class="sxs-lookup"><span data-stu-id="472f1-106">If you are targeting Windows Phone 8.1 Silverlight, please refer to the [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) version.</span></span> <span data-ttu-id="472f1-107">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span><span class="sxs-lookup"><span data-stu-id="472f1-107">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="472f1-108">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, and so on.</span><span class="sxs-lookup"><span data-stu-id="472f1-108">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, and so on.</span></span> 

<span data-ttu-id="472f1-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span><span class="sxs-lookup"><span data-stu-id="472f1-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="472f1-110">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span><span class="sxs-lookup"><span data-stu-id="472f1-110">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="472f1-111">Because tags are simply strings, they do not have to be provisioned in advance.</span><span class="sxs-lookup"><span data-stu-id="472f1-111">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="472f1-112">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="472f1-112">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="472f1-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="472f1-113">Prerequisites</span></span>
<span data-ttu-id="472f1-114">This topic builds on the app you created in [Get started with Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="472f1-114">This topic builds on the app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="472f1-115">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="472f1-115">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="472f1-116">Add category selection to the app</span><span class="sxs-lookup"><span data-stu-id="472f1-116">Add category selection to the app</span></span>
<span data-ttu-id="472f1-117">The first step is to add the UI elements to your existing main page that enable the user to select categories to register.</span><span class="sxs-lookup"><span data-stu-id="472f1-117">The first step is to add the UI elements to your existing main page that enable the user to select categories to register.</span></span> <span data-ttu-id="472f1-118">The categories selected by a user are stored on the device.</span><span class="sxs-lookup"><span data-stu-id="472f1-118">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="472f1-119">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span><span class="sxs-lookup"><span data-stu-id="472f1-119">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="472f1-120">Open the MainPage.xaml project file, then copy the following code in the **Grid** element:</span><span class="sxs-lookup"><span data-stu-id="472f1-120">Open the MainPage.xaml project file, then copy the following code in the **Grid** element:</span></span>
   
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
2. <span data-ttu-id="472f1-121">Right click the **Shared** project and add a new class named **Notifications**, add the **public** modifier to the class definition, then add the following **using** statements to the new code file:</span><span class="sxs-lookup"><span data-stu-id="472f1-121">Right click the **Shared** project and add a new class named **Notifications**, add the **public** modifier to the class definition, then add the following **using** statements to the new code file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.Storage;
        using System.Threading.Tasks;
3. <span data-ttu-id="472f1-122">Copy the following code into the new **Notifications** class:</span><span class="sxs-lookup"><span data-stu-id="472f1-122">Copy the following code into the new **Notifications** class:</span></span>
   
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
   
    <span data-ttu-id="472f1-123">This class uses the local storage to store the categories of news that this device has to receive.</span><span class="sxs-lookup"><span data-stu-id="472f1-123">This class uses the local storage to store the categories of news that this device has to receive.</span></span> <span data-ttu-id="472f1-124">Note that instead of calling the *RegisterNativeAsync* method we call *RegisterTemplateAsync* to register for the categories using a template registration.</span><span class="sxs-lookup"><span data-stu-id="472f1-124">Note that instead of calling the *RegisterNativeAsync* method we call *RegisterTemplateAsync* to register for the categories using a template registration.</span></span> 
   
    <span data-ttu-id="472f1-125">We also provide a name for the template ("simpleWNSTemplateExample"), because we might want to register more than one template (for instance one for toast notifications and one for tiles) and we need to name them in order to be able to update or delete them.</span><span class="sxs-lookup"><span data-stu-id="472f1-125">We also provide a name for the template ("simpleWNSTemplateExample"), because we might want to register more than one template (for instance one for toast notifications and one for tiles) and we need to name them in order to be able to update or delete them.</span></span>
   
    <span data-ttu-id="472f1-126">Note that if a device registers multiple templates with the same tag, an incoming message targeting that tag will result in multiple notifications delivered to the device (one for each template).</span><span class="sxs-lookup"><span data-stu-id="472f1-126">Note that if a device registers multiple templates with the same tag, an incoming message targeting that tag will result in multiple notifications delivered to the device (one for each template).</span></span> <span data-ttu-id="472f1-127">This behavior is useful when the same logical message has to result in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span><span class="sxs-lookup"><span data-stu-id="472f1-127">This behavior is useful when the same logical message has to result in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
   
    <span data-ttu-id="472f1-128">For more information on templates, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="472f1-128">For more information on templates, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>
4. <span data-ttu-id="472f1-129">In the App.xaml.cs project file, add the following property to the **App** class:</span><span class="sxs-lookup"><span data-stu-id="472f1-129">In the App.xaml.cs project file, add the following property to the **App** class:</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
    <span data-ttu-id="472f1-130">This property is used to create and access a **Notifications** instance.</span><span class="sxs-lookup"><span data-stu-id="472f1-130">This property is used to create and access a **Notifications** instance.</span></span>
   
    <span data-ttu-id="472f1-131">In the above code, replace the `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span><span class="sxs-lookup"><span data-stu-id="472f1-131">In the above code, replace the `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="472f1-132">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span><span class="sxs-lookup"><span data-stu-id="472f1-132">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="472f1-133">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span><span class="sxs-lookup"><span data-stu-id="472f1-133">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="472f1-134">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span><span class="sxs-lookup"><span data-stu-id="472f1-134">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
5. <span data-ttu-id="472f1-135">In your MainPage.xaml.cs, add the following line:</span><span class="sxs-lookup"><span data-stu-id="472f1-135">In your MainPage.xaml.cs, add the following line:</span></span>
   
        using Windows.UI.Popups;
6. <span data-ttu-id="472f1-136">In the MainPage.xaml.cs project file, add the following method:</span><span class="sxs-lookup"><span data-stu-id="472f1-136">In the MainPage.xaml.cs project file, add the following method:</span></span>
   
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
   
    <span data-ttu-id="472f1-137">This method creates a list of categories and uses the **Notifications** class to store the list in the local storage and register the corresponding tags with your notification hub.</span><span class="sxs-lookup"><span data-stu-id="472f1-137">This method creates a list of categories and uses the **Notifications** class to store the list in the local storage and register the corresponding tags with your notification hub.</span></span> <span data-ttu-id="472f1-138">When categories are changed, the registration is recreated with the new categories.</span><span class="sxs-lookup"><span data-stu-id="472f1-138">When categories are changed, the registration is recreated with the new categories.</span></span>

<span data-ttu-id="472f1-139">Your app is now able to store a set of categories in local storage on the device and register with the notification hub whenever the user changes the selection of categories.</span><span class="sxs-lookup"><span data-stu-id="472f1-139">Your app is now able to store a set of categories in local storage on the device and register with the notification hub whenever the user changes the selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="472f1-140">Register for notifications</span><span class="sxs-lookup"><span data-stu-id="472f1-140">Register for notifications</span></span>
<span data-ttu-id="472f1-141">These steps register with the notification hub on startup using the categories that have been stored in local storage.</span><span class="sxs-lookup"><span data-stu-id="472f1-141">These steps register with the notification hub on startup using the categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="472f1-142">Because the channel URI assigned by the Windows Notification Service (WNS) can change at any time, you should register for notifications frequently to avoid notification failures.</span><span class="sxs-lookup"><span data-stu-id="472f1-142">Because the channel URI assigned by the Windows Notification Service (WNS) can change at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="472f1-143">This example registers for notification every time that the app starts.</span><span class="sxs-lookup"><span data-stu-id="472f1-143">This example registers for notification every time that the app starts.</span></span> <span data-ttu-id="472f1-144">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span><span class="sxs-lookup"><span data-stu-id="472f1-144">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
> 
> 

1. <span data-ttu-id="472f1-145">Open the App.xaml.cs file and update the **InitNotificationsAsync** method to use the `notifications` class to subscribe based on categories.</span><span class="sxs-lookup"><span data-stu-id="472f1-145">Open the App.xaml.cs file and update the **InitNotificationsAsync** method to use the `notifications` class to subscribe based on categories.</span></span>
   
        // *** Remove or comment out these lines *** 
        //var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
        //var hub = new NotificationHub("your hub name", "your listen connection string");
        //var result = await hub.RegisterNativeAsync(channel.Uri);
   
        var result = await notifications.SubscribeToCategories();
   
    <span data-ttu-id="472f1-146">This makes sure that every time the app starts it retrieves the categories from local storage and requests a registeration for these categories.</span><span class="sxs-lookup"><span data-stu-id="472f1-146">This makes sure that every time the app starts it retrieves the categories from local storage and requests a registeration for these categories.</span></span> <span data-ttu-id="472f1-147">The **InitNotificationsAsync** method was created as part of the [Get started with Notification Hubs][get-started] tutorial.</span><span class="sxs-lookup"><span data-stu-id="472f1-147">The **InitNotificationsAsync** method was created as part of the [Get started with Notification Hubs][get-started] tutorial.</span></span>
2. <span data-ttu-id="472f1-148">In the MainPage.xaml.cs project file, add the following code to the *OnNavigatedTo* method:</span><span class="sxs-lookup"><span data-stu-id="472f1-148">In the MainPage.xaml.cs project file, add the following code to the *OnNavigatedTo* method:</span></span>
   
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
   
    <span data-ttu-id="472f1-149">This updates the main page based on the status of previously saved categories.</span><span class="sxs-lookup"><span data-stu-id="472f1-149">This updates the main page based on the status of previously saved categories.</span></span>

<span data-ttu-id="472f1-150">The app is now complete and can store a set of categories in the device local storage used to register with the notification hub whenever the user changes the selection of categories.</span><span class="sxs-lookup"><span data-stu-id="472f1-150">The app is now complete and can store a set of categories in the device local storage used to register with the notification hub whenever the user changes the selection of categories.</span></span> <span data-ttu-id="472f1-151">Next, we will define a backend that can send category notifications to this app.</span><span class="sxs-lookup"><span data-stu-id="472f1-151">Next, we will define a backend that can send category notifications to this app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="472f1-152">Sending tagged notifications</span><span class="sxs-lookup"><span data-stu-id="472f1-152">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="472f1-153">Run the app and generate notifications</span><span class="sxs-lookup"><span data-stu-id="472f1-153">Run the app and generate notifications</span></span>
1. <span data-ttu-id="472f1-154">In Visual Studio, press F5 to compile and start the app.</span><span class="sxs-lookup"><span data-stu-id="472f1-154">In Visual Studio, press F5 to compile and start the app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="472f1-155">Note that the app UI provides a set of toggles that lets you choose the categories to subscribe to.</span><span class="sxs-lookup"><span data-stu-id="472f1-155">Note that the app UI provides a set of toggles that lets you choose the categories to subscribe to.</span></span>
2. <span data-ttu-id="472f1-156">Enable one or more categories toggles, then click **Subscribe**.</span><span class="sxs-lookup"><span data-stu-id="472f1-156">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="472f1-157">The app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span><span class="sxs-lookup"><span data-stu-id="472f1-157">The app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span> <span data-ttu-id="472f1-158">The registered categories are returned and displayed in a dialog.</span><span class="sxs-lookup"><span data-stu-id="472f1-158">The registered categories are returned and displayed in a dialog.</span></span>
   
    ![][19]
3. <span data-ttu-id="472f1-159">Send a new notification from the backend in one of the following ways:</span><span class="sxs-lookup"><span data-stu-id="472f1-159">Send a new notification from the backend in one of the following ways:</span></span>
   
   * <span data-ttu-id="472f1-160">**Console app:** start the console app.</span><span class="sxs-lookup"><span data-stu-id="472f1-160">**Console app:** start the console app.</span></span>
   * <span data-ttu-id="472f1-161">**Java/PHP:** run your app/script.</span><span class="sxs-lookup"><span data-stu-id="472f1-161">**Java/PHP:** run your app/script.</span></span>
     
     <span data-ttu-id="472f1-162">Notifications for the selected categories appear as toast notifications.</span><span class="sxs-lookup"><span data-stu-id="472f1-162">Notifications for the selected categories appear as toast notifications.</span></span>
     
     ![][14]

## <a name="next-steps"></a><span data-ttu-id="472f1-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="472f1-163">Next steps</span></span>
<span data-ttu-id="472f1-164">In this tutorial we learned how to broadcast breaking news by category.</span><span class="sxs-lookup"><span data-stu-id="472f1-164">In this tutorial we learned how to broadcast breaking news by category.</span></span> <span data-ttu-id="472f1-165">Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:</span><span class="sxs-lookup"><span data-stu-id="472f1-165">Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="472f1-166">[Use Notification Hubs to broadcast localized breaking news]</span><span class="sxs-lookup"><span data-stu-id="472f1-166">[Use Notification Hubs to broadcast localized breaking news]</span></span>
  
    <span data-ttu-id="472f1-167">Learn how to expand the breaking news app to enable sending localized notifications.</span><span class="sxs-lookup"><span data-stu-id="472f1-167">Learn how to expand the breaking news app to enable sending localized notifications.</span></span>

<!-- Anchors. -->
[Add category selection to the app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run the app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-breakingnews-win1.png

[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-toast-2.png


[19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-reg-2.png

<!-- URLs.-->
[get-started]: /manage/services/notification-hubs/getting-started-windows-dotnet/
[Use Notification Hubs to broadcast localized breaking news]: /manage/services/notification-hubs/breaking-news-localized-dotnet/
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591



