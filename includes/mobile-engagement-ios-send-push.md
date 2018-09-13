### <a name="grant-access-to-your-push-certificate-to-mobile-engagement"></a><span data-ttu-id="0ddcc-101">Grant access to your Push Certificate to Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="0ddcc-101">Grant access to your Push Certificate to Mobile Engagement</span></span>
<span data-ttu-id="0ddcc-102">To allow Mobile Engagement to send Push Notifications on your behalf, you need to grant it access to your certificate.</span><span class="sxs-lookup"><span data-stu-id="0ddcc-102">To allow Mobile Engagement to send Push Notifications on your behalf, you need to grant it access to your certificate.</span></span> <span data-ttu-id="0ddcc-103">This is done by configuring and entering your certificate into the Mobile Engagement portal.</span><span class="sxs-lookup"><span data-stu-id="0ddcc-103">This is done by configuring and entering your certificate into the Mobile Engagement portal.</span></span> <span data-ttu-id="0ddcc-104">Make sure you obtain your .p12 certificate as explained in [Apple's documentation](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span><span class="sxs-lookup"><span data-stu-id="0ddcc-104">Make sure you obtain your .p12 certificate as explained in [Apple's documentation](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

1. <span data-ttu-id="0ddcc-105">Navigate to your Mobile Engagement portal.</span><span class="sxs-lookup"><span data-stu-id="0ddcc-105">Navigate to your Mobile Engagement portal.</span></span> <span data-ttu-id="0ddcc-106">Ensure you're in the correct and then click on the **Engage** button at the bottom:</span><span class="sxs-lookup"><span data-stu-id="0ddcc-106">Ensure you're in the correct and then click on the **Engage** button at the bottom:</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/mobile-engagement-ios-send-push/engage-button.png)
2. <span data-ttu-id="0ddcc-107">Click on the **Settings** page in your Engagement Portal.</span><span class="sxs-lookup"><span data-stu-id="0ddcc-107">Click on the **Settings** page in your Engagement Portal.</span></span> <span data-ttu-id="0ddcc-108">From there click on the **Native Push** section to upload your p12 certificate:</span><span class="sxs-lookup"><span data-stu-id="0ddcc-108">From there click on the **Native Push** section to upload your p12 certificate:</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/mobile-engagement-ios-send-push/engagement-portal.png)
3. <span data-ttu-id="0ddcc-109">Select your p12, upload it and type your password:</span><span class="sxs-lookup"><span data-stu-id="0ddcc-109">Select your p12, upload it and type your password:</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/mobile-engagement-ios-send-push/native-push-settings.png)

## <a id="send"></a><span data-ttu-id="0ddcc-110">Send a notification to your app</span><span class="sxs-lookup"><span data-stu-id="0ddcc-110">Send a notification to your app</span></span>
<span data-ttu-id="0ddcc-111">We will now create a simple Push Notification campaign that will send a push to our app:</span><span class="sxs-lookup"><span data-stu-id="0ddcc-111">We will now create a simple Push Notification campaign that will send a push to our app:</span></span>

1. <span data-ttu-id="0ddcc-112">Navigate to the **Reach** tab in your Mobile Engagement portal.</span><span class="sxs-lookup"><span data-stu-id="0ddcc-112">Navigate to the **Reach** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="0ddcc-113">Click **New Announcement** to create your push campaign</span><span class="sxs-lookup"><span data-stu-id="0ddcc-113">Click **New Announcement** to create your push campaign</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/mobile-engagement-ios-send-push/new-announcement.png)
3. <span data-ttu-id="0ddcc-114">Setup the first fields of your campaign:</span><span class="sxs-lookup"><span data-stu-id="0ddcc-114">Setup the first fields of your campaign:</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/mobile-engagement-ios-send-push/campaign-first-params.png)
   
   * <span data-ttu-id="0ddcc-115">Provide a **Name** for your campaign</span><span class="sxs-lookup"><span data-stu-id="0ddcc-115">Provide a **Name** for your campaign</span></span> 
   * <span data-ttu-id="0ddcc-116">Select the **Delivery time** as **Out of app only**: this is the simple Apple push notification type that features some text.</span><span class="sxs-lookup"><span data-stu-id="0ddcc-116">Select the **Delivery time** as **Out of app only**: this is the simple Apple push notification type that features some text.</span></span>
   * <span data-ttu-id="0ddcc-117">In the notification text, type first the **Title** which will be the first line in the push.</span><span class="sxs-lookup"><span data-stu-id="0ddcc-117">In the notification text, type first the **Title** which will be the first line in the push.</span></span>
   * <span data-ttu-id="0ddcc-118">Then type your **Message** which will be the second line</span><span class="sxs-lookup"><span data-stu-id="0ddcc-118">Then type your **Message** which will be the second line</span></span>
4. <span data-ttu-id="0ddcc-119">Scroll down, and in the content section select **Notification only**</span><span class="sxs-lookup"><span data-stu-id="0ddcc-119">Scroll down, and in the content section select **Notification only**</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/mobile-engagement-ios-send-push/campaign-content.png)
5. <span data-ttu-id="0ddcc-120">You're done setting the most basic campaign.</span><span class="sxs-lookup"><span data-stu-id="0ddcc-120">You're done setting the most basic campaign.</span></span> <span data-ttu-id="0ddcc-121">Now scroll down and click on **Create** button to save your push notification campaign.</span><span class="sxs-lookup"><span data-stu-id="0ddcc-121">Now scroll down and click on **Create** button to save your push notification campaign.</span></span> 
6. <span data-ttu-id="0ddcc-122">Finally - click on **Activate** to send push notification.</span><span class="sxs-lookup"><span data-stu-id="0ddcc-122">Finally - click on **Activate** to send push notification.</span></span> 
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/mobile-engagement-ios-send-push/campaign-activate.png)
7. <span data-ttu-id="0ddcc-123">You will be able receive the notification on your iOS device in the notification center like the following:</span><span class="sxs-lookup"><span data-stu-id="0ddcc-123">You will be able receive the notification on your iOS device in the notification center like the following:</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/mobile-engagement-ios-send-push/iphone-notification.png)
8. <span data-ttu-id="0ddcc-124">If you have an Apple Watch paired with this iOS device then you will see the notification on your Apple Watch:</span><span class="sxs-lookup"><span data-stu-id="0ddcc-124">If you have an Apple Watch paired with this iOS device then you will see the notification on your Apple Watch:</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/mobile-engagement-ios-send-push/apple-watch.png)










