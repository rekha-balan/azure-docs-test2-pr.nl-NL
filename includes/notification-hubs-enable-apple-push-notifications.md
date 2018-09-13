

## <a name="generate-the-certificate-signing-request-file"></a><span data-ttu-id="70ea8-101">Generate the Certificate Signing Request file</span><span class="sxs-lookup"><span data-stu-id="70ea8-101">Generate the Certificate Signing Request file</span></span>
<span data-ttu-id="70ea8-102">The Apple Push Notification Service (APNS) uses certificates to authenticate your push notifications.</span><span class="sxs-lookup"><span data-stu-id="70ea8-102">The Apple Push Notification Service (APNS) uses certificates to authenticate your push notifications.</span></span> <span data-ttu-id="70ea8-103">Follow these instructions to create the necessary push certificate to send and receive notifications.</span><span class="sxs-lookup"><span data-stu-id="70ea8-103">Follow these instructions to create the necessary push certificate to send and receive notifications.</span></span> <span data-ttu-id="70ea8-104">For more information on these concepts see the official [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) documentation.</span><span class="sxs-lookup"><span data-stu-id="70ea8-104">For more information on these concepts see the official [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) documentation.</span></span>

<span data-ttu-id="70ea8-105">Generate the Certificate Signing Request (CSR) file, which is used by Apple to generate a signed push certificate.</span><span class="sxs-lookup"><span data-stu-id="70ea8-105">Generate the Certificate Signing Request (CSR) file, which is used by Apple to generate a signed push certificate.</span></span>

1. <span data-ttu-id="70ea8-106">On your Mac, run the Keychain Access tool.</span><span class="sxs-lookup"><span data-stu-id="70ea8-106">On your Mac, run the Keychain Access tool.</span></span> <span data-ttu-id="70ea8-107">It can be opened from the **Utilities** folder or the **Other** folder on the launch pad.</span><span class="sxs-lookup"><span data-stu-id="70ea8-107">It can be opened from the **Utilities** folder or the **Other** folder on the launch pad.</span></span>
2. <span data-ttu-id="70ea8-108">Click **Keychain Access**, expand **Certificate Assistant**, then click **Request a Certificate from a Certificate Authority...**.</span><span class="sxs-lookup"><span data-stu-id="70ea8-108">Click **Keychain Access**, expand **Certificate Assistant**, then click **Request a Certificate from a Certificate Authority...**.</span></span>
   
      ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-enable-apple-push-notifications/notification-hubs-request-cert-from-ca.png)
3. <span data-ttu-id="70ea8-109">Select your **User Email Address** and **Common Name** , make sure that **Saved to disk** is selected, and then click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="70ea8-109">Select your **User Email Address** and **Common Name** , make sure that **Saved to disk** is selected, and then click **Continue**.</span></span> <span data-ttu-id="70ea8-110">Leave the **CA Email Address** field blank as it is not required.</span><span class="sxs-lookup"><span data-stu-id="70ea8-110">Leave the **CA Email Address** field blank as it is not required.</span></span>
   
      ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-enable-apple-push-notifications/notification-hubs-csr-info.png)
4. <span data-ttu-id="70ea8-111">Type a name for the Certificate Signing Request (CSR) file in **Save As**, select the location in **Where**, then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="70ea8-111">Type a name for the Certificate Signing Request (CSR) file in **Save As**, select the location in **Where**, then click **Save**.</span></span>
   
      ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-enable-apple-push-notifications/notification-hubs-save-csr.png)
   
      <span data-ttu-id="70ea8-112">This saves the CSR file in the selected location; the default location is in the Desktop.</span><span class="sxs-lookup"><span data-stu-id="70ea8-112">This saves the CSR file in the selected location; the default location is in the Desktop.</span></span> <span data-ttu-id="70ea8-113">Remember the location chosen for this file.</span><span class="sxs-lookup"><span data-stu-id="70ea8-113">Remember the location chosen for this file.</span></span>

<span data-ttu-id="70ea8-114">Next, you will register your app with Apple, enable push notifications, and upload this exported CSR to create a push certificate.</span><span class="sxs-lookup"><span data-stu-id="70ea8-114">Next, you will register your app with Apple, enable push notifications, and upload this exported CSR to create a push certificate.</span></span>

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="70ea8-115">Register your app for push notifications</span><span class="sxs-lookup"><span data-stu-id="70ea8-115">Register your app for push notifications</span></span>
<span data-ttu-id="70ea8-116">To be able to send push notifications to an iOS app, you must register your application with Apple and also register for push notifications.</span><span class="sxs-lookup"><span data-stu-id="70ea8-116">To be able to send push notifications to an iOS app, you must register your application with Apple and also register for push notifications.</span></span>  

