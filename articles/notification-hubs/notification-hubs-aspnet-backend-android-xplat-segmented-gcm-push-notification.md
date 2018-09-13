---
title: Notification Hubs Breaking News Tutorial - Android
description: Learn how to use Azure Service Bus Notification Hubs to send breaking news notifications to Android devices.
services: notification-hubs
documentationcenter: android
author: ysxu
manager: erikre
editor: ''
ms.assetid: 3c23cb80-9d35-4dde-b26d-a7bfd4cb8f81
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 86e55ea4c0f1e41cf77475578a49032a7b9c521e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548774"
---
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="53f74-103">Use Notification Hubs to send breaking news</span><span class="sxs-lookup"><span data-stu-id="53f74-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="53f74-104">Overview</span><span class="sxs-lookup"><span data-stu-id="53f74-104">Overview</span></span>
<span data-ttu-id="53f74-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to an Android app.</span><span class="sxs-lookup"><span data-stu-id="53f74-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to an Android app.</span></span> <span data-ttu-id="53f74-106">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span><span class="sxs-lookup"><span data-stu-id="53f74-106">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="53f74-107">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span><span class="sxs-lookup"><span data-stu-id="53f74-107">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="53f74-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span><span class="sxs-lookup"><span data-stu-id="53f74-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="53f74-109">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span><span class="sxs-lookup"><span data-stu-id="53f74-109">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="53f74-110">Because tags are simply strings, they do not have to be provisioned in advance.</span><span class="sxs-lookup"><span data-stu-id="53f74-110">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="53f74-111">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="53f74-111">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="53f74-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="53f74-112">Prerequisites</span></span>
<span data-ttu-id="53f74-113">This topic builds on the app you created in [Get started with Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="53f74-113">This topic builds on the app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="53f74-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="53f74-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="53f74-115">Add category selection to the app</span><span class="sxs-lookup"><span data-stu-id="53f74-115">Add category selection to the app</span></span>
<span data-ttu-id="53f74-116">The first step is to add the UI elements to your existing main activity that enable the user to select categories to register.</span><span class="sxs-lookup"><span data-stu-id="53f74-116">The first step is to add the UI elements to your existing main activity that enable the user to select categories to register.</span></span> <span data-ttu-id="53f74-117">The categories selected by a user are stored on the device.</span><span class="sxs-lookup"><span data-stu-id="53f74-117">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="53f74-118">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span><span class="sxs-lookup"><span data-stu-id="53f74-118">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="53f74-119">Open your res/layout/activity_main.xml file, and substitute the content with the following:</span><span class="sxs-lookup"><span data-stu-id="53f74-119">Open your res/layout/activity_main.xml file, and substitute the content with the following:</span></span>
   
        <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
            xmlns:tools="http://schemas.android.com/tools"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:paddingBottom="@dimen/activity_vertical_margin"
            android:paddingLeft="@dimen/activity_horizontal_margin"
            android:paddingRight="@dimen/activity_horizontal_margin"
            android:paddingTop="@dimen/activity_vertical_margin"
            tools:context="com.example.breakingnews.MainActivity"
            android:orientation="vertical">
   
                <CheckBox
                    android:id="@+id/worldBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_world" />
                <CheckBox
                    android:id="@+id/politicsBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_politics" />
                <CheckBox
                    android:id="@+id/businessBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_business" />
                <CheckBox
                    android:id="@+id/technologyBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_technology" />
                <CheckBox
                    android:id="@+id/scienceBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_science" />
                <CheckBox
                    android:id="@+id/sportsBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_sports" />
                <Button
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:onClick="subscribe"
                    android:text="@string/button_subscribe" />
        </LinearLayout>
2. <span data-ttu-id="53f74-120">Open your res/values/strings.xml file and add the following lines:</span><span class="sxs-lookup"><span data-stu-id="53f74-120">Open your res/values/strings.xml file and add the following lines:</span></span>
   
        <string name="button_subscribe">Subscribe</string>
        <string name="label_world">World</string>
        <string name="label_politics">Politics</string>
        <string name="label_business">Business</string>
        <string name="label_technology">Technology</string>
        <string name="label_science">Science</string>
        <string name="label_sports">Sports</string>
   
    <span data-ttu-id="53f74-121">Your main_activity.xml graphical layout should now look like this:</span><span class="sxs-lookup"><span data-stu-id="53f74-121">Your main_activity.xml graphical layout should now look like this:</span></span>
   
    ![][A1]
3. <span data-ttu-id="53f74-122">Now create a class **Notifications** in the same package as your **MainActivity** class.</span><span class="sxs-lookup"><span data-stu-id="53f74-122">Now create a class **Notifications** in the same package as your **MainActivity** class.</span></span>
   
        import java.util.HashSet;
        import java.util.Set;
   
        import android.content.Context;
        import android.content.SharedPreferences;
        import android.os.AsyncTask;
        import android.util.Log;
        import android.widget.Toast;
   
        import com.google.android.gms.gcm.GoogleCloudMessaging;
        import com.microsoft.windowsazure.messaging.NotificationHub;
   
        public class Notifications {
            private static final String PREFS_NAME = "BreakingNewsCategories";
            private GoogleCloudMessaging gcm;
            private NotificationHub hub;
            private Context context;
            private String senderId;
   
            public Notifications(Context context, String senderId, String hubName, 
                                    String listenConnectionString) {
                this.context = context;
                this.senderId = senderId;
   
                gcm = GoogleCloudMessaging.getInstance(context);
                hub = new NotificationHub(hubName, listenConnectionString, context);
            }
   
            public void storeCategoriesAndSubscribe(Set<String> categories)
            {
                SharedPreferences settings = context.getSharedPreferences(PREFS_NAME, 0);
                settings.edit().putStringSet("categories", categories).commit();
                subscribeToCategories(categories);
            }
   
            public Set<String> retrieveCategories() {
                SharedPreferences settings = context.getSharedPreferences(PREFS_NAME, 0);
                return settings.getStringSet("categories", new HashSet<String>());
            }
   
            public void subscribeToCategories(final Set<String> categories) {
                new AsyncTask<Object, Object, Object>() {
                    @Override
                    protected Object doInBackground(Object... params) {
                        try {
                            String regid = gcm.register(senderId);
   
                            String templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";
   
                            hub.registerTemplate(regid,"simpleGCMTemplate", templateBodyGCM, 
                                categories.toArray(new String[categories.size()]));
                        } catch (Exception e) {
                            Log.e("MainActivity", "Failed to register - " + e.getMessage());
                            return e;
                        }
                        return null;
                    }
   
                    protected void onPostExecute(Object result) {
                        String message = "Subscribed for categories: "
                                + categories.toString();
                        Toast.makeText(context, message,
                                Toast.LENGTH_LONG).show();
                    }
                }.execute(null, null, null);
            }
   
        }
   
    <span data-ttu-id="53f74-123">This class uses the local storage to store the categories of news that this device has to receive.</span><span class="sxs-lookup"><span data-stu-id="53f74-123">This class uses the local storage to store the categories of news that this device has to receive.</span></span> <span data-ttu-id="53f74-124">It also contains methods to register for these categories.</span><span class="sxs-lookup"><span data-stu-id="53f74-124">It also contains methods to register for these categories.</span></span>
4. <span data-ttu-id="53f74-125">In your **MainActivity** class remove your private fields for **NotificationHub** and **GoogleCloudMessaging**, and add a field for **Notifications**:</span><span class="sxs-lookup"><span data-stu-id="53f74-125">In your **MainActivity** class remove your private fields for **NotificationHub** and **GoogleCloudMessaging**, and add a field for **Notifications**:</span></span>
   
        // private GoogleCloudMessaging gcm;
        // private NotificationHub hub;
        private Notifications notifications;
5. <span data-ttu-id="53f74-126">Then, in the **onCreate** method, remove the initialization of the **hub** field and the **registerWithNotificationHubs** method.</span><span class="sxs-lookup"><span data-stu-id="53f74-126">Then, in the **onCreate** method, remove the initialization of the **hub** field and the **registerWithNotificationHubs** method.</span></span> <span data-ttu-id="53f74-127">Then add the following lines which initialize an instance of the **Notifications** class.</span><span class="sxs-lookup"><span data-stu-id="53f74-127">Then add the following lines which initialize an instance of the **Notifications** class.</span></span> 

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            MyHandler.mainActivity = this;

            NotificationsManager.handleNotifications(this, SENDER_ID,
                    MyHandler.class);

            notifications = new Notifications(this, SENDER_ID, HubName, HubListenConnectionString);

            notifications.subscribeToCategories(notifications.retrieveCategories());
        }

    <span data-ttu-id="53f74-128">`HubName` and `HubListenConnectionString` should already be set with the `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span><span class="sxs-lookup"><span data-stu-id="53f74-128">`HubName` and `HubListenConnectionString` should already be set with the `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>

    > [AZURE.NOTE] <span data-ttu-id="53f74-129">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span><span class="sxs-lookup"><span data-stu-id="53f74-129">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="53f74-130">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span><span class="sxs-lookup"><span data-stu-id="53f74-130">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="53f74-131">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span><span class="sxs-lookup"><span data-stu-id="53f74-131">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>


