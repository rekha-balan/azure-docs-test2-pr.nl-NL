
<span data-ttu-id="d84b4-101">To register the app for push notifications through Apple Push Notification Service (APNS), you must create a push certificate, App ID, and provisioning profile for the project on Apple's developer portal.</span><span class="sxs-lookup"><span data-stu-id="d84b4-101">To register the app for push notifications through Apple Push Notification Service (APNS), you must create a push certificate, App ID, and provisioning profile for the project on Apple's developer portal.</span></span>

<span data-ttu-id="d84b4-102">The App ID contains the configuration settings that enable your app to send and receive push notifications.</span><span class="sxs-lookup"><span data-stu-id="d84b4-102">The App ID contains the configuration settings that enable your app to send and receive push notifications.</span></span> <span data-ttu-id="d84b4-103">These settings include the push notification certificate that's needed to authenticate with APNS when the app is sending and receiving push notifications.</span><span class="sxs-lookup"><span data-stu-id="d84b4-103">These settings include the push notification certificate that's needed to authenticate with APNS when the app is sending and receiving push notifications.</span></span>

<span data-ttu-id="d84b4-104">For more information about these concepts, see the official [Apple Push Notification Service](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1) documentation.</span><span class="sxs-lookup"><span data-stu-id="d84b4-104">For more information about these concepts, see the official [Apple Push Notification Service](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1) documentation.</span></span>

## <a name="generate-the-certificate-signing-request-file-for-the-push-certificate"></a><span data-ttu-id="d84b4-105">Generate the certificate signing request file for the push certificate</span><span class="sxs-lookup"><span data-stu-id="d84b4-105">Generate the certificate signing request file for the push certificate</span></span>
<span data-ttu-id="d84b4-106">These steps walk you through the process of creating the certificate signing request, which generates a push certificate that's used with APNS.</span><span class="sxs-lookup"><span data-stu-id="d84b4-106">These steps walk you through the process of creating the certificate signing request, which generates a push certificate that's used with APNS.</span></span>

1. <span data-ttu-id="d84b4-107">On your Mac, run the Keychain Access tool.</span><span class="sxs-lookup"><span data-stu-id="d84b4-107">On your Mac, run the Keychain Access tool.</span></span> <span data-ttu-id="d84b4-108">It can be opened from the **Utilities** folder or the **Other** folder on the launch pad.</span><span class="sxs-lookup"><span data-stu-id="d84b4-108">It can be opened from the **Utilities** folder or the **Other** folder on the launch pad.</span></span>

2. <span data-ttu-id="d84b4-109">Select **Keychain Access**, expand **Certificate Assistant**, and then select **Request a Certificate from a Certificate Authority...**.</span><span class="sxs-lookup"><span data-stu-id="d84b4-109">Select **Keychain Access**, expand **Certificate Assistant**, and then select **Request a Certificate from a Certificate Authority...**.</span></span>

      ![Request a certificate](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-xamarin-enable-apple-push-notifications/notification-hubs-request-cert-from-ca.png)

3. <span data-ttu-id="d84b4-111">Select your **User Email Address** and **Common Name**.</span><span class="sxs-lookup"><span data-stu-id="d84b4-111">Select your **User Email Address** and **Common Name**.</span></span>

4. <span data-ttu-id="d84b4-112">Make sure that **Saved to disk** is selected, and then select **Continue**.</span><span class="sxs-lookup"><span data-stu-id="d84b4-112">Make sure that **Saved to disk** is selected, and then select **Continue**.</span></span> <span data-ttu-id="d84b4-113">Leave the **CA Email Address** field blank, since it's not required.</span><span class="sxs-lookup"><span data-stu-id="d84b4-113">Leave the **CA Email Address** field blank, since it's not required.</span></span>

      ![Certificate information](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-xamarin-enable-apple-push-notifications/notification-hubs-csr-info.png)