1. <span data-ttu-id="70ea8-117">If you have not already registered your app, navigate to the <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a> at the Apple Developer Center, log on with your Apple ID, click **Identifiers**, then click **App IDs**, and finally click on the **+** sign to register a new app.</span><span class="sxs-lookup"><span data-stu-id="70ea8-117">If you have not already registered your app, navigate to the <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a> at the Apple Developer Center, log on with your Apple ID, click **Identifiers**, then click **App IDs**, and finally click on the **+** sign to register a new app.</span></span>
   
      ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids.png)
      
2. <span data-ttu-id="70ea8-118">Update the following three fields for your new app and then click **Continue**:</span><span class="sxs-lookup"><span data-stu-id="70ea8-118">Update the following three fields for your new app and then click **Continue**:</span></span>
   
   * <span data-ttu-id="70ea8-119">**Name**: Type a descriptive name for your app in the **Name** field in the **App ID Description** section.</span><span class="sxs-lookup"><span data-stu-id="70ea8-119">**Name**: Type a descriptive name for your app in the **Name** field in the **App ID Description** section.</span></span>
   * <span data-ttu-id="70ea8-120">**Bundle Identifier**: Under the **Explicit App ID** section, enter a **Bundle Identifier** in the form `<Organization Identifier>.<Product Name>` as mentioned in the [App Distribution Guide](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8).</span><span class="sxs-lookup"><span data-stu-id="70ea8-120">**Bundle Identifier**: Under the **Explicit App ID** section, enter a **Bundle Identifier** in the form `<Organization Identifier>.<Product Name>` as mentioned in the [App Distribution Guide](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8).</span></span> <span data-ttu-id="70ea8-121">The *Organization Identifier* and *Product Name* you use must match the organization identifier and product name you will use when you create your XCode project.</span><span class="sxs-lookup"><span data-stu-id="70ea8-121">The *Organization Identifier* and *Product Name* you use must match the organization identifier and product name you will use when you create your XCode project.</span></span> <span data-ttu-id="70ea8-122">In the screeshot below *NotificationHubs* is used as a organization idenitifier and *GetStarted* is used as the product name.</span><span class="sxs-lookup"><span data-stu-id="70ea8-122">In the screeshot below *NotificationHubs* is used as a organization idenitifier and *GetStarted* is used as the product name.</span></span> <span data-ttu-id="70ea8-123">Making sure this matches the values you will use in your XCode project will allow you to use the correct publishing profile with XCode.</span><span class="sxs-lookup"><span data-stu-id="70ea8-123">Making sure this matches the values you will use in your XCode project will allow you to use the correct publishing profile with XCode.</span></span> 
   * <span data-ttu-id="70ea8-124">**Push Notifications**: Check the **Push Notifications** option in the **App Services** section, .</span><span class="sxs-lookup"><span data-stu-id="70ea8-124">**Push Notifications**: Check the **Push Notifications** option in the **App Services** section, .</span></span>
     
      ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-appid-info.png)
     
      <span data-ttu-id="70ea8-125">This generates your App ID and requests you to confirm the information.</span><span class="sxs-lookup"><span data-stu-id="70ea8-125">This generates your App ID and requests you to confirm the information.</span></span> <span data-ttu-id="70ea8-126">Click **Register** to confirm the new App ID.</span><span class="sxs-lookup"><span data-stu-id="70ea8-126">Click **Register** to confirm the new App ID.</span></span>
     
      <span data-ttu-id="70ea8-127">Once you click **Register**, you will see the **Registration complete** screen, as shown below.</span><span class="sxs-lookup"><span data-stu-id="70ea8-127">Once you click **Register**, you will see the **Registration complete** screen, as shown below.</span></span> <span data-ttu-id="70ea8-128">Click **Done**.</span><span class="sxs-lookup"><span data-stu-id="70ea8-128">Click **Done**.</span></span>
      
      ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-registration-complete.png)