1. <span data-ttu-id="53f74-132">Then, add the following imports and `subscribe` method to handle the subscribe button click event:</span><span class="sxs-lookup"><span data-stu-id="53f74-132">Then, add the following imports and `subscribe` method to handle the subscribe button click event:</span></span>
   
        import android.widget.CheckBox;
        import java.util.HashSet;
        import java.util.Set;
   
        public void subscribe(View sender) {
            final Set<String> categories = new HashSet<String>();
   
            CheckBox world = (CheckBox) findViewById(R.id.worldBox);
            if (world.isChecked())
                categories.add("world");
            CheckBox politics = (CheckBox) findViewById(R.id.politicsBox);
            if (politics.isChecked())
                categories.add("politics");
            CheckBox business = (CheckBox) findViewById(R.id.businessBox);
            if (business.isChecked())
                categories.add("business");
            CheckBox technology = (CheckBox) findViewById(R.id.technologyBox);
            if (technology.isChecked())
                categories.add("technology");
            CheckBox science = (CheckBox) findViewById(R.id.scienceBox);
            if (science.isChecked())
                categories.add("science");
            CheckBox sports = (CheckBox) findViewById(R.id.sportsBox);
            if (sports.isChecked())
                categories.add("sports");
   
            notifications.storeCategoriesAndSubscribe(categories);
        }
   
    <span data-ttu-id="53f74-133">This method creates a list of categories and uses the **Notifications** class to store the list in the local storage and register the corresponding tags with your notification hub.</span><span class="sxs-lookup"><span data-stu-id="53f74-133">This method creates a list of categories and uses the **Notifications** class to store the list in the local storage and register the corresponding tags with your notification hub.</span></span> <span data-ttu-id="53f74-134">When categories are changed, the registration is recreated with the new categories.</span><span class="sxs-lookup"><span data-stu-id="53f74-134">When categories are changed, the registration is recreated with the new categories.</span></span>

