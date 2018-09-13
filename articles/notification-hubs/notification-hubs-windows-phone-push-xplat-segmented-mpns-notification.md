---
title: Push notifications to specific Windows phones using Azure Notification Hubs | Microsoft Docs
description: In this tutorial, you learn how to use Azure Notification Hubs to push notifications to specific (not all) Windows Phone 8 or Windows Phone 8.1 devices registered with the application backend.
services: notification-hubs
documentationcenter: windows
author: dimazaid
manager: kpiteira
editor: spelluru
ms.assetid: 42726bf5-cc82-438d-9eaa-238da3322d80
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: tutorial
ms.custom: mvc
ms.date: 04/14/2018
ms.author: dimazaid
ms.openlocfilehash: fb408765a1185ac64a664cee458432bfce061c91
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44821007"
---
# <a name="tutorial-push-notifications-to-specific-windows-phone-devices-by-using-azure-notification-hubs"></a><span data-ttu-id="712bf-103">Tutorial: Push notifications to specific Windows Phone devices by using Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="712bf-103">Tutorial: Push notifications to specific Windows Phone devices by using Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

<span data-ttu-id="712bf-104">This tutorial shows you how to use Azure Notification Hubs to send push notifications to specific Windows Phone 8 or Windows Phone 8.1 devices.</span><span class="sxs-lookup"><span data-stu-id="712bf-104">This tutorial shows you how to use Azure Notification Hubs to send push notifications to specific Windows Phone 8 or Windows Phone 8.1 devices.</span></span> <span data-ttu-id="712bf-105">If you are targeting Windows Phone 8.1 (non-Silverlight), see the [Windows Universal](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) version of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="712bf-105">If you are targeting Windows Phone 8.1 (non-Silverlight), see the [Windows Universal](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) version of this tutorial.</span></span>