1. <span data-ttu-id="70ea8-129">In the Developer Center, under App IDs, locate the app ID that you just created, and click on its row.</span><span class="sxs-lookup"><span data-stu-id="70ea8-129">In the Developer Center, under App IDs, locate the app ID that you just created, and click on its row.</span></span>
   
      ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids2.png)
   
      <span data-ttu-id="70ea8-130">Clicking on the app ID will display the app details.</span><span class="sxs-lookup"><span data-stu-id="70ea8-130">Clicking on the app ID will display the app details.</span></span> <span data-ttu-id="70ea8-131">Click the **Edit** button at the bottom.</span><span class="sxs-lookup"><span data-stu-id="70ea8-131">Click the **Edit** button at the bottom.</span></span>
   
      ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-enable-apple-push-notifications/notification-hubs-edit-appid.png)
      
2. <span data-ttu-id="70ea8-132">Scroll to the bottom of the screen, and click the **Create Certificate...** button under the section **Development Push SSL Certificate**.</span><span class="sxs-lookup"><span data-stu-id="70ea8-132">Scroll to the bottom of the screen, and click the **Create Certificate...** button under the section **Development Push SSL Certificate**.</span></span>
   
      ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-create-cert.png)
   
      <span data-ttu-id="70ea8-133">This displays the "Add iOS Certificate" assistant.</span><span class="sxs-lookup"><span data-stu-id="70ea8-133">This displays the "Add iOS Certificate" assistant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="70ea8-134">This tutorial uses a development certificate.</span><span class="sxs-lookup"><span data-stu-id="70ea8-134">This tutorial uses a development certificate.</span></span> <span data-ttu-id="70ea8-135">The same process is used when registering a production certificate.</span><span class="sxs-lookup"><span data-stu-id="70ea8-135">The same process is used when registering a production certificate.</span></span> <span data-ttu-id="70ea8-136">Just make sure that you use the same certificate type when sending notifications.</span><span class="sxs-lookup"><span data-stu-id="70ea8-136">Just make sure that you use the same certificate type when sending notifications.</span></span>
   > 
   > 
3. <span data-ttu-id="70ea8-137">Click **Choose File**, browse to the location where you saved the CSR file that you created in the first task, then click **Generate**.</span><span class="sxs-lookup"><span data-stu-id="70ea8-137">Click **Choose File**, browse to the location where you saved the CSR file that you created in the first task, then click **Generate**.</span></span>
   
      ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-cert-choose-csr.png)
4. <span data-ttu-id="70ea8-138">After the certificate is created by the portal, click the **Download** button, and click **Done**.</span><span class="sxs-lookup"><span data-stu-id="70ea8-138">After the certificate is created by the portal, click the **Download** button, and click **Done**.</span></span>
   
      ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-download-cert.png)
   
      <span data-ttu-id="70ea8-139">This downloads the certificate and saves it to your computer in your Downloads folder.</span><span class="sxs-lookup"><span data-stu-id="70ea8-139">This downloads the certificate and saves it to your computer in your Downloads folder.</span></span>
   
      ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-downloaded.png)
   
   > [!NOTE]
   > <span data-ttu-id="70ea8-140">By default, the downloaded file a development certificate is named **aps_development.cer**.</span><span class="sxs-lookup"><span data-stu-id="70ea8-140">By default, the downloaded file a development certificate is named **aps_development.cer**.</span></span>
   > 
   > 
5. <span data-ttu-id="70ea8-141">Double-click the downloaded push certificate **aps_development.cer**.</span><span class="sxs-lookup"><span data-stu-id="70ea8-141">Double-click the downloaded push certificate **aps_development.cer**.</span></span>
   
      <span data-ttu-id="70ea8-142">This installs the new certificate in the Keychain, as shown below:</span><span class="sxs-lookup"><span data-stu-id="70ea8-142">This installs the new certificate in the Keychain, as shown below:</span></span>
   
      ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-in-keychain.png)
   
   > [!NOTE]
   > <span data-ttu-id="70ea8-143">The name in your certificate might be different, but it will be prefixed with **Apple Development iOS Push Services:**.</span><span class="sxs-lookup"><span data-stu-id="70ea8-143">The name in your certificate might be different, but it will be prefixed with **Apple Development iOS Push Services:**.</span></span>
   > 
   > 
