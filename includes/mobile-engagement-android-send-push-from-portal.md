### <a name="grant-mobile-engagement-access-to-your-gcm-api-key"></a><span data-ttu-id="e679b-101">Grant Mobile Engagement access to your GCM API Key</span><span class="sxs-lookup"><span data-stu-id="e679b-101">Grant Mobile Engagement access to your GCM API Key</span></span>
<span data-ttu-id="e679b-102">To allow Mobile Engagement to send push notifications on your behalf, you need to grant it access to your API Key.</span><span class="sxs-lookup"><span data-stu-id="e679b-102">To allow Mobile Engagement to send push notifications on your behalf, you need to grant it access to your API Key.</span></span> <span data-ttu-id="e679b-103">This is done by configuring and entering your key into the Mobile Engagement portal.</span><span class="sxs-lookup"><span data-stu-id="e679b-103">This is done by configuring and entering your key into the Mobile Engagement portal.</span></span>

1. <span data-ttu-id="e679b-104">From your Azure Classic Portal, ensure you're in the app we're using for this project, and then click the **Engage** button at the bottom:</span><span class="sxs-lookup"><span data-stu-id="e679b-104">From your Azure Classic Portal, ensure you're in the app we're using for this project, and then click the **Engage** button at the bottom:</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/mobile-engagement-android-send-push/engage-button.png)
2. <span data-ttu-id="e679b-105">Then click the **Settings** -> **Native Push** section to enter your GCM Key:</span><span class="sxs-lookup"><span data-stu-id="e679b-105">Then click the **Settings** -> **Native Push** section to enter your GCM Key:</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/mobile-engagement-android-send-push/engagement-portal.png)
3. <span data-ttu-id="e679b-106">Click the **Edit** icon in front of **API Key** in the **GCM Settings** section as shown below:</span><span class="sxs-lookup"><span data-stu-id="e679b-106">Click the **Edit** icon in front of **API Key** in the **GCM Settings** section as shown below:</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/mobile-engagement-android-send-push/native-push-settings.png)
4. <span data-ttu-id="e679b-107">In the pop-up, paste the GCM Server Key you obtained before and then click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="e679b-107">In the pop-up, paste the GCM Server Key you obtained before and then click **Ok**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/mobile-engagement-android-send-push/api-key.png)

## <a id="send"></a><span data-ttu-id="e679b-108">Send a notification to your app</span><span class="sxs-lookup"><span data-stu-id="e679b-108">Send a notification to your app</span></span>
<span data-ttu-id="e679b-109">We will now create a simple push notification campaign that sends a push notification to our app.</span><span class="sxs-lookup"><span data-stu-id="e679b-109">We will now create a simple push notification campaign that sends a push notification to our app.</span></span>

1. <span data-ttu-id="e679b-110">Navigate to the **REACH** tab in your Mobile Engagement portal.</span><span class="sxs-lookup"><span data-stu-id="e679b-110">Navigate to the **REACH** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="e679b-111">Click **New announcement** to create your push notification campaign.</span><span class="sxs-lookup"><span data-stu-id="e679b-111">Click **New announcement** to create your push notification campaign.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/mobile-engagement-android-send-push/new-announcement.png)
3. <span data-ttu-id="e679b-112">Set up the first field of your campaign through the following steps:</span><span class="sxs-lookup"><span data-stu-id="e679b-112">Set up the first field of your campaign through the following steps:</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/mobile-engagement-android-send-push/campaign-first-params.png)
   
    <span data-ttu-id="e679b-113">a.</span><span class="sxs-lookup"><span data-stu-id="e679b-113">a.</span></span> <span data-ttu-id="e679b-114">Name your campaign.</span><span class="sxs-lookup"><span data-stu-id="e679b-114">Name your campaign.</span></span>
   
    <span data-ttu-id="e679b-115">b.</span><span class="sxs-lookup"><span data-stu-id="e679b-115">b.</span></span> <span data-ttu-id="e679b-116">Select the **Delivery type** as *System notification -> Simple*: This is the simple Android push notification type that features a title and a small line of text.</span><span class="sxs-lookup"><span data-stu-id="e679b-116">Select the **Delivery type** as *System notification -> Simple*: This is the simple Android push notification type that features a title and a small line of text.</span></span>
   
    <span data-ttu-id="e679b-117">c.</span><span class="sxs-lookup"><span data-stu-id="e679b-117">c.</span></span> <span data-ttu-id="e679b-118">Select **Delivery time** as *Any time* to allow the app to receive a notification whether the app is started or not.</span><span class="sxs-lookup"><span data-stu-id="e679b-118">Select **Delivery time** as *Any time* to allow the app to receive a notification whether the app is started or not.</span></span>
   
    <span data-ttu-id="e679b-119">d.</span><span class="sxs-lookup"><span data-stu-id="e679b-119">d.</span></span> <span data-ttu-id="e679b-120">In the notification text type the **Title** which will be in bold in the push.</span><span class="sxs-lookup"><span data-stu-id="e679b-120">In the notification text type the **Title** which will be in bold in the push.</span></span>
   
    <span data-ttu-id="e679b-121">e.</span><span class="sxs-lookup"><span data-stu-id="e679b-121">e.</span></span> <span data-ttu-id="e679b-122">Then type your **Message**</span><span class="sxs-lookup"><span data-stu-id="e679b-122">Then type your **Message**</span></span>
4. <span data-ttu-id="e679b-123">Scroll down, and in the **Content** section, select **Notification only**.</span><span class="sxs-lookup"><span data-stu-id="e679b-123">Scroll down, and in the **Content** section, select **Notification only**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/mobile-engagement-android-send-push/campaign-content.png)
5. <span data-ttu-id="e679b-124">You're done setting the most basic campaign possible.</span><span class="sxs-lookup"><span data-stu-id="e679b-124">You're done setting the most basic campaign possible.</span></span> <span data-ttu-id="e679b-125">Now scroll down again and click the **Create** button to save your campaign.</span><span class="sxs-lookup"><span data-stu-id="e679b-125">Now scroll down again and click the **Create** button to save your campaign.</span></span>
6. <span data-ttu-id="e679b-126">Last step: click **Activate** to activate your campaign to send push notifications.</span><span class="sxs-lookup"><span data-stu-id="e679b-126">Last step: click **Activate** to activate your campaign to send push notifications.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/mobile-engagement-android-send-push/campaign-activate.png)