4. <span data-ttu-id="d84b4-115">Type a name for the certificate signing request (CSR) file in **Save As**.</span><span class="sxs-lookup"><span data-stu-id="d84b4-115">Type a name for the certificate signing request (CSR) file in **Save As**.</span></span>
5. <span data-ttu-id="d84b4-116">Select the location in **Where**, and then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="d84b4-116">Select the location in **Where**, and then select **Save**.</span></span>

      ![Save the certificate signing request](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-xamarin-enable-apple-push-notifications/notification-hubs-save-csr.png)

      <span data-ttu-id="d84b4-118">This saves the CSR file in the selected location.</span><span class="sxs-lookup"><span data-stu-id="d84b4-118">This saves the CSR file in the selected location.</span></span> <span data-ttu-id="d84b4-119">(The default location is your desktop.) Remember the location that you choose for this file.</span><span class="sxs-lookup"><span data-stu-id="d84b4-119">(The default location is your desktop.) Remember the location that you choose for this file.</span></span>

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="d84b4-120">Register your app for push notifications</span><span class="sxs-lookup"><span data-stu-id="d84b4-120">Register your app for push notifications</span></span>
<span data-ttu-id="d84b4-121">Create a new Explicit App ID for your application with Apple, and then configure it for push notifications.</span><span class="sxs-lookup"><span data-stu-id="d84b4-121">Create a new Explicit App ID for your application with Apple, and then configure it for push notifications.</span></span>  