<span data-ttu-id="712bf-106">You enable this scenario by including one or more *tags* when creating a registration in the notification hub.</span><span class="sxs-lookup"><span data-stu-id="712bf-106">You enable this scenario by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="712bf-107">When notifications are sent to a tag, all devices that have registered for the tag receive the notification.</span><span class="sxs-lookup"><span data-stu-id="712bf-107">When notifications are sent to a tag, all devices that have registered for the tag receive the notification.</span></span> <span data-ttu-id="712bf-108">For more information about tags, see [Tags in registrations](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="712bf-108">For more information about tags, see [Tags in registrations](notification-hubs-tags-segment-push-message.md).</span></span>

> [!NOTE]
> <span data-ttu-id="712bf-109">The Notification Hubs Windows Phone SDK does not support using the Windows Push Notification Service (WNS) with Windows Phone 8.1 Silverlight apps.</span><span class="sxs-lookup"><span data-stu-id="712bf-109">The Notification Hubs Windows Phone SDK does not support using the Windows Push Notification Service (WNS) with Windows Phone 8.1 Silverlight apps.</span></span> <span data-ttu-id="712bf-110">To use WNS (instead of MPNS) with Windows Phone 8.1 Silverlight apps, follow the [Notification Hubs - Windows Phone Silverlight tutorial], which uses REST APIs.</span><span class="sxs-lookup"><span data-stu-id="712bf-110">To use WNS (instead of MPNS) with Windows Phone 8.1 Silverlight apps, follow the [Notification Hubs - Windows Phone Silverlight tutorial], which uses REST APIs.</span></span>

<span data-ttu-id="712bf-111">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="712bf-111">In this tutorial, you learn how to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="712bf-112">Add category selection to the mobile app</span><span class="sxs-lookup"><span data-stu-id="712bf-112">Add category selection to the mobile app</span></span>
> * <span data-ttu-id="712bf-113">Register for notifications with tags</span><span class="sxs-lookup"><span data-stu-id="712bf-113">Register for notifications with tags</span></span>
> * <span data-ttu-id="712bf-114">Send tagged notifications</span><span class="sxs-lookup"><span data-stu-id="712bf-114">Send tagged notifications</span></span>
> * <span data-ttu-id="712bf-115">Test the app</span><span class="sxs-lookup"><span data-stu-id="712bf-115">Test the app</span></span>

## <a name="prerequisites"></a><span data-ttu-id="712bf-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="712bf-116">Prerequisites</span></span>
<span data-ttu-id="712bf-117">Complete the [Tutorial: Push notifications to Windows Phone apps by using Azure Notification Hubs](notification-hubs-windows-mobile-push-notifications-mpns.md).</span><span class="sxs-lookup"><span data-stu-id="712bf-117">Complete the [Tutorial: Push notifications to Windows Phone apps by using Azure Notification Hubs](notification-hubs-windows-mobile-push-notifications-mpns.md).</span></span> <span data-ttu-id="712bf-118">In this tutorial, you update the mobile application so that you can register for breaking news categories you are interested in, and receive only push notifications for those categories.</span><span class="sxs-lookup"><span data-stu-id="712bf-118">In this tutorial, you update the mobile application so that you can register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> 

## <a name="add-category-selection-to-the-mobile-app"></a><span data-ttu-id="712bf-119">Add category selection to the mobile app</span><span class="sxs-lookup"><span data-stu-id="712bf-119">Add category selection to the mobile app</span></span>
<span data-ttu-id="712bf-120">The first step is to add the UI elements to your existing main page that enable the user to select categories to register.</span><span class="sxs-lookup"><span data-stu-id="712bf-120">The first step is to add the UI elements to your existing main page that enable the user to select categories to register.</span></span> <span data-ttu-id="712bf-121">The categories selected by a user are stored on the device.</span><span class="sxs-lookup"><span data-stu-id="712bf-121">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="712bf-122">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span><span class="sxs-lookup"><span data-stu-id="712bf-122">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="712bf-123">Open the MainPage.xaml project file, then replace the **Grid** elements named `TitlePanel` and `ContentPanel` with the following code:</span><span class="sxs-lookup"><span data-stu-id="712bf-123">Open the MainPage.xaml project file, then replace the **Grid** elements named `TitlePanel` and `ContentPanel` with the following code:</span></span>
   
        <StackPanel x:Name="TitlePanel" Grid.Row="0" Margin="12,17,0,28">
            <TextBlock Text="Breaking News" Style="{StaticResource PhoneTextNormalStyle}" Margin="12,0"/>
            <TextBlock Text="Categories" Margin="9,-7,0,0" Style="{StaticResource PhoneTextTitle1Style}"/>
        </StackPanel>
   
        <Grid Name="ContentPanel" Grid.Row="1" Margin="12,0,12,0">
            <Grid.RowDefinitions>
                <RowDefinition Height="auto"/>
                <RowDefinition Height="auto" />
                <RowDefinition Height="auto" />
                <RowDefinition Height="auto" />
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition />
                <ColumnDefinition />
            </Grid.ColumnDefinitions>
            <CheckBox Name="WorldCheckBox" Grid.Row="0" Grid.Column="0">World</CheckBox>
            <CheckBox Name="PoliticsCheckBox" Grid.Row="1" Grid.Column="0">Politics</CheckBox>
            <CheckBox Name="BusinessCheckBox" Grid.Row="2" Grid.Column="0">Business</CheckBox>
            <CheckBox Name="TechnologyCheckBox" Grid.Row="0" Grid.Column="1">Technology</CheckBox>
            <CheckBox Name="ScienceCheckBox" Grid.Row="1" Grid.Column="1">Science</CheckBox>
            <CheckBox Name="SportsCheckBox" Grid.Row="2" Grid.Column="1">Sports</CheckBox>
            <Button Name="SubscribeButton" Content="Subscribe" HorizontalAlignment="Center" Grid.Row="3" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click" />
        </Grid>
2. <span data-ttu-id="712bf-124">Add a class named **Notifications** to the project.</span><span class="sxs-lookup"><span data-stu-id="712bf-124">Add a class named **Notifications** to the project.</span></span> <span data-ttu-id="712bf-125">Add the **public** modifier to the class definition.</span><span class="sxs-lookup"><span data-stu-id="712bf-125">Add the **public** modifier to the class definition.</span></span> <span data-ttu-id="712bf-126">Then, add the following **using** statements to the new code file:</span><span class="sxs-lookup"><span data-stu-id="712bf-126">Then, add the following **using** statements to the new code file:</span></span>
   
    ```csharp
    using Microsoft.Phone.Notification;
    using Microsoft.WindowsAzure.Messaging;
    using System.IO.IsolatedStorage;
    using System.Windows;
    ```
1. <span data-ttu-id="712bf-127">Copy the following code into the new **Notifications** class:</span><span class="sxs-lookup"><span data-stu-id="712bf-127">Copy the following code into the new **Notifications** class:</span></span>
   
    ```csharp
    private NotificationHub hub;

    // Registration task to complete registration in the ChannelUriUpdated event handler
    private TaskCompletionSource<Registration> registrationTask;

    public Notifications(string hubName, string listenConnectionString)
    {
        hub = new NotificationHub(hubName, listenConnectionString);
    }

    public IEnumerable<string> RetrieveCategories()
    {
        var categories = (string)IsolatedStorageSettings.ApplicationSettings["categories"];
        return categories != null ? categories.Split(',') : new string[0];
    }

    public async Task<Registration> StoreCategoriesAndSubscribe(IEnumerable<string> categories)
    {
        var categoriesAsString = string.Join(",", categories);
        var settings = IsolatedStorageSettings.ApplicationSettings;
        if (!settings.Contains("categories"))
        {
            settings.Add("categories", categoriesAsString);
        }
        else
        {
            settings["categories"] = categoriesAsString;
        }
        settings.Save();

        return await SubscribeToCategories();
    }

    public async Task<Registration> SubscribeToCategories()
    {
        registrationTask = new TaskCompletionSource<Registration>();

        var channel = HttpNotificationChannel.Find("MyPushChannel");

        if (channel == null)
        {
            channel = new HttpNotificationChannel("MyPushChannel");
            channel.Open();
            channel.BindToShellToast();
            channel.ChannelUriUpdated += channel_ChannelUriUpdated;

            // This is optional, used to receive notifications while the app is running.
            channel.ShellToastNotificationReceived += channel_ShellToastNotificationReceived;
        }

        // If channel.ChannelUri is not null, complete the registrationTask here.  
        // If it is null, the registrationTask will be completed in the ChannelUriUpdated event handler.
        if (channel.ChannelUri != null)
        {
            await RegisterTemplate(channel.ChannelUri);
        }

        return await registrationTask.Task;
    }

    async void channel_ChannelUriUpdated(object sender, NotificationChannelUriEventArgs e)
    {
        await RegisterTemplate(e.ChannelUri);
    }

    async Task<Registration> RegisterTemplate(Uri channelUri)
    {
        // Using a template registration to support notifications across platforms.
        // Any template notifications that contain messageParam and a corresponding tag expression
        // will be delivered for this registration.

        const string templateBodyMPNS = "<wp:Notification xmlns:wp=\"WPNotification\">" +
                                            "<wp:Toast>" +
                                                "<wp:Text1>$(messageParam)</wp:Text1>" +
                                            "</wp:Toast>" +
                                        "</wp:Notification>";

        // The stored categories tags are passed with the template registration.

        registrationTask.SetResult(await hub.RegisterTemplateAsync(channelUri.ToString(), 
            templateBodyMPNS, "simpleMPNSTemplateExample", this.RetrieveCategories()));

        return await registrationTask.Task;
    }

    // This is optional. It is used to receive notifications while the app is running.
    void channel_ShellToastNotificationReceived(object sender, NotificationEventArgs e)
    {
        StringBuilder message = new StringBuilder();
        string relativeUri = string.Empty;

        message.AppendFormat("Received Toast {0}:\n", DateTime.Now.ToShortTimeString());

        // Parse out the information that was part of the message.
        foreach (string key in e.Collection.Keys)
        {
            message.AppendFormat("{0}: {1}\n", key, e.Collection[key]);

            if (string.Compare(
                key,
                "wp:Param",
                System.Globalization.CultureInfo.InvariantCulture,
                System.Globalization.CompareOptions.IgnoreCase) == 0)
            {
                relativeUri = e.Collection[key];
            }
        }

        // Display a dialog of all the fields in the toast.
        System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() => 
        { 
            MessageBox.Show(message.ToString()); 
        });
    }
    ```
    
    <span data-ttu-id="712bf-128">This class uses the isolated storage to store the categories of news that this device is to receive.</span><span class="sxs-lookup"><span data-stu-id="712bf-128">This class uses the isolated storage to store the categories of news that this device is to receive.</span></span> <span data-ttu-id="712bf-129">It also contains methods to register for these categories using a [template](notification-hubs-templates-cross-platform-push-messages.md) notification registration.</span><span class="sxs-lookup"><span data-stu-id="712bf-129">It also contains methods to register for these categories using a [template](notification-hubs-templates-cross-platform-push-messages.md) notification registration.</span></span>
1. <span data-ttu-id="712bf-130">In the App.xaml.cs project file, add the following property to the **App** class.</span><span class="sxs-lookup"><span data-stu-id="712bf-130">In the App.xaml.cs project file, add the following property to the **App** class.</span></span> <span data-ttu-id="712bf-131">Replace the `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span><span class="sxs-lookup"><span data-stu-id="712bf-131">Replace the `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
    ```csharp
    public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
    ```

   > [!NOTE]
   > <span data-ttu-id="712bf-132">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span><span class="sxs-lookup"><span data-stu-id="712bf-132">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="712bf-133">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span><span class="sxs-lookup"><span data-stu-id="712bf-133">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="712bf-134">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span><span class="sxs-lookup"><span data-stu-id="712bf-134">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
2. <span data-ttu-id="712bf-135">In your MainPage.xaml.cs, add the following line:</span><span class="sxs-lookup"><span data-stu-id="712bf-135">In your MainPage.xaml.cs, add the following line:</span></span>
   
    ```csharp
    using Windows.UI.Popups;
    ```
1. <span data-ttu-id="712bf-136">In the MainPage.xaml.cs project file, add the following method:</span><span class="sxs-lookup"><span data-stu-id="712bf-136">In the MainPage.xaml.cs project file, add the following method:</span></span>
   
    ```csharp
    private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
    {
        var categories = new HashSet<string>();
        if (WorldCheckBox.IsChecked == true) categories.Add("World");
        if (PoliticsCheckBox.IsChecked == true) categories.Add("Politics");
        if (BusinessCheckBox.IsChecked == true) categories.Add("Business");
        if (TechnologyCheckBox.IsChecked == true) categories.Add("Technology");
        if (ScienceCheckBox.IsChecked == true) categories.Add("Science");
        if (SportsCheckBox.IsChecked == true) categories.Add("Sports");

        var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(categories);

        MessageBox.Show("Subscribed to: " + string.Join(",", categories) + " on registration id : " +
            result.RegistrationId);
    }
    ```
   
    <span data-ttu-id="712bf-137">This method creates a list of categories and uses the **Notifications** class to store the list in the local storage and register the corresponding tags with your notification hub.</span><span class="sxs-lookup"><span data-stu-id="712bf-137">This method creates a list of categories and uses the **Notifications** class to store the list in the local storage and register the corresponding tags with your notification hub.</span></span> <span data-ttu-id="712bf-138">When categories are changed, the registration is recreated with the new categories.</span><span class="sxs-lookup"><span data-stu-id="712bf-138">When categories are changed, the registration is recreated with the new categories.</span></span>

<span data-ttu-id="712bf-139">Your app is now able to store a set of categories in local storage on the device and register with the notification hub whenever the user changes the selection of categories.</span><span class="sxs-lookup"><span data-stu-id="712bf-139">Your app is now able to store a set of categories in local storage on the device and register with the notification hub whenever the user changes the selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="712bf-140">Register for notifications</span><span class="sxs-lookup"><span data-stu-id="712bf-140">Register for notifications</span></span>
<span data-ttu-id="712bf-141">These steps register with the notification hub on startup using the categories that have been stored in local storage.</span><span class="sxs-lookup"><span data-stu-id="712bf-141">These steps register with the notification hub on startup using the categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="712bf-142">Because the channel URI assigned by the Microsoft Push Notification Service (MPNS) can change at any time, you should register for notifications frequently to avoid notification failures.</span><span class="sxs-lookup"><span data-stu-id="712bf-142">Because the channel URI assigned by the Microsoft Push Notification Service (MPNS) can change at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="712bf-143">This example registers for notifications every time that the app starts.</span><span class="sxs-lookup"><span data-stu-id="712bf-143">This example registers for notifications every time that the app starts.</span></span> <span data-ttu-id="712bf-144">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span><span class="sxs-lookup"><span data-stu-id="712bf-144">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>

1. <span data-ttu-id="712bf-145">Open the App.xaml.cs file and add the **async** modifier to **Application_Launching** method and replace the Notification Hubs registration code that you added in [Get started with Notification Hubs] with the following code:</span><span class="sxs-lookup"><span data-stu-id="712bf-145">Open the App.xaml.cs file and add the **async** modifier to **Application_Launching** method and replace the Notification Hubs registration code that you added in [Get started with Notification Hubs] with the following code:</span></span>
   
    ```csharp
    private async void Application_Launching(object sender, LaunchingEventArgs e)
    {
        var result = await notifications.SubscribeToCategories();
    
        if (result != null)
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
            {
                MessageBox.Show("Registration Id :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
            });
    }
    ```
   
    <span data-ttu-id="712bf-146">This code makes sure that every time the app starts it retrieves the categories from local storage and requests a registration for these categories.</span><span class="sxs-lookup"><span data-stu-id="712bf-146">This code makes sure that every time the app starts it retrieves the categories from local storage and requests a registration for these categories.</span></span>
2. <span data-ttu-id="712bf-147">In the MainPage.xaml.cs project file, add the following code that implements the **OnNavigatedTo** method:</span><span class="sxs-lookup"><span data-stu-id="712bf-147">In the MainPage.xaml.cs project file, add the following code that implements the **OnNavigatedTo** method:</span></span>
   
    ```csharp
    protected override void OnNavigatedTo(NavigationEventArgs e)
    {
        var categories = ((App)Application.Current).notifications.RetrieveCategories();
    
        if (categories.Contains("World")) WorldCheckBox.IsChecked = true;
        if (categories.Contains("Politics")) PoliticsCheckBox.IsChecked = true;
        if (categories.Contains("Business")) BusinessCheckBox.IsChecked = true;
        if (categories.Contains("Technology")) TechnologyCheckBox.IsChecked = true;
        if (categories.Contains("Science")) ScienceCheckBox.IsChecked = true;
        if (categories.Contains("Sports")) SportsCheckBox.IsChecked = true;
    }
    ```
   
    <span data-ttu-id="712bf-148">This code updates the main page based on the status of previously saved categories.</span><span class="sxs-lookup"><span data-stu-id="712bf-148">This code updates the main page based on the status of previously saved categories.</span></span>

<span data-ttu-id="712bf-149">The app is now complete and can store a set of categories in the device local storage used to register with the notification hub whenever the user changes the selection of categories.</span><span class="sxs-lookup"><span data-stu-id="712bf-149">The app is now complete and can store a set of categories in the device local storage used to register with the notification hub whenever the user changes the selection of categories.</span></span> <span data-ttu-id="712bf-150">Next, define a backend that can send category notifications to this app.</span><span class="sxs-lookup"><span data-stu-id="712bf-150">Next, define a backend that can send category notifications to this app.</span></span>

## <a name="send-tagged-notifications"></a><span data-ttu-id="712bf-151">Send tagged notifications</span><span class="sxs-lookup"><span data-stu-id="712bf-151">Send tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="test-the-app"></a><span data-ttu-id="712bf-152">Test the app</span><span class="sxs-lookup"><span data-stu-id="712bf-152">Test the app</span></span>
1. <span data-ttu-id="712bf-153">In Visual Studio, press F5 to compile and start the app.</span><span class="sxs-lookup"><span data-stu-id="712bf-153">In Visual Studio, press F5 to compile and start the app.</span></span>
   
    ![Mobile app with categories][1]
   
    <span data-ttu-id="712bf-155">The app UI provides a set of toggles that lets you choose the categories to subscribe to.</span><span class="sxs-lookup"><span data-stu-id="712bf-155">The app UI provides a set of toggles that lets you choose the categories to subscribe to.</span></span>
2. <span data-ttu-id="712bf-156">Enable one or more categories toggles, then click **Subscribe**.</span><span class="sxs-lookup"><span data-stu-id="712bf-156">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="712bf-157">The app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span><span class="sxs-lookup"><span data-stu-id="712bf-157">The app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span> <span data-ttu-id="712bf-158">The registered categories are returned and displayed in a dialog.</span><span class="sxs-lookup"><span data-stu-id="712bf-158">The registered categories are returned and displayed in a dialog.</span></span>
   
    ![Subscribed message][2]
3. <span data-ttu-id="712bf-160">After receiving a confirmation that your categories were subscription completed, run the console app to send notifications for each category.</span><span class="sxs-lookup"><span data-stu-id="712bf-160">After receiving a confirmation that your categories were subscription completed, run the console app to send notifications for each category.</span></span> <span data-ttu-id="712bf-161">Verify you only receive a notification for the categories you have subscribed to.</span><span class="sxs-lookup"><span data-stu-id="712bf-161">Verify you only receive a notification for the categories you have subscribed to.</span></span>
   
    ![Notification message][3]

## <a name="next-steps"></a><span data-ttu-id="712bf-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="712bf-163">Next steps</span></span>
<span data-ttu-id="712bf-164">In this tutorial, you learned how to push notifications to specific devices that have tags associated with their registrations.</span><span class="sxs-lookup"><span data-stu-id="712bf-164">In this tutorial, you learned how to push notifications to specific devices that have tags associated with their registrations.</span></span> <span data-ttu-id="712bf-165">To learn how to push notifications to specific users who may be using multiple devices, advance to the following tutorial:</span><span class="sxs-lookup"><span data-stu-id="712bf-165">To learn how to push notifications to specific users who may be using multiple devices, advance to the following tutorial:</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="712bf-166">Push notifications to specific users</span><span class="sxs-lookup"><span data-stu-id="712bf-166">Push notifications to specific users</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md)


<!-- Anchors. -->
[Add category selection to the app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run the app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-breakingnews.png
[2]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-registration.png
[3]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-toast.png



<!-- URLs.-->
[Get started with Notification Hubs]: notification-hubs-windows-mobile-push-notifications-mpns.md
[Use Notification Hubs to broadcast localized breaking news]: notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md
[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Windows Phone]: ??