<span data-ttu-id="53f74-135">Your app is now able to store a set of categories in local storage on the device and register with the notification hub whenever the user changes the selection of categories.</span><span class="sxs-lookup"><span data-stu-id="53f74-135">Your app is now able to store a set of categories in local storage on the device and register with the notification hub whenever the user changes the selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="53f74-136">Register for notifications</span><span class="sxs-lookup"><span data-stu-id="53f74-136">Register for notifications</span></span>
<span data-ttu-id="53f74-137">These steps register with the notification hub on startup using the categories that have been stored in local storage.</span><span class="sxs-lookup"><span data-stu-id="53f74-137">These steps register with the notification hub on startup using the categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="53f74-138">Because the registrationId assigned by Google Cloud Messaging (GCM) can change at any time, you should register for notifications frequently to avoid notification failures.</span><span class="sxs-lookup"><span data-stu-id="53f74-138">Because the registrationId assigned by Google Cloud Messaging (GCM) can change at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="53f74-139">This example registers for notification every time that the app starts.</span><span class="sxs-lookup"><span data-stu-id="53f74-139">This example registers for notification every time that the app starts.</span></span> <span data-ttu-id="53f74-140">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span><span class="sxs-lookup"><span data-stu-id="53f74-140">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
> 
> 

1. <span data-ttu-id="53f74-141">Add the following code at the end of the **onCreate** method in the **MainActivity** class:</span><span class="sxs-lookup"><span data-stu-id="53f74-141">Add the following code at the end of the **onCreate** method in the **MainActivity** class:</span></span>
   
        notifications.subscribeToCategories(notifications.retrieveCategories());
   
    <span data-ttu-id="53f74-142">This makes sure that every time the app starts it retrieves the categories from local storage and requests a registeration for these categories.</span><span class="sxs-lookup"><span data-stu-id="53f74-142">This makes sure that every time the app starts it retrieves the categories from local storage and requests a registeration for these categories.</span></span> 
2. <span data-ttu-id="53f74-143">Then update the `onStart()` method of the `MainActivity` class as follows:</span><span class="sxs-lookup"><span data-stu-id="53f74-143">Then update the `onStart()` method of the `MainActivity` class as follows:</span></span>
   
    <span data-ttu-id="53f74-144">@Override  protected void onStart() {</span><span class="sxs-lookup"><span data-stu-id="53f74-144">@Override  protected void onStart() {</span></span>
   
        super.onStart();
        isVisible = true;
   
        Set<String> categories = notifications.retrieveCategories();
   
        CheckBox world = (CheckBox) findViewById(R.id.worldBox);
        world.setChecked(categories.contains("world"));
        CheckBox politics = (CheckBox) findViewById(R.id.politicsBox);
        politics.setChecked(categories.contains("politics"));
        CheckBox business = (CheckBox) findViewById(R.id.businessBox);
        business.setChecked(categories.contains("business"));
        CheckBox technology = (CheckBox) findViewById(R.id.technologyBox);
        technology.setChecked(categories.contains("technology"));
        CheckBox science = (CheckBox) findViewById(R.id.scienceBox);
        science.setChecked(categories.contains("science"));
        CheckBox sports = (CheckBox) findViewById(R.id.sportsBox);
        sports.setChecked(categories.contains("sports"));
    <span data-ttu-id="53f74-145">}</span><span class="sxs-lookup"><span data-stu-id="53f74-145">}</span></span>
   
    <span data-ttu-id="53f74-146">This updates the main activity based on the status of previously saved categories.</span><span class="sxs-lookup"><span data-stu-id="53f74-146">This updates the main activity based on the status of previously saved categories.</span></span>

