1. <span data-ttu-id="9a9f0-101">Open the Android SDK Manager by clicking the icon on the toolbar of Android Studio or by clicking **Tools** -> **Android** -> **SDK Manager** on the menu.</span><span class="sxs-lookup"><span data-stu-id="9a9f0-101">Open the Android SDK Manager by clicking the icon on the toolbar of Android Studio or by clicking **Tools** -> **Android** -> **SDK Manager** on the menu.</span></span> <span data-ttu-id="9a9f0-102">Locate the target version of the Android SDK that is used in your project , open it by clicking **Show Package Details**, and choose **Google APIs**, if it is not already installed.</span><span class="sxs-lookup"><span data-stu-id="9a9f0-102">Locate the target version of the Android SDK that is used in your project , open it by clicking **Show Package Details**, and choose **Google APIs**, if it is not already installed.</span></span>
2. <span data-ttu-id="9a9f0-103">Click the **SDK Tools** tab. If you haven't already installed Google Play Service, click **Google Play Services** as shown below.</span><span class="sxs-lookup"><span data-stu-id="9a9f0-103">Click the **SDK Tools** tab. If you haven't already installed Google Play Service, click **Google Play Services** as shown below.</span></span> <span data-ttu-id="9a9f0-104">Then click **Apply** to install.</span><span class="sxs-lookup"><span data-stu-id="9a9f0-104">Then click **Apply** to install.</span></span> 
   
    <span data-ttu-id="9a9f0-105">Note the SDK path, for use in a later step.</span><span class="sxs-lookup"><span data-stu-id="9a9f0-105">Note the SDK path, for use in a later step.</span></span> 
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-sdk-manager.png)
3. <span data-ttu-id="9a9f0-106">Open the **build.gradle** file in the app directory.</span><span class="sxs-lookup"><span data-stu-id="9a9f0-106">Open the **build.gradle** file in the app directory.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-add-google-play-dependency.png)
4. <span data-ttu-id="9a9f0-107">Add this line under *dependencies*:</span><span class="sxs-lookup"><span data-stu-id="9a9f0-107">Add this line under *dependencies*:</span></span> 
   
           compile 'com.google.android.gms:play-services-gcm:9.2.0'
5. <span data-ttu-id="9a9f0-108">Click the **Sync Project with Gradle Files** icon in the tool bar.</span><span class="sxs-lookup"><span data-stu-id="9a9f0-108">Click the **Sync Project with Gradle Files** icon in the tool bar.</span></span>
6. <span data-ttu-id="9a9f0-109">Open **AndroidManifest.xml** and add this tag to the *application* tag.</span><span class="sxs-lookup"><span data-stu-id="9a9f0-109">Open **AndroidManifest.xml** and add this tag to the *application* tag.</span></span>
   
        <meta-data android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />



