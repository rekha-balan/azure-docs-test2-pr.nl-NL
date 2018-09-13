
1. <span data-ttu-id="a5fd1-101">Navigate to the [Google Cloud Console](https://console.developers.google.com/project), sign in with your Google account credentials.</span><span class="sxs-lookup"><span data-stu-id="a5fd1-101">Navigate to the [Google Cloud Console](https://console.developers.google.com/project), sign in with your Google account credentials.</span></span> 
2. <span data-ttu-id="a5fd1-102">Click **Create Project**, type a project name, then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a5fd1-102">Click **Create Project**, type a project name, then click **Create**.</span></span> <span data-ttu-id="a5fd1-103">If requested, carry out the SMS Verification, and click **Create** again.</span><span class="sxs-lookup"><span data-stu-id="a5fd1-103">If requested, carry out the SMS Verification, and click **Create** again.</span></span>
   
    ![Create new project](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/mobile-services-enable-google-cloud-messaging/mobile-services-google-new-project.png)   
   
     <span data-ttu-id="a5fd1-105">Type in your new **Project name** and click **Create project**.</span><span class="sxs-lookup"><span data-stu-id="a5fd1-105">Type in your new **Project name** and click **Create project**.</span></span>
3. <span data-ttu-id="a5fd1-106">Click the **Utilities and More** button and then click **Project Information**.</span><span class="sxs-lookup"><span data-stu-id="a5fd1-106">Click the **Utilities and More** button and then click **Project Information**.</span></span> <span data-ttu-id="a5fd1-107">Make a note of the **Project Number**.</span><span class="sxs-lookup"><span data-stu-id="a5fd1-107">Make a note of the **Project Number**.</span></span> <span data-ttu-id="a5fd1-108">You will need to set this value as the `SenderId` variable in the client app.</span><span class="sxs-lookup"><span data-stu-id="a5fd1-108">You will need to set this value as the `SenderId` variable in the client app.</span></span>
   
    ![Utilites and more](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/mobile-services-enable-google-cloud-messaging/notification-hubs-utilities-and-more.png)
4. <span data-ttu-id="a5fd1-110">In the project dashboard, under **Mobile APIs**, click **Google Cloud Messaging**, then on the next page click **Enable API** and accept the terms of service.</span><span class="sxs-lookup"><span data-stu-id="a5fd1-110">In the project dashboard, under **Mobile APIs**, click **Google Cloud Messaging**, then on the next page click **Enable API** and accept the terms of service.</span></span> 
   
    ![Enabling GCM](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/mobile-services-enable-google-cloud-messaging/enable-GCM.png)
   
    ![Enabling GCM](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/mobile-services-enable-google-cloud-messaging/enable-gcm-2.png) 
5. <span data-ttu-id="a5fd1-113">In the project dashboard, Click **Credentials** > **Create Credential** > **API Key**.</span><span class="sxs-lookup"><span data-stu-id="a5fd1-113">In the project dashboard, Click **Credentials** > **Create Credential** > **API Key**.</span></span> 
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/mobile-services-enable-google-cloud-messaging/mobile-services-google-create-server-key.png)
6. <span data-ttu-id="a5fd1-114">In **Create a new key**, click **Server key**, type a name for your key, then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a5fd1-114">In **Create a new key**, click **Server key**, type a name for your key, then click **Create**.</span></span>
7. <span data-ttu-id="a5fd1-115">Make a note of the **API KEY** value.</span><span class="sxs-lookup"><span data-stu-id="a5fd1-115">Make a note of the **API KEY** value.</span></span>
   
    <span data-ttu-id="a5fd1-116">You will use this API key value to enable Azure to authenticate with GCM and send push notifications on behalf of your app.</span><span class="sxs-lookup"><span data-stu-id="a5fd1-116">You will use this API key value to enable Azure to authenticate with GCM and send push notifications on behalf of your app.</span></span>