<span data-ttu-id="53f74-147">The app is now complete and can store a set of categories in the device local storage used to register with the notification hub whenever the user changes the selection of categories.</span><span class="sxs-lookup"><span data-stu-id="53f74-147">The app is now complete and can store a set of categories in the device local storage used to register with the notification hub whenever the user changes the selection of categories.</span></span> <span data-ttu-id="53f74-148">Next, we will define a backend that can send category notifications to this app.</span><span class="sxs-lookup"><span data-stu-id="53f74-148">Next, we will define a backend that can send category notifications to this app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="53f74-149">Sending tagged notifications</span><span class="sxs-lookup"><span data-stu-id="53f74-149">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="53f74-150">Run the app and generate notifications</span><span class="sxs-lookup"><span data-stu-id="53f74-150">Run the app and generate notifications</span></span>
1. <span data-ttu-id="53f74-151">In Android Studio, build the app and start it on a device or emulator.</span><span class="sxs-lookup"><span data-stu-id="53f74-151">In Android Studio, build the app and start it on a device or emulator.</span></span>
   
    <span data-ttu-id="53f74-152">Note that the app UI provides a set of toggles that lets you choose the categories to subscribe to.</span><span class="sxs-lookup"><span data-stu-id="53f74-152">Note that the app UI provides a set of toggles that lets you choose the categories to subscribe to.</span></span>
2. <span data-ttu-id="53f74-153">Enable one or more categories toggles, then click **Subscribe**.</span><span class="sxs-lookup"><span data-stu-id="53f74-153">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="53f74-154">The app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span><span class="sxs-lookup"><span data-stu-id="53f74-154">The app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span> <span data-ttu-id="53f74-155">The registered categories are returned and displayed in a toast notification.</span><span class="sxs-lookup"><span data-stu-id="53f74-155">The registered categories are returned and displayed in a toast notification.</span></span>
3. <span data-ttu-id="53f74-156">Send a new notification by running the .NET Console app.</span><span class="sxs-lookup"><span data-stu-id="53f74-156">Send a new notification by running the .NET Console app.</span></span>  <span data-ttu-id="53f74-157">Alternatively, you can send tagged template notifications using the debug tab of your notification hub in the [Azure Classic Portal].</span><span class="sxs-lookup"><span data-stu-id="53f74-157">Alternatively, you can send tagged template notifications using the debug tab of your notification hub in the [Azure Classic Portal].</span></span>
   
    <span data-ttu-id="53f74-158">Notifications for the selected categories appear as toast notifications.</span><span class="sxs-lookup"><span data-stu-id="53f74-158">Notifications for the selected categories appear as toast notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53f74-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="53f74-159">Next steps</span></span>
<span data-ttu-id="53f74-160">In this tutorial we learned how to broadcast breaking news by category.</span><span class="sxs-lookup"><span data-stu-id="53f74-160">In this tutorial we learned how to broadcast breaking news by category.</span></span> <span data-ttu-id="53f74-161">Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:</span><span class="sxs-lookup"><span data-stu-id="53f74-161">Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="53f74-162">[Use Notification Hubs to broadcast localized breaking news]</span><span class="sxs-lookup"><span data-stu-id="53f74-162">[Use Notification Hubs to broadcast localized breaking news]</span></span>
  
    <span data-ttu-id="53f74-163">Learn how to expand the breaking news app to enable sending localized notifications.</span><span class="sxs-lookup"><span data-stu-id="53f74-163">Learn how to expand the breaking news app to enable sending localized notifications.</span></span>

<!-- Images. -->
[A1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-aspnet-backend-android-breaking-news/android-breaking-news1.PNG

<!-- URLs.-->
[get-started]: notification-hubs-android-push-notification-google-gcm-get-started.md
[Use Notification Hubs to broadcast localized breaking news]: /manage/services/notification-hubs/breaking-news-localized-dotnet/
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Azure Classic Portal]: https://manage.windowsazure.com
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591