1. <span data-ttu-id="d84b4-122">Navigate to the [iOS Provisioning Portal](http://go.microsoft.com/fwlink/p/?LinkId=272456) at the Apple Developer Center, and then sign in with your Apple ID.</span><span class="sxs-lookup"><span data-stu-id="d84b4-122">Navigate to the [iOS Provisioning Portal](http://go.microsoft.com/fwlink/p/?LinkId=272456) at the Apple Developer Center, and then sign in with your Apple ID.</span></span>

2. <span data-ttu-id="d84b4-123">Select **Identifiers**, and then select **App IDs**.</span><span class="sxs-lookup"><span data-stu-id="d84b4-123">Select **Identifiers**, and then select **App IDs**.</span></span>

3. <span data-ttu-id="d84b4-124">Select the **+** sign to register a new app.</span><span class="sxs-lookup"><span data-stu-id="d84b4-124">Select the **+** sign to register a new app.</span></span>

      ![Register a new app](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-xamarin-enable-apple-push-notifications/notification-hubs-ios-appids.png)

4. <span data-ttu-id="d84b4-126">Update the following three fields for your new app, and then select **Continue**:</span><span class="sxs-lookup"><span data-stu-id="d84b4-126">Update the following three fields for your new app, and then select **Continue**:</span></span>

   * <span data-ttu-id="d84b4-127">**Name**: In the **App ID Description** section, type a descriptive name for your app.</span><span class="sxs-lookup"><span data-stu-id="d84b4-127">**Name**: In the **App ID Description** section, type a descriptive name for your app.</span></span>

   * <span data-ttu-id="d84b4-128">**Bundle Identifier**: Under the **Explicit App ID** section, enter a **Bundle Identifier** in the form `<Organization Identifier>.<Product Name>`, as described in the [App Distribution Guide](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8).</span><span class="sxs-lookup"><span data-stu-id="d84b4-128">**Bundle Identifier**: Under the **Explicit App ID** section, enter a **Bundle Identifier** in the form `<Organization Identifier>.<Product Name>`, as described in the [App Distribution Guide](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8).</span></span> <span data-ttu-id="d84b4-129">This must match what's used in the XCode, Xamarin, or Cordova project for your app.</span><span class="sxs-lookup"><span data-stu-id="d84b4-129">This must match what's used in the XCode, Xamarin, or Cordova project for your app.</span></span>

   * <span data-ttu-id="d84b4-130">**Push Notifications**: Select the **Push Notifications** option in the **App Services** section.</span><span class="sxs-lookup"><span data-stu-id="d84b4-130">**Push Notifications**: Select the **Push Notifications** option in the **App Services** section.</span></span>

     ![Register app ID](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-xamarin-enable-apple-push-notifications/notification-hubs-new-appid-info.png)

5. <span data-ttu-id="d84b4-132">On the **Confirm your App ID screen**, review the settings.</span><span class="sxs-lookup"><span data-stu-id="d84b4-132">On the **Confirm your App ID screen**, review the settings.</span></span> <span data-ttu-id="d84b4-133">After you've verified them, select **Register**.</span><span class="sxs-lookup"><span data-stu-id="d84b4-133">After you've verified them, select **Register**.</span></span>

6. <span data-ttu-id="d84b4-134">After submitting the new App ID, you see the **Registration complete** screen.</span><span class="sxs-lookup"><span data-stu-id="d84b4-134">After submitting the new App ID, you see the **Registration complete** screen.</span></span> <span data-ttu-id="d84b4-135">Select **Done**.</span><span class="sxs-lookup"><span data-stu-id="d84b4-135">Select **Done**.</span></span>

7. <span data-ttu-id="d84b4-136">In the Developer Center, under **App IDs**, locate the app ID that you created, and select its row.</span><span class="sxs-lookup"><span data-stu-id="d84b4-136">In the Developer Center, under **App IDs**, locate the app ID that you created, and select its row.</span></span> <span data-ttu-id="d84b4-137">Selecting the app ID row displays the app details.</span><span class="sxs-lookup"><span data-stu-id="d84b4-137">Selecting the app ID row displays the app details.</span></span> <span data-ttu-id="d84b4-138">Then select the **Edit** button at the bottom.</span><span class="sxs-lookup"><span data-stu-id="d84b4-138">Then select the **Edit** button at the bottom.</span></span>

8. <span data-ttu-id="d84b4-139">Scroll to the bottom of the screen, and then select the **Create Certificate...** button under the section **Development SSL Certificate**.</span><span class="sxs-lookup"><span data-stu-id="d84b4-139">Scroll to the bottom of the screen, and then select the **Create Certificate...** button under the section **Development SSL Certificate**.</span></span>

      ![Development Push SSL Certificate](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-xamarin-enable-apple-push-notifications/notification-hubs-appid-create-cert.png)

 <span data-ttu-id="d84b4-141">This displays the "Add iOS Certificate" assistant.</span><span class="sxs-lookup"><span data-stu-id="d84b4-141">This displays the "Add iOS Certificate" assistant.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d84b4-142">This tutorial uses a development certificate.</span><span class="sxs-lookup"><span data-stu-id="d84b4-142">This tutorial uses a development certificate.</span></span> <span data-ttu-id="d84b4-143">You use the same process when you register a production certificate.</span><span class="sxs-lookup"><span data-stu-id="d84b4-143">You use the same process when you register a production certificate.</span></span> <span data-ttu-id="d84b4-144">Make sure that you use the same certificate type when sending notifications.</span><span class="sxs-lookup"><span data-stu-id="d84b4-144">Make sure that you use the same certificate type when sending notifications.</span></span>
   >

9. <span data-ttu-id="d84b4-145">Select **Choose File**, and then browse to the location where you saved the CSR for your push certificate.</span><span class="sxs-lookup"><span data-stu-id="d84b4-145">Select **Choose File**, and then browse to the location where you saved the CSR for your push certificate.</span></span> <span data-ttu-id="d84b4-146">Then select **Generate**.</span><span class="sxs-lookup"><span data-stu-id="d84b4-146">Then select **Generate**.</span></span>

      ![Generate certificate](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-xamarin-enable-apple-push-notifications/notification-hubs-appid-cert-choose-csr.png)

10. <span data-ttu-id="d84b4-148">After the certificate has been created by the portal, select the **Download** button.</span><span class="sxs-lookup"><span data-stu-id="d84b4-148">After the certificate has been created by the portal, select the **Download** button.</span></span>

      ![Certificate ready](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-xamarin-enable-apple-push-notifications/notification-hubs-appid-download-cert.png)

       <span data-ttu-id="d84b4-150">This downloads the signing certificate and saves it to your computer in your Downloads folder.</span><span class="sxs-lookup"><span data-stu-id="d84b4-150">This downloads the signing certificate and saves it to your computer in your Downloads folder.</span></span>

      ![Download folder](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-downloaded.png)

   > [!NOTE]
   > <span data-ttu-id="d84b4-152">By default, the downloaded file is a development certificate that's named **aps_development.cer**.</span><span class="sxs-lookup"><span data-stu-id="d84b4-152">By default, the downloaded file is a development certificate that's named **aps_development.cer**.</span></span>
   >
   >
11. <span data-ttu-id="d84b4-153">Double-click the downloaded push certificate **aps_development.cer**.</span><span class="sxs-lookup"><span data-stu-id="d84b4-153">Double-click the downloaded push certificate **aps_development.cer**.</span></span> <span data-ttu-id="d84b4-154">This installs the new certificate in the Keychain, as shown in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="d84b4-154">This installs the new certificate in the Keychain, as shown in the following screenshot:</span></span>

       ![Keychain access](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-xamarin-enable-apple-push-notifications/notification-hubs-cert-in-keychain.png)

   > [!NOTE]
   > <span data-ttu-id="d84b4-156">The name in your certificate might be different, but it is prefixed with **Apple Development iOS Push Services**.</span><span class="sxs-lookup"><span data-stu-id="d84b4-156">The name in your certificate might be different, but it is prefixed with **Apple Development iOS Push Services**.</span></span>
   >
   >
12. <span data-ttu-id="d84b4-157">In **Keychain Access**, select the new push certificate that you created in the **Certificates** category.</span><span class="sxs-lookup"><span data-stu-id="d84b4-157">In **Keychain Access**, select the new push certificate that you created in the **Certificates** category.</span></span> <span data-ttu-id="d84b4-158">Select **Export**, name the file, select the **.p12** format, and then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="d84b4-158">Select **Export**, name the file, select the **.p12** format, and then select **Save**.</span></span>

    <span data-ttu-id="d84b4-159">Remember the file name and location of the exported .p12 push certificate.</span><span class="sxs-lookup"><span data-stu-id="d84b4-159">Remember the file name and location of the exported .p12 push certificate.</span></span> <span data-ttu-id="d84b4-160">You use it to enable authentication with APNS by uploading it on the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="d84b4-160">You use it to enable authentication with APNS by uploading it on the Azure classic portal.</span></span> <span data-ttu-id="d84b4-161">If the **.p12** format option is not available, you might need to restart Keychain Access.</span><span class="sxs-lookup"><span data-stu-id="d84b4-161">If the **.p12** format option is not available, you might need to restart Keychain Access.</span></span>

## <a name="create-a-provisioning-profile-for-the-app"></a><span data-ttu-id="d84b4-162">Create a provisioning profile for the app</span><span class="sxs-lookup"><span data-stu-id="d84b4-162">Create a provisioning profile for the app</span></span>
1. <span data-ttu-id="d84b4-163">Back in the <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a>, select **Provisioning Profiles**, select **All**, and then select the **+** button to create a profile.</span><span class="sxs-lookup"><span data-stu-id="d84b4-163">Back in the <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a>, select **Provisioning Profiles**, select **All**, and then select the **+** button to create a profile.</span></span> <span data-ttu-id="d84b4-164">This launches the **Add iOS Provisioning** profile tool.</span><span class="sxs-lookup"><span data-stu-id="d84b4-164">This launches the **Add iOS Provisioning** profile tool.</span></span>

      ![Provisioning profiles](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-xamarin-enable-apple-push-notifications/notification-hubs-new-provisioning-profile.png)

2. <span data-ttu-id="d84b4-166">Under **Development**, select **iOS App Development** as the provisioning profile type, and then select **Continue**.</span><span class="sxs-lookup"><span data-stu-id="d84b4-166">Under **Development**, select **iOS App Development** as the provisioning profile type, and then select **Continue**.</span></span>

3. <span data-ttu-id="d84b4-167">In the **App ID** drop-down list, select the app ID you created, and then select **Continue**.</span><span class="sxs-lookup"><span data-stu-id="d84b4-167">In the **App ID** drop-down list, select the app ID you created, and then select **Continue**.</span></span>

      ![Select app ID](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-xamarin-enable-apple-push-notifications/notification-hubs-select-appid-for-provisioning.png)

4. <span data-ttu-id="d84b4-169">In the **Select certificates** screen, select the development certificate that you use for code signing, and then select **Continue**.</span><span class="sxs-lookup"><span data-stu-id="d84b4-169">In the **Select certificates** screen, select the development certificate that you use for code signing, and then select **Continue**.</span></span> <span data-ttu-id="d84b4-170">This is a signing certificate, not the push certificate you created.</span><span class="sxs-lookup"><span data-stu-id="d84b4-170">This is a signing certificate, not the push certificate you created.</span></span>

       ![Signing certificate](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-xamarin-enable-apple-push-notifications/notification-hubs-provisioning-select-cert.png)

5. <span data-ttu-id="d84b4-171">Select the **Devices** to use for testing, and then select **Continue**.</span><span class="sxs-lookup"><span data-stu-id="d84b4-171">Select the **Devices** to use for testing, and then select **Continue**.</span></span>

     ![Add provisioning profile](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-xamarin-enable-apple-push-notifications/notification-hubs-provisioning-select-devices.png)

6. <span data-ttu-id="d84b4-173">Finally, in **Profile Name**, pick a name for the profile, and then select **Generate**.</span><span class="sxs-lookup"><span data-stu-id="d84b4-173">Finally, in **Profile Name**, pick a name for the profile, and then select **Generate**.</span></span>

      ![Name the profile](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-xamarin-enable-apple-push-notifications/notification-hubs-provisioning-name-profile.png)