6. <span data-ttu-id="70ea8-144">In Keychain Access, right-click the new push certificate that you created in the **Certificates** category.</span><span class="sxs-lookup"><span data-stu-id="70ea8-144">In Keychain Access, right-click the new push certificate that you created in the **Certificates** category.</span></span> <span data-ttu-id="70ea8-145">Click **Export**, name the file, select the **.p12** format, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="70ea8-145">Click **Export**, name the file, select the **.p12** format, and then click **Save**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-enable-apple-push-notifications/notification-hubs-export-cert-p12.png)
   
    <span data-ttu-id="70ea8-146">Make a note of the file name and location of the exported .p12 certificate.</span><span class="sxs-lookup"><span data-stu-id="70ea8-146">Make a note of the file name and location of the exported .p12 certificate.</span></span> <span data-ttu-id="70ea8-147">It will be used to enable authentication with APNS.</span><span class="sxs-lookup"><span data-stu-id="70ea8-147">It will be used to enable authentication with APNS.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="70ea8-148">This tutorial creates a QuickStart.p12 file.</span><span class="sxs-lookup"><span data-stu-id="70ea8-148">This tutorial creates a QuickStart.p12 file.</span></span> <span data-ttu-id="70ea8-149">Your file name and location might be different.</span><span class="sxs-lookup"><span data-stu-id="70ea8-149">Your file name and location might be different.</span></span>
   > 
   > 

## <a name="create-a-provisioning-profile-for-the-app"></a><span data-ttu-id="70ea8-150">Create a provisioning profile for the app</span><span class="sxs-lookup"><span data-stu-id="70ea8-150">Create a provisioning profile for the app</span></span>
1. <span data-ttu-id="70ea8-151">Back in the <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a>, select **Provisioning Profiles**, select **All**, and then click the **+** button to create a new profile.</span><span class="sxs-lookup"><span data-stu-id="70ea8-151">Back in the <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a>, select **Provisioning Profiles**, select **All**, and then click the **+** button to create a new profile.</span></span> <span data-ttu-id="70ea8-152">This launches the **Add iOS Provisiong Profile** Wizard</span><span class="sxs-lookup"><span data-stu-id="70ea8-152">This launches the **Add iOS Provisiong Profile** Wizard</span></span>
   
      ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-provisioning-profile.png)
2. <span data-ttu-id="70ea8-153">Select **iOS App Development** under **Development** as the provisiong profile type, and click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="70ea8-153">Select **iOS App Development** under **Development** as the provisiong profile type, and click **Continue**.</span></span> 
3. <span data-ttu-id="70ea8-154">Next, select the app ID you just created from the **App ID** drop-down list, and click **Continue**</span><span class="sxs-lookup"><span data-stu-id="70ea8-154">Next, select the app ID you just created from the **App ID** drop-down list, and click **Continue**</span></span>
   
      ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-enable-apple-push-notifications/notification-hubs-select-appid-for-provisioning.png)
4. <span data-ttu-id="70ea8-155">In the **Select certificates** screen, select your usual development certificate used for code signing, and click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="70ea8-155">In the **Select certificates** screen, select your usual development certificate used for code signing, and click **Continue**.</span></span> <span data-ttu-id="70ea8-156">This is not the push certificate you just created.</span><span class="sxs-lookup"><span data-stu-id="70ea8-156">This is not the push certificate you just created.</span></span>
   
      ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-cert.png)
5. <span data-ttu-id="70ea8-157">Next, select the **Devices** to use for testing, and click **Continue**</span><span class="sxs-lookup"><span data-stu-id="70ea8-157">Next, select the **Devices** to use for testing, and click **Continue**</span></span>
   
      ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-devices.png)
6. <span data-ttu-id="70ea8-158">Finally, pick a name for the profile in **Profile Name**, click **Generate**.</span><span class="sxs-lookup"><span data-stu-id="70ea8-158">Finally, pick a name for the profile in **Profile Name**, click **Generate**.</span></span>
   
      ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-name-profile.png)
7. <span data-ttu-id="70ea8-159">When the new provisioning profile is created click to download it and install it on your Xcode development machine.</span><span class="sxs-lookup"><span data-stu-id="70ea8-159">When the new provisioning profile is created click to download it and install it on your Xcode development machine.</span></span> <span data-ttu-id="70ea8-160">Then click **Done**.</span><span class="sxs-lookup"><span data-stu-id="70ea8-160">Then click **Done**.</span></span>
   
      ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-profile-ready.png)




















