1. <span data-ttu-id="549da-101">In your **app** project, open the file `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="549da-101">In your **app** project, open the file `AndroidManifest.xml`.</span></span> <span data-ttu-id="549da-102">In the code in the next two steps, replace *`**my_app_package**`* with the name of the app package for your project.</span><span class="sxs-lookup"><span data-stu-id="549da-102">In the code in the next two steps, replace *`**my_app_package**`* with the name of the app package for your project.</span></span> <span data-ttu-id="549da-103">This is the value of the `package` attribute of the `manifest` tag.</span><span class="sxs-lookup"><span data-stu-id="549da-103">This is the value of the `package` attribute of the `manifest` tag.</span></span>
2. <span data-ttu-id="549da-104">Add the following new permissions after the existing `uses-permission` element:</span><span class="sxs-lookup"><span data-stu-id="549da-104">Add the following new permissions after the existing `uses-permission` element:</span></span>

        <permission android:name="**my_app_package**.permission.C2D_MESSAGE"
            android:protectionLevel="signature" />
        <uses-permission android:name="**my_app_package**.permission.C2D_MESSAGE" />
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="android.permission.GET_ACCOUNTS" />
        <uses-permission android:name="android.permission.WAKE_LOCK" />
3. <span data-ttu-id="549da-105">Add the following code after the `application` opening tag:</span><span class="sxs-lookup"><span data-stu-id="549da-105">Add the following code after the `application` opening tag:</span></span>

        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
                                         android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="**my_app_package**" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="549da-106">Open the file *ToDoActivity.java*, and add the following import statement:</span><span class="sxs-lookup"><span data-stu-id="549da-106">Open the file *ToDoActivity.java*, and add the following import statement:</span></span>

        import com.microsoft.windowsazure.notifications.NotificationsManager;
5. <span data-ttu-id="549da-107">Add the following private variable to the class.</span><span class="sxs-lookup"><span data-stu-id="549da-107">Add the following private variable to the class.</span></span> <span data-ttu-id="549da-108">Replace *`<PROJECT_NUMBER>`* with the project number assigned by Google to your app in the preceding procedure.</span><span class="sxs-lookup"><span data-stu-id="549da-108">Replace *`<PROJECT_NUMBER>`* with the project number assigned by Google to your app in the preceding procedure.</span></span>

        public static final String SENDER_ID = "<PROJECT_NUMBER>";
6. <span data-ttu-id="549da-109">Change the definition of *MobileServiceClient* from **private** to **public static**, so it now looks like this:</span><span class="sxs-lookup"><span data-stu-id="549da-109">Change the definition of *MobileServiceClient* from **private** to **public static**, so it now looks like this:</span></span>

        public static MobileServiceClient mClient;
7. <span data-ttu-id="549da-110">Add a new class to handle notifications.</span><span class="sxs-lookup"><span data-stu-id="549da-110">Add a new class to handle notifications.</span></span> <span data-ttu-id="549da-111">In Project Explorer, open the **src** > **main** > **java** nodes, and right-click the package name node.</span><span class="sxs-lookup"><span data-stu-id="549da-111">In Project Explorer, open the **src** > **main** > **java** nodes, and right-click the package name node.</span></span> <span data-ttu-id="549da-112">Click **New**, and then click **Java Class**.</span><span class="sxs-lookup"><span data-stu-id="549da-112">Click **New**, and then click **Java Class**.</span></span>
8. <span data-ttu-id="549da-113">In **Name**, type `MyHandler`, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="549da-113">In **Name**, type `MyHandler`, and then click **OK**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/app-service-mobile-android-configure-push/android-studio-create-class.png)

9. <span data-ttu-id="549da-114">In the MyHandler file, replace the class declaration with:</span><span class="sxs-lookup"><span data-stu-id="549da-114">In the MyHandler file, replace the class declaration with:</span></span>

        public class MyHandler extends NotificationsHandler {
10. <span data-ttu-id="549da-115">Add the following import statements for the `MyHandler` class:</span><span class="sxs-lookup"><span data-stu-id="549da-115">Add the following import statements for the `MyHandler` class:</span></span>

        import com.microsoft.windowsazure.notifications.NotificationsHandler;
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.AsyncTask;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
11. <span data-ttu-id="549da-116">Next add this member to the `MyHandler` class:</span><span class="sxs-lookup"><span data-stu-id="549da-116">Next add this member to the `MyHandler` class:</span></span>

        public static final int NOTIFICATION_ID = 1;
12. <span data-ttu-id="549da-117">In the `MyHandler` class, add the following code to override the **onRegistered** method, which registers your device with the mobile service notification hub.</span><span class="sxs-lookup"><span data-stu-id="549da-117">In the `MyHandler` class, add the following code to override the **onRegistered** method, which registers your device with the mobile service notification hub.</span></span>

        @Override
        public void onRegistered(Context context,  final String gcmRegistrationId) {
           super.onRegistered(context, gcmRegistrationId);

           new AsyncTask<Void, Void, Void>() {

               protected Void doInBackground(Void... params) {
                   try {
                       ToDoActivity.mClient.getPush().register(gcmRegistrationId);
                       return null;
                   }
                   catch(Exception e) {
                       // handle error                
                   }
                   return null;              
               }
           }.execute();
       <span data-ttu-id="549da-118">}</span><span class="sxs-lookup"><span data-stu-id="549da-118">}</span></span>
13. <span data-ttu-id="549da-119">In the `MyHandler` class, add the following code to override the **onReceive** method, which causes the notification to display when it is received.</span><span class="sxs-lookup"><span data-stu-id="549da-119">In the `MyHandler` class, add the following code to override the **onReceive** method, which causes the notification to display when it is received.</span></span>

        @Override
        public void onReceive(Context context, Bundle bundle) {
               String msg = bundle.getString("message");

               PendingIntent contentIntent = PendingIntent.getActivity(context,
                       0, // requestCode
                       new Intent(context, ToDoActivity.class),
                       0); // flags

               Notification notification = new NotificationCompat.Builder(context)
                       .setSmallIcon(R.drawable.ic_launcher)
                       .setContentTitle("Notification Hub Demo")
                       .setStyle(new NotificationCompat.BigTextStyle().bigText(msg))
                       .setContentText(msg)
                       .setContentIntent(contentIntent)
                       .build();

               NotificationManager notificationManager = (NotificationManager)
                       context.getSystemService(Context.NOTIFICATION_SERVICE);
               notificationManager.notify(NOTIFICATION_ID, notification);
       <span data-ttu-id="549da-120">}</span><span class="sxs-lookup"><span data-stu-id="549da-120">}</span></span>
14. <span data-ttu-id="549da-121">Back in the TodoActivity.java file, update the **onCreate** method of the *ToDoActivity* class to register the notification handler class.</span><span class="sxs-lookup"><span data-stu-id="549da-121">Back in the TodoActivity.java file, update the **onCreate** method of the *ToDoActivity* class to register the notification handler class.</span></span> <span data-ttu-id="549da-122">Make sure to add this code after the *MobileServiceClient* is instantiated.</span><span class="sxs-lookup"><span data-stu-id="549da-122">Make sure to add this code after the *MobileServiceClient* is instantiated.</span></span>

        NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);

    <span data-ttu-id="549da-123">Your app is now updated to support push notifications.</span><span class="sxs-lookup"><span data-stu-id="549da-123">Your app is now updated to support push notifications.</span></span>

