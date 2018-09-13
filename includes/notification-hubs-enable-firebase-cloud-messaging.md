

1. Sign in to the [Firebase console](https://firebase.google.com/console/). Create a new Firebase project if you don't already have one.
2. After your project is created, click **Add Firebase to your Android app** and follow the instructions provided.

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-enable-firebase-cloud-messaging/notification-hubs-add-firebase-to-android-app.png)
3. In the Firebase console, click the cog for your project and then click **Project Settings**.

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-enable-firebase-cloud-messaging/notification-hubs-firebase-console-project-settings.png)
4. Click the **Cloud Messaging** tab in your project settings, and copy the value of the **Server key** and **Sender ID**. These values will be used later to configure the notification hub access policy, and your notification handler in the app.


